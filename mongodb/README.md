# MongoDB
  

### Downloading and Installing MongoDB (for Development)

**Mac OSX Install procedure:**  

1.  Go to the downloads page [http://www.mongodb.org/downloads](http://www.mongodb.org/downloads)
2.  Download the latest "Production Release" version for Mac OSX to a directory where you would like to install MongoDB
3.  Open Terminal on the Mac (Applications => Utilities => Terminal) 
4.  Change directories to where you have downloaded MongoDB, for example:
    ```
    cd /Users/andrew/apps/mongodb/
    ```
5.  Run this command to unzip the MongoDB installation:
    ```
    tar -xzvf mongodb-osx-x86_64-2.2.1.tgz
    ```
6.  Run this command to create the db directory for MongoDB (for development purposes we just make the directory world writeable):
    ```
    sudo /data/db  
    sudo chmod 777 /data/db
    ```
7.  Run this commands to change directories to the bin folder and start MongoDB server:
    ```
    cd mongodb-osx-x86_64-2.2.1/bin  
    sudo ./mongod
    ```
8.  Now your server is set up, now to use MongoDB, in another Terminal tab, cd to the bin directory again and run this command to connect to MongoDB:  
    ```
    ./mongo
    ```

### Edit records using MongoDB shell

_(Assuming your MongoDB server is already running...)_  

1.  Open a command prompt / terminal and cd to the MongoDB bin directory and start [mongo shell](http://docs.mongodb.org/manual/mongo/#using-the-mongo-shell) with the following command:  
    ```
    ./mongo
    ```
2.  Now you should have been auto-connected to the "test" database.
3.  Run these commands to add a mongo _collection_ "foo" with a single _document_ "message" with value "hello":  
    ```
    \> db.foo.save({'name':'bob','message':'hello'})
    ```
    **Common Mistake:** When saving the update to the database, don't forget the curly braces, for example:  
    ```
    \> db.foo.save('name':'bob','message':'hello')  
    Mon Dec 20 12:04:06 SyntaxError: missing ) after argument list (shell):1
    ```
4.  Run this command to view all of the documents in the foo _collection_: 
    ``` 
    \> db.foo.find()
    ```
    Output of the command should look something like this:  
    ```
    { "_id" : ObjectId("50d8b21fc769d0a05087c7e9"), "name" : "bob", "message" : "hello" }
    ```
5.  Now you added a new record, let's try updating our "message" property in the document:
    ```
    \> var bob = db.foo.findOne({'name':'bob'})  
    \> bob  
    {  
        "_id" : ObjectId("50d8b21fc769d0a05087c7e9"),  
        "name" : "bob",  
        "message" : "hello"  
    }  
    \> bob.message = "hello world"  
    hello world  
    \> bob  
    {  
        "_id" : ObjectId("50d8b21fc769d0a05087c7e9"),  
        "name" : "bob",  
        "message" : "hello world"  
    }
    ```
6.  Now this update doesn't actually get committed to the database until we save (we call db.foo.find() to show the data before and after):  
    ```
    \> db.foo.find()  
    { "_id" : ObjectId("50d8b21fc769d0a05087c7e9"), "name" : "bob", "message" : "hello" }  
    \> db.foo.save(bob)  
    \> db.foo.find()  
    { "_id" : ObjectId("50d8b21fc769d0a05087c7e9"), "name" : "bob", "message" : "hello world" }  
    ```
    **Common Mistake:** When saving the update to the database, don't forget to pass the object as a parameter to save:  
    ```
    \> db.foo.save()  
    Mon Dec 20 12:04:06 uncaught exception: can't save a null
    ```
    The correct command should have been `db.foo.save(bob)`
7.  Now we will remove the document (after this we run `db.foo.find()` then we see that there are now no records in the foo collection):  
    ```
    \> db.foo.remove(bob)
    \> db.foo.find()
    ```
