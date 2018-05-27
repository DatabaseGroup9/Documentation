# Documentation


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

