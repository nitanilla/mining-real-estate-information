# midaas-expanded-api

## Overview

Extension of the [midaas-API](https://github.com/CommerceDataService/midaas-api) with education, industry and occupation data from the ACS 5 year data 2010-2014

## Issues

Plesae report any trouble with the API or questions as [Issues](https://github.com/accenturelabs/midaas-expanded-api/issues) and we will respond to them ASAP

## API Documentation

### [GET] /quantiles.php
**query params**:  `state, race, sex, agegroup, education, industry, occupation` _(see below for options)_<br>
**response format**:  
```
{
  "overall": {
    "<quantile>":  <income>, 
    "<quantile>":  <income>, 
    ...
    "count": <number of incomes sampled> 
  }
}
```
**example**:
```
curl http://54.226.19.203/quantiles.php?education=9&agegroup=25-34&sex=female&race=african american&industry=29
{
  "overall": {
    "5%":  8000,
    "10%": 20300,
    "20%": 40000,
    "30%": 50000,
    "40%": 62300,
    "50%": 74100,
    "60%": 85000,
    "70%": 100000,
    "80%": 108200,
    "90%": 121500,
    "95%": 136400,
    "99%": 297800,
    "count": 130
  }
}
```
#### What are `0` Results?
Results of all `0` indicate no data for this query.<br>
**example**:
```
curl http://54.226.19.203/quantiles.php?education=9&agegroup=25-34&sex=female&race=african american&occupation=29000
{
  "overall": {
    "5%":  0,
    "10%": 0,
    "20%": 0,
    "30%": 0,
    "40%": 0,
    "50%": 0,
    "60%": 0,
    "70%": 0,
    "80%": 0,
    "90%": 0,
    "95%": 0,
    "99%": 0,
    "count": 0
  }
}
```
**SOLUTION:** Instead of searching for the occupation grouping `29000`, try searching the full industry of `29`

### Comparing Results

To make accessing the data easier the following groups can be compared, which returns all options for these parameters **`race, sex, agegroup, education`**

#### Query Parameter for Comparison
To use this function pass the parameter **`compare`** with any of these options
```
"race",
"sex",
"agegroup",
"education"
```

#### Sex Comparison Example
**example**:
```
curl http://54.226.19.203/quantiles.php?education=9&agegroup=25-34&race=african%20american&industry=29&compare=sex
{
  "male": {
    "5%": 13900,
    "10%": 23600,
    "20%": 39800,
    "30%": 40200,
    "40%": 50000,
    "50%": 53000,
    "60%": 88600,
    "70%": 112900,
    "80%": 126100,
    "90%": 181200,
    "95%": 222500,
    "99%": 371000,
    "count": 51
  },
  "female": {
    "5%": 8000,
    "10%": 20300,
    "20%": 40000,
    "30%": 50000,
    "40%": 62300,
    "50%": 74100,
    "60%": 85000,
    "70%": 100000,
    "80%": 108200,
    "90%": 121500,
    "95%": 136400,
    "99%": 297800,
    "count": 130
  }
}
```

### Query Parameter Options

The query parameters **`state, race, sex, agegroup`** match the [midaas-API](https://github.com/CommerceDataService/midaas-api) definitions and should be entered as plaintext *without* quotes, see the example above.
**`education, industry, occupation`** are new query options and their values are defined below. **NOTE:** if both parameters **`industry, occupation`** are specified the **`industry`** parameter will be ignored; occupation implies that the industry is known.

#### state

The two letter postal abbreviation...

```
"AL", "AK", "AR", "AZ", "CA", "CO", "CT", "DE",
"DC", "FL", "GA", "HI", "ID", "IL", "IN", "IA",
"KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN",
"MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM",
"NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI",
"SC", "SD", "TN", "TX", "UT", "VT", "VA", "WA",
"WV", "WI", "WY", "PR", "undefined"
```

#### race

```
"white",
"african american",
"hispanic",
"asian",
"other"
```

#### sex

```
"male",
"female"
```

#### agegroup

```
"18-24",
"25-34",
"35-44",
"45-54",
"55-64",
"65+"
```

#### education

ID | Description
---|------------
0 | No Education Defined
1 | No High School
2 | High School
3 | GED
4 | Some College
5 | Associates Degree
6 | Bachelors Degree
7 | Masters Degree
8 | Professionals Degree
9 | Doctorate Degree

#### industry

**NOTE:** if both parameters **`industry, occupation`** are specified the **`industry`** parameter will be ignored; occupation implies that the industry is known.

ID | Description
---|------------
0 | No Industry Defined
11 | Management
13 | Business and Financial Operations
15 | Computer and Mathematical
17 | Architecture and Engineering
19 | Life, Physical, and Social Science
21 | Community and Social Service
23 | Legal
25 | Education, Training, and Library
27 | Arts, Design, Entertainment, Sports, and Media
29 | Healthcare Practitioners and Technical
31 | Healthcare Support
33 | Protective Service
35 | Food Preparation and Serving Related
37 | Building and Grounds Cleaning and Maintenance
39 | Personal Care and Service
41 | Sales and Related
43 | Office and Administrative Support
45 | Farming, Fishing, and Forestry
47 | Construction and Extraction
49 | Installation, Maintenance, and Repair
51 | Production
53 | Transportation and Material Moving
55 | Military Specific
99 | Unemployed with no work experience in last 5 years or never worked

#### occuptation
Occupation IDs are split by industry for ease of access. **NOTE:** if both parameters **`industry, occupation`** are specified the **`industry`** parameter will be ignored; occupation implies that the industry is known.

##### No Industry Defined
ID | Description
---|------------
0 | No Occupation Defined

##### Management
ID | Description
---|------------
110000 | Management Occupations:
1110XX | Chief executives and legislators
111011 | Chief executives
111031 | Legislators
111021 | General and operations managers
112011 | Advertising and promotions managers
112020 | Marketing and sales managers
112031 | Public relations and fundraising managers
113011 | Administrative services managers
113021 | Computer and information systems managers
113031 | Financial managers
113111 | Compensation and benefits managers
113121 | Human resources managers
113131 | Training and development managers
113051 | Industrial production managers
113061 | Purchasing managers
113071 | Transportation, storage, and distribution managers
119013 | Farmers, ranchers, and other agricultural managers
119021 | Construction managers
119030 | Education administrators
119041 | Architectural and engineering managers
119051 | Food service managers
119071 | Gaming managers
119081 | Lodging managers
119111 | Medical and health services managers
119121 | Natural sciences managers
119141 | Property, real estate, and community association managers
119151 | Social and community service managers
119161 | Emergency management directors
119XXX | Miscellaneous managers, including funeral service managers and postmasters and mail superintendents
119061 | Funeral service managers
119131 | Postmasters and mail superintendents
119199 | Managers, all other

##### Business and Financial Operations
ID | Description
---|------------
130000 | Business and Financial Operations Occupations:
131011 | Agents and business managers of artists, performers, and athletes
131021 | Buyers and purchasing agents, farm products
131022 | Wholesale and retail buyers, except farm products
131023 | Purchasing agents, except wholesale, retail, and farm products
131030 | Claims adjusters, appraisers, examiners, and investigators
131041 | Compliance officers
131051 | Cost estimators
131070 | Human resources workers
131141 | Compensation, benefits, and job analysis specialists
131151 | Training and development specialists
131081 | Logisticians
131111 | Management analysts
131121 | Meeting, convention, and event planners
131131 | Fundraisers
131161 | Market research analysts and marketing specialists
131199 | Business operations specialists, all other
132011 | Accountants and auditors
132021 | Appraisers and assessors of real estate
132031 | Budget analysts
132041 | Credit analysts
132051 | Financial analysts
132052 | Personal financial advisors
132053 | Insurance underwriters
132061 | Financial examiners
132070 | Credit counselors and loan officers
132081 | Tax examiners and collectors, and revenue agents
132082 | Tax preparers
132099 | Financial specialists, all other

##### Computer and Mathematical
ID | Description
---|------------
150000 | Computer and mathematical occupations:
151111 | Computer and information research scientists
151121 | Computer systems analysts
151122 | Information security analysts
151131 | Computer programmers
15113X | Software developers, applications and systems software
151134 | Web developers
151150 | Computer support specialists
151141 | Database administrators
151142 | Network and computer systems administrators
151143 | Computer network architects 
151199 | Computer occupations, all other
152011 | Actuaries
152031 | Operations research analysts
1520XX | Miscellaneous mathematical science occupations, including mathematicians and statisticians
152021 | Mathematicians
152041 | Statisticians
152090 | Miscellaneous mathematical science occupations

##### Architecture and Engineering
ID | Description
---|------------
170000 | Architecture and Engineering Occupations:
171010 | Architects, except naval
171020 | Surveyors, cartographers, and photogrammetrists
172011 | Aerospace engineers
1720XX | Biomedical and agricultural engineers
172021 | Agricultural engineers
172031 | Biomedical engineers
172041 | Chemical engineers
172051 | Civil engineers
172061 | Computer hardware engineers
172070 | Electrical and electronics engineers
172081 | Environmental engineers
172110 | Industrial engineers, including health and safety
172121 | Marine engineers and naval architects
172131 | Materials engineers
172141 | Mechanical engineers
1721XX | Petroleum, mining and geological engineers, including mining safety engineers
172151 | Mining and geological engineers, including mining safety engineers
172171 | Petroleum engineers
1721YY | Miscellaneous engineers, including nuclear engineers
172161 | Nuclear engineers
172199 | Engineers, all other
173010 | Drafters
173020 | Engineering technicians, except drafters
173031 | Surveying and mapping technicians

##### Life, Physical, and Social Science
ID | Description
---|------------
190000 | Life, Physical, and Social Science Occupations:
191010 | Agricultural and food scientists
191020 | Biological scientists
191030 | Conservation scientists and foresters
1910XX | Medical scientists, and life scientists, all other
191040 | Medical scientists
191099 | Life scientists, all other
192010 | Astronomers and physicists
192021 | Atmospheric and space scientists
192030 | Chemists and materials scientists
192040 | Environmental scientists and geoscientists
192099 | Physical scientists, all other
193011 | Economists
193030 | Psychologists
193051 | Urban and regional planners
1930XX | Miscellaneous social scientists, including survey researchers and sociologists
193022 | Survey researchers
193041 | Sociologists
193090 | Miscellaneous social scientists and related workers
194011 | Agricultural and food science technicians
194021 | Biological technicians
194031 | Chemical technicians
1940XX | Geological and petroleum technicians, and nuclear technicians
194041 | Geological and petroleum technicians
194051 | Nuclear technicians
1940YY | Miscellaneous life, physical, and social science technicians, including social science research assistants
194061 | Social science research assistants
194090 | Miscellaneous life, physical, and social science technicians

##### Community and Social Service
ID | Description
---|------------
210000 | Community and Social Service Occupations:
211010 | Counselors
211020 | Social workers
211092 | Probation officers and correctional treatment specialists
211093 | Social and human service assistants
21109X | Miscellaneous community and social service specialists, including health educators and community health workers
212011 | Clergy
212021 | Directors, religious activities and education
212099 | Religious workers, all other

##### Legal
ID | Description
---|------------
230000 | Legal Occupations:
2310XX | Lawyers, and judges, magistrates, and other judicial workers
231011 | Lawyers
231020 | Judges, magistrates, and other judicial workers
231012 | Judicial law clerks
232011 | Paralegals and legal assistants
232090 | Miscellaneous legal support workers

##### Education, Training, and Library
ID | Description
---|------------
250000 | Education, Training, and Library Occupations:
251000 | Postsecondary teachers
252010 | Preschool and kindergarten teachers
252020 | Elementary and middle school teachers
252030 | Secondary school teachers
252050 | Special education teachers
253000 | Other teachers and instructors
254010 | Archivists, curators, and museum technicians
254021 | Librarians
254031 | Library technicians
259041 | Teacher assistants
2590XX | Other education, training, and library workers
259011 | Audio-visual collections specialists
259021 | Farm and home management advisors
259031 | Instructional coordinators
259099 | Education, training, and library workers, all others

##### Arts, Design, Entertainment, Sports, and Media
ID | Description
---|------------
270000 | Arts, Design, Entertainment, Sports, and Media Occupations:
271010 | Artists and related workers
271020 | Designers
272011 | Actors
272012 | Producers and directors
272020 | Athletes, coaches, umpires, and related workers
272030 | Dancers and choreographers
272040 | Musicians, singers, and related workers
272099 | Entertainers and performers, sports and related workers, all other
273010 | Announcers
273020 | News analysts, reporters and correspondents
273031 | Public relations specialists
273041 | Editors
273042 | Technical writers
273043 | Writers and authors
273090 | Miscellaneous media and communication workers
2740XX | Broadcast and sound engineering technicians and radio operators, and media and communication equipment workers, all other
274010 | Broadcast and sound engineering technicians and radio operators
274099 | Media and communication equipment workers, all other
274021 | Photographers
274030 | Television, video, and motion picture camera operators and editors

##### Healthcare Practitioners and Technical
ID | Description
---|------------
290000 | Healthcare Practitioners and Technical Occupations:
291011 | Chiropractors
291020 | Dentists
291031 | Dietitians and nutritionists
291041 | Optometrists
291051 | Pharmacists
291060 | Physicians and surgeons
291071 | Physician assistants
291081 | Podiatrists
291181 | Audiologists
291122 | Occupational therapists
291123 | Physical therapists
291124 | Radiation therapists
291125 | Recreational therapists
291126 | Respiratory therapists
291127 | Speech-language pathologists
29112X | Other therapists, including exercise physiologists
291128 | Exercise physiologists
291129 | Therapists, all other
291131 | Veterinarians
291141 | Registered nurses
291151 | Nurse anesthetists
2911XX | Nurse practitioners and nurse midwives
291161 | Nurse midwives
291171 | Nurse practitioners
291199 | Health diagnosing and treating practitioners, all other
292010 | Clinical laboratory technologists and technicians
292021 | Dental hygienists
292030 | Diagnostic related technologists and technicians
292041 | Emergency medical technicians and paramedics
292050 | Health practitioner support technologists and technicians
292061 | Licensed practical and licensed vocational nurses
292071 | Medical records and health information technicians
292081 | Opticians, dispensing
292090 | Miscellaneous health technologists and technicians
299000 | Other healthcare practitioners and technical occupations

##### Healthcare Support
ID | Description
---|------------
310000 | Healthcare Support Occupations:
311010 | Nursing, psychiatric, and home health aides
312010 | Occupational therapy assistants and aides
312020 | Physical therapist assistants and aides
319011 | Massage therapists
319091 | Dental assistants
319092 | Medical assistants
319094 | Medical transcriptionists
319095 | Pharmacy aides
319096 | Veterinary assistants and laboratory animal caretakers
319097 | Phlebotomists
31909X | Healthcare support workers, all other, including medical equipment preparers
319093 | Medical equipment preparers
319099 | Healthcare support workers, all other

##### Protective Service
ID | Description
---|------------
330000 | Protective Service Occupations:
331011 | First-line supervisors of correctional officers
331012 | First-line supervisors of police and detectives
331021 | First-line supervisors of fire fighting and prevention workers
331099 | First-line supervisors of protective service workers, all other
332011 | Firefighters
332020 | Fire inspectors
333010 | Bailiffs, correctional officers, and jailers
333021 | Detectives and criminal investigators
3330XX | Miscellaneous law enforcement workers
333031 | Fish and game wardens
333041 | Parking enforcement workers
333050 | Police officers
333051 | Police and sheriff's patrol officers
333052 | Transit and railroad police
339011 | Animal control workers
339021 | Private detectives and investigators
339030 | Security guards and gaming surveillance officers
339091 | Crossing guards
339093 | Transportation security screeners
33909X | Lifeguards and other recreational, and all other protective service workers
339092 | Lifeguards, ski patrol, and other recreational protective service workers
339099 | Protective service workers, all other

##### Food Preparation and Serving Related
ID | Description
---|------------
350000 | Food Preparation and Serving Related Occupations:
351011 | Chefs and head cooks
351012 | First-line supervisors of food preparation and serving workers
352010 | Cooks
352021 | Food preparation workers
353011 | Bartenders
353021 | Combined food preparation and serving workers, including fast food
353022 | Counter attendants, cafeteria, food concession, and coffee shop
353031 | Waiters and waitresses
353041 | Food servers, nonrestaurant
3590XX | Miscellaneous food preparation and serving related workers, including dining room and cafeteria attendants and bartender helpers
359011 | Dining room and cafeteria attendants and bartender helpers
359099 | Food preparation and serving related workers, all other
359021 | Dishwashers
359031 | Hosts and hostesses, restaurant, lounge, and coffee shop

##### Building and Grounds Cleaning and Maintenance
ID | Description
---|------------
370000 | Building and Grounds Cleaning and Maintenance Occupations:
371011 | First-line supervisors of housekeeping and janitorial workers
371012 | First-line supervisors of landscaping, lawn service, and groundskeeping workers
37201X | Janitors and building cleaners
372011 | Janitors and cleaners, except maids and housekeeping cleaners
372019 | Building cleaning workers, all other
372012 | Maids and housekeeping cleaners
372021 | Pest control workers
373010 | Grounds maintenance workers

##### Personal Care and Service
ID | Description
---|------------
390000 | Personal Care and Service Occupations:
391010 | First-line supervisors of gaming workers
391021 | First-line supervisors of personal service workers
392011 | Animal trainers
392021 | Nonfarm animal caretakers
393010 | Gaming services workers
393021 | Motion picture projectionists
393031 | Ushers, lobby attendants, and ticket takers
393090 | Miscellaneous entertainment attendants and related workers
3940XX | Embalmers and funeral attendants
394031 | Morticians, undertakers, and funeral directors
395011 | Barbers
395012 | Hairdressers, hairstylists, and cosmetologists
395090 | Miscellaneous personal appearance workers
396010 | Baggage porters, bellhops, and concierges
397010 | Tour and travel guides
399011 | Childcare workers
399021 | Personal care aides
399030 | Recreation and fitness workers
399041 | Residential advisors
399099 | Personal care and service workers, all other

##### Sales and Related
ID | Description
---|------------
410000 | Sales and Related Occupations:
411011 | First-line supervisors of retail sales workers
411012 | First-line supervisors of non-retail sales workers
412010 | Cashiers
412021 | Counter and rental clerks
412022 | Parts salespersons
412031 | Retail salespersons
413011 | Advertising sales agents
413021 | Insurance sales agents
413031 | Securities, commodities, and financial services sales agents
413041 | Travel agents
413099 | Sales representatives, services, all other
414010 | Sales representatives, wholesale and manufacturing
419010 | Models, demonstrators, and product promoters
419020 | Real estate brokers and sales agents
419031 | Sales engineers
419041 | Telemarketers
419091 | Door-to-door sales workers, news and street vendors, and related workers
419099 | Sales and related workers, all other

##### Office and Administrative Support
ID | Description
---|------------
430000 | Office and Administrative Support Occupations:
431011 | First-line supervisors of office and administrative support workers
432011 | Switchboard operators, including answering service
432021 | Telephone operators
432099 | Communications equipment operators, all other
433011 | Bill and account collectors
433021 | Billing and posting clerks 
433031 | Bookkeeping, accounting, and auditing clerks
433041 | Gaming cage workers
433051 | Payroll and timekeeping clerks
433061 | Procurement clerks
433071 | Tellers
433099 | Financial clerks, all other
434011 | Brokerage clerks
434031 | Court, municipal, and license clerks
434041 | Credit authorizers, checkers, and clerks
434051 | Customer service representatives
434061 | Eligibility interviewers, government programs
434071 | File clerks
434081 | Hotel, motel, and resort desk clerks
434111 | Interviewers, except eligibility and loan
434121 | Library assistants, clerical
434131 | Loan interviewers and clerks
434141 | New accounts clerks
434XXX | Correspondence clerks and order clerks
434021 | Correspondence clerks
434151 | Order clerks
434161 | Human resources assistants, except payroll and timekeeping
434171 | Receptionists and information clerks
434181 | Reservation and transportation ticket agents and travel clerks
434199 | Information and record clerks, all other
435011 | Cargo and freight agents
435021 | Couriers and messengers
435030 | Dispatchers
435041 | Meter readers, utilities
435051 | Postal service clerks
435052 | Postal service mail carriers
435053 | Postal service mail sorters, processors, and processing machine operators
435061 | Production, planning, and expediting clerks
435071 | Shipping, receiving, and traffic clerks
435081 | Stock clerks and order fillers
435111 | Weighers, measurers, checkers, and samplers, recordkeeping
436010 | Secretaries and administrative assistants
439011 | Computer operators
439021 | Data entry keyers
439022 | Word processors and typists
439041 | Insurance claims and policy processing clerks
439051 | Mail clerks and mail machine operators, except postal service
439061 | Office clerks, general
439071 | Office machine operators, except computer
439081 | Proofreaders and copy markers
439111 | Statistical assistants
439XXX | Miscellaneous office and administrative support workers, including desktop publishers
439031 | Desktop publishers
439199 | Office and administrative support workers, all other

##### Farming, Fishing, and Forestry
ID | Description
---|------------
450000 | Farming, Fishing, and Forestry Occupations:
451011 | First-line supervisors of farming, fishing, and forestry workers
452011 | Agricultural inspectors
452041 | Graders and sorters, agricultural products
4520XX | Miscellaneous agricultural workers, including animal breeders
452021 | Animal breeders
452090 | Miscellaneous agricultural workers 
453000 | Fishing and hunting workers
453011 | Fishers and related fishing workers
453021 | Hunters and trappers
454011 | Forest and conservation workers
454020 | Logging workers

##### Construction and Extraction
ID | Description
---|------------
470000 | Construction and Extraction Occupations:
471011 | First-line supervisors of construction trades and extraction workers
472011 | Boilermakers
472020 | Brickmasons, blockmasons, and stonemasons
472031 | Carpenters
472040 | Carpet, floor, and tile installers and finishers
472050 | Cement masons, concrete finishers, and terrazzo workers
472061 | Construction laborers
472071 | Paving, surfacing, and tamping equipment operators
47207X | Construction equipment operators except paving, surfacing, and tamping equipment operators
472072 | Pile-driver operators
472073 | Operating engineers and other construction equipment operators
472080 | Drywall installers, ceiling tile installers, and tapers
472111 | Electricians
472121 | Glaziers
472130 | Insulation workers
472141 | Painters, construction and maintenance
472142 | Paperhangers
472150 | Pipelayers, plumbers, pipefitters, and steamfitters
472161 | Plasterers and stucco masons
472171 | Reinforcing iron and rebar workers
472181 | Roofers
472211 | Sheet metal workers
472221 | Structural iron and steel workers
473010 | Helpers, construction trades
474011 | Construction and building inspectors
474021 | Elevator installers and repairers
474031 | Fence erectors
474041 | Hazardous materials removal workers
474051 | Highway maintenance workers
474061 | Rail-track laying and maintenance equipment operators
47XXXX | Miscellaneous construction workers, including solar photovoltaic installers, septic tank servicers and sewer pipe cleaners
472231 | Solar photovoltaic installers
474071 | Septic tank servicers and sewer pipe cleaners
474090 | Miscellaneous construction and related workers
4750YY | Derrick, rotary drill, and service unit operators, and roustabouts, oil, gas, and mining
475010 | Derrick, rotary drill, and service unit operators, oil, gas, and mining
475071 | Roustabouts, oil and gas
475021 | Earth drillers, except oil and gas
475031 | Explosives workers, ordnance handling experts, and blasters
475040 | Mining machine operators
4750XX | Miscellaneous extraction workers, including roof bolters and helpers
475061 | Roof bolters, mining
475081 | Helpers--extraction workers
4750XX | Other extraction workers
475051 | Rock splitters, quarry
475099 | Extraction workers, all others

##### Installation, Maintenance, and Repair
ID | Description
---|------------
490000 | Installation, Maintenance, and Repair Occupations:
491011 | First-line supervisors of mechanics, installers, and repairers
492011 | Computer, automated teller, and office machine repairers
492020 | Radio and telecommunications equipment installers and repairers
492091 | Avionics technicians
492092 | Electric motor, power tool, and related repairers
49209X | Electrical and electronics repairers, transportation equipment, and industrial and utility
492093 | Electrical and electronics installers and repairers, transportation equipment
49209X | Electrical and electronics repairers, industrial and utility
492094 | Electrical and electronics repairers, commercial and industrial equipment
492095 | Electrical and electronics repairers, powerhouse, substation, and relay
492096 | Electronic equipment installers and repairers, motor vehicles
492097 | Electronic home entertainment equipment installers and repairers
492098 | Security and fire alarm systems installers
493011 | Aircraft mechanics and service technicians
493021 | Automotive body and related repairers
493022 | Automotive glass installers and repairers
493023 | Automotive service technicians and mechanics
493031 | Bus and truck mechanics and diesel engine specialists
493040 | Heavy vehicle and mobile equipment service technicians and mechanics
493050 | Small engine mechanics
493090 | Miscellaneous vehicle and mobile equipment mechanics, installers, and repairers
499010 | Control and valve installers and repairers
499021 | Heating, air conditioning, and refrigeration mechanics and installers
499031 | Home appliance repairers
49904X | Industrial and refractory machinery mechanics
499041 | Industrial machinery mechanics
499045 | Refractory materials repairers, except brickmasons
499071 | Maintenance and repair workers, general
499043 | Maintenance workers, machinery
499044 | Millwrights
499051 | Electrical power-line installers and repairers
499052 | Telecommunications line installers and repairers
499060 | Precision instrument and equipment repairers
499091 | Coin, vending, and amusement machine servicers and repairers
499094 | Locksmiths and safe repairers
499095 | Manufactured building and mobile home installers
499096 | Riggers
499098 | Helpers--installation, maintenance, and repair workers 
49909X | Other installation, maintenance, and repair workers, including wind turbine service technicians, and commercial divers, and signal and track switch repairers
499081 | Wind turbine service technicians
499092 | Commercial divers
499097 | Signal and track switch repairers
49909X | Other installation, maintenance, and repair workers
499093 | Fabric menders, except garment
499099 | Installation, maintenance, and repair workers, all other

##### Production
ID | Description
---|------------
510000 | Production Occupations:
511011 | First-line supervisors of production and operating workers
512011 | Aircraft structure, surfaces, rigging, and systems assemblers
512020 | Electrical, electronics, and electromechanical assemblers
512031 | Engine and other machine assemblers
512041 | Structural metal fabricators and fitters
512090 | Miscellaneous assemblers and fabricators
513011 | Bakers
513020 | Butchers and other meat, poultry, and fish processing workers
513091 | Food and tobacco roasting, baking, and drying machine operators and tenders
513092 | Food batchmakers
513093 | Food cooking machine operators and tenders
513099 | Food processing workers, all other
514010 | Computer control programmers and operators
514021 | Extruding and drawing machine setters, operators, and tenders, metal and plastic
514022 | Forging machine setters, operators, and tenders, metal and plastic
514023 | Rolling machine setters, operators, and tenders, metal and plastic
514031 | Cutting, punching, and press machine setters, operators, and tenders, metal and plastic
514032 | Drilling and boring machine tool setters, operators, and tenders, metal and plastic 
514033 | Grinding, lapping, polishing, and buffing machine tool setters, operators, and tenders, metal and plastic
514034 | Lathe and turning machine tool setters, operators, and tenders, metal and plastic
514041 | Machinists
514050 | Metal furnace operators, tenders, pourers, and casters
514060 | Model makers and patternmakers, metal and plastic
514070 | Molders and molding machine setters, operators, and tenders, metal and plastic
514111 | Tool and die makers
514120 | Welding, soldering, and brazing workers
514191 | Heat treating equipment setters, operators, and tenders, metal and plastic
514193 | Plating and coating machine setters, operators, and tenders, metal and plastic
514194 | Tool grinders, filers, and sharpeners
514XXX | Miscellaneous metal workers and plastic workers, including milling and planing machine setters, and multiple machine tool setters, and layout workers
514035 | Milling and planing machine setters, operators, and tenders, metal and plastic
514081 | Multiple machine tool setters, operators, and tenders, metal and plastic 
514192 | Layout workers, metal and plastic
514199 | Metal workers and plastic workers, all other
515111 | Prepress technicians and workers
515112 | Printing press operators
515113 | Print binding and finishing workers
516011 | Laundry and dry-cleaning workers
516021 | Pressers, textile, garment, and related materials
516031 | Sewing machine operators
516041 | Shoe and leather workers and repairers
516042 | Shoe machine operators and tenders
516050 | Tailors, dressmakers, and sewers
51606X | Textile bleaching and dyeing, and cutting machine setters, operators, and tenders
516061 | Textile bleaching and dyeing machine operators and tenders
516062 | Textile cutting machine setters, operators, and tenders
516063 | Textile knitting and weaving machine setters, operators, and tenders
516064 | Textile winding, twisting, and drawing out machine setters, operators, and tenders
516093 | Upholsterers
51609X | Miscellaneous textile, apparel, and furnishings workers except upholsterers
516091 | Extruding and forming machine setters, operators, and tenders, synthetic and glass fibers
516092 | Fabric and apparel patternmakers
516099 | Textile, apparel, and furnishings workers, all other
517011 | Cabinetmakers and bench carpenters
517021 | Furniture finishers
517041 | Sawing machine setters, operators, and tenders, wood
517042 | Woodworking machine setters, operators, and tenders, except sawing
5170XX | Miscellaneous woodworkers, including model makers and patternmakers
517030 | Model makers and patternmakers, wood
517099 | Woodworkers, all other
518010 | Power plant operators, distributors, and dispatchers
518021 | Stationary engineers and boiler operators
518031 | Water and wastewater treatment plant and system operators
518090 | Miscellaneous plant and system operators
519010 | Chemical processing machine setters, operators, and tenders
519020 | Crushing, grinding, polishing, mixing, and blending workers
519030 | Cutting workers
519041 | Extruding, forming, pressing, and compacting machine setters, operators, and tenders
519051 | Furnace, kiln, oven, drier, and kettle operators and tenders
519061 | Inspectors, testers, sorters, samplers, and weighers
519071 | Jewelers and precious stone and metal workers
519080 | Medical, dental, and ophthalmic laboratory technicians
519111 | Packaging and filling machine operators and tenders
519120 | Painting workers
519151 | Photographic process workers and processing machine operators
519191 | Adhesive bonding machine operators and tenders
519192 | Cleaning, washing, and metal pickling equipment operators and tenders
519194 | Etchers and engravers
519195 | Molders, shapers, and casters, except metal and plastic
519196 | Paper goods machine setters, operators, and tenders
519197 | Tire builders
519198 | Helpers--production workers
5191XX | Other production workers, including semiconductor processors and cooling and freezing equipment operators
519141 | Semiconductor processors
519193 | Cooling and freezing equipment operators and tenders
519199 | Production workers, all other

##### Transportation and Material Moving
ID | Description
---|------------
530000 | Transportation and Material Moving Occupations:
531000 | Supervisors of transportation and material moving workers
532010 | Aircraft pilots and flight engineers
532020 | Air traffic controllers and airfield operations specialists
532031 | Flight attendants
533011 | Ambulance drivers and attendants, except emergency medical technicians
533020 | Bus drivers
533030 | Driver/sales workers and truck drivers
533041 | Taxi drivers and chauffeurs
533099 | Motor vehicle operators, all other
534010 | Locomotive engineers and operators
534021 | Railroad brake, signal, and switch operators
534031 | Railroad conductors and yardmasters
5340XX | Subway, streetcar, and other rail transportation workers
534041 | Subway and streetcar operators
534099 | Rail transportation workers, all other
5350XX | Sailors and marine oilers, and ship engineers
535011 | Sailors and marine oilers
535031 | Ship engineers
535020 | Ship and boat captains and operators
536021 | Parking lot attendants
536031 | Automotive and watercraft service attendants  
536051 | Transportation inspectors
536061 | Transportation attendants, except flight attendants
5360XX | Miscellaneous transportation workers, including bridge and lock tenders and traffic technicians
536011 | Bridge and lock tenders
5360XX | Other transportation workers 
536041 | Traffic technicians
536099 | Transportation workers, all other
537021 | Crane and tower operators
537030 | Dredge, excavating, and loading machine operators
537000 | Material Moving Occupations:
5370XX | Conveyor operators and tenders, and hoist and winch operators
537011 | Conveyor operators and tenders
537041 | Hoist and winch operators
537051 | Industrial truck and tractor operators
537061 | Cleaners of vehicles and equipment
537062 | Laborers and freight, stock, and material movers, hand
537063 | Machine feeders and offbearers
537064 | Packers and packagers, hand
537070 | Pumping station operators
537081 | Refuse and recyclable material collectors
5371XX | Miscellaneous material moving workers, including mine shuttle car operators, and tank car, truck, and ship loaders
537111 | Mine shuttle car operators
537121 | Tank car, truck, and ship loaders
537199 | Material moving workers, all other

##### Military Specific
ID | Description
---|------------
551010 | Military officer special and tactical operations leaders
552010 | First-line enlisted military supervisors
553010 | Military enlisted tactical operations and air/weapons specialists and crew members
559830 | Military, rank not specified

##### Unemployed with no work experience in last 5 years or never worked
ID | Description
---|------------
999920 | Unemployed, with no work experience in the last 5 years or earlier or never worked
