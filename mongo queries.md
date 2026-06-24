PS D:\Kp> mongod --version
db version v6.0.8
Build Info: {
    "version": "6.0.8",
    "gitVersion": "3d84c0dd4e5d99be0d69003652313e7eaf4cdd74",
    "modules": [],
    "allocator": "tcmalloc",
    "environment": {
        "distmod": "windows",
        "distarch": "x86_64",
        "target_arch": "x86_64"
    }
}


PS D:\Kp> mongosh       
Current Mongosh Log ID: 6a3a293ed7c66f2f6a33f744
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+1.10.3
Using MongoDB:          6.0.8
Using Mongosh:          1.10.3

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2026-06-15T10:49:41.172+05:30: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted 
------

test> use mydb1
switched to db mydb1
mydb1> db
mydb1


mydb1> show collections


mydb1> db.createCollection("Student")
{ ok: 1 }


mydb1> db.faculty.drop()
false


mydb1> db.createCollection("faculty")
{ ok: 1 }


mydb1> db.faculty.drop()
true


mydb1> db.student.insertOne({name:'A',rollno:1})
{
  acknowledged: true,
  insertedId: ObjectId("6a3a2a55d7c66f2f6a33f745")
}


mydb1> db.student.insertMany([{name:'B',rollno:2},{name:'C',rollno:3}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("6a3a2aa8d7c66f2f6a33f746"),
    '1': ObjectId("6a3a2aa8d7c66f2f6a33f747")
  }
}


mydb1> db.student.find
[Function: find] AsyncFunction {
  returnsPromise: true,
  apiVersions: [ 1, Infinity ],
  returnType: 'Cursor',
  serverVersions: [ '0.0.0', '999.999.999' ],
  topologies: [ 'ReplSet', 'Sharded', 'LoadBalanced', 'Standalone' ],
  deprecated: false,
  platforms: [ 'Compass', 'Browser', 'CLI' ],
  isDirectShellCommand: false,
  acceptsRawInput: false,
  shellCommandCompleter: undefined,
  help: [Function (anonymous)] Help
}


mydb1> db.student.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 }
]


mydb1> db.student.insertMany([{name:'B',city:'Ahmedabad'}]
... db.student.insertMany([{name:'B',city:'Ahmedabad'}])
Uncaught:
SyntaxError: Unexpected token, expected "," (2:0)

  1 | db.student.insertMany([{name:'B',city:'Ahmedabad'}]
> 2 | db.student.insertMany([{name:'B',city:'Ahmedabad'}])
    | ^
  3 |



mydb1> db.student.insertOne({name:'D',city:'Ahmedabad'})
{
  acknowledged: true,
  insertedId: ObjectId("6a3a2b4cd7c66f2f6a33f748")
}

mydb1> db.student.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]


mydb1> db.student.renameCollection('students')
{ ok: 1 }


mydb1> show collections
Student 
students


mydb1> db.student.find()



mydb1> db.students.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]


mydb1> db.Student.find()



mydb1> db.Student.drop()
true


mydb1> show collections
students


mydb1> db.find({name:'A'})
TypeError: db.find is not a function


mydb1> db.students.find({name:'A'})
[ { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A', rollno: 1 } ]


mydb1> db.students.find({},{name:1})
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A' },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B' },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C' },
  { _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"), name: 'D' }
]


mydb1> db.students.find({},{name:0})
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), rollno: 3 },
  { _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"), city: 'Ahmedabad' }
]


mydb1> db.students.find({},{_id:0,name:'A'})
[ { name: 'A' }, { name: 'A' }, { name: 'A' }, { name: 'A' } ]


mydb1> db.students.find({},{city:0,name:1})
MongoServerError: Cannot do inclusion on field name in exclusion projection


mydb1> db.students.find({},{_id:0,name:1})
[ { name: 'A' }, { name: 'B' }, { name: 'C' }, { name: 'D' } ]


mydb1> db.students.find({},{city:0})
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  { _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"), name: 'D' }
]




mydb1> db.students.find({name:'A'},{_id:0,rollno:false})
[ { name: 'A' } ]


mydb1> db.students.find({name:'A'},{_id:1,rollno:false})
[ { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A' } ]


mydb1> db.students.findOne({},{name:1})
{ _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A' }


mydb1> db.students.findOne({rollno:3},{name:1})
{ _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C' }


mydb1> db.students.find().limit
[Function: limit] {    
  returnType: 'Cursor',
  serverVersions: [ '0.0.0', '999.999.999' ],
  apiVersions: [ 0, Infinity ],
  topologies: [ 'ReplSet', 'Sharded', 'LoadBalanced', 'Standalone' ],
  returnsPromise: false,
  deprecated: false,
  platforms: [ 'Compass', 'Browser', 'CLI' ],
  isDirectShellCommand: false,
  acceptsRawInput: false,
  shellCommandCompleter: undefined,
  help: [Function (anonymous)] Help
}


mydb1> db.students.find().limit(2)
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'A', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 }
]


mydb1> db.students.find().limit(2).skip(1)
[
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 }
]


mydb1> db.updateOne({name:'A'},{$set:{name:'AA'}})
TypeError: db.updateOne is not a function


mydb1> db.students.updateOne({name:'A'},{$set:{name:'AA'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}


mydb1> db.students.updateOne({name:'A'},{$set:{name:'AA',city:'Hmt'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}


mydb1> db.students.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]


mydb1> db.students.updateOne({name:'A'},{$set:{name:'AA',rollno:11}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}


mydb1> db.students.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 1 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]


mydb1> db.students.updateOne({name:'AA'},{$set:{name:'A'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}


mydb1> db.students.updateOne({name:'A'},{$set:{name:'AA',rollno:11}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}


mydb1> db.students.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 11 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]



mydb1> db.students.updateMany({name:'A'},{$set:{name:'AA',rollno:11}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}


mydb1> db.students.updateOne({name:'AA'},{$set:{name:'A'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}



mydb1> db.students.updateMany({name:'A'},{$set:{name:'AA',rollno:11}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}



mydb1> db.students.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 11 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]


mydb1> db.students.updateOne({name:'E'},{$set:{name:'EE',rollno:5}},{upsert:true})
{
  acknowledged: true,
  insertedId: ObjectId("6a3a32f36c07e5e7dc640eaf"),
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 1
}


mydb1> db.students.find()
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 11 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  },
  { _id: ObjectId("6a3a32f36c07e5e7dc640eaf"), name: 'EE', rollno: 5 }
]



mydb1> db.students.count()
DeprecationWarning: Collection.count() is deprecated. Use countDocuments or estimatedDocumentCount.
5


mydb1> db.students.find().count()
5


mydb1> db.students.find().countDocument()
TypeError: db.students.find().countDocument is not a function


mydb1> db.students.find().countDocuments()
TypeError: db.students.find().countDocuments is not a function


mydb1> db.students.countDocuments()
5


mydb1> db.student.find().sort({rollno:1})



mydb1> db.students.find().sort({rollno:1})
[  
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  { _id: ObjectId("6a3a32f36c07e5e7dc640eaf"), name: 'EE', rollno: 5 },
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 11 }
]


mydb1> db.students.find().sort({rollno:-1})
[
  { _id: ObjectId("6a3a2a55d7c66f2f6a33f745"), name: 'AA', rollno: 11 },
  { _id: ObjectId("6a3a32f36c07e5e7dc640eaf"), name: 'EE', rollno: 5 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f747"), name: 'C', rollno: 3 },
  { _id: ObjectId("6a3a2aa8d7c66f2f6a33f746"), name: 'B', rollno: 2 },
  {
    _id: ObjectId("6a3a2b4cd7c66f2f6a33f748"),
    name: 'D',
    city: 'Ahmedabad'
  }
]
