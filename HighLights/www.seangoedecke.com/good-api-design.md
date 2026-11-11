---
title: "Everything I know about good API design"
url: "https://www.seangoedecke.com/good-api-design/"
domain: "www.seangoedecke.com"
created: "2026-10-16 16:09"
tags:
  - web-highlight
  - notaty
---

# Everything I know about good API design

- **Source URL:** [https://www.seangoedecke.com/good-api-design/](https://www.seangoedecke.com/good-api-design/)
- **Captured:** 2026-10-16 16:09

---

## Highlights

> "Designing APIs is a balance between familiarity and flexibility

If this is true about systems — and it is — it’s even more true about APIs: good APIs are boring. An API that’s interesting is a bad API (or at least it would be a better one if it were less interesting)." `[YELLOW]`
— *Captured at 2026-10-12 06:08*

> "For the developers who build them, APIs are complex products that they spend time designing and polishing. But for the developers who use them, APIs are tools that they use in order to accomplish some other goal. Any time they spend thinking about the API instead of about that goal is time wasted." `[YELLOW]`
— *Captured at 2026-10-12 06:09*

> "For the developers who build them, APIs are complex products that they spend time designing and polishing. But for the developers who use them, APIs are tools that they use in order to accomplish some other goal. Any time they spend thinking about the API instead of about that goal is time wasted." `[YELLOW]`
— *Captured at 2026-10-12 06:09*

> "APIs are hard to change." `[YELLOW]`
— *Captured at 2026-10-12 06:09*

> "any change to the interface will break your users’ software" `[YELLOW]`
— *Captured at 2026-10-12 06:10*

> "each change imposes a serious cost: every time you force your users to update their software, they will give serious thought to using a different API that’s more stable. That gives API-builders a strong incentive to design carefully and get it right the first time." `[YELLOW]`
— *Captured at 2026-10-12 06:10*

> "This tension leads to an interesting dynamic for engineers who build APIs. On the one hand, they want to build the simplest API possible. On the other hand, they want to do clever things to maintain flexibility long-term. In broad strokes, API design is about finding a balance between those two incompatible goals." `[YELLOW]`
— *Captured at 2026-10-12 06:10*

> "WE DO NOT BREAK USERSPACE" `[YELLOW]`
— *Captured at 2026-10-12 06:11*

> "Additive changes — for instance, putting a new field in the response — are typically fine." `[YELLOW]`
— *Captured at 2026-10-12 06:11*

> "However, you can’t remove or change the types of fields. You can’t change the structure of existing fields (for instance, moving user.address to user.details.address in the JSON response). If you do, every single piece of code that relies on those fields will immediately break." `[YELLOW]`
— *Captured at 2026-10-12 06:12*

> "The “referer” header in the HTTP specification is famously a misspelling of the word “referrer”, but they haven’t changed it, because we do not break userspace." `[YELLOW]`
— *Captured at 2026-10-12 06:16*

> "API versioning means “serve both the old and new version of your API at the same time”. Existing consumers can continue to use the old version, while new consumers can opt-in to the new one. The easiest way to do this is to include something like /v1/ in your API url." `[YELLOW]`
— *Captured at 2026-10-12 06:17*

> "OpenAI’s chat API is at v1/chat/completions, so if they ever want to totally rework the structure, they can do that in v2/chat/completions and keep the existing consumers working." `[YELLOW]`
— *Captured at 2026-10-12 06:17*

> "In short, you should only use API versioning as a last resort." `[YELLOW]`
— *Captured at 2026-10-12 06:23*

> "The success of your API depends entirely on the product" `[YELLOW]`
— *Captured at 2026-10-12 06:23*

> "Poorly-designed products will usually have bad APIs" `[YELLOW]`
— *Captured at 2026-10-12 06:25*

> "a technically-poor product can make it nearly impossible to build an elegant API. That’s because API design usually tracks the “basic resources” of a product (for instance, Jira’s resources would be issues, projects, users and so on). When those resources are set up awkwardly, that makes the API awkward as well." `[YELLOW]`
— *Captured at 2026-10-12 06:25*

> "Technical constraints that can be cleverly hidden in the UI are laid bare in the API, forcing API consumers to understand far more of the system design than they should reasonably have to." `[YELLOW]`
— *Captured at 2026-10-12 06:26*

> "You should let people use your APIs with a long-lived API key. Yes, API keys are not as secure as various forms of short-lived credentials, like OAuth (which you should probably also support). It doesn’t matter. Every integration with your API begins life as a simple script, and using an API key is the easiest way to get a simple script working. You want to make it as easy as possible for engineers to get started." `[YELLOW]`
— *Captured at 2026-10-12 06:27*

> "Idempotency and retries" `[YELLOW]`
— *Captured at 2026-10-12 06:28*

> "If you’re hitting some Jira API to create an issue comment, and the request 500s or times out, should you retry? You don’t know for sure whether the comment has been created or not, since the error might be happening after that operation." `[YELLOW]`
— *Captured at 2026-10-12 06:29*

> "The solution is idempotency, which is a fancy word for “the request should be safely retriable without creating duplicates”." `[YELLOW]`
— *Captured at 2026-10-12 06:29*

> "The standard way to do this is to support an “idempotency key” in the request (say, some user-defined string in a parameter or header). When the API server gets a “create comment” request with an idempotency key, it first looks to see if it’s seen this idempotency key before. If so, it does nothing" `[YELLOW]`
— *Captured at 2026-10-12 08:05*

> "How should you store the key? I’ve seen people store it in some durable, resource-specific way (e.g. as a column on the comments table), but I don’t think that’s strictly necessary. The easiest way is to put them in Redis or some similar key/value store (with the idempotency key as the key). UUIDs are unique enough that you don’t need to scope them by user, but you may as well. If you’re not dealing with payments, you can even expire them after a few hours, since most retries happen immediately." `[YELLOW]`
— *Captured at 2026-10-12 08:06*

> "you don’t need them for read requests, since double-reads are harmless." `[YELLOW]`
— *Captured at 2026-10-12 08:06*

> "You also typically4 don’t need them for delete requests, since if you’re deleting by resource ID, that ID serves as the idempotency key." `[YELLOW]`
— *Captured at 2026-10-12 08:07*

> "For most cases, idempotency should be optional. Like I said above, you want to make sure that your API is accessible to non-engineers (who often find idempotency a tricky concept)." `[YELLOW]`
— *Captured at 2026-10-12 08:08*

> "Safety and rate limiting" `[YELLOW]`
— *Captured at 2026-10-12 08:08*

> "Any operation you expose via an API can be called at the speed of code." `[YELLOW]`
— *Captured at 2026-10-12 08:08*

> "Be careful about APIs that do a lot of work in a single request. When I worked at Zendesk, we had an API that let you fan out notifications to all the users of a particular app. Some enterprising third-party developer5 used this to build an in-app chat system, where every message sent a notification to every other user on the account. For accounts with more than a handful of active users, this reliably killed the Apps backend server." `[GREEN]`
— *Captured at 2026-10-12 08:10*

> "You should put a rate limit on your API, with tighter limits for expensive operations." `[YELLOW]`
— *Captured at 2026-10-12 08:11*

> "It’s also sensible to reserve the ability to temporarily disable the API for specific customers, so you can take the pressure off your backend system if it’s really getting hammered." `[YELLOW]`
— *Captured at 2026-10-12 08:11*

> "Include rate limiting metadata in your API responses. X-Limit-Remaining and Retry-After headers give clients the information they need to be respectful consumers of your API, and allow you to set stricter rate limits than you would otherwise be able to" `[YELLOW]`
— *Captured at 2026-10-12 08:11*

> "The simplest way to paginate is to use pages (or “offsets”, more generically). When you hit /tickets, you get the first ten tickets on the account. To get more, you have to hit either /tickets?page=2 or /tickets?offset=20. This is easy to implement, since the server can just add OFFSET 20 LIMIT 10 to the end of the database query. But it doesn’t scale to really high numbers of records." `[YELLOW]`
— *Captured at 2026-10-12 08:12*

> "Relational databases have to count through your offset every time, so each page you serve gets a little slower than the last page. By the time your offset is in the hundreds of thousands, it’s a real problem." `[YELLOW]`
— *Captured at 2026-10-12 08:12*

> "The solution is “cursor-based pagination”. Instead of passing offset=20 to get the second page, you take the final ticket on the first page (say, with ID 32) and pass cursor=32. The API will then return the next ten tickets, starting with ticket number 32. Instead of using OFFSET, the query becomes WHERE id > cursor ORDER BY id LIMIT 10. That query is equally quick whether you’re at the start of the collection or hundreds of thousands of tickets in, because the database can instantly find the (indexed) position of your cursor ticket instead of having to count through the entire offset." `[YELLOW]`
— *Captured at 2026-10-12 08:13*

> "You should always use cursor-based pagination for datasets that might end up being large." `[YELLOW]`
— *Captured at 2026-10-12 08:13*

> "It’s usually wise to include a next_page field in your API list responses. That saves consumers having to figure out the next page number or cursor on their own." `[YELLOW]`
— *Captured at 2026-10-12 08:14*

> "If parts of your API response are expensive to serve, make them optional. For instance, if fetching the user’s subscription status requires your backend to make an API call, consider making your /users/:id endpoint not return subscription unless the request passes an include_subscription parameter." `[YELLOW]`
— *Captured at 2026-10-12 08:14*

> "As a more general approach, you could have an includes array parameter with all your optional fields." `[YELLOW]`
— *Captured at 2026-10-12 08:14*

> "This is part of the idea behind GraphQL, a style of API where instead of hitting different endpoints per-operation, you craft a single query with all the data you need and the backend figures it out6." `[YELLOW]`
— *Captured at 2026-10-12 08:14*

> "Internal APIs" `[YELLOW]`
— *Captured at 2026-10-12 08:15*

> "internal APIs can still be a source of incidents, and still need to be idempotent for key operations." `[YELLOW]`
— *Captured at 2026-10-12 08:16*

> "Summary

    APIs are hard to build because they’re inflexible but must be easy to adopt
    API maintainers’ primary duty is to NOT BREAK USERSPACE. Never make breaking changes to public APIs
    Versioning your API lets you make changes, but imposes significant implementation and adoption barriers
    If your product is valuable enough, it doesn’t really matter how good your API is, people will use it anyway
    If your product is badly-designed enough, it doesn’t matter how carefully you design your API, it will likely suck
    Your API should support simple API keys for authentication, because many of your users will not be professional engineers
    Requests that take action (particularly high-stakes action like payments) should include some kind of idempotency key to make retries safe
    Your API will always be a source of incidents. Make sure you have rate limits and killswitches in place
    Use cursor-based pagination for datasets that might end up being very large
    Make expensive fields optional and off-by-default, but (in my opinion) GraphQL is overkill
    Internal APIs are different in some ways (because your consumers are very different)" `[GREEN]`
— *Captured at 2026-10-12 08:16*

