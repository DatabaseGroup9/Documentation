# MongoDB Documentation

## MongoDB One-Click Application in Digital Ocean
_We have added a droplet intended for our MongoDB database and set up by this following this steps:_
1. Create MongoDB Droplet
2. Accessing MongoDB by this command:
``
mongo
``

## Importing the data in MongoDB database
We used a Java Application to import the csv files, see [here](https://github.com/DatabaseGroup9/dataimport).

_Document Structure:_
```
{ "_id" : ObjectId("5b06bc8246391031d0a72538"), 
  "bookID" : "1257",
  "bookTitle" : "The Three Musketeers",
  "author" : {
    "authorID" : "v10500468",
    "fullName" : "Dumas, Alexandre",
    "firstName" : "Alexandre",
    "surName" : "Dumas",
    "title" : "" 
  },
  "cities" : [{ 
    "cityID" : "1002145",
    "name" : "George",
    "lat" : -33.963,
    "lon" : 22.46173 
   },... 
] }
```
### Data Optimization:
Since this application is only intended for reading the data, we have deicded to add index on all the properties to enhance the runtime execution of performing the query by using this command.
```

```
