---
layout: post
title: Learnings from Uberconf - 2016
date: 2016-08-01
draft: false
tags: conference java programming career
comments: true
description: I got to attend the wonderful technical conference uberconf and I would like share feedback about the conference and summary of my learnings in this post. 

---
# Learnings from Uberconf - 2016 
 I got to attend the wonderful technical conference - [uberconf](https://uberconf.com/) and I would like share summary of my learnings in this post. 
 
## Feedback about the uberconf
       
 Before I jump on to the summary sessions, let me share my impression about the conference. This is one the best technical conference I ever attended. I tweeted 
      
 > Uninterrupted flow of food for mind and body.   
 
 The best thing I liked about the conference is that the sessions are 1.5 hours long that gave us enough time to learn deep-dive and learn the subject. Also the some of the longer subjects are split into two parts so that we can learn them in depth and do some hands on work.  The speakers are not only experts on their subject, they are good mentors and presented their sessions more engaging style.
 <br>        
 The only complaint, I can tell is that we are given only audio recordings of the session to offline listen after the conference. It would be have been great if video recordings are available after the conference.
  
## Summary of learnings from sessions

###  Twelve ways to make code suck less by [Venkat Subramanium](https://twitter.com/venkat_s)

* **12. Schedule Time to Lower Technical Debts :**  if technical debt is not payed back, we’ll end up with technical bankruptcy.
* **11. Favor high cohesion:** Narrow, focused, does only one thing well
* **10. Favor Loose Coupling:** Tight coupling make code hard to extend hard to test
* **09. Program with Intention:** Most of the time, we program accidentally without deliberate. Any code written should have clear intention.
* **08. Avoid Primitive Obsession:** Favor Functional code over imperative.
* **07.  Prefer Clear Code over Clever Code**
* **06. Apply Zinsser's Principle on Writing:** Great timeless book On writing well by Zinsser's for writing english. But very well applies to code. Principles are Simplicity , Clarity, Brevity, Humanity
* **05. Comment Why, not What:** Use comments to describe its purpose and constraints. Do’t use commenting as substitute for good code.
* **04. Avoid long methods**
* **03. Apply SLAP** A method should have singly level of abstraction.
* **02. Do tactical code reviews:** Peer reviews catch 60% of defects.
* **01. Reduce State & State Mutation :** Messing with state is the root of many problems.
 
###  Evolutionary Architecture by [Venkat Subramanium](https://twitter.com/venkat_s)
                          
#### Why Evolutionary architecture?

* We won't have a good picture in begining of project typically when architecture is created. Our knowledge of system will improve as project mature.
* We should do **enough** up-front design not ~~big~~ up-front design.
* The ***feedback loop*** is extremely important to be able to course correct.

#### Planning for Evolutionary architecture

* When prioritizing stories, analyze both business value and architectural impact.
* Work on most **valuable** and more **impactful** stuff in the begining.
* > **Scrum Velocity ** - It doesn't matter *how fast* you run, it's important that you run in *right* direction.

#### Principles for Evolutionary Architecture
 
 * **Keep it simple:**  Do minimum to meet the requirements.
 * **Reversibility:**  When making a decision, If it is easier to reverse, go for it. If it is hard to reverse, postpone decision it you no longer can.
 **Wait for last responsible moment:**  Compare cost of doing it *now* vs cost of doing it *later*. 
		
`
    Now   Later
            cost >  cost   -> delay
            cost == cost   -> delay
            cost <  cost 
 -probability of needing it in future
                            low -> delay
                            high -> now.
`
 
* **Automated testing** - Without automated testing and feedback, it's hard to make a decision later and verify everything still work.
 * **Triangulate**
	+ You don't a interface or abstract base class for everything.
    + Instead write a class, write another similar class if it happens, then. **triangulate ** - extract what is common into a base.
 * **Postle's law** - Follow [Robustness Principle](https://en.wikipedia.org/wiki/Robustness_principle)  Be conservative in what you send, be liberal in what you accept
* **Minimize libraries and frameworks:** Don't build what you can buy (or available open source) . Don't buy (or download) what you don't need. 

###  Measuring Quality of Design by [Venkat Subramanium](https://twitter.com/venkat_s)

* Quality of design can be measured using two key qualities ***Stability***  `(I)` and ***Abstractness***  `(A)`of all packages in application.  Where
	 `I = Number of classes this package depends on / (Number of classes this package depends on + Number of classes depends on this package)` And
    ` A = Number of interfaces / Number of interfaces + Number of clases ` in this package.
* The distance from ideal design is computed as `D' = | A + I | - 1` . Where, smaller `D'` is better .
	* The ideal value of `D'` is 0. But don't go for it.
	* `D' > 0.25` is a call for refactoring.
	* `D' < 0.25` is fairly ok, don't put to much effort in lowering. Because it's hard to measure quality of refactoring.
* All of these can be automatically computed using [jdepend](http://clarkware.com/software/JDepend.html) tool (plugins are available for build systems and IDEs) and tracked in CI tools like jenkins.

###  Parallel programming with Java 8 Streams by [Venkat Subramanium](https://twitter.com/venkat_s)

* Leverage the power of Java 8 streams to easily switch sequential code to concurrent code by using parallel streams.

###  Frege for Java Programmers by [Venkat Subramanium](https://twitter.com/venkat_s)

* [Frege](https://github.com/Frege/frege) is a Haskell for the JVM.
* Frege compiles to Java, runs on the JVM, and reuse with existing java libraries.
* If you love **Haskell** and *purely* functional language.  ***Frege*** is a great choice.

###  Software Architecture Fundamentals by  [Neal Ford](https://twitter.com/@neal4d) and [Mark Richards](https://twitter.com/@markrichardssa)

* We should move from tranditional *layerd N-tier* architecture to ***microservices*** architecture.
	* *microservices* architecture has high score for most of architecture characteristics like *agility, testability, scalabilty, evolutionary*
	* But major complication is we can no longer manually manage applications, deployments , tests , builds etc. **DevOps** becomes very important.
* ***Service-based architecture*** can be used as a middle ground to reduce complexities of *microservices* architecture.
	* Instead of splitting into thousands of microservices and combine the into *service components*.
* ***Event driven architecture:*** Works best for applications that doesn't need immediate response and everything can be asynchronously processed.
	* It's easy build concurrent, scalable , reactive and reselient applications using event drive architecure.
    * But the problem with event drive approach is it becomes  **Really hard** to understand and monitor entire flow. 
* ***Microkernal Architecture:*** can be used to build *core system* to run minimal functionality and support more functionalities using *plugin-modules* .
	* Managing *transitive dependencies* and *plugin-contracts* are the biggest problems with this architecture.

###  Why does yesterday's best practice becomes tomorrow's Anti-pattern by [Neal Ford](https://twitter.com/@neal4d)

* Adapdability of software is more important than predictability of software.
* Evolutionary architecuture is crucial for different parts of application to evolve on it's own phase.
* *Microservices* helps to move towards Evoluationary architecture.

###   Java Optimizations That Matter by Douglas Hawkins

* Micro-optimizations are just that - not much *valuable*. Modern compilers are smart enough to implicitly do bunch of optimizations.    
* `java.util.concurrent` is *awesome* , but read docs *carefully*. 

###    Concurrency Concepts in Java by Douglas Hawkins

* There is no automatic concurrency management in Java.  We need to explicitly code for synchronous handling of states during concurrent execution. 
* **Immutablity is your best friend**
> Immutable objects have a very compelling list of positive qualities. When you create immutable classes, entire categories of problems simpy disappear .
