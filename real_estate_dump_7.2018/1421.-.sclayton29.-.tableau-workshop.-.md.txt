## About
Last Updated Feburary 2017  
Created by [Sarah Clayton](https://github.com/sclayton29), [Carolyn Mead-Harvey](https://github.com/carolyn-meadharvey), and [Paul Vieth](https://github.com/crispzips)  
University of Oklahoma Libraries


## Table of Contents
* [Introduction](#introduction)
* [Getting the Data](#getting-the-data)
* [Loading Data into Tableau](#loading-data-into-tableau)
* [Creating a Map](#creating-a-map)
  * [Selecting the Data](#selecting-the-data)
  * [Selecting the Visualization Type](#selecting-the-visualization-type)
  * [Styling the Visualization](#styling-the-visualization)
* [Creating a Line Graph](#creating-a-line-graph)
  * [Analytics with Tableau](#analytics-with-tableau)
* [Creating a Bar Chart](#creating-a-bar-chart)
* [Creating an Interactive Dashboard](#creating-an-interactive-dashboard)
  * [Adding Worksheets](#adding-worksheets)
  * [Styling the Dashboard](#styling-the-dashboard)
  * [Filtering on the Dashboard](#filtering-on-the-dashboard)
  * [Adding Other information](#adding-other-information)
* [Sharing your Visualizations](#sharing-your-visualizations)

## Introduction
This lesson will take you through creating a data visualization with Tableau.

Tableau is a drag and drop tool that allows users to create interactive visualizations without any programming. This can be a good way to explore or present your data. 

Tableau Public is available for anyone for free, but you have to save your visualizations to the Tableau server. If you have data you cannot or do not want to make public, [academic trials of the full software are available](https://www.tableau.com/academic).

If you follow along with this material, by the end of the workshop you will have a visualization that looks similar to the one below. 
{% include tableau-viz.html %} 

[Return to Top](#about)


## Getting the Data
We are going to be mapping Crime Data in the US from 1960 to 2014. This data comes from the FBI's Uniform Crime Reporting Statistics. The table was created using the [UCR Data Tool](https://www.ucrdatatool.gov/) using the State by state and national estimates options. Like most real world data this data is not perfect.[View the notes on this data set](/data/data-notes.md)

We also performed minor clean up for this data to be more easily useable.

1. [Download the cleaned data](https://github.com/sclayton29/tableau-workshop/raw/master/data/CrimeStatebyState.zip)
2. Unzip the data.
3. Move the file to your desktop or another location where you can easily locate it.
4. Look over the spreadsheet to gain a better understanding of what you will be visualizing.

[Return to Top](#about)

## Loading Data into Tableau
Now, we can load our data into Tableau.
1. Open your Tableau application.
2. Under connect, select Text File. * Note: Tableau classifies CSV files as text files not Excel. ![Fig_01: Connecting to a File](images/fig_01.png)
3. Navigate to and open your file in the explorer or finder window that appears.
4. You should now see your table displayed in tableau. ![Fig_02: Data in Tableau Explorer](images/fig_02.png)
5. Click the Orange Sheet 1 tab at the bottom left of the screen. There may be a bit of a delay while Tableau loads your data. With this dataset, this step shouldn't take longer than a few moments.

[Return to Top](#about)

## Creating a Map
We will create a map that shows the violent crime rates by state through the years as our first visualization. 
1. Before we create anything, let's rename Sheet 1 to a more approriate name. Right click on Sheet 1 and select Rename Sheet. Then, type in whatever name you would like. For this example, we will use Map. Press enter to save the new name. ![Fig_03: Renaming your sheet](images/fig_03.png)

[Return to Top](#about)

### Selecting the data
2. Tableau has broken down our spreadsheet to be useable by the software. On the left side of the screen, you should see a list of the columns from the original spreadsheet. These are broken into Dimensions and Measures. Tableau has automatically broken down your data into these two roles (You can change this manually by right clicking an item). Next to each column name, there is an icon indicating the data type. The globe icon indicates that it is geographic data, the # indiciates that it numberic data, and Abc indicates that it is textual data.
3. Drag the State Dimension to columns and the Violent Crime rate measure to Rows. Tableau will automatically create a bar graph. ![Fig_04: Dragging data](images/fig_04.png) * Note: the Crime Rate is crimes per 100,000 people. 
4. When you dragged violent crime rate to Rows. Tableau changed it to the SUM of the Violent Crime Rate. Let's change that to the average. Click SUM(Violent Crime rate). Hover over Measure (Sum) and select Average.![Fig_05: Changing SUM to AVG](images/fig_05.png)

[Return to Top](#about)

### Selecting the Visualization Type
5. The bar chart is interesting, but we wanted to see the data as a map. Click the Show Me icon in the top right of the application. Select the filled map option (2nd row in the middle). Now, you should see a map. ![Fig_06: Changing Viz Type](images/fig_06.png) *Notice that Tableau has moved State and AVG(Violent Crime rate) under Marks on the left side of the screen and added Longitude and Latitude to your rows and columns. 
6. Click the Show Me Tab again to hide the different visualization options. 
7. Tableau will automatically generate a color scheme for the map and add a legend to the right side of the map. We can change the colors to something more approriate. Click the arrow next to AVG(Violent Crime Rate) on the legend and select Edit Colors. 
8. Click the Down Arrow next palette to select a different color scheme. In our example, we will choose Red-Green Diveraging. We want green to indicate less crime so we will select the Reserve Checkbox. Click Apply to see your changes on the map. Click OK to exit the color selection window. ![Fig_07: Chaning the colors](images/fig_07.png)

[Return to Top](#about)

### Styling the Visualization 
9. That worked but now it looks like all of our states are shades of green. However, if you zoom into Washington, DC, you should see a red speck.(Hint: double click to zoom in and hold shift to drag the map around). Hovering over DC will show a violent crime rate over 1,600. The next closest is Florida with 729. If we examine the data closely, we notice that outside DC the highest crime for any one year caps off at about 1,200. Let's cap our range at 1,200. We could include a note about this in our final product. Open the Edit Colors window again. Click Advanced to reveal additoinal options. Click the checkboxes next to Start and End. Now, we can enter 0 for the start and 1,200 for the end. I'm going to leave the Center at the default right in between the start and end. You can check Stepped Colors if you want clearer categories. Click OK to apply your changes and exit. ![Fig_08: Setting fixed start and end](images/fig_08.png)
10. We can update our Legend title from AVG(Violent Crime Rate) to something more human readable and descriptive. Click the down arrow next to AVG(Violent Crime Rate). Select Edit Title. Type in your new title. In our example, we will use Violent Crimes per 100,000 people. Click OK to save your changes. 
11. We further style of map by using the Marks box on the left side of the screen. 
12. You may have noticed that when you hover over a state on the map a pop-up appears with the name of the state and the actual number for the average violent crime rate. This is called the Tootip. ![Fig_09: ToolTip Box](images/fig_09.png)
13. We can add additional element by dragging measures to the tooltip box under Marks. Drag the Violent Crime total on top of the Tooltip box. Now, SUM(Violent Crime Total) should appear below AVG(Violent Crimes Rates) with a the tooltip icon beside it. 
14. Tableau will automatically pull the column title as the label in the Tooltip. You can customize this by clicking the Tooltip Box. A text box will appear to let you edit the display. In this example, I will just add that the rate is per 100,000 people. Click OK when you are satisified. ![Fig_10: Changing the ToolTip](images/fig_10.png)
15. We can also add labels to our map. Click the Label box under Marks. Click the Show Mark Labels Check box. You can choose to allow labels to overlap if you want parts of labels visable in more compact states. ![Fig_11: Adding Labels](images/fig_11.png)

[Return to Top](#about)

### Adding Filters
16. We can apply filters to let people interact with our data. Let's create one for years. Drag the Year dimension to the Filters box(above Marks). Leave the defaults and click OK. ![Fig_12: Adding Year as a Filter](images/fig_12.png)
17. Click Year and Show Filter to expose the filter for visitors to manipulate. 
18. There are several different options for your filter. By default, you should see a slider. This is nice for a range of dates, but makes it difficult to select a single year. If you click the exposed year filter (on the right side of the screen), you should see three options to display your filter: Range of Values, At least, and At most. These are the options for a continous data type. ![Fig_13: Year filter continous options](images/fig_13.png)
19. We can change the data type to discrete to see more options. Go back to the filter box on the left side of the screen. Click year and select Discrete. ![Fig_14: Change to Discrete](images/fig_14.png) In the pop-up window that appears, select All and click OK. You will need to select Show Filter again to expose it. 
20. Go to the exposed filter (on the right). Select whichever style you prefer. For this example, we are going to use the Wildcard Match style. ![Fig_15: Discrete Filter Styles](images/fig_15.png)

Now, we have a nice map that will allow others to view and interact with our data. Let's create some other visualizations. 

[Return to Top](#about)


## Creating a Line Graph
In the next steps, we will create a line graph to show violent crime rates through the years. 
1. Begin by creating a new sheet. Click the new worksheet button on the bottom of the screen. ![New Worksheet Creation](images/fig_16.png)
2. Rename the worksheet something meaningful. We will call our sheet *Violent Crimes by Year*. 
3. This time we will drag Year to Columns and Violent Crime Rate to Rows. ![Year and Violent Crimes in columns/rows](images/fig_17.png)
4. Notice the rows defaults to SUM(Violent Crime Rates). To change this to an average click on SUM(Violent Crime Rates), hover over Measure and select Average.

[Return to Top](#about)

### Analytics With Tableau
Tableau allows you to perform basic statistical analysis. Let's add a trend line to this graph. 
5. Right click on the view and select Trend Lines > Show Trend Lines. You will now see a trend line representing a linear regression model based on our data.  
6. To view the trend line model and information about its significance, right click on the view and select Trend Lines > Describe Trend Model. This menu shows the model's formula, p-value, ANOVA table, and R-Squared value.
7. Right click on the view and select Trend Lines > Trend Lines Options. The Trend Line Options menu gives options for changing the model type, including or excluding factors, and adding confidence bands. 

[Return to Top](#about)

## Creating a Bar Chart
1. Add a new sheet and name it Violent Crime Breakdown. 
2. The FBI classifies aggreviated assult, murder, rape, and robbery as violent crimes. In this section, we will create a bar chart with the break down of these cateogories of crimes.  
3. Drag these cateogories in the rows box. As you add each cateogory, they will be shown as different charts. ![Fig_18: Categories in Row](images/fig_18.png)
4. Click Show Me and Select the horizontal bar chart. This will combine all of your measures into one chart. Notice that your measures have moved to a new location. They are now in a new box called measure values on the left side of the screen below Marks. ![Fig_19: Measure Values Box](images/fig_19.png)
5. For display purposes, we want to move the Measure Values to the x axis and number of crimes to the y axis. Tableau has a built in feature to easily accomplish this. Click the Swamp rows and columns button on the top toolbar. ![Fig_20: Swamp rows and columns button](images/fig_20.png)
6. Notice there's something askew about the rape measure values. First, we have two different statistics for the total number of rapes committed in all states for all years of our dataset. Second, the "revised rape" measure value is so small as to be negligible on the scale of this bar graph. We don't want to visually (or in any way) minimize rape as a phenomenon. When we investigate these discrepancies, we learn that the FBI began using [a new definition of rape in 2013](https://ucr.fbi.gov/crime-in-the-u.s/2013/crime-in-the-u.s.-2013/violent-crime/rape). So, the two different measure values aren't depicting different crimes, but a change in definition of a crime, so we need to aggregate those two values to give a realistic portrait of violent sexual assault in the United States in proportion to measures of other violent crimes. 
7. To do this, click the dropdown menu in the upper right hand corner of the "Measure Values" card. Click the first option, "New Calculation." ![Add Calculation to Measure Values](images/TableauBarchartImg01.png) We want to aggregate the sums of the two definitions of rape. This is as simple as adding "+" between "SUM(item_1)" and "SUM(item_2)". Tableau accepts the addition operator, but will not accept SUMs of SUMs. When you enter this calculation, Tableau will change the addition operator to an aggregation "AGG()", though this is not a selectable parameter in advance.

[Return to Top](#about)

## Creating an Interactive Dashboard
Now we can create a dashboard to view all of our visualizations at once. 
1. Click the New Dashboard button at the bottom of the screen. It is to the right of the new worksheet button. ![Fig_21: New dashboard button](images/fig_21.png)
2. Rename you dashboard, Violent Crimes in the USA.   

[Return to Top](#about)

### Adding Worksheets
2. In your new Dashboard, you should see Size and Sheets in the left column. ![Fig_22: Size and Sheets](images/fig_22.png)Under size, you can change the size of your dashboard to optimize it to different displays. You have the option to use a range, fixed size, or have your visualization change automatically based on your display. For this example, we will choose automatic. Click the down arrow beside the size option and click Automatic. 
3. To add worksheets to the dashboard, you need to drag the sheet name to the center of the screen, where you see the text, "Drop sheets here."
4. Start by dragging the map. It will be default, take up the entire workspace and add the legend and filter to the right. 
5. Now, drag Violent Crimes by Year to the Map. When you drag the sheet, you will notice that different parts of the screen become highlighted. This is showing you where the sheet will be placed. Drop the chart so it will take up the bottom half of the screen. Don't worrry about the style yet. We will fix that at the end. ![Fig_23: Adding Line Chart to Dashboard](images/fig_23.png)
6. Let's add the final visualization to the map. Drag Violent Crime Breakdown so it appears in the bottom right corner of the dashboard. ![Fig_24: Adding Bar Graph to Dashboard](images/fig_24.png)

[Return to Top](#about)

### Styling the Dashboard
7. Now that the data is add, we can make our dashboard more user-friendly by adding some styling. The map sheet needs more screen real estate than the other visualizations. Hoover over the bottom of the map sheet until you see a black arrow. Then, drag the map down until it is the size you want. 
8. We can do a similar process orto give the line chart more horizontial space. Hoover in between the line chart and bar graph until you see another black arrow. Drag until you have your desired position. 
9. We can add a title to the map. In the bottom left corner, click the Show Dashboard Title box. ![Fig_25: Adding the Title](images/fig_25.png) You can double click the title to open a text box that will allow you to style the text and add any additional text you may like. For this example, we will append "from 1960 to 2014" to the end of the title and center it. Click OK to apply the changes. ![Fig_26: Edited title](images/fig_26.png)
10. The year filter and map legend are taking up a lot of space. We can fix this by changing these boxes to floating elements. Click down arrow on the year box. Select Floating. ![Fig_27: Floating Element](images/fig_27.png) Open the year menu again (with the down arrow) under float order, select bring to front. Repeat for the legend. Notice after both the legend and year have been made floating, the map and charts expand to fill the space. Place the year filter and legend where you want them. 
11. Let's remove the Map title to free up even more space. Open the menu for the map (using the down arrow at the upper right corner of the map). Click on Title to remove the title from the dashboard. ![Fig_28: Removing Title from Map](images/fig_28.png)

[Return to Top](#about)

### Filtering on the Dashboard
12. In order to make our dashboard more interactive, we can filter other data based on what the user has selected on the map. Go back to the menu for the map and select use as filter. ![Fig_29: Use as Filter](images/fig_29.png)Now, when you select a state on map the other visualizations adjust to just include that state's data. You can also select multiple states by using the Command key(Macs) or Control key (Windows).
13. We also want to expand our year filter to apply to the map and the bar graph. To do this, click the down arrow on the year box. Select Apply to Worksheets and choose Selected Worksheets. ![Fig_30: Apply Filter to Selected Worksheets](images/fig_30.png)
14. In the pop-up window that appears, check Violent Crime Breakdown or whatever you have named your bar graph. Click OK.
15. Test your filters to make sure that they are functioning as expected. 

[Return to Top](#about)

### Adding Other information

16. You can add supplementary information to you dashboard to give context or make it more useable. On the bottom left, you should see a section titled objects with a variety of options. ![Fig_31: Objects section](images/fig_31.png) We are going to insert some text boxes for additional information. Let's start with adding information about our data source. 
17. Double click Text under the Objects section. In the box that appears enter information about the data source. In this example, we will enter "Data from the Uniform Crime Report, U.S. Department of Justice, FBI. Data Notes: https://oudsl.github.io/tableau-workshop/data/data-notes.html" Click OK to save the Text box. 
18. The text will automatically appear in the top left corner. Use the menu (click the down arrown at the top of the box) to make the text box floating, select the floating order bring to front, and reposition it. 
19. We also want to add some instructions for using the year search box. Let's hide the year label to give us more space. Click the menu on the year box and select show Title. 
20. Now, add an addition text for instructions. Double click on text under Objects in the bottom left corner. Enter your instructions. Make the box floating and bring to front. Then, position it where you would like. 
21. You may also want to add an addition box to give yourself credit as the creator of this visualization. 

[Return to Top](#about)

## Sharing Your Visualizations
1. We are going to walk through how to share your visualizations through Tableau Public. If you are using Tableau Desktop (this is what you have if you are using the academic trial), you will have more options.
2. In the top left of your window, select the save icon (floppy disk) ![Save icon](images/fig_33.png)
3. In the pop up window that appears, enter your Tableau user name and password. If you do no have account, go ahead and click the link to create one. 
4. After you have entered your credentials, your visualization will save. You may get a message letting you know it is being uploaded to the Tableau Public Server. 
5. Once it is saved, a new tab will open in your browser. Now, you can configure what people can access. 
6. Click edit details in the top right of the visualization open in your browser window. ![Edit Details](images/fig_34.png)
7. You can update your title, a permalink to your website where you plan on embedding your visualization, and add a more robust description. 
8. Under toolbar settings, you can control what appears on the viewer's toolbar. Note: you can give access to the data if you want that to be available. For our example, we will make the data available. 
9. Under other settings, you can choose to show workbook sheets as tabs. If you deselect this options, viewers will see whatever what displayed when you saved to Tableau public. For this example, we will deselect this option so our viewers will only see the dashboard. ![Editting Details on Tableau Public](images/fig_35.png) Click Save to apply your changes. 
10. Tableau Public makes it easy to share your visualization on social media or embed it into a web site. Beneath your visualization on the right side, you should see a Share buttom. Click that will get you an embed code, a link, and options to email, tweet or facebook your visualization. ![Sharing Viz](images/fig_36.png)

[Return to Top](#about)
