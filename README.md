###### Data Representation and Querying - Exercise 7
# CouchDB
In this exercise we will look at the document-oriented NoSQL database CouchDB, and it's API.

## Introduction

1. NoSQL is the umbrella term for databases that do not conform to the relational, SQL-style model.

1. Two common NoSQL database types are Document-oriented and Graph.

1. CouchDB is a document-oriented database.

1. Documents are represented in CouchDB as JSON objects.

1. Each document has its own id and revision, indicated by fields _id and _rev in the JSON document.

1. Updating a document leaves its _id intact, but updates its _rev.

1. Different documents can have different properties - there is no schema.

1. The main interface with CouchDB, for storage and retreival is a HTTP API.

1. CouchDB uses HTTP methods such as GET, POST, PUT and DELETE to retrieve, add, update and delete documents.

## Exercises
    
1. Go to the [Smileupps CouchDB website](https://www.smileupps.com/store/apps/couchdb) and set up a free CouchDB instance.

1. Explore the Futon interface.

1. Create a CouchDB database for storing emails using curl.

    ```sh
    curl -X PUT http://yourdb.smileupps.com/emails
    ```

1. Create a file called email1.json with the following contents.

    ```json
    {
      "from": "bill.gates@microsoft.com"
      , "to": "michael.dell@dell.com"
      , "subject": "PCs"
      , "content": "Hi Michael, I like your PCs. From Bill"
      , "read": false
    }
    ```

1. Use curl to create a document based on the JSON in your Smileups CouchDB database.

    ```sh
    curl -X POST http://yourdb.smileupps.com/emails -H "Content-Type: application/json" -d @email1.json
    ```
    
1. Examine the response from the previous step. Note that you are shown the id and rev of the document.


1. Use curl to get all of the documents from the database.

    ```sh
    curl -X GET http://yourdb.smileupps.com/emails/_all_docs
    ```

1. Do the same again, but this time including the document contents. Note the URL encoded data.

    ```sh
    curl -X GET http://yourdb.smileupps.com/emails/_all_docs?include_docs=true
    ```

1. Examine the response from the previous step. 

1. Update your document, changing the read property to true. You must replace [_id] and [_rev] with your documents id and rev.

    ```sh
    curl -X PUT http://yourdb.smileupps.com/emails/[_id] -d '{ "read" : true, "_rev" : "[_rev]" }'
    ```

1. Now get your document and make sure the change was saved.

    ```sh
    curl http://yourdb.smileupps.com/emails/[_id]
    ```
    
## Advanced exercises

1. Create a second document in your database. The document should be an email with to, from, subject, content, datetime and read fields. Make up your own values for thoese.

1. Delete the first document from your database.

## Notes

- [CouchDB website](http://couchdb.apache.org/)

- [CoucDB - The Definitive Guide](http://guide.couchdb.org/editions/1/en/index.html)

- [Smileupps](https://www.smileupps.com/store/apps/couchdb) - a free CouchDB hosting service.

- Tutorialspoint [CouchDB Tutorial](http://www.tutorialspoint.com/couchdb/index.htm).

- [tuts+ CouchDB tutorial](http://code.tutsplus.com/articles/getting-started-with-couchdb--net-18801)
