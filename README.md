# Software Engineering cheat sheet


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
