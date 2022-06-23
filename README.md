# Shokunin: Spring 2022 - O'Reilly Architecture Katas

This repository contains the materials offered for submission, for our participation in the
[O'Reilly Spring 2022 Architecture KATA class](https://learning.oreilly.com/featured/architectural-katas/) course.

**Please note**
Due to personal circumstances we have not been able to get as far as we had hoped. Nevertheless we really appreciate the oppertunity to participate.

## Document outline

- [Executive summary](#executive-summary)

_Context and introduction_

- ['Splotlight Platform' - Program narrative](#splotlight-platform-program-narrative)
- [Ubiquitous Language](#ubiquitous-language-a-language-shared-by-all-stakeholders)
- [Personas](#personas)

_Technical implementation_

- [User Stories](#user-stories)
- [System boundaries](#defining-the-system-boundaries)
- [Context Diagram](#ddd-context-map-in-depth-level-3)

## Executive Summary

The proposed solution aims to facilitate people from under-represented demographics in finding non-profit organisations that can help them start or further their career in tech, as well as support non-profit organisations in sharing what they already provide to offer even better guidance and support for the community.

The platform helps candidates discover the most interesting non-profit organisations and the services they offer, tries to keep them engaged and track progress (also for their own insights). This is achieved by excelent search capabilities, non-profit-candidate matching suggestsions and notifications as well as activity insights.

The platform allows non-profits to showcase their community offerings, provides an excellent search experience for potential candidates they can serve, identify missing offerings in their portfolio and team-up with other non-profits to achieve a better overall service experience.

## 'Splotlight Platform' Program narrative

> “The test of our progress is not whether we add more to the abundance of those who have much; it is whether we provide enough for those who have too little.”
> ― Franklin D. Roosevelt

Diversity Cyber Council has launched a program named _Spotlight Platform_ with the goal to establish a sustainable and diverse talent pipeline that extends career equity to underrepresented demographics by providing access to competent training programs that lead to direct employment opportunities. The project name inherently says it all, there is an abundance of light, we just need to make sure it points at the right person. And for that, we are here to help. We'll guide you through our recommended approach of solving some of the challenges you are facing and transition towards a state in which you'll reap the benefits of the vision you have established.

## Ubiquitous Language (A language shared by all stakeholders)

The following list provides a list of definitions, to establish terms that are relevant for the content and ensure there are no misconceptions about what is meant by them.

- **Non-profit organisation** ("non-profit") Group of people that aims to help under-represented demographics in the tech industry by facilitating education, training, and staffing opportunities to establish a sustainable and diverse talent pipeline to the workforce without a profit motive.
- **Offering** collection of _services_ offered by a _non-profit_
- **Service** initiative deployed by a non-profit to help candidates overcome a particular challenge
- **Candidate** A member of an under-represented demographic that, consumer of non-profit offerings that is deliverd via the platform
- **Platform** An online system provided by the [Diversity Cyber Counsil](https://www.diversitycybercouncil.com/) both aimed at: helping, connecting and furthering candidates in their carreer in the tech industry, as well as support inter non-profit collaboration and sharing to fill in the gaps of service and overall impact.

_Idea borrowed from Eric Evan's book on Domain Driven Design - the Ubiquitous Language ([Domain-Driven Design : Tackling Complexity in the Heart of Software](https://www.dddcommunity.org/book/evans_2003/))_

## Personas

Two different profiles of the typical user of the platform (i.e. perona's) can be identified and described:

- **Non-profit (the facilitator)** Kobe, 42, grew up in the suburbs of Chicago. He has witnessed first hand how difficult it can be to break away from stigmas and get a better life. Since 5 years he has been investing his time in helping people from underrepresented backgrounds to land their dream job. One of the things he loves working on is providing teenagers a connected experience. An experience in which they feel supported and empowered. Jonathon is good add coaching and seeing how small pieces of the puzzle fit together.

- **Candidate (the lifelong-learner)** Janine, 28, works 2 jobs at a supermarket and local restaurant, has the smarts and is eager to 'get out' bus doesn't know how. She has an interest in technology and would love to have a career at a tech company, but does not have the right education for it and therefore was not able to land a job in tech. She works long hours and doesn't make enough money to afford expensive training during working hours and the time she has is often fragmented over a day and is.
  She believes that given a chance for an interview, she'll be able to convince the company that she'll be of great value and is willing to learn anything to prove that.

_Note:_ whereas the 'platform administrator' role is certainly also relevant required to operate the platform, no persona was created because a) there is no 'experience' of the platform that they will have to do their administrative tasks, that requires understanding of their character and b) time considerations.

## User stories

The following user-stories were top of mind when considering the usage of the platform:

### User Story 1: [Engagement]

As a **facilitator** I want to be able to share resources that have worked well for other candidates, so that candidates can take similer paths and be in a better situation to act/make decisions. --> sharing functionality

### User Story 2: [Discovery]

As a **facilitator** I want to be able to find/group/filter (discover/search) candidates with similar needs/profiles, so that I can recommend them services which can help them in improving their current situation. --> search + Proactive reachout

### User Story 3: [Matching]

As a **facilitator** I want to know which candidates are potential consumers, such that I know who to target and I'm in the best place to help these candidates solve their problems / reach their goals

### User Story 4: [Grow]

As a **lifelong-learner** I want to know what my weakpoints are, such that I can create a curriculum to overcome these weaknesses and have a change of landing my dream job.

### User Story 5: [Reward]

As a **lifelong-learner** I want to know how much progress I have made, such that I remain motivated to reach my goals and can celebrate milestones along the way.

### User Story 6: [Matching]

As a **lifelong-learner** I want to know which offerings best match the problem I try to solve/goal I try to reach, such that I can make deliberate decisions which enable me to solve my problem or reach my goal

## Defining the system boundaries

We'll be leveraging a context diagram to create a simplified representation of our system which is understandable for a wide audience (i.e. technical and non-technical stakeholders). At first, we focus on the stakeholders we try to empower and leave the operational part out of scope (i.e. admin user). The context diagram as depicted in Figure 1:

![Figure 1: Diversity Cyber Council Context Diagram](./assets/context_diagram.png)

## Domain Driven Design (DDD) Context Map (level 1 + 2)

On a high level, the [context diagram](#defining-the-system-boundaries) provides a very rough overview of the actors and key components. In this section, we'll group them together in domains. The domains provide clear boundaries between services and teams, improve isolation and deployability, and simplify accountability.

The main parts identified in the context diagram, can roughly be grouped together in the following domains: Non-profits, Candidates, Matching and Insights.

- **Non-profits domain** stores all information about the non-profit organisations, their offerings and services within the platform. It provides onboarding- and search capabilities and is responsible for notifying the activity context about internal events.

- **Candidates domain** stores all information about the candidates, looking to benefit from the non-profit offerings. It offers search an discovery capabilities, asset storage capabilities (like resume etc.) and request submission capabilities. Also responsible for notifying the activity context about internal events.

- **Matching domain** service that is able to suggest non-profit-with-non-profit maches as well as candidate-with-non-profit matches. Retrieves data from candidate and non-profit context in order to achieve this. Also responsible for notifying the activity context about internal events.

- **Insights domain** provides insights for candidates, non-profits as well as platform administrators for both operational as well as analytical purposes. It leverages all the beforementioned domains as well as the activities domain (see below).

- **Activities domain** receives event notifications from all domains which enables a myriad of event-driven use-cases like notifications, time-series-analytics and engagement insights.

The domain driven design context map looks as follows: 

![DDD context map](./assets/DDD-context-map.png).

Please note the following (technical) relations:

- There is a _partnership_ regarding the schema design and implementation between the _matching context_ and _Non-profit/Candidate context_. Althought the Matching context is the consumer, both the non-profits and candidate context reap the benefits from a good matching algorithm, resulting in eagerness from both parties to partner up.

- The _activity context_ implements an _Anti-corruption layer_ to translate any concepts from other domains to its own domain. The activity context plays an important role as it is the central place from which insights can be derived (reports, but also search, discoverabilty and fill-in-the-gap)

- The _Insight Context_ has a _conformist_ relationship with the _Activity Context_'s domain. Because it is a consumer without any power over the activity context and therefore needs to conform (i.e. take it or leave it).

### DDD context-map in depth (level 3)

Based on the [C4 Model](https://c4model.com/) we can 'zoom in' from the context down to code/implementation. This looks as follows:

![c4](./assets/c4.png)

Level 1 and 2 (grey and green boxes) have been covered in previous sections of this document. 


Level 3 (the blue box) shows already some of the details of an implementation and the interaction between contexts, for which Architecture Decision Record (ADRs) have been written:

- The contexts are implemented as autonomous, independent services, i.e. 'microservices'.<br>
  [ADR0001 Microservices architecture](adr/00001-microservices-architecture-style.md)

- The frontend will communicate to all the backend services through a single endpoint - a federated GraphQL endpoint:<br>
  [ADR0002 Federated GraphQ Endpoint for Search and Discovery - NOT WRITTEN](adr/00002-Integration-discoverability-and-search-through-federated-graphql.md)

- All the backend services post internal events onto a messaging solution that is consumed by the 'activity' service<br>
  [ADR0003 Redis used for internal events - NOT WRITTEN](adr/00003-Redis-for-events.md)


Level 4 (red box) shows further detail of the components within a service, also for which ADRs have been written. The diagram focusses on the 'non-profit' domain:

- The service exposes a GraphQL endpoint for querying and modifying the data.<br>
  [ADR0005 Expose service data through GraphQL](adr/00005-expose-fuctionality-through-graphql.md)

- Non-profit data is persisted in data stores optimized for usage<br>
  [ADR0006 RDBMS choice for non-profit data - NOT WRITTEN]()<br>
  [ADR0007 ElasticSearch for querying non-profits](adr/00007-Elastic-for-non-profit-search.md)




**Please note**
Due to personal circumstances we have not been able to get as far as we had hoped. This is as far as we got.

<!--
Based on [federated graphql](./adr/00002-Integration-discoverability-and-search-through-federated-graphql.md) and [domains-expose-apis-through-subgraphs](./adr/00003-all-domains-expose-graphql-subgraphs.md), we come to the conclusion that integration between services is largely achieved through GraphQL federation. Each domain has its distinct subgraph which can be queried by external consumers through the graph api.

Moreover, all domains publish activity events to a message queue which is owned and consumed by the activity context. We choose to do this asynchronously as the activity context is not a user facing application. Besides using a message queue for publishing activities, we also leverage it for our notification service within the activity context.

Finally, a batch job is responsible for ingesting data in the data warehouse within the Insights context. This data will be used for generating the analytic reports.

## Domain services (level 4)

summary:
Per domain:

- one line what each block in the domain does
- what kind of storage we will leverage
- how service is exposed/communicates with other services

## Deployment Diagram

summary:

- explain platform choice
- explain why chosen services
- explain one other option
- link to bff adr which explains why went for backend for frontend

![Deployment diagram](./assets/Azure_deployment_diagram.png)

[Backend for Frontend (BFF)](./adr/0004-backend-for-frontend.md)

## How graphql enables innovation through integration

Summary:

- explain how discoverability improved
- explain how data integrity improved
- explain how offering search was improved
- Explain how insights generation was improved

## Federated GraphQL

Reference: [Diversity Cyber Council Kata Requirements 2022](https://docs.google.com/document/d/1XjEpcGJ87xYg1eWN9eE0_tH7te5HcVAgPvoONLHY4qQ/edit#)

### parking

These will be considered our domains (we'll cover how search and exploration is enabled through our technology choice in [Federated GraphQL](#federated-graphql)).
Additional to the previously mentioned 4 domains, we identified another domain: 'Activity' as it plays a vital role within the entire solution.
Consequently, we want to give it a separate domain to emphasize it's importance and have a dedicated team work on it to improve progress and innovation.


!-->
