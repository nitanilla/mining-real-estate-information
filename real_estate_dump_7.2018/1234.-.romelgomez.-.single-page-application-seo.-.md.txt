# Single Page Application SEO

Well, is about the approach, we have the classic app where the page are prerendered in the server and shipped to client, with all meta tags already defined, and on the other hand we have the single page application (SPA), where we shipped to clients a static page, index.html that not change, or change in the client later, that in fact, seen to be not good for the crawlers bots, because, they do not wait for all the page finish loading.
   
In response to this problem, we have a lot of the crawlers paid services, that render all the page (that mean, wait for all JavaScript Process and DOM changes), and save as a snapshot, that later is shipped in demand to crawlers bots (Googlebot, Facebot, etc). 

Well how to avoid all these crawlers paid services and similar hacks based on PhantomJS, well as I said is about the approach, what if we merge the both approach, of the classic and the SPA, to have a hybrid approach, like seems to be used for Youtube site, is like an Ajax app or SPA and the same time is classic app where the page is rendered on the server, when you request some video, you get a processed page, all meta tags has the video related data, but when you change to another video, the meta tags are not updated. 

As code example, we see here the current code of https://londres.herokuapp.com/ a full SPA APP made with Angular 1.X Express Firebase:   

As note, I use handlebars for render the view in the server. 


**Angular Routes**

```javascript
'use strict';

angular.module('routes',[])
  .constant('SECURED_ROUTES', {})
  .constant('LOGIN_REDIRECT_PATH', '/login')
  /**
   * Adds a special `whenAuthenticated` method onto $routeProvider. This special method,
   * when called, invokes Auth.$requireAuth() service (see Auth.js).
   *
   * The promise either resolves to the authenticated user object and makes it available to
   * dependency injection (see AccountCtrl), or rejects the promise if user is not logged in,
   * forcing a redirect to the /login page
   */
  .config(['$routeProvider', 'SECURED_ROUTES', function($routeProvider, SECURED_ROUTES) {
    // credits for this idea: https://groups.google.com/forum/#!msg/angular/dPr9BpIZID0/MgWVluo_Tg8J
    // unfortunately, a decorator cannot be use here because they are not applied until after
    // the .config calls resolve, so they can't be used during route configuration, so we have
    // to hack it directly onto the $routeProvider object
    $routeProvider.whenAuthenticated = function(path, route) {
      route.resolve = route.resolve || {};
      route.resolve.user = ['FireAuth', function(FireAuth) {
        return FireAuth.$requireSignIn();
      }];
      $routeProvider.when(path, route);
      SECURED_ROUTES[path] = true;
      return $routeProvider;
    };
  }])
  /**
   * configure views; whenAuthenticated adds a resolve method to ensure users authenticate
   * before trying to access that route
   */
  .config(['$routeProvider', '$locationProvider', function($routeProvider, $locationProvider) {

    $locationProvider.html5Mode(true).hashPrefix('!');

    $routeProvider
      .when('/', {
        templateUrl: 'static/assets/views/main.html',
        controller: 'MainController',
        reloadOnSearch: false
      })
      .when('/privacy-policy', {
        templateUrl: 'static/assets/views/privacyPolicy.html',
        controller: 'EmptyController'
      })
      .when('/terms-of-service', {
        templateUrl: 'static/assets/views/termsOfService.html',
        controller: 'EmptyController'
      })
      .whenAuthenticated('/new-publication', {
        templateUrl: 'static/assets/views/publication.html',
        controller: 'PublicationsController'
      })
      .whenAuthenticated('/edit-publication/:publicationId', {
        templateUrl: 'static/assets/views/publication.html',
        controller: 'PublicationsController'
      })
      .when('/view-publication/:publicationID/:title', {
        templateUrl: 'static/assets/views/viewPublication.html',
        controller: 'ViewPublicationController'
      })
      .when('/login', {
        templateUrl: 'static/assets/views/login.html',
        controller: 'LoginController'
      })
      .whenAuthenticated('/account', {
        templateUrl: 'static/assets/views/account.html',
        controller: 'AccountController',
        reloadOnSearch: false
      })
      .when('/:accountName/:categoriesAndLocations/:publicationID/:title', {
        templateUrl: 'static/assets/views/viewPublication.html',
        controller: 'ViewPublicationController'
      })
      .when('/:accountName', {
        templateUrl: 'static/assets/views/accountPublications.html',
        controller: 'AccountPublicationsController',
        reloadOnSearch: false
      })
      .otherwise({redirectTo: '/'});
  }])
  /**
   * Apply some route security. Any route's resolve method can reject the promise with
   * "AUTH_REQUIRED" to force a redirect. This method enforces that and also watches
   * for changes in auth status which might require us to navigate away from a path
   * that we can no longer view.
   */
  .run([
    '$rootScope',
    '$location',
    'FireAuth',
    'SECURED_ROUTES',
    'LOGIN_REDIRECT_PATH',
    function($rootScope, $location, FireAuth, SECURED_ROUTES, LOGIN_REDIRECT_PATH) {

      // watch for login status changes and redirect if appropriate
      FireAuth.$onAuthStateChanged(function (authenticatedUser) {

        // authenticatedUser : object or null
        if( !authenticatedUser && SECURED_ROUTES.hasOwnProperty($location.path())) {
          $location.path(LOGIN_REDIRECT_PATH);
        }

      });

      // some of our routes may reject resolve promises with the special {authRequired: true} error
      // this redirects to the login page whenever that is encountered
      $rootScope.$on('$routeChangeError', function(event, next, previous, error) {
        if( error.toString() === 'AUTH_REQUIRED' ) {
          $location.path(LOGIN_REDIRECT_PATH);
        }
      });

    }
  ]);

```
 
**The Express Route config:**
  
```javascript  
var path = require('path');
var fs = require('fs');
var Q = require('q');
var handlebars = require('handlebars');
var md5 = require('js-md5');


//var Firebase = require("firebase");
//var FireRef = new Firebase('berlin.firebaseio.com/');
var firebase = require('./fire');


var _ = require('lodash');


var basePath = '';

switch(process.env.NODE_ENV) {
  case 'production':
    basePath = '/dist';
    break;
  case 'development':
    basePath = '/public';
    break;
}

var metaTags = {
  title:          'Market of London - Real Estate and Jobs Classified Ads - UK',
  url:            'http://www.marketoflondon.co.uk',
  description:    'Share your brand, jobs offers and real estate publications in social networks.',
  image:          'http://res.cloudinary.com/berlin/image/upload/c_fill,e_sepia:77,h_630,q_auto:best,w_1200/v1471288313/Market_Of_London_share_image_xan9wg.webp',
  twitterAccount: '@MarketOfLondon'
};

function capitalizeFirstChar(input) {
  return (!!input) ? input.trim().replace(/(^\w?)/g, function(txt){return txt.charAt(0).toUpperCase() + txt.substr(1);}) : '';
}

function lodashTruncates(text, length) {
  var _text = _.truncate(text, {
    length: length,
    separator: /,? +/
  });
  return capitalizeFirstChar(_text);
}

function readFile(fileName){
  var deferred = Q.defer();

  fs.readFile( path.join(process.cwd(), basePath, fileName), function (error, source) {
    if (error) {
      deferred.reject(error);
    }else{
      deferred.resolve({source: source});
    }
  });

  return deferred.promise;
}

function getPublicationByUUDID (uuid){
  var deferred = Q.defer();

  firebase.FireRef.child('publications/'+uuid).once('value')
    .then(function(snapshot){

      var publication = snapshot.val();
      publication.$id = snapshot.key;

      if(snapshot.exists()){
        deferred.resolve(publication);
      }else{
        deferred.reject('Error in getPublication function');
      }

    }, function (error) {
      deferred.reject(error);
    });

  return deferred.promise;
}

function getUserByUUID (uuid){
  var deferred = Q.defer();

  firebase.FireRef.child('users/'+uuid).once('value')
    .then(function(snapshot){

      if(snapshot.exists()){
        var user = snapshot.val();
        user.$id = snapshot.key;
        deferred.resolve(user);
      }else{
        deferred.reject('User does not exist');
      }

    }, function (error) {
      deferred.reject(error);
    });

  return deferred.promise;
}

function getUserByAccountName (accountName){
  var deferred = Q.defer();

  firebase.FireRef.child('accountNames').child(accountName).once('value')
    .then(function(snapshot){
      if(snapshot.exists()){
        // get profile data by the id (snapshot.val() - facebook:10204911533563856)
        return  getUserByUUID(snapshot.val());
      }else{
        // maybe is a userID
        return  getUserByUUID(accountName);
      }
    })
    .then(function(user){
      if(typeof user.startedAt !== 'undefined'){
        deferred.resolve(user);
      }else {
        deferred.reject();
      }
    }, function (error) {
      deferred.reject(error);
    });

  return deferred.promise;
}

function slug(input) {
  return (!!input) ? String(input).toLowerCase().replace(/[^a-zá-źA-ZÁ-Ź0-9]/g, ' ').trim().replace(/\s{2,}/g, ' ').replace(/\s+/g, '-') : '';
}

function capitalize(input) {
  return (!!input) ? input.replace(/([^\W_]+[^\s-]*) */g, function(txt){return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();}) : '';
}

function setMetaImage (images, featuredImageId){
  var $images = [];

  for (var imageID in images) {
    if( images.hasOwnProperty( imageID ) ) {
      images[imageID].$id = imageID;
      if(imageID !== featuredImageId){
        $images.push(images[imageID]);
      }else{
        $images.unshift(images[imageID])
      }
    }
  }

  metaTags.image = $images.length > 0? ('http://res.cloudinary.com/berlin/image/upload/c_fill,h_630,q_auto:best,w_1200/'+ $images[0].$id +'.webp') : metaTags.image;
}

function defaultRoute(req, res){
  readFile('index1.html')
    .then(function(the){
      var template = handlebars.compile(the.source.toString());
      return Q.when({result: template(metaTags)})
    })
    .then(function(the){
      metaTags = {
        title:          'Market of London - Real Estate and Jobs Classified Ads - UK',
        url:            'http://www.marketoflondon.co.uk',
        description:    'Share your brand, jobs offers and real estate publications in social networks.',
        image:          'http://res.cloudinary.com/berlin/image/upload/c_fill,e_sepia:77,h_630,q_auto:best,w_1200/v1471288313/Market_Of_London_share_image_xan9wg.webp',
        twitterAccount: '@MarketOfLondon'
      };
      res.send(the.result);
    },function(error){
      throw error;
    });

  //res.sendFile('index1.html', {root: path.join(process.cwd(), basePath)});
}

module.exports = function(app) {

  app.get('/', function(req, res) {
    // Rewrite Cache-Control set defined in app.js
    //res.set({
    //  'Cache-Control': 'no-cache'
    //});
    defaultRoute(req, res);
  });

  // google-site-verification for http://www.marketoflondon.co.uk/
  app.get('/flippa_7016811.txt', function(req, res) {
    res.sendFile('flippa_7016811.txt', {root: path.join(process.cwd(), basePath)});
  });

  // google-site-verification for http://www.marketoflondon.co.uk/
  app.get('/googleb3b941affe88d9b8.html', function(req, res) {
    res.sendFile('googleb3b941affe88d9b8.html', {root: path.join(process.cwd(), basePath)});
  });

  app.get('/sitemap.txt', function(req, res) {
    res.sendFile('sitemap.txt', {root: path.join(process.cwd(), basePath)});
  });

  app.get('/sitemap.xml', function(req, res) {
    res.sendFile('sitemap.xml', {root: path.join(process.cwd(), basePath)});
  });

  app.get('/robots.txt', function(req, res) {
    res.sendFile('robots.txt', {root: path.join(process.cwd(), basePath)});
  });

  app.get('/robots.xml', function(req, res) {
    res.sendFile('robots.xml', {root: path.join(process.cwd(), basePath)});
  });

  app.get('/manifest.txt', function(req, res) {
    res.sendFile('manifest.txt', {root: path.join(process.cwd(), basePath)});
  });

  app.get('/privacy-policy', function(req, res) {
    defaultRoute(req, res);
  });

  app.get('/terms-of-service', function(req, res) {
    defaultRoute(req, res);
  });

  app.get('/new-publication', function(req, res){
    defaultRoute(req, res);
  });

  app.get('/edit-publication/:publicationId', function(req, res){
    defaultRoute(req, res);
  });

  app.get('/login', function(req, res){
    defaultRoute(req, res);
  });

  app.get('/account', function(req, res){
    defaultRoute(req, res);
  });

  app.get('/:accountName', function(req, res){

    getUserByAccountName(req.params.accountName)
      .then(function (user) {

        // META Title
        // ***********************************
        var metaTitle = 'Look @';
        metaTitle += typeof user.accountName !== 'undefined' && user.accountName !== '' ? user.accountName : user.$id;
        metaTitle += ' Publications in Market of London';
        metaTags.title = metaTitle;

        // META URL
        // ***********************************
        var metaURL = 'http://www.marketoflondon.co.uk/';
        metaURL += typeof user.accountName !== 'undefined' && user.accountName !== '' ? user.accountName : user.$id;
        metaTags.url = metaURL;

        // META Description
        // ***********************************
        metaTags.description = typeof user.bio !== 'undefined' && user.bio !== '' ? lodashTruncates(user.bio, 159) : 'MarketOfLondon.co.uk - Jobs, Real Estate, Transport, Services, Marketplace related Publications';

        // META image
        // ***********************************
        setMetaImage(user.images, user.featuredImageId);

        // META twitter
        // ***********************************
        metaTags.twitterAccount = typeof user.twitterAccount !== 'undefined' && user.twitterAccount !== '' ? '@' + user.twitterAccount : metaTags.twitterAccount;

        return readFile('index1.html');
      })
      .then(function(the){
        var template = handlebars.compile(the.source.toString());
        return Q.when({result: template(metaTags)})
      })
      .then(function(the){
        metaTags = {
          title:          'Market of London - Real Estate and Jobs Classified Ads - UK',
          url:            'http://www.marketoflondon.co.uk',
          description:    'Share your brand, jobs offers and real estate publications in social networks.',
          image:          'http://res.cloudinary.com/berlin/image/upload/c_fill,e_sepia:77,h_630,q_auto:best,w_1200/v1471288313/Market_Of_London_share_image_xan9wg.webp',
          twitterAccount: '@MarketOfLondon'
        };
        res.send(the.result);
      },function(){
        res.redirect('/');
      });

  });

  /**
   * Example url: /walesServicesLTD/transport-specialized-in-scotland-central-scotland/-KIz5P7HuvRD7k6D8rPB/wethepeople-envy-35.html
  */
  app.get('/:accountName/:categoriesAndLocations/:publicationID/:title', function(req, res){

    var publication = {};
    var user = {};

    getPublicationByUUDID(req.params.publicationID)
      .then(function(_publication_){
        publication = _publication_;
        return getUserByUUID(publication.userID);
      })
      .then(function(_user_){
        user = _user_;

        // META TITLE
        // ***********************************
        var metaTitle = capitalize(publication.title).trim();
        metaTitle += publication.department === 'Real Estate'? ' for ' + publication.reHomeFor.toUpperCase() : '';
        metaTitle += ' - Market of London';
        metaTags.title = metaTitle;

        // META URL
        // ***********************************
        var metaURL = 'http://www.marketoflondon.co.uk/';

        /*
         locations: [ 'Scotland', 'North East Scotland', 'Dundee East' ],
         categories: [ 'Transport', 'Specialized', 'Others' ],
         */
        var categoriesAndLocations = '';
        var categories = _.join(publication.categories, ' ');
        var locations  = _.join(publication.locations, ' ');
        categoriesAndLocations += categories;
        categoriesAndLocations += ' in ';
        categoriesAndLocations += locations;

        metaURL += typeof user.accountName !== 'undefined' && user.accountName !== '' ? user.accountName + '/': user.$id + '/';
        metaURL += slug(categoriesAndLocations) + '/';
        metaURL += publication.$id + '/';
        metaURL += slug(publication.title) + '.html';
        metaTags.url = metaURL;

        metaTags.twitterURL = 'http://www.marketoflondon.co.uk/v/l/' + publication.$id + '/t';

        // META Description
        // ***********************************
        metaTags.description = lodashTruncates(publication.description, 159);

        // META Image
        // ***********************************
        setMetaImage(publication.images, publication.featuredImageId);

        // META twitter
        // ***********************************
        metaTags.twitterAccount = typeof user.twitterAccount !== 'undefined' && user.twitterAccount !== '' ? '@' + user.twitterAccount : metaTags.twitterAccount;

        return readFile('index1.html');
      })
      .then(function(the){
        var template = handlebars.compile(the.source.toString());
        return Q.when({result: template(metaTags)});
      })
      .then(function(the){
        metaTags = {
          title:          'Market of London - Real Estate and Jobs Classified Ads - UK',
          url:            'http://www.marketoflondon.co.uk',
          description:    'Share your brand, jobs offers and real estate publications in social networks.',
          image:          'http://res.cloudinary.com/berlin/image/upload/c_fill,e_sepia:77,h_630,q_auto:best,w_1200/v1471288313/Market_Of_London_share_image_xan9wg.webp',
          twitterAccount: '@MarketOfLondon'
        };
        res.send(the.result);
      },function(error){
        //throw error;
        res.redirect('/');
      });

  });

  app.get('*', function(req, res){
    defaultRoute(req, res);
  });

};
```

**The index.html**

```
<!doctype html>
<!-- The manifest.txt file is for specify which files will be cached  -->
<html class="no-js" ng-app="app" manifest="http://www.marketoflondon.co.uk/manifest.txt">
<!-- The HEAD is Analyzed and Processed by the Node Server process Handlebars for SEO  -->
<head>
  <meta charset="utf-8">
  <base href="/">
  <meta name="fragment" content="!" />
  <meta name="viewport" content="width=device-width">

  <title>{{title}}</title>
  <meta name="description" content="{{description}}">

  <meta name="keywords" content="jobs,UK">

  <meta property="og:title" content="{{title}}" />
  <meta property="og:url" content="{{url}}" />
  <meta property="og:description" content="{{description}}" />
  <meta property="og:image" content="{{image}}" />
  <meta property="og:image:width" content="1200" />
  <meta property="og:image:height" content="630" />
  <meta property="og:type" content="website" />
  <meta property="og:site_name" content="MarketOfLondon.co.uk" />

  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:site" content="{{twitterAccount}}" />

  <meta name="twitter:title" content="{{title}}" />
  <meta name="twitter:url" content="{{twitterURL}}" />
  <meta name="twitter:description" content="{{description}}">
  <meta name="twitter:image" content="{{image}}" />
  <meta name="twitter:image:src" content="{{image}}" />

  <meta property="fb:app_id" content="1717304911824824" />
  <meta name="google-site-verification" content="YOiFO50lpwetbHnGX5GNRX2q_4dHqz9VpdxUbLAmnTc" />
  <meta name="msvalidate.01" content="1A19A3125B32232A0474555B4C910442" />

  <link rel="publisher" href="https://plus.google.com/+MarketoflondonUk" />

</head>
<body ng-controller="AppController">
<div id="fb-root"></div>

<!--[if lt IE 7]>
<p class="browsehappy">You are using an <strong>outdated</strong> browser. Please <a href="http://browsehappy.com/">upgrade your browser</a> to improve your experience.</p>
<![endif]-->

<div class="navbar navbar-default navbar-fixed-top" role="navigation" style="margin-bottom: 0;">
  <div class="container" >
    <div class="navbar-header">

      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#js-navbar-collapse">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>

      <a class="navbar-brand font-raleway" ng-href="/" style="padding: 6px;">

        <picture>
          <source type="image/webp" srcset="https://res.cloudinary.com/berlin/image/upload/c_scale,q_auto:low,w_250/v1472222421/logo_3_iglbc5.webp">
          <img src="https://res.cloudinary.com/berlin/image/upload/c_scale,q_auto:low,w_250/v1472222421/logo_3_iglbc5.png" class="img-responsive" alt="Market of London">
        </picture>


      </a>

    </div>

    <div class="collapse navbar-collapse" id="js-navbar-collapse"  ng-cloak="">
      <ul class="nav navbar-nav">
        <li><a ng-href="/new-publication" style="color: #337ab7;">Publish Something for FREE!</a></li>
        <li ng-cloak ng-show="firebaseUser" ><a ng-href="/account">Account</a></li>
        <li ng-cloak ng-show="!firebaseUser" ><a ng-href="/login" style="color: #337ab7;" >Log in</a></li>
        <li ng-cloak ng-show="firebaseUser" ><a ng-click="logout()" style="cursor: pointer; color: red;" >logout</a></li>
      </ul>
    </div>
  </div>
</div>

<!-- Publications -->
<div ng-show="locationPath === '/'">

  <div class="container" style="margin-top: 20px;">
    <div class="panel panel-default">
      <div class="panel-body">

        <!-- Main title description of the site
        - FOR SEO must kept in this way, the google search engine will look for the <h1> tag y will replace the content of the description meta-tag  -->
        <div class="main-title">
          <h1>
            Market of London - Real Estate and Jobs Classified Ads - UK
            <br>
            <small>Share your brand, jobs offers and real estate publications in social networks.</small>
          </h1>
          <h2 class="hidden">Share your brand, jobs offers and real estate publications in social networks.</h2>
        </div>

        <div>
          <div ng-show="!lording.isDone" style="margin-top: 10px; border: 0; border-top: 1px solid #eee;">
            <div cg-busy="{promise: lording.promise, message:'Just a moment'}">
              <div class="loading-background img-responsive">
                <div>

                </div>
              </div>
            </div>
          </div>

          <div ng-show="lording.isDone">
            <hr class="hr-xs">

            <list-publications lording="lording"></list-publications>

          </div>
        </div>

      </div>
    </div>

  </div>


</div>

<!-- Other Views -->
<div>
  <div ng-view="" autoscroll="true"></div>
</div>


<!-- Footer -->
<div class="footer">
  <div class="container">
    <div class="visible-xs-block">
      <div>
        <p>
          Copyright ©2016 MarketOfLondon.co.uk
        </p>
      </div>
      <div>
        <p>
          <a ng-href="/privacy-policy">Privacy Policy</a>
        </p>
      </div>
      <div>
        <p>
          <a ng-href="/terms-of-service">Terms Of Service</a>
        </p>
      </div>
      <div>
        <p>
          Follow us on Twitter <a href="https://twitter.com/marketoflondon" target="_blank">@marketoflondon</a>
        </p>
      </div>
    </div>
    <div class="visible-sm-block visible-md-block visible-lg-block">
      <p>
        Copyright ©2016 MarketOfLondon.co.uk
        - <a ng-href="/privacy-policy">Privacy Policy</a>
        - <a ng-href="/terms-of-service">Terms Of Service</a>
        - Follow us on Twitter <a href="https://twitter.com/marketoflondon" target="_blank">@marketoflondon</a>
      </p>
    </div>
  </div>
</div>


<!-- build:css({.,public}) static/assets/styles/all.min.css -->
<link property="stylesheet" rel="stylesheet" href="/bower_components/bootstrap/dist/css/bootstrap.css" />
<link property="stylesheet" rel="stylesheet" href="/bower_components/bootstrap-social/bootstrap-social.css" />
<link property="stylesheet" rel="stylesheet" href="/bower_components/pnotify/pnotify.core.css" />
<link property="stylesheet" rel="stylesheet" href="/bower_components/angular-busy/dist/angular-busy.css" />
<link property="stylesheet" rel="stylesheet" href="/bower_components/angular-loading-bar/build/loading-bar.css" />
<link property="stylesheet" rel="stylesheet" href="/bower_components/font-awesome/css/font-awesome.css" />
<link property="stylesheet" rel="stylesheet" href="/bower_components/angular-trustpass/dist/tr-trustpass.min.css">
<link property="stylesheet" rel="stylesheet" href="static/plugins/redactor/redactor.css">
<link property="stylesheet" rel="stylesheet" href="static/assets/styles/main.css">
<!-- endbuild -->

<!-- build:js({.,public}) static/assets/scripts/all.min.js -->
<script src="/bower_components/jquery/dist/jquery.js"></script>
<script src="/bower_components/bootstrap/dist/js/bootstrap.js"></script>
<script src="/bower_components/angular/angular.js"></script>
<script src="/bower_components/angular-animate/angular-animate.js"></script>
<script src="/bower_components/angular-messages/angular-messages.js"></script>
<script src="/bower_components/angular-route/angular-route.js"></script>
<script src="/bower_components/lodash/lodash.js"></script>
<script src="/bower_components/algoliasearch/dist/algoliasearch.angular.min.js"></script>
<script src="/bower_components/angular-bootstrap/ui-bootstrap-tpls.js"></script>
<script src="/bower_components/angular-busy/dist/angular-busy.js"></script>
<script src="/bower_components/angular-loading-bar/build/loading-bar.js"></script>
<script src="/bower_components/angular-update-meta/dist/update-meta.js"></script>
<script src="/bower_components/pnotify/pnotify.core.js"></script>
<script src="/bower_components/angular-pnotify/src/angular-pnotify.js"></script>
<script src="/bower_components/angular-redactor/angular-redactor.js"></script>
<script src="/bower_components/angular-uuid-service/angular-uuid-service.js"></script>
<script src="/bower_components/angular-validation-match/dist/angular-validation-match.min.js"></script>
<script src="/bower_components/firebase/firebase.js"></script>
<script src="/bower_components/angularfire/dist/angularfire.js"></script>
<script src="/bower_components/ng-file-upload/ng-file-upload.js"></script>
<script src="/bower_components/ng-file-upload-shim/ng-file-upload-shim.js"></script>
<script src="/bower_components/angular-trustpass/dist/tr-trustpass.min.js"></script>
<script src="/bower_components/ng-password-strength/dist/scripts/ng-password-strength.js"></script>
<script src="static/assets/scripts/app.js"></script>
<script src="static/assets/scripts/config.js"></script>
<script src="static/assets/scripts/main.js"></script>
<script src="static/assets/scripts/filters.js"></script>
<script src="static/assets/scripts/validators.js"></script>
<script src="static/assets/scripts/routes.js"></script>
<script src="static/assets/scripts/publications.js"></script>
<script src="static/assets/scripts/publications.view.js"></script>
<script src="static/assets/scripts/publications.images.js"></script>
<script src="static/assets/scripts/publications.list.js"></script>
<script src="static/assets/scripts/publications.list.categories.js"></script>
<script src="static/assets/scripts/publications.list.locations.js"></script>
<script src="static/assets/scripts/publications.list.categories.routeParameters.js"></script>
<script src="static/assets/scripts/publications.list.locations.routeParameters.js"></script>
<script src="static/assets/scripts/login.js"></script>
<script src="static/assets/scripts/account.js"></script>
<script src="static/assets/scripts/accountPublications.js"></script>
<script src="static/plugins/redactor/redactor.js"></script>
<!-- endbuild -->

</body>
</html>
```

And that's all.

---
Prof. Romel Gomez. 
@romelgomez07
