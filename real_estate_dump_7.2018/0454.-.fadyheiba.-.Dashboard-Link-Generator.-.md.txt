# Dashboard-Link-Generator
## Allows you to share your current dashboard by generating a link to your app/sheet/selections.

This Qlik Sense extension generates a shareable link to the current app, sheet, and selections made so that the person receiving the link can see exactly what you're seeing. You can share the generated link through three output methods: Copy to Clipboard, Create New Email with link, or a Textbox.

###Usage:
- The extension was built to take up as least real estate on the sheet as possible, all three output methods are able to scale down to a 1 x 1 square.
- Please make sure to include both folders, DashboardLinkGenerator and DashboardLinkGeneratorURLResolver, in the extensions folder.

###Output Methods:
####Copy To Clipboard:
![alt tag](https://github.com/fadyheiba/Dashboard-Link-Generator/blob/master/FEI-DashboardLinkGenerator/Resources/Copy%20To%20Clipboard%20Output%20Method.png)
####New Email with link:
![alt tag](https://github.com/fadyheiba/Dashboard-Link-Generator/blob/master/FEI-DashboardLinkGenerator/Resources/New%20Email%20Output%20Method.png)
![alt tag](https://github.com/fadyheiba/Dashboard-Link-Generator/blob/master/FEI-DashboardLinkGenerator/Resources/New%20Generated%20Email.png)
####Textbox:
![alt tag](https://github.com/fadyheiba/Dashboard-Link-Generator/blob/master/FEI-DashboardLinkGenerator/Resources/Copy%20to%20Textbox%20Output%20Method.png)

###For Sense 2.x:
This version of the extension is for Sense 3.0 and above. If you would like to the version for 2.x version, it is included in a .zip file in the main folder. However, it is recommended to use this extension in Sense 3.0 as the new release fixed bugs in Sense 2.x that made the link resolution process more stable, specifically with date values including spaces.

####Credit:
- Original App Integration logic for 2.x created by Piotr Cyupla
