# California Water Rights Dataset - Version 0.0.5
--------------------------------------------------------------------------------

THIS IS A WORK IN PROGRESS. We will note when this document is final. 04/28/2014 -- Laci Videmsky

--------------------------------------------------------------------------------

The State Water Resource Control board maintains a dataset of Water Rights, Statements of Diversions, Permits, and Licenses for water use in the State of California. This includes appropriative water rights, some riparian water rights, some groundwater recordations (i.e. well readings, probably mostly in adjudicated basins), and possibly some listings of some tribal water rights. As you might expect, this does not include illegal diversions.

We are working to create a dataset that is developer-friendly, accurate, up-to-date and well-documented. We believe this will help to speed communication and promote clarity and innovation about water usage in the State. We began in December 2012, and are doing more improvements in Summer 2013. Please watch this Github repository for updates. We would like to have a great & re-usable dataset worked out by January 2014.

--------------------------------------------------------------------------------

## Details & Stats about the Water Rights Dataset

### Computer systems used by the State of California
The state uses the eWRIMS system (a custom built CMS) and also an ArcGIS server to maintain geographic information.
eWRIMS:
ARCGIS server:

#### Number of Water Right Applications and Records
About 50K

#### Approximate number of active water rights in California (2013)
* 5000?

#### Number of Statements of Diversion
* About 40K records total. 
* Statements of Diversion have been required by law since 2009.
* A water right holder can submit several yearly reports
* Number SOD records not digitized yet by the SWRCB: 6000 (mostly for 2012?)

#### Frequency of updates
Weekly, about 10-100 records per year.  (Question is this about right? Seasons?)

#### Comprehensiveness of the dataset
This is all of the digitized data that the State has 

#### Accuracy
The State strives to be comprehensive.

We are also striving to mirror the State's dataset and eventually get the state to host data for all of us. If you have legal questions about water rights, please refer to the State's system and not us, we are providing this information as a convenience and for exploring new opportunities in communicating about water rights.

As a State, we have passed laws that require water rights holder to report their usage, and in come cases failure to report requires that water rights holders pay fines. These fines go to supporting the SWRCB (???), ___ including efforts to maintain datasets (???) Trained staff help water rights holders fill in information about their water right, which includes information from various water meters, in some cases a watermaster physically unlocks a diversion, the location of points of diversion is required to be surveyed, information about water conservation is reported. 

Water rights range from small domestic water rights to full scale water rights holdings by municipalities that supply a city with water, or water districts that supply a group of farmers with water. As such, the larger water rights holders usually have lawyers to help them fill in details, and the smaller holding are a little bit less precise, but not always.

When there is not a recording or a diversion is illegal there is, as you might expect, no data.

--------------------------------------------------------------------------------

#### How we are improving the data:
* Seeking real time data stream, or at least a quarterly updated dataset.
* Documenting the various fields in partnership with the State Water Resource Control Board
* Attempting to get dataset into data.ca.gov

### How to Download the data
We are working on a MongoDB database in geoJSON format that can be readily downloaded by developers, and are working to document the fields in the dataset, since water rights are complex and there is significant legal meanings.

[Bulk Download](https://www.dropbox.com/sh/drxi19pstribdsq/HrRgu6Gllm "Bulk Download")

### Updates
We would like to update the dataset at least twice per year, and eventually monthly or to have a real-time updated dataset available on http://data.ca.gov. 

### How we are working
As a small community of water-interested computer programmers, we are working to recommend what we need to known and access in order to use the valuable water rights data. 

### Quality Assurance and Tests
We are considering how we test and verify that our information is accurate.

### Github
To collaborate, we are putting the documentation, data & processing tools into Github, a public & social place where programmers collaborate on code or data projects. 
* http://github.com/NewCaliforniaWaterAtlas/data-water-rights

### License
New California Water Atlas, and data adapted and shared by the [New California Water Atlas](https://www.dropbox.com/sh/drxi19pstribdsq/HrRgu6Gllm "New California Water Atlas") is licensed under a [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/deed.en_US "Creative Commons Attribution-ShareAlike 3.0 Unported License").

--------------------------------------------------------------------------------

#### Workgroup / Team

##### People
* Chacha Sikes (New California Water Atlas)
* Ted Grantham (UC Davis Department of Watershed Sciences)
* Phil Crader (State Water Resources Control Board) He is advising us and answering our questions, helping us make sure this information is accurate.
* Laci Videmsky (New California Water Atlas)

##### Groups
If you are interested in helping to make water rights data better in California, please contact the New California Water Atlas at info@statewater.org. 
* Blog and file sharing: http://ca.statewater.org/water-rights
* We are also thinking about starting a Code for America Brigade for California State Water or other Natural Resources.

#### Sponsors
New California Water Atlas: Making Water Understandable in California
http://ca.statewater.org  @CAStateWater

Work done as part of California Water Rights project, incubated by the Resource Renewal Institute http://rri.org with financial support from Patagonia. http://patagonia.com.


--------------------------------------------------------------------------------

### What is the Water Rights data useful for?
This data can be used for creating models of water usage in the state, for visualizing usage across the states, for creating more maps and visualizations of water rights and usage in the state. Similiarly, we hope that our process of working to clean up and make datasets friendly for re-presenting on the web, we hope this process to be something we can inspire others to take on for other important datasets.

#### Sample applications
California Water Rights interactive: http://ca.statewater.org/water-rights
Launched April 2013. Update planned for August 2013.

### Supplementary Datasets
These datasets help tell the story of water rights.
* Unimpaired flows
* Fully Appropriated Streams
* Stream Gauges (USGS (machine readable) 400 sensors & CDEC (NOT machine-readable) 400 sensors)
* National Hydrography Dataset
* Cropscape
* Landsat
* Others?

--------------------------------------------------------------------------------
## Fields


Field Template:
### machine_readable_name | Human Readable Field Name
* Description: What the field is for
* Definition: Technical definition
* Format: string, machine-readable (alphanumeric, no spaces, etc), Integer, etc.
* Examples: Samples, along with the syntax format of the fields {{description}}_{{number}}  (ignore the braces {{}} )
* Notes: Notes about this field, used for complex fields
* Proposed changes: Ideas about ways to better represent the data in future versions.
* Values: some of the fields have specific kinds of values that have important meaning (ex. water right status) - we will note where there is a list of the values and their definitions.

### Priority of fields
* Unique Identifiers
* Basic Fields (Name, geographic location, face value amount, diversion type (storage, diversion))
* Amounts of water (formats -* cfs, afy)
* Holder information (address, etc)
* Location information (watershed details, mostly from ArcGIS)
* Relationship to other water rights (pod_id)
* Dates (time of first use) -* how legal is that information? applied, received * revoked
* @TODO timeframe? months of use
* Data from Statements of Diversion (use code, conservation methods, monthly breakdown of use (different numbers), description)
* @TODO Add description of Permits, need sample data

### About this fields

* We are filling in fields by priority. There are about 200 possible fields - so it will be a lot of work to do them all, so we will focus on the most important ones, and can update the more obvious ones (such as "billing address") when we have time, or if there is important information to know about those fields.
* Fields are compiled from ArcGIS & eWRIMS & a exported database dump of California records (Winter 2012) - this is why there are duplicates


### Sample Records
These are examples of the data we are compiling
@TODO Add samples
* GIS data export from SWRCB
* XLS record for one Water Right Application
* Statements of Diversion
* License (?) (digital & pdfs)
* Permit (?) (digital & pdfs)
* Photos of records not yet digitized


----------------------------------------------------------

## Working Definitions & Our Questions
We have been able to work with the SWRCB as well as to meet lawyers to learn more about water rights. It can be very technical, and calling things by the wrong name can stress out water rights holders if you are not careful. Water in California is contentious. We are learning ourselves.

* Water Right  (well documented)
* Appropriative Right (well documented)
* Riparian Right  (well documented)
* Groundwater Recordation (on website?)
* Stream * how big is it? * measured in volume? How much?
* River * how big is it?
* Do springs have diversions? Are they supposed to? Ex. Arrowhead drinking water springs


#### How is a Face Value Amount calculated?
This is a conservative estimate of the total amount of water allowed. This is NOT usually how much gets allocated.

#### How is the actual amount of water allocation determined?
We don't know yet. We are trying to find out.

#### How is water usage measured?
Meters… what else?

#### Read more about Water Rights
The SWRCB maintains a FAQ page: http://www.waterboards.ca.gov/waterrights/board_info/faqs.shtml


### Use Codes
* Format: String
* How water is used
* Can be multiple values per water rights application? (???)
* Values:

Stockwatering                                   10522
Irrigation                                      9644
Domestic                                        5472
Fish and Wildlife Protection and/or Enhancement 2191
Recreational                                    1391
Fire Protection                                 1220
Other                                           579
Dust Control                                    541
Power                                           505
Municipal                                       361
Frost Protection                                344
Industrial                                      258
Fish Culture                                    120
Mining                                          89
Heat Protection                                 65
Incidental Power                                21
Milling                                         15
Snow Making                                     6
(blank)                                         12178

@TODO is this all of them?
@TODO These need definitions… though they appear to be self-explanatory.
@TODO Are the blank entries our mistake or is there not data?

### Water Rights Status
This the the status of the water right in the state
Claimed                         15065
Licensed                        12027
Certified                       5286
Inactive                        3433
Permitted                       2337
Revoked                         1562
Cancelled                       997
Pending                         977
Registered                      696
Claimed - Local Oversight       683
State Filing                    183
Active                          113
Non Jurisdictional              105
Rejected                        22
Adjudicated                     20
Closed                          13
Temporary                       10
Waste Water Change Order        1
(blank)                         1992

@TODO Need definitions
@TODO Need to confirm which ones of these count towards actual water use in the state.

### Water Rights Type
Appropriative                 18564
Statement of Div and Use      14628
Stockpond                     5514
Groundwater Recordation       3396
Federal Filings               1973
Small Domestic Reg            856
Not Determined                185
Livestock Stockpond           129
No Right Required             109
Temporary Permit              93
Cert of Right - Power         37
Pre-1914 Claim of Right       19
Section 12 File               16
Riparian Claim of Right       1
Waste Water Change            1
(blank)                       2

@TODO These need definitions

### Organization Type
Individual                    16383
Corporation                   15427
Government (State/Municipal)  3905
Federal Government            1835
Trust                         1211
Limited Liability Company     1131
Organization/Association      790
Limited Partner               200
Partnership or Co-owners      122
Estate                        22
Joint Venture                 3
Receivership/Fiduciary        3
(blank)                       4490

### POD Status
Active                        39479
Inactive                      3019
Revoked                       1672
Canceled                      1128
Removed                       34
(blank)                       191

### Year first use
1900's-2013
@TODO Some values are incorrect (ex. 1040, 4897) Is this an artifact from the import?


--------------------------------------------------------------------------------
--------------------------------------------------------------------------------
** FIELDS **
--------------------------------------------------------------------------------

## Fields - Unique Identifiers

### id | ID
* Description:  NWCA Field Addition. Application POD ID, individual geographic location
* Definition: This is the location of a point of diversion. Could be one of several PODs.
* Format: alphanumeric, with underscores {{ApplicationID}}_{{POD value}}
* Examples: C003105_01, C003105_02

### properties.pod_id | Point of Diversion ID
* Duplicate fields? * "pod_number" * some compiled data are the same. Which one is better?
* Description: 
* Definition: 
* Format: 
* Examples: "01", "02"
* Notes: A water right (based on its Application ID) can have several geographic locations. These are usually built
water diversions that lead to different locations, such as storage facilities or an agriculture field.

### properties.water_right_id | Water Right ID
* Description: A value from the eWRIMS system
* Definition: 
* Format: 
* Examples: 
* Notes: This field is necessary for correctly looking up the urls to statements of diversions and water reports. In the Mongo DB there may be some mismatches due to the way information had to be retrieved.

### properties.application_id : Application ID
* Description: The unique record id for one individual water right with a specific face value amount.
* Definition: 
* Format: 
* Examples: "C003105"

### "application_pod" : "C003105_01",
* Description: 
* Definition: 
* Format: 
* Examples:

### "ewrims_db_id" : "13976",
* Description: 
* Definition: 
* Format: 
* Examples:

### "appl_id" : "C003105",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "podid" : "3912",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "permit_id" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:


--------------------------------------------------------------------------------

## Fields - Record ID

### kind | Kind
* Description: NWCA MongoDB specific field for storing object record
* Definition: A description of the kind of record, used in each record.
* Format: string
* Examples: "right"
* Proposed change: "water_right"

--------------------------------------------------------------------------------

## Fields - Metadata

### name | Name
* Description: Name of the "Holder Name", who holds the water right. Might not be the same as the Primary Owner.
* Definition: The name of the holder, a person, organization or other entity.
* Format: string, alphanumeric
* Examples: JOE  ALBERTA

### "use_code" : "Stockwatering",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "organization_type" : "Individual",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "pod_status" : "Active"
* Description: 
* Definition: 
* Format: 
* Examples: 
* Notes: This is from ArcGIS

### "status" : "Certified",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "water_right_status" : "Certified",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "first_name" : "JOE",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "holder_name" : "ALBERTA",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "primary_owner" : "JOE  ALBERTA",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "primary_owner_entity_type" : "Individual",
* Description: 
* Definition: 
* Format: 
* Examples:

### "entity_type" : "Individual",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

###  "name_type" : "Primary Owner",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "last_update_user_id" : 9,
* Description: 
* Definition: 
* Format: 
* Examples: 

### "date_last_updated" : 1191046438000,
* Description: 
* Definition: 
* Format: 
* Examples:

### "agent_name" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "agent_entity_type" : "",
* Description: 
* Definition: 
* Format: 
* Examples:

### "mailing_street_number" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "mailing_street_name" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "mailing_address_line2" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "mailing_city" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "mailing_state" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "mailing_country" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "mailing_zipcode" : null,

* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "billing_street_number" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

###  "billing_street_name" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "billing_city" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "billing_state" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "billing_country" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "billing_zipcode" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "phone" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_status_new" : "Migrated from old WRIMS data",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_population" : "0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "water_right_description" : ""
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### source | Source
* Description: NWCA Field Addition Web url of the source of the data record
* Definition: Should point to the URL about the original dataset
* Format: url
* Examples: http://gispublic.waterboards.ca.gov/
* Proposed Changes
  * Change field name to "data_source" | Data Source
  * Add extra field pointing to page that describes the data conversion, example this github repository.
  * Merge with source_alt

### "source_alt" : "http://ciwqs.waterboards.ca.gov/",
* Description: NWCA Field Addition
* Definition: 
* Format: 
* Examples: 
* Proposed Changes
  * Make Data Source a multiple entry object.


--------------------------------------------------------------------------------

## Fields - Location Information

### "place_id" : 663256,
* Description: 
* Definition: 
* Format: 
* Examples: 

### "latitude" : 37.24426798,
* Description: 
* Definition: 
* Format: 
* Examples: 

### "longitude" : -119.70260375,  
* Description: 
* Definition: 
* Format: 
* Examples:

###  "range_direction" : "E",
* Description: 
* Definition: 
* Format: 
* Examples:

### "township_direction" : "S",
* Description: 
* Definition: 
* Format: 
* Examples:

### "range_number" : "21",
* Description: 
* Definition: 
* Format: 
* Examples:

### "section_number" : "8",
* Description: 
* Definition: 
* Format: 
* Examples:

### "section_classifier" : "",
* Description: 
* Definition: 
* Format: 
* Examples:

### "quarter" : "SW",
* Description: 
* Definition: 
* Format: 
* Examples:

### quarter_quarter" : "SE"
* Description: 
* Definition: 
* Format: 
* Examples:

### "meridian" : "Mount Diablo",
* Description: 
* Definition: 
* Format: 
* Examples:

### "northing" : "1912401",
* Description: 
* Definition: 
* Format: 
* Examples:

### "easting" : "6793775",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "sp_zone" : "3",
* Description: 
* Definition: 
* Format: 
* Examples:

### "township_number" : "8",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "trib_desc" : "",
* Description: 
* Definition: 
* Format: 
* Examples:

### "location_method" : "DD_NE",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "source_name" : "UNST",
* Description: 
* Definition: 
* Format: 
* Examples:

### "moveable" : "N",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "has_opod" : "N",
* Description: 
* Definition: 
* Format: 
* Examples:

### "watershed" : "AHWAHNEE",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "county" : "Madera",
* Description: 
* Definition: 
* Format: 
* Examples:

### "quad_map_name" : "O'NEALS",
* Description: 
* Definition: 
* Format: 
* Examples:

### "quad_map_num" : "JJ023 ",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "quad_map_min_ser" : "7.5",
* Description: 
* Definition: 
* Format: 
* Examples:

### "parcel_number" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "special_area" : null,
* Description: 
* Definition: 
* Format: 
* Examples:


--------------------------------------------------------------------------------

## Fields - Water Amounts & Physical Attributes

### face_value_amount | Face Value Amount
* Description: 
* Definition: 
* Format: 
* Examples: 

### "direct_div_amount" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "diversion_storage_amount" : "2.5",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "diversion_acre_feet" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "diversion_type" : "Direct Diversion",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "diversion_code_type" : "Diversion point",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "water_right_type" : "Stockpond",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Values: 
    Appropriative                 18564
    Statement of Div and Use      14628
    Stockpond                     5514
    Groundwater Recordation       3396
    Federal Filings               1973
    Small Domestic Reg            856
    Not Determined                185
    Livestock Stockpond           129
    No Right Required             109
    Temporary Permit              93
    Cert of Right - Power         37
    Pre-1914 Claim of Right       19
    Section 12 File               16
    Riparian Claim of Right       1
    Waste Water Change            1
    (blank)                       2

### "storage_type" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "pod_unit" : "Gallons per Day",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "well_number" : "   ",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "face_value_units" : "Acre-feet per Year",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "max_dd_appl" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples:

### "max_dd_units" : "Gallons per Day",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "max_dd_ann" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples:

### "max_storage" : "2.5",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "max_use_appl" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change: 


### "use_net_acreage" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_gross_acreage" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_dd_annual" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_dd_rate" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_dd_rate_units" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_storage_amount" : "2.5",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "pod_max_dd" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "source_max_dd_unit" : "","
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "pod_max_storage" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "pod_max_storage" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "pod_max_storage" : "0.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "source_max_storage_unit" : "Gallons per Day",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "pod_gis_maintained_data" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

--------------------------------------------------------------------------------

## Fields - Permits / Licenses / Seasonal Use

                
### date_received" : ""
* Description: 
* Definition: 
* Format: 
* Examples: 

### "date_accepted" : "01/06/1978",
* Description: 
* Definition: 
* Format: 
* Examples:

### "date_notice" : "",
* Description: 
* Definition: 
* Format: 
* Examples:

### "protest" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 

### "number_protests" : "0",
* Description: 
* Definition: 
* Format: 
* Examples:

### "year_first_use" : "1968.0",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "effective_from_date" : "09/15/1994",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "effective_to_date" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "issue_date" : "1979-03-26",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "construction_completed_by" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "planned_project_completion_date" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "permit_terms" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "term_id" : "0000021",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "direct_div_season_div_rate" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "storage_season_amount" : "2.5",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "direct_div_season_annual_amount" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "storage_season_begin_date" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "storage_season_end_date" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "use_seasons" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "direct_div_season_begin_date" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### "direct_div_season_end_date" : null,
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### direct_div_season_div_rate_units" : "",
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

--------------------------------------------------------------------------------

## Fields - Statement of Diversion
@TODO Move this to its own record type… will be easier to index and search.

### {{year}} : 2009
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:

### {{year}}.usage | 2009
* Description: From use code
* Definition: 
* Format: 
* Examples: "Other"
* Proposed change:

### {{year}}.usage_quantity
* Description: Has description of usage.
* Definition: 
* Format: 
* Examples: "6054 Ac. Waterfowl Habitat, and Rice Straw Decomp. "
* Proposed change:

### {{year}}.diversion_unit
* Description:  
* Definition: 
* Format: 
* Examples: "Acre-Feet",
* Proposed change:

### {{year}}.diversion_unit
* Description: 
* Definition: 
* Format: 
* Examples: 6466
* Proposed change:

### {{year}}.total_diverted
* Description: 
* Definition: 
* Format: 
* Examples: "Other"
* Proposed change:

### {{year}}.total_used
* Description: 
* Definition: 
* Format: 
* Examples: "Other"
* Proposed change:

### {{year}}.diversion_total
* Description: 
* Definition: 
* Format: 
* Examples: "Other"
* Proposed change:

### {{year}}.amount_diverted
* Description: 
* Definition: 
* Format: 
* Examples: "Other"
* Proposed change:  

### {{year}}.amount_diverted.January
* Description: 
* Definition: 
* Format: 
* Examples: "1028"
* Proposed change:    

### {{year}}.amount_diverted.Total
* Description: 
* Definition: 
* Format: 
* Examples: "6466"
* Proposed change: 

### {{year}}.amount_used.January
* Description: 
* Definition: 
* Format: 
* Examples: "1028"
* Proposed change:    

### {{year}}.amount_used.Total
* Description:
* Definition: 
* Format: 
* Examples: "6466"
* Proposed change: 

### year
* Description:
* Definition: 
* Format: 
* Examples: "2009"
* Proposed change:

### ewrims_db_id
* Description:
* Definition: 
* Format: 
* Examples: "13976"
* Proposed change:

### ewrims_form_id
* Description:
* Definition: 
* Format: 
* Examples: "37516"
* Proposed change:

--------------------------------------------------------------------------------

## Fields - Unknown

### "version_number" : "2.0"
* Description: 
* Definition: 
* Format: 
* Examples: 
* Proposed change:







--------------------------------------------------------------------------------
** END of FIELDS ** 
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------










## Install Mongo Database
--------------------------------------------------------------------------------
Mongodump file located here: 
https://github.com/NewCaliforniaWaterAtlas/watertransfers/tree/master/data/dump/watertransfer

This is the current MongoDB for the Water Rights interactive. 
* It is a database of geoJSON objects for each water rights record.
* About 50K records
* Filesize: About 139MB BSON (Mongo dump file format)

@TODO Document how to import mongodump file into Mongo
@TODO Rename to waterrights -- watertransfers is relic of earlier project idea.


## Install Mongo Database
--------------------------------------------------------------------------------
@TODO Sample Queries
@TODO Sample Collections and indexes



## Export Mongo Database as CSV file
--------------------------------------------------------------------------------
@TODO Document this better.
In general, the command is something like this:
mongoexport -d watertransfer -c database -f properties.application_pod,properties.name,properties.water_right_type,properties.max_dd_ann,properties.diversion_acre_feet,properties.organization_type,properties.use_dd_annual,properties.use_dd_rate,properties.use_dd_rate_units,properties.pod_status,properties.diversion_storage_amount,properties.direct_div_amount,properties.latitude,properties.longitude,properties.face_value_amount,properties.water_right_status,properties.issue_date,properties.use_code,properties.year_first_use --csv --out /Users/username/htdocs/folder/data/export/4_13_2013_a.csv 

@TODO Make list of all of the fields that could be exported (there are lots.)

## Sample geoJSON Record Object of a Water Right
--------------------------------------------------------------------------------

@TODO Add a few different examples: individual, state water project, municipal project, farm
@TODO Proposed Change: move Statements of Diversion into their own record format.

```json
{
        "id" : "C003105_01",
        "kind" : "right",
        "type" : "Feature",
        "coordinates" : [
                -119.70260375,
                37.24426798
        ],
        "geometry" : {
                "type" : "Point",
                "coordinates" : [
                        -119.70260375,
                        37.24426798
                ]
        },
        "properties" : {
                "id" : "C003105_01",
                "kind" : "right",
                "source" : "http://gispublic.waterboards.ca.gov/",
                "name" : "JOE  ALBERTA",
                "pod_id" : "01",
                "water_right_id" : "13601",
                "pod_number" : "01",
                "application_id" : "C003105",
                "direct_div_amount" : "0.0",
                "diversion_storage_amount" : "2.5",
                "diversion_acre_feet" : "0.0",
                "place_id" : 663256,
                "pod_status" : "Active",
                "face_value_amount" : "0.0",
                "diversion_type" : "Direct Diversion",
                "diversion_code_type" : "Diversion point",
                "water_right_type" : "Stockpond",
                "water_right_status" : "Certified",
                "storage_type" : "",
                "pod_unit" : "Gallons per Day",
                "first_name" : "JOE",
                "holder_name" : "ALBERTA",
                "organization_type" : "Individual",
                "application_pod" : "C003105_01",
                "township_number" : "8",
                "range_direction" : "E",
                "township_direction" : "S",
                "range_number" : "21",
                "section_number" : "8",
                "section_classifier" : "",
                "quarter" : "SW",
                "quarter_quarter" : "SE",
                "meridian" : "Mount Diablo",
                "northing" : "1912401",
                "easting" : "6793775",
                "sp_zone" : "3",
                "latitude" : 37.24426798,
                "longitude" : -119.70260375,
                "trib_desc" : "",
                "location_method" : "DD_NE",
                "source_name" : "UNST",
                "moveable" : "N",
                "has_opod" : "N",
                "watershed" : "AHWAHNEE",
                "county" : "Madera",
                "well_number" : "   ",
                "quad_map_name" : "O'NEALS",
                "quad_map_num" : "JJ023 ",
                "quad_map_min_ser" : "7.5",
                "parcel_number" : "",
                "special_area" : null,
                "last_update_user_id" : 9,
                "date_last_updated" : 1191046438000,
                "status" : "Certified",
                "ewrims_db_id" : "13976",
                "reports" : {
                        "2009" : {
                                "usage" : [
                                        "Other"
                                ],
                                "usage_quantity" : [
                                        " 6054 Ac. Waterfowl Habitat, and Rice Straw Decomp. "
                                ],
                                "diversion_unit" : "Acre-Feet",
                                "total_diverted" : 6466,
                                "total_used" : 6466,
                                "diversion_total" : "6466",
                                "used_total" : "6466",
                                "amount_diverted" : [
                                        {
                                                "January" : "1028"
                                        },
                                        {
                                                "February" : "0"
                                        },
                                        {
                                                "March" : "0"
                                        },
                                        {
                                                "April" : "0"
                                        },
                                        {
                                                "May" : "0"
                                        },
                                        {
                                                "June" : "0"
                                        },
                                        {
                                                "July" : "0"
                                        },
                                        {
                                                "August" : "0"
                                        },
                                        {
                                                "September" : "0"
                                        },
                                        {
                                                "October" : "0"
                                        },
                                        {
                                                "November" : "3703"
                                        },
                                        {
                                                "December" : "1735"
                                        },
                                        {
                                                "Total" : "6466"
                                        }
                                ],
                                "amount_used" : [
                                        {
                                                "January" : "1028"
                                        },
                                        {
                                                "February" : "0"
                                        },
                                        {
                                                "March" : "0"
                                        },
                                        {
                                                "April" : "0"
                                        },
                                        {
                                                "May" : "0"
                                        },
                                        {
                                                "June" : "0"
                                        },
                                        {
                                                "July" : "0"
                                        },
                                        {
                                                "August" : "0"
                                        },
                                        {
                                                "September" : "0"
                                        },
                                        {
                                                "October" : "0"
                                        },
                                        {
                                                "November" : "3703"
                                        },
                                        {
                                                "December" : "1735"
                                        },
                                        {
                                                "Total" : "6466"
                                        }
                                ],
                                "year" : "2009",
                                "ewrims_db_id" : "13976",
                                "ewrims_form_id" : "37516"
                        }
                },
                "source_alt" : "http://ciwqs.waterboards.ca.gov/",
                "date_received" : "",
                "date_accepted" : "01/06/1978",
                "date_notice" : "",
                "protest" : "",
                "number_protests" : "0",
                "agent_name" : "",
                "agent_entity_type" : "",
                "primary_owner" : "JOE  ALBERTA",
                "primary_owner_entity_type" : "Individual",
                "face_value_units" : "Acre-feet per Year",
                "max_dd_appl" : "0.0",
                "max_dd_units" : "Gallons per Day",
                "max_dd_ann" : "0.0",
                "max_storage" : "2.5",
                "max_use_appl" : "0.0",
                "year_first_use" : "1968.0",
                "effective_from_date" : "09/15/1994",
                "effective_to_date" : "",
                "entity_type" : "Individual",
                "name_type" : "Primary Owner",
                "mailing_street_number" : null,
                "mailing_street_name" : null,
                "mailing_address_line2" : null,
                "mailing_city" : null,
                "mailing_state" : null,
                "mailing_country" : null,
                "mailing_zipcode" : null,
                "billing_street_number" : null,
                "billing_street_name" : null,
                "billing_city" : null,
                "billing_state" : null,
                "billing_country" : null,
                "billing_zipcode" : null,
                "phone" : null,
                "use_code" : "Stockwatering",
                "use_status_new" : "Migrated from old WRIMS data",
                "use_population" : "0",
                "use_net_acreage" : "0.0",
                "use_gross_acreage" : "0.0",
                "use_dd_annual" : "0.0",
                "use_dd_rate" : "",
                "use_dd_rate_units" : "",
                "use_storage_amount" : "2.5",
                "use_seasons" : "",
                "direct_div_season_begin_date" : null,
                "direct_div_season_end_date" : null,
                "direct_div_season_div_rate" : "",
                "direct_div_season_div_rate_units" : "",
                "direct_div_season_annual_amount" : "",
                "storage_season_begin_date" : null,
                "storage_season_end_date" : null,
                "storage_season_amount" : "2.5",
                "pod_max_dd" : "0.0",
                "source_max_dd_unit" : "",
                "pod_max_storage" : "0.0",
                "source_max_storage_unit" : "Gallons per Day",
                "pod_gis_maintained_data" : "",
                "appl_id" : "C003105",
                "podid" : "3912",
                "permit_id" : "",
                "water_right_description" : "",
                "issue_date" : "1979-03-26",
                "construction_completed_by" : "",
                "planned_project_completion_date" : "",
                "permit_terms" : "",
                "term_id" : "0000021",
                "version_number" : "2.0"
        },
        "_id" : ObjectId("50f334c57ed9c041de0000dc")
}
```





