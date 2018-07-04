# App-MainAndSettingsPages

Use uiOutput/renderUI to implement a "settings" page

I need a way for users to change global settings, 
but don't want to dedicate valuable real estate on the web page for that purpose. 
A pop-up window would do the trick
but I haven't found out how to do pop-up windows in shiny.

This solution is for a pageWithSidebar layout.
It replaces the mainPanel content with 
a "Settings Page" accepting text input from the user and holding an actionButton
to re-display the "Main Page" when clicked. 
The user input carries over and replaces the original content on the Main Page.
