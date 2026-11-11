---
chapter: 1
title: "Exam — Scale From Zero To Millions Of Users"
tags: [system-design, exam, sdi-alex-xu, chapter-1]
---

# 📝 Exam · Ch 1 — Scale From Zero To Millions Of Users

> [!info] How to use
> Answers are **folded**: click the callout to reveal. Try each section closed-book first.
> **Scoring:** Part A = 1 pt each (20) · Part B = 2 pts each (20) · Part C = 10 pts each (20) · **Total 60**
> 48+ = solid · 36–47 = re-read weak sections · <36 = re-read the chapter
> Summary: [[Ch01 - Scale From Zero To Millions Of Users]]

---

## Part A — Multiple Choice (1 pt each)

**A1.** In the single-server request flow, who usually hosts DNS?
a) Your web server b) Your database c) A paid 3rd-party service d) The CDN
> [!check]- Answer
> **c** — DNS is usually a paid service from 3rd parties, not hosted on your servers.

**A2.** Which is the most common API response format between mobile apps and the web server?
a) XML b) JSON c) YAML d) HTML
> [!check]- Answer
> **b** — JSON, because of its simplicity.

**A3.** Which is NOT one of the four NoSQL categories in the book?
a) Key-value b) Graph c) Relational d) Document
> [!check]- Answer
> **c** — The four are key-value, graph, column, and document stores.

**A4.** Which is NOT a reason to choose a NoSQL database?
a) Super-low latency b) Many joins across tables c) Unstructured data d) Massive amount of data
> [!check]- Answer
> **b** — Joins are generally *not supported* in NoSQL. The fourth reason is "only need to serialize/deserialize data".

**A5.** The main advantage of vertical scaling is:
a) Unlimited capacity b) Redundancy c) Simplicity d) Low cost
> [!check]- Answer
> **c** — Simplicity. It has a hard limit, no failover, and powerful servers are expensive.

**A6.** After adding a load balancer, how do the LB and web servers communicate?
a) Public IPs b) Private IPs c) DNS names d) geoDNS
> [!check]- Answer
> **b** — Private IPs, which are reachable only between servers on the same network. This improves security.

**A7.** In master/slave replication, a `DELETE` statement goes to:
a) Any slave b) The master c) The cache d) All nodes at the same time
> [!check]- Answer
> **b** — All data-modifying commands (insert, update, delete) go to the master.

**A8.** Why do systems usually have more slave DBs than master DBs?
a) Slaves are cheaper b) Reads vastly outnumber writes c) Masters can't replicate d) For sharding
> [!check]- Answer
> **b** — Most apps have a much higher read-to-write ratio.

**A9.** You have exactly one slave and it goes offline. Reads go to:
a) The cache only b) The CDN c) The master, temporarily d) Nowhere: reads fail
> [!check]- Answer
> **c** — Reads go to the master temporarily until a new slave replaces the old one.

**A10.** The caching strategy described in the chapter (check cache → on miss query DB → store → return) is called:
a) Write-through b) Write-back c) Read-through d) Cache-aside eviction
> [!check]- Answer
> **c** — Read-through cache (as the book names it).

**A11.** The most popular cache eviction policy is:
a) FIFO b) LFU c) LRU d) Random
> [!check]- Answer
> **c** — LRU (Least Recently Used).

**A12.** Setting a cache expiration that is **too short** causes:
a) Stale data b) Reloading data from the DB too often c) Memory overflow d) SPOF
> [!check]- Answer
> **b** — Too short means frequent DB reloads. Too long means stale data.

**A13.** Besides multiple cache servers across DCs, the book recommends which other way to mitigate cache failures?
a) Sticky sessions b) Overprovisioning memory by a certain % c) Sharding the cache by user_id d) Disabling expiration
> [!check]- Answer
> **b** — Overprovision the required memory as a buffer for growing usage.

**A14.** In the CDN workflow, what tells the CDN how long to cache an object?
a) ETag b) Optional TTL HTTP header from origin c) DNS record d) Cookie
> [!check]- Answer
> **b** — The origin returns the object with an optional Time-to-Live (TTL) header.

**A15.** `image.png?v=2` is an example of:
a) CDN fallback b) Object versioning c) Sharding key d) Geo-routing
> [!check]- Answer
> **b** — Object versioning is one of two ways to invalidate a CDN file. The other is the vendor's invalidation API.

**A16.** Which load balancer feature is needed to make a **stateful** architecture work?
a) Health checks b) Sticky sessions c) SSL termination d) Autoscaling
> [!check]- Answer
> **b** — Sticky sessions route the same client to the same server. They add overhead and make adding or removing servers harder.

**A17.** In the book's stateless design, which store is chosen for session data, and why?
a) RDBMS: joins b) NoSQL: easy to scale c) CDN: close to users d) Message queue: async
> [!check]- Answer
> **b** — NoSQL, because it is easy to scale. (Redis/Memcached or an RDBMS are also possible.)

**A18.** geoDNS resolves domain names to IPs based on:
a) Server load b) User's location c) Time of day d) Cookie
> [!check]- Answer
> **b** — User location, so users are routed to the closest data center.

**A19.** Which is NOT a type of metric listed in the chapter?
a) Host-level b) Aggregated-level c) Key business metrics d) Compiler-level
> [!check]- Answer
> **d** — The three are host-level (CPU, memory, disk I/O), aggregated-level (whole DB or cache tier), and business metrics (DAU, retention, revenue).

**A20.** The technique the book points to for solving **resharding** problems is:
a) De-normalization b) Consistent hashing c) Read replicas d) LRU
> [!check]- Answer
> **b** — Consistent hashing (covered in Chapter 5).

---

## Part B — Short Answer (2 pts each)

**B1.** Give the two serious limitations of vertical scaling as stated in the "Vertical vs horizontal scaling" section.
> [!check]- Answer
> 1. **Hard limit**: you can't add unlimited CPU/RAM to a single server.
> 2. **No failover/redundancy**: if the server goes down, the whole site goes down.
> *(The DB section adds: greater SPOF risk and high cost.)*

**B2.** List the three advantages of database replication.
> [!check]- Answer
> **Better performance** (parallel reads on slaves) · **Reliability** (data survives disasters because it's replicated across locations) · **High availability** (site stays up if one DB goes offline).

**B3.** Why is promoting a slave to master complicated in production, and how is it handled?
> [!check]- Answer
> The slave's data **might not be up to date**. The missing data has to be filled in by running **data recovery scripts**. Multi-master or circular replication can help, but they are more complex.

**B4.** Name the 5 considerations for using a cache.
> [!check]- Answer
> 1. **When to use** (read-heavy, rarely modified; cache is volatile)
> 2. **Expiration policy**
> 3. **Consistency** (DB and cache aren't updated in one transaction)
> 4. **Mitigating failures** (SPOF → multiple servers across DCs + overprovision memory)
> 5. **Eviction policy** (LRU, LFU, FIFO)

**B5.** Why can't a cache be your primary data store?
> [!check]- Answer
> Cached data lives in **volatile memory**. If the cache server restarts, all its data is lost. Important data must be kept in **persistent data stores**.

**B6.** Name the 4 considerations for using a CDN.
> [!check]- Answer
> **Cost** (pay for data in and out; remove rarely used assets) · **Appropriate cache expiry** · **CDN fallback** (clients detect an outage and fetch from origin) · **Invalidating files** (API or object versioning).

**B7.** Explain stateful vs stateless servers, and what stateless enables.
> [!check]- Answer
> A **stateful** server remembers client data (state) between requests, so the same client must always reach the same server. A **stateless** server keeps no state; it fetches state from a **shared data store**, so **any server can handle any request**. Stateless is simpler, more robust, and more scalable, and it makes **autoscaling** easy.

**B8.** What are the three technical challenges of a multi-data-center setup?
> [!check]- Answer
> 1. **Traffic redirection** (e.g. GeoDNS)
> 2. **Data synchronization** (replicate data across DCs, e.g. Netflix's async multi-DC replication)
> 3. **Test and deployment** (test at different locations; automated deployment keeps DCs consistent)

**B9.** In the photo-processing example, how does a message queue help with scaling?
> [!check]- Answer
> Web servers (**producers**) publish jobs. **Workers** (consumers) process them asynchronously. Producers and consumers **scale independently**: when the queue grows, add workers; when it's mostly empty, remove workers. Either side can keep working even if the other is down.

**B10.** List the three main challenges of sharding and a fix for each.
> [!check]- Answer
> | Challenge | Fix |
> |---|---|
> | **Resharding** (shard full / shard exhaustion from uneven distribution) | Consistent hashing |
> | **Celebrity / hotspot key** | Dedicated shard per celebrity (maybe further partitioned) |
> | **Joins across shards** | De-normalize so queries hit a single table |

---

## Part C — Design Scenarios (10 pts each)

**C1.** Your startup runs everything on **one server**. Traffic is growing fast, the server sometimes dies, and users in Europe complain that images load slowly (your server is in San Francisco). Write out, **in order**, the changes you'd make and *why*. Draw the final design in Mermaid if you like.

> [!check]- Model answer & rubric
> 1. **Split web and DB tiers** so each scales independently. *(1 pt)*
> 2. **Load balancer + ≥2 web servers**: failover and load spreading; servers sit on private IPs. *(2 pts)*
> 3. **DB replication (master + slaves)**: writes go to the master, reads to slaves; covers failover, performance, and reliability. *(2 pts)*
> 4. **Cache tier** for read-heavy data, with an expiration and eviction (LRU) policy and multiple cache nodes to avoid a SPOF. *(1.5 pts)*
> 5. **CDN for static assets**: Europe gets images from a nearby edge server; set TTLs, a fallback to origin, and versioning. *(2 pts)*
> 6. **Make the web tier stateless** (sessions in NoSQL/Redis) so it can autoscale. *(1.5 pts)*
>
> *Bonus thinking:* later on, multi-DC with geoDNS, message queues for slow work, and logs/metrics.

**C2.** You run a social app sharded with `user_id % 4`. Two problems appear: (a) shard 2 is at 95% disk while the others are at 40%, and (b) whenever a famous singer posts, shard 1 melts down. Also, (c) the analytics team complains their `JOIN` queries across users broke. Diagnose each and propose fixes. Then explain why picking `user_id` might or might not have been a good **sharding key**.

> [!check]- Model answer & rubric
> - **(a) Shard exhaustion from uneven data distribution.** Resharding is needed: update the sharding function and move data. Use **consistent hashing** (Ch 5) so adding shards moves minimal data. *(3 pts)*
> - **(b) Celebrity / hotspot key problem.** Give the celebrity (or each celebrity) a **dedicated shard**, possibly partitioned further. Caching hot reads helps too. *(3 pts)*
> - **(c) Joins across shards are hard.** **De-normalize** the data so queries run against a single table. Optionally move non-relational data or workloads to NoSQL. *(2 pts)*
> - **Sharding key:** the main criterion is **even data distribution**. `user_id` is spread out and routes most per-user queries to one shard (good). But it can't prevent hotspots from very active users, and `% N` makes resharding painful. *(2 pts)*

---

## 🎯 Rapid-fire (oral drill: answer out loud in <5 s each)

1. Scale up = ? → *vertical*
2. Scale out = ? → *horizontal*
3. Sharding = which kind of scaling? → *horizontal*
4. Who gets writes? → *master*
5. SPOF stands for? → *single point of failure*
6. TTL stands for? → *time to live*
7. LRU / LFU / FIFO are what? → *eviction policies*
8. CDN serves what kind of content (in this book)? → *static*
9. Stack Overflow 2013: how many master DBs? → *1*
10. Max RAM of an Amazon RDS server cited in the book? → *24 TB*
11. The single most important decision in sharding? → *the sharding key*
12. The 8-point chapter summary starts with? → *keep the web tier stateless*
