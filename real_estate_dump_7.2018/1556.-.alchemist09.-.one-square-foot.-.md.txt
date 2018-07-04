# one-square-foot
The one-square-foot application is a web-based application that is meant to be used in tenant management.
The application is built from scratch without any framework.
The application enables an individual or company that is tasked with estate management to setup it up
by adding properties, setting rooms in properties, move in tenants, handle tenant operations such as taking
payments which might be rent payments, deposit payments for utilities or even down payments for space let.
The application is meant to enable web-based receipt printing and also generate reports in either HTML or PDF
formats.

System Requirements
---------------------
Your system should be able to meet the following requirements for you to be able to install it:
*PHP 5.3+ (Very Important) PHP 5.3 is required since it introduced late static bindings in the case
of inheriting methods that have been declared as static. Most classes in the system extend from a
database abstraction class that has most of its methods that do non-class specific operations declared as static
*MySQL 5.0+
*An HTTP Server, preferably Apache 2.0+

Required Extensions
--------------------
Perl Compatible Regular Extensions(PCRE) must be installed on your server. They are used for data validation purposes in the system

Installation
---------------
Download and extract the application files and folders into a folder located within your web server document root.
For example, your can create a folder named "one-square-foot" in your web server document root.

Create the One-Square-Foot Database
-----------------------------------
Create the One-Sqaure-Foot database by either using the MySQL Console (a command-line-like utility for operating on MySQL), or a MySQL administration application like phpmyadmin.

Edit INIT And Database Class Files
-----------------------------------
The credentials you used in creating the one-sqaure-foot database are used in determining site-wide application constants that are loaded with an "init" file during application launch. For example, say you created the the database with a name of "database", a username of "username", and a password of "password", open the class.Database.php file located in the "lib/" directory of your application and edit the database connection constants to match your credentials accordingly.

Next you need to edit the constant that defines the root of the application. It's located in the "init.php" file in the "lib/"
directory. The line typically looks like:

##### defined('SITE_ROOT') ? NULL : define('SITE_ROOT', $_SERVER['DOCUMENT_ROOT'].DS.'app_real_estate-v02');

The above line defines the root of your application. The portion "app_real_estate-v02" is the name of the folder located in your web server document root into which you extracted the applications files and folders. Rename it to match the name you gave to that folder.

Edit Database File
--------------------
Edit the database file that contains structure of the application's database. Open the "database.sql" file using a text editing tool like notepad, then edit the database name to correspond to the name you assigned to the database created in the
previous step. The line that contains information about the database typically looks like:

###### 

--
-- Database: `app_real_estate_v2`
--
CREATE DATABASE IF NOT EXISTS `app_real_estate_v2` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci;
USE `app_real_estate_v2`;

-- -----

In the above line, replace every instance of "app_real_estate_v2" with the name you gave your database. Save the file, then import it using either the MySQL console or phpmyadmin to setup the database tables for the application.

You are now good to go. Go to the the browser and fire up the application from the base URL of your web server. E.g, say you 
are running the application on localhost, and extracted it to a folder named "one-sqaure-foot", go to http://localhost/one-square-foot and get started using the application by logging in as an administrator using a username of "admin" and password of "pass". You can now start using the application by setting up properties, rooms, tenants, taking payments, and producing reports.




