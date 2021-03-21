Micro Service

It is based on services and its inter communication. It is collection of light weight and loosely coupled interconnected services which perform each specific
function.

Advantage:

1. Low coupling
2. Imporve modularity
3. Promotes parallel development
4. Promotes scalability


Drawbacks:

1. Higher infrastructure cost
2. Integration testing complexity
3. Service management & deployment
4. nanoservice anti pattern

Challenges:

1. lack of Planning
2. lack of Knowledge
3. skill
4. time

How to avoid project failure

1. identify the requirement that to cover in the services
2. automate the activities such as CI/CD
3. Avoid common pifalls and use proper design pattern.


Microservice Template:

It is much important becuase of below reasons

1. For any project, it take initially significant amount of time to setup
2. Code repetition on each micro-service setup
3. Connection setup for DB, message brokers
4. Unit testing project structure


Code repository:

Mono-repo

Pros:

1. Easier to keep input/output contracts in sync
2. Easier to version the entire repo with a build number

Cons:
1. multiple teams work in the same repo can cause code breakage and create dependency issue with CI/CD deployment
2. high possibility of creating tight coupling of code
3. as large code base, it take longer time to build and deploy


Discre repo:

Pros:
Scope and ownership of the repository will be much clearer

Cons:
1. Contract versioning become more complex
2. If not managed properly it may become monothic
3. More cost for setting environment for each services including CI/CD pipeline


Communication:

inter service communication:

It can be done using synchronous and asynchornous way.

Synchronous:

RPI - Reporte procedure invocation

A service send a request to another service and wait for its response to proceed further.


Asynchronous:

messaging bus: A micro service park a message in a queue and another micro service will read it from there (publish-subscribe pattern).


Service registry:

It is required for dynamic scaling.

service registry microservice will hold details of each micro service and its network information. it keep tracks of the available instances of the microservices.

On the service startup, the service send a request to register component and register itself. Similarly, when it is shutdown, it will send a request to the registry component to remove the detail. The registry component periodically make health check calls with the each of the registered services.


Microservice Discovery:

client side discovery:

a micro service will call service registry and get the network information about the target/destination server details and once obtained it will the endpoint

Server side discovery:

a micro service will directly call load balancer which will take responsibility to call service registry to know the target endpoint details and once obtained it will make the call. The issue with this approach is multiple network call required. Also, the Load balancer component plays a critical role, we need to ensure that component availability all the time.


DataBase:

1. Shared database  - it will cause latency in db and two services may attempt to update on a data same time.
2. Database per service. - it will bring coupling between services which a bit complex to write queries which satisfies the requirement of each dependent services. This can be avoided by Api composition and Event sourcing.


API composition:

it acts as a centeral component and make a call to underlying services and aggregate the response from them and send it back.
Issue with this is, the underlying services sometime may return bulk response and the parent may not be able to handle such case which impact the performance.


Event source:

It acts as a message broker and each component will register for events.

Lets say services A, B & C which perform some actions. The service A updates some data in its DB and also publish the information about the update into the Event store. The services B & C registered with the Event store to receive the information about the update.

two phase commit:

A coordinator involved and send message to underlying services and wait for the response. if all the services responded with successful response then it will send another request to commit the transaction. If any of the transaction failed the coordinator will send rollback message to the services to rollback the changes. if any issue happened during the commit phase with any of the service, it will return alert to reverse the previous transaction.
