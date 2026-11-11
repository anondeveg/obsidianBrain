---
chapters: [2, 3]
title: "Exam — Ch 2 Estimation + Ch 3 Interview Framework"
tags: [system-design, exam, sdi-alex-xu, chapter-2, chapter-3]
---

# 📝 Exam · Ch 2 (Estimation) + Ch 3 (Interview Framework)

> [!info] How to use
> Answers are **folded**: click to reveal. Do Part C with **pen and paper and no calculator**, like the real interview.
> **Scoring:** Part A = 1 pt each (20) · Part B = 2 pts each (20) · Part C = 5 pts each (20) · Part D = 10 pts (10) · **Total 70**
> 56+ = solid · 42–55 = re-read weak sections · <42 = re-read both chapters
> Summaries: [[Ch02 - Back-of-the-envelope Estimation]] · [[Ch03 - A Framework For System Design Interviews]]

---

## Part A — Multiple Choice (1 pt each)

### Chapter 2

**A1.** According to Jeff Dean, back-of-the-envelope calculations combine thought experiments with:
a) Load testing b) Common performance numbers c) Production logs d) Benchmarks of your own code
> [!check]- Answer
> **b**: common performance numbers, to get a feel for which designs will meet your requirements.

**A2.** 2⁴⁰ bytes is approximately:
a) 1 GB b) 1 TB c) 1 PB d) 1 MB
> [!check]- Answer
> **b**: 2⁴⁰ ≈ 1 trillion = 1 terabyte.

**A3.** How much memory does one ASCII character use?
a) 1 bit b) 4 bits c) 1 byte d) 2 bytes
> [!check]- Answer
> **c**: 1 byte (8 bits).

**A4.** Which is the slowest?
a) Disk seek b) Round trip within the same data center c) Read 1 MB sequentially from memory d) Main memory reference
> [!check]- Answer
> **a**: disk seek ≈ 10 ms. DC round trip 500 µs, 1 MB from memory 250 µs, memory reference 100 ns.

**A5.** Reading 1 MB sequentially from disk takes about:
a) 250 µs b) 10 ms c) 30 ms d) 150 ms
> [!check]- Answer
> **c**: 30 ms. (10 ms is 1 MB from the network; 150 ms is a CA → Netherlands → CA packet.)

**A6.** 1 ms equals:
a) 1,000 ns b) 1,000 µs c) 10⁻⁶ s d) 100 µs
> [!check]- Answer
> **b**: 1 ms = 1,000 µs = 1,000,000 ns = 10⁻³ s.

**A7.** Which is NOT one of the chapter's conclusions from the latency numbers?
a) Avoid disk seeks b) Compress data before sending it over the internet c) Network is always faster than disk d) Simple compression algorithms are fast
> [!check]- Answer
> **c**: not a conclusion. The five are: memory fast/disk slow, avoid disk seeks, simple compression is fast, compress before sending over the internet, cross-region transfers take time.

**A8.** An SLA is an agreement between:
a) Two internal teams b) You (the service provider) and your customer c) You and your cloud provider only d) Developers and QA
> [!check]- Answer
> **b**: it formally defines the uptime level your service will deliver.

**A9.** Amazon, Google and Microsoft set their SLAs at:
a) 99% b) 99.5% c) 99.9% or above d) 100%
> [!check]- Answer
> **c**: 99.9% or above.

**A10.** A service with 99.99% availability can be down about how long per year?
a) 3.65 days b) 8.77 hours c) 52.6 minutes d) 5.26 minutes
> [!check]- Answer
> **c**: 52.6 minutes. (99% = 3.65 days, 99.9% = 8.77 h, 99.999% = 5.26 min.)

**A11.** In the book's Twitter example, peak QPS is estimated as:
a) QPS + 1,000 b) 2 × QPS c) 10 × QPS d) QPS² 
> [!check]- Answer
> **b**: Peak QPS = 2 × QPS ≈ 7,000.

**A12.** "99987 / 9.1" in an interview should be:
a) Computed precisely to 2 decimals b) Simplified to 100,000 / 10 c) Skipped d) Done on a phone calculator
> [!check]- Answer
> **b**: rounding and approximation; precision is not expected.

### Chapter 3

**A13.** What matters most in a system design interview, according to the book?
a) The final design b) The design process c) Naming real technologies d) Finishing fast
> [!check]- Answer
> **b**: the final design is less important than the work you put into the design process.

**A14.** Which red flag does the chapter call "a real disease of many engineers"?
a) Asking too many questions b) Over-engineering c) Drawing diagrams d) Using estimations
> [!check]- Answer
> **b**: over-engineering: delighting in design purity, ignoring trade-offs and their compounding costs.

**A15.** The interviewer answers your question with "make an assumption". You should:
a) Pick anything silently b) Write the assumption down c) Ask again d) Skip the feature
> [!check]- Answer
> **b**: write it on the whiteboard or paper; you might need it later.

**A16.** In the news-feed example, how is the feed sorted?
a) By weight b) By likes c) Reverse chronological order d) Random
> [!check]- Answer
> **c**: reverse chronological, to keep things simple.

**A17.** For which problem does the book say API endpoints and DB schema are "fair game" during the high-level step?
a) Google search engine b) Multi-player poker game backend c) YouTube d) Web crawler
> [!check]- Answer
> **b**: poker backend. For Google search they're too low-level.

**A18.** For a senior candidate, the deep dive often focuses on:
a) UI design b) Performance characteristics: bottlenecks and resource estimations c) Coding the API d) Choosing a programming language
> [!check]- Answer
> **b**.

**A19.** In a 45-minute interview, the book's rough time for the design deep dive is:
a) 3–5 min b) 3–10 min c) 10–15 min d) 10–25 min
> [!check]- Answer
> **d**: scope 3–10, high-level 10–15, deep dive 10–25, wrap up 3–5.

**A20.** When is the interview done?
a) After you present the design b) After the deep dive c) When the interviewer says you're done d) At exactly 45 minutes
> [!check]- Answer
> **c**: ask for feedback early and often.

---

## Part B — Short Answer (2 pts each)

**B1.** Name the three sets of numbers you need for back-of-the-envelope estimation.
> [!check]- Answer
> **Powers of two**, **latency numbers every programmer should know**, and **availability numbers**.

**B2.** Define high availability and how it's measured.
> [!check]- Answer
> The ability of a system to be **continuously operational for a desirably long period**. Measured as a **percentage of uptime** (100% = zero downtime; most services are between 99% and 100%), traditionally counted in **"nines"**.

**B3.** List the four estimation tips from Chapter 2.
> [!check]- Answer
> 1. **Rounding and approximation** 2. **Write down your assumptions** 3. **Label your units** 4. **Practice commonly asked estimates** (QPS, peak QPS, storage, cache, number of servers)

**B4.** Using the latency table, explain why Chapter 1 recommends a cache tier.
> [!check]- Answer
> Memory is far faster than disk: reading 1 MB from **memory takes 250 µs** vs **30 ms from disk** (~120× slower), and a **disk seek costs 10 ms**. Serving hot data from memory avoids disk seeks and cuts response time and DB load.

**B5.** What does the system design interview simulate, and what signals does the interviewer want beyond technical skill?
> [!check]- Answer
> It simulates **two co-workers collaborating on an ambiguous problem** to find a solution that meets their goals. Signals: ability to **collaborate**, **work under pressure**, **resolve ambiguity constructively**, and **ask good questions**.

**B6.** Give the four starter questions for Step 1.
> [!check]- Answer
> 1. What **specific features** are we building? 2. How many **users**? 3. How fast will it **scale** (3 months, 6 months, a year)? 4. What's the **tech stack**, and which **existing services** can we use?

**B7.** List the four things you should have achieved before starting the deep dive.
> [!check]- Answer
> Agreed on **goals and feature scope** · sketched a **high-level blueprint** · got **feedback** on it · have **initial ideas for deep-dive areas** based on that feedback.

**B8.** Give the two deep-dive examples the book uses, and one example of *too much* detail.
> [!check]- Answer
> **URL shortener** → the hash function that converts long URLs to short ones. **Chat system** → reducing latency and online/offline status. Too much detail: explaining **Facebook's EdgeRank** ranking algorithm.

**B9.** Name at least five directions for the wrap-up step.
> [!check]- Answer
> Identify **bottlenecks & improvements** (never call it perfect) · **recap** the design · **error cases** (server failure, network loss) · **operations** (monitoring metrics and logs, rollout) · **next scale curve** (1M → 10M users) · **other refinements** with more time.

**B10.** "There's neither a right answer nor a best answer." Explain using the book's example.
> [!check]- Answer
> A solution for a **young startup** differs from one for an **established company with millions of users**. The right design depends on the **requirements**, so understand them first.

---

## Part C — Estimation Problems (5 pts each)

> [!tip] Show your steps: assumptions → DAU → QPS → peak → storage. Round aggressively.

**C1. The book's example from memory.** 300M MAU, 50% daily, 2 tweets/day, 10% with media (1 MB), 5-year retention. Compute DAU, QPS, peak QPS, media storage/day, 5-year media storage.
> [!check]- Answer
> - DAU = 300M × 50% = **150M**
> - QPS = 150M × 2 ÷ 86,400 ≈ **3,500**
> - Peak = 2 × 3,500 ≈ **7,000**
> - Media/day = 150M × 2 × 10% × 1 MB = **30 TB/day**
> - 5 years = 30 TB × 365 × 5 ≈ **55 PB**

**C2. Photo app.** 100M DAU. Each user uploads 1 photo per day on average; each photo is 2 MB. Users view 50 photos/day. Keep photos 10 years. Estimate: write QPS, read QPS, peak read QPS, storage per day, 10-year storage.
> [!check]- Answer
> - Write QPS = 100M ÷ 10⁵ s ≈ **~1,000** (exact: 100M ÷ 86,400 ≈ 1,160)
> - Read QPS = 100M × 50 ÷ 10⁵ ≈ **~50,000** (exact ≈ 58,000)
> - Peak read ≈ 2 × 50K = **~100,000 QPS**
> - Storage/day = 100M × 2 MB = 200M MB = **200 TB/day**
> - 10 years = 200 TB × 365 × 10 ≈ 730,000 TB ≈ **730 PB** (~0.7 EB)
> *Grading: 1 pt each. Round numbers are fine if the method is right.*

**C3. Availability.** Your SLA promises 99.9%. (a) Max downtime per day and per year? (b) Last month you were down 3 hours. Did you meet the SLA? (c) What does moving to 99.99% buy you per year?
> [!check]- Answer
> (a) **1.44 min/day**, **8.77 h/year**.
> (b) A month allows about 8.77 h ÷ 12 ≈ **44 minutes**. 3 hours **breaks the SLA** for that month.
> (c) 8.77 hours → **52.6 minutes**: about **10× less downtime**.

**C4. Latency reasoning.** A request makes 5 sequential DB queries. Each query does one disk seek. The user is in Europe and the servers are in California. Roughly how long does it take, and what would you change?
> [!check]- Answer
> - Cross-continent round trip ≈ **150 ms**
> - 5 disk seeks × 10 ms = **50 ms**
> - In-DC round trips: 5 × 0.5 ms ≈ 2.5 ms (negligible)
> - Total ≈ **~200 ms**, dominated by geography.
> Fixes (Ch 1 + Ch 2): serve from a **data center or CDN near Europe**; **cache** query results in memory (100 ns–250 µs instead of 10 ms); **avoid disk seeks**; **batch or parallelize** queries; **compress** responses.

---

## Part D — Interview Simulation (10 pts)

**D1.** The interviewer says: *"Design Instagram."* Write the **first 5 minutes** of your interview: the exact questions you'd ask, the assumptions you'd write down, a quick estimate, and what you'd say before starting the high-level design. Then list three things you would **not** do.

> [!check]- Model answer & rubric
> **Clarifying questions (3 pts)**: mobile, web or both? Core features (upload photos, follow users, view a feed)? Feed order (reverse chronological or ranked)? How many users / DAU? Growth in 3, 6, 12 months? Photos only, or video too? Existing tech stack or services to reuse?
> **Assumptions written down (2 pts)**: e.g. 100M DAU, 1 upload/user/day at 2 MB, 50 views/day, reverse chronological feed, photos only.
> **Estimate (2 pts)**: ~1K write QPS, ~50K read QPS (~100K peak), ~200 TB/day of new photos → a read-heavy system, so CDN, cache and object storage matter. Ask first: "Is an estimate useful here?"
> **Transition (1 pt)**: "Let me sketch a high-level design: two flows, upload and feed. Then I'd like your feedback before we go deeper."
> **Don'ts (2 pts)**: jump straight into a solution; dive into one component (e.g. a ranking algorithm) too early; think in silence; over-engineer; claim the design is perfect; assume you're done before the interviewer says so.

---

## 🎯 Rapid-fire (answer out loud in under 5 seconds)

1. 2²⁰ ≈ ? → *1 million / 1 MB*
2. Main memory reference? → *100 ns*
3. Disk seek? → *10 ms*
4. Round trip in the same DC? → *500 µs*
5. CA → NL → CA packet? → *150 ms*
6. 99% downtime per year? → *3.65 days*
7. 99.999% downtime per year? → *5.26 minutes*
8. Peak QPS ≈ ? → *2 × QPS*
9. Step 1 of the framework? → *understand the problem and establish design scope*
10. The kid you shouldn't be? → *Jimmy*
11. Deep dive time in 45 min? → *10–25 min*
12. Never say this in the wrap-up? → *"my design is perfect"*
