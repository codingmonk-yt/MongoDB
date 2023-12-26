# Getting started with MongoDB

## Section 1.1:Execution of a JavaScript file in MongoDB

```sh
./mongo localhost:27017/mydb myjsfile.js
```

**Explanation**: This operation executes the myjsfile.js script in a mongo shell that connects to the mydb database on the mongod instance accessible via the localhost interface on port 27017. localhost:27017 is not mandatory as this is the default port mongodb uses.

Also, you can run a .js file from within mongo console.

```sh
>load("myjsfile.js")
```

## Section 1.2: Making the output of find readable in shell

We add three records to our collection test as:

```sh
> db.test.insert({"key":"value1","key2":"Val2","key3":"val3"})
WriteResult({ "nInserted" : 1 })
> db.test.insert({"key":"value2","key2":"Val21","key3":"val31"})
WriteResult({ "nInserted" : 1 })
> db.test.insert({"key":"value3","key2":"Val22","key3":"val33"})
WriteResult({ "nInserted" : 1 })
```

If we see them via find, they will look very ugly.

```sh
> db.test.find()
{ "_id" : ObjectId("5790c5cecae25b3d38c3c7ae"), "key" : "value1", "key2" : "Val2
", "key3" : "val3" }
{ "_id" : ObjectId("5790c5d9cae25b3d38c3c7af"), "key" : "value2", "key2" : "Val2
1", "key3" : "val31" }
{ "_id" : ObjectId("5790c5e9cae25b3d38c3c7b0"), "key" : "value3", "key2" : "Val2
2", "key3" : "val33" }
```

To work around this and make them readable, use the pretty() function.

```sh
> db.test.find().pretty()
```

```sh
{
    "_id" : ObjectId("5790c5cecae25b3d38c3c7ae"),
    "key" : "value1",
    "key2" : "Val2",
    "key3" : "val3"
}
{
    "_id" : ObjectId("5790c5d9cae25b3d38c3c7af"),
    "key" : "value2",
    "key2" : "Val21",
    "key3" : "val31"
}
{
    "_id" : ObjectId("5790c5e9cae25b3d38c3c7b0"),
    "key" : "value3",
    "key2" : "Val22",
    "key3" : "val33"
}
>
```

## Section 1.3: Complementary Terms

| SQL Terms | MongoDB Terms |
|-----------|---------------|
| Database | Database |
| Table | Collection |
| Entity / Row | Document |
| Column | Key / Field |
| Table Join | [Embedded Documents](https://docs.mongodb.com/manual/tutorial/model-embedded-one-to-many-relationships-between-documents/) |
| Primary Key | [Primary Key](https://docs.mongodb.com/manual/indexes/#default-id-index)(Default key _id provided by mongodb itself) |

## Section 1.4: Installation

To install MongoDB, follow the steps below:

* **For Mac OS:**

  1. There are two options for Mac OS: manual install or homebrew.
  2. Installing with homebrew:
     * Type the following command into the terminal:
                 ```sh
                     $ brew install mongodb
                 ```
  3. Installing manually:
     * Download the latest release here. Make sure that you are downloading the appropriate file, specially check whether your operating system type is 32-bit or 64-bit. The
       downloaded file is in format tgz.
     * Go to the directory where this file is downloaded. Then type the following command:
                 ```sh
                   $ tar xvf mongodb-osx-xyz.tgz
                 ```
       * Instead of xyz, there would be some version and system type information. The extracted folder would be same name as the tgz file. Inside the folder, their would be a
         subfolder named bin which would contain several binary file along with mongod and mongo.
       * By default server keeps data in folder /data/db. So, we have to create that directory and then run the server having the following commands:
      
         ```sh
         $ sudo bash
         # mkdir -p /data/db # chmod 777 /data
         # chmod 777 /data/db # exit
         ```
       * To start the server, the following command should be given from the current location:
          ```sh
          $ ./mongod
          ```
          It would start the server on port 27017 by default.
         
       * To start the client, a new terminal should be opened having the same directory as before. Then the following command would start the client and connect to the server.
          ```sh
          $ ./mongo
          ```
          
        * By default it connects to the test database. If you see the line like connecting to: test. Then you have successfully installed MongoDB. Congrats! Now, you can test
          Hello World to be more confident.


* **For Windows:** 

  1. Download the latest release here. Make sure that you are downloading the appropriate file, specially check whether your operating system type is 32-bit or 64-bit.
  2. The downloaded binary file has extension exe. Run it. It will prompt an installation wizard.
  3. Click Next.
  4. Accept the licence agreement and click Next.
  5. Select Complete Installation.
  6. Click on Install. It might prompt a window for asking administrator's permission. Click Yes.
  7. After installation click on Finish.
  8. Now, the mongodb is installed on the path C:/Program Files/MongoDB/Server/3.2/bin. Instead of version 3.2, there could be some other version for your case. The path name
     would be changed accordingly.
  9. bin directory contain several binary file along with mongod and mongo. To run it from other folder, you could add the path in system path. To do it:
 
      * Right click on **My Computer** and select **Properties.**
      * Click on **Advanced system setting** on the left pane.
      * Click on **Environment Variables...** under the **Advanced** tab.
      * Select **Path** from **System variables** section and click on **Edit....**
      * Before Windows 10, append a semi-colon and paste the path given above. From Windows 10, there is a **New** button to add new path.
      * Click **OK**s to save changes.
    
 10. Now, create a folder named data having a sub-folder named db where you want to run the server.
 11. Start command prompt from their. Either changing the path in cmd or clicking on **Open command window here** which would be visible after right clicking on the empty space of
     the folder GUI pressing the Shift and Ctrl key together.

12. Write the command to start the server:

    ```sh
    > mongod
    ```
     It would start the server on port 27017 by default.
13. Open another command prompt and type the following to start client:

    ```sh
    > mongo
    ```
14. By default it connects to the test database. If you see the line like: test. Then you have successfully installed MongoDB. Congrats! Now, you can test Hello World to be more
    confident.

* **For Linux:**
  Almost same as Mac OS except some equivalent command is needed.

  1. For Debian-based distros (using apt-get):
     * Import MongoDB Repository key.
    
       ```sh
       $ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
         gpg: Total number processed: 1\
         gpg: imported: 1 (RSA: 1)
       ```
     * Add repository to package list on **Ubuntu 16.04**.
    
       ```sh
       $ echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
       ```
     * on Ubuntu 14.04.

       ```sh
       $ echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
       ```
     * Update package list.

       ```sh
       $ sudo apt-get update
       ```
     * Install MongoDB.

       ```sh
       $ sudo apt-get install mongodb-org
       ```
  2. For Red Hat based distros (using yum):
 
     * use a text editor which you prefer.
    
       ```sh
       $ vi /etc/yum.repos.d/mongodb-org-3.4.repo
       ```

     * Paste following text.

       ```sh
        [mongodb-org-3.4]
        name=MongoDB Repository baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/ gpgcheck=1
        enabled=1
        gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
       ```

     * Update package list.
    
       ```sh
       $ sudo yum update
       ```
     * Install MongoDB

       ```sh
       $ sudo yum install mongodb-org
       ```

## Section 1.5: Basic commands on mongo shell

Show all available databases:

```sh
show dbs;
```

Select a particular database to access, e.g. mydb. This will create mydb if it does not already exist:

```sh
use mydb;
```

Show all collections in the database (be sure to select one first, see above):

```sh
show collections;
```

Show all functions that can be used with the database:

```sh
db.mydb.help();
```

To check your currently selected database, use the command db

```sh
>  db mydb
mydb
```

**db.dropDatabase()** command is used to drop a existing database.

```sh
db.dropDatabase()
```

## Section 1.6: Hello World

After installation process, the following lines should be entered in mongo shell (client terminal).

```sh
> db.world.insert({ "speech" : "Hello World!" });
> cur = db.world.find();x=cur.next();print(x["speech"]);
```

> Hello World!


**Explanation:**
* In the first line, we have inserted a { key : value } paired document in the default database test and in the collection named world.
* In the second line we retrieve the data we have just inserted.
* The retrieved data is kept in a javascript variable named cur.
* Then by the next() function, we retrieved the first and only document and kept it in another js variable named x.
* Then printed the value of the document providing the key.

_________________________

# CRUD Operation

## Section 2.1: Create

```sh
db.people.insert({name: 'Tom', age: 28});
```

Or

```sh
db.people.save({name: 'Tom', age: 28});
```

* The difference with save is that if the passed document contains an _id field, if a document already exists with that _id it will be updated instead of being added as new.
* Two new methods to insert documents into a collection, in MongoDB 3.2.x: Use insertOne to insert only one record:

```sh
db.people.insertOne({name: 'Tom', age: 28});
```

Use insertMany to insert multiple records:

```sh
db.people.insertMany([{name: 'Tom', age: 28},{name: 'John', age: 25}, {name: 'Kathy', age: 23}])
```

## Section 2.2: Update

Update the **entire** object:

```sh
db.people.update({name: 'Tom'}, {age: 29, name: 'Tom'})
```

```sh
// New in MongoDB 3.2
db.people.updateOne({name: 'Tom'},{age: 29, name: 'Tom'}) //Will replace only first matching document.
```

```sh
db.people.updateMany({name: 'Tom'},{age: 29, name: 'Tom'}) //Will replace all matching documents.
```

Or just update a single field of a document. In this case age:

```sh
db.people.update({name: 'Tom'}, {$set: {age: 29}})
```

You can also update multiple documents simultaneously by adding a third parameter. This query will update all documents where the name equals Tom:

```sh
db.people.update({name: 'Tom'}, {$set: {age: 29}}, {multi: true}) // New in MongoDB 3.2

db.people.updateOne({name: 'Tom'},{$set:{age: 30}) //Will update only first matching document.

db.people.updateMany({name: 'Tom'},{$set:{age: 30}}) //Will update all matching documents.
```

If a new field is coming for update, that field will be added to the document.

```sh
db.people.updateMany({name: 'Tom'},{$set:{age: 30, salary:50000}})// Document will have `salary` field as well.
```

If a document is needed to be replaced,

```sh
db.collection.replaceOne({name:'Tom'}, {name:'Lakmal',age:25,address:'Sri Lanka'})
```

can be used.

**Note**: Fields you use to identify the object will be saved in the updated document. Field that are not defined in the update section will be removed from the document.

## Section 2.3: Delete

Deletes all documents matching the query parameter:

```sh
// New in MongoDB 3.2
db.people.deleteMany({name: 'Tom'})

// All versions
db.people.remove({name: 'Tom'})
```
Or just one

```sh
// New in MongoDB 3.2
db.people.deleteOne({name: 'Tom'})

// All versions
db.people.remove({name: 'Tom'}, true)
```

MongoDB's remove() method. If you execute this command without any argument or without empty argument it will remove all documents from the collection.

```sh
db.people.remove();
```

or

```sh
db.people.remove({});
```

## Section 2.4: Read

Query for all the docs in the people collection that have a name field with a value of 'Tom':

```sh
db.people.find({name: 'Tom'})
```

Or just the first one:

```sh
db.people.findOne({name: 'Tom'})
```

You can also specify which fields to return by passing a field selection parameter. The following will exclude the _id
field and only include the age field:

```sh
db.people.find({name: 'Tom'}, {_id: 0, age: 1})
```

**Note**: by default, the _id field will be returned, even if you don't ask for it. If you would like not to get the _id back, you can just follow the previous example and ask for the _id to be excluded by specifying _id: 0 (or _id: false).If you want to find sub record like address object contains country, city, etc.

```sh
db.people.find({'address.country': 'US'})
```

& specify field too if required

```sh
db.people.find({'address.country': 'US'}, {'name': true, 'address.city': true})
# Remember that the result has a `.pretty()` method that pretty-prints resulting JSON:

db.people.find().pretty()
```

## Section 2.5: Update of embedded documents

For the following schema:

```sh
{name: 'Tom', age: 28, marks: [50, 60, 70]}
```

Update Tom's marks to 55 where marks are 50 (Use the positional operator $):

```sh
db.people.update({name: "Tom", marks: 50}, {"$set": {"marks.$": 55}})
```

For the following schema:

```sh
{name: 'Tom', age: 28, marks: [{subject: "English", marks: 90},{subject: "Maths", marks: 100},
{subject: "Computes", marks: 20}]}
```

Update Tom's English marks to 85 :

```sh
db.people.update({name: "Tom", "marks.subject": "English"},{"$set":{"marks.$.marks": 85}})
```

Explaining above example:

By using {name: "Tom", "marks.subject": "English"} you will get the position of the object in the marks array, where subject is English. In "marks.$.marks", $ is used to update in that position of the marks array


### Update Values in an Array 

The positional $ operator identifies an element in an array to update without explicitly specifying the position of the element in the array.

Consider a collection students with the following documents:

```sh
{ "_id" : 1, "grades" : [ 80, 85, 90 ] }
{ "_id" : 2, "grades" : [ 88, 90, 92 ] }
{ "_id" : 3, "grades" : [ 85, 100, 90 ] }
```

To update 80 to 82 in the grades array in the first document, use the positional $ operator if you do not know the position of the element in the array:

```sh
db.students.update(
   { _id: 1, grades: 80 },
   { $set: { "grades.$" : 82 } }
)
```

## Section 2.6: More update operators

You can use other operators besides $set when updating a document. The $push operator allows you to push a value into an array, in this case we will add a new nickname to the nicknames array.

```sh
db.people.update({name: 'Tom'}, {$push: {nicknames: 'Tommy'}})
// This adds the string 'Tommy' into the nicknames array in Tom's document.
```

The $pull operator is the opposite of $push, you can pull specific items from arrays.

```sh
db.people.update({name: 'Tom'}, {$pull: {nicknames: 'Tommy'}})
// This removes the string 'Tommy' from the nicknames array in Tom's document.
```

The $pop operator allows you to remove the first or the last value from an array. Let's say Tom's document has a property called siblings that has the value ['Marie', 'Bob', 'Kevin', 'Alex'].

```sh
db.people.update({name: 'Tom'}, {$pop: {siblings: -1}})
// This will remove the first value from the siblings array, which is 'Marie' in this case.

db.people.update({name: 'Tom'}, {$pop: {siblings: 1}})
// This will remove the last value from the siblings array, which is 'Alex' in this case.
```

## Section 2.7: "multi" Parameter while updating multiple documents

To update multiple documents in a collection, set the multi option to true.

```sh
db.collection.update(
   query,
   update, {
     upsert: boolean,
     multi: boolean,
     writeConcern: document
    }
)
```

multi is optional. If set to true, updates multiple documents that meet the query criteria. If set to false, updates one document. The default value is false.

> db.mycol.find()


>    { "_id" : ObjectId(598354878df45ec5), "title":"MongoDB Overview"}
>    { "_id" : ObjectId(59835487adf45ec6), "title":"NoSQL Overview"}
>    { "_id" : ObjectId(59835487adf45ec7), "title":"Tutorials Point Overview"}


> db.mycol.update({'title':'MongoDB Overview'}, {$set:{'title':'New MongoDB Tutorial'}},{multi:true})


# Getting database information

## Section 3.1: List all collections in database

```sh
show collections
```

or

```sh
show tables
```

or

```sh
db.getCollectionNames()
```

## Section 3.2: List all databases

```sh
show dbs
```
or

```sh
db.adminCommand('listDatabases')
```

or 

```sh
db.getMongo().getDBNames()
```








       

  
