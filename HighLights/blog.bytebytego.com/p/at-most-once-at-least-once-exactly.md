---
title: "At most once, at least once, exactly once - by Alex Xu"
url: "https://blog.bytebytego.com/p/at-most-once-at-least-once-exactly"
domain: "blog.bytebytego.com"
created: "2026-08-19 15:06"
tags:
  - web-highlight
  - notaty
---

# At most once, at least once, exactly once - by Alex Xu

- **Source URL:** [https://blog.bytebytego.com/p/at-most-once-at-least-once-exactly](https://blog.bytebytego.com/p/at-most-once-at-least-once-exactly)
- **Captured:** 2026-08-19 15:06

---

## Highlights

# at most once

> "As the name suggests, at-most once means a message will be delivered not more than once. Messages may be lost but are not redelivered. This is how at-most once delivery works at the high level.

Use cases: It is suitable for use cases like monitoring metrics, where a small amount of data loss is acceptable." `[YELLOW]`
— *Captured at 2026-08-19 15:05*

> "With this data delivery semantic, it’s acceptable to deliver a message more than once, but no message should be lost.

Use cases: With at-least once, messages won’t be lost but the same message might be delivered multiple times. While not ideal from a user perspective, at-least once delivery semantics are usually good enough for use cases where data duplication is not a big issue or deduplication is possible on the consumer side. For example, with a unique key in each message, a message can be rejected when writing duplicate data to the database." `[YELLOW]`

my opinion: **this option should be the default and most popular option because deduplication from consumer side is usually trivial, so this strucks a balance between UserExperience and simplicity.**

— *Captured at 2026-08-19 15:05*

> "Exactly once is the most difficult delivery semantic to implement. It is friendly to users, but it has a high cost for the system’s performance and complexity.

Use cases: Financial-related use cases (payment, trading, accounting, etc.). Exactly once is especially important when duplication is not acceptable and the downstream service or third party doesn’t support idempotency." `[YELLOW]`
— *Captured at 2026-08-19 15:06*

