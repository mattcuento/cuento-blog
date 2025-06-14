---
title: "Building a DBMS from Scratch: Part 2 - The Start of a Storage Engine"
date: 2025-06-13
draft: true
tags: []
summary: 
author: 'Matt Cuento'
---

In the previous [post](2025-06-06-building-dbms-pt-1.md), we discussed a vision and roadmap for a distributed, interchangeable, key-value DBMS. In this post we'll focus on parts of the storage engine and how we manage deployments.

# Deployments
Step one, how can we quickly get our software running? I've chosen to start this project in the JVM, using Java. I'm a total beginner here, but many of my favorite tools are written in Java (Kafka, Flink, Cassandra), so I thought I'd give it a go.

## Decision Point - Processes or Containers?
I'm using [Gradle](https://gradle.org/) to manage the project, and then raised the question of whether I want to run nodes on different processes, or in containers. I think the answer is both, but for the sake of learning more about the JVM, I chose to begin with processes. I've marked containerization as a future task.

## Configuration


## Health Checks

# The Storage Engine

## Durability

## Optimizing Recovery - Snapshots

## Persistence Data Structures
