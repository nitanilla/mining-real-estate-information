To Run the Real Estate App

1. Download easy_gui from http://easygui.sourceforge.net/download/version_0.96/index.html
	a. Download the .tar.gz file of your choice
	b. Open the directory of the easy gui folder in terminal 
c. Run python setup.py install
2. Run the prop.sql file to create the tables and initial entries for the database. The database is setup to work for user (-u root) with password (-p password) and database named properties.  A database named properties will need to be setup or the configurations can be changed in the db.py file to meet the specifications of an existing database.
3. To run the app, open the app folder in terminal and run it via ‘python2.7 app.py’ or ‘python app.py’
