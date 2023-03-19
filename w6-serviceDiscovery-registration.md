###  Microservices
- microservices are a branch of independently running services.
- Each services exposes an API and runs in a dedicated port of a server 


### how to manage the interaction between microservices?

## Service Discovery and Registration
- to deal with the potential challenges, the concept called "Service Discovery and Registration" can be used 
- It hepls us to locate and manage various instances of running microservices.
### Service Discovery and Registration functioin works as follows:
- A central repo of all network address of each registered microservices should be maintained.
- Every new microservices instance or client that needs to be associated with this central repo should register its address with the server.
- the server will periodically poll all its clients for their status.

## Load balancer vs service discovery 

## setting up service discovery 

- In spring cloud, service discovery and registration can be implemented using many open sources.
### some of them are given below :
- Eureka Service(From Netfilx)
- Apache ZooKeeper
- Consul

## Step 1 : create mvc add few new dependencies
- Eureka Server
- Config Client 
- Spring Boot Actuator
## step 2 : add annotation in main class
- @EnableEurekaServer
## Step 3 : add this exclusions file inside eureka dependency

```
			<exclusions>
				<exclusion>
					<groupId>org.springframework.cloud</groupId>
					<artifactId>spring-cloud-starter-ribbon</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.netflix.ribbon</groupId>
					<artifactId>ribbon-eureka</artifactId>
				</exclusion>
			</exclusions>
```

 - Eureka ribbon : It is a cloud library that provides the client-side load balancing so to prevent we are using exclusions. 
## step 4 : add application.properties
```
spring.application.name=eurekaserver
spring.config.import=configserver:http://localhost:8087/
spring.cloud.loadbalancer.ribbon.enabled=false
spring.freemarker.template-loader-path= classpath:/templates/
spring.freemarker.prefer-file-system-access= false
```

## step 5 : create new file in git-config name as "eurekaserver.properties"
```

server.port = 8088
eureka.instance.hostname=localhost
eureka.client.registerWithEureka = false
eureka.client.fetchRegistry = false
eureka.client.serviceUrl.defaultZone=http://${eureka.instance.hostname}:${server.port}/eureka/

```

# Feign Clients

## step 1 : add dependency and add annotation @EnableFeignClients in main class 
```
        <dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-openfeign</artifactId>
		</dependency>
```
## step 2 : create a packge in.bank.accounts.service.client and create interface 
```java
package in.bank.accounts.service.client;

import java.util.List;

import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import in.bank.accounts.model.Cards;
import in.bank.accounts.model.Customers;



@FeignClient("cards")
public interface CardsFeignClient {
	 
	@RequestMapping(method = RequestMethod.POST , value = "cards" , consumes = "application/json")
	List<Cards> getCardDetails(@RequestBody Customers customer);
}
```


## step 3 : add Cards class to accounts application 

## step 4 : add CustomerDetails class in model package 
```java 
import java.util.List;

public class CustomerDetails {
	
	private Accounts accounts;
	private List<Cards> cards;
	public Accounts getAccounts() {
		return accounts;
	}
	public void setAccounts(Accounts accounts) {
		this.accounts = accounts;
	}
	public List<Cards> getCards() {
		return cards;
	}
	public void setCards(List<Cards> cards) {
		this.cards = cards;
	}
	
}
```


