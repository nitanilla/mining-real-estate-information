# lewis_CSCI2270_FinalProject
# Housing Search Network

Summary:

This program will allow Real Estate workers to use this database in order to easily keep track of properties. The realtor can use this program to add houses to the database, search for homes that would be perfect for a buyer. The search will be based on several parameters including number of bedrooms, number of bathrooms, square footage, type of house (apartment, townhome, house), neighborhood, and the price. Using all these parameters the program will allow users to easily find the perfect house.

How to Run:

Download the FinalProject.cpp, House.h, and House.cpp files and run them together in Codeblocks. A menu will be displayed with a list of options the user can choose from. When the user selects an option from the menu, further instructions will be printed to the command window for the user to follow in order to fulfill the functions.

Dependencies:

The only library needed for this program is the standard library for printing and strings.

System Requirements:

Runs best in Codeblocks.

Group Members:

Rachel Lewis

Contributors:

Michael Condon (SuperialCondon)
Phillip McKenzie (bredtoshred)

Open Issues/Bugs:

**Resolved**: If the user initially selects the quit option without doing anything else, the program prints the address of the head and then seg-faults. For example: Menu displays, user enters "7" for quit, prints "1058 virgor", then seg faults.
		Fixed by changing the head->next pointer in the house constructor
