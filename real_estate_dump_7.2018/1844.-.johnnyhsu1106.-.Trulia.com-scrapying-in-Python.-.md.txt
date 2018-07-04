### Web Scarping in Python from www.Trulia.com/property/<br>
This code is to use Python 3.5 to parse the content of property from Trulia.com as the follows and photo of property.<br>
1. Features <br>
2. Public Record <br>
3. Price History <br>
4. Real Estate Trend <br>
This infomation will be stored as json. The code will use the Beautifulsoup Class mainly so before you run the code, you have to install the bs4 library first. Please unzip the beautifulsoup4-4.1.0.tar and run the follown command propmt in Windows or terminal in Mac<br>
```
> python setup.py install
```
In command prompt, run the following in command propmt as example <br>

a. output json file and photo <br>
```
> python webscrap_trulia.py properties.txt -a <br>
```
b. output json file only <br>
```
> python webscrap_trulia.py properties.txt -j <br>
```
c. output photo only (format jpg) <br>
```
python webscrap_trulia.py properties.txt -p <br>
```
Annotation:<br>

(1) properties.txt  is a txt file containing links from Trulia and each link is separated by newline character as attached file "properties.txt"<br>
(2) The filename of photo is the address of each property, each word separated by "-", like 830-E-Copper-St-Tucson-AZ-85719<br>
(3) The filename of json is the same as the filename of properties.txt, like properties.json <br>
(4) json format<br>

{  link A:
   { "Features": [  ] ,
     "Public Records" : [  ] , 
     "Price History": [ ],
     "Real Estate Trends": [ ] }, 
     
   link B:
     { "Features": [  ] ,
        "Public Records" : [  ] , 
         "Price History": [ ],
         "Real Estate Trends": [ ] },
         ..........
         .......... }    
