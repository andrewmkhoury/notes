# MongoDB
 

### Edit records using MongoDB shell

_(Assuming your MongoDB server is already running...)_  

1.  Open a command prompt / terminal and cd to the MongoDB bin directory and start [mongo shell](http://docs.mongodb.org/manual/mongo/#using-the-mongo-shell) with the following command:  
    ./mongo
2.  Now you should have been auto-connected to the "test" database.
3.  Run these commands to add a mongo _collection_ "foo" with a single _document_ "message" with value "hello":  
    \> db.foo.save({'name':'bob','message':'hello'})**Common Mistake:** When saving the update to the database, don't forget the curly braces, for example:  
    \> db.foo.save('name':'bob','message':'hello')  
    Mon Dec 20 12:04:06 SyntaxError: missing ) after argument list (shell):1
4.  Run this command to view all of the documents in the foo _collection_:  
    \> db.foo.find()  
    Output of the command should look something like this:  
    { "_id" : ObjectId("50d8b21fc769d0a05087c7e9"), "name" : "bob", "message" : "hello" }
5.  Now you added a new record, let's try updating our "message" property in the document:  
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
6.  Now this update doesn't actually get committed to the database until we save (we call db.foo.find() to show the data before and after):  
    \> db.foo.find()  
    { "_id" : ObjectId("50d8b21fc769d0a05087c7e9"), "name" : "bob", "message" : "hello" }  
    \> db.foo.save(bob)  
    \> db.foo.find()  
    { "_id" : ObjectId("50d8b21fc769d0a05087c7e9"), "name" : "bob", "message" : "hello world" }  
      
    **Common Mistake:** When saving the update to the database, don't forget to pass the object as a parameter to save:  
    \> db.foo.save()  
    Mon Dec 20 12:04:06 uncaught exception: can't save a null  
    The correct command should have been db.foo.save(bob)
7.  Now we will remove the document (after this we run db.foo.find() then we see that there are now no records in the foo collection):  
    \> db.foo.remove(bob)  
    \> db.foo.find()

Posted by [Andrew](https://www.blogger.com/profile/16901614970730543854 "author profile") at  [12:15 PM](https://mongodbblog.blogspot.com/2012/12/add-find-update-and-remove-records-in.html "permanent link") [![](https://resources.blogblog.com/img/icon18_edit_allbkg.gif)](https://www.blogger.com/post-edit.g?blogID=7477022229347268502&postID=3234666125798618326&from=pencil "Edit Post")

[Email This](https://www.blogger.com/share-post.g?blogID=7477022229347268502&postID=3234666125798618326&target=email "Email This")[BlogThis!](https://www.blogger.com/share-post.g?blogID=7477022229347268502&postID=3234666125798618326&target=blog "BlogThis!")[Share to Twitter](https://www.blogger.com/share-post.g?blogID=7477022229347268502&postID=3234666125798618326&target=twitter "Share to Twitter")[Share to Facebook](https://www.blogger.com/share-post.g?blogID=7477022229347268502&postID=3234666125798618326&target=facebook "Share to Facebook")[Share to Pinterest](https://www.blogger.com/share-post.g?blogID=7477022229347268502&postID=3234666125798618326&target=pinterest "Share to Pinterest")

Labels: [mongo shell](https://mongodbblog.blogspot.com/search/label/mongo%20shell), [mongodb](https://mongodbblog.blogspot.com/search/label/mongodb)
