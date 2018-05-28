


### The Application REST API can be found here

[REST API Documentation](http://207.154.232.47:8080/api-doc/)

### How we set up the documentation

Create documentation with swagger.io:

```https://editor.swagger.io```

Build as website with this repo:

```https://github.com/bootprint/bootprint-openapi#overview```


Build documentation locally:

```bootprint openapi ./swagger.json target```


Push to server

```scp ./*  root@207.154.232.47:/opt/tomcat/webapps/api-doc/```
