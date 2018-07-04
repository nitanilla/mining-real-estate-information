# KWrealtors

Project for the LaunchCode JAVA CS350 course

JAVA swing application for an in-house employee portal used by a real estate company.
The portal frame that an employee is directed to depends on their job type. 
The type of employees are:  

Agents - can make changes to property listings     
Clerical Staff - can make changes to employee db     
Managers. 

Each job type is allowed to preform certain activities such as add or update a property listing or delete an employee from the database. 

Program will asked for you to sign-in. Will need to know an Employee ID and password. 
- start by using id: 11111  and passw:  'ABC'       
with this ID user can then list out other all ids, property listings

4 hibernate tables are use to store the company info. 
Employee - stores all employee info. Only the Clerical staff can make changes to this table.
Property - stores all the avaliable property listed by the company. Only an agent can make changes to this table. Agents can add a listing and only that agent can then update or delete that listing. 
User - contains ID & passwords of all active employees.
Key - used as a storage of the instance ID & real estate License No
                    
BeanTableModel; RowTableModel         
from GitHub account - arlahiru

java version:  1.8.0 
