# NotesMongoDB

## Install

https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition-using-deb-packages
https://www.mongodb.com/download-center/community

To test if the database are installed you can check by running:

```Bash
mongod --version
```

## Start database

By default uses /data/db as the storage path, if follow this standard you can start database without any arguments.
Run this on terminal:

```Bash
mongod --dbpath "my/new/path"
```

or

```Bash
mongo
```

## Use mongo

From another terminal run:

```Mongo
mongo --port <port_where_database_are>
```

Example:

```Bash
mongo --port 27018
```

## Database infos

```Mongo
show dbs
```

## Create new database

```Mongo
use <name_of_new_database>
```

example:

```Mongo
use shop
```

## Insert data to database

```Mongo
db.<name_of_data>.insertOne({"key0":"value0", key1:"value1"})
```

example:

```Mongo
db.products.insertOne({name: "computer", price: 100.999, description: "This is a high value product.", details:{ cpu: "Intel i7","memory": "32" }})
```

## Retrive data from database

```Mongo
db.<name_of_data>.find()
```

To beautify the results it can be use the pretty function:

```Mongo
db.<name_of_data>.find().pretty()
```

example:

```Mongo
db.products.find().pretty()
```

## Mongo drivers

https://docs.mongodb.com/ecosystem/drivers/


