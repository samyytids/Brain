---
tags:
  - note
Project:
  - "[[Epc paper]]"
Status: Finished
Url: https://www.huangchristine.com/assets/files/ChristineZH_utd_jmp.pdf
---
# Thoughts on how to achieve KNN
I have no idea how you would construct this dataset. Without having N rows of the same house with a separate identifier for which circle it is in. I don't know if I have the compute power for this?

# Abstract
They find that properties that have another property within 0.1 miles that engages in green upgrades are more likely to also upgrade their property.

# Introduction
Residential properties make up a lot of green house gasses. 
- EPA, 2024, Inventory of U.S. greenhouse gas emissions and sinks: 1990-2022. https://www.epa.gov/system/files/documents/2024-04/us-ghg-inventory-2024-main-text_04-18-2024.pdf

These upgrades have benefits and incentives beyond GHG emission reductions
- Dodge Data & Analytics, 2020, Green single family and multifamily homes 2020, https://proddrupalcontent.construction.com/s3fs-public/2020-Green-Homes-SmartMarket-Brief-16Jan.pdf

Peer networks have been shown to be important in a variety of contexts
- Maturana and Nickerson (2019), McCartney and Shah (2022), Gupta (2019)), property invest-ments (Bayer, Mangum, and Roberts (2021), Bailey et al. (2018)), and consumption (Bailey et al. (2022))

In general, the idea is that finding information about these green investments can be difficult and as such having a neighbour that has already made one of these investments makes them a valuable resource to other people in the same area. This results in an increased likelihood of investing in green stuff since you have someone to talk to that has already done it. ==(Could be interesting to see if this is something that occurs more strongly in rural areas than in urban areas, IE I have never ever spoken to my neighbours but my Dad has.)== ==They do a more specific look at this by using owner occupied property dense neighbourhoods as being more likely to have closer ties to their communities than renter dense areas. We can also make use of this specification!==

Evidence for lack of adoption due to lack of information.
- Matisoff, Noonan, and Flowers (2016), Howarth and Andersson (1993), and Ramos et al. (2015) and Giraudet (2020).

Evidence regarding uncertainty of requirements/benefits.
- (CEC (2008)

Model choice basis, theoretical basis
- Brock and Durlauf (2001)

Model choice basis, empirical basis (definite read)
Using nearest neighbour design we can gain causal inference.
Basic principle is looking at tight clusters of properties, they also use looser specs using 0.1, 0.3 and 0.5 mile blocks. It seems that the general principle is to use the outer rings as a comparison jump (RDD all over again). To show a causal impact of local neighbours on each other. Think I may talk to my next door neighbour but I probably don't talk to the guy 0.9 miles from my house.
- Bayer, Mangum, and Roberts (2021), Bayer et al. (2022), McCartney and Shah (2022), and McCartney, Orellana-Li, and Zhang (2024).

Empirical validation of confounding neighbourhood confounds.
- (Manski (1993))

Empirical validation of demographic characteristics being relatively stable at close distances
- Bayer, Mangum, and Roberts (2021))

Green investments generally offer negative returns, this paper however disagrees. We potentially also disagree. 
- Fowlie, Greenstone, and Wolfram (2018)

They use a green certification as a marker of whether a property has made green investments, we have a much easier specification since we can measure them directly. They measure exposure of a focal household to be the quarterly rolling sum over the past four quarters of the number of households within a distance threshold that have newly gained green certifications. ==I suppose we could use a count of the number of properties that have made an investment. ==

==Robustness checks include adding in ZIP code and temporal fixed effects as well as a slue of property and neighbourhood characteristics.==

They find that the information sharing effect is most potent when the number of investments in the area is low. IE once the first person does it the impact is huge and as the number of people making the same investment increases the impact diminishes. ==It may be worth looking at a non flattened spec to see if specific investments being made is the most important part or if any investment leads to an increase in any other kind of investment.== Paper finds this is the case (similar rather than exact, so maybe we want to do some aggregation as well.)

They also add a test where they use multi-property owners as a way of showing the the impact is from neighbours and not other effects. Basically if a property they own experiences the peer effect this will leak into their properties that exist far away from the property that experienced the effect. Showing that it is caused by learning and not some other effect. 

==They show a more impactful peer effect in areas where green properties see above median price appreciation. We could also do this!==

They find that financial benefits are the primary drivers of probability over a general preference for being green ==(they measure this using measures like electric car usage and climate opinions per area. These don't significantly vary between high and low investment areas, but places that do experience it the most do have high price benefits from these investments.)==

They use this method to show policy implications, for example that policy implementations should consider the factors outlined above to get the best bang for their buck.

Papers talking about the peer effect in different contexts
- Hong, Kubik, and Stein (2004), Brown et al. (2008)), property investment (Bayer, Mangum, and Roberts (2021), Bailey et al. (2018)), refinancing (Maturana and Nickerson (2019), McCartney and Shah (2022)), mortgage repayments (Gupta (2019)), and consumption (Bailey et al. (2022))

Papers talking about the peer effect in more similar contexts
- (Bollinger and Gillingham (2012), Graziano and Gillingham (2015), Rode and Müller (2021), Bigler and Janzen (2023), Bollinger, Burkhardt, and Gillingham (2020))

Papers on home improvements
- (Montgomery (1992), Choi, Hong, and Scheinkman (2014), Melzer (2017))

Similar paper but in an institutional context
- Qiu, Yin, and Wang (2016)

Similar papers on environmental influences in other decisions
- (Anderson and Robinson (2019)), investment portfolio (Choi, Gao, and Jiang (2020), Fisman et al. (2023), Ilhan (2020)), and consumption (Gargano and Rossi (2024))

Papers on pro env vs financial motives. ==In absence of data on ROI from EPC invesments from the paper we can look at how much the investments that have been made impact on the selling price as a way of measuring the return?==
- (Riedl and Smeets (2017), Hartzmark and Sussman (2019), Barber, Morse, and Yasuda (2021), Bauer, Ruof, and Smeets (2021), Giglio et al. (2025))

# Theoretical framework
Outlining the theoretical basis for why this works.
- Households have a decision to make on whether they invest
- Household utility = payoff from investing minus the cost of investing
- Payoff is simple and assumed to be linear
- Cost has 2 aspects
	- Physical (literal) cost of adoption
	- Information gathering costs
		- Cost of finding out about the investment (decreased by more neighbours having sunk the cost)
		- (Xiong, Payne, and Kinsella (2016), Rogers, Singhal, and Quinlan (2014))
		- Cost of obtaining idiosyncratic information, IE whether they/their house is explicitly eligible for the investment

# Institutional background
Link to US version of EPC
==I should probably reference what an EPC is as well then. They also mention things like the coverage of the certification systems. I suppose we would also want to do this too.==
- (Department of Energy (2010))

# Data
==They have a measure for climate opinion derived from a survey, this might be an interesting control if I can find one==
- (Howe et al. (2015)

# Empirical research design
They mention 2 confounds: 
- Non-random assignment (pick house based on income and social group).
- Local shocks may lead to collective decision making rather than the peer effect (think a flood making people invest in flood prevention).

See [[Green Neighbors, Greener Neighborhoods Peer Effects in Residential Green Investments#Introduction|the third block in introduction]] which lists the references they use for how they avoid these confounds. ==The basic approach is to us the decisions of hyper local neighbours while controlling for the decisions of more distant neighbours==. 
The logic being that the reason that people live 0.1 miles away from one another instead of 0.3 miles away from one another is quasi random.
Which is backed up by the fact that demographics are usually very uniform at this level so there is no reason to assume any kind of strategic sorting at that level of closeness. 
Further backed up by the fact that people are limited by the thinness of sales in small areas, IE only so many houses will be for sale in a 0.3 mile area so people cannot perfectly select for certain locations. 

==They show a measurement of similarity in the A. Property Characteristics Similarity section, this is used to show that the areas are similar beyond just the fact that they are close to one another==. The best I can do here is to use the total floor area, type of property and the lod. Maybe I could also add in some of the EPC stuff? To get an idea of similarity? ==Ask Danny==

==They show a jump in exposure at the hyper close specification.==

## Regression specification 
Y = an arbitrary value assigned based on who made the investments first.
This is set to 10,000 for the first person that makes an investment in the area. 
They include controls for all three of the exposure rings, interpretation is that each ring shows the additional effect of being in that specific ring (since all controls are cumulative).
They also include some basic controls for property and location characteristics. 

# Results
Blah blah blah
