# JDBC-Relational-DB-application
In this assignment you will develop a DB-backed Java application for management of real estates.

## 1. Development of a relational database application

In this assignment you will develop a DB-backed Java application for management of real estates. This is the domain model:

![UML Diagram](https://user-images.githubusercontent.com/12661590/39948822-fdce41e0-5577-11e8-9808-e8e5ef1ea10a.JPG)

The central entity is an estate agent that manages estates. It has a unique login name as well as a password.
There are two basic types of estates: houses and apartments. Apartments are rented, whereas houses are sold. 
For each estate, some general information are stored: identifcation number, address (comprised of city, postal code, street and number) and square area. 
Additionally, each apartment has a floor number, a rent (price), a certain number of rooms, a flag indicating whether there is a balcony and a flag indicating whether there is a built-in kitchen. 
Houses on the other hand have a number of floors, a price and a flag for whether a garden is included.

For every tenancy and every sale, respectively, there is formal a contract which has a uniqe contract number, a contract date and a settlement place. Tenancy agreements (for apartments) have a start date, a tenancy duration and extra charges (utilities). 
A house can be paid by installments. 
The amount of installments and the interest rate are part of the sale contract.

For every contract, there is only one renting/buying person, but each person can rent/buy an arbitrary amount of properties.

### 1.1. DB-schema

Translate the above model to a relational model by defining the respective DB schema. Fulfill the following requirements:
- The commands for creating the DB objects are contained in SQL scripts.
- Choose an inheritance model (e.g. horizontal partitioning)
- Define a primary key for every relation (surrogate keys are ok). Define foreign keys.
- Initialize the tables with appropriate sample data. There should for instance be an estate agent account you can use to log in.
- Create the tables using Squirrel or the DB2 CLI

The tables created in this part of the assignment are the basis for the next part.

### 1.2 Java application
Implement an estate management using the previously created DB schema. The realization of the UI (graphical or command-line interface) is up to you.
The application should support the following functionalitites:
- Management mode for estate agents
  - Account creation
  - Changing and deleting accounts

  To access this mode, the user has to enter a password, which is hard-coded in the application for simplicity.

- Management mode for estates
  - Estate agents can log in
  - Creating, deleting and updating estates
  
- Contract management
  - Insert persons
  - Sign (create) contracts
  - Overview of all contracts

There is a sample project */usr/remote/lehre/dis/Blatt2.zip*. For your implementation you can either use this project or create your own. If you create your own, don't forget to add *db2jcc.jar* and *db2jcc_licence_cu.jar* to your classpath.

### Note
- On the pool PCs there are Eclipse installations you can use (/usr/remote/bin/eclipse361).
- When working at home, please use your own Eclipse installation
- The duration of this assignment is two weeks
- You don't have to submit your results. The completion of the assigment will be verified by practical demonstration in front of your device.
- Before executing the example, change db2.properties and create the example table Makler. The respective DDL script is in the Makler class. The character encoding is UTF-8. If you have problem with umlauts, please change the encoding in your Eclipse preferences to UTF-8.
