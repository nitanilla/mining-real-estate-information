# Property Matcher

This solution implements a Property Matcher for following requirements

## Overview

Real Estate agencies have a few different ways of advertising their properties. One of them is to send us an XML file with the property details. In this scenario, the assumption is to match received properties with properties already present in database. This will be used to determine if a property needs to be created or updated.

For the purpose of this exercise there are 3 agencies using this system, each with different property matching rules:

### Only The Best Real Estate! (AgencyCode: OTBRE)

Only The Best Real Estate!  use a lot of punctuation in their property names and addresses.  A property is considered to be a match if both the property name and address match when punctuation is excluded.  For example, the property “*Super*-High! APARTMENTS (Sydney)” located at “32 Sir John-Young Crescent, Sydney, NSW.” would be a match for a property called “Super High Apartments, Sydney” located at “32 Sir John Young Crescent, Sydney NSW”.

### Location Real Estate (AgencyCode: LRE)

Location Real Estate are not really good at locating properties, and as a result their properties will often appear to be up to 200 metres away from the actual location when placed on a map.  A property is considered to be a match if the agency code is the same and the property is within 200 metres or less of the actual property location.  For the sake of simplicity, assume that 1 degree of latitude or longitude is equal to 111km.

### Contrary Real Estate (AgencyCode: CRE)

Contrary Real Estate like to have their property names backwards.  A property is considered a match if the names match when the words in the name of the property are reversed.  For example, a property with the name “Apartments Summit The” is a match for a property with the name “The Summit Apartments”.


## Running the Application
The application has been developed in Visual Studio 2013. Below are the steps for running the application.

1. [Clone](https://help.github.com/articles/cloning-a-repository/) the repository to create a local copy on your computer.
2. Open **PropertyMatcher** Solution in Visual Studio.
3. Build the solution through Visual Studio. This will restore all NuGet packages during the build.
4. Select the project **PropertyMatcher.Test** and run the tests.

## Running Tests

### Unit Tests

Unit tests are implemented using MSTest and are part of the **PropertyMatcher.Test** project. These tests can be run using the Test Explorer within Visual Studio. For more details, please visit [How to: Run Tests from Microsoft Visual Studio](https://msdn.microsoft.com/en-us/library/ms182470(v=vs.120).aspx) 

