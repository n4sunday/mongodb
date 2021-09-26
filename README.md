# MongoDB

## 🚀 NoSQL

### Structure Store

- Key - Value Store
  - Associative Arrays (key:value) or Dictionary
- Document Store
- Graph Store
- Wid Column Store

#### Key - Value Store

- Associative Arrays (key:value) or Dictionary

`Ex RDMS`

- Redis
- Oracle NoSQL Database
- Voldemorte
- Artospike

#### Document Store

- Document-Oriented
- Semi Structure Date (XML, JSON, BJSON)

`Ex RDMS`

- MongoDB
- CouchDB

#### Graph Store

- Node store Entity And use Edge for relation
- Social Network, AI, ML

`Ex RDMS`

- neo4j

#### Wide Column Storage

- Key Store 2D

`Ex RDMS`

- Cassandra
- HBase
- DynamoDB
- Microsoft Azure Cosmos DB

## 🚀 Intro Mongo

- Document Store
- Store JSON save to **BSON** (Binary JSON)

### Structure Store

- Database
- Collection
- Document

## 🚀 Basic Command

### ⚡️ Database

**show all database**

```sh
show dbs
```

**use database**

```sh
use <database_name>
```

**drop database**

```sh
db.dropDatabase()
```

### ⚡️ Collection

**show collection**

```sh
show collection
```

**create collection**

```sh
db.createCollection("collection_name")
```

**rename collection**

```sh
db.<collection_name>.renameCollection("new_collection_name)
```

**delete collection**

```sh
db.<collection_name>.drop()
```

### ⚡️ Insert Document

**add document**

```sh
db.<collection_name>.insertOne(<document>)
```

**add multi document**

```sh
db.<collection_name>.insertMany([<document>])
```

`Ex`

```sh
use mydb

db.createCollection("user")

db.user.insertOne({name:"sunday"})

db.user.insertMany([{name:"john"},{name:"dany"}])
```

`In database mydb collection user`

```JSON
[
 {
    "_id": {"$oid": "614fc9db58f3ba2123999cce"},
    "name": "sunday"
  },
  {
    "_id": {"$oid": "614fca4458f3ba2123999cd3"},
    "name": "john"
  },
  {
    "_id": {"$oid": "614fca4458f3ba2123999cd4"},
    "name": "dany"
  }
]
```

**insert value array** `Ex`

```sh
db.user.insertOne({name:"robert",position: ["king","warrior"]})
```

`In database mydb collection user`

```JSON
[
  {
    "_id": {"$oid": "614fcd4258f3ba2123999ce0"},
    "name": "robert",
    "position": ["king", "warrior"]
  }
]
```

**insert value object** `Ex`

```sh
db.user.insertOne({name:"robb", general: {weight: 60, height: 190, gender: "male"}})
```

### ⚡️ Find Document

**Find One**

```sh
db.<collection_name>.findOne()

```

**Find**

```sh
db.<collection_name>.find()
```

**Find Condition**

```sh
// Initial Database
use mydb

db.createCollection("one_piece")

db.one_piece.insertOne({name:"Monkey D Luffy", position: "caption", wanted: 1500000000 })
db.one_piece.insertOne({name:"Roronoa Zoro", position: "swordsman", wanted: 320000000 })
db.one_piece.insertOne({name:"Nami", position: "navigate", wanted: 35000000 })
db.one_piece.insertOne({name:"God Usopp", position: "sniper", wanted: 200000000 })
db.one_piece.insertOne({name:"Vinsmoke Sanji", position: "cook", wanted: 330000000 })
db.one_piece.insertOne({name:"Chopper", position: "doctor", wanted: 100 })
db.one_piece.insertOne({name:"Nico Robin", position: "archaeologist", wanted: 130000000 })
db.one_piece.insertOne({name:"The SK Brook", position: "musician", wanted: 83000000 })
```

```sh

```
