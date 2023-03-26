---
layout: page
title: "Telegram Bot with Go and AWS Lambda"
categories: Go
---

# Introduction
During last time I launched different Telegram Bot, for solve my problems, for example Habit Bot (to control my habits) 
and I recognized that I'm solving similar problems from bot to bot. Futhermore when I started develop bots in Go, I recognized that there is no good tutorial about bot building in Go. Thus I decided to explain how I'm building Telegram Bots with Go and AWS Lambda.

# Problem definition
To make this post more interesting, let's create not just "echo bot", but bot which solves real problem, for example:

Bot should send new Hacker News posts every morning at 7am EST and bot shouldn't costs money for a deployment.

# Problem decomposition
For solve our problem bot should:
1. Read Hacker News posts.
2. Automatically triggers at 7am EST and send Hacker News posts.
3. Bot should register new users for send news.
4. Bot should be deployed at AWS Lambda, because free tier covers all bot cases, thus we will not pay money for it.

# Solution 
1. Telegram bot created with Bot Father registers webhook for which Telegram will send updates
2. Go code deployed as AWS Lambda and handles updates from Telegram


## Architecture
![Architecture](/attachments/2023-03-25-telegram-bot/architecture.png)

1. Telegram servers will send updates throughout WebHook, which will launch a bot
    * Throughout this channel of communication bot will register new users for receive a news
2. AWS Event Bridge will send scheduled event every day at 7am EST to send news
    * Bot will send news for all registered users
3. Bot will be deployed as AWS lambda and it will be launched on every trigger event: Telegram update or scheduled event
4. DynamoDB will store information about registered users

### Key decisions
1. Use AWS Lambda - this AWS service will results in free bot deployment or very cheap costs per month
2. DynamoDB - for hobby project it will be free per month, thus we can use it for or hobby projects. If we will use some RDS, it will costs us at least 10$ per month, while DynamoDB will be a free option.
3. AWS Event Bridge - bot should be triggered once per day at 7am EST, so there is no another option except external scheduler, because `in memory scheduler` will make our lambda decision useless and we will have a bot with costs at least 10$ per month for cheap EC2 machine.

## Business flows
### User registration flow
![User registration](/attachments/2023-03-25-telegram-bot/register-user-flow.png)
1. User sends Telegram Bot command `/start` in HTTP request throughout web hook
2. AWS Lambda starts Bot code
3. AWS Lambda wraps HTTP request in AWS event
4. AWS Lambda sends event with `/start` command to bot
5. Bot retrieves information about current `chat_id` which bot will use for send news
6. Bot saves chat id to DynamoDB
7. DynamoDB returns success response
8. Bot returns success response for user

# Architecture

# Resources
