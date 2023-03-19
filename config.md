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

## step 1: we have to configure our application in order to read all the json data coming from the configserver
- create package called config
- create  class name as AccountsConfigServer
```java
@Configuration
@ConfigurationProperties(prefix = "accounts")
public class AccountsConfigServer {
	 private String msg;
	 private String buildVersion;
	 private Map<String, String> mailDetails;
	 private List<String> activeBranches;
	public String getMsg() {
		return msg;
	}
	public void setMsg(String msg) {
		this.msg = msg;
	}
	public String getBuildVersion() {
		return buildVersion;
	}
	public void setBuildVersion(String buildVersion) {
		this.buildVersion = buildVersion;
	}
	public Map<String, String> getMailDetails() {
		return mailDetails;
	}
	public void setMailDetails(Map<String, String> mailDetails) {
		this.mailDetails = mailDetails;
	}
	public List<String> getActiveBranches() {
		return activeBranches;
	}
	public void setActiveBranches(List<String> activeBranches) {
		this.activeBranches = activeBranches;
	}
	 
}
```

## step 2 : create a model 
- create class "ConfigProp"
```java

public class ConfigProp {

	private String msg;
	private String buildVersion;
	private Map<String, String> mailDetails;
	private List<String> activeBranches;

	public String getMsg() {
		return msg;
	}

	public void setMsg(String msg) {
		this.msg = msg;
	}

	public String getBuildVersion() {
		return buildVersion;
	}

	public void setBuildVersion(String buildVersion) {
		this.buildVersion = buildVersion;
	}

	public Map<String, String> getMailDetails() {
		return mailDetails;
	}

	public void setMailDetails(Map<String, String> mailDetails) {
		this.mailDetails = mailDetails;
	}

	public List<String> getActiveBranches() {
		return activeBranches;
	}

	public void setActiveBranches(List<String> activeBranches) {
		this.activeBranches = activeBranches;
	}

	public ConfigProp(String msg, String buildVersion, Map<String, String> mailDetails, List<String> activeBranches) {

		this.msg = msg;
		this.buildVersion = buildVersion;
		this.mailDetails = mailDetails;
		this.activeBranches = activeBranches;
	}

	// here in model we are mapping all the fields getting from controller with constructor

}
```


