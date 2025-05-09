## Definition
The Software Architecture of a system is a high-level description of the system's structure, its different components, and how those components communicate with each other to fulfill the systems' requirements and constraints.

### Explanations
- An abstraction that shows us the important components while hiding the implementation details - allows us to reason about our system.
- Technologies or programming languages are not part of the software architecture but a part of the implementation. Decisions about implementation should be delayed to the very end of the design
- The components here are "black box" elements defined by their behavior and APIs. The components may themselves be complex systems with their own software architecture diagrams
- Components come together to do what the system mush do, which are our requirements. 
- The system doesn't not do what is shouldn't do, which are the constraints

## Level of Abstractions
Software architecture can have many different levels of abstractions:
1. Classes
2. Modules / Packages / Libraries
3. Services (processes / groups of processes)

## Architectural Drivers
Following 3 types of requirements drive architectural decisions;
1. Features of the system
- Functional Requirements
2. Quality Attributes
- Non-functional requirements
3. System Constraints
- Limitations and boundaries

### Functional Requirements
#### Steps Involves
1. Identify all the users and the actors
2. Gathering all the use cases
3. Expanding each use case with flow of interactions between the actors in our system

### Quality Requirements
1. **Systems are frequently redesigned NOT because of functional requriments**
But because the system as it stands
- isn't fast enough
- doesn't scale
- slow to develop
- hard to maintain
- not secure enough
2. Quality requirements provide a quality measure on how well our system performs on a particular dimension.They have a direct correlation with the architecture of our system

#### Considerations
##### Testability and Measurability
Quality attributes need to be measurable and testable

##### Trade-offs
No single software architecture can provide all the quality attributes because 
- certain quality attributes contradict with each other.
- some combinations of quality attributes are very hard / impossible to achieve
**We need to make the right trade-offs**

##### Feasibility
To make sure we can deliver on what we promise

### System Constraints
A system constraint is essentially a decision that was already either fully or partially made for us, restricting our degrees of freedom. 

System constraints are referred as pillars for software architecture because;
- they provide us us a solid starting point
- The rest of the system need to be designed around them

#### Types of Constraints
1. Technical Constraints - programming language / frameworks / cloud vendor / hardware / database technology / etc
2. Business Constraints
- Limited budget or a strict deadline will force us to make very different architectural choices
- Usage of third party APIs based on our business engagements
3. Legal / Regulatory Constraints - HIPAA / GDPR / PCI-DSS / COPPA / etc
