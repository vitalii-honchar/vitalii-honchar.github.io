---
layout: page
title: "Application development: Layered Architecture"
categories: Post
---

## Introduction

Layered Architecture - classic words in the commercial development. I used it during long time, because this is a default choice for a new application in Spring, Flask or anything else. But after Autumn 2020 when I first time touched Domain Driven Design in Ajax Systems with modular monolith I changed my mind and decided that layered architecture is a legacy thing and shouldn't be used in nowadays. I thought so during long time, but what an interesting moment, so why I chose this kind of architecture to launch some product about which I can't tell or why this architecture was chose by startups?
Answer is simple - because this kind of an architecture is a good architecture in right hands and it also has its pros and cons.

Also during reading a book "Software Architecture Fundamentals" I found proofs of my thoughts which I had about layered architecture during last year. So in this blog post I will explain what is layered architecture and when to use it.

## Layered Architecture

This is an architecture where responsibilities of components bound to them technical implementation.

# Layers

![Layered Architecture](/attachments/2023-06-01-layered-architecture/layered-architecture.png)

Generic there is 3 layers - web layer, business layer (or service layer) and database layer. All code related to different business entities exists throughout this three layers. 

# Components

From components perspective it will looks like on the picture below. Components related to different business entities lives together in one layer, for example: user controller and device controller exists together even when them represents different business entities. This is also true for another layers.

![Layered Architecture Components](/attachments/2023-06-01-layered-architecture/layered-architecture-components.png)

# Main problem of this architecture

First and main problem is when one business entity components begins to use another business entity component increasing coupling of business entities, like on the picture below.

![Layered Architecture Components Coupled](/attachments/2023-06-01-layered-architecture/layered-architecture-coupled-components.png)


This coupling of components makes support of the system as a nightmare, also it will be hard to scale a team for this architecture.

# Pros

* Very fast speed of development.
* Very simple idea, so people can easy to understand it.
* Low learning curve.

# Cons

* Hard to scale due to high coupling between components.
* Hard to test due to high coupling between components.
* Hard to support (develop new features and fix bugs) system due to high coupling between components.

# Where to use layered architecture?

This is a hard question, because even with minuses related to high coupling this architecture has a big plus - simplicity. So I can highlight main usage of this architecture:

* Startups where speed of development is the most valuable property of a system.
* Small applications where no need sophisticated solution which need to support during long time.
* Microservices, due to an idea "one small service - one responsibility" this architecture ideally fits with microservices, because each service is small, so layered architecture will not become too expensive for support, due to small service.

# Where do not use layered architecture?

* In monoliths which continuously evolute, use modular architecture instead.
  * At the start of monolith live, it's OK to use layered architecture, but with time it should be reworked to increase team performance with a monolith application.
* In medium size services - everything related to monolith is also true for medium size service, because it's like a monolith, but small one.

## Conclusions

In this post I explained what layered architecture is and when to use it. Even when I know more sophisticated techniques, like modular architecture or approaches from DDD, I still can use this kind of an architecture for small applications or when I'm developing proof of concepts for my ideas. Also I think that this kind of an architecture is the best choice for startups due to high speed of a development. And I highly recommend do not use DDD for everything which need to develop, instead think about an application and consider probably more simpler ways to achieve a business target, because this is what engineers solves, not an architecture problem.