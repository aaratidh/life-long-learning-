### Relational Database 
- Relation database are not good for fix schema 
- Relational database are not good for dynamic schema
- transaction is situation : when one user is accessing  data  another user is upadting, and another is waiting then the data wiil be locked and the user  who is accessing the data will get  upadted but system wiill be locked untill it is updated. 
- used to store the data in consitantly  eg. financial transaction
- they are not highly available
- Data need to be consistent
 
#### Eventually available  NO
- Available  when one user is accessing  data  another user is upadting , and another is waiting then the user who is accessing the data will get older version of data but system will be available to the every user

###  MOngo DB
- MongoDb is a cross-platform, document oriented datbase that provides, high performance, high availability, and easy scalability
- MongoDb work on concept of collection and document
- flexible to different cloud
- self hostage
- Table are like container (collection of dictionary)
- We can add record interm of documnet 
- Each document is added like a dictionary
- NoSql are databases which are used to stored the data when you are not sure about schema
- The activity we perform will only affect the record not whole database like relation data
-  no strict requiremnt for strict consistancy
#### Database 
- Database is a physical container for collections. Each database get its own set of files on the file system.
- Single MongoDb server typically has multiple database
  
#### Collection 
- Collection is a group of MongoDb documents. It is the equivalent of an RDBMS table. A collection exist within a single database.
- collection do not enforce a schema.
- Documents within a collection can have different fields.
- Typically, all documents in a collection are of similar or related purpose

#### Document 
- A document is a set of key-value pairs.
- IT has Dynamic schema
- Dyanmic schema means that documents in the same collection do not need to have the same set of field or structure
- Common filed in a collection's documents may hold different types of data
  
- Every time you inser data sytem genarte sytem key 
- 12 bytes of data (timestamp, machine id, process id , incrematal values)
- always geting

### You can not do aggaeration in Dynamo DB you need to brith data from DynaoDB to Redshift 

#### 
- Document Oriented Storage
- Index on any attibute
- replication and high availability
- Auto- Sharding
- Rich Query
- Fast in -place updates
- big data
- Data hub
- USer
- NoSQL solution
- User Data Management
- Data Hub
- Mobile application MongoDB are used
- Fast upadted

#### Data Modeling 
##### Denormalized data  Embedded Data MOdel
![image](https://github.com/user-attachments/assets/28c959ec-4a66-4d3a-8615-03d7eec8e3da)

##### Normalized Data 
![image](https://github.com/user-attachments/assets/a9ce52b6-1717-46c1-a446-db43ea605459)

### Note: If you find that one document size does not go beyound 16 MB then use Embedded Data model other wise use Normalized Data model 

#### Data types in MOngo DB 

![image](https://github.com/user-attachments/assets/55c8b20e-15fc-4ff6-b82c-dd67733cd51b)

#### Aggragtion framework 
- MongoDB version of SQL Group by
- $match $group 

###  connecting spark with mongodb  
Spark has in-build connector  only for hive and HDFS for other you have to use the jar file to connect with Database system 

```py
mongosh "mongodb+srv://dbuser:dbpass@clustername.mongodb.net/mydb1" --apiVersion 1 --username dbuser
```

#### Read from mongoDB 

```py
df = spark.read.format("com.mongodb.spark.sql.DefaultSource").option("uri", "mongodb+srv://dbuser:dbpass@clustername.mongodb.net/sampleDB.mycol").load()
```

#### Write in MongoDB 

```py
people.write.format("com.mongodb.spark.sql.DefaultSource").mode("append").option("uri","mongodb+srv://dbuser:dbpass@clustername.mongodb.net/mydb1.contacts").save()
```

#### Aggeration function GROUP in PostgreSQL 
- db.mycol.aggregate([{$group : {_id : "$by", num_tutorial : {$sum : 1}}}])
- db.mycol.aggregate([{$group : {_id : "$by", sumofLikes : {$sum : "$likes"}}}])
- db.mycol.aggregate([{$group : {_id : "$by", avgOfLikes : {$avg : "$likes"}}}])
- db.mycol.aggregate([{$group : {_id : "$by", minLikes : {$min : "$likes"}}}])
- db.mycol.aggregate([{$group : {_id : "$by", maxLikes : {$max : "$likes"}}}])

#### Functions in MongoDB 
- db.mycol.find()
- db.mycol.find().pretty()
- Equality db.mycol.find({"by":"bootcamp"}).pretty()
- Less than  db.mycol.find({"likes":{$lt:50}}).pretty()
- Less Than Equals db.mycol.find({"likes":{$lte:50}}).pretty()
- Greater Than db.mycol.find({"likes":{$gt:50}}).pretty()
- Greater Than Equals db.mycol.find({"likes":{$gte:50}}).pretty()


  
  
