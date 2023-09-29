# Mongo Important commands
- MongoDB is case Sensitive.
- To see list of databases.
```
show dbs;
```
- To use any databases or to create database(Note: if there is not collections in db then it will not be in list){eg. use STUDENTS_Database}.
```
use database_name;
```
- To check collections attributes inside database (like tables in SQL).
```
show collections;
```
- To create collections inside database {eg. db.createCollection("Courses");}.
```
db.createCollection("CollectionName");
```
- To print all the documents inside collection(like select in SQL){db.courses.find();}.
```
db.collectionName.find();
```
- To insert data in collection{db.courses.insertOne({name:"Physics",type:"practical",marks:100});}.
```
db.collectionName.insertOne(json);
```
- insert more than one documents in collection{db.courses.insertMany([{name:"english",type:"Theory"},{name:"P.Ed",mandatory:"No"}]);}.
```
db.collectionName.insertMany([json..])
```
- Some find function type.
```
db.collectionName.findOne() //give first documents
db.collectionName.findOne({filter}) // one documents have this filter like where in SQL
db.collectionName.find({filter})  // give all the documents having property filter
db.collectionName.find({_id:ObjectId('id')}); // to get by id
```
- To count the number of Documents insider collection.
```
db.collectionName.count();
```
- Limit in mongodb (mongo have limit method).
```
db.collectionName.count().limit(number);
```
- Projection:To get only some property of document, find function take two paramters. First take filter and second take what you want to in documents to show just like select {dash,dash} rather than * in SQL. Second arguments take 0 for not include and 1 for include.
```
db.collectionName.find({filter},{key:1}).limit(1); // second arguments is projection
```
- Mongo have toArray() method to convert results in form of array, so that you can apply array methods (but it not worked in findOne like count not work).
- Mongo have sort method to sort the result.
```
db.collectionName.find().sort(); // to sort the documents
db.collectionName.find().sort({key:1/0}) // 1->asc,0->dec
```
## Delete the collections
- To delete the records.
```
db.collectionName.deleteOne({filter});
db.collectionName.deleteMany({filter}); // to delete many
```
## Update the collections
- To update one record.
```
db.collectionName.updateOne({filter},{$set:{key:value}});
db.collectionName.updateOne({filter},{$inc:{key:1 or -1}}); // to increment the key by 1 or -1
```
- To update All the record.
```
db.collectionName.updateMany({filter},{$set:{key:value}},{$inc:{key:1/-1}});
```

## Operators in MongoDB
- $lt:less than, $gt:greater than,$ne:not equal to, $gte:greater than equal to, $and etc.
- distinct property of collection.
```
db.collectionName.distinct("key");
```
## Indexes
It is another DataStructures that arranged the records for efficient use.
- To create Index.
```
db.collectionName.createIndex({property:1/-1}); // this will create temp another data collection for optimized operatoins
```
- explain method to check details of property {db.temp.find({type:"sm"}.explain("executionStats"))}.
```
db.collectionName.find({filter}).explain("property");// ex. executionStats
```
- You can also create "Compound Index" to give multiple fields.
