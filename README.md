# Software Engineering cheat sheet
## The requirements in software engineering
### Functional requirements
Functional requirements define the basic system behaviour, they are ***what*** the system does or must not do, and can be thought of in terms of how the system responds to inputs.

Functional requirements are features that allow the system to function as it was intended. Put another way, if the functional requirements are not met, the system will not work. Functional requirements are product features and focus on user requirements.

#### Some of the functional requirements: 
* Business Rules.
* Transaction corrections, adjustments and cancellations.
* Administrative functions
* Authentication
* Authorization levels
* Audit Tracking
* External Interfaces
* Certification Requirements
* Reporting Requirements
* Historical Data
* Legal or Regulatory Requirements


### Non functional requirements
While functional requirements define what the system does or must not do, non-functional requirements specify how the system should do it. Non-functional requirements do not affect the basic functionality of the system (hence the name, non-functional requirements). Even if the non-functional requirements are not met, the system will still perform its basic purpose.
#### Some of the non functional requirements
* Performance – for example Response Time, Throughput, Utilization, Static Volumetric
* Scalability
* Capacity
* Availability
* Reliability
* Recoverability
* Maintainability
* Serviceability
* Security
* Regulatory
* Manageability
* Environmental
* Data Integrity
* Usability
* Interoperability

### Difference between functional and non-functional requirements
![difference](https://i.imgur.com/uzUqsX8.png "difference")

### Examples of functional and non-functional requirements

#### Functional Requirements Example:

Authentication of a user when he/she tries to log into the system.

System shutdown in the case of a cyber attack.

Verification email is sent to user whenever he/she registers for the first time on some software system.

#### Non-functional Requirements Example:

Emails should be sent with a latency of no greater than 12 hours.

Each request should be processed within 10 seconds.

The site should load in 3 seconds when the number of simultaneous users are > 10000

*** 
## User cases and User case diagramm
### User case diagramm
The user case diagramm is a high level methode to describe an idea of a System in a simple way that can be understood from all users.

The User case diagramm contains: 
* System: could be Wep application, software component or Business process.
* Actor: could be any user that has access to this system like admin, user, another system, organisation or an external device.
* User case: is a description of a function that will be done from an actor (e.g. actor make login to the system, login will be an user case)
* Relationship: is a way to descripe how all actors and user case connect with each other.
  * Type of the relationships:
    * Association: is a base relationship between two sides.
    * Include: an Included use case (B) is inside a base use case (A). (B) has to be done that let (A) to be done. to connect between (A) (B) we drow (A)---->(B)
    * Extend: has a base use case (A) and extend use case (E), when (A) is executed, (E) will sometimes be executed. (E) will only be executed in certain conditions. (A)<----(E)
    ![different between Include and Extend](https://i.imgur.com/QmaWEmF.png)
    * Generalization .

Example for a Banking App Usecase diagramm ```based on``` [UML Use Case Diagram Tutorial](https://www.youtube.com/watch?v=zid-MVo7M-E)

![img](https://i.imgur.com/78KLF9P.png)

### User Story
The user story describes pieces of functionality from a user’s point of view, expressed in a solid, compact way. They reflect what a particular class of user needs and the value to be gained.

User stories provide an excellent way to define your product with clarity. A set of well-defined, prioritized user stories can help you articulate the functionality of your product using ‘plain English’ — with no technicalities and implementation details.
The ‘user story’ approach empowers meaningful product discussions, both within the product development team and with external stakeholders.

#### How to write a good user story?
There are several variations to write a good user story, including:

``` “As a <role or persona>, I can <goal/need> so that <why>” ``` 

Or

```“As a <particular class of user>, I want to <be able to perform/do something> so that <I get some form of value or benefit>”```

*** 
## Entity Relationship diagram (ERD)
An Entity Relationship diagram is a way to descripe the relationship between all elements, tables and components in the Database. An ERD consists of many Entities, every entity reference a table on our Database. The entity has all atributes and keys in the original Database table.

we connect our entities with relations. There is a many types of relations to create ERD, we will talk about relationship types in UML.
### Relations types in UML
* one to one (1:1): Entity_A has just one element from Entity_B and Entity_B has just one element from Entity_A
* one to N (1:N): Entity_A has more than one element from Entity_B and Entity_B has just one element from Entity_A 
* N to M (N:M): Entity_A has more than one element from Entity_B and Entity_B has more than one element from Entity_A
#### Notation for relationship
* Assoziation: is the normal relationship between entities (Entity_A and Entity_B use each other): the relation between a doctor and patient is Assoziation.
* Assoziation classes: is a relationship between three entities, the middle entity connect the other two entities and does not exist without the other two. e.g. a company need an employ and an employ is a person with more attributes.A company has more than one employ and the employ works for one company, an employ is one person but the person could be an employ in more than on company. That is an Assoziation classes.
* Generalization: a Entity_B and Entity_C inherit some attributes from Entity_A.
* Aggrigation: is a relationship between two entities one is strong(parent) and onther is weak(child) with the ability to delete the parent without effect on the child. Car(parent) and Engine(child): if we delete the Car the relationship will be also deleted but the engine still exist and meaningfull.
* Composition: is a relationship between two entities one is strong(parent) and onther is weak(child) with the no ability to delete the parent without effect on the child. That mean ifwe delete the parent the child will be meaningless and automatily deleted. Person(parent) and Hand(Child): if we delete the Person the relationship will be also deleted and the Hand will be also meaningless (Hand does not exist without person) so the Hand will be also deleted.


***
## Stateful vs Stateless Applications
### Stateful application:
a statefull application is an application that use a defined state to make its job. Lets imagen that we have a Server1 has two services Login and viewProfile.
a client want to login to this Server, he send a http request to the server1 with a username and password.

The Server has a state ***logged*** and it is false by default. When the server receives the request, it send another request to the DB, to check if the user is registerd, if the user is registerd then the state in the server will be changed to **true**. So long the client send the request to the server1, it should be no problem, because the state in server1 is **ture**.

**BUT** if there is another server2 and the client send the request to this server2 then it will be problem, becausse the state in server2 is **false**, although the user has been logged in. In this case a Load Balancer will be used to manage the requests between the servers.
![stateful app](https://i.imgur.com/U6jUVPO.png "stateful app")


### Stateless application:
a stateless application is an application that does not have a defined state.

Back to our example: both server1 and server2 has no ***logged*** state, they use another concept, they use *token*.

When a client send a login request to the server with username and password, if the user us registerd the server send token to the user, and always when the cilent send a request to the server, he send a token with. This token tells the server that this user is registed (instead of a changeable state).

In that way it does not matter which server will be asked from the user, becase the token will be sent to both of servers.

The problem herre could be the high number of requests from the server to DB to check the the token is very request.

![stateless app](https://i.imgur.com/r4Lih4H.png "stateless app")

```based on Hussein Nasser's video``` [Stateful vs Stateless Applications (Explained by Example)](https://www.youtube.com/watch?v=nFPzI_Qg3FU)
