# ADR 00001: Leverage a microservices architecture style to improve deployability, leverage domain driven design to keep teams relatively small and improve time to market.

## Status
Proposed

## Context
Diversity Cyber Council wants to build a platform which models a complex landscape. 
It has to manage a wide variety of use-cases, needs to integrate with many non-profit offerings which are expected to increase over time while keeping end user ease-of-use central.
To help people as quickly as possible, time to market is critical and new offerings should be added without much delay.

## Decision
We'll leverage a [microservices architecture style](https://en.wikipedia.org/wiki/Microservices) to improve deployability of the solution and time to market of its features. In addition, teams will be built around domains (Domain driven design) to facilitate a ubiquitous language within team boundaries and abstract away.

## Consequences
Opting for a microservices architecture style has the following positive consequences:
- Improve independent deployability and lower time to market (when done right, services can have independent lifecycle-management)
- Improve testability (service testing in isolation)
- Ideal for containerization
- Indepedentent scalability of the services

The negative consequences of this decision (downsides) are:
- Increased deployment complexity (more components to deploy)
- Increased service integration complexity (sevices communicate by contract, which will be subject to changes over time)
- Increased operational complexity (hosting is not as easy as single VM, monitoring and debugging now becomes distributed) 

_Rejected:_
- Monolithic:
    - We deliberately choose to not go for a monolith architecture as it limits the agility of teams to deploy new functionality.
    In addition, codebase can grow unwieldly in a short time and onboarding of new developers can be more challenging.
    
- Serverless:
    - Many of the application parts can be created using serverless functions (e.g. AWS lambda, Azure functions, Google cloud functions).
    However, there are some downsides. serverless functions often have a hard runtime limit making it not suitable to run long-running processes.
    - It ties you to a specific vendor (vendor lock-in), whereas containered deployments can be deployed to any cloud provider
    - Due to future use of long-running tasks, engineers basically need to be adapt in a wider variety of tooling/services.