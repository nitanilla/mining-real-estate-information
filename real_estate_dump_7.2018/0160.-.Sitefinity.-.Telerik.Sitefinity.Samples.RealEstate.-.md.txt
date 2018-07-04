Progress.Sitefinity.Samples.RealEstate
=====================================

### This repository is not automatically upgraded to latest Sitefintiy version. The repository is monitored for pull requests and fixes. The latest official version of Sitefinity that supports this sample is 9.1. Be aware that using a higher version could cause unexpected behavior. If you successfully upgrade the example to a greater version, please share your work with the community by submitting your changes via pull request.

[![Build Status](http://sdk-jenkins-ci.cloudapp.net/buildStatus/icon?job=Telerik.Sitefinity.Samples.RealEstate.CI)](http://sdk-jenkins-ci.cloudapp.net/job/Telerik.Sitefinity.Samples.RealEstate.CI/)

The Real Estate starter kit is developed for companies in the fields of real estate, tourism, and hospitality. Such companies want to effectively showcase their properties, keep information up to date, and present attractive offers. This ultimately results in more sales and profits. 

This starter kit provides companies with a head start on their project. In addition, the starter kit gives developers a template for adding custom features to Sitefinity CMS. Some of the starter kit's features are:

* property listing module
* property search
* agent directory
* photo galleries
* maps


### Requirements

* Sitefinity CMS license
* .NET Framework 4.5
* Visual Studio 2012
* Microsoft SQL Server 2008R2 or later versions


### Prerequisites

Clear the NuGet cache files. To do this:

1. In Windows Explorer, open the **%localappdata%\NuGet\Cache** folder.
2. Select all files and delete them.

You need to attach the database backup files to your SQL Server. To do this:

1. In SQL Management Studio, open the context menu of _Databases_ and click _Attach..._
2. Click the _Add..._ button and navigate to the _SitefinityWebApp_ » *App_Data* folder.
3. Select the **SitefinityRealEstateStarterKit.mdf** file and click _OK_.
4. Click _OK_.

### Nuget package restoration
The solution in this repository relies on NuGet packages with automatic package restore while the build procedure takes place.   
For a full list of the referenced packages and their versions see the [packages.config](https://github.com/Sitefinity-SDK/Telerik.Sitefinity.Samples.RealEstate/blob/master/SitefinityWebApp/packages.config) file.    
For a history and additional information related to package versions on different releases of this repository, see the [Releases page](https://github.com/Sitefinity-SDK/Telerik.Sitefinity.Samples.RealEstate/releases).    


### Installation instructions: SDK Samples from GitHub

1. In Solution Explorer, navigate to _SitefinityWebApp_ » *App_Data* » _Sitefinity_ » _Configuration_ and select the **DataConfig.config** file.
2. Modify the **connectionString** value to match your server address.


For version-specific details about the required Sitefinity NuGet packages for this sample application, click on [Releases](https://github.com/Sitefinity-SDK/Telerik.Sitefinity.Samples.RealEstate/releases).


### Login

To login to Sitefinity CMS backend, use the following credentials:  
**Username:** admin  
**Password:** password


### Additional resources
Progress Sitefinity CMS Documentation:
* [Develop: Use and extend Sitefinity CMS functionality](http://docs.sitefinity.com/develop-create-and-manage-website-content) 

