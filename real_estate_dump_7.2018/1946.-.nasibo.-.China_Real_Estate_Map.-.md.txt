# China_Real_Estate_Map
Files to create a D3 map of Chinese housing price changes from 2011 to 2016

China_Res_Housing_Monthly_Prices.csv is a file containing data on monthly residential real estate price monthly price changes. Each data point in indexed to the previous month. So a data point of 103.4 means that that city's real estate prices went up by 3.4% over last month. 

China_Housing_Index.R reads in China_Res_Housing_Monthly_Prices.csv and indexes the data to December 2010. It also grabs the latitude and longitude of each city with the geocode() command. It then creates a .csv file called Indexed_China_Housing_to_April_2016.csv. IMPORTANT! do not open and save this new csv file in excel, excel will change the date format and then it won't work with the index.html (D3 map) file. Never use excel. 

index.html is the code for the D3 map of Chinese real estate price changes. A static image of it is provided in this repository as Final Map (Static).png. This index.html file also contains the css for the map in the top section of the code. 

To open all the files in chrome put them in the same folder. Then in the terminal open a python simple server by typeing "python -m SimpleHTTPServer $ 8888", then in Chrome go to http://localhost:8888/ where you can direct yourself to the folder containing all the files. 

Any advice on how to improve this code or process would be appreciated! 
