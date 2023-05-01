---
layout: page
title: "Software Architecture: which should I use?"
categories: Go
---

# Introduction

During my career I saw different projects with different software architecture.
Every project has some points why to choose some kind of architecture. In this
post I want to describe my thougths about architecture which I would like to
choose if I will start a new project.

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

* Small team
* Need to develop product as fast as possible, for example release full product
  in 3 days (if you know what I mean :))
* Small budget for project

Monolith architecture is an ideal architecture for start ups and small
companies with small IT department, because this kind of architecture is the
most cheapest architecture.

## Pros

* Very fast development
  * Team of developers shouldn't to communicate with another departments for
    implement feature or no need to change infrastructure
* Simple infrastructure 
  * No need or minimal DevOps team, dev team can easily adjust simple CI/CD pipelines and
    deploy monolith to AWS ECS or EC2.
* Simple scaling: very big mistake is to think that monolith can't be scaled.
  * Monolith scales and does it very well, all what need to do is just to develop it it a right way.
* Cheap rent for servers

## Cons

* Complex code base, because all components are highly coupled
  * As far as everything is in one place it's very common situation when one
    thing in monolith appplication knows everything about system. This problem
    can be solved with modular monolith.
* Changes in one component requires retesting full system
  * This is not always true, but is true in a lot of cases. Modular monolith
    solves this.
* Usually full regress testing required before release a new version of
  monolith

# Modular monolith

# Microservices
