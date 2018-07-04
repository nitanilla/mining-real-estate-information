Real Estate Wizard® v1.0 Cyken Co.™ 
----------

Program Features
-------------------------------------------------------------------------------------------------------------------------------------------------------
Real Estate Wizard is basicly a estate sharing program where every user could share and see
estates. It allows people to communicate with estate owners, examine the present ads and 
filtering in a detailed way

A new feature arises!
REW comes with the feature called "Event-Focused Search". People could directly chose the 
estate for short term loaning by the event which they want to do in that estate. Program 
analyzes houses, offices and lands, and shows the suitable ones for the user. For instance,
to make a birthday party, house should contain some tools, should be near to the supermarket
and many other features are considered in that search style. 

Put ads with different features at the same time with component/entity system!
You can put your estate for both loan and sale at the same time

Communicate with the sellers by REW!
People can directly send a message to the seller while looking the estate ad. Simply quick..

See the locations of estates via Google Maps!

Sort and filter estates however you want!

And many others... 

To Run the Program
-------------------------------------------------------------------------------------------------------------------------------------------------------
Just run the RealEstate.jar file to run the program
Also just for the version v1.0, you need to setup the xampp to run the program to use database

Minimum System Requirements
-------------------------------------------------------------------------------------------------------------------------------------------------------
2.0 Ghz Processor
512 MB RAM 
256 MB V-RAM
50 MB Storage Space
10 Mbps Internet Connection

Technique Information
-------------------------------------------------------------------------------------------------------------------------------------------------------
We seperate the program into 3 parts:
1-Database
2-GUI(View)
3-Model Classes

In database part, we used MYSQL and Notepad. In MYSQL part we stored almost all informartion
about our program; house details, user details, pictures and all of them except the
conversation details. Conversation Details stored in notepad file with the ObjectOutputStream
class write and read methods. Our MYSQL table design could be seen in slides. 

In GUI part, we used JavaFX. We choose it rather than java.swing and java.awt because its 
graphical tools are much better than them. We create 2 classses for every frame; one is
controller, other one is fxml files. 

Model classes were shown in slides. Names of them:
-RealEstate: abstract class for house office and land
-House: represents houses
-Office: represents offices
-Land: represent lands
-User: contains features of User; name,surname,etc..
-Message: message object with text, date, sender and receiver
-Conversation: contains message list
-Wizard: contains some methods that are used in program
-Component: Component ArrayList system enables us to put ads sale, longtermloan and shorttermloan
at the same time
-Sale: sale component
-LongTermLoan: longtermloan component
-ShortTermLoan: shorttermloan component

About Us
-------------------------------------------------------------------------------------------------------------------------------------------------------
We are Computer Science students at Bilkent University. This is the project assingment of
the course CS-102 Algorithms and Programming. We founded Cyken Co. in 2016. 
Kerem Ayöz:  		keremayoz@hotmail.com
Emre Sülün:  		emresulun93@gmail.com
Yasin Balcancý: 	ybalcanci@gmail.com
Nurefþan Müsevitoðlu: 	musevitoglunurefsan@gmail.com