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
### Query Optimization:
We have added an index on the queried field such as the city's name, book title and author's full name, or compound index on the set of fields such as in geolocation to enhance the performance of the read operations. This technique prevents the query from scanning the whole collection to find and return the results.

Query   | Description     |  Added index command                      |
--------|-----------------|-------------------------------------------|
1       | getBooksByCity  | ```db.books.createIndex({"cities.name":1})``` |
2       | getCitiesByBookTitle  | ```db.books.createIndex({"bookTitle":1})``` |
3       | getBooksByAuthor      | ```db.books.createIndex({"author.fullName":1})``` |
4       | getBooksByGeolocation | ```db.books.createIndex({"cities.lat":1,"cities.lon":1})``` |

#### Difference in performance sample:
_By profiling the query before and after indexing: (Input data: "Most", not so realistic city but has the highest query result of 33214 books)_
> Before:<br>
![before index](https://user-images.githubusercontent.com/16150075/40591090-fc64b600-620a-11e8-95ef-96721d26d514.png)

> After:<br>
![image](https://user-images.githubusercontent.com/16150075/40591113-40a3f9c0-620b-11e8-9051-1f2f94dcbd77.png)

_The executime falls from 222ms to 40ms after performing index scanning, which is weigh more faster._


