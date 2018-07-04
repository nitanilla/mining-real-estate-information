Classifieds Install using maven version 3.0.4

1.	 Depending on DB, replace the desired jdbc dependency to the pom.xml 
	
	    <dependency>
               <groupId>net.sourceforge</groupId>
               <artifactId>jtds</artifactId>
               <version>1.2.5</version>
           </dependency>

	
2.	 Modify "applicationContext.xml" with your appropriate "ServerDialect":

    	sample for MSSQL:
	
	<prop key="hibernate.dialect">org.hibernate.dialect.SQLServerDialect</prop>


3. 	Modify "applicationContext.xml" with your appropriate db properties:

	<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName">
			<value>net.sourceforge.jtds.jdbc.Driver</value>
		</property>
		<property name="url">
			<value>jdbc:jtds:sqlserver://localhost:1433;instance=SQLEXPRESS;databaseName=uPortal</value>
		</property>
		<property name="username">
			<value>sa</value>
		</property>
		<property name="password">
			<value>password</value>
		</property>
	</bean>
	
4.	 Modify portlet.xml to give the desired group as admin rights to classifieds portlet

		<security-role-ref>
            	<role-name>Portal_Administrators</role-name>
           		 <role-link>local.2</role-link>
    	</security-role-ref>

5. 	If needed, modify ApplicationContext.xml to configure desired Ad Grooming values

        <property name="hourToCheck" value="12"/> (what hour of day to perform grooming (24 hour clock)
    	<property name="minuteToCheck" value="0"/> (the minute of hour to perform grooming)
    	<property name="checkInterval" value="60"/> (how often to check if it is time to groom)
     	<property name="maxCheckIntervalMillis" value="43200000"/> (the max amount of time between grooming)		
		
6.   	Change directory to ClassifiedsPortlet folder 
   		
7. 	 mvn clean package

8.  	Change directory to your uPortal folder 

9.  	ant deployPortletApp -DportletApp=c:\ClassifedsPortlet\target\ClassifiedsPortlet.war

10. 	Configure Classifeds Portlet on uPortal portlet manager	







Classifieds portlet Setup:

1. 	Logon to uPortal with administrator rights to Classifieds Portlet.

2. 	Click on "Classifieds Administration" Link at bottom right corner.

3. 	Enter Categories that are appropriate for your site:

      	Example categories:

		announcments
	        condos / vacation rentals
                free stuf
                lost and found
                rides / carpools
                volunteer opportunities
		wanted
		help wanted
		house sitting
		pet sitting
		services
		autos / motorcycles
                books
                clothing
                computers / electronics
                food
                houshold items
                all other
                animals / pets
                sports / outdoors
                tickets
                toys
                homes
                rentals
                roomates
		

4. 	Enter Headings that are appropriate for your site( when entering heading you can multiselect the desired categories for that category)

     	example headings:

                environmental
                real estate
                employment / services
                miscellaneous
                community
                for sale

5. 	Enter Help Title and Text

   	Help text is displayed when the Help button is clicked

6. 	Enter Policy Title and Text 

    	Policy Text is displayed when Policy link is clicked. A person entering an Ad, must click on the Policy reviewed box before an Ad can be entered.





