# Introduction
## Types of System Requirements;
1. Functional - dictates the functionality / features of the product
> Unique to the product - functionality, business logic, UX

2. <mark>Non-functional (Quality Attributes) - performance, scalability, reliability, availability, security, organizational scalability > Common challenges -> common solutions -> common architectural patterns</mark>

3. System constraints - Subset of technologies, APIs, Existing systems - it limits our design choices

## <mark>Architectural Patterns
- Universal solutions to common design problems
- Successfully used by many companies
- Implementation Independent</mark>

## Design Patterns (GoF) vs Architectural patterns
Design Patterns are targeted towards standalone applications implemented with OOP languages.

### Design Patterns benefits;
- Better code organization
- Code Re-usability
- Code Extensibility
- Higher developer productivity

### <mark>Design Patterns are NOT very helpful in architecting;</mark>
1. Large Scale System
2. Using multiple independently deployable services
3. Implemented in different languages (some may not be Object Oriented)
4. Design Patterns don't address 
- Performance
- User Experience
- Error Handling
- Processing big data or high network traffic

## Cloud Computing Pattern
A general solution to a problem that many companies were dealing with.
### Benefits
1. Instant Access to (virtually) infinite 
- Computing
- Storage
- Network
called IaaS - no need to hire specialists and spend months on setting up an infra. 
2. Quick go-to-market - no-entry level barrier, especially for startups
3. Pay for what you use
4. Large set of tools & features to improve performance, availability and scalability
5. Multi-region and multi-zone deployments - closer to user - lower latency, better use experience
6. Multi-zone (isolation zones) - high availability & reliability as each zones utilize its own power, network and cooling services

#### Infra components (IaaS)
- Virtual Machines
- Network Routers
- Switches
- Storage devices

#### Platform services (PaaS)
- Databases
- Message Brokers
- Load Balancers
- Monitoring
- Logging services
- FaaS / Server-less deployment

### Cloud computing limitations;
- More we scale, costlier it gets <mark>As software architect, apart from NFRs, we also have to manage cost efficiency & profitability</mark>
- Infra is out of our direct control
- Not the most high end hardware
- Not the newest hardware - can fail anytime
