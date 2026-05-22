# Redis
### In-memory database
- It has a feature to save persistent data
- It serves from RAM 
- Redis acts as a server
- Database can be managed using this
- Data is stored in key-value pairs

Note
- User uses request, response as per usual backend search with database and send the data.
- with Redis in between server and database, it cache the request and serves data directly, in case of cache hit else serve it from backend and cache it.
- Now, we can reduce the load on database of reading data or hot data read requests

### Patterns
- We can add redis server directly in server.

|  | Pros | Cons |
| -------- | -------- | -------- |
| Inside server  | Zero network latency  | Resource contention  |
|   |Lower cost  | Crashes, in case of memory leaks  |
|   |Simpler Setup | No independent scaling  |

- We can cache along with sessionStorage of active users, so that inactive users can be kept out of memory.
- 

### UseCases
- Rate Limiting
- OTPs
- Queues like Emails
- setting TTLs

Note:
- Drop-In alternatives are just same as redis where we can just update env and work seamlessly