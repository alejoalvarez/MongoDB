# MongoDB

## Features

- It is an open source initiative
- It is a NoSQL database (Not only SQL, it does not go against SQL, only that it proposes a different way of handling the information)
- Database focused on handling large amounts of data
- Oriented to document storage
- It comes from the term humongous (which means giant)
- Mongo is flexible and scalable (More resources can be added simply by adding more servers, usually known as a cluster)
- It is written in C ++
- Easy change of production scheme
- It is possible to run JS on the mongo server
- Mongo is documents oriented
- Each record in mongo is a document
- Mongo is schemales
- Provides easy horizontal scaling
- The data format of the documents is JSON
- The data types of the documents are the same as those handled in javascript!

## Importants MongoDB programs

- **mongod** (initialize the database server) "server"
- **mongo** (connects to the database) "client"

## Concepts MongoDB
- **Database** 
- **Collections** (it is the division within the database, it resembles the tables in SQL)
- **Documents** (they are the records in JSON format that are stored for the collections)

![item1](https://user-images.githubusercontent.com/13514156/126917325-2a122652-5c40-41b1-8ba5-112496413c27.png)

## Database commands
- ```show dbs``` -> (shows databases)
- ```db``` -> (shows current database)
- ```db.help```-> (shows all the methods that can be used with mongoDB)
- ```use <databse>```-> (create a database and switch to it, only use it temporarily, but actually create it only when at least 1 record is inserted)
- ```db.dropDatabase ()```-> drops the current database, it is important to run ```db``` first to ensure that it is the database to drop.

## Collections commands
- ```show collections``` -> (see db collections)
- ```db.createCollections ("name")```-> creates a collection within the current db
- ```db.<collectionName>.drop()``` (drops the **collectionName** collection within the current db)

## Documents commands

**Find**
- ```db.products.find().pretty()``` -> find all documents in the **products** collection (pretty organize the output format)
- ```db.products.find( { "nameProduct" : "valueToFind" } )``` -> Search for a field
- ```db.products.find( { "nameProduct" : { $ne : "Keyboard"} } )``` -> Find those that are not equal to a certain value
- ```db.products.find( { "field1" : "value1" , "field2": "value2"})``` -> Search for two fields
- ```db.products.find( { "field1" : "value1" }  , { "_id" : 0, "field1": 1 } )``` -> When I need to search only some properties of the document. If I want to exclude any field in the result **"field1": 0** 
- ```db.products.find( { "field1" : "value1" } ).sort( { field : 1 } ) ``` -> Query and order the result asc
- - ```db.products.find( { "field1" : "value1" } ).sort( { field : -1 } ) ``` -> Query and order the result desc

**Insert**

- ```db.products.insert( {"nameProduct": "Laptop"})``` -> creates a document in the **products** collection, if the collection does not exist mongo creates it

```Note: When a record is stored in mongo, what mogo does is convert that object into BSON format (JSON Binary to optimize the query and other operations on the data)```

- Create multiple documents

```json
db.products.insert([ { "nameProdct" : "Keyboard", "price": "22"	} , { "nameProduct": "Laptop", "price": "200"	} ] )
```

