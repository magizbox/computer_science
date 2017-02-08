# [Mongo](https://www.mongodb.com/)


![](https://webassets.mongodb.com/_com_assets/cms/MongoDB-Logo-5c3a7405a85675366beb3a5ec4c032348c390b3f142f5e6dddf1d78e2df5cb5c.png)

MongoDB is an open-source document database that provides high performance, high availability, and automatic scaling.

MongoDB provides high performance data persistence. In particular,

* Support for embedded data models reduces I/O activity on database system.
* Indexes support faster queries and can include keys from embedded documents and arrays.

MongoDB is #1 in the Document Store according to [db-engines](http://db-engines.com/en/ranking/document+store)

# Client

## Mongo Shell

The [mongo shell](https://docs.mongodb.com/getting-started/shell/client/) is an interactive JavaScript interface to MongoDB and is a component of the MongoDB package. You can use the mongo shell to query and update data as well as perform administrative operations.

**Start Mongo**

Once you have installed and have started MongoDB, connect the mongo shell to your running MongoDB instance. Ensure that MongoDB is running before attempting to launch the mongo shell.

```sh
mongo
```

**Interact with mongo via shell**

```sh
# Show list database
> show dbs

# Create or use a database
> use <database_name>
> use test # example

# List collection
> show collections

# Create or use a collection
> db.<collection_name>
> db.new_collection # example

# Read document
> db.new_collection.find()

# Insert new document
> db.new_collection.insertOne({"a": "b"})

# Update document
> db.new_collection.update({"a": "b"}, {$set: {"a": "bcd"}})

# Remove document
> db.new_collection.remove({"a": "b"})
```

## PyMongo - Python Client

[PyMongo](https://api.mongodb.com/python/current/) is a Python distribution containing tools for working with MongoDB, and is the recommended way to work with MongoDB from Python. This documentation attempts to explain everything you need to know to use PyMongo.

### Installation

We recommend using pip to install pymongo on all platforms:

```
pip install pymongo
```

### Usage

```python
import pymongo
# create connection
client = pymongo.MongoClient('127.0.0.1', 27017)
-> MongoClient(host=['127.0.0.1:27017'], document_class=dict, tz_aware=False, connect=True)

# create database
db = client.db_test
-> Database(MongoClient(host=['127.0.0.1:27017'], document_class=dict, tz_aware=False, connect=True), u'db_test')

# create collection (collection is the same with table in SQL)
collection = db.new_collection

# insert document to collection (document is the same with rows in SQL)
db.collection.insert_one({"c": "d"})
->  <pymongo.results.InsertOneResult at 0x7f7eab3c9f00>

# read document of collection
db.new_collection.find_one({"c": "d"})
-> {u'_id': ObjectId('589a8195f23e627a973c4d3c'), u'c': u'd'}

# update documents of collection
db.new_collection.update(
    { "c" : "d" },
    { "$set": { "c": "def"}}
)
-> {u'n': 1, u'nModified': 1, u'ok': 1.0, 'updatedExisting': True}

# remove document of collection
db.new_collection.remove({"c": "def"})
-> {u'n': 1, u'ok': 1.0}
```

## Docker

### Docker Run

Run images and share port

```
docker run -p 27017:27017 mongo:latest
```
