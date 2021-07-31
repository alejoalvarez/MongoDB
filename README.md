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

## When to use NoSQL
- My application will have a very fast growth
- My application will have servers in the cloud
- I want to mount a database as fast as possible
- My data will not always have the same structure
- The information will be very dynamic
- you will have many users accessing at the same time

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

- find all documents in the **products** collection (pretty organize the output format)

```db.products.find().pretty()```
- Search for a field

```db.products.find( { "nameProduct" : "valueToFind" } )``` 
- Find those that are not equal to a certain value

```db.products.find( { "nameProduct" : { $ne : "Keyboard"} } )```
- Search for two fields

```db.products.find( { "field1" : "value1" , "field2": "value2"})``` 
- When I need to search only some properties of the document. If I want to exclude any field in the result **"field1": 0** 

```db.products.find( { "field1" : "value1" }  , { "_id" : 0, "field1": 1 } )``` 
- Query and order the result asc

```db.products.find( { "field1" : "value1" } ).sort( { field : 1 } ) ```
- Query and order the result desc

```db.products.find( { "field1" : "value1" } ).sort( { field : -1 } ) ```
- Total records

```db.products.count()```
- In mongo you can execute functions, for example (bring the registers and go through them 1 by 1):

```db.products.find().forEach(product -> print( "Product Name " + product.name ))```

### **Insert**

- creates a document in the **products** collection, if the collection does not exist mongo creates it

```db.products.insert( {"nameProduct": "Laptop"})```


```Note: When a record is stored in mongo, what mongo does is convert that object into BSON format (JSON Binary to optimize the query and other operations on the data)```

- Create multiple documents

```json
db.products.insert([ { "nameProdct" : "Keyboard", "price": "22"	} , { "nameProduct": "Laptop", "price": "200"	} ] )
```

### **Update**

- update a document, replace the entire record

```db.products.update( { "field" : "value" }, { "price" : 99.99 } )```
- update various document attributes

```db.products.update( { "field" : "value" }, { "price" : 99.99, "name" : "value" } )```
- **$set** updates an existing field, or if it doesn't exist it creates it

```db.products.update({"name" : "laptop"} , { $set : { "description" : "value" } } )```
- If it is required to update a record and it has not been created, it can be created as follows

```db.product.update( { "name" : "desktop" } , { $set: { "description" : "gaming desktop" } }, { upset: true } )```
- If you need to change the name of any property you can use rename

```db.products.update( { "name" : "desktop" } , { $rename : { "name" : "nombre" } } )```
- If I want to delete a field I can use unset

```db.employee.update ( { "name" : "Alejo"} , { $unset : { edad : 1 } } )```


###  **Remove**
- To delete a record, use remove

```db.products.remove( { "name" : "valor" } ) ```
- If you need to delete everything, the search json is left empty
```db.products.remove( { } )```

### Some operators
- **$gt** ```>``` greater than
- **$gte** ```>=``` greater than equals
- **$lt** ```<``` less than
- **$lte** ```<=``` less than equals

### 1 to Many
- To implement the 1 to many relationship in mongo, arrays are used
- Occurs when an array can store a document


### Arrays
```js
var array = [1, 2, 3]
var user= { "name": "Alejo1"  values : array }
db.users.insert( user )
```

- Search if the element exists and if not add it (**$addToSet**)

```db.users.update ( { } ,   $addToSet: { values: 4}  }) ```
- if required add the value regardless of whether it exists (**$push**)

```db.users.update( { } , { $push: { values: 4 } } )```
- if you want to enter multiple values

```db.users.update( { } , { $push: { values: { $each : [ 5 , 6] } } } )```
- if you want to enter multiple values

```db.users.update( { } , { $addToSet: { values: { $each : [ 5, 6] } } } )```
- insert at a specific position

```db.usuarios.update( { } , { $addToSet: { values: { $each : [ 8, 9] , $position: 4 } } } )```
- if after inserting you need to order  

```db.usuarios.update( { } , { $addToSet: { values: { $each : [ 10, 11] , $sort:1 } } } ) ```
- indicate to apply the changes if it finds multiple records

```db.employee.update({ age: { $gte : 28 }} , { $set : { level2: 2 } } , { multi:true } )```



