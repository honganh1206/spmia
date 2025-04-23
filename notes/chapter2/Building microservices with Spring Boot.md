Sometimes delivered software artifacts are:

- Tightly coupled - Increase the chance that a small change in one piece can break other pieces
- Leaky - Since a CRM application might manage multiple types of data in the same data model, one team might attempt to access data from another team
- Monolithic - One change to the code means the entire application has to be recompiled, tested and redeployed

A microservice architecture allows:

- Services to be constrained with a single set of responsibilities
- Services to be loosely coupled
- Abstracting services with each service having its own data structures and sources
- Services to be independent

To build a good microservice architecture, we must incorporate the perspectives of multiple individuals within the organization, like a successful police detective trying to get to the truth by considering multiple factors

We must consider three perspective: [[The Architect]], [[The Software Developer]] and [[The DevOps Engineer]]

[[When not to use microservices]]