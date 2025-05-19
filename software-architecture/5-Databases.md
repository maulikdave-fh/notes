## RDBMS
### Advantages
1. Ability to form complex and flexible queries
2. Efficient storage due to normalization  and joins
3. Easy to reason about because it represents a natural structure of data for humans
4. ACID transaction guarantees

### Disadvantages
1. Rigid structure enforced by table's schema
- the schema has to be defined ahead of time before we can use the table
- if we want to change the schema (add/remove column), we would have some maintenance time
2. Hard to maintain / scale
3. Slower read operations

### When to choose RDBMS?
1. Perform complex and flexible queries to analyze our data
2. Guarantee ACID transactions between different entities in our database

### When not to choose RDBMS?
1. There isn't any inherent relationship between different records that justifies storing our data in tables
2. Read performance is the most important quality that we need for providing good UX

## Non-Relational DB (NoSQL DB)
1. Allows logical grouping
- they allow to logically group a set of records without forcing all of them to have the same structure
2. Supports programming language friendly data structures
- most programming langauges don't have table as a data structure
- eliminates the need for an ORM
3. Designed for faster queries

### Trade-offs
1. When we allow flexible schemas we lose the ability to easily analyze those records
2. Analyzing multiple groups of records (join operations) also becomes hard
3. ACID transactions are rarely supported by NoSQL databases

### Categories of NoSQL DBs
#### Key/Value Store
1. Like a large-scale hashtable or dictionary
2. It has a very few constraints on the type of values we have for each key

**Use cases**
1. Counters that multiple service instances can read and increment
2. Caching pages or data

#### Document Store
1. We can store collections of documents, with more structure inside each document
2. Each document is an object with different attributes - those attributes can be of different types
3. Documents inside a document store are easily mapped to objects inside a programming language

**Examples of Documents**
- JSON object representing a movie
- YAML configuration representing some business logic
- XML representing a form submitted by a user

#### Graph DB
1. Extension of a document store with additional capabilities to
- link
- traverse
- analyze
multiple records more efficiently 
2. Optimized for navigating and analyzing relationships between different records

**Use cases**
1. Fraud detection
- Multiple logical users identified as same person trying to initiate multiple transactions using same email/computer
2. Recommendation Engines
- recommend new products to users based on past purchase history or friends of the user

### When to choose Non-Relational DB?
- Perfect choice for caching due to faster queries - in-memory key-value DBs are particularly optimized for this
- Handling real-time big data - Document Store
- When data is unstructured - different records can contain different attributes - Document store. Examples; User Profiles, Content Mgmt where we have different type of user generated content - images / videos / etc

### Non-Relational DBs - Solutions
#### Key/Value Stores Examples
1. Redis
2. Aerospike
3. Amazon DynamoDB

#### Document Store Examples
1. Cassandra
2. MongoDB

#### Graph Databases Examples
1. Amazon Neptune
2. NEO4J



