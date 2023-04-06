---
date: 23-03-2022
title: PGBouncer
tags: ['db', 'postgres']
---

Today I learned about connection pooling, what it does and why it's needed. I also learned specifically about PGBouncer.

## The Problem
Postgres "Postmaster" forks into a new process on every new connection. 

https://www.youtube.com/watch?v=ddKm7a7xOpk

What type of traffic does connection pooling help with?

Is there a scenario where connection pooling is worse than direct connections?