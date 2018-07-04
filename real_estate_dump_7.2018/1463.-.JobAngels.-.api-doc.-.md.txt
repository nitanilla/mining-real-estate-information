FORMAT: 1A
HOST: https://api.jobangels.com

# JobAngels API Documentation
JobAngels API ponúka základnú správu pracovných ponúk a k ním priradený firemný profil. Umožňuje tiež získavať informácie o uchádzačoch, ktorý sa uchádzajú na danú pozíciu.

# Allowed HTTPs requests:
<pre>
GET    : Get a resource or list of resources
PUT    : To create resource
POST   : To update resource 
DELETE : To delete resource
</pre>

# Description Of Usual Server Responses:
- 200 `OK` - the request was successful (some API calls may return 201 instead).
- 201 `Created` - the request was successful and a resource was created.
- 204 `No Content` - the request was successful but there is no representation to return (i.e. the response is empty).
- 400 `Bad Request` - the request could not be understood or was missing required parameters.
- 401 `Unauthorized` - authentication failed or user doesn't have permissions for requested operation.
- 403 `Forbidden` - access denied.
- 404 `Not Found` - resource was not found.
- 405 `Method Not Allowed` - requested method is not supported for resource.
- 2001 `Already exists` - the request was successful but the creating resourse already exists.
- 2002 `Limited` - the request was successfull but you have limited resource creation.

# Successed Result:
    
    {
      "success": true,
      "data": [
        {
          "name": "JobAngels",
        }
      ]
    }

# Successed Result with Pagination:
    
    {
      "success": true,
      "data": [
        {
          "name": "JobAngels",
        },
        {
          "name": "Challengest",
        }
      ],
      "page": 3,
      "perPage": 10,
      "itemCount": 34,
      "prevPage": "/companies?page=2",
      "nextPage": "/companies?page=4"
    }

# Result with errors:
    
    {
      "success": false,
      "errors": [
        {
          "code": 404,
          "message": "Page not found",
        }
      ]
    }

# Group Company

**Company attributes:**
- id `(number)` : Unique identifier.
- name `(string)` : Company name.
- brand_name `(string)` : Brand name.
- logo `(string)` : Company logo as URL.
- profile_url `(string)` : Company profile as URL on JobAngels.co.
- status `(string)` : Current status of company.
- size `(number)` : Size of company represented as number (Company size).
- business_id `(string)` : Company business identification number in their country (ex. IČO).
- tax_number `(string)` : Tax identification number to identify taxpayers of their national tax affairs.
- vat_number `(string)` : VAT identification number.
- country_key `(string)` : Unique identifier of country as code (ISO 3166-1 alpha-2) *(alias for billing_address.country_key)*.
- billing_address `(object)` : Company billing address.
- contact_address `(object)` : Company contact address.


**Company statuses:**
<table>
    <tr>
        <td> active </td>
        <td> The company has an active package and company profile is published. </td>    
    </tr>
    <tr>
        <td> unpublished </td>
        <td> The company has an active package but company profile is unpublished. </td> 
    </tr>
    <tr>
        <td> paused </td>
        <td> The company has not active package. </td> 
    </tr>
    <tr>
        <td> blocked </td>
        <td> The company is blocked. </td> 
    </tr>
</table>


**Company sizes:**
<table>
    <tr>
        <td>1</td>
        <td>freelancer</td>
    </tr>
    <tr>
        <td>2</td>
        <td>startup</td>
    </tr>
    <tr>
        <td>3</td>
        <td>small business (less than 15 employees)</td>
    </tr>
    <tr>
        <td>4</td>
        <td>medium business (less than 200 employees)</td>
    </tr>
    <tr>
        <td>5</td>
        <td>large business (more than 200 employees)</td>
    </tr>
    <tr>
        <td>6</td>
        <td>non-profit organization</td>
    </tr>
    <tr>
        <td>7</td>
        <td>educational institution</td>
    </tr>
</table>

## Company Colletion [/companies{?business_id,country_key,status,page,limit}]

+ Parameters:
    + business_id: `0123456789` (string, optional) - Company identification numbers in specified country. (ex. IČO in SR)
    + country_key: SK (string, optional) - Billing country code (ISO 3166-1 alpha-2).
    + status (string, optional) - Current status of company. Possible values are active|paused|uncompleted|blocked
    + page (number, optional) - The current page number.
        + Default: 1
    + limit (number, optional) - Maximum of results. Limit can be a number from 1 - 100.
        + Default: 10

### List of companies [GET]

+ Response 200 (application/json)

        {   
            "success": true,
            "data": [
                {
                    "id": 1,
                    "name": "JobAngels.co, s.r.o.",
                    "brand_name": "JobAngels & Challengest",
                    "business_id": "47944129",
                    "country_key": "SK",
                    "status": "active"
                },
                {
                    "id": 2,
                    "name": "Challengest, s.r.o.",
                    "brand_name": "Challengest, s.r.o.",
                    "business_id": "462422156",
                    "country_key": "SK",
                    "status": "uncompleted"
                }
            ]
            "page": 1,
            "perPage": 2,
            "itemCount": 314,
            "prevPage": null,
            "nextPage": "/companies?page=2"
        }

+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "messages": "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

### Create company [POST]

+ Request (application/json)

        {
            "name": "JobAngels.co, s.r.o.",
            "business_id": "47944129",
            "country_key": "SK"
        }
                
        
+ Response 201 (application/json)

        {
            "success": true,
            "data": {
                "id": 1
                "name": "JobAngels.co, s.r.o.",
                "business_id": "47944129",
                "country_key": "SK"
            }
        }
            
        
+ Response 2001 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 2001,
                    "message" : "Sorry, company with this business_id and country_key already exists."
                }
            ]
        }

+ Response 2002 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 2002,
                    "message" : "Sorry, you can create only one main company profile."
                }
            ]
        }


+ Response 401 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }

## Company [/companies/{id}]

+ Parameters
    + id (required, Number, `1`) - Numeric `id` of the Company to perform action with.

### Detail of company [GET] 
+ Response 200 (application/json)
    
        {
            "success": true,
            "data": {
                "id": 1,
                "name": "JobAngels.co, s.r.o.",
                "brand_name": "JobAngels & Challengest",
                "logo": "https://jobangels.net/jobangels/image/upload/c_fit,h_76,w_76/v1486575885/05e9e3222762786d18e8da2c97fb6fcf47888b33665978c2ca0c8d4c9abd72d71a27c80b.png",
                "profile_url": "https://jobangels.com/JobAngels&Challengest",
                "country_key": "SK",
                "billing_address": {
                    "country_key": "SK"
                    "contry_name": "Slovakia"
                    "street": "",
                    "city": "",
                    "postal_code": ""
                },
                "contact_address": {
                    "country_key": "SK"
                    "contry_name": "Slovakia"
                    "street": "",
                    "city": "",
                    "postal_code": ""
                },
                "status": "uncompleted",
                "size": null,
                "business_id": "47944129",
                "tax_id_number": "",
                "vat_number": ""
            }
        }

+ Response 401 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }

### Update Company [PUT]

+ Request (application/json)

        {
            "billing_address": {
                "country_key": "SK"
                "street": "Černyševského 10",
                "city": "Bratislava",
                "postal_code": "85104"
            },
            "contact_address": {
                "country_key": "SK"
                "street": "Jakubovo nám. 13",
                "city": "Bratislava",
                "postal_code": "81109"
            },
            "size": 2,
            "business_id": "47944129",
            "tax_id_number": "2024155210",
            "vat_number": "SK2024155210"
        }
        
+ Response 200 (application/json)
    
        {
            "success": true,
            "data": {
                "id": 1,
                "name": "JobAngels.co, s.r.o.",
                "brand_name": "JobAngels & Challengest",
                "logo": "https://jobangels.net/jobangels/image/upload/c_fit,h_76,w_76/v1486575885/05e9e3222762786d18e8da2c97fb6fcf47888b33665978c2ca0c8d4c9abd72d71a27c80b.png",
                "profile_url": "https://jobangels.com/JobAngels&Challengest",
                "country_key": "SK",
                "billing_address": {
                    "country_key": "SK"
                    "street": "Černyševského 10",
                    "city": "Bratislava",
                    "postal_code": "85104"
                },
                "contact_address": {
                    "country_key": "SK"
                    "street": "Jakubovo nám. 13",
                    "city": "Bratislava",
                    "postal_code": "81109"
                },
                "status": "active",
                "size": 2,
                "business_id": "47944129",
                "tax_id_number": "2024155210",
                "vat_number": "SK2024155210"
            }
        }

+ Response 401 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }


## Company Jobs Collection [/companies/{id}/jobs{?status,page,limit}]

+ Parameters:
    + id (number, required, `1`) - Company identifier as integer.
    + status (string, optional, `published`) - Current status of job.
    + page (number, optional) - The current page number.
        + Default: 1
    + limit (number, optional) - Maximum of results. Limit can be a number from 1 - 100.
        + Default: 10

### Retrive Jobs of Company[GET]

+ Response 200 (application/json)

        {
            "success": false
            "data": [
                {
                    "id": 15,
                    "key": "ab2dh6fe",
                    "name": "PHP Programmer",
                    "status": "published"
                },
                {
                    "id": 248,
                    "key": "poklrei7",
                    "name": "Sales Manager",
                    "status": "closed"
                }
            ],
            "page": 1,
            "perPage": 2,
            "itemCount": 314,
            "prevPage": null,
            "nextPage": "/companies/1/jobs?page=2"
        }

+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

### Create Job [POST]

+ Request (application/json)

        {
            "name": "PHP Junior Programator"
        }

   
+ Response 201 (application/json)

        {
            "success": false
            "data": {
                "id": 1
                "key": "ab2dh6fe"
                "name": ""PHP Junior Programator"
            }
        }
            


+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

# Group Job

**Job attributes:**

- id `(number)` : Unique identifier.
- key `(number)` : Unique string identifier (8 characters).
- name `(string)` : Job position name.
- url `(string)` : Job as URL on JobAngels.co.
- cover `(string)` : Job cover as URL in origin size.
- reward `(object)` : Reward for possible hiring (total, angel, currency).
- salary `(object)` : Salary as range (min, max, currency). Showing only if salary is not hidden.
- status `(string)` : Current status of job.
- lang `(string)`: Job language represented as key (two characters: sk, cs, en).
- locations `(object)`: Job locations.
- field_of_work `(object)` : Job field of work as object (id, name).


**Job statuses:**
<table>
    <tr>
        <th> draft </th>
        <th> The job is only in draft version and it's not published. </th>    
    </tr>
    <tr>
        <td> published </td>
        <td> The job is published. </td> 
    </tr>
    <tr>
        <td> closed </td>
        <td> The job is closed. </td> 
    </tr>
    <tr>
        <td> blocked </td>
        <td> The job is blocked. </td> 
    </tr>
</table>


**Fields of work:**
<table>
    <tr>
        <th> id </th>
        <th> name </th>
    </tr>
    <tr>
        <td> 1 </td>
        <td> Client Management & Business Development </td>
    </tr>
    <tr>
        <td> 2 </td>
        <td> IT & Telecommunication </td>
    </tr>
    <tr>
        <td> 3 </td>
        <td> Production & Manufacturing </td>
    </tr>
    <tr>
        <td> 4 </td>
        <td> Marketing & PR </td>
    </tr>
    <tr>
        <td> 5 </td>
        <td> Administrative & Assistant jobs </td>
    </tr>
    <tr>
        <td> 6 </td>
        <td> Audit & Consultancy </td>
    </tr>
    <tr>
        <td> 7 </td>
        <td> Banking & Finance </td>
    </tr>
    <tr>
        <td> 8 </td>
        <td> Education, Science & Research </td>
    </tr>
    <tr>
        <td> 9 </td>
        <td> Engineering </td>
    </tr>
    <tr>
        <td> 10</td>
        <td> Creative & Design jobs </td>
    </tr>
    <tr>
        <td> 11</td>
        <td> Agriculture </td>
    </tr>
    <tr>
        <td>12</td>
        <td> Healthcare </td>
    </tr>
    <tr>
        <td>13</td>
        <td> "Logistics, Transportation" </td>
    </tr>
    <tr>
        <td>14</td>
        <td> Economics and Accountancy </td>
    </tr>
    <tr>
        <td>15</td>
        <td> Law </td>
    </tr>
    <tr>
        <td>16</td>
        <td> Construction, Architecture & Real Estates </td>
    </tr>
    <tr>
        <td>17</td>
        <td> Automotive </td>
    </tr>
    <tr>
        <td>18</td>
        <td> Electrical and Power Engineering </td>
    </tr>
    <tr>
        <td>19</td>
        <td> Travel & Hospitality jobs </td>
    </tr>
    <tr>
        <td>20</td>
        <td> Customer Support </td>
    </tr>
    <tr>
        <td>21</td>
        <td> Quality Assurance </td>
    </tr>
    <tr>
        <td>22</td>
        <td> Human Resources </td>
    </tr>
    <tr>
        <td>23</td>
        <td> Insurance jobs </td>
    </tr>
    <tr>
        <td>24</td>
        <td> Pharmacy </td>
    </tr>
    <tr>
        <td>25</td>
        <td> Safety & Protection </td>
    </tr>
    <tr>
        <td>26</td>
        <td> Chemical Industry </td>
    </tr>
    <tr>
        <td>27</td>
        <td> Journalism </td>
    </tr>
    <tr>
        <td>28</td>
        <td> Fashion </td>
    </tr>
    <tr>
        <td>29</td>
        <td> Public Sector </td>
    </tr>
    <tr>
        <td>30</td>
        <td> Translation and Interpretation </td>
    </tr>
    <tr>
        <td>31</td>
        <td> Retail jobs </td>
    </tr>
    <tr>
        <td>32</td>
        <td> Game Development </td>
    </tr>
    <tr>
        <td>33</td>
        <td> E-commerce </td>
    </tr>
    <tr>
        <td>34</td>
        <td> Retail </td>
    </tr>
    <tr>
        <td>35</td>
        <td> Services </td>
    </tr>
</table>


## Colletion [/jobs{?fields,field_of_work,status,page,limit}]

### List [GET]

+ Parameters
    + field_of_work: 1 (number, optional) - Return jobs only with this field of work
    + status (string, optional) - Current status of job (Job statuses.)
    + page (number, optional) - The current page number.
        + Default: 1
    + limit (number, optional) - Maximum of results. Limit can be a number from 1 - 100.
        + Default: 10
        

+ Response 200 (application/json)

        {
            "success": true,
            "data": [
                {
                    "id": 15,
                    "key": "ab2dh6fe",
                    "name": "PHP Programmer",
                    "company_id": 1,
                    "url": "https://jobangels.com/ab2dh6fe/PHP-Programmer",
                    "reward": {
                        total: 1200,
                        angel: 600,
                        currency: "EUR"
                    },
                    "salary": {
                        min: 1200,
                        max: 2500,
                        currency: "EUR"
                    },
                    "status": "published"
                },
                {
                    "id": 248,
                    "key": "poklrei7",
                    "name": "Sales Manager - Praha",
                    "company_id": 2,
                    "url": "https://jobangels.com/poklrei7/Sales-Manager-Praha",
                    "reward": {
                        total: 450,
                        angel: 225,
                        currency: "EUR"
                    },
                    "salary": {
                        min: 25000,
                        max: 35000,
                        currency: "CZK"
                    },
                    "status": "closed"
                }
            ],
            "page": 1,
            "perPage": 2,
            "itemCount": 513,
            "prevPage": null,
            "nextPage": "/jobs?page=2"
        }

+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

## Job [/jobs/{id}]

+ Parameters
    + id (required, number, `1`) - Numeric `id` of the job to perform action with.


### Detail of job [GET] 

+ Response 200

        {
            "success": true,
            "data": {
                "id": 15,
                "key": "ab2dh6fe",
                "name": "PHP Programmers",
                "url": "https://jobangels.com/ab2dh6fe/PHP-Programmer",
                "cover": "https://jobangels.net/jobangels/image/upload/c_crop,h_1732,w_3694,x_0,y_240/c_fill,h_450,w_960/4bc9372c0583fa97fd062eda271c98dc0c442185c9791b13c11cf063788f21cfd30e84f5.jpg",
                "company_id": 1,
                "lang": "sk",
                "reward": {
                    total: 1200,
                    angel: 600,
                    currency: "EUR"
                },
                "salary": {
                    min: 1200,
                    max: 2500,
                    currency: "EUR"
                },
                "status": "published",
                "locations":[
                    {
                          "id": 351,
                          "country_key": "SK",
                          "street": "Jakubovo nám. 13",
                          "city": "Bratislava",
                          "postal_code": "811 09",
                          "region": "Bratislavský kraj",
                          "lat": 48.1459258,
                          "lng": 17.1071938  
                    },
                    {
                          "id": 351,
                          "country_key": "SK",
                          "street": "Černyševského 10",
                          "city": "Petržalka",
                          "postal_code": "85104",
                          "region": "Bratislavský kraj",
                          "lat": 48.3804996,
                          "lng": 17.5877285    
                    }
                ],
                "field_of_work": {
                    "id": 2,
                    "name": "IT & Telecommunication"
                }
            }
        }

+ Response 401 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }

### Update job [PUT]

+ Request (application/json)

        {
            "name": "PHP Junior Programmer",
            "reward": {
                total: 2000
            }
        }
        
+ Response 200 (application/json)
    
        {
            "success": true,
            "data": {
                "id": 15,
                "key": "ab2dh6fe",
                "name": "PHP Junior Programmer",
                "url": "https://jobangels.com/ab2dh6fe/PHP-Programmer",
                "cover": "https://jobangels.net/jobangels/image/upload/c_crop,h_1732,w_3694,x_0,y_240/c_fill,h_450,w_960/4bc9372c0583fa97fd062eda271c98dc0c442185c9791b13c11cf063788f21cfd30e84f5.jpg",
                "company_id": 1,
                "lang": "sk",
                "reward": {
                    total: 2000,
                    angel: 1000,
                    currency: "EUR"
                },
                "salary": {
                    min: 1200,
                    max: 2500,
                    currency: "EUR"
                },
                "status": "published",
                "locations":[
                    {
                          "id": 351,
                          "country_key": "SK",
                          "street": "Jakubovo nám. 13",
                          "city": "Bratislava",
                          "postal_code": "811 09",
                          "region": "Bratislavský kraj",
                          "lat": 48.1459258,
                          "lng": 17.1071938  
                    },
                    {
                          "id": 351,
                          "country_key": "SK",
                          "street": "Černyševského 10",
                          "city": "Petržalka",
                          "postal_code": "85104",
                          "region": "Bratislavský kraj",
                          "lat": 48.3804996,
                          "lng": 17.5877285    
                    }
                ],
                "field_of_work": {
                    "id": 2,
                    "name": "IT & Telecommunication"
                }
            }
        }

+ Response 401 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }



## Job Applications Collection [/jobs/{id}/applications{?status,page,limit}]

+ Parameters
    + id (number, required, `15`) - Job identifier as integer.
    + status (string, optional) - Status of application (new, viewed, hired, rejected, released).
    + page (number, optional) - The current page number.
        + Default: 1
    + limit (number, optional) - Maximum of results. Limit can be a number from 1 - 100.
        + Default: 10


### List of job applications [GET]

+ Response 200 (application/json)

        [
            "success": true,
            "data": [
                {
                    "id": 1512,
                    "fname": "Peter",
                    "sname": "K.",
                    "application_date": "2018-01-11T08:40:51.620Z",
                    "status": "new"
                },
                {
                    "id": 248,
                    "fname": "Jaroslav",
                    "sname": "Novotný",
                    "application_date": "2018-01-14T18:34:17.186Z",
                    "viewed_date": "2018-01-15T09:03:52.152Z",
                    "status": "viewed"
                }
            ],
            "page": 1,
            "perPage": 2,
            "itemCount": 7,
            "prevPage": null,
            "nextPage": "/jobs/1/applications?page=2"


+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

## Job Application [/jobs/{id}/applications/{application_id}]




## Job Locations Collection [/jobs/{id}/locations{?status,page,limit}]

+ Parameters
    + id (number, required, `15`) - Company identifier as integer.
    + status (string, optional) - Status of application (new, viewed, hired, rejected, released).
    + page (number, optional) - The current page number.
        + Default: 1
    + limit (number, optional) - Maximum of results. Limit can be a number from 1 - 100.
        + Default: 10

### Retrive List of job locations [GET]

+ Response 200 (application/json)

        {
            "success": true,
            "data": [
                {
                      "id": 351,
                      "job_id": 15,
                      "country_key": "SK",
                      "street": "Jakubovo nám. 13",
                      "city": "Bratislava",
                      "postal_code": "811 09",
                      "region": "Bratislavský kraj",
                      "lat": 48.1459258,
                      "lng": 17.1071938  
                },
                {
                      "id": 351,
                      "job_id": 15,
                      "country_key": "SK",
                      "street": "Černyševského 10",
                      "city": "Petržalka",
                      "postal_code": "85104",
                      "region": "Bratislavský kraj",
                      "lat": 48.3804996,
                      "lng": 17.5877285    
                }
            ],
            "page": 1,
            "perPage": 2,
            "itemCount": 7,
            "prevPage": null,
            "nextPage": "/jobs/1/locations?page=2"
        }

+ Response 403 (application/json)

        {
            "success": false,
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

### Create new job location [POST]

+ Request (application/json)

        {
            "address": "Jakubovo nám. 13, Bratislava"
        }

   
+ Response 201 (application/json)

        {
            "success": true,
            "data" :{
                "id": 153,
                "country_key": "SK",
                "street": "Jakubovo námestie 13",
                "city": "Bratislava",
                "postal_code": "811 09",
                "region": "Bratislavský kraj",
                "lat": 48.1459258,
                "lng": 17.1071938 
            }
        }


+ Response 401 (application/json)

        {
            "success": false,
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }

+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

## Job Location [/jobs/{id}/locations/{location_id}]

### Update Job Location [PUT]

+ Request (application/json)

        {
            "address": "Černyševského 10, Bratislava"
        }

   
+ Response 201 (application/json)

        {
            "success": true,
            "data" :{
                "id": 153,
                "country_key": "SK",
                "street": "Černyševského 10",
                "city": "Petržalka",
                "postal_code": "85105",
                "region": "Bratislavský kraj",
                "lat": 48.1459258,
                "lng": 17.1071938 
            }
        }


+ Response 401 (application/json)

        {
            "success": false,
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }

+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }

### Delete Job Location [DELETE]
   
+ Response 204 (application/json)

+ Response 401 (application/json)

        {
            "success": false,
            "errors": [
                {
                    "code": 401,
                    "message" : "Sorry, your access token is invalid or has been expired."
                }
            ]
        }

+ Response 403 (application/json)

        {
            "success": false
            "errors": [
                {
                    "code": 403,
                    "message" : "The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort."
                }
            ]
        }


# Group Changelog

## 0.4 (2018-01-25)
**Update Results**
- results with success
- result with error
- result with pagination
**Update Resource**
- delete job location


## 0.3 (2018-01-17)
**Add Resources**
- Location resourse - basic
**Update Resource**
- company colletion was updated
- job colletion was updated


## 0.2 (2018-01-11)
**Add Resources**
- Job resourse - basic


## 0.1 (2018-01-10)
**Add Resources**
- Company resourse - basic

