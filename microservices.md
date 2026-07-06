# Microservices 

## What is monolithic application ?
``` text
🔹 What is a Monolithic Application?
A Monolithic Application is a software architecture where the entire application is built as a single unit.Single large codebase ,single Database
, everything tightly coupled.


🔹 Simple Idea
One big application → one codebase → one deployment

🔹 Example (Real-world analogy )
Think of a restaurant where one person does everything:

Takes orders
Cooks food
Serves customers



# Drwabacks of Monolithic architecture



1) Single Point of failure :: 
  
    In a monolithic application, all modules (User, Product, Order, Payment, etc.) run inside one application.Now imagine the Payment Module has a 
	bug and causes the application to crash.If the application crashes, every feature becomes unavailable.

2) Re-Deploy entire app ::

   Even if you change only one small feature, you must rebuild and deploy the entire application.
   
3) Maintenence of the app ::
     As the application grows, it becomes difficult to understand, update, and fix.
	 
4) Burden on server :: 
    
	In a monolithic application, all modules run on the same server.
    If one module receives heavy traffic, you must scale the entire application, even though the other modules are not busy.


```
---



## What are microservices ?
```text 
It is an architectural desing pattern.Microservices is a way of building an application by dividing it into small, independent parts (services), 
where each part does one specific job and works on its own.

 In very easy words:
Instead of making one big application, you make many small applications that work together.

 Example:
Think of a shopping app:


Login → one service
Payment → another service
Orders → another service


Each service works independently but connects with others.


# Advantages  :: 

1) Loosely Coupled :

   In a microservices architecture, each service is independent of the others.
   A change in one service usually does not affect the others.
   
2) Easy Maintenence :

   Each microservice is small and focuses on one specific business function.
   This makes the code easier to understand, debug, and maintain.
   
3) Load will be distributed :
  
    Each service can be scaled independently based on its traffic.
	
4) Technology Independency :

     Each microservice can be developed using the technology that best fits its requirements.
     One service is not forced to use the same programming language or database as the others.
	 
5) High Availability :
      
	If one microservice fails, the other services can continue working.
	The failure is isolated to that service.


# Disadvantage :: 


1) Bounded Context (deciding no.of rest apis to develop)
2) Duplicate Configuration
3) Visibility


```
---

## Microservices Architecture

![Microservices Architecture](images/microservices-architecture.jpeg)


```text

  
-> There is no standard architecture for Microservices development

-> People are customizing microservices project architecture according to their requirement.


1) Service Registry
2) Admin Server
3) Zipkin Server
4) Backend Services (REST APIs)
5) API Gateway
6) Feign Client
7) Config Server
8) Apache Kafka
9) Redis Cache
10) Docker

```
---


##  Service Registry 

``` text

A Service Registry is a central directory where all the microservices register themselves so that other services can find and communicate with them.


-> Service Registry is used to maintain list of services available in the project.

-> It provides information about registered services like

		Name of service, url of service, status of service

-> It provides no.of instances available for each service.

-> If a service crashes, it is removed from the registry.

-> We can use Eureka Server as a service registry

-> Eureka server provided by Spring Cloud Netflix library

```
---

## Admin Server 

```text 

-> Actuators  are used to monitor and manage our applications

-> Monitoring and managing all the apis seperatley is a challenging task

-> Admin Server Provides an user interface to monitor and manage all the apis at one place using actuator endpoints.




How it works ::

Step 1: Admin Server starts

Spring Boot Admin Server

↓
Waits for applications to register.

Step 2: Microservices register

User Service  ------------\
Order Service  ------------> Admin Server
Payment Service ----------/

The Admin Server now knows about all running services.

Step 3: Dashboard

-----------------------------------
Spring Boot Admin Dashboard
-----------------------------------
User Service        UP
Order Service       UP
Payment Service     DOWN
Inventory Service   UP
-----------------------------------

You can click a service to see more details such as:

Health
Metrics
Beans
Environment
Configuration
Loggers
Mappings

```
---

## Zipkin Server

```text

 A Zipkin Server is used for distributed tracing in a microservices architecture.

When a single user request passes through multiple microservices, Zipkin helps you trace the complete journey of that request and identify where 
time is being spent or where failures occur.

-> It is Used for Distributed tracing

-> Using zipkin server, we can monitor which api is taking more time to process request.

-> Using Zipkin we can understand how many apis involved in request processing.

```
---

## Backend apis
``` text

-> Backend apis contains business logic

-> Backend apis are also called as REST APIs / services / microservices

	Ex: payment-api, cart-api, flights-api, hotels-api

Note: Backend api can register as client for Service Registry, Admin server & Zipkin server (It is optional)

```
---


## FeignClient

``` text

-> It is provided by spring cloud libraries

-> It is used for Inter Service Communication

-> Inter service communication means one api is accessing another api using Service Registry. 

Note: External communication means accessing third party apis.

-> When we are using FeignClient we no need mention URL of the api to access. Using service name feign client will get service URL from s
service registry.

-> Feign Client uses Ribbon to perform Client side load balancing.

 Note: Ribbon is deprecated. It has been replaced by Spring Cloud LoadBalancer.



```
---


## Load Balancing 

```text 

Load Balancing is the process of distributing incoming requests across multiple instances of the same service so that no single instance 
becomes overloaded.

```
---

## API Gateway 

``` text 
An API Gateway is the single entry point for all client requests in a microservices architecture.

Instead of the client calling individual microservices directly, it sends all requests to the API Gateway. The gateway then routes each request 
to the appropriate microservice.

In Spring Boot, Spring Cloud Gateway is the recommended API Gateway implementation.


> API Gateway is used to manage our project backend apis

-> API Gateway acts as mediator between user requests and backend apis

-> API Gateway acts as entrypoint for all backend apis

-> In API Gateway we will have 2 types of logics

		1) Request Filter : To validate the request (go / no-go)

		2) Request Router : forward request to particular backend-api based on URL Pattern

				/hotels => hotels - api

				/flights => flights - api

				/trains => trains - api


```
---

## What is Routing?

```text

Routing is the process of sending an incoming request to the correct microservice based on predefined rules, such as the request URL, HTTP method, 
headers, or other criteria.

Routing is one of the main responsibilities of an API Gateway.

``` 
---


## Steps to develop Service Registry Application (Eureka Server)
```text
1) Create Service Registry application with below dependency

	 - EurekaServer (spring-cloud-starter-netflix-eureka-server)

2) Configure @EnableEurekaServer annotation in boot start class

3) Configure below properties in application.yml file

server:
  port: 8761
  
eureka:
  client:
    register-with-eureka: false

Note: If Service-Registry project port is 8761 then clients can discover service-registry and will register automatically with service-registry. If service-registry project running on any other port number then we have to register clients with service-registry manually.

4) Once application started we can access Eureka Dashboard using below URL

		URL : http://localhost:8761/
		
		
		
# What is the purpose @EnableEurekaServer ?

@EnableEurekaServer is used to convert a Spring Boot application into a Eureka Server (Service Registry).

Why do we need @EnableEurekaServer?

In a microservices architecture, there can be many services:

User Service
Order Service
Payment Service
Inventory Service

Instead of every service remembering the IP address and port of every other service, they all register with the Eureka Server.

The Eureka Server acts like a phone directory or service registry.

               Eureka Server
             (Service Registry)
                    |
        --------------------------
        |     |      |          |
     User   Order  Payment  Inventory
    Service Service Service   Service
	
	
	
# eureka.client.register-with-eureka=false  Why we use this property ?
  
 A Eureka Server also contains Eureka Client functionality. By default, it tries to register itself with another Eureka Server.
If you have only one Eureka Server, there is no other server to register with. Therefore, we disable self-registration.
	
```
---

## Steps to develop Spring Admin-Server
```text

1) Create Boot application with admin-server dependency 
	(select it while creating the project)

2) Configure @EnableAdminServer annotation at start class

3) Change Port Number (Optional)

4) Run the boot application

5) Access application URL in browser (We can see Admin Server UI)


@EnableAdminServer is used to convert a Spring Boot application into a Spring Boot Admin Server. It provides a web 
dashboard to monitor and manage Spring Boot applications.


```
---


## Difference between Eureka Server and  Admin Server
```text
| Eureka Server                  | Spring Boot Admin Server              |
| ------------------------------ | ------------------------------------- |
| Used for **Service Discovery** | Used for **Monitoring**               |
| Stores service locations       | Displays health and metrics           |
| Helps services find each other | Helps developers monitor applications |
| Maintains a service registry   | Provides a monitoring dashboard       |

```
---

## Steps to work with Zipkin Server
======================================

```text
1) Download Zipin Jar file 

		URL : https://zipkin.io/pages/quickstart.html

2) Run zipkin jar file 

		$ java -jar <jar-name>

3) Zipkin Server Runs on Port Number 9411

4) Access zipkin server dashboard

		URL : http://localhost:9411/
		
```
---

## @EnableDiscoveryClient 

```text
@EnableDiscoveryClient is used to enable a Spring Boot application to register with a Service Registry (such as Eureka) 
and discover other registered services.
```
---


##  Steps to develop WELCOME-API

```text

1) Create Spring Boot application with below dependencies

		- eureka-discovery-client
		- starter-web
		- devtools
		- actuator
		- zipkin
		- admin-client

2) Configure @EnableDiscoveryClient annotation at boot start class

3) Create RestController with required method

4) Configure below properties in application.yml file

-----------------------application.yml-----------------------------------------
server:
  port: 1111

spring:
  application:
    name: WELCOME-API

  boot:
    admin:
      client:
        url: http://localhost:9090/
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka

management:
  endpoints:
    web:
      exposure:
        include: '*'

-------------------------------------------------------------------

5) Run the application and check in Eureka Dashboard (It should display in eureka dashboard)

6) Check Admin Server Dashboard (It should display) (we can access application details from here)

	Ex: Beans, loggers, heap dump, thred dump, metrics, mappings etc...


7) Send Request to REST API method

8) Check Zipkin Server UI and click on Run Query button
	(it will display trace-id with details)
	
```
---



























