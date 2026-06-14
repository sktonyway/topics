# Cursor 

## Sorting and Limiting 

In mongodb, cursor is the result set of a query.
\
For Example: `find()` method return a cursor and finds the pointer which match them
\
Cursor methods can be chained to queries and can perform specific actions on the result set
- Use `cursor.sort()` to return query results in a specified order. Within the parentheses of `sort()`, include an object that specifies the field(s) to sort by and the order of the sort. Use *1 for ascending order*, and *-1 for descending order*.

Syntax: 
`db.collection.find(<query>).sort(<sort>)`

```js
// all music companies sorted in ascending order
// _id is sorted for consistency 
db.companies.find({ category_code: "music" }).sort({ name: 1, _id: 1 });
```
- Use `cursor.limit()` to specify the maximum number of documents the cursor will return. Within the parentheses of `limit()`, specify the maximum number of documents to return.

Syntax: 
`db.companies.find(<query>).limit(<number>)`
```js
// Top three music companies based on no. of employees
db.companies
  .find({ category_code: "music" })
  .sort({ number_of_employees: -1, _id: 1 })
  .limit(3);
```

## Projection

Sometimes we want only some fields from document or limit number of fields in document for reduction of bandwidth cost.
\
We can either use inclusion or exclusion of fields from document. 
\
Syntax: `db.collection.find( <query>, <projection> )`
```js
// Return all restaurant inspections - business name, result, and _id fields only
db.inspections.find(
  { sector: "Restaurant - 818" },
  { business_name: 1, result: 1 }
)
```
```js
// Return all inspections with result of "Pass" or "Warning" - exclude date and zip code
db.inspections.find(
  { result: { $in: ["Pass", "Warning"] } },
  { date: 0, "address.zip": 0 }
)
```
