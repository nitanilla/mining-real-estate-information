# Real-Estate
Purpose
Inheritance and polymorphism can be used to model many real-world environments. In this lab you will use these features to efficiently model a simple set of real estate objects. In contrast with other labs there is not much computation in this lab. The primary task here is to organize the data needed to represent real estate objects, in particular properties and the associated taxes.
Key Reading
•	10.1-10.4
•	Frequently Asked Questions
Requirement
•	You are required to attend a help session before requesting personal TA help.  Please refer to the TA schedule for help session times/location.
Background
In this lab, you will compute the taxes due on a set of properties described in a data file.  You will design a main function to prompt the user to enter the location of the data file.  Based on the data in the file you will add properties to a vector of property pointers. Once you have read in the data you will display it and then produce a summary of the taxes due.
You will create a Main.cpp and also create classes with corresponding .h and .cpp files to represent the various types of real estate properties. You must create a base class for a generic real estate property and derived classes for specific types of real estate. You will be graded in part based on your use of inheritance to efficiently model the data in this application.
Part 1 – Base class for real estate (8 points)
After creating a Main program, create a .h and .cpp for the base real estate Property class.
•	You should have a Main.cpp file that contains your main function and code that creates new Property objects.
•	Create a very simple Property class. It must contain at least an address member and a toString( ) function to render it as a string.
•	Prompt the user for a file of property data.
•	Read in the property data, create corresponding Property object pointers, and put them in a vector of Property*. Note that for this step you may ignore all of the data in the file except the address.
The file will include lines that look like this for residential properties:
Residential 1 200000 1 42 Iris Way
“Residential” is a tag that marks the line as information about a residential property, “1” indicates that the property is a rental (it would have been “0” if not a rental), “200000” is the value of the property, the second “1” indicates that it is occupied (not vacant), and “42 Iris Way” is the address.
A commercial property will have a line that looks like:
Commercial 0 1234567 1 0.20 350 Sea Towers
“Commercial” indicates that it is commercial, “0” indicates that it is not a rental, “1234567” is the value, “1” indicates that its taxes are discounted, and “0.20” is the discount rate, meaning taxes are paid on only 80% of its value. The rest of the line “350 Sea Towers” is the address. The discount rate will always be present, even if no tax discount applies.
•	Display the list of Property objects. For now that can just be the addresses, so it might look like:
42 Iris Way
350 Sea Towers
Note that you do not need to demonstrate this simple version to the TA if you have completed the more complete version described below.
Part 2 - Create sub classes (10 points)
•	Before proceeding, note that from this point forward you will not be directly using the Property class you created in Part 1. You will use it only as an abstract base class.
•	Make two subclasses, one for each type of property (Residential and Commercial). Each class should have a .h and a .cpp.
•	Add data members for each field described in Part 1. For example: the address, the bool that indicates whether a property is a rental, etc. You are expected to use good judgment by putting the data members in the correct classes. Any common data must be in the base Property class. Information, such as the Discount Rate, which applies only to Commercial properties, should go in the Commercial class.
•	In addition to the data provided in the file, each property must be given a unique integer ID starting at 0.
•	All data members must be private or protected. Values of data members should be set by a constructor. All classes must have a toString( ) function which produces a string representing all of the data related to the property.
•	Adjust your main program so that the data is read in from the file and is loaded into the appropriate types of objects.
•	Your main function should still display the data related to the properties, but now the output should look like:
All valid properties:
Property id: 0  Address:  42 Iris way  Rental  Estimated value: 200000 occupied
Property id: 1  Address:  350 Sea Towers      NOT rental      Estimated value: 1.23457e+006   Discounted     Discount 0.2
If it is not discounted, just say “Not discounted” without the discount rate. In case you are curious, 1234567 was written, by C++ in scientific notation, 1.23457e+006, by default. You need not do any special formatting of numbers.
Part 3 – Compute taxes (10 points)
•	The Property classes must include functions to compute taxes as follows:
o	For commercial rental properties the rate is 0.012 (1.2%). For non-rental commercial properties it is 0.01 (1%). Also, taxes on commercial properties may be discounted in accordance with the specified amount.
o	For residential properties the rate is 0.006 (0.6%) if the property is occupied and 0.009 (0.9%) if not:
•	Using these tax computation functions you should then display a tax report that looks like:
NOW PRINTING TAX REPORT:
** Taxes due for the property at:  42 Iris Way
        Property id:                                                                0
        This property has an estimated value of:       200000
        Taxes due on this property are:                         1200
** Taxes due for the property at:  350 Sea Towers
        Property id:                                                                1
        This property has an estimated value of:       1.23457e+006
        Taxes due on this property are:                         9876.54
Part 4 – Important Details  (12 points)
As noted above, this is primarily a lab about the creation of classes. Thus you will be graded on how you set up those classes and on your appropriate use of object oriented programming.
•	Use virtual methods where appropriate.
•	Use at least one pure virtual.
•	Use static and const where appropriate.  Use at least one static data member.
•	Strictly limit the use of “public”
•	Use inheritance and polymorphism where appropriate.
In addition you must:
•	Use a vector.
•	Tolerate errors in the input file. Specifically you should display any incorrect lines and identify them as bad, then skip them and go on,
•	Tolerate blanks (white space) in the address.
•	Display an error message and quit if you are given a file name that does not exist.
•	Make at least 3 test case input files that contain at least 5-10 Properties each with various characteristics such that all of the features of program are tested.
•	Have at least 10 files, (3 .h files and 4 .cpp files, 3 test cases).
•	Have no global variables, no goto’s, and no magic numbers.
•	Use good style with good names, indenting, etc.
