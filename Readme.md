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

<hr>
<h1>Aggregation pipeline in Mongo db</h1>
<p>Aggregation pipelines allow us to group, sort, perform calculations and analyze data. Aggregation pipelines can have one or more "stages". The order of these stages are important. Each stage acts upon the results of the previous stage.</p>

```shell

db.collection_name.aggregate([
//first stage to match the data 
{
$match:{condition}
},

//stage 2 will be group all the documents and perform some operations like calculating the total of the data.

{
$group:{_id:"$category or other value", totalviews:{$sum:"$views"}}
}

//group will create another group of document on basis of unique id

])
```

<h2>Aggregation $group</h2>
<p>This aggregation stage groups documents by the unique "_id" expression</p>

```shell
db.collection_name.aggregae([
{
$group:{_id:"$category"}
}
])
```

<hr>
<h2>Aggregation $limit</h2>
<p>This stage limit the number of documents passed to the next stage.</p>
<hr>

```shell

db.collection_name.aggregate([
{ $limit:1 }
])

//this will return only one document from the collection

```

<hr>
<h2>Aggregation $project</h2>
<p>This aggregation stage  passes only the specified fields to the next aggregation stage.</p>
<hr>

```shell
db.restaurants.aggregate([

{
 $project:{
 "name":1,
 "cuisine":1,
 "address":1
  }
},
{
$limit: 5
}
])

//here restaurants is a collection name
// 1 refers that we want to display the data
//if we do not want to send the data to the next stage then that value can be changed to 0
```

<hr>
<h2>Aggregation $sort</h2>
<p>This aggregation stage groups sort all documents in the specified sort order.</p>
<hr>

```shell
db.listingsAndReviews.aggregate([

{
$sort:{"accommodates":-1}
},
{
  $project:{
  "name":1,
  "accommodates":1,
  }
},
{
$limit:5
}
])

```

<hr>
<h2>Aggregation $match</h2>
<p>this aggregation stage behaves like a find. It will filter documents that match the query provided</p>

```shell
db.listingsAndReviews.aggregate([
{
$match:{property_type:"House"}
},
{$limit:2},
{
$project:{
"name":1,
"bedrooms":1,
"price":1,
}
}
])

```
<hr>
<h2>Aggregation $addFields</h2>
<p>This aggregation stage adds new fields to documents.</p>
<hr>

```shell
db.restaurants.aggregate([
  {
    $addFields:{
          avgGrade:{ $avg: "$grades.score"}
       }
   },
 {
   $project:{
 "name":1,
"avgGrade":1,
}
},
{$limit:5}
])


```

<hr>
<h2>Aggregation $count</h2>
<p>This aggregation stage counts the total amount of documents passed from the previous stage</p>
<hr>

```shell
db.restaurants.aggregate([
{
$match:{"cuisine":"chinese"}
},
{
$count:"totalChinese"
}
])
```

<hr>
<h2>Aggregation $lookup</h2>
<p>This aggregation stage performs a left outer join to a collection in the same database.</p>
<h5>There are four required fieilds </h5>
<ul>
 <li>from : The collection to use for lookup in the same database</li>
 <li>LocalField: The field in the primary collection that can be used as a unique identifier  in the form collection.</li>
 <li>foreignField: the field in the from collection that can be used as a unique identifier in the primary collection</li>
 <li>as: the name of the new field that will contain the matching documents  from the  from collection</li>
</ul>

```shell
db.comments.aggregate([
  {
    $lookup: {
      from: "movies",
      localField: "movie_id",
      foreignField: "_id",
      as: "movie_details",
    },
  },
  {
    $limit: 1
  }
])

```

<img src="" alt="aggregation $lookup"/>










