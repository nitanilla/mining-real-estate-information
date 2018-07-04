# Shorelands-api [![Build Status](http://shorelandsrealestate.com:8081/buildStatus/icon?job=Shorelands Api)](http://shorelandsrealestate.com:8081/job/Shorelands%20Api/)


Api services for Shorelands Real Estate website

### Development

lein run

bin\transactor config\samples\dev-transactor-template.properties
bin\console -p 8080 dev datomic:dev://localhost:4334/

### License

Copyright © 2016 Shorelands Real Estate
