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

### ⚡️ Limit

`{$limit: <number_of_document>}`

```sh
db.one_piece.aggregate([
    {$limit: 2},
])
```

```sh
db.one_piece.aggregate([
    {$match:
        { wanted: {$gte: 300000000 }}
    },
    {$sort: { wanted: -1 } },
    {$project: {name: 1, wanted: 1}},
    {$limit: 3},
])
```

### ⚡️ Skip

`{$skip: <number_of_document>}`

```sh
db.one_piece.aggregate([
    {$project: {name: 1}},
    {$skip: 2}
])
```

### ⚡️ Group (GROUP BY)

`{$group: {<field_for_group>:<statistic_operation>}}`

|    Name     |                  Description                  |
| :---------: | :-------------------------------------------: |
|   `$sum`    |        หาผลรวมของ Document ภายในกลุ่ม         |
|   `$avg`    |        หาค่าเฉลี่ย Document ภายในกลุ่ม        |
|   `$min`    |        หาค่าต่ำสุด Document ภายในกลุ่ม        |
|   `$max`    |        หาค่าสูงสุด Document ภายในกลุ่ม        |
|  `$first`   |        หาค่า Document ลำดับแรกในกลุ่ม         |
|   `$last`   |        หาค่า Document ลำดับท้ายในกลุ่ม        |
|   `$push`   |       แทรกค่า Array ไปยังผลลัพธ์ในกลุ่ม       |
| `$addToSet` | แทรกค่า Array ไปยังผลลัพธ์ในกลุ่มโดยไม่ซ้ำกัน |

**group and count**

```sh
db.one_piece.aggregate([
    {$group:{ _id: "$group", member: {$count:{} } } }
])
```

```JSON
// Response
[
  {
    "_id": "straw hat",
    "member": 8
  },
  {
    "_id": "buggy",
    "member": 1
  },
  {
    "_id": "kuja",
    "member": 1
  },
  {
    "_id": "doflamingo",
    "member": 1
  }
]
```

**sum**

```sh
db.one_piece.aggregate([
    {$group:{ _id: null, total:{$sum: "$wanted"} } }
])
```

**avg and sum**

```sh
db.one_piece.aggregate([
    {$group:{ _id: "$group", avg:{$sum: "$wanted"} } }
])
```

**match, group, avg and sum**

```sh
db.one_piece.aggregate([
    {$match: { "general.gender": "female"}},
    {$group:{ _id: "$group", avg:{$sum: "$wanted"} } }
])
```

**max**

```sh
db.one_piece.aggregate([
    {$group: { _id: "$group" ,wanted_max: {$max: "$wanted"} } }
])
```

**mix**

```sh
db.one_piece.aggregate([
    {$group: { _id: "$group" ,wanted_min: {$min: "$wanted"} } }
])
```

**first**

```sh
db.one_piece.aggregate([
    {$group: { _id: "$group" ,first_name: {$first: "$name"} } }
])
```

**last**

```sh
db.one_piece.aggregate([
    {$group: { _id: "$group" ,last_name: {$last: "$name"} } }
])
```

**push**

```sh
db.one_piece.aggregate([
    {
        $group: {
            _id: "$group",
            sum_wanted: {$sum: "$wanted"},
            detail: {$push: {name: "$name", wanted: "$wanted"} }
        }
     }
])
```

```JSON
// Response
[
  {
    "_id": "doflamingo",
    "detail": [
      {
        "name": "Donquixote Doflamingo",
        "wanted": 340000000
      }
    ],
    "sum_wanted": 340000000
  },
  {
    "_id": "straw hat",
    "detail": [
      {
        "name": "Roronoa Zoro",
        "wanted": 320000000
      },
      {
        "name": "Nami",
        "wanted": 80000000
      },
      {
        "name": "God Usopp",
        "wanted": 200000000
      },
      {
        "name": "Vinsmoke Sanji",
        "wanted": 330000000
      },
      {
        "name": "Chopper",
        "wanted": 100
      },
      {
        "name": "Nico Robin",
        "wanted": 130000000
      },
      {
        "name": "The SK Brook",
        "wanted": 83000000
      },
      {
        "name": "Monkey D Luffy",
        "wanted": 1500000000
      }
    ],
    "sum_wanted": 2643000100
  },
  {
    "_id": "kuja",
    "detail": [
      {
        "name": "Boa Hancock",
        "wanted": 50000000
      }
    ],
    "sum_wanted": 50000000
  },
  {
    "_id": "buggy",
    "detail": [
      {
        "name": "Buggy",
        "wanted": 550000000
      }
    ],
    "sum_wanted": 550000000
  }
]
```

**addToSet**

```sh
db.one_piece.aggregate([
    {
        $group: {
            _id: "$group",
            sum_wanted: {$sum: "$wanted"},
            data_member: {$addToSet: "$name"}
        }
     }
])
```

```JSON
[
  {
    "_id": "doflamingo",
    "data_member": ["Donquixote Doflamingo"],
    "sum_wanted": 340000000
  },
  {
    "_id": "straw hat",
    "data_member": ["Nico Robin", "The SK Brook", "God Usopp", "Roronoa Zoro", "Chopper", "Vinsmoke Sanji", "Monkey D Luffy", "Nami"],
    "sum_wanted": 2643000100
  },
  {
    "_id": "kuja",
    "data_member": ["Boa Hancock"],
    "sum_wanted": 50000000
  },
  {
    "_id": "buggy",
    "data_member": ["Buggy"],
    "sum_wanted": 550000000
  }
]
```

### ⚡️ Lookup (JOIN)

```sh
{
  $lookup: {
    from: "collection_name_foreign",
    localField: "field_main_collection",
    foreignField: "field_relation_collection",
    as: "name_of_result"
  }
}

```

initial data

```sh
db.createCollection("switch")
db.createCollection("brand")

db.brand.insertMany([
    {_id: "6158e3275bd37e5dfc4e5283", name:"Cherry MX"},
    {_id: "6158e4215bd37e5dfc4e5290", name:"Drop"},
    {_id: "6158e4215bd37e5dfc4e5291",name:"Gateron"},
    {_id: "6158e4215bd37e5dfc4e5292",name:"Durock"},
    {_id: "6158e4215bd37e5dfc4e5294",name:"NovelKey"},
    {_id: "6158e4215bd37e5dfc4e5295",name:"Zeal"},
    {_id: "6158e4215bd37e5dfc4e5296",name:"Akko"},
    {_id: "6158e4215bd37e5dfc4e5297",name:"Outemu"},
    {_id: "6158e4215bd37e5dfc4e5298",name:"Gazzew"},
    {_id: "6158e4215bd37e5dfc4e5299",name:"Kailh"},
])

db.switch.insertMany([
    {name: "MX Speed Silver", type: "linear", force: 46, brand_id: "6158e3275bd37e5dfc4e5283"},
    {name: "Black Inks", type: "linear", force: 60, brand_id: "6158e4215bd37e5dfc4e5291"},
    {name: "T1", type: "tactile", force: 67, brand_id: "6158e4215bd37e5dfc4e5292"},
    {name: "Alpaca V2", type: "linear", force: 62, brand_id: "6158e4215bd37e5dfc4e5292"},
    {name: "Cream", type: "linear", force: 55, brand_id: "6158e4215bd37e5dfc4e5294"},
    {name: "Tealios V2", type: "linear", force: 67, brand_id: "6158e4215bd37e5dfc4e5295"},
    {name: "Boba U4T", type: "tactile", force: 62, brand_id: "6158e4215bd37e5dfc4e5298"},
    {name: "BOX Heavy Dark Yellow", type: "linear", force: 70, brand_id: "6158e4215bd37e5dfc4e5299"},
    {name: "NK_Blueberry", type: "tactile", force: 80, brand_id: "6158e4215bd37e5dfc4e5294"},
    {name: "MX Black", type: "linear", force: 60, brand_id: "6158e3275bd37e5dfc4e5283"},
])
```

`Ex`

```sh
db.switch.aggregate([
  {$lookup: {
      from: "brand",
      localField: "brand_id",
      foreignField: "_id",
      as: "brand"
  }}
])
```

```JSON
// Response
[
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e529c"},
    "brand": [
      {
        "_id": "6158e3275bd37e5dfc4e5283",
        "name": "Cherry MX"
      }
    ],
    "brand_id": "6158e3275bd37e5dfc4e5283",
    "force": 46,
    "name": "MX Speed Silver",
    "type": "linear"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e529d"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5291",
        "name": "Gateron"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5291",
    "force": 60,
    "name": "Black Inks",
    "type": "linear"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e529e"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5292",
        "name": "Durock"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5292",
    "force": 67,
    "name": "T1",
    "type": "tactile"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e529f"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5292",
        "name": "Durock"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5292",
    "force": 62,
    "name": "Alpaca V2",
    "type": "linear"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e52a0"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5294",
        "name": "NovelKey"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5294",
    "force": 55,
    "name": "Cream",
    "type": "linear"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e52a1"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5295",
        "name": "Zeal"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5295",
    "force": 67,
    "name": "Tealios V2",
    "type": "linear"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e52a2"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5298",
        "name": "Gazzew"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5298",
    "force": 62,
    "name": "Boba U4T",
    "type": "tactile"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e52a3"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5299",
        "name": "Kailh"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5299",
    "force": 70,
    "name": "BOX Heavy Dark Yellow",
    "type": "linear"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e52a4"},
    "brand": [
      {
        "_id": "6158e4215bd37e5dfc4e5294",
        "name": "NovelKey"
      }
    ],
    "brand_id": "6158e4215bd37e5dfc4e5294",
    "force": 80,
    "name": "NK_Blueberry",
    "type": "tactile"
  },
  {
    "_id": {"$oid": "6158e6175bd37e5dfc4e52a5"},
    "brand": [
      {
        "_id": "6158e3275bd37e5dfc4e5283",
        "name": "Cherry MX"
      }
    ],
    "brand_id": "6158e3275bd37e5dfc4e5283",
    "force": 60,
    "name": "MX Black",
    "type": "linear"
  }
]
```

look and match

```sh
db.switch.aggregate([
  {$lookup: {
      from: "brand",
      localField: "brand_id",
      foreignField: "_id",
      as: "brand"
  }},
  {$match: {"brand.name": "Cherry MX"}},
])
```
```sh
db.switch.aggregate([
  {$lookup: {
      from: "brand",
      localField: "brand_id",
      foreignField: "_id",
      as: "brand"
  }},
  {$match: {"force": { $gte: 50 }}},
])
```
