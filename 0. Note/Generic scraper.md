---
tags:
  - note
Project:
  - "[[1. Projects/Generic scraper|Generic scraper]]"
Status: In progress
---
# Functionality
- [x] Take a list of urls in (json/csv) format.
- [x] Verify all urls are valid
	- [x] If not prompt user that XYZ are not valid urls?
- [x] Define data in form of pydantic models to specify data requirements
- [x] Fetch a response from each url
- [ ] Make sure the request isn't too long.
- [x] Send response to GPT for processing
- [x] Store results somehow
- [ ] Output results into CSV format
- [ ] Refine error handling in get_responses to give more information about the error.
- [ ] Figure out how to flatten list of output so tinydb doesn't have so many rows per scrape.
- [ ] Front end for submitting data format
- [ ] Building data format with said information
	- [ ] Dict that has main construct as the first key
	- [ ] Make it a list of tuples
		- [ ] #(key, type, value(s), optional, Many)
		- [ ] Above will depend on the type (so type must come from a drop down)
		- [ ] Ability to add multiple clusters of data so that we can just use #(products, DefinedType, optional, many)

# Storing results
I think some kind of sqlite database could be good? The question is how would I create the schema?
I guess it could be derived from the pydantic models at the "build" stage?
Take the relationship types derived from if the value is a list etc.
and use these to create the schema. We have typing and optionality defined by default. This may actually be pretty easy.
Thinking about this more, SQL would be annoying maybe just json or some nosql sqlite equivalent.
I think TinyDb looks like a good solution for this (mongo but sqlite).
I think we want to use some kind of name or hash for the scrapes so that we can keep everything synced up and queried separately. These need to be exposed to the user though.

# Error handling
Json errors: User could provide invalid json or json that does not fit the requirements. This will need to be verified at start.

Url verification: Say the url is missing some key component, we could flag this before requests are made and specify which urls are the problematic ones.

Pydantic model: These could be improperly formatted, I suppose I just need to verify that the final container exists.

Response errors: Any given url could return a non-200 status code. IF this happens I think this is important information and should be stored somewhere and provided to the user so they know that some information was missed.

Cloudflare or other blocks: Need some way to detect if the page is some kind of bot detection layer and bring that up to the user. 

Token length: need to ensure that the message being sent to open AI isn't too long. Requires tiktoken-ing the entire text. Once done I can then measure the length of the system prompt from pydantic as well as the html then apply some sort of trimming.

ChatGPT errors: I suppose these are mainly internal, warrant some kind of retry mechanism. If too many retries give up and tell user X url was missed. 

Database errors: If the user provides a scrape name that doesn't exist we need to tell them this and maybe list out the existing scrape names so that they can pick one of those instead.

Output to CSV: There could be formatting issues, but hopefully not. I suppose the main thing would be how do we construct it given an open schema?