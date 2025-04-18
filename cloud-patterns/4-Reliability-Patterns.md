# 1. The Saga Pattern
https://github.com/maulikdave-fh/notes/blob/main/msa_eda/5-Event_Driven_Microservices_Design_Patterns.md#saga-pattern

# 2. Transactional Outbox Pattern
It addresses reliability concern for Event driven architecture. 

## Problem Statement
We have a service (example, User Service in Job Search App) that needs to update its database and also publish an event to trigger the next operation in another service. 
![Transactional Outbox Pattern!](images/top1.png)

```
   void addUser(User user) [
        Connection connection = db.connect();
        // Following 2 are non-atomic operation. And there is no concept of Transaction between
        // a database and a message broker
        connection.insert(user, "UsersTable");
        // What if service crashes here, before sending a message to the message broker?
        messageBroker.send(new NewUser(user,...));
   }
```

## Solution
Inside our database, we add another table, say Outbox table. Instead of sending an event to message broker, we write a message to this Outbox table by clubbing it together as a database transaction along with user insert.

![Transactional Outbox Pattern!](images/top2.png)

Additionally, we add another service, Message Relay Service (MRS). This service monitors the Outbox table for updates. As soon as new message appears in the table, it takes it and sends it to the message broker. Then is marks the message as SENT or simply deletes it.
![Transactional Outbox Pattern!](images/top3.png)

## Issues & Considerations
1. Possibility of Duplicate Events
What if the MRS crashed immediately after sending a message to the message broker? The message in the Outbox table will be read again when MRS instance comes back / other MRS instance reads the message from the Outbox table. 

Use At-least once pattern - i.e.; MRS puts a message at least once in the queue. If the consumer services have idempotent operations, we don't need any special handling. Otherwise, following considerations are needed;
- use message Id for each message in the Outbox table, so consumer services can ignore message(s) that were already processed
![Transactional Outbox Pattern!](images/top4.png)

2. What if our microservices uses database (say NoSQL DB) that doesn't have Transaction support? 
Solved by adding fields to the original database document - this is an atomic operation. 
Add outbox attribute to the object;
```
    {
        user_id : "...."
        user_name : "...."
        user_email: "....'
        outbox: [...]
    }
```
MRS can periodically run a query to check if "outbox" attribute is present in any of the user's document
![Transactional Outbox Pattern!](images/top5.png)

3. Ordering of Events
To maintain sequence of delivery by MRS to the message broker, put sequence counter for each entry in the Outbox table

4. MRS demonstrates Side-car pattern. MRS runs on the same host as a service.

5. Technology like Debezium can be used by MRS to watch changes in the outbox table. More about Debezium;
**Debezium**
Streams changes from your database.

Debezium is an open source distributed platform for change data capture (CDC). Start it up, point it at your databases, 
and your apps can start responding to all of the inserts, updates, and deletes that other apps commit to your databases. 
Debezium is durable and fast, so your apps can respond quickly and never miss an event, even when things go wrong. 


# 3. Event Sourcing Pattern
https://github.com/maulikdave-fh/notes/blob/main/msa_eda/5-Event_Driven_Microservices_Design_Patterns.md#event-sourcing-pattern
