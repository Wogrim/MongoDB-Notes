## MongoDB Basics

MongoDB *basically* stores data as JSON, which makes it very easy to use with JavaScript  
You can throw in a bunch of random stuff, but usually you group the same types of things together to keep things manageable  
These individual things will generally be objects, which can have whatever you want in them, including arrays or other objects  
MongoDB is meant to be fast, so it is common to repeat data instead of using relationships to reference other database entries  
You can run MongoDB on your own server, but there's a cloud solution called *MongoDB Atlas* which lets you worry less about database security  
MongoDB automatically makes a *_id* on database entries

organization
- **Database** - a group of collections (like SQL *Schema*)
- **Collection** - a group of documents (like a SQL *Table*)
- **Document** - a single entry in the database (like a SQL *Row* / *Record*)

## MongoDB commands / queries

you can run commands from MongoDB Shell or the terminal in MongoDB Compass
- your server will probably use a library so knowing these commands isn't too important
- these seem to be different in older versions of MongoDB (autocomplete in MongoDB Compass helps)
- you can write these multi-line (with nice indentation) in Notepad and copy-paste them into MongoDB Compass

### database
- **show dbs** - show all the databases
- **db** - show the currently selected database
- **use my_project** - select the *my_project* database
- **db.dropDatabase()** - delete the currently selected database

### collection
- **show collections** - show all the collections in the currently selected database
- **db.createCollection('my_collection')** - create a collection called *my_collection*
- **db.my_collection.drop()** - delete *my_collection*

### document

[official documentation](https://www.mongodb.com/docs/manual/crud/)  
[query operators](https://www.mongodb.com/docs/manual/reference/operator/query/) (for filtering what you read/delete/update)

create
- **db.my_collection.insertOne({name: "John", age: 39})** - create a new document in *my_collection* syntax like a JSON object

read
- **db.my_collection.find().pretty()** - read all documents in *my_collection* with pretty formatting
- **db.my_collection.find({name: "John"})** - read all documents in *my_collection* with name === *John*
- **db.my_collection.find({age: {$gt: 30}})** - read all documents in *my_colection* with age > 30

delete
- **db.my_collection.deleteMany({name: "James"})** - remove all documents in *my_collection* with name === *James*
- **db.my_collection.deleteOne({name: "Jacob"})** - remove the first document in *my_collection* with name === *Jacob*

update is the most complicated because you specify a filter and then how you are updating
- see documentation on [update operators](https://www.mongodb.com/docs/manual/reference/operator/update/#std-label-update-operators)

set wins to zero in all documents in *my_collection*
```
db.my_collection.updateMany(
	{},
	{ $set: { wins: 0 } }
)
```

increment *wins* by 1 for all documents in *my_collection* that have age > 30
```
db.my_collection.updateMany(
	{ age: {$gt: 30} },
	{ $inc: { wins: 1 } }
)
```

## install MongoDB server on your computer

download and install current version of [MongoDB Community](https://www.mongodb.com/try/download/community)
- default install options
- it comes with **MongoDB Compass** (a GUI for managing it, similar to *MySQL Workbench* for MySQL)
- it will run by default on port 27017

## MongoDB Compass

- connect
- you can run MongoDB commands from the terminal in the bottom left corner

## MongoDB Shell

a separate download to run `mongosh` from a terminal, which lets you run commands / queries on your database
