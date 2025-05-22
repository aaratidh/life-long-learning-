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
  
  
