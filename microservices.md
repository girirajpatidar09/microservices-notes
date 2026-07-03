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












