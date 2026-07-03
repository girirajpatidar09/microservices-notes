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

## What are the disadvantages of Monolithic Application ?
```text
A monolithic application is built as a single, tightly coupled unit—UI, business logic, and database access all bundled together. That simplicity helps early on, but it creates real problems as the system grows.

Here are the key disadvantages:

1. Hard to Scale 🚫

You can’t scale just one part of the system.
If only one module needs more resources, you still have to scale the entire application.

👉 Example: If login traffic increases, you still scale the whole app—even unrelated modules.

2. Slower Development Over Time 🐢

As codebase grows:

It becomes complex and harder to understand
New developers take longer to onboard
Small changes can affect unrelated parts

3. Deployment Risk ⚠️

You must deploy the entire application for even a small change.

👉 Risk:

One bug → whole system down
Rollbacks are painful
4. Poor Fault Isolation 💥

A single failure can crash the whole system.

👉 Example:
If payment module fails → entire app may go down

5. Technology Lock-in 🔒

You are stuck with one tech stack.

👉 Want to use a new language or framework?
You’ll likely need to rewrite a big part of the system.

6. Difficult to Maintain 😵

Tightly coupled code means:

Fixing one issue may break another
Refactoring is risky and time-consuming


7. Limits Team Productivity 👥

Multiple teams working on the same codebase:

Causes conflicts
Requires heavy coordination
Slows down releases

8. Longer Build & Startup Time 

Large applications:

Take longer to build
Take longer to start
Slows development and testing cycles

9. Not Suitable for Modern Distributed Systems 

Monoliths struggle with:

Cloud-native architecture
Continuous deployment
Independent scaling
Simple Summary

# Monolithic apps are:
Easy to start
Hard to scale, maintain, and evolve



# Conclusion

1. Single point of failure.
2. Re-Deploy entire app.
3. Maintenenece of app.
4. Burden on Server.


```
---


## What are microservices ?
```
Microservices (simple definition):
It is an architectural desing pattern
 Microservices is a way of building an application by dividing it into small, independent parts (services), where each part does one specific job and works 
on its own.

 In very easy words:
Instead of making one big application, you make many small applications that work together.

 Example:
Think of a shopping app:


Login → one service
Payment → another service
Orders → another service


Each service works independently but connects with others.


# Cons : Complecity in communication , Distributed tracing and data consistency

```
---

##  Microservices is an Architecture
```text
Small, independent services
Built around business capabilities
Each service owns its own data
Communicate via APIs or events
Deployed and scaled independently
Resilient to failures
Not just multiple Spring Boot apps
```
---







