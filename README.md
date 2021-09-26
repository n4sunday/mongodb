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

db.one_piece.insertOne({name:"Monkey D Luffy", position: "captain", wanted: 1500000000, general: {gender: "male"}, color: ["red", "blue", "yellow"] })
db.one_piece.insertOne({name:"Roronoa Zoro", position: "swordsman", wanted: 320000000, general: {gender: "male"}, color: ["white", "green"]  })
db.one_piece.insertOne({name:"Nami", position: "navigate", wanted: 35000000, general: {gender: "female"}, color: ["orange", "green"] })
db.one_piece.insertOne({name:"God Usopp", position: "sniper", wanted: 200000000, general: {gender: "male"}, color: ["brown", "green"] })
db.one_piece.insertOne({name:"Vinsmoke Sanji", position: "cook", wanted: 330000000, general: {gender: "male"}, color: ["yellow", "black"]})
db.one_piece.insertOne({name:"Chopper", position: "doctor", wanted: 100, general: {gender: "male"}, color: ["brown", "pink", "white"]})
db.one_piece.insertOne({name:"Nico Robin", position: "archaeologist", wanted: 130000000, general: {gender: "female"}, color: ["purple", "black"] })
db.one_piece.insertOne({name:"The SK Brook", position: "musician", wanted: 83000000, general: {gender: "male"}, color: ["purple", "black", "white"] })
```

```sh
db.one_piece.find({wanted: 1500000000})

// Response
[
  {
    "_id": {"$oid": "614fd42358f3ba2123999d04"},
    "name": "Monkey D Luffy",
    "position": "caption",
    "wanted": 1500000000
  }
]
```

**Find Condition In Object**

```sh
db.one_piece.find({"general.gender": "female"})

```

**Find Condition In Array**

```sh
db.one_piece.find({color:"black"})
db.one_piece.find({color:["purple", "black"]})
```

#### 🔥 Operator Condition

|  Name  |              Description              |                  Ex                  |
| :----: | :-----------------------------------: | :----------------------------------: |
| `$eq`  |            เท่ากับ (Equal)            | {field:{$eq:value}} or {field:value} |
| `$gt`  |           มากกว่า (Greater)           |         {field:{$gt:value}}          |
| `$gte` | มากกว่าหรือเท่ากับ (Greater or Equal) |         {field:{$gte:value}}         |
| `$lt`  |            น้อยกว่า (Less)            |         {field:{$lt:value}}          |
| `$lte` |  น้อยกว่าหรือเท่ากับ (Less or Equal)  |         {field:{$lte:value}}         |
| `$ne`  |        ไม่เท่ากับ (์Not Equal)        |         {field:{$ne:value}}          |
| `$in`  |             มีค่าใน Array             |    {field:{$in:[value1,value2]}}     |
| `$nin` |          ไม่มีมีค่าใน Array           |    {field:{$nin:[value1,value2]}}    |

##### Operation `$gte` `Ex`

```sh
db.one_piece.find({wanted: {$gte: 100000000 }})
```

```json
[
  {
    "_id": { "$oid": "6150bd4e10b244329cdf57de" },
    "color": ["red", "blue", "yellow"],
    "general": {
      "gender": "male"
    },
    "name": "Monkey D Luffy",
    "position": "captain",
    "wanted": 1500000000
  },
  {
    "_id": { "$oid": "6150bd4e10b244329cdf57df" },
    "color": ["white", "green"],
    "general": {
      "gender": "male"
    },
    "name": "Roronoa Zoro",
    "position": "swordsman",
    "wanted": 320000000
  },
  {
    "_id": { "$oid": "6150bd4f10b244329cdf57e2" },
    "color": ["yellow", "black"],
    "general": {
      "gender": "male"
    },
    "name": "Vinsmoke Sanji",
    "position": "cook",
    "wanted": 330000000
  }
]
```

##### Operation `$in` `Ex`

```sh
db.one_piece.find({color: {$in: ["black"]}})
```

```json
[
  {
    "_id": { "$oid": "6150bd4f10b244329cdf57e2" },
    "color": ["yellow", "black"],
    "general": {
      "gender": "male"
    },
    "name": "Vinsmoke Sanji",
    "position": "cook",
    "wanted": 330000000
  },
  {
    "_id": { "$oid": "6150bd5010b244329cdf57e4" },
    "color": ["purple", "black"],
    "general": {
      "gender": "female"
    },
    "name": "Nico Robin",
    "position": "archaeologist",
    "wanted": 130000000
  },
  {
    "_id": { "$oid": "6150bd5110b244329cdf57e5" },
    "color": ["purple", "black", "white"],
    "general": {
      "gender": "male"
    },
    "name": "The SK Brook",
    "position": "musician",
    "wanted": 83000000
  }
]
```

#### 🔥 Logical Conditions Operator

|  Name  |          Description          |
| :----: | :---------------------------: |
| `$and` |      ตรงทั้งสองเงื่อนไข       |
| `$or`  | ตรงกับเงื่อนไขใดเงื่อนไขหนึ่ง |
| `$nor` |    ไม่ตรงกับเงื่อนไขใดเลย     |
| `$not` |  ตรงข้ามกับเงื่อนไขที่กำหนด   |

##### Logical Conditions `$and` `Ex`

```sh
db.one_piece.find({
  $and: [
    {color: {$in: ["black"]}},
    {wanted: {$gte: 300000000}}
  ]
})
```

```json
[
  {
    "_id": { "$oid": "6150bd4f10b244329cdf57e2" },
    "color": ["yellow", "black"],
    "general": {
      "gender": "male"
    },
    "name": "Vinsmoke Sanji",
    "position": "cook",
    "wanted": 330000000
  }
]
```

### ⚡️ Update Document

**Update One**
`db.<collection_name>.updateOne({<one>,<two>,<three>})`
**one:** Document for edit
**two:** Data for edit
**three:** Options

```sh
db.one_piece.updateOne(
    {name: "Roronoa Zoro"},
    {$set:{wanted: 200}}
)
```

**Update Many**
`db.<collection_name>.updateMany({<one>,<two>,<three>})`
**one:** Document for edit
**two:** Data for edit
**three:** Options

```sh
db.one_piece.updateMany(
    {"general.gender": "female"},
    {$set:{wanted: 0}}
)
```

### ⚡️ Delete Document

**Delete One**
`db.<collection_name>.deleteOne({<filter>})`

```sh
db.one_piece.insertOne({name:"Buggy", position: "captain", wanted: 550000000, general: {gender: "male"}, color: ["red", "blue", "yellow"] })

db.one_piece.deleteOne({name: "Buggy"})
```

**Delete Many**
`db.<collection_name>.deleteMany({<filter>})`

```sh
db.one_piece.insertOne({name:"Buggy", position: "captain", wanted: 550000000, general: {gender: "male"}, color: ["red", "blue", "yellow"] })
db.one_piece.insertOne({name:"Donquixote Doflamingo", position: "captain", wanted: 340000000, general: {gender: "male"}, color: ["pink", "yellow"] })
db.one_piece.insertOne({name:"Monkey D Luffy", position: "captain", wanted: 1500000000, general: {gender: "male"}, color: ["red", "blue", "yellow"] })

db.one_piece.deleteMany({position: "captain"})
```

## 🚀 Advance MongoDB

### ⚡️ Aggregation And Pipeline

`Collection` ▶ `Stages` ▶ `Output`

- Pipeline use `aggregate()` for document array in collection

`Input` ▶ `$match` ▶ `$group` ▶`$sort` ▶`Output`

**How to use**

`db.<collection_name>.aggregate([stage])`

🔥 **SQL vs Stage**

|    SQL     |   Stage    |
| :--------: | :--------: |
|  `WHERE`   |  `$match`  |
| `GROUP BY` |  `$group`  |
|  `SELECT`  | `$project` |
| `ORDER BY` |  `$sort`   |
|  `LIMIT`   |  `$limit`  |
|   `JOIN`   | `$lookup`  |

|   Stage    |                 Description                  |
| :--------: | :------------------------------------------: |
|  `$match`  | กรองเอาเฉพาะ Document ตรงตามเงื่อนไขที่กำหนด |
|  `$group`  |  จัดกลุ่ม Document และคำนวนค่าเก็บใน Output  |
| `$project` |  แสดงข้อมูลในโปรเจคเอาเฉพาะ Field ที่กำหนด   |
|  `$sort`   |              จัดเรียง Document               |
|  `$skip`   |        ข้าม Document ตามจำนวนที่ระบุ         |
|  `$limit`  |          จำกัดการแสดงจำนวน Document          |
| `$unwind`  |    แยกสมาชิก Field Array ออกเป็น Document    |
|  `$count`  |              นับจำนวน Document               |
| `$lookup`  |  ดูข้อมูล Document ที่มี Collection ต่างกัน  |

### ⚡️ Projection (SELECT)

- `0`: hidden field
- `1`: show field

`{$project:{<field_name>: <number>, <field_name>: <number>}}`

**find only name**

```sh
db.one_piece.aggregate({
    $project: {name: 1}
})
```

### ⚡️ Match (WHERE)

`{$match:{ <field_name>: <number> }}`
**match and project**

```sh
db.one_piece.aggregate([
    {$match: {position: "captain"}},
    {$project: {name: 1, wanted: 1}}
])
```

```sh
db.one_piece.aggregate([
    {$match:
        { wanted: {$gte: 300000000 }}
    },
    {$project: {name: 1, wanted: 1}}
])
```

### ⚡️ Count

`{$count:{ <field_name>: <string> }}`

```sh
db.one_piece.aggregate([
    {$match:
        { wanted: {$gte: 300000000 }}
    },
    {$count: "wanted 300M"},
])
```

### ⚡️ Sort (ORDER BY)

- `1`: Ascending
- `-1`: Descending

`{$sort:{ <field_name>: <number>, <field_name>: <number> }}`

```sh
db.one_piece.aggregate([
    {$sort:
        { wanted: -1 }
    },
])
```

```sh
db.one_piece.aggregate([
    {$sort: { wanted: -1 } },
    {$project: {name: 1, wanted: 1}},
])
```

```sh
db.one_piece.aggregate([
    {$match:
        { wanted: {$gte: 300000000 }}
    },
    {$sort: { wanted: -1 } },
    {$project: {name: 1, wanted: 1}},
])
```
