---
title: "Tutorial: Developing a RESTful API with Go and Gin - The Go Programming Language"
url: "https://go.dev/doc/tutorial/web-service-gin"
domain: "go.dev"
created: "2026-08-19 14:59"
tags:
  - web-highlight
  - notaty
---

# Tutorial: Developing a RESTful API with Go and Gin - The Go Programming Language

- **Source URL:** [https://go.dev/doc/tutorial/web-service-gin](https://go.dev/doc/tutorial/web-service-gin)
- **Captured:** 2026-08-19 14:59

---

## Highlights

> "gin.Context is the most important part of Gin. It carries request details, validates and serializes JSON, and more. (Despite the similar name, this is different from Go’s built-in context package.)" `[YELLOW]`
— *Captured at 2026-08-19 14:16*

> "Call Context.IndentedJSON to serialize the struct into JSON and add it to the response." `[YELLOW]`
— *Captured at 2026-08-19 14:16*

> "Note that you can replace Context.IndentedJSON with a call to Context.JSON to send more compact JSON. In practice, the indented form is much easier to work with when debugging and the size difference is usually small." `[YELLOW]`
— *Captured at 2026-08-19 14:19*

> "// Call BindJSON to bind the received JSON to
    // newAlbum." `[YELLOW]`
— *Captured at 2026-08-19 14:31*

> "Use Context.Param to retrieve the id path parameter from the URL. When you map this handler to a path, you’ll include a placeholder for the parameter in the path." `[YELLOW]`
— *Captured at 2026-08-19 14:45*

