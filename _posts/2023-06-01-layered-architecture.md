---
layout: page
title: "Application development: Layered Architecture"
categories: Post
---

## Introduction

Layered Architecture - classic words in the commercial development. I used it during long time, because this is default choice for a new application in Spring, Flask or anything else. But after Autumn 2020 when I first time touched Domain Driven Design in Ajax Systems with modular monolith I changed my mind and decided that layered architecture is an architecture for low-skill engineers. I think so during long time, but what an interesting moment if this is for low-skill engineers, so why I chose this kind of architecture to launch some product about which I can't tell or why this architecture was chose by startups?
Answer is simple - because this kind of an architecture is a good architecture in right hands and it also has its pros and cons.

Also during reading a book "Software Architecture Fundamentals" I found proofs of my thoughts which I had about layered architecture during last year. So in this blog post I will explain what is layered architecture and when to use it. Also I will provide an implementation in Go.

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


