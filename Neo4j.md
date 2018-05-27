# Documentation

### Setting up the Neo4J database

Setting up Neo4J with Docker on DigitalOcean 

Create a Ubuntu-16.04.4 x64 droplet on DigitalOcean with your SSH keys added.

When created ssh into the droplet and run the follwing command to install Docker:

```wget -O - https://bit.ly/docker-install | bash```


```mkdir plugins
   cd plugins
   echo "Downloading Neo4J-Spatial plugin"
   wget https://github.com/neo4j-contrib/spatial/releases/download/0.25.5-neo4j-3.3.5/neo4j-spatial-0.25.5-neo4j-3.3.5-server-plugin.jar
   cd .. 

   docker run \
    -d --name neo4j \
    --rm \
    --publish=7474:7474 \
    --publish=7687:7687 \
    -v $(pwd):/data/databases \
    --volume=$(pwd)/plugins:/plugins \
    --env NEO4J_AUTH=neo4j/class \
    neo4j    
```
*class - is the password for logging in.*
### Importing the data

```http://`[ip-address]:7474/browser/```

Use the password *class* to log in.

Import the nodes and cities using the gui and the csv files:

```
LOAD CSV WITH HEADERS FROM "https://raw.githubusercontent.com/DatabaseGroup9/dataimport/master/data/books_cleaned.csv" AS row
MERGE (b:Book {bookID: row.bookID, bookTitle: row.title})
ON CREATE SET b.bookShortTitle = row.short_title
ON MATCH SET b.bookShortTitle = row.short_title


LOAD CSV WITH HEADERS FROM "https://raw.githubusercontent.com/DatabaseGroup9/dataimport/master/data/authors_cleaned.csv" AS row
MERGE (a:Author {authorID: row.authorID, fullName: row.fullName, firstName: row.firstName, surName: row.surName })
ON CREATE SET a.title = row.title
ON MATCH SET a.title = row.title

USING PERIODIC COMMIT
LOAD CSV WITH HEADERS FROM "https://raw.githubusercontent.com/DatabaseGroup9/dataimport/master/data/cities_cleaned.csv" AS row
MERGE (:City {cityID: row.cityID, name: row.name, location: point({longitude: toFloat(row.lon), latitude: toFloat(row.lat)})});

CREATE INDEX ON :Book(bookID)
CREATE INDEX ON :City(cityID)


USING PERIODIC COMMIT 
LOAD CSV WITH HEADERS FROM "https://raw.githubusercontent.com/DatabaseGroup9/dataimport/master/data/wrote_cleaned.csv" AS row
MATCH (b:Book {bookID: toString(row.bookID)}), 
                      (a:Author {authorID :toString(row.authorID)})
CREATE (a)-[:AUTHORED]->(b);



USING PERIODIC COMMIT
LOAD CSV WITH HEADERS FROM "https://raw.githubusercontent.com/DatabaseGroup9/dataimport/master/data/mentioned_cleaned.csv" AS row
MATCH (b:Book {bookID: replace(toString(row.bookID), " ", "") }),(c:City {cityID: replace(toString(row.cityID), " ", "")})
CREATE (b)-[:MENTIONS {mentions: row.count}]->(c);```

