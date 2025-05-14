## REST
REpresentational State Transfer (REST) - a set of architectural constraints and best practices for defining APIs for the web

It is not a standard or a protocol - it is an architectural style for designing APIs that are easy for our clients to use and understand

**An API that obeys the REST architectural constraints is called a RESTful API**

### RPC vs REST API
1. RPC is service / method oriented and REST is resource oriented
2. REST API is dynamic in nature using HATEOAS - in RPC, operations defined in IDL can only be called. In RESTful APIs, this interface is a lot more dynamic through **Hypermedia As The Engine Of the Application State**. This is achieved by accompanying a state representation response to the client with hypermedia links

![REST!](images.rest1.png)

### RESTful API Quality Attributes
#### 1. Statelessness
1. The server is stateless
2. This helps us achieve high scalability and availability

#### 2. Cacheability
1. The server has to either explicitly / implicitly define each response as either
- Cacheable
- Non-cacheable

### Resources
The hierarchy of resources is represented as "/"
#### 1. Simple Resource
1. Has state
2. Can contain one or more sub-resources

#### 2. Collection Resource
1. Contains a list of resources of the same-type

![REST!](images.rest2.png)

![REST!](images.rest3.png)

![REST!](images.rest4.png)

The representation of each resource state can be expressed in a variety of ways such as;
Image, A link to a movie stream, An object, An HTML page, Binary blob, Executable code like Javascript


### Best Practices
1. Naming resources using nouns
2. Making distinction between collection resources and simple resources
- plural names for collections
- singular names for single resource
3. Giving our resources clear and meaningful names
4. Resource identifiers should be unique and URL friendly

### REST operations
Tied to HTTP methods
1. GET method is considered safe - applying to resource won't change its state
2. GET, PUT, DELETE methods are idenpotent
3. GET requests are usually considered cacheable by default
4. Responses to POST requests can be made cacheable by sending appropriate HTTP header in the response
