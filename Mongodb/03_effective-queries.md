# Effective Queries

In real world, we have to use various parameters for taking a decision, which involve logical thinking and much more.
\
To tackle those queries, mongodb has various methods. Here some are common mentioned.

## Comparison Operators
To use a comparison operator, we use `<field>: { <operator> : <value> }`
- `$gt`: It returns documents where specified field value is greater than given value
- `$lt`: less than
- `$eq`: equals to 
- `$lte`: less than or equals to 
- `$gte`: greater than or equals to 
```js
// returns every objects matching conditions
db.sales.find({ "items.price": { $gt: 50}})
db.sales.find({ "items.price": { $lt: 50}})
db.sales.find({ "customer.age": { $lte: 65}})
```

## Logical Operators
- Use implicit `$and` to select documents that match multiple expressions.
- Use the `$or` operator to select documents that match at least one of the included expressions. 
```js
db.routes.find({
  $and: [
    { $or: [{ dst_airport: "SEA" }, { src_airport: "SEA" }] },
    { $or: [{ "airline.name": "American Airlines" }, { airplane: 320 }] },
  ]
})
```

## Querying on array elements 
Use the `$elemMatch` operator to find all documents that contain the specified subdocument.
```js
{
  "_id": 1,
  "results": [
    { "product": "abc", "score": 10 },
    { "product": "xyz", "score": 70 }
  ]
}

db.students.find({ results: { $elemMatch: { product: "abc", score: { $gt: 50 } } } })
```

#### Note: 
Combining these methods can be used for complex decisions.