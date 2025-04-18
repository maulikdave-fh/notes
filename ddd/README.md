# Domain
A sphere of knowledge, influence, or activity - A field | industry in which the business operate - For example; Banking, Oil & Gas, Retail, etc.
1. Made up of mulitple sub-domains. For example; Banking domain has Loans Accounts, Retail Accounts and Merchant Accounts
2. Typically, SME / domain expert is aligned with a sub-domain - No one expert knows everything about the domain.

# What DDD is for?
1. Complex domains
2. Difficult communication between domain experts and technical people
3. Muddled concepts

It has 2 portions;
## Strategic Design 
1. Establish boundaries, isolating different designs through <b>strategic design pattern</b> called, <b><i>Bounded Contexts</i></b>
2. Focus design efforts on most valuable parts - Core and supporting subdomains
3. Integrate multiple bounded contexts using a technique called <b><i>Context mapping</i></b>.

## Tactical Design
1. Collaborative exploration of models using <b><i>Aggregate Pattern</i></b>
2. Emphasis on language of design

# Models
<s>UML Class Diagrams</s><br>
<s>A Layer of Software</s>

## Definition of Model
Domain is a Sphere of knowledge or activity. A model is a system of abstractions representing selected aspects of a domain. The goal of the modeling is to traverse through a complex domain and represent the domain in abstract and simpler (understandable) form.

Models are central to DDD, but the word ‘model’ means many things, so we need to be specific. The sense of the word we apply in DDD is a basic and old one, not specifically tied to software: We simply say a model is a system of abstractions. It is a set of concepts that we can use to reason about a domain. It is a distillation of our knowledge about a specific domain - addresses a subset of information about the domain. It excludes information that is not particularly relevant to the problem at hand - allows us to focus on and simplify the problem. Models are specialized, not general - specific solution to a specific type of problems. Models are artificial. Models evolve.

During modeling sessions, try to come up with multiple ideas. If all the ideas are good, may be you are not doing it right. Choose a model that's suited to the purpose at hand.
   
# What is Domain Driven Design?
DDD tries to combine following 2 ideas;
1. Technical Design perspective
2. The language and collaboration perspective - this is about collaborating / engaging with a domain expert, without bringing in technical jargon into the discussion, and developing a model that a developer and domain expert both can reason about, without compromising on software design practices.

It is a tool for us to talk to business folks about the design in a language that business folks can understand.

According to Eric Evans, a domain model is not a particular diagram; it is the idea that the diagram is intended to convey. It is not just the knowledge in a domain expert’s head; it is a rigorously organized and selective abstraction of that knowledge. A diagram can represent and communicate a model, as can carefully written code, as can an English sentence.

In short, DDD is primarily about modeling a <i>Ubiquitous Language</i> in an explicitly <i>Bounded Context</i>.

# Strategic Design
## Ubiquitous Language
A language structured around the domain model and used by all team members to connect all the activities of the team with the software. It is specific to a project / subsystem that we are working on. Outside of the subsystem, for another subsystem, there may be a different language. I.e.; the language is contextual.

Ubiquitous language is used within a bounded context.

Domain Experts, is not a job title but rather describes those who are primarily focused on the business. It’s their mental model that we start with to form the
foundation of the team’s Ubiquitous Language. Both developers and Domain Experts should reject any tendency to allow documents to rule over conversation. The best Ubiquitous Language will be developed by a collaborative feedback loop that drives out the combined mental model of the team. Open conversation, exploration, and
challenges to your current knowledge base result in deeper insights about the Core Domain.

A core principle of domain-driven design is to use a language based on the model. Since the model is the common ground, the place where the software meets the domain, it is appropriate to use it as the building ground for this language.

Use the model as the backbone of a language. Request that the team use the language consistently in all communications, and also in the code. While sharing knowledge and hammering out the model, the team uses speech, writing and diagrams. Make sure this language appears consistently in all the communication
forms used by the team; for this reason, the language is called the Ubiquitous Language.

The Ubiquitous Language connects all the parts of the design, and creates the premise for the design team to function well. It takes weeks and even months for large scale project designs to take shape. The team members discover that some of the initial concepts were incorrect or inappropriately used, or they discover new elements of the design which need to be considered and fit into the overall design. All this is not possible without a common language.

Languages do not appear overnight. It takes hard work and a lot of focus to make sure that the key elements of the language are brought to light. We need to find those key concepts which define the domain and the design, and find corresponding words for them, and start using them. Some of them are easily spotted, but some are harder. 

Building a language like that has a clear outcome: the model and the language are strongly interconnected with one another. A change in the language should become a change to the model.

If domain experts cannot understand something in the model or the language, then it is most likely that there is something is wrong with it. On the other hand, developers should watch for ambiguity or inconsistency that will tend to appear in design.

It is also highly recommended for the developers to implement the main concepts of the model in the code. By creating classes for the corresponding model concepts,
we are mapping between the model and the code, and between the language and the code. This is very helpful as it makes the code more readable, and makes it reproduce the model. Having the code express the model pays off later in the project, when the model grows large, and when changes in the code can have undesirable consequences if the code was not properly designed.

## Bounded Context
A <b><i>Bounded Context</b></i> is a semantic contextual boundary. This means that within the boundary each component of the software model has a specific meaning and does specific things. The components inside a Bounded Context are context specific and semantically motivated. 

When you are just getting started in your software modeling efforts, your Bounded Context is somewhat conceptual. You could think of it as part of your problem space. However, as your model starts to take on deeper meaning and clarity, your Bounded Context will quickly transition to your solution space , with your software model being reflected as project source code. 

Remember that a Bounded Context is where a model is implemented, and you will have separate software artifacts for each Bounded Context.

Your problem space is where you perform high-level strategic analysis and design steps within the constraints of a given project. You can use simple diagrams as you discuss the high-level project drivers and note important goals and risks. In practice, Context Maps work very well in the problem space. Note too that Bounded Contexts may be used in problem space discussions, when needed, but are also closely associated with your solution space.

Your solution space is where you actually implement the solution that your problem space discussions identify as your Core Domain. When the Bounded Context is being
developed as a key strategic initiative of your organization, it’s called the <b>Core Domain</b>. You develop your solution in the Bounded Context as code, both main source and test source. You will also produce code in your solution space that supports integration with other Bounded Contexts. 

When compared with all the software your organization uses, a Core Domain is a software model that ranks among the most important, because it is a means to achieve greatness. A Core Domain is developed to distinguish your organization competitively from all others. At the very least it addresses a major line of business. Your organization can’t excel at everything and shouldn’t even try. So you choose wisely what should be part of your Core Domain and what should not. This is the
primary value proposition of DDD, and you want to invest appropriately by committing your best resources to a Core Domain.

There should be one team assigned to work on one Bounded Context. There should also be a separate source code repository for each Bounded Context. It is possible that one team could work on multiple Bounded Contexts , but multiple teams should not work on a single Bounded Context. Cleanly separate the source code and database schema for each Bounded Context in the same way that you separate the Ubiquitous Language. Keep acceptance tests and unit tests together with the main source code.

## The Process
Usually there are long discussions between software architects or developers and the domain experts. The software specialists want to extract knowledge from the domain experts, and they also have to transform it into a useful form. At some point, they might want to create an early prototype to see how it works so far. While
doing that they may find some issues with their model, or their approach, and may want to change the model.

We, the software specialists (software architects and developers) and the domain experts, are creating the model of the domain together, and the model is the place where those two areas of expertise meet. This might seem like a very time consuming process, and it is, but this is how it should be, because in the end the software’s purpose is to solve business problems in a real life domain, so it has to blend perfectly with the domain.

The model should be constructed with an eye open to the software and design considerations. Developers should be included in the modeling process. The main idea is to choose a model which can be appropriately expressed in software, so that the design process is straightforward and based on the model. Tightly relating the code to an underlying model gives the code meaning and makes the model relevant.

Those who write the code should know the model very well, and should feel responsible for its integrity. They should realize that a change to the code implies a change to the model; otherwise they will refactor the code to the point where it no longer expresses the original model. If the analyst is separated from the
implementation process, he will soon lose his concern about the limitations introduced by development. The result is a model which is not practical.

Any technical person contributing to the model must spend some time touching the code, whatever primary role he or she plays on the project. Anyone responsible for changing code must learn to express a model through the code. Every developer must be involved in some level of discussion about the model and have contact with domain experts. Those who contribute in different ways must consciously engage those who touch the code in a dynamic exchange of model ideas through the Ubiquitous
Language.

## Technology-Free Domain Model
Although there will be technology scattered throughout your architecture, the domain model should be free of technology. For one thing, that’s why transactions are managed by the application services and not by the domain model.

Any domain can be expressed with many models, and any model can be expressed in various ways in code. For each particular problem there can be more than one solution. Which one do we choose? Having one analytically correct model does not mean the model can be directly expressed in code. Or maybe its implementation will break some software design principles, which is not advisable. It is important to choose a model which can be easily and accurately put into code.

## Most Optimal Modeling Composition
One Subdomain per Bounded Context , and one Bounded Context per Subdomain. 

In some situations, there may be multiple Subdomains in one Bounded Context , but that doesn’t achieve the most optimal modeling outcome.

## What is a Subdomain?
Simply stated, a Subdomain is a sub-part of your overall business domain. You can think of a Subdomain as representing a single, logical domain model. Most business domains are usually too large and complex to reason about as a whole, so we generally concern ourselves only with the Subdomains that we must use within a single project. Subdomains can be used to logically break up your whole business domain so that you can understand your problem space on a large, complex project.

Another way to think of a Subdomain is that it is a clear area of expertise, assuming that it is responsible for providing a solution to a core area of your business. This implies that the particular Subdomain will have one or more Domain Experts who understand very well the aspects of the business that a specific Subdomain facilitates. The Subdomain also has greater or lesser strategic significance to your business.

## Types of Subdomains
### Core Domain
This is where you are making a strategic investment in a single, well-defined domain model, committing significant resources for carefully crafting your Ubiquitous
Language in an explicit Bounded Context. This is very high on your organization’s list of projects because it will distinguish it from all competitors. Since your organization can’t be distinguished in everything that it does, your Core Domain demarcates where it must excel. Achieving the level of deep learning and understanding required to make such a determination requires commitment, collaboration, and experimentation. It’s where the organization needs to invest most liberally in software. 
1. Understand the core domain deeply. Creative Collaboration - domain experts and software practitioners. Ask why.
2. Go for the best model. Explore and iterate. 
3. Isolate the work in a clean, bounded context.Use Ubiquitious language
4. Assign your best designers - who are good at abstractions, good at design & good at collaborating with non-technical people.

Core Domain is where you thoroughly apply tactical level of DDD. 

### Supporting Subdomains
This is a modeling situation that calls for custom development, because an off-the-shelf solution doesn’t exist. However, you will still not make the kind of
investment that you have made for your Core Domain. You may want to consider outsourcing this kind of Bounded Context to avoid mistaking it for something strategically distinguishing, and thus investing heavily in it. This is still an important software model, because your Core Domain cannot be successful without it.

Possible can be outsourced, or can use your B string team to build it.

### Generic Subdomains
This kind of solution may be available for purchase off the shelf but may also be outsourced or even developed in house by a team that doesn’t have the kind of elite
developers that you assign to your Core Domain or even a lesser Supporting Subdomain.

The biggest cost of building generic subdomains in-house is the opportunity cost. Why tie-up your resources in building something that you can buy off-the-shelf?

## Context Mapping
When we talk about Context Mapping , what is of interest to us is what kind of inter-team relationship and integration is represented by the line between any two Bounded Contexts. Well-defined boundaries and contracts between them support controlled changes over time. There are several kinds of Context Mappings , both team and technical, that can be represented by the line. In some cases both an inter-team relationship and an integration mapping will be blended.

### Types of Mappings
#### Partnership
A Partnership relationship exists between two teams. Each team is responsible for one Bounded Context. They create a Partnership to align the two teams with a dependent set of goals. It is said that the two teams will succeed or fail together. Since they are so closely aligned, they will meet frequently to synchronize schedules and dependent work, and they will have to use continuous integration to keep their integration in harmony.

It can be challenging to maintain a Partnership over the long term, so many teams that enter a Partnership may do best to set limits on the term of the relationship. The Partnership should last only as long as it provides an advantage, and it should be remapped to a different relationship when the advantage is trumped by the drain of commitment.

#### Shared Kernel
A Shared Kernel describes the relationship between two (or more) teams that share a small but common model. The teams must agree on what model elements they are to share. It’s possible that only one of the teams will maintain the code, build, and test for what is shared. A Shared Kernel is often very difficult to conceive in the
first place, and difficult to maintain, because you must have open communication between teams and constant agreement on what constitutes the model to be shared.

#### Customer-Supplier
A Customer-Supplier describes a relationship between two Bounded Contexts and respective teams, where the Supplier is upstream and the Customer is downstream. The Supplier holds sway in this relationship because it must provide what the Customer needs. It’s up to the Customer to plan with the Supplier to meet various expectations, but in the end the Supplier determines what the Customer will get and when. This is a very typical and practical relationship between teams, even within the same organization, as long as corporate culture does not allow the Supplier to be completely autonomous and unresponsive to the real needs of Customers.

#### Conformist
A Conformist relationship exists when there are upstream and downstream teams, and the upstream team has no motivation to support the specific needs of the downstream team. For various reasons the downstream team cannot sustain an effort to translate the Ubiquitous Language of the upstream model to fit its specific needs, so the team conforms to the upstream model as is. A team will often become a Conformist , for example, when integrating with a very large and complex model that is well established. Example: Consider the need to conform to the Amazon.com model when integrating as one of Amazon’s affiliate sellers.

#### Anti-corruption Layer 
An Anti-corruption Layer is the most defensive Context Mapping relationship, where the downstream team creates a translation layer between its Ubiquitous Language (model) and the Ubiquitous Language (model) that is upstream to it. The layer isolates the downstream model from the upstream model and translates between the two. Thus, this is also an approach to integration.

Whenever possible, you should try to create an Anti-corruption Layer between your downstream model and an upstream integration model, so that you can produce model concepts on your side of the integration that specifically fit your business needs and that keep you completely isolated from foreign concepts. Yet, just like hiring a translator to act between two teams speaking different languages, the cost could be too high in various ways for some cases.

#### Open Host Service
An Open Host Service defines a protocol or interface that gives access to your Bounded Context as a set of services. The protocol is “open” so that all who need to integrate with your Bounded Context can use it with relative ease. The services offered by the application programming interface (API) are well documented and a pleasure to use. Even if you could not take time to create an isolating Anti-corruption Layer for your side of the integration, it would be much more tolerable to be a Conformist to this model than many legacy systems you may encounter. We might say that the language of the Open Host Service is much easier to consume than that of other types of systems.

#### Published Language
A Published Language is a well-documented information exchange language enabling simple consumption and translation by any number of consuming Bounded Contexts. Consumers who both read and write can translate from and into the shared language with confidence that their integration are correct. Such a Published Language can
be defined with XML Schema, JSON Schema, or a more optimal wire format, such as Protobuf or Avro. Often an Open Host Service serves and consumes a Published Language , which provides the best integration experience for third parties. This combination makes the translations between two Ubiquitous Languages very convenient.

#### Separate Ways
Separate Ways describes a situation where integration with one or more Bounded Contexts will not produce significant payoff through the consumption of various Ubiquitous Languages. Perhaps the functionality that you seek is not fully provided by any one Ubiquitous Language. In this case produce your own specialized solution in your Bounded Context and forget integrating for this special case.

#### Big Ball of Mud
1. A growing number of Aggregates cross-contaminate because of unwarranted connections and dependencies.
2. Maintaining one part of the Big Ball of Mud causes ripples across the model, which leads to “whack-a-mole” issues.
3. Only tribal knowledge and heroics—speaking all languages at once—save the system from complete collapse.

The problem is that there are already many Big Balls of Mud out there in the wide world of software systems, and the number will no doubt grow every month. Even if you are able to avoid creating a Big Ball of Mud by employing DDD techniques, you may still need to integrate with one or more. If you must integrate with one or more, try to create an Anti-corruption Layer against each legacy system in order to protect your own model from the cruft that would otherwise pollute your model with the incomprehensible morass. Whatever you do, don’t speak that language!

# Tactical Design
## Entity
An Entity models an individual thing. Each Entity has a unique identity in that you can distinguish its individuality from among all other Entities of the same or a different type. Many times, perhaps even most times, an Entity will be mutable; that is, its state will change over time. Still, an Entity is not of necessity mutable and may be immutable. The main thing that separates an Entity from other modeling tools is its uniqueness—its individuality.

Consider a bank accounting system. Each account has its own number. An account can be precisely identified by its number. This number remains unchanged throughout the life of the system, and assures continuity. The account number can exist as an object in the memory, or it can be destroyed in memory and sent to the database. It can also be archived when the account is closed, but it still exists somewhere as long as there is some interest in keeping it around. It does not matter what
representation it takes, the number remains the same.

## Value Objects
A Value Object , or simply a Value , models an immutable conceptual whole. Within the model the Value is just that, a value. Unlike an Entity , it does not have a unique identity, and equivalence is determined by comparing the attributes encapsulated by the Value type. Furthermore, a Value Object is not a thing but is often used to describe, quantify, or measure an Entity. Value Objects can contain other Value Objects, and they can even contain references to Entities.

## Services
When we analyze the domain and try to define the main objects that make up the model, we discover that some aspects of the domain are not easily mapped to objects. Objects are generally considered as having attributes, an internal state which is managed by the object, and exhibit a behavior. When we develop the ubiquitous language, the key concepts of the domain are introduced in the language, and the nouns of the language are easily mapped to objects. The verbs of the language, associated with their corresponding nouns become the part of the behavior of those objects. But there are some actions in the domain, some verbs, which do not seem to belong to any object. They represent an important behavior of the domain, so they cannot be neglected or simply incorporated into some of the Entities or
Value Objects.

For example, to transfer money from one account to another; should that function be in the sending account or the receiving account? It feels just as misplaced in either.

When such a behavior is recognized in the domain, the best practice is to declare it as a Service. Such an object does not have an internal state, and its purpose is to simply provide functionality for the domain. The assistance provided by a Service can be a significant one, and a Service can group related functionality which serves the Entities and the Value Objects. It is much better to declare the Service explicitly, because it creates a clear distinction in the domain, it encapsulates a concept.

A Service should not replace the operation which normally belongs on domain objects. We should not create a Service for every operation needed. But when such an operation stands out as an important concept in the domain, a Service should be created for it. There are three characteristics of a Service:
1. The operation performed by the Service refers to a domain concept which does not naturally belong to an Entity or Value Object.
2. The operation performed refers to other objects in the domain.
3. The operation is stateless.

When a significant process or transformation in the domain is not a natural responsibility of an Entity or Value Object, add an operation to the model as a standalone interface declared as a Service. Define the interface in terms of the language of the model and make sure the operation name is part of the Ubiquitous Language. Make the Service stateless.

While using Services, is important to keep the domain layer isolated. It is easy to get confused between services which belong to the domain layer, and those belonging to the infrastructure. There can also be services in the application layer which adds a supplementary level of complexity. Those services
are even more difficult to separate from their counterparts residing in the domain layer. While working on the model and during the design phase, we need to make sure that the domain level remains isolated from the other levels.

## Modules
For a large and complex application, the model tends to grow bigger and bigger. The model reaches a point where it is hard to talk about as a whole, and   understanding the relationships and interactions between different parts becomes difficult. For that reason, it is necessary to organize the model into modules.
Modules are used as a method of organizing related concepts and tasks in order to reduce complexity.

Modules are widely used in most projects. It is easier to get the picture of a large model if you look at the modules it contains, then at the relationships between those modules. After the interaction between modules is understood, one can start figuring out the details inside of a module. It’s a simple and efficient way to manage complexity.

Two of the most used are communication cohesion and functional cohesion. Communication cohesion is achieved when parts of the module operate on the same data. It makes sense to group them, because there is a strong relationship between them. The functional cohesion is achieved when all parts of the module work together to perform a well-defined task. This is considered the best type of cohesion.

Modules should have well defined interfaces which are accessed by other modules. Instead of calling three objects of a module, it is better to access one interface, because it reduces coupling. Low coupling reduces complexity, and increases maintainability. It is easier to understand how a system functions when there are few connections between modules which perform well defined tasks, than when every module has lots of connections to all the other modules.

Choose Modules that tell the story of the system and contain a cohesive set of concepts.

Seek low coupling in the sense of concepts that can be understood and reasoned about independently of each other. Refine the model until it partitions according to high-level domain concepts and the corresponding code is decoupled as well.

Give the Modules names that become part of the Ubiquitous Language. Modules and their names should reflect insight into the domain.

## Aggregate
Aggregates deal with following aspects;
### Transaction / Consistency boundaries
#### Aggregates are always internally consistent
invariants apply at every transaction commit
#### Agrregates are "eventually consistent" with each other
asynchronous updates propagate through system. How long the system will take to achieve the eventual consistency should be captured in SLA - business people should be involved to understand business consequence of any delays. For example; 90th percentile of the updates will be reflected in less than 100 seconds.
### Distribution boundaries
### Concurrency boundaries

Each Aggregate is composed of one or more Entities, where one Entity is called the Aggregate Root. The Root Entity of each Aggregate owns all the other elements clustered inside it. The name of the Root Entity is the Aggregate ’s conceptual name. You should choose a name that properly describes the conceptual whole that the Aggregate models.

Each Aggregate forms a transactional consistency boundary. This means that within a single Aggregate , all composed parts must be consistent, according to business rules, when the controlling transaction is committed to the database. This doesn’t necessarily mean that you are not supposed to compose other elements within an Aggregate that don’t need to be consistent after a transaction. After all, an Aggregate also models a conceptual whole. But you should be first and foremost concerned with transactional consistency.

The reasons for the transactional boundary are business motivated, because it is the business that determines what a valid state of the cluster should be at any given time. In other words, if the Aggregate was not stored in a whole and valid state, the business operation that was performed would be considered incorrect according to business rules.

The four basic rules of Aggregate design:
1. Protect business invariants inside Aggregate boundaries - the business should ultimately determine Aggregate compositions based on what must be consistent when a transaction is committed.
2. Design small Aggregates - The memory footprint and transactional scope of each Aggregate should be relatively small. Following this rule has the added benefit that each Aggregate will be easier to work on, because each associated task can be managed by a single developer. This also means that the Aggregate will be easier to test. Another thing to keep in mind when designing Aggregates is the Single Responsibility Principle (SRP). If your Aggregate is trying to do too many things, it is not following SRP, and this will likely be telling in its size.
4. Reference other Aggregates by identity only - This helps keep Aggregates small and prevents reaching out to modify multiple Aggregates in the same transaction.
This further helps keep the Aggregate design small and efficient, making for lower memory requirements and quicker loading from a persistence store. It also helps enforce the rule not to modify other Aggregate instances within the same transaction. With only identities of other Aggregates, there is no easy way to obtain a direct object reference to them. Another benefit to using reference by identity only is that your Aggregates can be easily stored in just about any kind of persistence mechanism, such as relational database, document database, key-value store, and data grids/fabrics. This means that you have options to use a MySQL relational table, a JSON-based store such as PostgreSQL or MongoDB, GemFire/Geode, Coherence, and GigaSpaces.
5. Update other Aggregates using eventual consistency.

Aggregates may also have Value Objects composed on them. Value Objects are used inside both Aggregates.

## Factories
When a client object wants to create another object, it calls its constructor and possibly passes some parameters. But when the object construction is a laborious process, creating the object involves a lot of knowledge about the internal structure of the object, about the relationships between the objects contained,
and the rules applied to them. This means that each client of the object will hold specific knowledge about the object built. This breaks encapsulation of the domain objects and of the Aggregates. If the client belongs to the application layer, a part of the domain layer has been moved outside, messing up the entire design. In real life, it is like we are given plastic, rubber, metal, silicon, and we are building our own printer. It’s not impossible, but is it really worth doing it?

Creation of an object can be a major operation in itself, but complex assembly operations do not fit the responsibility of the created objects. Combining such responsibilities can produce ungainly designs that are hard to understand.

Therefore, a new concept is necessary to be introduced, one that help to encapsulate the process of complex object creation. This is called Factory. Factories are used to encapsulate the knowledge necessary for object creation, and they are especially useful to create Aggregates. When the root of the Aggregate is created, all the objects contained by the Aggregate are created along with it, and all the invariants are enforced.

It is important for the creation process to be atomic. If it is not, there is a chance for the creation process to be half done for some objects, leaving them in an undefined state. This is even more true for Aggregates. When the root is created, it is necessary that all objects subject to invariants are created too. Otherwise the invariants cannot be enforced. For immutable Value Objects it means that all attributes are initialized to their valid state. If an object cannot be created properly, an exception should be raised, making sure that an invalid value is not returned.

Therefore, shift the responsibility for creating instances of complex objects and Aggregates to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects being instantiated. Create entire Aggregates as a unit, enforcing their invariants.

A Factory Method is an object method which contains and hides knowledge necessary to create another object. This is very useful when a client wants to create an object which belongs to an Aggregate. The solution is to add a method to the Aggregate root, which takes care of the object creation, enforces all invariants, and returns a reference to that object, or to a copy of it.

When creating a Factory, we are forced to violate an object’s encapsulation, which must be done carefully. Whenever something changes in the object that has an impact on construction rules or on some of the invariants, we need to make sure the Factory is updated to support the new condition. Factories are tightly related to the objects they are created. That can be a weakness, but it can also be a strength. An Aggregate contains a series of objects that are closely related. The
construction of the root is related to the creation of the other objects in the Aggregate. There has to be some logic which puts together an Aggregate. The logic does not naturally belong to any of the objects, because it is about the construction of other objects. It seems appropriate to use a special Factory class which
is given the task of creating the entire Aggregate, and which will contain the rules, the constraints and the invariants which have to be enforced for the Aggregate to be valid. The objects will remain simple and will serve their specific purpose without the clutter of complex construction logic.

## Repositories
In a model-driven design, objects have a life cycle starting with creation and ending with deletion or archiving. A constructor or a Factory takes care of object creation. The entire purpose of creating objects is to use them. In an object-oriented language, one must hold a reference to an object in order to be able to use
it. To have such a reference, the client must either create the object or obtain it from another, by traversing an existing association. For example, to obtain a Value Object of an Aggregate, the client must request it from the root of the Aggregate. The problem is now that the client must have a reference to the root. For large applications, this becomes a problem because one must make sure the client always has a reference to the object needed, or to another which has a reference to the respective object. Using such a rule in the design  will force the objects to hold on a series of references they probably wouldn’t keep otherwise. This increases coupling, creating a series of associations which are not really needed.

To use an object means the object has already been created. If the object is the root of an Aggregate, then it is an Entity, and chances are it will be stored in a persistent state in a database or another form of persistence. If it is a Value Object, it may be obtainable from an Entity by traversing an association. It turns
out that a great deal of objects can be obtained directly from the database. This solves the problem of getting reference of objects. When a client wants to use an object, it accesses the database, retrieves the object from it and uses it. This seems like a quick and simple solution, but it has negative impacts on the design.

Databases are part of the infrastructure. A poor solution is for the client to be aware of the details needed to access a database. For example, the client has to create SQL queries to retrieve the desired data. The database query may return a set of records, exposing even more of its internal details. When many clients
have to create objects directly from the database, it turns out that such code is scattered throughout the entire domain. At that point the domain model becomes compromised. It has to deal with lots of infrastructure details instead of dealing with domain concepts. What happens if a decision is made to change the underlying database? All that scattered code needs to be changed to be able to access the new storage. When client code accesses a database directly, it is possible that it will restore an object internal to an Aggregate. This breaks the encapsulation of the Aggregate with unknown consequences.

Repository, the purpose of which is to encapsulate all the logic needed to obtain object references. The domain objects won’t have to deal with the infrastructure to get the needed references to other objects of the domain. They will just get them from the Repository and the model is regaining its clarity and focus.

The Repository may store references to some of the objects. When an object is created, it may be saved in the Repository, and retrieved from there to be used later. If the client requested an object from the Repository, and the Repository does not have it, it may get it from the storage. Either way, the Repository acts
as a storage place for globally accessible objects.

The Repository may also include a Strategy. It may access one persistence storage or another based on the specified Strategy. It may use different storage locations for different type of objects. The overall effect is that the domain model is decoupled from the need of storing objects or their references, and accessing the
underlying persistence infrastructure.

It can be noted that the implementation of a repository can be closely liked to the infrastructure, but that the repository interface will be pure domain model.

There is a relationship between Factory and Repository. They are both patterns of the model-driven design, and they both help us to manage the life cycle of domain objects. While the Factory is concerned with the creation of objects, the Repository takes care of already existing objects. The Repository may cache objects locally, but most often it needs to retrieve them from a persistent storage. Objects are either created using a constructor or they are passed to a Factory to be constructed. For this reason, the Repository may be seen as a Factory, because it creates objects. It is not a creation from scratch, but a reconstitution of
an object which existed. We should not mix a Repository with a Factory. The Factory should create new objects, while the Repository should find already created objects. When a new object is to be added to the Repository, it should be created first using the Factory, and then it should be given to the Repository which will store it.

# Tactical Design with Domain Events
## Event Sourcing
Event Sourcing can be described as persisting all Domain Events that have occurred for an Aggregate instance as a record of what changed about that Aggregate instance. Rather than persisting the Aggregate state as a whole, you store all the individual Domain Events that have happened to it. 

All of the Domain Events that have occurred for one Aggregate instance, ordered as they originally occurred, make up its event stream. The event stream begins with the first Domain Event  that ever occurred for the Aggregate instance and continues until the last Domain Event that occurred. As new Domain Events occur for a given Aggregate instance, they are appended to the end of its event stream. Reapplying the event stream to the Aggregate allows its state to be reconstituted from
persistence back into memory. In other words, when using Event Sourcing , an Aggregate that was removed from memory for any reason is reconstituted entirely from its event stream. 

One of the greatest advantages of using Event Sourcing is that it saves a record of everything that has ever happened in your Core Domain , at the individual occurrence level. This can be very helpful to your business for many reasons, ones that you can imagine today, such as compliance and analytics, and ones that you won’t realize until later. There are also technical advantages. For example, software developers can use event streams to examine usage trends and to debug their source code.

# Keep in mind some of the pitfalls of domain modeling:
1. Stay hands-on. Modelers need to code
2. Focus on concrete scenarios. Abstract thinking has to be anchored in concrete cases.
3. Don't try to apply DDD to everything. Draw a context map and decide on where you will make a push for DDD and where you will not. And then don't worry about it outside those boundaries.
4. Experiment a lot and expect to make lots of mistakes. Modeling is a creative process.


