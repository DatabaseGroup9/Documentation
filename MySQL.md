# MySQL Documentation


```SQL
setup.sql


CREATE TABLE Books(
bookID VARCHAR(15) NOT NULL,
title VARCHAR(500),
PRIMARY KEY (bookID)
);
    
CREATE TABLE Authors(
authorID VARCHAR(15) NOT NULL,
fullName VARCHAR(50),
firstName VARCHAR(50),
surName VARCHAR(50),
title VARCHAR(50),
PRIMARY KEY (authorID)
);

CREATE TABLE Cities(
cityID int NOT NULL,
name VARCHAR(30),
lat DOUBLE,
lon DOUBLE,
PRIMARY KEY (cityID)
);

CREATE TABLE Wrote(
ID int NOT NULL AUTO_INCREMENT,
authorID VARCHAR(15),
bookID int,
PRIMARY KEY (ID),
FOREIGN KEY (authorID) REFERENCES Authors(authorID),
FOREIGN KEY (bookID) REFERENCES Books(bookID)
);

CREATE TABLE Mentions(
ID int NOT NULL AUTO_INCREMENT,
bookID VARCHAR(15),
cityID int,
count int
PRIMARY KEY (ID),
FOREIGN KEY (bookID) REFERENCES Books(bookID),
FOREIGN KEY (cityID) REFERENCES Cities(cityID)
);

CREATE VIEW BooksTable AS
SELECT Books.bookID, Books.BookTitle, Cities.cityID, cities.name, cities.lat, cities.lon, Author.authorID, Author.fullName, author.firstName, Author.surName, Author.title FROM `Mentions` JOIN Books ON Mentions.bookID = Books.bookID JOIN Cities ON Mentions.cityID = Cities.cityID JOIN Wrote ON Wrote.bookID = Books.bookID JOIN Authors ON Authors.authorID = Wrote.authorID

```

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-remote-database-to-optimize-site-performance-with-mysql

```SQL

SELECT * FROM `Mentions` JOIN Books ON Mentions.bookID = Books.bookID JOIN Cities ON Mentions.cityID = Cities.cityID JOIN Wrote ON Wrote.bookID = Books.bookID JOIN Authors ON Authors.authorID = Wrote.authorID
```
