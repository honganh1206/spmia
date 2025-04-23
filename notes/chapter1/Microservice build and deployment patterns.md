Each instance of a microservice should be identical to all its other instances

Immutable infrastructure: Once a service is deployed, the infrastructure it's running on is **never** touched again by human hands

Our goal: Integrate the configuration of the infrastructure into the build-deployment process so we do not have to deploy artifacts on already running infrastructure

Build and deployment pipeline - Create a repeatable build and deployment process

Infrastructure as code - Treat the provisioning of our services as code capable of being executed and managed under source control

Immutable servers - Ensure deployed microservice image does not change

Phoenix servers - Ensure servers running microservices get torn down and recreated on a regular basis

![[Pasted image 20250422132812.png]]

