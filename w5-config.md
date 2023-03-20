## step 1 : 
- create a maven application "configserver"
- add dependency 
"config server"
"spring boot actuator"
## step 2 :
- add @EnableConfigServer at runnable class

## Step 3 :
-add config files at src/main/java/resource paste with application.properties

## step 4:
- add properties in application.properties
```
spring.application.name=configserver
spring.profiles.active=native
server.cloud.config.server.git.uri=classpath:/config
server.port = 8087
```
- run

## step 5 : to get config details from git 
- create repo in git and upload config file 
- add these properties to application.properties file 
```
spring.application.name=configserver
spring.profiles.active=git
spring.cloud.config.server.git.uri=https://github.com/Abhishek8602/config.git
spring.cloud.congig.server.git.default-label=master
spring.cloud.congig.server.git.clone-on-start=true
server.port = 8087
```

- run

## wired(accounts and cards)
- add these line to pom.xml file just after dependency tag in configserver

```
<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
```

- add these lines in application.properties of accounts

```
spring.application.name=accounts
spring.profile.active=prod
spring.config.import=optional:configserver:http://localhost:8087
```
