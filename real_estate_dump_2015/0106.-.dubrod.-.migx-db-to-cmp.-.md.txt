migx-db-to-cmp
==============

**How to create a MODX Custom Manager Page with MIGX DB**

This example is about building a Real Estate Map with Category Filter and Polygons so it covers a few extra features.

We assume you have already Installed MIGX via Package Manager

-----

##1. Create a holding Template Variable
 - define your base name, this example is "interactivemap"
 - TV name = **base_name**
 - TV Input Type = migxdb
 - Configuration = **base_name**

![TV Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/tv-setup.png)

##2. XML Schema
 - Create your XML schema, its a basis for inputs to the Database. 
 - Use the example in this repo and strip out things you don't need

##3. MIGX Package Manager Tab
 - Package name = **base_name**
 - CLICK "Create Package" Button
 - CLICK "XML Schema" Tab
 - PASTE your XML Schema
 - CLICK "Save Schema" Button
 - CLICK "Parse Schema" Tab > "Parse Schema" Button
 - CLICK "Create Tables" Tab > "Create Tables" Button
 
##4. MIGX Tab

   - **Settings**
     - name - **base_name**
     - unique MIDX id - **base_name**
 
   - **Formtabs**
   - Add 1 Item - I call mine "Published Items"
     - Inside that Add 1 item for each field in your schema file
     - typically just *fieldname* and *caption* is needed
     - you can also define your **Input TV Type** here (image | listbox | richtext | textarea | etc) 
     - listbox example: click Input Options Tab > Input Option Values > `Commercial==commercial||Single Family==single-family||Multi-Family==multi-family||Legacy==legacy`
     
![FormTabs Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/published-items.png)

   - **Columns**
   - First column must be "Header" > "ID"  & "field" > "id"
   - Enter additional columns you want to show from your input fields, *Page Title, category, etc*

![Columns Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/columns.png)

   - **MIGXdb-Settings**
   - Package = **base_name**
   - Classname = **base_name**

![migxdb Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/migxdb-setting.png)

   - **CMP-Settings**
   - Captions for the manager page

![cmptab Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/cmp-tab.png) 

##5. System > Menus
 - "Create Menu" for parent. Example: Lexicon = "Maps"
 - you might not want a parent
 - Create again, Lexicon = "Interactive Map"

![cmpmenu Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/cmp-menu.png)

 - action = index
 - parameters = &configs=interactivemap||migxconfigs||setup
 - **Note the base_name in that string**
 - namespace = migx

![menu Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/update-menu.png)

##Your Setup is Complete!

###Call it!

In your tempalte or whereever.

```
[[migxLoopCollection? &packageName=`interactivemap` &classname=`interactivemap` &tpl=`interactivemap-row`]]
```

###What the page looks like:

![menu Setup](https://dl.dropboxusercontent.com/u/4277345/MODX/migx-to-cmp/cmp-page.png)


