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
