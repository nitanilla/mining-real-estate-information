# lone-wolf

A node.js client for the [Lone Wolf](https://www.lwolf.com) WolfConnect API. This module supports all endpoints that were published in the Lone Wolf API Resource Guides, as of 2015-01-05.

### Authentication

To use this module you'll need to obtain a `customer key` and `secret key` from Lone Wolf Real Estate Technologies. Lone Wolf will also provide you with a copy of their Intrgration Guide, which will have instructions for generating an `API token`.

## Installation

```cli
npm install lone-wolf
```

## Usage

This module requires you to pass three values to the constructor, `apiToken`, `clientCode`, and `secretKey`. These values will be used to generate the `Content-MD5` and `Authorization` headers that are required to validate each API request.

```Javascript
var LoneWolf = require('lone-wolf');
var api = new LoneWolf({
	apiToken: 'your-api-token',
	clientCode: 'your-client-code',
	secretKey: 'your-secret-key'
});
```

## Callbacks or Promises

All of the methods below will work with either a standard Javascipt callback function `(error, result)` or promises. This module uses the Bluebird promise library.

## Methods

* getPropertyTypes
* getClassifications
* getContactTypes
* getMembers
* getMembersInOutStatus
* getMember
* getMemberProfileImage
* setMemberProfileImage
* deleteMemberProfileImage
* getMemberPublicProfileImage
* getMemberInOutStatus
* getTransactions
* getTransaction
* createTransaction
* updateTransaction
* finalizeTransaction
* deleteTransaction

#### getPropertyTypes(*[callback]*)

All of the property types that are configured for the Client Code used during the authentication process will be returned. The property types returned where LWCompanyCode is blank are for offices that are not synced with brokerWOLF. 

**Sample Response**
```javascript
[
    {
        "Id": "I1LeQ4ZKZdwWWSWPdobXBQ==",
        "Class": "Commercial",
        "LWCompanyCode": "",
        "Code": "Com",
        "Name": "Commercial",
        "Default": false,
        "ClassCode": "C",
        "InactiveDate": null
    },
    {
        "Id": "UsQZDrX_zlF-ndCfgQZFoQ==",
        "Class": "Residential",
        "LWCompanyCode": "",
        "Code": "Res",
        "Name": "Residential",
        "Default": false,
        "ClassCode": "R",
        "InactiveDate": null
    },
    ...
]
```

#### getClassifications(*[callback]*)

All of the classifications that are configured for the Client Code used during the authentication process will be returned. The classifications returned where LWCompanyCode is blank are for offices that are not synced with brokerWOLF.  

**Sample Response**
```javascript
[
    {
        "Id": "I1LeQ4ZKZdwWWSWPdobXBQ==",
        "LWCompanyCode": "",
        "Code": "AP",
        "Name": "Appraisals",
        "EndCount": 0,
        "InactiveDate": null
    },
    {
        "Id": "UsQZDrX_zlF-ndCfgQZFoQ==",
        "LWCompanyCode": "",
        "Code": "LE",
        "Name": "Lease/Rentals",
        "EndCount": 0,
        "InactiveDate": null
    },
    ...
]
```

#### getContactTypes(*[callback]*)

All of the contact types that are configured for the Client Code used during the authentication process will be returned. The contact types returned where LWCompanyCode is blank are for offices that are not synced with brokerWOLF.

**Sample Response**
```javascript
[
    {
        "Id": "I1LeQ4ZKZdwWWSWPdobXBQ==",
        "LWCompanyCode": "",
        "Code": "Escrow",
        "Name": "Escrow",
        "CategoryCode": "B",
        "InactiveDate": "2015-12-10"
    },
    {
        "Id": "UsQZDrX_zlF-ndCfgQZFoQ==",
        "LWCompanyCode": "",
        "Code": "Lawyer",
        "Name": "Lawyer",
        "CategoryCode": "B",
        "InactiveDate": "2015-12-10"
    },
    ...
]
```

#### getMembers(*[options]*, *[callback]*)

Retrieves a collection of members within the current client code. OData can be used to filter, order and page through the list. 

**Available Options**

| Name        | Description |
|:------------|:------------|
| $expand     | causes related entities to be included inline in the results. |
| $filter     | specifies an expression for filtering results. | 
| $orderby    | specifies an expression for determining what values are used to order the results. | 
| $skip       | skipts the first N items of the result set. | 
| $top        | selects only the first N items of the result set. |

**Sample Code**
```javascript
//gets the first 100 members
api.getMembers({$top: 100})
.then(function(results) {
	//do something with the results
});
```

**Sample Response**
```javascript
[
    {
        "Id": "rXIMmtQ5eC5000l5ntjzsg==",
        "MemberTypeId": "i2qvo45Ne5XkHLIQFRAASg==",
        "OfficeId": "vmb6hx000CY6IjV9eL36Ew==",
        "CreatedTimestamp": "2015-01-01T11:50:01.5570000+00:00",
        "ModifiedTimestamp": "2015-01-01T11:50:01.5570000+00:00",
        "MemberChangedTimestamp": "2015-01-01T11:50:01.5570000+00:00",
        "FirstName": "Test",
        "MiddleName": "",
        "LastName": "User",
        "Number": "1234",
        "Title": "",
        "Suffix": "",
        "Nickname": "",
        "GenderCode": "",
        "LegalName": "",
        "Username": "testuser",
        "LoadingDocsUsername": "testuser",
        "AnniversaryDate": "2000-01-01",
        "BirthDate": "1970-01-01",
        "CommencementDate": "2000-01-01",
        "InactiveDate": null,
        "StartDate": "2010-12-31",
        "Office": {
            "Id": "vmb6hx3fxC0000V9eL36Ew==",
            "Name": "Test Office",
            "LWCompanyCode": ""
        },
        "MemberType": {
            "Id": "i2qvo45Ne5XkHLIQFRAASg==",
            "Name": "Agent",
            "Code": null
        },
        "Addresses": [
            {
                "Line1": "123 Main St",
                "Line2": "Suite A",
                "Line3": "",
                "Line4": "",
                "City": "San Francisco",
                "ProvinceCode": "CA",
                "Province": "California",
                "PostalCode": "95001",
                "CountryCode": "US",
                "Country": "United States",
                "Type": "Mailing",
                "TypeCode": "M",
                "Confidential": false
            }
        ],
        "EmailAddresses": [
            {
                "TypeCode": "B",
                "Type": "Business",
                "Address": "test@example.com",
                "Primary": null
            }
        ],
        "MLSBoards": [],
        "PhoneNumbers": [
            {
                "TypeCode": "B",
                "Type": "Business",
                "Number": "4155551212",
                "Extension": "",
                "Primary": false,
                "Confidential": false
            }
        ],
        "PublicProfiles": [
            {
                "CreatedTimestamp": "2016-01-01T11:50:01.5570000+00:00",
                "ModifiedTimestamp": "2016-01-01T11:50:01.5570000+00:00",
                "Name": "globalWOLF",
                "FirstName": "",
                "MiddleName": "",
                "LastName": "",
                "Title": "",
                "Addresses": [],
                "EmailAddresses": [],
                "PhoneNumbers": [],
                "Websites": []
            }
        ],
        "Tags": [],
        "Websites": []
    },
    ...
]
```

#### getMembersInOutStatus(*[callback]*)

Returns the in/out statuses and the notes and detailed notes for all active members for a given client code.

**Sample Code**
```javascript
api.getMembersInOutStatus()
.then(function(results) {
	//do something with the results
});
```

**Sample Response**
```javascript
//unable to get a sample response, since my credentials didn't have access to this endpoint.
```

#### getMember(*memberId*, *[options]*, *[callback]*)

Retrieves a Member. The data in the response will contain all of the data to which you have read access. Properties with values of NULL typically mean that you do not have read access to that property. Please see the Permissions section of the Lone Wolf API Integration Guide for more information.

**Available Options**

| Name        | Description |
|:------------|:------------|
| $expand     | causes related entities to be included inline in the results. |


**Sample Code**
```javascript
api.getMember('rXIMmtQ5eC5000l5ntjzsg==')
.then(function(member) {
	//do something with the member object
});
```

**Sample Response**
```javascript
{
    "Id": "rXIMmtQ5eC5000l5ntjzsg==",
    "MemberTypeId": "i2qvo45Ne5XkHLIQFRAASg==",
    "OfficeId": "vmb6hx000CY6IjV9eL36Ew==",
    "CreatedTimestamp": "2015-01-01T11:50:01.5570000+00:00",
    "ModifiedTimestamp": "2015-01-01T11:50:01.5570000+00:00",
    "MemberChangedTimestamp": "2015-01-01T11:50:01.5570000+00:00",
    "FirstName": "Test",
    "MiddleName": "",
    "LastName": "User",
    "Number": "1234",
    "Title": "",
    "Suffix": "",
    "Nickname": "",
    "GenderCode": "",
    "LegalName": "",
    "Username": "testuser",
    "LoadingDocsUsername": "testuser",
    "AnniversaryDate": "2000-01-01",
    "BirthDate": "1970-01-01",
    "CommencementDate": "2000-01-01",
    "InactiveDate": null,
    "StartDate": "2010-12-31",
    "Office": {
        "Id": "vmb6hx3fxC0000V9eL36Ew==",
        "Name": "Test Office",
        "LWCompanyCode": ""
    },
    "MemberType": {
        "Id": "i2qvo45Ne5XkHLIQFRAASg==",
        "Name": "Agent",
        "Code": null
    },
    "Addresses": [
        {
            "Line1": "123 Main St",
            "Line2": "Suite A",
            "Line3": "",
            "Line4": "",
            "City": "San Francisco",
            "ProvinceCode": "CA",
            "Province": "California",
            "PostalCode": "95001",
            "CountryCode": "US",
            "Country": "United States",
            "Type": "Mailing",
            "TypeCode": "M",
            "Confidential": false
        }
    ],
    "EmailAddresses": [
        {
            "TypeCode": "B",
            "Type": "Business",
            "Address": "test@example.com",
            "Primary": null
        }
    ],
    "MLSBoards": [],
    "PhoneNumbers": [
        {
            "TypeCode": "B",
            "Type": "Business",
            "Number": "4155551212",
            "Extension": "",
            "Primary": false,
            "Confidential": false
        }
    ],
    "PublicProfiles": [
        {
            "CreatedTimestamp": "2016-01-01T11:50:01.5570000+00:00",
            "ModifiedTimestamp": "2016-01-01T11:50:01.5570000+00:00",
            "Name": "globalWOLF",
            "FirstName": "",
            "MiddleName": "",
            "LastName": "",
            "Title": "",
            "Addresses": [],
            "EmailAddresses": [],
            "PhoneNumbers": [],
            "Websites": []
        }
    ],
    "Tags": [],
    "Websites": []
}
```

#### getMemberProfileImage(*memberId*, *[options]*, *[callback]*)

Retrieves the base64 encoded profile image for the member that was uploaded through the member profile page in WOLFconnect.

**Options**

| Name         | Description |
|:-------------|:------------|
| size          | The size of the image returned.<br/><br/>`normal`: 150 X 200 (Default)<br/>`small`: 100 X 133<br/>`tiny`: 70 X 93 |
| width        | Specifies a custom width of for the returned image. The height will be adjusted to keep the same aspect ratio. The width can only be a number less than or equal to 150, as that is the max width of any stored image. |

**Sample Code**
```javascript
api.getMemberProfileImage('rXIMmtQ5eC5000l5ntjzsg==', {size: 'tiny'})
.error(function(err) {
	//could throw an error, if the user has no profile image
})
.then(function(image) {
	//do something with the image.
});
```

#### setMemberProfileImage(*memberId*, *formData*, *[callback]*)

Sets the profile image for a member. The request must be a multi-part request containing the original image and the coordinates to use to crop the image.

**Form Data**

| Name         | Description |
|:-------------|:------------|
| left         | The left image coordinate of the cropping rectangle. |
| top          | The top image coordinate of the cropping rectangle. |
| width        | The width of the cropping rectangle. |
| height       | The height of the cropping rectangle. |
| profileImage | The original image file to use for the profile image. This is the image that will be cropped using the coordinates above. This should be a `Buffer`. |

The coordinates should be specified in an aspect ratio of 3:4. For instance, if you have an image that is 800 X 800, and you want the center of the image selected for the profile image, you would pass in the following for the coordinates:

| Name         | Description |
|:-------------|:------------|
| Left         | 100         |
| Top          | 0           |
| Width        | 600         |
| Bottom       | 800         |

This will set the profile image to start 100 pixels from the left and go 600 pixels wide. 600 X 800 is in the 3:4 ratio.

*You can specify 0 for all the coordinates and the API will create the biggest possible image from the original image. It would save the same image as above if all parameters were set to 0. It will center the rectangle horizontally if the original image is too wide and it will use the top of the original image if it is too long.*

**Sample Code**
```javascript
var formData = {
	left: 0,
	top: 0,
	width: 0,
	height: 0,
	profileImage: fs.readFileSync(__dirname + '/profilephoto_small.jpg')
}

api.setMemberProfileImage('rXIMmtQ5eC5000l5ntjzsg==', formData)
.error(function(err) {
	//could throw an error, if the user has no profile image
})
.then(function(image) {
	//do something with the image.
});
```

#### deleteMemberProfileImage(*memberId*, *[callback]*)

Deletes the profile image for the member. 

*NOTE: This resource returns OK even if the member does not have a profile image.*

**Sample Code**
```javascript
api.deleteMemberProfileImage('rXIMmtQ5eC5000l5ntjzsg==')
.error(function(err) {
	//could throw an error, if the user has no profile image
})
.error(function(err) {
	//will return an error if you don't have permission to delete the image.
})
.then(function(response) {
	//response will be blank if successful.
});
```

#### getMemberPublicProfileImage(*memberId*, *[callback]*)

Retrieves the base64 encoded public profile image for the member that was uploaded through the public profile page in WOLFconnect. Members can have different images for their internal profile as opposed to their public profiles. By default, if no public profile image has been uploaded, then the member profile image is returned.

**Options**

| Name         | Description |
|:-------------|:------------|
| publicProfileOnly         | Flag to tell the API whether or not to return the internal profile image if the public profile image does not exist. <br/><br/>`true`: Do not return the internal profile image when no public profile image exists.<br/><br/>`false`: Return the internal profile image when no public profile image exists. (Default)  |
| size          | The size of the image returned.<br/><br/>`normal`: 150 X 200 (Default)<br/>`small`: 100 X 133<br/>`tiny`: 70 X 93 |
| width        | Specifies a custom width of for the returned image. The height will be adjusted to keep the same aspect ratio. The width can only be a number less than or equal to 150, as that is the max width of any stored image. |

**Sample Code**
```javascript
api.getMemberPublicProfileImage('rXIMmtQ5eC5000l5ntjzsg==')
.error(function(err) {
	//could throw an error, if the user has no profile image
})
.then(function(image) {
	//do something with the image.
});
```

#### getMemberInOutStatus(*memberId*, *[callback]*)

Gets the in/out status (displayed in the top-left corner of WOLFconnect) and the notes and detailed notes for the member (if enabled, displayed on the In/Out popup window that appears when first logging in).

**Sample Code**
```javascript
api.getMemberInOutStatus('rXIMmtQ5eC5000l5ntjzsg==')
.then(function(results) {
	//do something with the results
});
```

**Sample Response**
```javascript
//unable to get a sample response, since my credentials didn't have access to this endpoint.
```

#### getTransactions(*[options]*, *[callback]*)

Retrieves a collection of transactions within the current client code. OData can be used to filter, order and page through the list. 

**Available Options**

| Name        | Description |
|:------------|:------------|
| $expand     | causes related entities to be included inline in the results. |
| $filter     | specifies an expression for filtering results. | 
| $orderby    | specifies an expression for determining what values are used to order the results. | 
| $skip       | skipts the first N items of the result set. | 
| $top        | selects only the first N items of the result set. |


**Sample Code**
```javascript
api.getTransactions()
.then(function(results) {
	//do something with the results
});
```

**Sample Response**
```javascript
[
    {
        "Id": "x4VNnqE4000RFXHFhwggpQ==",
        "PropertyTypeId": "UsQZDrX_zlF-ndCfgQZFoQ==",
        "ClassificationId": "XYem-Xc45UpJ8Bl5VdE-hg==",
        "Status": "Open",
        "CreatedTimestamp": "2016-01-01T11:52:16.7470000+00:00",
        "ModifiedTimestamp": "2016-01-01T11:52:16.7470000+00:00",
        "TransactionChangedTimestamp": "2016-01-02T11:52:18.0570000+00:00",
        "Number": "123",
        "MLSNumber": "",
        "EntryDate": "2016-01-01",
        "CloseDate": "2016-02-01",
        "OfferDate": "2016-01-01",
        "SellPrice": 125000,
        "StatusCode": "N",
        "LegalDescription": "",
        "RowVersion": 1649000,
        "MLSAddress": {
            "StreetNumber": "123",
            "StreetName": "Main St",
            "StreetDirection": "",
            "Unit": "",
            "City": "San Francisco",
            "ProvinceCode": "CA",
            "Province": "California",
            "PostalCode": "95001",
            "CountryCode": "US",
            "Country": "United States"
        },
        "PropertyType": {
            "Id": "UsQZDrX_zlF-ndCfgQZFoQ==",
            "Class": "Residential",
            "LWCompanyCode": "",
            "Code": "Res",
            "Name": "Residential",
            "Default": false,
            "ClassCode": "R",
            "InactiveDate": null
        },
        "Classification": {
            "Id": "XYem-Xc45UpJ8Bl5VdE-hg==",
            "LWCompanyCode": "",
            "Code": "S",
            "Name": "Selling",
            "EndCount": 1,
            "InactiveDate": null
        },
        "BusinessContacts": [],
        "ClientContacts": [],
        "Conditions": [],
        "Tasks": [],
        "Tiers": [
            {
                "Id": "kAjU9tx0000xGV6a2sHPWQ==",
                "ClassificationId": "I1LeQ4ZKZdwWWSWPdobXBQ==",
                "Status": "Open",
                "CreatedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
                "ModifiedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
                "Name": null,
                "StatusCode": "N",
                "SellPrice": 125000,
                "CloseDate": "2016-02-01",
                "SellingCommission": 7500,
                "BuyingCommission": 0,
                "TotalCommission": 7500,
                "RowVersion": 1649002,
                "Classification": {
                    "Id": "I1LeQ4ZKZdwWWSWPdobXBQ==",
                    "LWCompanyCode": "",
                    "Code": "AP",
                    "Name": "Appraisals",
                    "EndCount": 0,
                    "InactiveDate": null
                },
                "AgentCommissions": [
                    {
                        "Id": "bM4XGPUbkuo0000imfLyWw==",
                        "AgentId": "rXIMmtV50000EHl5ntjzsg==",
                        "TeamLeaderId": "",
                        "End": "Selling",
                        "CreatedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
                        "ModifiedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
                        "EndCode": "S",
                        "EndCount": 1,
                        "CommissionPercentage": 0.03,
                        "Commission": 7500,
                        "RowVersion": 1649003,
                        "Agent": {
                            "Id": "rXIMmtV50000EHl5ntjzsg==",
                            "OfficeId": "vmb6hx3fx0000jV9eL36Ew==",
                            "FirstName": "Test",
                            "MiddleName": null,
                            "LastName": "Agent"
                        },
                        "TeamLeader": null
                    }
                ],
                "ExternalAgentCommissions": []
            }
        ]
    },
    ...
]
```

#### getTransaction(*transactionId*, *[options]*, *[callback]*)

Retrieves a transaction. The data in the response will contain all of the data to which you have read access. Properties with values of NULL typically mean that you do not have read access to that property. Please see the Permissions section of the Lone Wolf API Integration Guide for more information.

**Available Options**

| Name        | Description |
|:------------|:------------|
| $expand     | causes related entities to be included inline in the results. |

**Sample Code**
```javascript
api.getTransaction('x4VNnqE4000RFXHFhwggpQ==')
.then(function(transaction) {
	//do something with the transaction
});
```

**Sample Response**
```javascript
{
    "Id": "x4VNnqE4000RFXHFhwggpQ==",
    "PropertyTypeId": "UsQZDrX_zlF-ndCfgQZFoQ==",
    "ClassificationId": "XYem-Xc45UpJ8Bl5VdE-hg==",
    "Status": "Open",
    "CreatedTimestamp": "2016-01-01T11:52:16.7470000+00:00",
    "ModifiedTimestamp": "2016-01-01T11:52:16.7470000+00:00",
    "TransactionChangedTimestamp": "2016-01-02T11:52:18.0570000+00:00",
    "Number": "123",
    "MLSNumber": "",
    "EntryDate": "2016-01-01",
    "CloseDate": "2016-02-01",
    "OfferDate": "2016-01-01",
    "SellPrice": 125000,
    "StatusCode": "N",
    "LegalDescription": "",
    "RowVersion": 1649000,
    "MLSAddress": {
        "StreetNumber": "123",
        "StreetName": "Main St",
        "StreetDirection": "",
        "Unit": "",
        "City": "San Francisco",
        "ProvinceCode": "CA",
        "Province": "California",
        "PostalCode": "95001",
        "CountryCode": "US",
        "Country": "United States"
    },
    "PropertyType": {
        "Id": "UsQZDrX_zlF-ndCfgQZFoQ==",
        "Class": "Residential",
        "LWCompanyCode": "",
        "Code": "Res",
        "Name": "Residential",
        "Default": false,
        "ClassCode": "R",
        "InactiveDate": null
    },
    "Classification": {
        "Id": "XYem-Xc45UpJ8Bl5VdE-hg==",
        "LWCompanyCode": "",
        "Code": "S",
        "Name": "Selling",
        "EndCount": 1,
        "InactiveDate": null
    },
    "BusinessContacts": [],
    "ClientContacts": [],
    "Conditions": [],
    "Tasks": [],
    "Tiers": [
        {
            "Id": "kAjU9tx0000xGV6a2sHPWQ==",
            "ClassificationId": "I1LeQ4ZKZdwWWSWPdobXBQ==",
            "Status": "Open",
            "CreatedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
            "ModifiedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
            "Name": null,
            "StatusCode": "N",
            "SellPrice": 125000,
            "CloseDate": "2016-02-01",
            "SellingCommission": 7500,
            "BuyingCommission": 0,
            "TotalCommission": 7500,
            "RowVersion": 1649002,
            "Classification": {
                "Id": "I1LeQ4ZKZdwWWSWPdobXBQ==",
                "LWCompanyCode": "",
                "Code": "AP",
                "Name": "Appraisals",
                "EndCount": 0,
                "InactiveDate": null
            },
            "AgentCommissions": [
                {
                    "Id": "bM4XGPUbkuo0000imfLyWw==",
                    "AgentId": "rXIMmtV50000EHl5ntjzsg==",
                    "TeamLeaderId": "",
                    "End": "Selling",
                    "CreatedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
                    "ModifiedTimestamp": "2016-01-01T11:52:16.7930000+00:00",
                    "EndCode": "S",
                    "EndCount": 1,
                    "CommissionPercentage": 0.03,
                    "Commission": 7500,
                    "RowVersion": 1649003,
                    "Agent": {
                        "Id": "rXIMmtV50000EHl5ntjzsg==",
                        "OfficeId": "vmb6hx3fx0000jV9eL36Ew==",
                        "FirstName": "Test",
                        "MiddleName": null,
                        "LastName": "Agent"
                    },
                    "TeamLeader": null
                }
            ],
            "ExternalAgentCommissions": []
        }
    ]
}
```

#### createTransaction(*transaction*, *[options]*, *[callback]*)

A new Transaction must have one Tier associated to it and that Tier must have at least one AgentCommission associated to it; you will receive a validation error if you send a Transaction object without that data.

`Number` should be set to NULL unless the primary office for the transaction allows manual entry of a transaction number. The response will contain the newly created transaction object populated with all of the data to which you have read access. 

You can use the OData `$expand` option to limit the data that is returned. 

Please see the Creating and Updating Data section of the Lone Wolf API Integration Guide for more information on how to set property values.

*The response returned by this method is identical to the `getTransaction` response.*

**Available Options**

| Name        | Description |
|:------------|:------------|
| $expand     | causes related entities to be included inline in the results. |

**Sample Code**
```javascript
var transaction = {
	ClassificationId: 'XYem-Xc45UpJ8Bl5VdE-hg==',
	PropertyTypeId: 'UsQZDrX_zlF-ndCfgQZFoQ==',
	SellPrice: 1000000,
	CloseDate: '2016-02-03',
	OfferDate: '2016-01-03',
	MLSAddress: {
		StreetNumber: '123',
		StreetName: 'Main St',
		City: 'San Jose',
		ProvinceCode: 'CA',
		PostalCode: '95125',
		CountryCode: 'US',
		Country: 'United States'
	},
	Tiers: [
		{
			ClassificationId: 'I1LeQ4ZKZdwWWSWPdobXBQ==',
			CloseDate: '2016-02-03',
			Status: 'Open',
			StatusCode: 'N',
			SellPrice: 1000000,
			AgentCommissions: [
				{
					AgentId: 'rXIMmtV5eC0000l5ntjzsg==',
					End: 'Selling',
					EndCode: 'S',
					EndCount: 1,
					CommissionPercentage: 0.03,
					Commission: 30000
				}
			]
		}
	]
}

api.createTransaction(transaction)
.error(function(err) {
	//errors may be returned if validation is not successful.
})
.then(function(results) {
	//do something with the response
});
```

#### updateTransaction(*transactionId*, *transaction*, *[options]*, *[callback]*)

It is best practice to only send data that you want updated as it will return a much faster response. For instance, if you only need to update the Transaction.CloseDate value, then you should set all other Transaction properties to null so that only a close date update is attempted.

Unless the primary office allows manual entry for a transaction number and you actually want to change the transaction number, it is best to always set the Transaction.Number property to NULL before sending the request. This will guarantee that the transaction number is not updated. 

The status of a transaction cannot be updated using this resource. The status is a read only property. You must use finalize resource to change the status. 

Please see the Creating and Updating Data section of the Lone Wolf API Integration Guide for more information on how to set property values.

The response will contain the updated transaction object populated with all of the data to which you have read access regardless of the properties sent in the request. For instance, if you sent a Transaction object with the Conditions property set to null but the transaction contained 2 conditions, the Transaction.Conditions property of the response will contain those 2 conditions. You can use the OData $expand parameter to limit the data that is returned. 

**Available Options**

| Name        | Description |
|:------------|:------------|
| $expand     | causes related entities to be included inline in the results. |

**Sample Code**
```javascript
var updatedValues = {
	MLSNumber: '12345'
}

api.updateTransaction('x4VNnqE4000RFXHFhwggpQ==', transaction)
.error(function(err) {
	//errors may be returned if validation is not successful.
})
.then(function(results) {
	//do something with the response
});
```

#### finalizeTransaction(*transactionId*, *statusCode*, *[callback]*)

The status of a transaction cannot be updated through the normal update process as you must call this resource to change the status. This resource will finalize all of the associated transaction tiers with the specified status code as well. 

| Status Code | Description |
|:------------|:------------|
| N | Open |
| A | Closed |
| P | Partially closed (not all but at least one tier has been finalized) |
| B | Fallen through because of a condition |
| C | Fallen through |

**TODO: This method is untested. Need to talk to Lone Wolf about request format. Documentation states "A string holding the status code for the finalized transaction."**

**Sample Code**
```javascript
api.finalizeTransaction('x4VNnqE4000RFXHFhwggpQ==', 'C')
.error(function(err) {
	//errors may be returned.
})
.then(function(results) {
	//do something with the response
});
```

**Sample Response**
```javascript
//unable to get a sample response, since I haven't been able to test this method.
```

#### deleteTransaction(*transactionId*, *[callback]*)

Deletes a transaction. There is no way to undo this operation, so please use caution. 

**Sample Code**
```javascript
api.deleteTransaction('x4VNnqE4000RFXHFhwggpQ==')
.error(function(err) {
	//errors may be returned.
})
.then(function(results) {
	//a successful response will return an empty string.
});
```
