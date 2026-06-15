# Drivers

Drivers are useful for enabling capablities in different programming languages

In node js, we can use `mongodb`
\
we use mongoclient to 


- An application should use single mongoclient for all db requests
- creating mongoclient is resource intensive
- 

<details>
<summary>
Basic <b>mongoclient</b> setup
</summary>

```js
// Require MongoDB language driver
const { MongoClient } = require("mongodb")

// Set the value of uri to your Atlas connection string.
const uri = 'mongodb+srv://myAtlasDBUser:myatlas-00yg1@myatlasclusteredu.jeoh6rw.mongodb.net'

// Create the MongoClient instance
const client = new MongoClient(uri)

// Establishes a connection to the database using the MongoClient instance
const main = async () => {
   try {
      await client.connect()
      console.log("Connected to MongoDB Atlas!")
      // list out all the databases in the cluster
      const dbs = await client.db().admin().listDatabases()
      console.table(dbs.databases)
   } catch (error) {
      console.error(error)
   } finally {
      await client.close()
   }
}

// Run the main function, catch any errors and finally close the connection when the main function is done
main()
   .catch((err) => console.log(err))
   .finally(() => client.close())
```

</details>

# Connection using Shell
MongoDB uses two formats for connection strings:
- Standard format `mongodb://`
- SRV format `mongodb+srv://` [default for atlas]

SRV format secures connection using TLS and simplify the connection by providing a list of hosts 
\
MongoDB driver perform a dns lookup to retrieve the srv record using domain name specified with `@`
\
The srv record list the collection name of nodes while related text records provide additional collection options for client


#### Note
- mongosh [powerful shell provided by mongodb] is included with certain MongoDB server edition
- mongsh can be used to manage databases


```bash
mongosh <string_url> --apiVersion 1 --username user2
# to connect atlas db
```  

```bash
db # logs current db
use notes # to enter notes db
```  
## Js in Shell
We can even integrate javascript directly using shell or with loading a separate js file
```js
// within shell
const randomMovie = () =>
  db.movies.aggregate([{ $sample: { size: 1 } }]).toArray();
randomMovie()
```

#### Note
- We can use editors within shell for bigger queries 
- `config.set("editor", "nano")`
- `edit`
```js
db.transactions.updateOne(
  { account_id: 000000 }, // UPDATE THIS!
  {
    $push: {
      transactions: {
        date: new Date(),
        amount: Math.floor(Math.random() * 1000),
        transaction_code: Math.random() < 0.5 ? "buy" : "sell",
        symbol: "test",
        price: "100.00",
        total: "1337.10",
      },
    },
  }
);
```

Rest can can be seen [here CRUD](/02_CRUD.md)