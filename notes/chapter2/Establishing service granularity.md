Goal: Take major pieces of functionality (Assets, License, Contract, Organization) and extract them into completely self-contained units. Such units can be built and deployed independently of each other

Take note when building a microservice architecture

1. Start broad with your microservice and refactor to smaller services - Decomposing the problem domain into small services often leads to **premature complexity**
2. Focus first on how the services will interact with each other 
3. Service responsibilities will change over time as your understanding of the problem domain grows - The original microservice acts as an orchestration layer for the new services

[[The smells of a bad microservice]]