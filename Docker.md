# Docker and Microservices

## Step 1 : maven build
	- Go to this folder "src/test/java"

```java
          @SpringBootTest(classes = runnableclassname.class
```
	build success

## Step 2: go to pom.xml and add below version tag 
``` <packaging>jar</packaging> ```

## Step 3: java -jar jar-name

Step 4: Create a file name as “Dockerfile”
```
FROM eclipse-temurin:17
MAINTAINER bank.in
COPY target/AccountTest-0.0.1-SNAPSHOT.jar AccountTest-0.0.1-SNAPSHOT.jar

ENTRYPOINT ["java","-jar","AccountTest-0.0.1-SNAPSHOT.jar"]
```
## Step 5: go to cmd and create images
	

	``` docker build . -t username/projectname  ```      
	 “all in small letter”

## Step 6: execute docker image 

	``` docker run -p 8081:8081 username/project name ```




