# agri-erpnext
A set of  agriculture modules for erpnext 
1. Land Assets (Tree# )

    Estate (the physical Farm). For a Company having more than one estate or farm and in multiple localities. Accounting wise, it is a factory within Assets.
    Division. Estate may be divided into divisions or may not be divided depending on the organisation structure. Generally its divided for operational efficiency. Accounting-wise, it is a factory warehouse.
    Field. Divisions are further divided into fields like field 1, 2 etc. This is for work allocation. Work is always allotted based on field nos. Accounting-wise it is a warehouse within the factory warehouse.
    Blocks Further divisions of fields. Soil, water and plant analysis can be done in specific blocks of a field. Work happens at a field level, encompassing several blocks. However progress can be assigned per block. Accounting-wise it is a child warehouse of the parent warehouse "Field".

Example:

    Company: Future Farming Enterprises Inc.
        Divisions: Atlantis Farm, Mulligan Farm
            Atlantis Farm (contains 2 fields)
                Fields: A, B
                    Field A (contains 7 blocks)
                        Blocks: 0100, 0101, 0102, 0103; 0201, 0202, 0203
                    Field B (contains 3 blocks)
                        Blocks: 0101, 0102; 0201
            Mulligan Farm (contains 3 fields)
                Fields: A, C, D
                    Field A (contains 4 blocks)
                        Blocks: lettuce, kale; spinach, spinach02
                    Field B (contains 9 blocks)
                        Blocks: 0101, 0102, 0103, 0104, 0107; 0201, 0203; 0301, 0304
                    Field B (contains 2 blocks)
                        Blocks: test-organic, test-regular

One would be able to refer to Atlantis Farm>Field A>Block 0103
2. Setup (Documents)
Estate or Farm Master.

    Parent is an Asset account.
    Name of estate
    Attached documents (proof of ownership, etc.)
    Coordinate options
        One placemark or coordinate or,
        Polygon defined in Google Earth or other GIS software (In such a way that the corners of the polygon are either uploaded directly as a.kml of the estate, or, if present and an option selected, aggregated from individual block or field polygons to create a temporary, single, large polygon to represent the estate. To be manipulated by JSON or similar in the ERPNext app. An option to download the data would be fantastic.

Division Master.

    Parent MUST BE an an Estate or Farm, which must be selected.
    Name of estate or farm
    Coordinate options
        One placemark or coordinate or,
        Polygon defined in Google Earth or other GIS software (In such a way that the corners of the polygon are either uploaded directly as a .kml of the division, or, if present and an option selected, aggregated from individual block or field polygons to create a temporary, single, large polygon to represent the estate. To be manipulated by JSON or similar in the ERPNext app. An option to download the data would be fantastic.

Field Master.

    Parent MUST BE a division. If no division exists, one is created named exactly like farm or estate.
    Blocks created from the field master will inherit the most recent field master properties such as soil analysis, soil texture, placemark generated from field loaded polygon)
    Name (text)
    Location
    Coordinate options
        One placemark or coordinate
        Polygon defined in Google Earth or other GIS software (In such a way that the corners of the polygon can be aggregated with other field or block polygons to create a temporary, single, large polygon to represent field, division or farm. This can be uploaded in .kml or other format, to be manipulated by JSON or similar in the ERPNext app. An option to download the data would be fantastic.
        Size + UoM (among others: sq meter, sq feet, acres, Ha, etc.) This is determined by loaded polygon, or if absent, MUST be entered by user manually.
    Soil Texture values for field as a number. The resulting proportion will yield the textural classification as per Soil Texture Map. A nifty addition would be the triangle graph displaying the soil texture classification with a marker on the graph, using the numbers below. The graph should automatically update as numbers are entered. The graph should be exportable in a .jpg or .pdf or by using reports.
        date
        % Sand
        % Silt
        % Clay
    Color
    Soil analyses (child table)
        date
        pH
        ECEEC
        UoM (for the results)
        N, P, K, Ca, Mg, S, Fe, Mg, Cu, Zn, Mn, B, Mo

3. Crop Cycle

A crop cycle is a combination of activities and inputs, that occurs in between two dates. There can be many crop cycles on each block, but never overlapping on the same block. This can yield information on block availability for efficient use of agricultural real estate.
Crops can be:

    Perennial: Planted once, harvested continuously (ex. Bananas, Rubber)
    Period based: Planted once, harvested once. They can be
        Long term (2-3 years)
        Short term (7 days) Regardless of the class of crop, both perennial and period based crops are "work in progress" Where the manufacturing process begins on one date, and ends on another. In between, one can harvest several times, for those plants which are perennial, or plants whose harvested product regenerates on the same plant, such as Basil, which can be harvested (pruned) several times until the stock is too old and must be completely harvested, ending the particular crop cycle.

Crop Cycle creation page:

    Location (Single or multiple blocks or fields)
    Crop (Select from a table of available crops)
    Harvest objective (Select from a predetermined list of crop harvest objectives, which will assign activities for harvesting as per the harvest objectives)
    Beginning method (This is used to select a predetermined set of activities for each crop cycle, customizable by user)
        Planting (if selected, a planting date is created, and a new planting activity opens with preloaded tasks and inputs, of course, customizable)
        Transplanting (if selected, a transplanting date is created, and user is prompted for input block or field for warehouse transfer. A new transplanting activity opens with preloaded tasks and inputs, of course, customizable)
    Beginning date (defaults to today, but can be set to another date in the past or future)
    Estimated final harvest date (Depending on the harvest objectives, it estimates when the crop cycle ends)
    % overrun per cycle (a factor that helps in adjusting each cycle's duration for a longer period) (can have limits set by administrator)

Crop Cycle editing page:

    Can edit everything above, plus

    Add activity (Select an activity to be added to the crop cycle)
        Harvest (Generates a transfer to a sale warehouse. Sets warehouse expiration date before total decay of plant products.
        Select products harvested (Type, Quantity x UOM) Ideally, select from a table, or add on the go.
            Each harvest can yield different products. For Basil, one can harvest Microgreens, Baby leaves, Large leaves leaves

    Lbs, Kgs, Units x Quantity

one harvest can lead to several type of products. Example, we harvest oranges, and we get oranges Large, oranges Medium and oranges Small (each one are a different item)

    End crop cycle date (Actually ends the cycle, using today's date by default, or allowing another date entry.
    End method (Select wether you harvested or the crop failed)
        Harvest (Generates a transfer to a sale warehouse. Sets warehouse expiration date before total decay, which is used to alert user of inventory pending for shipping.)
        Crop failure (Generates a transfer to an "crop failure" expense account, where the inputs that were expensed during the cycle are transferred to. Labor costs are estimated here too.)

Once a crop cycle has been created, one can begin entering data activity according to sequences that pre-load with each cycle, or create activities manually.
Activities

    Beginning on a specific date, and ending on a future date. Each crop is comprised of separate activities. At a minimum, each crop cycle needs to have these activities preset:
        Planting (obligatory, unless plants are transplanted, in which case, Transplanting is obligatory)
        Intermediate Harvests
        Final Harvesting (obligatory to end the crop cycle)

A typical crop cycle would look like:

    Planting (obligatory, unless plants are transplanted, in which case, Transplanting is obligatory)
    Irrigation
    Transplanting
    Irrigation 2
    Agrochemical application
    Harvesting
    Final Harvesting (obligatory to end the crop cycle)

Crop Cycle Activity (Any activity, including harvest)

[it should be instead of the item {products} in manufacturing] ?? At a minimum, each crop cycle activity should have: - Type of activity: insecticide application, irrigation, harvest, final harvest, planting, transplanting - Crop (lookup to crop location, where crop cycle shows breadcrumb location in farm Division>Field>Block) - Date and time of activity start (dd-mm-yyyy hh:mm) UTC? - Date and time of activity END (dd-mm-yyyy hh:mm) UTC? - notes or comments: details about the activity. - attach images or documents for activity. - LABOR - Select from Employees - Add role for each from dropdown (Supervisor, field 1, field 2, field 3) - Add main task for each from dropdown or new entry (Tractor driver, Harvester, Irrigator) - INPUTS - Select from categorized warehouse and add inputs: Type, Quantity x UOM - Example: Water, 20 x Liters, NPK Fertilizer 45 x Kilograms - Warehouse categorized or filtered by inputs, fertilisers, fungicide, insecticide, adjuvants, Biological products - Once created, it estimates labor cost and input cost, adding it to the tally that will be totalled at the end of the crop cycle to report on particular crop cycle costs. It removes inputs from the warehouse upon creation, and charges hours only to crop cycle. Payroll is calculated from entry to exit time per day, at a determined rate. If it is a harvest activity, user must select the products from the harvest, Qty + UOM. These numbers will got to a storage warehouse.

Each activity should be able to save a "template" activity, such that crop cycles can refer to these template activities.

Inputs:

A crop cycle will have agricultural and labor inputs, and will use tools. For every Activity, inputs must be given to help in estimating the cost of the crop. As an example, one activity, planting, would involve at a minimum:

    Agricultural Inputs (to be selected from Ag warehouse, a warehouse whose items are objects from purchasing)
        Substrate
        Water
        Planting Trays
        Other Expendables (gloves, masks, etc.)
    Tools /Machinery (To be selected from Tools/Machinery warehouse, a warehouse whose items are objects that depreciate)

4. Dependencies
Crop table

    Name
    Scientific name
    Attached document (such as crop specifications, such as variety details)
    Image
    Harvest objectives and average days to objective. Each crop can serve for different harvest purposes. Since yields are dependent on the harvest purpose, and the harvest purpose is a function of time, several harvest purposes must be defined. A default purpose should be "Final harvest", where the plant is completely harvested. Each harvest, including the final harvest can yield different varieties of products (A tree can yield fruit and wood). This is easier understood with an example. Basil seeds can serve for at least three harvest objectives:
        Microgreens: From planting to Final harvest, 15 days. Average yield: 2 Oz. microgreen basil sprouts per 3 gm of seed.
        Baby basil+big leaves: From planting to first baby basil harvest, 20 days. Avg yield .04 Oz. baby basil leaves per plant(seed). To second harvest (pruning) 60 days Avg yield 1 Oz. baby Basil leaves per plant(seed). To (n < Final Harvest) harvest 90 days. Avg Yield 2 Oz. basil leaves per plant(seed) + 1 Oz. baby basil leaves per plant. To final harvest 120 days. Avg yield 1.5 Oz. per plant (seed). Notice that for the "complex" harvest objective, at 90 days we can harvest 2 Oz. large basil leaves per plant, and an additional 1 Oz. baby basil leaves per plant. Each harvest objective table shall have: Harvest objective for Baby basil+big leaves separated by commas, first line is header, each additional line is data:

Harvest_Number,Days Since Planting,Product_1,Yield_1,UOM/seed_1,Product_2,Yield_2,UOM/seed_2,IsFinalHarvest? Harvest 1,20,baby basil,.04,Oz.,,,,NO Harvest 2,60,baby basil,1.0,Oz.,,,,NO harvest n,,90,basil,2.0,Oz.,baby basil,2.0,Oz.,NO Harvest n+1,120,basil,1.5,Oz.,,,,YES

This table is important, because when one is picking an activity from the Crop Cycle Activities, it shall be populated by the default activities, and THESE activities. Perhaps even as a reminder. Displaying these on gantt charts would be great.
Activity templates table

A table where activity templates can be saved, for crop cycle referral in the future, as activities are created.
Crop cycle templates table

A table where crop cycle templates can be saved, for referral in the future. Mainly storing the duration from start to finish, according to particular crop and crop objectives.
Agricultural inputs

[just another kind of item of type “raw material”]

    Type of product (Fertilisers, Fungicide / insecticide, adjuvants, Biological product)
        if fertilizer needs % composition for each nutrients
        if fungicide, insecticide, adjuvant need the name of the active ingredients with UoM per UoM
    Name
    MoA group
    Packaging type (dropdown menu with possibility to add more)
    Quantity in package (number)
    UoM (lookup for UoM)
    Labelled application rate (UoM per UoM)
    Link to label (website link, link to a file)
    Link to safety sheet

    Labour Master: All labour data and class of employee – permanent, temporary, casual etc.. The labour is estate specific and hence the master has to be estate specific. We cannot have a labour master for the company as a whole. (part of HR Module)

    Staff Master: Similar to labour master

    Asset Master: All fixed assets and their follow up through out the life cycle

    Allowances Master: Wages and salaries include various components of allowances which need to be flexible as they change from time to time, season to season etc..

3. Activity Reporting

    Time Logs (extending existing functionality - work done etc)
    Crop Cycles in calendar (start to end date)
    Crop Cycles in maps (with selector for crop cycles running right now, crop cycles to end before x date
    Activity Master
    Calculate Wages
    All records tagged to a land asset
    time logs for machines, task work. tagged to a land asset meaning?
    labour report - attendance, work done for a certain period consolidated for full labour force at estate level and also individual labour wise report.
    we need to generate all reports with comparative data for the same period last year or for two years. if this is possible it would help a lot. for eg. on a daily basis we get the crop figures for the day, for the month, for the year. The same is compared with the current year last month and also for the last year. please give it a thought.

    Field
        Name of field.
        Location
        Size + UoM (among others: sq meter, sq feet, acres, Ha, etc.)
        Coordinates (upload a set of coordinates)
        Crop history (Child table related to previous crop on that field)
            Date planted, date harvested, Crops name, crops variety, Yield per UoM
        Soil analyses history (child table)
            date, N, P, K, Ca, S, Fe, Mg, Cu, Zn, Mn, B, Mo,

    Crops Nutrient program (analytics)
        Absolute values of fertilisers added Vs time
        Drop down to select Crop, to select date, to select field
        check box on:
            type of application (drench, foliar, overhead, hydroponic)
            type of nutrient (N, P, K, S, Ca, etc.)
            Cumulative values of fertilisers added Vs time
        Drop down to select Crop, to select date, to select field
        Calendar (with summary of all agrochem applied) - Gantt style
            check box to select any kind of products (Fertilizers, fungicide, insecticide, adjuvants, Biological products) + different color for each type of product.

    Crops expenses (analytics)
        Absolute values of Direct Costs Vs time (bar chart with different color for type of costs such as tasks, fertilizers, fungicide, adjuvants, Biological, etc.)
        Drop down to select Crop, to select date, to select field
        Cumulative values of Direct Costs Vs time (bar chart with different color for type of costs such as tasks, fertilizers, fungicide, adjuvants, Biological, etc.)
        Drop down to select Crop, to select date, to select field

4. Weather Reporting

    Weather Reading (type of measure, value) Unit of measure to be flexible. Eg. we measure rain in one place in cents and inches and in another place in mm.

5. Inventory Management

    Planning (fertlizer etc) - BOM? should be fine
        BOM should have a date on each item added.
    Harvesting (Stock Entry) some crops are harvested and sold immediately. eg. tea leaves, fruits etc. how do we handle the same?
    Plant nursery barcode labels for pots
    All records tagged to a land asset so that reports can be made

6. Checklists

    Checklists for various activities like Nursery, Transplanting, etc.
    Checklist Template
    Checklist
    Tagged to Land Asset good idea. we can expand the scope to other activities too like spraying, fertilizer application etc.. can be kept optional so users can decide if they want to use it or not.

HR

let the hr data be estate/ farm wise from which we can generate a company wise consolidated report if required. all employees can be tagged to a particular estate/ division
Fleet Management

details of vehicle usage - kms run / day, fuel consumption, service records, major repairs, hours, etc. something similar for machinery too like sprayers, weeding machines, pruning machines, chain saws etc.
Other

    Field Operation Diary: More of a report complied with all the above data recorded. Gives an idea what is happening for a day. This should have details for all the fields, divisions etc. The farming operation in totality.

    Post Harvest Management/ Production: In case value addition is done at the farm itself. I think the current software can handle this part.

    Planning of season and daily work for each crop: Like a calendar/ scheduler which helps managers plan the work.

    Work scheduling: Allotment of work based on the planner

    Calculators: labour required for a particular task, spraying calculators, fertiliser calculators

Reports:

    Crop cycle report in gantt format (shows activities, estimated harvest date calculated from selected crop, labor, inputs similar to a video editing screen, with "layers" representing the start and end of each activity)
    Crop cycle overview in map (shows the polygon for the block or field area in such a way that one can select crop cycles active now, or crop cycles about to end in x days, or crop cycles about to begin in x days. Another option would be to select week blocks in a slider and have it show in color coding which blocks or fields will be with a crop cycle beginning, crop cycle about to end, or no crop cycle.
    Crop variety report (shows crops in map by variety)
    Irrigation report
    Work report: separate report for each work activity like plucking, spraying etc..
    Rainfall and other weather data report
    Labour attendance report
    Harvesting Report

Map reports details (incomplete requirements)

    Show an aggregate of all fields and blocks created, displayed on a google map or similar, with a clickable layer that opens the related record, using these display options:
    Option 1. Show one entire polygon representing the entire farm, sourced from Geographical polygon data at field or block level.
    Option 2. Show the division polygons representing the divisions, sourced from geographical polygon data at field or block level.
    Option 3. Show the field polygons representing each field, sourced from geographical data at this level (field) or block level.
    Option 4. Show the block polygons representing each field, sourced from geographical data at block level. (This is the furthest drill down to be displayed in this document)

