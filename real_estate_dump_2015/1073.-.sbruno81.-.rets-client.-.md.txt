rets-client
===========
A RETS (Real Estate Transaction Standard) client for Node.js.


## Changes

#### 3.2.2

Version 3.2.2 adds support for per-object errors when calling `client.objects.getPhotos()`.  The
[Example RETS Session](#example-rets-session) illustrates proper error checking.

#### 3.2.0

Version 3.2 passes through any multipart headers (except for content-disposition, which gets split up first;
content-type which is renamed to `mime`; and content-transfer-encoding which is used internally and not passed) onto
the objects resolved from `client.objects.getPhotos()`. It also fixes a race condition in `client.objects.getPhotos()`.

#### 3.1.0

Version 3.1 adds a `response` field to the object resolved from `client.objects.getObject()`, containing the full HTTP
response object.  It also fixes a major bug interfering with `client.objects.getPhotos()` and
`client.objects.getObject()` calls.

#### 3.0.0

Version 3.x is out!  This represents a substantial rewrite of the underlying code, which should improve performance
(both CPU and memory use) for almost all RETS calls by using node-expat instead of xml2js for xml parsing.  The changes
are mostly internal, however there is 1 small backward-incompatible change needed for correctness, described below.
The large internal refactor plus even a small breaking change warrants a major version bump.

Version 3.x has almost the same interface as 2.x, which is completely different from 1.x.  If you wish to continue to
use the 1.x version, you can use the [v1 branch](https://github.com/sbruno81/rets-client/tree/v1).

Many of the metadata methods are capable of returning multiple sets of data, including (but not limited to) the
getAll* methods.  Versions 1.x and 2.x did not handle this properly; ~~version 1.x returns the values from the last set
encountered~~, and version 2.x returns the values from the first set encountered.  (This has been corrected in version
1.2.0.)  Version 3.x always returns all values encountered, by returning an array of data sets rather than a single one.  

In addition to the methods available in 2.x, version 3.0 adds `client.search.stream.searchRets()`, which returns a
text stream of the raw XML result, and `client.search.stream.query()`, which returns a stream of low-level objects
parsed from the XML.  (See the [streaming example](#simple-streaming-example) below.)  These streams, if used properly,
should result in a much lower memory footprint than their corresponding non-streaming counterparts.


## Implementation Notes

This interface uses promises, and an optional stream-based interface for better performance with large search results.
Future development will include an optional stream-based interface for object downloads, and an improved API for the
non-streaming object methods.

This library is written primarily in CoffeeScript, but may be used just as easily in a Node app using Javascript or
CoffeeScript.  Promises in this module are provided by [Bluebird](https://github.com/petkaantonov/bluebird).

The original module was developed against a server running RETS v1.7.2, so there may be incompatibilities with other
versions.  However, we want this library to work against any RETS servers that are in current use, so issue tickets
describing problems or (even better) pull requests that fix interactions with servers running other versions of RETS
are welcomed.

For more information about what all the parameters and return values and such mean, you might want to look at the
[RETS Specifications](http://www.reso.org/specifications)


## Contributions
Issue tickets and pull requests are welcome.  Pull requests must be backward-compatible to be considered, and ideally
should match existing code style.

#### TODO
- create optional streaming interface for object downloads; when implemented, this will be a 4.0 release
- create unit tests -- specifically ones that run off example RETS data rather than requiring access to a real RETS server


## Example Usage

##### Client Configuration
```javascript
    //create rets-client
    var clientSettings = {
        loginUrl:retsLoginUrl,
        username:retsUser,
        password:retsPassword,
        version:'RETS/1.7.2',
        userAgent:'RETS node-client/3.0'
    };
...
```    
##### Client Configuration with UA Authorization
```javascript
    //create rets-client
    var clientSettings = {
        version:'RETS/1.7.2',
        userAgent:userAgent,
        userAgentPassword:userAgentPassword,
        sessionId:sessionId
    };
...
```

#### Example RETS Session
```javascript
  var rets = require('rets-client');
  var fs = require('fs');
  var photoSourceId = '12345'; // <--- dummy example ID!  this will usually be a MLS number / listing id
  var outputFields = function(obj, fields) {
    for (var i=0; i<fields.length; i++) {
      console.log(fields[i]+": "+obj[fields[i]]);
    }
    console.log("");
  };
  // establish connection to RETS server which auto-logs out when we're done
  rets.getAutoLogoutClient(clientSettings, function (client) {
    //get resources metadata
    return client.metadata.getResources()
      .then(function (data) {
        console.log("======================================");
        console.log("========  Resources Metadata  ========");
        console.log("======================================");
        outputFields(data, ['Version', 'Date']);
        for (var dataItem = 0; dataItem < data.results[0].metadata.length; dataItem++) {
          console.log("-------- Resource " + dataItem + " --------");
          outputFields(data.results[0].metadata[dataItem], ['ResourceID', 'StandardName', 'VisibleName', 'ObjectVersion']);
        }
      }).then(function () {
        //get class metadata
        return client.metadata.getClass("Property");
      }).then(function (data) {
        console.log("===========================================================");
        console.log("========  Class Metadata (from Property Resource)  ========");
        console.log("===========================================================");
        outputFields(data, ['Version', 'Date', 'Resource']);
        for (var classItem = 0; classItem < data.results[0].metadata.length; classItem++) {
          console.log("-------- Table " + classItem + " --------");
          outputFields(data.results[0].metadata[classItem], ['ClassName', 'StandardName', 'VisibleName', 'TableVersion']);
        }
      }).then(function () {
        //get field data for open houses
        return client.metadata.getTable("OpenHouse", "OPENHOUSE");
      }).then(function (data) {
        console.log("=============================================");
        console.log("========  OpenHouse Table Metadata  ========");
        console.log("=============================================");
        outputFields(data, ['Version', 'Date', 'Resource', 'Class']);
        for (var tableItem = 0; tableItem < data.results[0].metadata.length; tableItem++) {
          console.log("-------- Field " + tableItem + " --------");
          outputFields(data.results[0].metadata[tableItem], ['MetadataEntryID', 'SystemName', 'ShortName', 'LongName', 'DataType']);
        }
        return data.results[0].metadata
      }).then(function (fieldsData) {
        var plucked = [];
        for (var fieldItem = 0; fieldItem < fieldsData.length; fieldItem++) {
          plucked.push(fieldsData[fieldItem].SystemName);
        }
        return plucked;
      }).then(function (fields) {
        //perform a query using DQML2 -- pass resource, class, and query, and options
        return client.search.query("OpenHouse", "OPENHOUSE", "(OpenHouseType=PUBLIC),(ActiveYN=1)", {limit:100, offset:10})
        .then(function (searchData) {
          console.log("===========================================");
          console.log("========  OpenHouse Query Results  ========");
          console.log("===========================================");
          console.log("");
          //iterate through search results
          for (var dataItem = 0; dataItem < searchData.results.length; dataItem++) {
            console.log("-------- Result " + dataItem + " --------");
            outputFields(searchData.results[dataItem], fields);
          }
          if (searchData.maxRowsExceeded) {
            console.log("-------- More rows available!");
          }
        });
      }).then(function () {
        // get photos
        return client.objects.getPhotos("Property", "LargePhoto", photoSourceId)
      }).then(function (photoList) {
        console.log("=================================");
        console.log("========  Photo Results  ========");
        console.log("=================================");
        for (var i = 0; i < photoList.length; i++) {
          if (photoList[i].error) {
            var msg;
            if (photoList[i].error instanceof rets.RetsReplyError) {
              msg = "Photo " + (i + 1) + " had an error: " + photoList[i].error;
            } else {
              msg = "Parsing error encountered after photo " + i +
                "; more photos may have been available.  Error: " + photoList[i].error;
            }
            console.log(msg);
          } else {
            console.log("Photo " + (i + 1) + " MIME type: " + photoList[i].mime);
            fs.writeFileSync(
              "/tmp/photo" + (i + 1) + "." + photoList[i].mime.match(/\w+\/(\w+)/i)[1],
              photoList[i].buffer
            );
          }
        }
      });
  }).catch(function (error) {
    console.log("ERROR: issue encountered: "+(error.stack||error));
  });
```

#### Simple streaming example
```javascript
  var rets = require('rets-client');
  var through2 = require('through2');
  var Promise = require('bluebird');
  // establish connection to RETS server which auto-logs out when we're done
  rets.getAutoLogoutClient(clientSettings, function (client) {
    // in order to have the auto-logout function work properly, we need to make a promise that either rejects or
    // resolves only once we're done processing the stream
    return new Promise(function (reject, resolve) {
      var retsStream = client.search.stream.query("OpenHouse", "OPENHOUSE", "(OpenHouseType=PUBLIC),(ActiveYN=1)", {limit:100, offset:10});
      var processorStream = through2.obj(function (event, encoding, callback) {
        switch (event.type) {
          case 'data':
            // event.payload is an object representing a single row of results
            // make sure callback is called only when all processing is complete
            doAsyncProcessing(event.payload, callback);
            break;
          case 'done':
            // event.payload is an object containing a count of rows actually received, plus some other things
            // now we can resolve the auto-logout promise
            resolve(event.payload.rowsReceived);
            callback();
            break;
          case 'error':
            // event.payload is an Error object
            console.log('Error streaming RETS results: '+event.payload);
            retsStream.unpipe(processorStream);
            processorStream.end();
            // we need to reject the auto-logout promise
            reject(event.payload);
            callback();
            break;
          default:
            // ignore other events
            callback();
        }
      });
      retsStream.pipe(processorStream);
    });
  });
```
