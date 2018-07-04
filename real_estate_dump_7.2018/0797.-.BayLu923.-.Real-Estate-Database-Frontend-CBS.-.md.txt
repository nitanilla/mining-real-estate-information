#Project objective
Help transaction database users identify investors in real estate market. Real estate investors play a significant role in housing market crisis and real estate cycle. Real estate individual investors are generally wealthy individuals who evaluate the real estate market and purchase property to build long-term wealth. Institutional investors are companies that make substantial investments in securities, properties, and other investment assets.(i.e. JP Morgan, BOA) 

It's important to know who are the investors in real estate market and make them under supervision and regulation. However, investors tend to hide themself because they want to protect them from regulations and counterparties. Public information will provide others with a roadmap to investors' identity, assets and strategy. The algorithm is used to scoring investor propensity in real estate market. With data of transaction record in each county, the algorithm will output score on probability for every person or institution appeared in the transaction record data.

#Data input
Transaction records of all counties in US: items including buyer, Seller, Property Id, Unique ID, Site Address, Mailing Address, Transaction Type (Loan or Purchase), Transaction Date, Loan Type, Transaction Amount, Loan Amount, …etc.

#Algorithm
The algorithm includes 4 parts to assign investor propensity scores:
#1. Max number of houses owned at once
Maximum # of properties each person/instituion owns on one day. Th more properties a person/instituion holds per day, the higher the probability this person/instituion may be an investor.
#2. Number of transactions with institutions in these categories: LLC/TRUST/CORP 
Investors register LLC/ TRUST/ HOLDINGS, transact properties to them and use them as intermediaries to make transactions for them. High # of transactions with specific intermediaries may indicate who are behind those intermediaries. The score is calculated based on 2 Benchmarks: 
1) # of transactions with intermediaries
2) Max # of transactions with specific intermediary
#3. Site and mailing address comparison
If a property was sold to a person with a different mailing address than the property address, it indicates that this person is an investor or second-home buyer. If this case happens to a person multiple times, than this person has a higher probability to be an investor.
#4. Average holding time of properties
We want to identify investors making continuous revenue off real estate, not individuals who ‘flip’ houses. Flippers maybe an manager in real estate broker who  Each person’s average holding time of all their properties is calculated with buy date and sell date.

