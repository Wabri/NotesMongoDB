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

## CRUD operations

* Create:

	```Mongo
	insertOne(data, options)
	```

	```Mongo
	insertMany(data, options)
	```

* Read:

	```Mongo
	find(filter, options)
	```

	```Mongo
	findOne(filter, options)
	```

* Update:

	```Mongo
	updateOne(filter, data, options)
	```

	```Mongo
	updateMany(filter, data, options)
	```

	```Mongo
	replaceOne(filter, data, options)
	```

* Delete:

	```Mongo
	deleteOne(filter, options)
	```

	```Mongo
	deleteMany(filter, options)
	```

## Insert data to database

```Mongo
db.<name_of_data>.insertOne({"key0":"value0", key1:"value1"})
```

example:

```Mongo
db.products.insertOne({
	name: "computer",
	price: 100.999,
	description: "This is a high value product.",
	details:{
		cpu: "Intel i7",
		"memory": "32"
	}
})
```

## Insert many datas to database

```Mongo
db.<name_of_data>.insertMany([
	{
		"key0":"value0",
		key1:"value1"
	},
	{
		"key2":"value2",
		key3:"value3"
	}
])
```

example:

```Mongo
db.flightData.insertMany([
	{
		"departureAirport": "MUC",
		"arrivalAirport": "SFO",
		"aircraft": "Airbus A380",
		"distance": 12000,
		"intercontinental": true
	},
	{
		"departureAirport": "LHR",
		"arrivalAirport": "TXL",
		"aircraft": "Airbus A320",
		"distance": 950,
		"intercontinental": false
	}
])
```

## Retrive data from database

### Find

```Mongo
db.<name_of_data>.find(filters, options)
```

To beautify the results it can be use the pretty function:

```Mongo
db.<name_of_data>.find(filter, options).pretty()
```

example:

```Mongo
db.products.find().pretty()
```

```Mongo
db.<name_of_data>.find({intercontinental: true}).pretty()
```

```Mongo
db.flightData.find({distance:{$gt:100}}).pretty()
```

```Mongo
db.passengers.find().toArray()
```

```Mongo
db.passengers.find().forEach((passengerData) => {printjson(passengerData)})
```

The use of find below is called projection:

```Mongo
db.passengers.find({}, {name:1}).pretty()
```

### FindOne

```Mongo
db.<name_of_data>.findOne()
```

example:

```Mongo
db.flightData.findOne({distance:{$gt:100}})
```

## Delete data from database

```Mongo
db.<name_of_data>.deleteOne({key_filter: value_filter})
```

example:

```Mongo
db.fightData.deleteOne({departureAirport: "1"})
```

```Mongo
db.fightData.deleteMany({marker: "toDelete"})
```

```Mongo
db.fightData.deleteMany({})
```

## Update data

Be worry about the update function, the first one replace all the filtered data:
```Mongo
db.<name_of_data>.update(
	{key_filter: value_filter},
	{key_update: value_update}
)
```

This second type of update need a option:

```Mongo
db.<name_of_data>.updateOne(
	{key_filter: value_filter},
	{$option: {key_update: value_update}}
)
```

example:

```Mongo
db.flightData.updateOne(
	{departureAirport:"123"},
	{$set:{marker: 'delete'}}
)
```

```Mongo
db.flightData.updateMany(
	{},
	{$set: {
		marker: 'toDelete'
	}}
)
```

```Mongo
db.flightData.update(
	{"_id":ObjectId("5d09ef2276acd23a2e3fb02b")},
	{delayed:false}
)
```

## Replace Data

```Mongo
db.<name_of_data>.replaceOne(filter, options)
```

example:

```Mongo
db.flightData.replaceOne(
	{"_id": ObjectId("5d09ef2276acd23a2e3fb02b")},
	{
		"departureAirport": "MUC",
		"arrivalAirport": "SFO",
		"aircraft": "Airbus A380",
		"distance": 12000,
		"intercontinental": true
	}
)
```
## Nested documents

```Mongo
db.flightData.updateMany(
	{},
	{$set: {
		status: {
			description: "on-time",
			lastUpdated: "1 hour ago",
			details: {
				responsible: "Max Schwarzmuller"
			}
		}
	}}
)
```

## Embedded documents and max document value

In MongoDB it's possible to have at least 100 levels of nesting.
Documents have a maximum size of 16MB.


## Mongo drivers

https://docs.mongodb.com/ecosystem/drivers/

