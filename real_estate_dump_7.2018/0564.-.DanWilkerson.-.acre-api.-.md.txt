#The Unofficial Allegheny County Real Estate API
An unofficial NodeJS API for retrieving property data from the Allegheny County Real Estate web service.
##Getting Started

	npm install acre-api

Then use the API by requiring it:
	
	var acreApi = require('acre-api');
	acreApi.street.street('Liberty', 'Pittsburgh - All Wards', function(err, parcels) {
		if(err) {
			console.log(err);
		} else {
			// Prints a list of houses on the street
			console.log(parcels);
		}
	});

##search(houseNumber, streetName, errback)
Search for a parcel at a number and street

	acreApi.search(1000, 'Liberty', function(err, parcel) {
		
		if(err) {
			console.log(err);
		} else {
			// Logs generalInfo for parcel
			console.log(parcel);
		}
	});

##Parcel
All parcel methods require a parcel ID

###generalInfo(parcelId, errback)
Returns general information about a parcel.

	acreApi.parcel.generalInfo('0009-P-00150-0000-00', function(err, parcel) {
		
		if(err) {
			console.log(err);
		} else {
			console.log(parcel);
		}
	});

	// Outputs
	{
		parcelId: '0009-P-00150-0000-00',
		municipality: '102  PITTSBURGH - 2ND WARD',
		address: '1000 LIBERTY AVEPITTSBURGH, PA 15222',
		ownerName: 'UNITED STATES OF AMERICA',
		school: 'City Of Pittsburgh',
		taxCode: 'Exempt',
		ownerCode: 'Corporation',
		stateCode: 'Government',
		useCode: 'FEDERAL GOVERNMENT',
		homestead: 'No',
		farmstead: 'No',
		neighborhoodCode: '51C01',
		recordingDate: -316897200000,
		salePrice: 0,
		deedBook: '',
		deedPage: '0',
		abatement: 'No',
		lotArea: 2,
		fullMarketValues: {
			2015:  {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900 
			},
			2014: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900 
			}
		},
		countyAssessedValues:  {
			2015: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900 
			},
			2014: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900 
			}
		}
	};

###buildingInfo(parcelId, errback)
Gets information about the structure on the parcel, if any.

	acreApi.parcel.buildingInfo('0084-N-00285-0000-00', function(err, parcel) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcel);
		}
	});

	// Outputs
	{
		parcelId: '0084-N-00285-0000-00',
		municipality: '107  PITTSBURGH - 7TH WARD',
		address: '5801 WALNUT ST PITTSBURGH, PA 15232',
		ownerName: 'BORETSKY ROBERT H & KAREN R (W)',
		useType: 'THREE FAMILY',
		totalRooms: 12,
		basement: 'Full Basement',
		style: 'MULTI-FAMILY',
		bedrooms: 6,
		grade: 'C+',
		stories: 2,
		fullBaths: 3,
		condition: 'Average',
		yearBuilt: '1900',
		halfBaths: 0,
		fireplaces: 0,
		exterior: 'Brick',
		heat: 'Central Heat',
		garages: 0,
		roof: 'Shingle',
		cooling: '',
		livableSquareFeet: 3362
	}

###taxInfo(parcelId, errback)
Gets tax information about the parcel.

	acreApi.parcel.taxInfo('0084-N-00285-0000-00', function(err, parcel) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcel);
		}
	});

	// Outputs
	{
		parcelId: '0084-N-00285-0000-00',
		municipality: '107  PITTSBURGH - 7TH WARD',
		address: '5801 WALNUT ST PITTSBURGH, PA 15232',
		ownerName: 'BORETSKY ROBERT H & KAREN R (W)',
		taxBillAddr: 'EQUITY REAL ESTATE2029 MURRAY AVEPITTSBURGH PA15217',
		netTaxDueThisMonth: 1251.56,
		grossTaxDueNextMonth: 1277.1,
		taxValue: 270000,
		millageRate: 4.73,
		taxHistory: {
			'2012': {
				paidStatus: 'PAID',
				tax: 978.07,
				penalty: 0,
				interest: 0,
				total: 978.07,
				datePaid: '5/21/2012'
			},
			'2013': {
				paidStatus: 'PAID',
				tax: 1251.56,
				penalty: 0,
				interest: 0,
				total: 1251.56,
				datePaid: '4/15/2013'
			},
			'2014': {
				paidStatus: 'PAID',
				tax: 1251.56,
				penalty: 0,
				interest: 0,
				total: 1251.56,
				datePaid: '3/10/2014'
			},
			'2015': {
				paidStatus: 'UNPAID',
				tax: 1251.56,
				penalty: 0,
				interest: 0,
				total: 1251.56,
				datePaid: '3/31/2015'
			}
		}
	}

###ownerHistory(parcelId, errback)
Gets information about the ownership history of the parcel.

	acreApi.parcel.ownerHistory(parcelId, function(err, parcel) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcel);
		}
	});

	// Outputs
	{
		parcelId: '0084-N-00285-0000-00',
		municipality: '107  PITTSBURGH - 7TH WARD',
		address: '5801 WALNUT ST PITTSBURGH, PA 15232',
		ownerName: 'BORETSKY ROBERT H & KAREN R (W)',
		deedBook: '10857',
		deedPage: '371',
		ownerHistory: [{
			owner: '',
			saleDate: '',
			salePrice: 1
		}, {
			owner: 'ANN MEDIS',
			saleDate: '2/8/1993',
			salePrice: 33000
		}, {
			owner: 'BORETSKY ROBERT H & KAREN R (W)',
			saleDate: '9/1/2000',
			salePrice: 125000
		}]
	}

###image(parcelId, errback)
Gets a link to the exterior photo on file.

	acreApi.parcel.image(parcelId, function(err, parcel) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcel);
		}
	});

	// Outputs
	{
		parcelId: '0084-N-00285-0000-00',
		municipality: '107  PITTSBURGH - 7TH WARD',
		address: '5801 WALNUT ST PITTSBURGH, PA 15232',
		ownerName: 'BORETSKY ROBERT H & KAREN R (W)',
		image: 'http://photos.county.allegheny.pa.us/iasworld/iDoc2/Services/GetPhoto.ashx?parid=0084N00285000000&jur=002&Rank=1&size=350x263'
	}

###comps(parcelId, errback)
Gets back information about comparable parcels.

	acreApi.parcel.comps(parcelId, function(err, parcel) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcel);
		}
	});

	// Outputs
	{
		parcelId: '0084-N-00285-0000-00',
		municipality: '107  PITTSBURGH - 7TH WARD',
		address: '5801 WALNUT ST PITTSBURGH, PA 15232',
		ownerName: 'BORETSKY ROBERT H & KAREN R (W)',
		comps: [{
			address: '5801 WALNUT ST',
			yearBuilt: '1900',
			parcelId: '0084N00285000000',
			salePrice: 190000,
			saleDate: '9/1/2000',
			livableSquareFeet: 3362,
			landValue: 178200,
			bldgValue: 150500,
			totalValue: 328700
		}, {
			address: '5735 HOWE ST',
			yearBuilt: '1900',
			parcelId: '0085A00281000000',
			salePrice: 372500,
			saleDate: '7/23/2010',
			livableSquareFeet: 2710,
			landValue: 182800,
			bldgValue: 157800,
			totalValue: 340600
		}, {
			address: '611 S AIKEN AVE',
			yearBuilt: '1919',
			parcelId: '0052D00118000000',
			salePrice: 260000,
			saleDate: '12/22/2008',
			livableSquareFeet: 2614,
			landValue: 146000,
			bldgValue: 135400,
			totalValue: 281400
		}, {
			address: '5536 KENTUCKY AVE',
			yearBuilt: '1900',
			parcelId: '0085E00038000000',
			salePrice: 380000,
			saleDate: '5/27/2009',
			livableSquareFeet: 2554,
			landValue: 150000,
			bldgValue: 188700,
			totalValue: 338700
		}, {
			address: '5529 HOWE ST',
			yearBuilt: '1910',
			parcelId: '0085A00018000000',
			salePrice: 215000,
			saleDate: '7/27/2009',
			livableSquareFeet: 2418,
			landValue: 149600,
			bldgValue: 64000,
			totalValue: 213600
		}]
	}

##Street
These methods are for retrieving lots of parcels.

###street(streetName, municipality, errback)
Returns top-level information on all of the parcels on a given street within a given municipality. streetName can match many street names.

	acreApi.street.street('Liberty', 'Pittsburgh - All Wards', function(err, parcels) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcels);
		}
	});

	// Outputs
	[{
		parcel_id: '0001-F-00048-0000-00',
		owner_name: 'COMMONWEALTH OF PENNSYLVANIA',
		address: 'LIBERTY AVE',
		municipality: 'PITTSBURGH - 1ST WARD',
		vacant: 'Yes'
	},{
		parcel_id: '0001-F-00020-0000-00',
		owner_name: 'COMMONWEALTH OF PENNSYLVANIA',
		address: 'LIBERTY AVE',
		municipality: 'PITTSBURGH - 1ST WARD',
		vacant: 'no'
	},{
		parcel_id: '0001-C-00200-0000-00',
		owner_name: 'HERTZ GATEWAY CENTER LP',
		address: 'LIBERTY AVE',
		municipality: 'PITTSBURGH - 1ST WARD',
		vacant: 'no'
	},{
		parcel_id: '0001-C-00200-0000-01',
		owner_name: 'PORT AUTHORITY OF ALLEGHENY COUNTY',
		address: 'LIBERTY AVE',
		municipality: 'PITTSBURGH - 1ST WARD',
		vacant: 'no'
	},{
		// ...
	}]

###block(blockNumber, streetName, errback)
Gets all of the parcels on a given block - streetName can match many street names. 

	acreApi.street.block(1000, 'Liberty', function(err, parcels) {
		if(err) {
			console.log(err);
		} else {
			console.log(parcels);
		}
	});

	// Outputs
	[{
		parcelId: '0009-P-00150-0000-00',
		municipality: '102  PITTSBURGH - 2ND WARD',
		address: '1000 LIBERTY AVE PITTSBURGH, PA 15222',
		ownerName: 'UNITED STATES OF AMERICA',
		school: 'City Of Pittsburgh',
		taxCode: 'Exempt',
		ownerCode: 'Corporation',
		stateCode: 'Government',
		useCode: 'FEDERAL GOVERNMENT',
		homestead: 'No',
		farmstead: 'No',
		neighborhoodCode: '51C01',
		recordingDate: '12/17/1959',
		salePrice: 0,
		deedBook: '',
		deedPage: '0',
		abatement: 'No',
		lotArea: 2,
		fullMarketValues: {
			2015: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900
			},
			2014: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900
			}
		},
		countyAssessedValues: {
			2015: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900
			},
			2014: {
				landValue: 7063200,
				buildingValue: 94595700,
				totalValue: 101658900
			}
		},
	},{
		parcelId: '0009-P-00050-0000-00',
		municipality: '102  PITTSBURGH - 2ND WARD',
		address: '1001 LIBERTY AVE PITTSBURGH, PA 15222',
		ownerName: 'IX LIBERTY CENTER OWNER LP',
		school: 'City Of Pittsburgh',
		taxCode: 'Taxable',
		ownerCode: 'Corporation',
		stateCode: 'Commercial',
		useCode: 'HOTELS',
		homestead: 'No',
		farmstead: 'No',
		neighborhoodCode: '51C01',
		recordingDate: '8/9/2013',
		salePrice: 124400000,
		deedBook: '15334',
		deedPage: '322',
		abatement: 'No',
		lotArea: 2,
		fullMarketValues: {
			2015: {
				landValue: 12000000,
				buildingValue: 111500000,
				totalValue: 123500000
			},
			2014: {
				landValue: 12000000,
				buildingValue: 111500000,
				totalValue: 123500000
			}
		},
		countyAssessedValues: {
			2015: {
				landValue: 12000000,
				buildingValue: 111500000,
				totalValue: 123500000
			},
			2014: {
				landValue: 12000000,
				buildingValue: 111500000,
				totalValue: 123500000
			}
		},
	},{
		// ...
	}]

##Municipalities
Methods for finding municipal codes.

###search(municipality)
Returns the municipal code for a given municipal name, if any.

	var muniId = acreApi.municipality.search('Pittsburgh - All Wards');
	console.log(muniId);
	
	// Outputs
	1

###all()
Returns all of the municipalities

	var muniIndex = acreApi.municipality.all();
	console.log(muniIndex);

	// Outputs
	{
		'Aleppo': 901,
		'Aspinwall': 801,
		'Avalon': 802,
		'Baldwin Boro': 877,
		...
	}

#Acknowledgements
The Allegheny County Real Estate API is maintained by [Dan Wilkerson](http://danwilkerson.com) and is in no way associated with the government of Allegheny County, its affiliates, or its subsidiaries.

&copy;2015 Dan Wilkerson under the [MIT License](http://opensource.org/licenses/mit-license.php).
