# Demo
Check out the demo at http://openfda.deleidos.com.

[Version 1.0](https://github.com/deleidos/prototype-20150626/tree/1.0.0) was created on June 26 at 1:50 p.m. EST.  

***

## Build and Install

Once the [dependencies are satisfied](https://github.com/deleidos/prototype-20150626/blob/master/docs/prerequisites.md), building the code, including execution of applicable tests, can be achieved by executing the following where you have cloned this repo:

```bash
mvn clean install
``` 

See the [install doc for running the prototype](https://github.com/deleidos/prototype-20150626/tree/master/docs/INSTALL.md).

***

# Approach
This prototype was created using the [Scrum](https://en.wikipedia.org/wiki/Scrum_(software_development)) methodology, [Digital Services Playbook](https://github.com/deleidos/prototype-20150626/blob/master/docs/playbook.md) guidance, and [Lean Startup](https://en.wikipedia.org/wiki/Lean_startup) principles.  

Scrum focuses on developing value-added features collaboratively with the end users. It emphasizes frequent communication at all levels and delivering working software within short release cycles. This process is especially valuable when detailed requirements are not well understood early in the program while still supporting the release of new capabilities delivered within months.  

Leidos’ Scrum agile development methodology emphasizes:
+	User-driven participation in software requirements, reviews, and testing of releases  
+	Close partnership and interaction with data owners to ease integration and reduce risks  
+	Streamlined agility by process reduction, design simplification, and incubation of innovative ideas  
+	A scaled-up set of agile management processes to support larger, more diverse teams and apply agility across all organizations of the program.  

![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/scrum_diagram1.png)

A description of this approach, as applied to the prototype, is as follows:

## Prototype Stakeholders

Implicitly, the RFQ was a stakeholder in the process. Our process would normally involve regular contact with all stakeholders. However, there was only one Q&A round permitted with this stakeholder.

In addition to specified requirements, the team interpreted the RFQ to define the relevant marketspace that the product manager and team was serving. For the sake of this prototype, a couple individuals outside of the design/development team took on the role of "People", who role-played in the marketspace. The team met with the "People" every other day during the design and development period. 

***

## Day 0: Wednesday, June 17
RFQ was issued.

## Day 1: Thursday, June 18

###Authorization and Accountability
Line management authorized a product manager to assemble a team and create a prototype for submission. ([See the email granting authorization and accountability](https://github.com/deleidos/prototype-20150626/blob/master/docs/archive/authorization.md))

## Day 2: Friday, June 19

###Assembly of Multidisciplinary and Collaborative Team
A subset of the Leidos DigitalEdge Team, consisting of a Product Manager, Technical Architect, Agile Coach, Interaction Designer, Delivery Manager, Front-end Web Developer and Back-end Web Developer, were assembled on Friday afternoon. 

###Human-Centered Design Technique No. 1: Adopting Multidisciplinary Skills and Perspectives
Because the data source was dictated by the RFQ, the team took the approach of first understanding the data and how the data could highlight the specified requirements.  

The multidisciplinary team discussed the data available and possibilities for new ways to serve the marketplace. In the ensuing discussion, the team began to focus on remixing the data to answer the question "Which drugs have been recalled in which states?"  

Following this, the technical architect presented options for the prototype given the data available on openFDA and the known timeline for delivery of the prototype. A preliminary architecture was created.  
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/whiteboard-drawing_20150619.JPG) 
The interaction designer proposed the following GUI mock-up:
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/prototype-gui-mockup1.png)

###Human-Centered Design Technique No. 2: Iterative Design Process
Given this architecture and proposed GUI, the team discussed the prototype and populated tasks into VersionOne. This was the beginning of the iterative process in agile, where tasks are specified and estimated, and updated continually during the effort.
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/versionone-tasks-screencapture-20150619.jpg)

## Day 3: Monday, June 22
  
###Groundwork
The day was mostly spent performing groundwork for the prototype. The team met midday to review progress and update the plan for the next 24 hours. (This was in addition to other non-prototype projects the team was juggling.)  

###Responsive Design
The team decided on an approach using Bootstrap to ensure that the prototype would work on multiple devices.

###Modern and Open Source Technologies
The software stack chosen for this prototype includes only [open source licensed technologies](https://github.com/deleidos/prototype-20150626/tree/master/docs/licenses). Many open source packages are included. Highlighted are Bootstrap, Docker, AngularJS, CentOS, Java, JavaScript, MongoDB, Leaflet, and DigitalEdge, to name at least five modern and open-sourced technologies.  

Each of these included open source packages is pre-existing. DigitalEdge, a new addition to open source by Leidos, is a container-based toolkit for creating big data solutions.

## Day 4: Tuesday, June 23

###Human-Centered Design Technique No. 3: Involvement of the Consumer in the Design and Production Process
Now that the team had a notion of what the data could support, it was time to consult with the "People" who were in the food and drug marketspace. In reviewing the data with the team, the "People" focused on the particular question of "For a given manufacturer, which states were affected by drugs produced by the manufacturer?"

This was slightly different from the premise that was originally drawn from the data on Friday. Now, it sought to address a customer who was in charge of PR for a manufacturer and wished to know which states had been most affected by recalls, thus steering where to direct communications about the recalls.

Consequently, the plan for the prototype was narrowed to highlight (1) consuming data from a publicly available API, (2) enriching the data record by transforming the freeform text field "distribution_pattern" into structured geographic elements, (3) leveraging a populated data repository to create query-time summarizations and publishing those results via a REST API, (4) presenting enriched elements in an intuitive GUI, and (5) remixing additional information by dynamically querying the source API.

![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/prototype_architecture-v1b.png)

###Continuous Integration
[jenkins-openfda was stood up](https://jenkins-openfda.deleidos.com) to poll the repository and configured to not only build and test the software frequently but also orchestrate the deployment of the Docker containers supporting the prototype to the provisioned EC2 instance. [![Build Status](https://jenkins-openfda.deleidos.com/job/prototype-20150626_master/badge/icon)](https://jenkins-openfda.deleidos.com/job/prototype-20150626_master/).

###IaaS Provider
Amazon Web Services was selected to be the deployment environment.  
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/aws-devtest3-screenshot1.png)

## Day 5: Wednesday, June 24

###Continuous Deployment
A Jenkins job allows for the automated deployment of the prototype to one or more CentOS 7 instances.   A Vagrantfile is provided in the deployment project, which allows configuration of a simple control machine outside the Jenkins environment to use for development and testing.  [![Deployment Status](https://jenkins-openfda.deleidos.com/job/Deploy_Prototype/badge/icon)](https://jenkins-openfda.deleidos.com/job/Deploy_Prototype/). 

## Configuration Management 
Ansible was used to orchestrate the installation and configuration of a CentOS 7 OS (currently using the official CentOS 7 EC2 Amazon Machine Image (AMI) from the AWS Marketplace) used for hosting the prototype.  For alternate deployment environments, any CentOS 7 OS (bare metal on premise or in the cloud, or cloud-provided VMs) will suffice.

## Continuous Monitoring
Because the prototype is deployed to a Docker execution environment, the traditional OS metrics tools (e.g., Cloudwatch, Ganglia, Graphite, Nagios) could be used; however, the team chose to use the awesome cAdvisor monitoring tool to perform traditional OS and container monitoring.  The cAdvisor interface is 
viewable here: http://openfda.deleidos.com:8080  

Application health monitoring is also traditionally configured to provide near–real-time information pertaining to the health of the various tiers of the application.  For the purposes of the prototype, a simple set of monitoring checks has been added with a very simple notification path in Jenkins.

[Monitoring by auditd](https://github.com/deleidos/prototype-20150626/blob/master/docs/archive/audit1.log) is also installed. Future improvements could include OSIM and off-box logging.

## Container-Based Deployment
Docker was used for containerization of the deployed software. The decision to use the power of the Linux container technology, facilitated by Docker, and the decoupling of the deployment of the containers enables the solution to run either on premise or in other cloud providers. Also, using an Ansible playbook to provision the CentOS 7 OS (and not a container orchestration tool like the AWS Container Service or Kubernetes) facilitates the documentation of the OS packages required to run the prototype and provides a heterogeneous execution environment for the application (one on premise, one in AWS, one in GCE; all load balanced through a proxy).

## Day 6: Thursday, June 25

###Design Style Guide
A [Color Palette](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/ColorPalette.png) was created for this prototype. [Fonts](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/TypographyStyleGuide.jpg) were selected for the type.

###Further Iterations
The Product Manager and Interaction Designer met again with the "People" to show them the latest version of the prototype and get feedback for further refinements.  

A slightly different layout was discussed to promote better use of real estate in different responsive modes. Also, scope was narrowed to focus on making the GUI stable for rendering remixed data.
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/versionone-tasks-screencapture-20150625.jpg)

## Day 7: Friday, June 26

###Unit Testing and Code Coverage
Unit tests were written and committed to the repo. The DevOps environment was configured by the Delivery Manager to [calculate code coverage](https://jenkins-openfda.deleidos.com/job/prototype-20150626_master/lastBuild/jacoco/).
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/codecoverage1.png)

###API Documentation
Documentation was added for the [Mongo REST API](http://openfda.deleidos.com/apidocs/swaggerui).

###Usability Testing
Usability testing was conducted, and issues identified were entered into the Issues page on GitHub.

## Day 8: Monday, June 29

###Issues Work-Off
[Issues were identified](https://github.com/deleidos/prototype-20150626/issues). High priority issues were worked and closed.
![](https://raw.githubusercontent.com/deleidos/prototype-20150626/master/docs/archive/issues1.jpg)

## Day 9: Thursday, July 2
The team completed some minor brush-up of the interface and added installation documentation.

## Day 10 &amp; 11: July 6th and 7th
Install docs testing. A couple last tweaks. Done.

&copy; Leidos 2015
