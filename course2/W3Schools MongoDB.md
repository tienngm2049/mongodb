# W3Schools.MongoDB

SQL is relational database while MongoDB is document database.

In MongoDB, instead of tables these are called collections.

In MongoDB, instead of column these are called categories.

- CRUD Operations

![Untitled](W3Schools%20MongoDB/Untitled.png)

![Untitled](W3Schools%20MongoDB/Untitled%201.png)

- Aggregation Pipeline
    
    ![Untitled](W3Schools%20MongoDB/Untitled%202.png)
    

`db` in your terminal

type `show dbs`

`use` then the name of the database

# Create/**Insert**

```jsx
// Create collection
db.createCollection("posts")

// Add documents into "posts" collection

// insertOne
db.posts.insertOne({
  title: "Post Title 1",
  body: "Body of post.",
  category: "News",
  likes: 1,
  tags: ["news", "events"],
  date: Date()
})

// insertMany
db.posts.insertMany([  
  {
    title: "Post Title 2",
    body: "Body of post.",
    category: "Event",
    likes: 2,
    tags: ["news", "events"],
    date: Date()
  },
  {
    title: "Post Title 3",
    body: "Body of post.",
    category: "Technology",
    likes: 3,
    tags: ["news", "events"],
    date: Date()
  },
  {
    title: "Post Title 4",
    body: "Body of post.",
    category: "Event",
    likes: 4,
    tags: ["news", "events"],
    date: Date()
  }
])
```

# Find

There are 2 methods to find and select data from a MongoDB collection, `find()` and `findOne()`. 

```jsx
db.posts.find()

db.posts.findOne()
```

```jsx
db.posts.find( {category: "News"} )
```

Both find methods accept a second parameter called `projection`. This parameter is optional. If omitted, all fields will be included in the results.

This parameter is an `object` that describes which fields to include in the results.

```jsx
db.posts.find({}, {title: 1, date: 1})

db.posts.find({}, {_id: 0, title: 1, date: 1})
```

We use a `1` to include a field and `0` to exclude a field.

**Note:** You cannot use both 0 and 1 in the same object. The only exception is the `_id` field. You should either specify the fields you would like to include or the fields you would like to exclude.

Tuy nhiên, nếu bạn muốn lấy tất cả trường ngoại trừ một hoặc một số trường cụ thể, bạn cần chỉ định tất cả các trường bạn muốn lấy và đặt giá trị của chúng thành **`1`**, và không đặt giá trị của trường bạn muốn loại bỏ thành **`0`**.

Ví dụ:

- Lấy tất cả trường ngoại trừ trường "date":

```jsx
db.posts.find({}, { date: 0 })
```

# Update

To update an existing document we can use the `updateOne()` or `updateMany()` methods.

The `updateOne()` method will update the first document that is found matching the provided query.

- Insert a new one

```jsx
//Let's see what the "like" count for the post with the title of "Post Title 1"
db.posts.find( { title: "Post Title 1" } )

//Now let's update the "likes" on this post to 2. To do this, we need to use the $set operator
db.posts.updateOne( { title: "Post Title 1" }, { $set: { likes: 2 } } )

// Check the document again and you'll see that the "like" have been updated
db.posts.find( { title: "Post Title 1" } )
```

- Insert if not found. If you would like to insert the document if it is not found, you can use the `upsert` option.

```jsx
db.posts.updateOne( 
  { title: "Post Title 5" }, 
  {
    $set: 
      {
        title: "Post Title 5",
        body: "Body of post.",
        category: "Event",
        likes: 5,
        tags: ["news", "events"],
        date: Date()
      }
  }, 
  { upsert: true }
)
```

The `updateMany()` method will update all documents that match the provided query.

```jsx
//Update likes on all documents by 1. For this we will use the $inc (increment) operator:

db.posts.updateMany({}, { $inc: { likes: 1 } })
```

update key of mongo db when ccategory is typing wrong

{
_id: ObjectId("65392d507093da4a9dbea19f"),
title: 'Post Title 1',
body: 'Body of post',
ccategory: 'News',
likes: 3
},

```jsx
db.collectionName.update( { _id: 1 }, { $rename: { 'brand': 'brands'} } )
```

# Delete

We can delete documents by using the methods `deleteOne()` or `deleteMany()`.

The `deleteOne()` method will delete the first document that matches the query provided.

```jsx
db.posts.deleteOne({ title: "Post Title 5" })
```

The `deleteMany()` method will delete all documents that match the query provided.

```jsx
db.posts.deleteMany({ category: "Technology" })
```

Remove field from document:

Try `$unset` in a call to `update()`

```jsx
db.collection_name.update({ _id: 1234 }, { $unset : { description : 1} })
```

f you want to remove one field from all (or multiple) documents you can use `updateMany()` like this:

```jsx
db.collection_name.updateMany({}, { $unset : { description : 1} })
```

Or `remove`

```jsx
db['name1.name2.name3.Properties'].remove([ { "key" : "name_key1" }, { "key" : "name_key2" }, { "key" : "name_key3" } )]
```