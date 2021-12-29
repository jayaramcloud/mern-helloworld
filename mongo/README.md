# Step by step doc to create a quick & simple Stateful deployment of MongoDB in the Kubernetes Cluster
```
jayadmin@cloudshell:~/mongodb (kubetrain-331123)$ kubectl apply -f mongod.yaml                                                                                                                                                                    
statefulset.apps/mongodb-standalone unchanged
service/database created
```

```
jayadmin@cloudshell:~/mongodb (kubetrain-331123)$ kubectl exec -it mongodb-standalone-0 sh
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
# mongo mongodb://mongodb-standalone-0.database:27017
MongoDB shell version v4.2.17
connecting to: mongodb://mongodb-standalone-0.database:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("933a93b9-9c37-480a-9e72-6c8aa378a963") }
MongoDB server version: 4.2.17
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
        https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
        https://community.mongodb.com
> use admin
switched to db admin
> db.auth('admin','password')
1
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
> db
admin
> use newdb_shopping_cart
switched to db newdb_shopping_cart
> db.coll.insertOne({name: "Max"})
{
        "acknowledged" : true,
        "insertedId" : ObjectId("61cca6d8dd5786b406cc1434")
}
> db.coll.insert([{name: "Max"}, {name:"Alex"}]) // ordered bulk insert
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 2,
        "nUpserted" : 0,
        "nMatched" : 0,
        "nModified" : 0,
        "nRemoved" : 0,
        "upserted" : [ ]
})
> db.coll.insert([{name: "Max"}, {name:"Alex"}], {ordered: false}) // unordered bulk insert
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 2,
        "nUpserted" : 0,
        "nMatched" : 0,
        "nModified" : 0,
        "nRemoved" : 0,
        "upserted" : [ ]
})
> db.coll.insert({date: ISODate()})
WriteResult({ "nInserted" : 1 })
> db.coll.insert({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
WriteResult({ "nInserted" : 1 })
> db.coll.findOne()
{ "_id" : ObjectId("61cca6d8dd5786b406cc1434"), "name" : "Max" }
>
```
