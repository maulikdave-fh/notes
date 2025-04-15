# Saga Pattern
## Problem Statement
In microservices architecture, we have a database per microservice. It means, we can't have ACID support for transactions spanning across multiple microservices

**Transaction** - to an external observer, a sequence of operations appears as a single operation.
This is referred as ACID guarantee - Atomicity, Consistency, Isolation, Durability

## The Pattern
Saga pattern gives transaction support across microservices using compensating txns to rollback previous transaction in case of a failure.
![Saga pattern!](images/saga1.png)

![Saga pattern!](images/saga2.png)

## Two ways to Implement
### Workflow Orchestration  
Based on request-response model where workflow orchestration service manages the state of each transaction. If anything goes wrong, it will fire compensating transaction requests to appropriate services.

Here, orchestration service is tightly coupled with all the involved microservices. 

### Event-Driven Model
Here, we remove the workflow orchestration service and delegate a task of managing the workflow to microservices themselves. The communication between involved microservices is done using message broker. Each microservice needs to be aware where it needs to send events when successful and failure scenarios to trigger the compensating ops. 

## Additional Notes
1. If I want stronger reliability:
- Outbox Table + Debezium (CDC) → Reliable and fast (near real-time).
- Kafka Transactions → Guarantees atomicity (DB & Kafka commit together).
2. If I want lower latency:
- Kafka Exactly-Once Processing → Reduces the need for outbox polling and de-duplication.
- Idempotent Kafka Producer → Speeds up event publishing.

# CQRS Pattern
## Introduction
- CQRS - Command and Query Responsibility Segregation
- Used in improving database communication performance
- Command - action that results in data change - Write / Update / Delete
- Query - only data read, no data change. Data can be returned as-is or after transformation (sorting / aggregation)

Segregate data & the service into 2 parts - one for Command & other for Query
![CQRS!](image/cqrs1.png)

To keep data in sync between command and query database, we use event-driven model.
![CQRS!](image/cqrs2.png)

## Benefits
Due to Separation of Concerns, we get following benefits;
1. SRP
- We can evolve each part independently using an optimal data model in our programming langauge for each workload 
2. High Performance  
- We can use optimal schema, structure and database technology for command and query database.
- Typically, RDBMS is used for write DB. And NoSQL is used for read DB for its performance benefits.
3. High Scalability
- We can adjust number of instances for each microservice & database instances depending on its traffic
4. Joining data from different microservices
![CQRS!](image/cqrs3.png)

## Additional Notes
- Since CQRS only guarantees eventual consistency, it may not be a right choice for certain financial use cases. E.g.; Show balance.

# Event Sourcing Pattern
