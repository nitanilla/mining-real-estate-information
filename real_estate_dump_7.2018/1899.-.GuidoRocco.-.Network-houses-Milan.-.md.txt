# Network-houses-Milan



> Network Houses Milan is a business network that implements a Blockchain than can instantly and safely manage 
transaction of houses. The underlying idea is to simplify and optimize the sales and buying process 
of houses in the city of Milan. 
The model file (.cto) contains, in a JSON-style format, all the necessary information in order to run 
the aforementioned business network. 

Such network is composed by: 


**Participants**

`Owners` 

The owners are citizen of Milan that have/don't have a house. Every owner is identified with an ID, that can be 
for example a hash that univocally identifies the person. Every identity has then a Social Security Number 
(Codice Fiscale in italian), the first name and the last name. A saldo and a monthly wage model the capacity 
of the person of buying/selling properties. 

In order to guarantee the correct functioning of the blockchain, it is necessary to implement a fictional owner 
with id 2000. This owner represents all the owners who are not citizen (in our case, banks and real estate 
agencies). 

`Banks` 

The business network contains the most important italian banks that operate in Milan, such as 
Intesa San Paolo, BPM and Deutsche Bank. 
In the business network, we suppose that the banks have an unlimited saldo (it is, in fact, unoptimal 
to implement a saldo that will contain a large integer, since we will have problems in the integer 
representation). 


`Estate Agencies` 

The estate agencies mediate between owners in buying/selling properties. Every estate agency 
has a list that contains the ids of the houses that they own. 
In the case of a purchase, the estate agency takes the 5% of the selling price as a commission. 

**Assets** 

`Properties` 

A property can be an apartment, a house or a commercial property (bar, shop, enterprise, etc.), legally registered 
in the municipality of Milan. 

**Transactions** 

`Buy` 

The Buy transaction models the purchase of a property that is legally owned by a participant. The purchase 
happens with the transfer of money between the saldos of the two owners. We suppose that taxes are included 
in the final price. 

`Buy with Agency` 

The transaction Buy can also happen with an estate agency. The owner buys, in this case, the property directly 
from the estate agency. The selling price does not include the commission of the agency, that will be computed 
as the 5% of the selling price of the property at the moment of the purchase. 
Then, the ownership of the property passes to the new owner. 

`Loan` 

The Loan transaction happens between an owner and a bank. A smart contract implemented in the blockchain 
controls that the monthly sum of the loan does not surpass the 33% of the monthly wage of the owner: in this case, 
the transaction is automatically rejected. 
In the loan monthly sum taxes must be included. 

`Add House` 

The transaction Add House can be made from the Municipality or from the estate agencies. The result of the transaction 
is the adding of a property in the registry of the estate agency's owned houses. 

`Remove House` 

The transaction Remove House can be made from the Mairy or from the estate agencies. The result of the transaction 
is the removal of a property in the registry of the estate agency's owned houses. 

`Transfer House` 

The transaction Transfer House models the transfer of a house between two estate agencies. 

`Sell to Agency`

The transaction Sell to Agency models the sale of a house from an owner to a real estate agency. 

**Rules** 

A file .acl manages the permissions of the Blockchain by specifying who can do/not do some actions 
(read, create, update and delete data). 

**Queries** 

A query file (.qry) defines the queries of the blockchain. A legend is given in the file. 

