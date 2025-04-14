Just breaking a large application into an arbitrary set of microservices won't give us any benefit.

Defining correct boundaries for the microservies is important so the system doesn't turn into a Big Ball of Mud.

# Boundaries of Microservices
## Common mistakes
1. Splitting by Application layers - separate microservices for presentation layer, business-logic layer, infrastructure layer
Every new feature will need change in all 3 microservices requiring careful planning and release coordination between different teams. No organization scalability. Breaking 3 tier app into more tiers won't work.
![Mistake 1!](images/mistake_tiers.png)

2. Splitting by Technology boundaries - while this may bring in some performance benefits, outside stakeholders (product managers, etc) won't know which subsystem / team / service gets new task. Naming terminology of each API will be too convoluted. Also, business logic layer microservice is still too big and has a potential to become yet another monolith.

![Mistake 2!](images/mistake_tech.png)

3. Splitting for Minimum size - we looked at "micro" in microservices and assumed that splitting the monolithic app into tiny services would give us the best benefits - smaller the better. Splitting by package / class is a common mistake.

![Mistake 3!](images/mistake_size.png)


## Core Principles
Each core principle below is related to common mistakes above, respectively
1. High Cohesion: Elements that are tightly related to each other and change together, should stay together. Allows each team to operate independently. 
2. Single Responsibility Principle: Each microservice should do only one thing and do it exceptionally well. No ambiguity about where new functionality should go and which team owns what. Easy to follow API for each microservice because all terminology (entities, identifiers, etc) are bound to a given context
3. Loosely coupled - Little / no inter-dependency - minimum communication with other microservices. 


