---
title: "Building a Database Management System (DBMS) From Scratch Pt. 1"
date: 2025-06-12
tags: [databases, distributed systems, projects]
summary: Building Database Internals - APIs, Durability, and Crash Recovery
author: 'Matt Cuento'
---

# The Vision

My college's motto was "Learn By Doing". What's more fitting to learn about database internals than building a DBMS from scratch? Crash recovery, sharding, replication, storage, and query processing -- I'm hoping to build basic implementations of these features wrapped into a single DBMS. 

What I think is the most novel piece of this project, is the idea of composability. One of my main goals here is to make different components interchangeable and extensible. Want to see what the trade-offs are of using B-trees vs. LSM-trees? Want to know the consistency tradeoffs of synchronous replication vs. asynchronous replication? 

The vision here is to build a system that allows one to simulate different use cases and failure scenarios under different conditions.

# The Requirements

I don't exactly have a customer except my own curiosity, so, what _am_ I curious to get out of this project?

Well, one of my largest interests is distributed systems. This project will be a distributed DBMS _by default_. We could just go ahead and say "I'm prioritizing for availability" here. 

![Distributed Systems](/distributed-systems.jpg)

I also don't want this project to have a massive barrier to entry. I'm most interested in the distributed systems trade-offs (_"what consistency challenges do I face with this replication model?"_) and the low-level details (_"Do I lose read-ahead caching when I use Direct I/O?"_), but not so much the in-between. 

In my mind, making this DBMS key-value based is a good starting point to trim some extra scope (e.g. schema management). Overall, I think the requirements can be summarized as follows:

- **Distributed**: The DBMS should be able to run on multiple nodes and handle distributed reads/writes and replication.
- **Key-Value Store**: The DBMS should be a key-value store, we will avoid schema management for now.
- **Configurable**: The DBMS should allow for different storage engines, replication models, and consistency levels to be swapped in and out easily.
- **Failure Simulation**: Aside from writing the DBMS itself, we should create tooling to simulate real-world failures to test the trade-offs of different architectural configurations.

# The Plan

The idea of building a DBMS from scratch is daunting, but the key to how I break up projects like this is thinking about my goals and the components I need to build. What feature gives me the most bang for my buck in terms of effort? 

Given this is a D(atabase)BMS, I think it makes sense to begin with the database itself. We also need to build the foundation that can easily configure and launch a deployment. Here are the questions I want to answer first.

- **Deployment Manager**: How can I spin up other nodes in a cluster? How do I determine health? How will nodes connect? What mechanism do we use to configure a deployment?
- **Storage Engine**: Do we want durability? What data structures will we use to store data? Will we support indexes? Do we prioritize read or write performance?
- **Crash Recovery**: How do we ensure that the database can recover from crashes? What logging mechanisms do we need?

# What's Next?

Now that we have some definition, it's time to build! In the next post, we'll explore how we manage deployments and the basics of a storage engine. Stay tuned!
