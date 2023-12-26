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
  
