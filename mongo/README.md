# Step by step doc to create a quick & simple Stateful deployment of MongoDB in the Kubernetes Cluster
## Created the MongoDB Deployment and the service
```
#jayadmin@cloudshell:~/mongodb (kubetrain-331123)$ kubectl apply -f mongod.yaml
#deployment.apps/mongo-depl created
#service/mongo-srv created
#persistentvolumeclaim/mongo-pvc created
```
## Login to the MongoDB Pod and the DB in the Kubernetes Cluster
```
kubectl exec -it mongod sh

root@mongo-depl-79948c9979-dvjcq:/# mongo mongodb://localhost:27017
MongoDB shell version v5.0.5
connecting to: mongodb://localhost:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("f1a17774-4aae-49d5-83d8-5d426c055d7f") }
MongoDB server version: 5.0.5
================
Warning: the "mongo" shell has been superseded by "mongosh",
which delivers improved usability and compatibility.The "mongo" shell has been deprecated and will be removed in
an upcoming release.
For installation instructions, see
https://docs.mongodb.com/mongodb-shell/install/
================
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
        https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
        https://community.mongodb.com
> user admin
uncaught exception: SyntaxError: unexpected token: identifier :
@(shell):1:5
> use admin
switched to db admin
> db.auth('admin','password2')
Error: Authentication failed.
0
> db.auth('admin','password')
1
> use newdb_shopping_cart
switched to db newdb_shopping_cart
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
> db.coll.findOne()
{ "_id" : ObjectId("61ccb00da553e6f45b8e9ca9"), "name" : "Max" }
> 
```
