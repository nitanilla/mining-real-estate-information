# Project Management System

Projects Management System for Constructions and Real Estate
IA Project (Phase One)
Task Definition:
A Constructions and Real Estate projects management system is a web application that allows customers that have projects want to establish it in to communicate and hire project managers and Team leaders to accomplish and deliver their projects in an easy and fast way.
Actors (Five actors):
- Admin
- Customers
- Project Managers (PMs)
- Team Leaders (TLs)
- Junior Engineers (JEs)
Layouts (Three layouts):
- Home page layout
- Admin, Project Managers and Team Leaders profile have the same layout
- Customer and Junior Engineers profiles have the same layout
Roles:
1- Admin:
a. Control Users (Customers, PM, TL, JE): Add, Remove Users.
b. Control the Home Profile: Add, Remove, Update Posts (Means Projects) created by the customers.
c. If the Customer Need to create a project ,then he will write a post ,then this post will be pending the approval of the admin to appear in the home page.
d. Admin page layout (profile) includes:
i. Admin information: Photo, Job description, FirstName, LastName, Mobile, Email.
ii. All the actors that using the system so that the admin can control them.
iii. All the posts that created by the customers so that the admin can control them.
iv. If the Admin remove a post from his profile It reflect directly to the home page and be removed.
2- Project Manager:
a. Surfing the projects created by the Customers in the home page and selecting the appropriate projects then starting to create the team to achieve and deliver the projects.
b. Project Manager layout (profile) includes:
i. PM information: Photo, Job description, FirstName, LastName, Mobile, Email.
ii. PM Statistical diagrams (Pie Chart or Histogram) that shows his Qualifications and experience.
iii. All the Current projects that he managing it.
iv. All the previous projects that he delivered it (history).
v. Creating teams Module:
1. Search for team leaders and sending requests to make them join the team.
2. Search for Junior Engineers and sending requests to make them join the team.
vi. Control Projects Module:
1. Set Schedule for each project.
2. Set the status for each project (on progress, Delivered).
3. Write Comments, set Price for each project.
4. Remove Members (remove Undesired member).
5. Remove Projects (leave the project).
3- Team Leader:
a. Checking His Profile to see the requests that have been sent by any project manager that need him to join the team and send response either accept or reject.
b. Team Leader layout (profile) includes:
i. TL information: Photo, Job description, FirstName, LastName, Mobile, Email.
ii. TL Statistical diagrams (Pie Chart or Histogram) that shows his Qualifications and experience.
iii. All the Current projects that he currently joining it.
iv. All the previous projects that he delivered it before (history).
v. Creating teams Module:
1. Send Requests to JEs to Help the PM to Search for Junior Engineers and sending requests to make them join the team.
vi. Evaluate Junior Engineers Module:
1. Evaluate JEs and send feedback to the PM.
2. Remove JE (remove Undesired member).
3. Remove Projects (leave the project).
4- Junior Engineers:
a. Checking His Profile to see the requests that have been sent by any project managers or Team leaders that need him to join the team and send response either accept or reject.
b. Junior Engineers layout (profile) includes:
i. JE information: Photo, Job description, FirstName, LastName, Mobile, Email.
ii. JE Statistical diagrams (Pie Chart or Histogram) that shows his Qualifications and experience.
iii. All the Current projects that he currently joining it.
iv. All the previous projects that he delivered it before (history).
v. Control Projects Module:
1. Remove Projects (leave the project).
5- Customers:
a. Creating projects.
b. Customer layout (profile) includes:
i. Customer information: Photo, description, FirstName, LastName, Mobile, Email.
ii. All the Current projects that not delivered yet.
iii. All the previous projects that have been delivered to him by the PM.
iv. Control Projects Module:
1. Remove Projects: remove the projects but if it has been assigned to PM then it cannot be removed.
2. Add Projects.
3. Assign Projects to PMs.
4. Edit Projects.
Layouts:
1- Home Page Layout:
a. Include Two Parts:
i. First Part: A form that the customer uses to post the new project.
ii. Second Part: All the Current not assigned projects (projects not assigned to PM).
b. How it work:
i. Only Customers that could use the form to add new projects.
ii. When the Customer adds a new project, it will allow any PM to submit the form, and then the customer will choose one of the PMs which is the most appropriate PM to manage this project.
iii. When the customer assign a PM then the post will be hidden from the Home page cause the Home page must have all Current not assigned projects.
Header
Navi
Footer
All Current not assigned projects
Home Page
Form
2- Admin, Project Managers and Team Leaders profile:
a. Include:
i. First Part: Actor personal Information.
ii. Second Part: Statistical Diagrams for PM and TL Only. (exclude the Admin)
iii. Third Part: See all requests send from other actors (PM and TL Only).
iv. Fourth Part: Send responses to other actors (PM and TL Only) to accept joining the team or reject.
v. Fifth Part: All Current Assigned Projects.
vi. Sixth Part: All the Previous Delivered Projects.
vii. Seventh Part: Admin Could Control Users as Explained in the Roles Part.
viii. Eight Part: PM and TL Could Control Projects and Users as Explained in the Roles Part.
Header
Navi
Footer
All Current and previous assigned projects
Admin, PM and TL Page Layout
3- Customer and Junior Engineers Page Layout:
i. First Part: Actor personal Information.
ii. Second Part: Statistical Diagrams for JEs Only. (exclude the Customer)
iii. Third Part: See all requests send from other actors to the JEs to join their teams.
iv. Fourth Part: Send responses to other actors to accept joining the team or reject (this case for the JEs Only).
v. Fifth Part: All Current Projects.
vi. Sixth Part: All the Previous Delivered Projects.
vii. Seventh Part: Customer Could Control Projects as Explained in the Roles Part.
viii. Eight Part: JEs Could Control projects as Explained in the Roles Part.
Header
Navi
All Current and previous assigned projects
Customer and JE page Layout
Important Notes:
1- Create Two Popups:
a. First Popup: For Login.
b. Second Popup: For Registration.
c. The Login popup is the first thing that will be open when the application runs, and it is a popup appeared from a button in the Home page.
d. If the users don’t have an account then he will register.
e. These two popups are appeared from a button in the Home Page.
2- Customers only are allowed to use the form in the Home Page to create new projects.
3- Customers only are allowed to choose the PM and assign him to the project.
4- PMs only are allowed to open and submit the posts created by the customers in the home page.
5- TLs and JEs are not allowed to interact with the home page (read only).
6- Customers can add new projects from their profiles then it appears in the home page (it is another way for the customer to add new projects).
7- When the PMs are assigned to the project by the customer, then the post disappear from the home page.
8- When the PMs Left the project, then the post appear in the home page.
9- Draw Statistical Diagrams as explained above in the role part depending on the experience and Number of projects deliver by the actor.
10- When the Customer add new project in the home page, PMs only are allowed to write comments to that Post.
11- PMs can report a specific customer.
…………………………………………………………………………………………………………….
