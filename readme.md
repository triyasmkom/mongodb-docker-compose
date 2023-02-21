# MongoDB
## Install mongoDB tanpa docker
Reference:
- https://www.mongodb.com/docs/manual/installation/

## Install mongoDB dan mongo express dengan docker compose
1. Install docker dan docker-compose terlebih dahulu
2. Buatlah folder baru dan buat file docker-compose.yml
    ```yaml
    version: '2.1'

    services:
      mongo:
        image: mongo
        container_name: mongoDB
        restart: always
        ports:
            - 27027:27017
        environment:
            MONGO_INITDB_ROOT_USERNAME: root
            MONGO_INITDB_ROOT_PASSWORD: '12345'
        volumes:
            - ./database/mongo:/data/db

      mongo-express:
        image: mongo-express
        container_name: mongoExpress
        restart: always
        ports:
            - 8081:8081
        environment:
            ME_CONFIG_MONGODB_ADMINUSERNAME: root
            ME_CONFIG_MONGODB_ADMINPASSWORD: '12345'
            ME_CONFIG_MONGODB_URL: mongodb://root:12345@mongo:27017/
        volumes:
            - ./database/mongo_express:/home/user/data
    ```
   
3. Buka terminal, jalankan perintah:

    **Menjalankan docker compose :**
    ```bash
    docker-compose up -d
    ```
   Output:
    ```
    root@pc:/home/user/mongo-db# docker-compose up -d

    Creating network "mongodb_default" with the default driver
    Pulling mongo-express (mongo-express:latest)...
    latest: Pulling from library/mongo-express
    6a428f9f83b0: Pulling fs layer
    6a428f9f83b0: Downloading [>                                                  ]   29.5kB/2.817MB: Downloading [>                                                  ]  22.
    f2b1fb32259e: Downloading [>                                                  ]  249
    6a428f9f83b0: Pull complete
    f2b1fb32259e: Pull complete
    40888f2a0a1f: Pull complete
    4e3cc9ce09be: Pull complete
    eaa1898f3899: Pull complete
    ab4078090382: Pull complete
    ae780a42c79e: Pull complete
    e60224d64a04: Pull complete
    Digest: sha256:dcfcf89bf91238ff129469a5a94523b3025913dcc41597d72d4d5f4a0339cc7d
    Status: Downloaded newer image for mongo-express:latest
    Creating mongodb_mongo_1 ... 
    Creating mongodb_mongo-express_1 ... 
    Creating mongodb_mongo-express_1
    Creating mongodb_mongo_1 ... done
    
    ```

    **Melihat container yang sedang berjalan :**
    ```bash
    docker-compose ps
    ```
   
   Output
    ```
    root@pc:/home/user/mongo-db# docker-compose ps

            Name                        Command                 State        Ports  
    ---------------------------------------------------------------------------------
    mongodb_mongo-express_1   tini -- /docker-entrypoint ...   Restarting            
    mongodb_mongo_1           docker-entrypoint.sh mongod      Up           27017/tcp
    ```

    **Menghentikan docker compose :**
    ```bash
    docker-compose down
    ```
   Output:
    ```
    root@pc:/home/user/mongo-db# docker-compose down

    Stopping mongodb_mongo_1         ... done
    Stopping mongodb_mongo-express_1 ... done
    Removing mongodb_mongo_1         ... done
    Removing mongodb_mongo-express_1 ... done
    Removing network mongodb_default
    ```
    **Command**
    ```
    Commands:
        build              Build or rebuild services
        bundle             Generate a Docker bundle from the Compose file
        config             Validate and view the Compose file
        create             Create services
        down               Stop and remove containers, networks, images, and volumes
        events             Receive real time events from containers
        exec               Execute a command in a running container
        help               Get help on a command
        images             List images
        kill               Kill containers
        logs               View output from containers
        pause              Pause services
        port               Print the public port for a port binding
        ps                 List containers
        pull               Pull service images
        push               Push service images
        restart            Restart services
        rm                 Remove stopped containers
        run                Run a one-off command
        scale              Set number of containers for a service
        start              Start services
        stop               Stop services
        top                Display the running processes
        unpause            Unpause services
        up                 Create and start containers
        version            Show the Docker-Compose version information
    ```
4. Buka mongo-express di localhost:8081

    ![image](./images/image2.png)

5. kita bisa juga masuk ke CLI nya docker dengan perintah (bagi yang memiliki pengetahuan linux)

   ```bash
    docker exec -it mongoDB bash
   ```

   ```
   root@triyas-ThinkPad-T420:/home/triyas/mongo-db# docker exec -it mongoDB bash
   root@415057c4988a:/#
   root@415057c4988a:/#
   ```
6. Kita juga bisa menggunakan vs code untuk connect ke mongoDB
    - Download package mongoDB

        ![image](./images/image3.png)

    - Ketikan F1 pada vs code pilih mongoDB-connect

        ![image](./images/image4.png)

    - Pilih open form kemudian pilih login dengan username dan password
        ![image](./images/image5.png)
    - Jika berhasil connect, klik simbol mongoDB di sebelah kiri

        ![image](./images/image6.png)

    - untuk query nya, kita bisa menggunakan playground dengan cara create playground baru, kemudian masukkan query yang diinginkan.

        ![image](./images/image7.png)

Referensi:
- https://hub.docker.com/_/mongo
- https://www.youtube.com/watch?v=tiD2ju8dK24
- https://www.learmoreseekmore.com/2022/03/demo-on-mongodb-running-on-docker-and-visual-studio-code-mongodb-extension-playground.html
- https://github.com/uzrnem/docker-compose-files/blob/main/mongodb-expressui.yml

## **Apa itu mongoDb ?**
1. NoSQL Database
2. Not Only SQL Database
3. Written in C++
4. Open Source Document Database

## **Jenis-jenis Database**
**NoSQL Database** | **NoSQL Database**
:-------------:|:-------------:|
Redis | SQLite
CouchDB | MySQL
Cloud Firestore| PostgreSQL
MongoDB | Oracle
dan lain-lain | dan lain-lain


## **Perbedaan Database NoSQL dan Realasional**

**NoSQL** | **Relational**
:-------------:|:-------------:|
 Document based | Table based
 Dynamic schema | Predefined schema
 Horizontally Scalable | Vertically scalable
 Not as good | Good for Complex queries


## Struktur database
1. Database
- A container for collections
- Has own set of files on system
- Can have multiple collections in single DB

2. Collections
- They are like Tables in RDBMS
- They contain a set of records, normally of similar type

3. Documents
- Set of key value pairs
- Not required to have same set of fields
- Fileds can have different types of data

**Struktur Database MongoDB**
    
![image](./images/image1.png) 

## Tipe Data
- String
- Integer
- Boolean
- Double
- Arrays
- TimeStamp
- Date
- Object
- Binary Data
- Etc.

**Contoh Data di MongoDB**

A Single Document inside a Collections
```json
{
    "id": ObjectId("dgfrefradewfewfdsawef"),
    "email": "Youremail@gmail.com",
    "status":"Success",
    "tags": ["java", "nodejs", "express-js"]
    "followes": 100,
    "comments": [
        {
            "username":"john@gmail.com",
            "text": "i like mongoDB",
            "likes": 4,
            "phone": "+628123456789"
        },
        {
            "username":"abc@gmail.com",
            "text": "i like mongoDB",
            "likes": 4,
            "phone": "+628123456789"
        }
    ]
}

```

USERS (Collections)
```json
{
    "id": ObjectId("dgfrefrewfwdadewfewfdsawef"),
    "email":"john@gmail.com",
    "username": "john",
    "phone": ["+628123456777"]
},
{
    "id": ObjectId("dgfrefrdsfsdadewfewfdsawef"),
    "email":"abc@gmail.com",
    "username": "abc",
    "phone": ["+628123456789", "+628123456788"]
}

```

**Contoh Perbedaan Query SQL dan MongoDB**

SQL Select Statement
```sql
SELECT * FROM people 
```

MongoDB Statement
```js
    db.people.find()
```
SQL Select Statement
```sql
SELECT * FROM people WHERE status= "A"
```
MongoDB Statement
```js
db.people.find({status:"A"})
```
SQL Select Statement
```sql
SELECT * FROM people WHERE status="A" OR age=50
```
MongoDB Statement
```js
db.people.find({$or: [{status: "A"}, {age:50}]})
```

## Query mongoDB
**Membuat Database dan Collections**

```js
// create database
use('my_db_test')

// create collection
db.createCollection('person')

```
Output:
```json
{
  "ok": 1
}
```
**Menambahkan document dalam collection**

Insert Many:
```js
// insert many
db.person.insertMany([
    {
        name:"triyas",
        age: 32
    },
    {
        name:"nando",
        age: 44
    }
])
```
Output:
```json
{
  "acknowledged": true,
  "insertedIds": {
    "0": {
      "$oid": "63ef21f6e748851d5d14b31d"
    },
    "1": {
      "$oid": "63ef21f6e748851d5d14b31e"
    }
  }
}
```
Insert One:
```js
// insert one
db.person.insertOne({
    name:"daniel",
    age: 32
})
```
Output:
```json
{
  "acknowledged": true,
  "insertedId": {
    "$oid": "63ef2264506424e9c7a6fc5f"
  }
}
```

**Menampilkan Document**

Select All:
```js
// find all
db.person.find()
```
Output:
```json
[
  {
    "_id": {
      "$oid": "63ef21f6e748851d5d14b31d"
    },
    "name": "triyas",
    "age": 32
  },
  {
    "_id": {
      "$oid": "63ef21f6e748851d5d14b31e"
    },
    "name": "nando",
    "age": 44
  }
]
```

Select One:
```js
// find one
db.person.find({name:"triyas"})
```

Output:
```json
[
  {
    "_id": {
      "$oid": "63ef21f6e748851d5d14b31d"
    },
    "name": "triyas",
    "age": 32
  }
]
```

Select with comparison operator:
```
$lt     : less than
$lte    : less than equal
$gt     : greater than
$gte    : greater than equal
etc.

```

```js
db.person.find({
    age:{
        $gt:35
    }
})
```

Output:
```json
[
  {
    "_id": {
      "$oid": "63ef21f6e748851d5d14b31e"
    },
    "name": "nando",
    "age": 44
  }
]
```

**Update Document**

Update One:
```js
// update one
db.person.updateOne({
    name:"triyas"
},{
    /**
     * field: The field name
     * expression: The expression.
     */
    $set: {
      age: 12
    }
})
```

Output:
```json
{
  "acknowledged": true,
  "insertedId": null,
  "matchedCount": 1,
  "modifiedCount": 1,
  "upsertedCount": 0
}
```
Update many:
```js
// update many
db.person.updateMany({
    age:{
        $gt: 35
    }
},{
    $set:{
        age:22
    }
})
```
Output:
```json
{
  "acknowledged": true,
  "insertedId": null,
  "matchedCount": 2,
  "modifiedCount": 2,
  "upsertedCount": 0
}
```

**Delete Document**

Delete One:
```js
db.person.deleteOne({
    name: triyas
})
```
Output:
```json
{
  "acknowledged": true,
  "deletedCount": 1
}
```

Delete many:
```js
db.person.deleteMany({
    age:22
})

```
Output:
```json
{
  "acknowledged": true,
  "deletedCount": 2
}
```

## Query
### Insert Document
Insert a Single Document
```js
db.inventory.insertOne({
    item: "canvas", 
    qty: 100, 
    tags: ["cotton"], 
    size: { 
        h: 28, 
        w: 35.5, 
        uom: "cm" 
    }            
})
```
Output:
```json
{
  "acknowledged": true,
  "insertedId": {
    "$oid": "63ef40a6a76c48ba86d5a557"
  }
}
```

Check Document:
```js
db.inventory.find( { item: "canvas" } )
```
```json
[
  {
    "_id": {
      "$oid": "63ef40a6a76c48ba86d5a557"
    },
    "item": "canvas",
    "qty": 100,
    "tags": [
      "cotton"
    ],
    "size": {
      "h": 28,
      "w": 35.5,
      "uom": "cm"
    }
  }
]
```

Insert Many Document
```js
db.inventory.insertMany([{ 
    item: "journal", 
    qty: 25, 
    tags: ["blank", "red"], 
    size: { 
        h: 14, 
        w: 21, 
        uom: "cm" 
    } 
},{ 
    item: "mat", 
    qty: 85, 
    tags: ["gray"], 
    size: { 
        h: 27.9, 
        w: 35.5, 
        uom: "cm" 
    } 
},{ 
    item: "mousepad", 
    qty: 25, 
    tags: ["gel", "blue"], 
    size: { 
        h: 19, 
        w: 22.85, 
        uom: "cm" 
    } 
}])
```
Output:
```json
{
  "acknowledged": true,
  "insertedIds": {
    "0": {
      "$oid": "63ef41aef8fc958bbc93421e"
    },
    "1": {
      "$oid": "63ef41aef8fc958bbc93421f"
    },
    "2": {
      "$oid": "63ef41aef8fc958bbc934220"
    }
  }
}
```


Check Document:
```js
db.inventory.find({})
```

Output:
```json
[
  {
    "_id": {
      "$oid": "63ef40a6a76c48ba86d5a557"
    },
    "item": "canvas",
    "qty": 100,
    "tags": [
      "cotton"
    ],
    "size": {
      "h": 28,
      "w": 35.5,
      "uom": "cm"
    }
  },
  {
    "_id": {
      "$oid": "63ef41aef8fc958bbc93421e"
    },
    "item": "journal",
    "qty": 25,
    "tags": [
      "blank",
      "red"
    ],
    "size": {
      "h": 14,
      "w": 21,
      "uom": "cm"
    }
  },
  {
    "_id": {
      "$oid": "63ef41aef8fc958bbc93421f"
    },
    "item": "mat",
    "qty": 85,
    "tags": [
      "gray"
    ],
    "size": {
      "h": 27.9,
      "w": 35.5,
      "uom": "cm"
    }
  },
  {
    "_id": {
      "$oid": "63ef41aef8fc958bbc934220"
    },
    "item": "mousepad",
    "qty": 25,
    "tags": [
      "gel",
      "blue"
    ],
    "size": {
      "h": 19,
      "w": 22.85,
      "uom": "cm"
    }
  }
]
```


### Query Document
1. Select All Documents in a Collection
    ```sql
    SELECT * FROM inventory
    ```
    ```js
    db.inventory.find({})
    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef40a6a76c48ba86d5a557"
        },
        "item": "canvas",
        "qty": 100,
        "tags": [
          "cotton"
        ],
        "size": {
          "h": 28,
          "w": 35.5,
          "uom": "cm"
        }
      },
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421e"
        },
        "item": "journal",
        "qty": 25,
        "tags": [
          "blank",
          "red"
        ],
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        }
      },
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421f"
        },
        "item": "mat",
        "qty": 85,
        "tags": [
          "gray"
        ],
        "size": {
          "h": 27.9,
          "w": 35.5,
          "uom": "cm"
        }
      },
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc934220"
        },
        "item": "mousepad",
        "qty": 25,
        "tags": [
          "gel",
          "blue"
        ],
        "size": {
          "h": 19,
          "w": 22.85,
          "uom": "cm"
        }
      }
    ]
    ```
2. Select document use filter

    **Kondisi Spesifik Persamaan:**
    ```sql
    # Query SQl:
    SELECT * FROM inventory WHERE status = "D"
    ```
    ```js
    // Query mongoDB:
    db.inventory.find({
        item: "mat"
    })

    db.inventory.find({
        _id: ObjectId("63ef41aef8fc958bbc93421e")
    })
    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421f"
        },
        "item": "mat",
        "qty": 85,
        "tags": [
          "gray"
        ],
        "size": {
          "h": 27.9,
          "w": 35.5,
          "uom": "cm"
        },
        "status": "C"
      }
    ]
    ```
    **Kondisi Spesifik menggunakan Operator Query**

    ```sql
    # Query SQL:
    SELECT * FROM inventory WHERE status in ("A", "D")
    ```

    ```js

    // Query MongoDB:
    db.inventory.find({
        status:{$in: ["D","B"]}
    })
    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef40a6a76c48ba86d5a557"
        },
        "item": "canvas",
        "qty": 100,
        "tags": [
          "cotton"
        ],
        "size": {
          "h": 28,
          "w": 35.5,
          "uom": "cm"
        },
        "status": "B"
      },
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc934220"
        },
        "item": "mousepad",
        "qty": 25,
        "tags": [
          "gel",
          "blue"
        ],
        "size": {
          "h": 19,
          "w": 22.85,
          "uom": "cm"
        },
        "status": "D"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb47"
        },
        "item": "paper",
        "qty": 100,
        "size": {
          "h": 8.5,
          "w": 11,
          "uom": "in"
        },
        "status": "D"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb48"
        },
        "item": "planner",
        "qty": 75,
        "size": {
          "h": 22.85,
          "w": 30,
          "uom": "cm"
        },
        "status": "D"
      }
    ]
    ```

    **Kondisi Operator AND**
    ```sql
    # Query SQL:
    SELECT * FROM inventory WHERE status = "A" AND qty < 30
    ```
    ```js
    // Query MongoDB:
    db.inventory.find({
        status:"A",
        qty: {$lt:30}
    })

    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421e"
        },
        "item": "journal",
        "qty": 25,
        "tags": [
          "blank",
          "red"
        ],
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb45"
        },
        "item": "journal",
        "qty": 25,
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      }
    ]
    ```

    **Kondisi Operator OR**
    ```sql
    # Query SQL:
    SELECT * FROM inventory WHERE status = "A" OR qty < 30
    ```
   
    ```js
    // Query MongoDB:
    db.inventory.find({
        $or:[
            {status:"A"},
            {qty:{
                $lt:30
            }}
        ]
    })
    ```
    Output:
    ```json

    [
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421e"
        },
        "item": "journal",
        "qty": 25,
        "tags": [
          "blank",
          "red"
        ],
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc934220"
        },
        "item": "mousepad",
        "qty": 25,
        "tags": [
          "gel",
          "blue"
        ],
        "size": {
          "h": 19,
          "w": 22.85,
          "uom": "cm"
        },
        "status": "D"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb45"
        },
        "item": "journal",
        "qty": 25,
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb46"
        },
        "item": "notebook",
        "qty": 50,
        "size": {
          "h": 8.5,
          "w": 11,
          "uom": "in"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb49"
        },
        "item": "postcard",
        "qty": 45,
        "size": {
          "h": 10,
          "w": 15.25,
          "uom": "cm"
        },
        "status": "A"
      }
    ]
    ```

    **Kondisi Operator AND atau OR**
    ```sql
    # Query SQL
    SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")
    ```
   
    ```js
    // Query MongoDB
    db.inventory.find({
        status:"A",
        $or:[
            {qty:{$lt:30}},
            {item: {$regex:'\^p'}}
        ]
    })
    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421e"
        },
        "item": "journal",
        "qty": 25,
        "tags": [
          "blank",
          "red"
        ],
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb45"
        },
        "item": "journal",
        "qty": 25,
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb49"
        },
        "item": "postcard",
        "qty": 45,
        "size": {
          "h": 10,
          "w": 15.25,
          "uom": "cm"
        },
        "status": "A"
      }
    ]
    ```
3. Query pada dokumen bersarang

    **Query Mencocokkan dengan dokumen bersarang**

    ```js
    // Query MongoDB:
    db.inventory.find({
        size:{h:10, w:15.25, uom:"cm"}
    })
    ```
   
    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb49"
        },
        "item": "postcard",
        "qty": 45,
        "size": {
          "h": 10,
          "w": 15.25,
          "uom": "cm"
        },
        "status": "A"
      }
    ]
    ```

    **Query pada field bersarang**
    ```js
    db.inventory.find({
        "size.h":{$lt:15}
    })
    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421e"
        },
        "item": "journal",
        "qty": 25,
        "tags": [
          "blank",
          "red"
        ],
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb45"
        },
        "item": "journal",
        "qty": 25,
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb46"
        },
        "item": "notebook",
        "qty": 50,
        "size": {
          "h": 8.5,
          "w": 11,
          "uom": "in"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb47"
        },
        "item": "paper",
        "qty": 100,
        "size": {
          "h": 8.5,
          "w": 11,
          "uom": "in"
        },
        "status": "D"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb49"
        },
        "item": "postcard",
        "qty": 45,
        "size": {
          "h": 10,
          "w": 15.25,
          "uom": "cm"
        },
        "status": "A"
      }
    ]
    ```

    Kondisi AND
    ```js
    db.inventory.find({
        "size.h":{$lt:15},
        "size.uom":"cm",
        status:"A"
    })

    ```

    Output:
    ```json
    [
      {
        "_id": {
          "$oid": "63ef41aef8fc958bbc93421e"
        },
        "item": "journal",
        "qty": 25,
        "tags": [
          "blank",
          "red"
        ],
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb45"
        },
        "item": "journal",
        "qty": 25,
        "size": {
          "h": 14,
          "w": 21,
          "uom": "cm"
        },
        "status": "A"
      },
      {
        "_id": {
          "$oid": "63f2e590e159415856c6eb49"
        },
        "item": "postcard",
        "qty": 45,
        "size": {
          "h": 10,
          "w": 15.25,
          "uom": "cm"
        },
        "status": "A"
      }
    ]
    ```
4. Query pada sebuah array 

   Insert data terlebih dahulu
   ```console
   # melihat database
   show databases;
   
   # pindah ke database / membuat database baru
   use test2;
   
   # menampilkan collections (tables)
   show collections;
   
   # memasukkan banyak data
   db.inventory.insertMany([
   { item: "journal", qty: 25, tags: ["blank", "red"], dim_cm: [ 14, 21 ] },
   { item: "notebook", qty: 50, tags: ["red", "blank"], dim_cm: [ 14, 21 ] },
   { item: "paper", qty: 100, tags: ["red", "blank", "plain"], dim_cm: [ 14, 21 ] },
   { item: "planner", qty: 75, tags: ["blank", "red"], dim_cm: [ 22.85, 30 ] },
   { item: "postcard", qty: 45, tags: ["blue"], dim_cm: [ 10, 15.25 ] }
   ]);
   
   # melihat semua data
   db.inventory.find({})
   ```
   Output:
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c0e"},
       "dim_cm": [14, 21],
       "item": "journal",
       "qty": 25,
       "tags": ["blank", "red"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c0f"},
       "dim_cm": [14, 21],
       "item": "notebook",
       "qty": 50,
       "tags": ["red", "blank"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c10"},
       "dim_cm": [14, 21],
       "item": "paper",
       "qty": 100,
       "tags": ["red", "blank", "plain"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c11"},
       "dim_cm": [22.85, 30],
       "item": "planner",
       "qty": 75,
       "tags": ["blank", "red"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c12"},
       "dim_cm": [10, 15.25],
       "item": "postcard",
       "qty": 45,
       "tags": ["blue"]
     }
   ]
   ```
   Table Inventory

   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c0e | \[14, 21\] | journal | 25 | \["blank", "red"\] |
   | 63f432f013067766079f3c0f | \[14, 21\] | notebook | 50 | \["red", "blank"\] |
   | 63f432f013067766079f3c10 | \[14, 21\] | paper | 100 | \["red", "blank", "plain"\] |
   | 63f432f013067766079f3c11 | \[22.85, 30\] | planner | 75 | \["blank", "red"\] |
   | 63f432f013067766079f3c12 | \[10, 15.25\] | postcard | 45 | \["blue"\] |

   **Query dalam sebuah array**
   ```js
   db.inventory.find({tags:["red", "blank"]})
   ```
   Output:
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c0f"},
       "dim_cm": [14, 21],
       "item": "notebook",
       "qty": 50,
       "tags": ["red", "blank"]
     }
   ]
   ```

   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c0f | \[14, 21\] | notebook | 50 | \["red", "blank"\] |

   Atau bisa menggunakan operator ```$all```:
   ```js
   db.inventory.find({
       tags: {
           $all:["red", "blank"]
       }
   })
   ```
   Output:
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c0e"},
       "dim_cm": [14, 21],
       "item": "journal",
       "qty": 25,
       "tags": ["blank", "red"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c0f"},
       "dim_cm": [14, 21],
       "item": "notebook",
       "qty": 50,
       "tags": ["red", "blank"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c10"},
       "dim_cm": [14, 21],
       "item": "paper",
       "qty": 100,
       "tags": ["red", "blank", "plain"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c11"},
       "dim_cm": [22.85, 30],
       "item": "planner",
       "qty": 75,
       "tags": ["blank", "red"]
     }
   ]
   ```
   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c0e | \[14, 21\] | journal | 25 | \["blank", "red"\] |
   | 63f432f013067766079f3c0f | \[14, 21\] | notebook | 50 | \["red", "blank"\] |
   | 63f432f013067766079f3c10 | \[14, 21\] | paper | 100 | \["red", "blank", "plain"\] |
   | 63f432f013067766079f3c11 | \[22.85, 30\] | planner | 75 | \["blank", "red"\] |

   **Query dalam sebuah array untuk sebuah element**
   ```js
   db.inventory.find({
       tags: "red"
   })
   ```
   
   Output:
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c0e"},
       "dim_cm": [14, 21],
       "item": "journal",
       "qty": 25,
       "tags": ["blank", "red"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c0f"},
       "dim_cm": [14, 21],
       "item": "notebook",
       "qty": 50,
       "tags": ["red", "blank"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c10"},
       "dim_cm": [14, 21],
       "item": "paper",
       "qty": 100,
       "tags": ["red", "blank", "plain"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c11"},
       "dim_cm": [22.85, 30],
       "item": "planner",
       "qty": 75,
       "tags": ["blank", "red"]
     }
   ]
   ```
   
   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c0e | \[14, 21\] | journal | 25 | \["blank", "red"\] |
   | 63f432f013067766079f3c0f | \[14, 21\] | notebook | 50 | \["red", "blank"\] |
   | 63f432f013067766079f3c10 | \[14, 21\] | paper | 100 | \["red", "blank", "plain"\] |
   | 63f432f013067766079f3c11 | \[22.85, 30\] | planner | 75 | \["blank", "red"\] |


   **Multi Kondisi untuk elemen array**

   Query dengan kondisi Filter gabungan pada elemen array
   
   ```js
   db.inventory.find({
       dim_cm:{
           $gt: 15,
           $lt: 20
       }
   })
   ```
   
   Output:
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c0e"},
       "dim_cm": [14, 21],
       "item": "journal",
       "qty": 25,
       "tags": ["blank", "red"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c0f"},
       "dim_cm": [14, 21],
       "item": "notebook",
       "qty": 50,
       "tags": ["red", "blank"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c10"},
       "dim_cm": [14, 21],
       "item": "paper",
       "qty": 100,
       "tags": ["red", "blank", "plain"]
     },
     {
       "_id": {"$oid": "63f432f013067766079f3c12"},
       "dim_cm": [10, 15.25],
       "item": "postcard",
       "qty": 45,
       "tags": ["blue"]
     }
   ]
   ```
   
   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c0e | \[14, 21\] | journal | 25 | \["blank", "red"\] |
   | 63f432f013067766079f3c0f | \[14, 21\] | notebook | 50 | \["red", "blank"\] |
   | 63f432f013067766079f3c10 | \[14, 21\] | paper | 100 | \["red", "blank", "plain"\] |
   | 63f432f013067766079f3c12 | \[10, 15.25\] | postcard | 45 | \["blue"\] |
   
   
   Query element array yang memenuhi banyak kriteria
   ```js
   db.inventory.find({
       dim_cm:{
           $elemMatch:{
               $gt:22,
               $lt:30
           }
       }
   })
   ```
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c11"},
       "dim_cm": [22.85, 30],
       "item": "planner",
       "qty": 75,
       "tags": ["blank", "red"]
     }
   ]
   ```
   
   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c11 | \[22.85, 30\] | planner | 75 | \["blank", "red"\] |
   
   Query untuk element dengan posisi indeks array
   ```js
   db.inventory.find({
       "dim_cm.1":{
           $gt:25
       }
   })
   ```
   
   Output:
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c11"},
       "dim_cm": [22.85, 30],
       "item": "planner",
       "qty": 75,
       "tags": ["blank", "red"]
     }
   ]
   ```
   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c11 | \[22.85, 30\] | planner | 75 | \["blank", "red"\] |
   
   
   Query sebuah array dengan panjang array
   ```js
   db.inventory.find({
       "tags": {
           $size:3
       }
   })
   ```
   ```json
   [
     {
       "_id": {"$oid": "63f432f013067766079f3c10"},
       "dim_cm": [14, 21],
       "item": "paper",
       "qty": 100,
       "tags": ["red", "blank", "plain"]
     }
   ]
   ```
   | \_id | dim\_cm | item | qty | tags |
   | :--- | :--- | :--- | :--- | :--- |
   | 63f432f013067766079f3c10 | \[14, 21\] | paper | 100 | \["red", "blank", "plain"\] |
   







Untuk lebih details nya bisa lihat di documentasi resminya mongoDB pada link berikut ini:
- https://www.mongodb.com/docs/manual/
