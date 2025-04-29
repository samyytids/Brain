---
tags:
  - note
Project:
  - "[[Gleam bolt]]"
Status: In progress
---
# General
- [ ] Restart in new repo.
- [ ] Really pay attention to using git.
- [ ] Think about how my output will be used with bolt message types (HELLO).
- [ ] I want to do this during my lunch breaks, just a chill slow dev no pressure.
# Functionality
- [ ] Get marker
- [ ] Remove marker
- [ ] Based on marker process data
	- [ ] Get n required bytes
	- [ ] parse bytes into data
	- [ ] OR just create value from marker
- [ ] Recursively call until array is empty
- [ ] Error handling
- [ ] BoltType (I confirmed this is valid by looking at rust_bolt)
# Error handling
Get marker: I don't think this will need error handling, I can make use of a let assert here as this will only be called if bit array's byte size is >= 1.

Remove marker: Will only be called if the above is called so *should* never error.

Based on marker: Marker could not be a valid marker. If so we need to error out.

Get n required bytes: If the number of bytes isn't available we need to error out.

Parse bytes into data: Data could be ill formatted (think the utf8 stuff). Could add a proper format check to give better errors here. 

## Error handling thoughts
I think the main things that need to be included in the errors are. 
- What caused the error (see above).
- Where the error was caused.
	- This could either be a singular byte
	- OR a selection of bytes depending on the cause
- The bytes that caused the error.

Example:
"Invalid marker byte: 0xCF at position 5"
"Data could not be parsed into type: Int8 at position 6-9, expected valid int instead got 0x12 0x12 0x12"

I might have a look at lustre's source code to get an idea of error handling practices?