//mongo db notes

<h5>There are two ways to use mongo db database</h5>
1. Mongo db atlas<br>
2. mongo db which can be installed in to our local machine

```shell
//creating database through mongosh command shell
//we can use command


use database_name // this will use the database if it is already existed if not then it will create new database

//creating collection in database
---> there are two ways to create collection
db.createcollection("collecton_name")

second method is:
we can directly insert document and then collection will be automatically created

db.collection_name.insertOne({objects})
//this will create collection along with the data


```

<hr>
<h3>CRUD operations in mongodb</h3>
<hr>

# insert or create
```shell
db.collection_name.insertOne({title:'testone'})
or
db.collection_name.insertMany({title:'testone'},{title:'test2'})
```

# Read 
```shell
db.collection_name.find()
//this will give us all the data from that collection

or
db.collection_name.find({title:'test1'})
//here we pass the condition like where in SQL database

db.collection_name.findOne()

//projection -. which means we can also define which data to be shown in the results

db.collection_name.find({}, {title:1})
//this will display results which contains title only
//if we change title value to 0 then the result will display all the values except title

db.collection_name.find({},{title:0})
```

 # update

```shell
db.collection_name.updateOne({condition},{$set:{value to change}})
//here value of first data will be updated by using "$set" operator

//if we want to  update multiple datas then

db.collection_name.updateMany({condition},{$set:{value to be changed}})
//this will update multiple data

//notes

//if we have to change the number value or integer values then

db.collection_name.updateMany({condition},{$inc:{value to be changed}})

```


# delete

```shell
//there are two methods which can be used to delete documents of collections

db.collection_name.deleteOne({title:'test1'})
//this will delete the first document that matches

or
db.collection_name.deleteMany({title:'test1'})
//this will delete multiple document that matches
```

# operators in mongo db

<hr>
<h3>Comparison operator</h3>
```shell
$eq -->equal to 
$ne -->not equal to
$gt -->greater than
$gte - greater then or equal to
$lt- less than
$lte - less than or equal to
$in - value is matched within the array
```
<hr>
<h3>Logical operator</h3>

```shell
$and -- Returns documents where both queries match
$or -- either of the values 
$nor --Returns documents where both queries fail to match
$not --Returns documents where the query does not match

```
<hr>
<h2>Evaluation operator</h2>

```shell
$regex - this one is used to search regular expressions
$text - this one is used to search the text
$where - this one uses javascript expressions to match document

```

<hr>

<h2>update operators</h2>

```shell
$currentdate - set the current date value
$inc - set the integer value
$set - to update the string values
$unset - to clear the field from the document
```









