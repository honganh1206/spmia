
Client-side load balancing - Cache the location of your service instances so that calls to multiple instances are load balanced to all the healthy instances

Circuit breakers pattern - Prevent a client from doing a call to a poorly performing service. Make the failing service fail fast

Fallback pattern - provide plug-in mechanism so the service client can carry out its work through alternative means

Bulkhead pattern - Microservice applications use *multiple distributed resources* to carry out their work, so we need to **compartmentalize** the calls so that *the misbehavior of one service does not affect other services e.g., taking up all the resources*

![[Pasted image 20250417175015.png]]

```java
// This method will not be directly invoked
// Instead delegated to a thread pool managed by Hystrix
// All calls to this method will occur in thread pool
@HystrixCommand(threadPoolKey = "helloThreadPool")
public String helloRemoteServiceCall(String firstName,
String lastName){
	ResponseEntity<String> restExchange =
	restTemplate.exchange(
	"http://logical-service-id/name/
	[ca]{firstName}/{lastName}",
	HttpMethod.GET,
	null, String.class, firstName, lastName);
	
	return restExchange.getBody();
}
```