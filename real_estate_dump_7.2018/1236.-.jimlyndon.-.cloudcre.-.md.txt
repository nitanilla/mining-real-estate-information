<h2>Cloud CRE</h2>
<p>
  See https://github.com/jimlyndon/cloudcre/wiki/Cloud-CRE
  See www.cloudcre.com
</p>
<p>
A full-featured commercial real estate appraisal reporting and comparable search 
application. Uses asp.net mvc/razor, lucene backed nHibernate search for indexing, 
jquery, knockout.js for data binding, twitter's boostrap, google's mapping api, 
OpenXml for dynamic excel report building, and a several of other open source tools
and libraries.
</p>
<hr>
<ul>
<li>clone the repo</li>
<li>build the solution (make sure nuget pulls the dependencies)</li>
<li>deploy the schema (mysql)</li>
<li>to enable user login see .asax and uncomment the account controller</li>
<li>to enable creation/edit of properties uncomment routes in propertybase controller</li>
<li>also, Cloudcre.Utilities contain test data loading and lucene indexing utility console apps</li>
</ul>