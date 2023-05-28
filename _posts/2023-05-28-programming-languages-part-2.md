---
layout: page
title: "Choosing programming language"
categories: Post
---

## Introduction

In the previous post I explained a my story with different programming languages and in the this post I want to explain my thoughts about choosing next programming language for a new project.

**What cases I will not cover?**

1. You have a team familiar with a some language and you should deliver business solution as fast as possible.
2. You just want some technology.

This cases don't give a possibility to choose an another programming language.

## Choosing programming languages

#### Case 1

**Main target:** launch a company as fast as possible and hire new engineers to give them development tasks and focus on business development.

**Type:** pet project with a dream to build own company.

**Team:** one engineer or small group of engineers which works on part-time.

**Architecture:** monolith, microservices are useless in such case, because with them time to solve operational problems, like deployments, communication between services will eat all time of small team. So for this case only a monolith architecture is a viable solution.

**Programming languages:** Python or Java.

Python is a very good tool to develop small projects and with Python it will be easy to hire new engineers.
Java can be an another very good option, because it simplifies development of monolith applications due to Spring Framework and there are a lot of engineers to hire available on market.

**Engineers level:** middle, in case of new company money is a very big problem.

**Hiring availability:** a lot of middle engineers in Python and Java.

**Important note:** a very big mistake here is to choose Go or Node.js to develop a project, which I did many times in a past. Here need a technology to very quickly launch a project and then scale a team to focus on the business, not on a development technologies.

#### Case 2

**Main target:** build project quickly to increase company income, in future scale a team.

**Size:** project in a small/medium company.

**Team:** small team.

**Architecture:** it depends on a problem which we are trying to solve, but in case of small company which means small amount of money which it can spend I would like to recommend use still monolith architecture due to simplicity and speed of development.

**Programming languages:** Java.

I prefer to use Java in case of small team in company, due to highly structurized project and again Spring Framework which will significantly increase speed of development. Also as far as this is company development deadlines and expectations from top management is present, so we need to use a technology which can be stable and predictable in estimates. Probably in future this project will be split to microservices, so for now Java is the best option.

**Engineers level:** middle/senior, to grows need top skilled people.

**Hiring availability:** a lot of highly skilled engineers in Java, but need to filter them from middle level engineers which can be a challenging task due to big amount of engineers available on a market.


#### Case 3

**Size:** big company.

**Team:** big team.

**Architecture:** microservices or service oriented architecture. This is a strict requirement, because with monolith it will be very hard to parallelize development of features between different teams.

**Programming languages:** Go, Python, Java.

In case of microservices architecture choosing of programming languages becomes more flexible, because services are small and engineers can play with different technologies. From speed of development I still prefer to use Java, but probably Go will be an awesome choice here too, for hire top-talents and keep good engineers in a company.

**Engineers level:** middle engineers to solve boring tasks, senior engineers to drive company evolution.

**Hiring availability:** all technologies have top level engineers, but speed of hiring depends on technology, in case of Go there can be a lot of top level engineers and probably it will be more easily to filter them from middle-level. In a case of Java it may be harder.


## Summary

In this post I explained how to choose  languages for different project types.
