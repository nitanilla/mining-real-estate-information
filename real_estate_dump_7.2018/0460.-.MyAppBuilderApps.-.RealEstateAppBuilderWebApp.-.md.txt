**Real Estate Web Application**

This is used as the default app template when creating new projects to capture new potential buyers and sell more homes.

###  **_App Controller_**  ##########

  www folder

i) index.html, templates(folder)

ii) js/app.js

iii) js/controller.js

## **_Sign in_** #############

Login controller inside the controller.js

API For User Sign In: **http://build.myappbuilder.com/api/login.json**

Code:

var userId = $('#userId').val();

                   var password = $('#password').val();

                   

                   $.ajax({

                          type: "POST",

                          url: "http://build.myappbuilder.com/api/login.json",

                          data:{'login':userId,'password':password},

                          success:function(response){

  },

                          error:function(error,status){

                         

                          }

                          });

## **_View Apps_** #############

 list view controller lists all the app under Real Estate

API For Getting all apps of the user: **http://build.myappbuilder.com/api/users.json**

Code:

$.ajax({

                          type: "GET",

                          url: "http://build.myappbuilder.com/api/users.json",

                          data:{'api_key':appkeyResult.api_key},

                          cache: false,

                          success:function(response){

  },

                          error:function(error,status){

                         

                          }

                          });

List of Apps is then filtered by App Type and App Keys under this root App.

Root App Key is maintained in key.txt file in **www/** folder.

Creator of the Root app can only be able to login as admin.

## **_Creating an App_** #############

API Used: **http://build.myappbuilder.com/api/apps.json**

Code:

$.ajax({

                          type: "POST",

                          url: "http://build.myappbuilder.com/api/apps.json",

                          data:{'api_key':appkeyResult.api_key,'title':$scope.appcreate.gridBookTitle,'description':$scope.appcreate.gridBookDesc},

                          success:function(response){

},

                          error:function(error,status){

                         

                          }

                          });

App Type and Apps under this root App are maintained as custom value for each app on creating an app -

API Used: **http://build.myappbuilder.com/api/book_custom_fields.json**

Code:

var booktype = new FormData();

                          booktype.append('api_key',appKey);

                          booktype.append('title',"AppType");

                          booktype.append('value','Real Estate');

                          $http.post('http://build.myappbuilder.com/api/book_custom_fields.json', booktype, {

                                     transformRequest: angular.identity,

                                     headers: {'Content-Type': undefined}

                                     }).

                          success(function(data, status, headers, config) {

                                  

                                  }).

                          error(function(data, status, headers, config) {

                                

                                });

                          

                          var booktype3 = new FormData();

                          booktype3.append('api_key',defaultkey);

                          booktype3.append('title',"keys");

                          booktype3.append('value',appKey);

                          $http.post('http://build.myappbuilder.com/api/book_custom_fields.json', booktype3, {

                                     transformRequest: angular.identity,

                                     headers: {'Content-Type': undefined}

                                     }).

                          success(function(data, status, headers, config) {

                                  

                                  }).

                          error(function(data, status, headers, config) {

                                

                                });

For edit and delete function use **PUT** and **DELETE** methods.

## **_Creating a New Listing_** #############

API Used: **http://build.myappbuilder.com/api/buttons.json**

Code:

$.ajax({

                                  type: "POST",

                                  url: "http://build.myappbuilder.com/api/buttons.json",

                                  data: formData,

                                  cache: false,

                                  contentType: false,

                                  processData: false,

                                  success:function(response){

                                      

                                  },

                                  error:function(error,status){

                                      

                                  }

                              });

This cordova plugin is used to compress the selected image to desired width and height.

For edit and delete function use **PUT** and **DELETE** methods.

## **_Creating and editing Contents_** #############

API Used to create: **http://build.myappbuilder.com/api/create_default.json**

API Used to edit: **http://build.myappbuilder.com/api/update_default.json**

Code:

if(editData == 'Edit'){

                   urlData ='http://build.myappbuilder.com/api/elements/update_default.json'

                   methodData = "PUT"

                   formData1.append('api_key',appKey);

                   formData1.append('id',elementId);

                   formData1.append('title',$scope.contentCreate.elementTitle);

                   formData1.append('text',$scope.contentCreate.elementText);

                   formData1.append('additional_field',$scope.contentCreate.elementAdditional_field);

                   editData = "";

                 }else{

                   urlData ='http://build.myappbuilder.com/api/elements/create_default.json'

                   methodData = "POST"

                   formData1.append('api_key',appKey);

                   formData1.append('button_id',buttonId);

                   formData1.append('title',$scope.contentCreate.elementTitle);

                   formData1.append('text',$scope.contentCreate.elementText);

                   formData1.append('additional_field',$scope.contentCreate.elementAdditional_field);

                   }

                   

                   $.ajax({

                          type: methodData,

                          url: urlData,

                          data: formData1,

                          cache: false,

                          contentType: false,

                          processData: false,

                          success:function(response){

  },

                          error:function(error,status){

                         

                          }

                          });

**Amenities are stored in tags field:**

API Used: **http://build.myappbuilder.com/api/elements/tags.json**

Code:

$.ajax({

                                 type: methodData,

                                 url: 'http://build.myappbuilder.com/api/elements/tags.json',

                                 data: formData5,

                                 cache: false,

                                 contentType: false,

                                 processData: false,

                                 success:function(response){

                                 

                                 },

                                 error:function(error,status){

                                 

                                 }

                                 });

**Other elements are added as custom values:**

API Used: **http://build.myappbuilder.com/api/custom_values.json**

Code:

$.ajax({

                                 type: methodData,

                                 url: 'http://build.myappbuilder.com/api/custom_values.json',

                                 data: formData2,

                                 cache: false,

                                 contentType: false,

                                 processData: false,

                                 success:function(response){

                                                                  

                                 },

                                 error:function(error,status){

                                

                                 }

                                 });

**Images are added through:**

API Used: **http://build.myappbuilder.com/api/elements/images.json**

Code:

 $http.post('http://build.myappbuilder.com/api/elements/images.json',formData1,{

                              transformRequest:angular.identity,

                              headers:{'Content-Type':undefined}

                              })

                   .success(function(response,status,headers,config){

                            

                            

                            })

                   .error(function(error,status,headers,config){

                          

                          });

**Agents are added as subscribers:**

API Used: **http://build.myappbuilder.com/api/subscribers.json**

Code:

$http.post('http://build.myappbuilder.com/api/subscribers.json',formData11,{

                              transformRequest:angular.identity,

                              headers:{'Content-Type':undefined}

                              })

                   .success(function(response,status,headers,config){

})

                   .error(function(error,status,headers,config){

                         

                    });

**For API references visit - ****http://build.myappbuilder.com/api**