---
layout: page
title: "A little bit about resilience testing in Go"
categories: Go
---

# Introduction
What are resilience tests? This is tests which covers unusual application behavior, for example: database outage, message broker outage and so on.
This kind of tests may sounds very important, but usually I didn't wrote them for my applications previously. I think that a lot of developers didn't created them too, because:
* Priorities were feature development
* E2E/IT tests were already created and them already tests infrastructure, so there is no reason to create dedicated tests for infrastructure failure
* Infrastructure failure is rare case, so there is no reason to spend efforts for cover this cases
and a lot of another similar reasons, why we should skip resilience tests. 

A reason "Priorities were feature development" is completely OK for skip resilience tests, because business money is not infinite, so I will not cover this reason in a my post.
But another two reasons will be covered in a this post.


## Usual E2E/IT tests covers infrastructure outage

No them not covers, main purpose of this tests are cover functionality of an application. 
And them tests application in a good conditions when database connection is alive which is not always a case in real production runtime. Usually tests don't cover loosing connection and then restoring connection and process business flow, but this conditions are usual for runtime. To have a possibility to test application resilience I can't rely on usual E2E which tests business flow, I need create separated E2E which tests application resilience.

## Infrastructure failure is rare case

Previously I think and heard a lot of this words:
- Infrastructure failure is rare
- If we will have outage of X we will have more problems rather than outage of Y, so there is no reason to think how to handle outage X

This words are partially right, but what if I say that infrastructure failure is not so rare, this is a common thing for modern applications? What if I say that we can think about handling outage of X to reduce downtime for our users and eliminate chain downtime of our services?


Resilience tests can make a software system more robust and decrease times for wake up developers at 3 A.M. to fix production environment and even more them can make users happy by reducing services downtime, because applications will know how to handle infrastructure downtime.

Theory sounds good, but in this post I will explain only how to write E2E test which will test loosing of connection to a message broker and then restoring it. To do so I created simple service which accepts HTTP requests and publishes message to a message broker.

# Service overview
An example service contains a simple HTTP endpoint which receives a request and sends it to NATS message broker.
I chose NATS as example of infrastructure component which can have an outage during system runtime, because NATS client has very interesting property: after lose a connection with NATS broker client tries to retry and when retry limit was reached client moves to `CLOSED` state and never tries to retry again. Which means that service which used NATS client goes to permanent outage, because service can't restore connection with NATS message broker by default NATS client configuration. I already saw service outage with loosing NATS connection some time ago, that's why I chose a NATS as example.



# Resources
* 