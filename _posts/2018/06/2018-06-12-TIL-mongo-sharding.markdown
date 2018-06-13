---
layout: post
title:  "TIL: A bit about MongoDB Sharding"
date:   2018-06-12 21:10:00 -0000
categories: TIL
---
I learned a bit about the process of sharding records using multiple MongoDBs today. From what I gathered from the phone call that I was sitting on this morning, nodes are used to basically power the different shards. These shards distribute the data between the two databases to try and offload the amount of traffic going to them. That way you can try to keep the the number of queries to your databases somewhat distributed... in theory.

💚