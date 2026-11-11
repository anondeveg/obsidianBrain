source: https://www.industrialempathy.com/posts/design-docs-at-google/
- **Wrtten:** 2026-10-07 12:25

SEE: [[design-docs-at-google]]

The design doc documents the high level implementation strategy and key design decisions with emphasis on the trade-offs that were considered during those decisions.

Besides the original documentation of a software design, design docs fulfill the following functions in the software development lifecycle:

Early identification of design issues when making changes is still cheap.

Achieving consensus around a design in the organization.

Ensuring consideration of cross-cutting concerns.

Scaling knowledge of senior engineers into the organization.

Form the basis of an organizational memory around design decisions.

Acts as a summary artifact in the technical portfolio of the software designer(s).

## Rule #1

Rule #1 is: Write them in whatever form makes the most sense for the particular project.

Having said that, a certain structure has established itself as really useful.

## Context and scope

This section gives the reader a very rough overview of the landscape in which the new system is being built and what is actually being built.

## Goals and non-goals

A short list of bullet points of what the goals of the system are, and, sometimes more importantly, what non-goals are. Note, that non-goals aren’t negated goals like “The system shouldn’t crash”, but rather things that could reasonably be goals, but are explicitly chosen not to be goals.

## The actual design

This section should start with an overview and then go into details.

## System-context-diagram

## APIs

If the system under design exposes an API, then sketching out that API is usually a good idea. In most cases, however, one should withstand the temptation to copy-paste formal interface or data definitions into the doc as these are often verbose, contain unnecessary detail and quickly get out of date.

## Data storage

Systems that store data should likely discuss how and in what rough form this happens.

## Code and pseudo-code

Design docs should rarely contain code, or pseudo-code except in situations where novel algorithms are described.

## Degree of constraint

One of the primary factors that would influence the shape of a software design and hence the design doc, is the degree of constraint of the solution space.

## Alternatives considered

This section lists alternative designs that would have reasonably achieved similar outcomes. The focus should be on the trade-offs that each respective design makes and how those trade-offs led to the decision to select the design that is the primary topic of the document.

This is where your organization can ensure that certain cross-cutting concerns such as security, privacy, and observability are always taken into consideration. These are often relatively short sections that explain how the design impacts the concern and how the concern is addressed.

## The length of a design doc

Design docs should be sufficiently detailed but short enough to actually be read by busy people. The sweet spot for a larger project seems to be around 10-20ish pages.

If you get way beyond that, it might make sense to split up the problem into more manageable sub problems. It should also be noted that it is absolutely possible to write a 1-3 page “mini design doc”.

## The design doc lifecycle

The steps in the lifecycle of a design document are:

Creation and rapid iteration

Review (may be in multiple rounds)

Implementation and iteration

Maintenance and learning