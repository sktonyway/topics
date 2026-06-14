# CRUD applications
#### Note
All these are direct shell commands

## Inserting Documents in mongodb collection [Create]
Suppose we want to insert one element in mongodb collection, we use 
`db.<collection>.insertOne()` for inserting.

#### Note:
- If collection doesn't exists it is created automatically. So, check twice before inserting as it creates new collection for mismatched name.
- Document require `_id`, if not provided it creates one.

```js
db.users.insertOne({
    username:"something",
    email: "abc@pqr.com",
    pass:"1234"
})

returns insertedId
```

Similarly we can insert many elements in one go, we use `db.<collection>.insertMany()`.

```js
db.users.insertMany({
    username:"something",
    email: "abc@pqr.com",
    pass:"1234"
}, {
    username:"something2",
    email:"abc@abc.com",
    pass:"1234"
    }
)

returns insertedId
```

## Finding Document/s in collection [Read]
For searching through documents, we use 
`db.<collection>.find()` and in shell we type `it` to iterate or show more.

- `{ field: { $eq: <value> } }` or `{ field: <value> }` to find field with associated values.
- `{ <field>: { $in: [<value>, <value>, ] } }` to find documents containing either of values
```js
//To find all users whose role is either "Admin" or "Moderator":
db.users.find({ role: { $in: ["Admin", "Moderator"] } })

// To find single element equivalent to 
db.books.findOne({title: {$eq: "Brave New World"}})
```

## Updating Document/s [Update]

`db.<collection>.updateOne(<filter>, <update>, {options})` is used for updating a single document.
- `$set` operator adds new fields and values to to a document or replaces the value with given value.
- `$push` operator appends a value to array or create array field with given value (if absent)
```js
db.orders.updateOne(
   { userId: 12345 },
   { $set: { status: "Shipped" } }
)
// or 
db.podcasts.updateOne(
  { _id: ObjectId("5e8f8f8f8f8f8f8f8f8f8f8") },
  { $push: { hosts: "Nic Raboy" } }
)
```

#### Note: 
upsert is used to insert document with details provided, if not matched with any document.

**UpdateMany**
- It is not all or none method i.e, If it is unable to match or triggered any other issues in the middle of update, it may stop in the middle causing partial update and doesn't roll back updates.
```js
// Every book doc status will be legacy, published before 2019
db.books.updateMany(
  { publishedDate: { $lt: new Date("2019-01-01") } },
  { $set: { status: "LEGACY" } }
)
```

## Deletion of Document/s [Delete]

To delete documents, use the `deleteOne()` or `deleteMany()` methods. Both methods accept a filter document and an options object.


```js
db.podcasts.deleteOne({ _id: Objectid("6282c9862acb966e76bbf20a") })
db.podcasts.deleteMany({category: “crime”})
```