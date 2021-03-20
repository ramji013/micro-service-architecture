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

