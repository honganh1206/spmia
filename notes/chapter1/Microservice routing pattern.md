Answer the question "How do I get my client's request for a service to a specific instance of a service?"

Service discovery - Make the microservice discoverable so that client applications can find them without hardcoding the service's location

Service routing - Provide a single entry point for all your services

```java
// The RestTemplate class contacts the Eureka service and look up the physical location of the "name" service instances
ResponseEntity<String> restExchange = restTemplate.exchange
(http://logical-service-id/name/{firstName}/{lastName}
```