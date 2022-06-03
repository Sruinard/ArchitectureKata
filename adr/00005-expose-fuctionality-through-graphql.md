# ADR 00005: Expose API functionality through a GraphQL endpoint

## Status

Proposed

## Context

The non-profit domain covers a wide variety of use-cases (e.g. search, discoverability, case and portfolie management, etc). Due to the large number of cases, we need our service to be adaptable and easy to use by both consumers and providers. As new functionality is provided by non-profits, we want it to be made available to users as soon as possible.

## Decision

We decide to leverage GraphQL for exposing our functionality with consumers through a single endpoint for quering and mutating data. A key aspect in our decision to leverage GraphQL is it's simplicity of to compose multiple objects in a single object (i.e. [composite pattern]("https://en.wikipedia.org/wiki/Composite_pattern")) and it's ability to discover new functionality immediately once it becomes available through graph introspection which results in faster exposure to end users.

## Consequence

By using GraphQL we gain several benefits:

- specification based: When a client makes a call, the schema validates the call.
- strongly typed: All objects/entities are specified in a GraphQL Schema which helps guaranteeing the data is of the right time, reducing errors.
- composition and fetching only data you require: Its easy to compose multiple objects into a singly object (reducing the need to make multiple calls to various endpoints). In addition, clients can query for only the data they need, resulting in saving time and bandwith.
- introspective graph: As all entities are modelled using the GraphQL Schema Definition Language (SDL), the graphQL endpoint can be queried for its schema. This improve discoverability of new functionality.

### Rejected Tradeoff:

One could also expose the API through a RESTful API. We have rejected this option as it:

- limits composition or requires multiple api calls resulting in chatty services.
- Reduces discoverability with respect to a GraphQL based API as it doesn't provide a graph which can be queried for objects and schemas.

#### Benefits lost due to rejecting tradeoff:

- Most developers are familiar with RESTful APIs. Sticking with a RESTful service would have reduced the learning curve for developers. In addition, more information can be found about RESTful applications, resulting in a reduced likelihood of running into issues due to lack of concept maturity.
