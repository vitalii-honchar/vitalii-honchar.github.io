---
layout: page
title: "Software Architectures Overview"
categories: Post
---

# Introduction

During my career I worked on different projects with different architectures.
In this post I will describe 3 most important architectures: monolith, modular
monolith and microservices.

# Monolith

Let's begin from good old monolith. This is the most simple architecture of
application which is usually perceived like something bad by engineers in 2023.

## One monolith application

![Monolith](/attachments/2023-05-01-software-architecture/monolith.png)

## Scaled monoliths

![Monolith Scale](/attachments/2023-05-01-software-architecture/monolith_scale.png)


## Main idea

All code components exists in one applications, deployed all
together.

## Use cases

* Small team.
* Need to develop product as fast as possible, for example release full product
  in 3 days (if you know what I mean :))
* Small budget for a project.

Monolith architecture is an ideal architecture for start ups and small
companies with small IT department, because this kind of architecture is the
most cheapest architecture.

## Pros

* Very fast development:
  * Team of developers shouldn't to communicate with another departments for
    implement feature or no need to change infrastructure.
* Simple infrastructure:
  * No need or minimal DevOps team, dev team can easily adjust simple CI/CD pipelines and
    deploy monolith to AWS ECS or EC2.
* Simple scaling:
  * Very big mistake is to think that monolith can't be scaled.
  * Monolith scales and does it very well, all what need to do is just to develop it it a right way.
* Cheap rent for servers:
  * With time servers renting becomes more expensive and this point becomes
    cons.

## Cons

* Complex code base, because all components are highly coupled:
  * As far as everything is in one place it's very common situation when one
    thing in monolith appplication knows everything about system. This problem
    can be solved with modular monolith.
* Degrades development speed and servers rent cost with time, because highly
  coupled components makes system hard to support.
* Changes in one component requires retesting full system:
  * This is not always true, but is true in a lot of cases. Modular monolith
    solves this.
* Usually full regress testing required before release a new version of
  monolith.
* Hard to scale a team:
  * Due to highly coupling of system components work on one monolith from
    different teams will overlaps, which will results in merge conflicts or so
    on. 

# Modular monolith

This is improved monolith version whih solves problems: 
* High component coupling.
* Scaling teams.
* Requirement to run full regress testing before release a new version.

## One modular monolith application

![Modular Monolith](/attachments/2023-05-01-software-architecture/modular_monolith.png)

## Scaled modular monoliths

![Modular Monolith Scaled](/attachments/2023-05-01-software-architecture/modular_monolith_scale.png)


## Main idea

Application splited internally on different modules according to module
responsibility, for example: 
* Auth module - contains code for authorize requests.
* Business logic module 1 - contains code for one of business flows in company.
* Business logic module 2 - contains code for another business flows in
  company.

This modules communicates which each other throughout in-memory API and them
should be implemented as independent applications, but still in one runtime.
Also all modules deploys all at once as one application, but maybe implemented possibility to
disable module throughout feature flag for emulate microservices behaviour.

## Use cases

* Small or medium team. Also it's a good choice for growing teams.
* Need to have a stable high development speed during some period of time.
* Need to have a possibility for easy migration to microservices architecture.
* Small/medium budget for a project.

Modular monolith architecture is an ideal architecture for growing business,
because it provides good scalability for teams and possibility for migration to
microservices architecture when business will be ready. Also this architecture
provides full cover for non-functional requirements and is not too expensive.

## Pros

* Scale team is more easy than with monolith architecture.
* Development speed is high during longer period of time, rather than in
  monolith architecture.
* Simple infrastructure.
* Simple scaling.
* Cheap servers rent price at start, but with time degrades as in monolith
  architecture too. Can be solved by possibility for disable/enable modules in
  application.
* Regress testing no longer required before release every version of software,
  need test only changed module and it's dependencies.

## Cons

* More complex application design in comparing to monolith architecture.
* Requires more skilled engineers in a team for control development direction,
  because with bad engineer practics it's easy to transform modular-monolith to
  monolith and loose all pros.
* Degradation of development speed and increasing of servers cost is slower in
  comparing with monolith architecture, but still is present.

# Microservices

The most popular architecture in nowadays. I think it happens, because
implementing microservices architecture is very complex and interesting task.
Also this architecture provides very good benefits as team scaling, simple
applications, scalability (but as I told previously scalability can be achieved in another
architecture too, so this shouldn't by main reason for choose microservices
architecture).


## One microservices system

![Microservices](/attachments/2023-05-01-software-architecture/microservices.png)

## Scaled microservices system

![Scaled Microservices](/attachments/2023-05-01-software-architecture/microservices_scale.png)

## Main idea

Split system by responsibility and create separate service for it.
Communication between microservices executes throughout network. Very
important in building microservice architecture is to track dependencies
between microservices, otherwise can be created distributed monolith which is
the worse mistake in architecture which can be done.

## Use cases

* Medium or big teams. Choice for growing from medium to big team.
* Need to have possibility for parallel development.
* Need to have possibility for scale different components of system.
* Big budget for a project.

As for me microservices is a good choice for big companies which have money for
big IT department.

## Pros

* Easy to scale team:
  * Due to different responsibilities in different services parallel
    development is an easy option.
  * Popular architecuture which I suggest decreases complexity for find new
    developers in the team.
* Every service is simple, thus speed of development for one service is high.
* Easy to scale:
  * Possibility to scale each service independently which may reduce costs for
    servers renting, but the same feature has modular monolith too.
* No need for regress testing in case if dependencies between services are one
  direction.
* Development speed and scalability don't degrades with time.

## Cons

* Complex infrastructure:
  * Dedicated DevOps team should be in company for adjust infrastructure.
* Need to have highly skilled engineers in the team to drive development:
  * Microservices architecture is the hardest architecture which seems very
    simple at first glance. Due to lack of skills in a team there is a big chance to build
    microservices which depends on each other or with shared databases. Which
    will results in very hard supported system.
* High cost for support this system, due to requirement to have highly skilled
  engineers, dedicated DevOps team and servers cost.
* Low development speed in comparing to modular-monolith.
* High requirements for communications between teams.

# Conclusions

In this post I described 3 main software architectures in nowadays. I didn't
explained how to choose architecture for a new project, because this post will
be overhelmed. I will create a new post with thoughts about choosing an
architecture. 
