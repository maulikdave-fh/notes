## API
The interface is a contract between;
1. Engineers who implement the system
2. Client applications that use the system

## API Categories
### Public APIs
1. Exposed to the general public - any developer can use / call them from their app
2. Good practice - requiring the users to register with us before allowing to send requests and use the system. This allows better control over;
- who uses the system externally
- how they use the system
- better security
- blacklist users that break rules

### Private / Internal APIs
1. Exposed internally within the company

### Partnet APIs
1. Similar to public APIs, but exposed to companies /users having business relationship with us

## Benefits of APIs
1. Client who uses it can immediately and easily enhance their business by using our system without knowing anything about our system's internal design / implementation 
2. Once we define and expose our API, clients can integrate with us without waiting for full implementation of our system
3. API makes it easier to design and architect the internal structure of our system

## API Best Practices & Patterns
### 1. Complete Encapsulation
1. Complete encapsulation of the internal design and implementation - abstracting it away from a developer wanting to use our system
2. API should be completely decoupled from our internal design and implementation - so that we can change the design later without breaking the contract with our clients


### 2. Easy of Use
1. Easy to use / simple
- only one way to get certain data /perform a task
- descriptive names for actions and resources
- exposing only the information and actions that users need
- keeping things consistent all across our API
2. Easy to understand
3. Impossible to misuse

### 3. Keeping the Operations Idempotent
1. Idempotent operations are preferred for our API as they are going to be used through the network. If a client application sends us a message;
- the message can be lost
- the response to that message may be lost
- the message wasn't received as a critical component in our system went down
Because of network decoupling, the client app has no idea which scenario actually happened. If the operation is idempotent, the client can simply resend the same message again without any consequences

### 4. API Pagination
1. Important when a response from our system to the client request contains a very large payload or dataset
2. Without pagination most client applications will;
- not be able to handle big responses
- result in a poor UX
3. Pagination allows the client
- to request only a small segment of the response
- specify the maximum size of each response from our system
- specify an offset within the overall dataset
To receive the next segment, we increment the offset

### 5. Asynchronous Operations
1. Some operations need one big result at the end and there is nothing meaningful that we can provide before the entire operation finishes. Examples;
- running a large report requiring our system to talk to many databases
- big data analysis that scans a lot of records/log files
- compression of large video files
2. If the operation takes a long time, the client app has to wait for the result. 
3. With Async API, a client receives a response immediately without having to wait for the final result. The response typically includes some kind of identifier that allows client to;
- track the progress and status of the operation
- receive the final result when ready

### 6. Versioning our APIs
1. Best API design allows us to make changes to the internal design and implementation without changing the API. But in practice, we may need to make non-backward compatible API changes
2. If we explicitly version the APIs we can;
- maintain **two** version of the APIs at the same time
- deprecate the older one gradually
