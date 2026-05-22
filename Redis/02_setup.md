# Redis Setup
Instead of getting connection string from database connection string, we can use string of docker
\
We can write services like redis, mongodb and postgres
\
```js
const express = require('express');
const Redis = require('ioredis'); // Assuming ioredis client
const mongoose = require('mongoose');

const app = express();
const redis = new Redis(process.env.REDIS_URL);

app.get('/redis', async (req, res) => {
    try {
        const reply = await redis.ping(); // Added await to get "PONG"
        res.send(`Redis Status: ${reply}`);
    } catch (error) {
        res.status(500).send(`Redis Error: ${error.message}`);
    }
});

app.get('/mongoose', async (req, res) => {
    try {
        // Checks the operational state of the Mongoose connection
        // 1 = connected, 0 = disconnected, 2 = connecting
        const dbStatus = mongoose.connection.readyState;
        
        if (dbStatus === 1) {
            res.send("Mongoose Status: Connected to MongoDB");
        } else {
            res.status(500).send("Mongoose Status: Disconnected");
        }
    } catch (error) {
        res.status(500).send(`Mongoose Error: ${error.message}`);
    }
});


```