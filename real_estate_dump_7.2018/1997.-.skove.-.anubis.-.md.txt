# Anubis
Real estate harvester, analyzer & evaluator. Anubis grabs real estate advertisement from:
- sreality.cz
- realitymix.centrum.cz
- reality.idnes.cz

and provides statistical overview above real estate internet market. In that way, some another estate can be appraised by comparing to those advertisements.  
⚠️ Tested only on Mac OS
## Installation
### Database
You have to have *docker* installed. Then just pull neo4j database image by:
```bash
docker pull neo4j:3.0
```
### Server
```bash
cd server
npm install
```

### Client
```bash
cd client
npm install
```
## Running
### Fill database
Here is some tricky commands to fill database and another useful functions  
**NOTE**: Neo4j server must be running before you run any command
```bash
cd server

# list available source adapters
./anubis adapters

# scrape raw data
./anubis scrape

# scrape raw data for specific source
./anubis scrape sreality.cz

# transform specific collection into competitors
./anubis transform sreality.cz

# compare for all
./anubis test

# export all competitors into `competitors.csv`
# export is not required for running
./anubis export-competitors
```
### Running servers
```bash
# run neo4j server
cd server/neo4j
./run.sh
# run api server
cd ..
npm start
# run client server
cd ../client
npm start
```

That's all folks!
