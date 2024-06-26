# service-registry
Spring Cloud Netflix Eureka Server is a key component of the Spring Cloud ecosystem, providing a highly available and scalable service registry for microservices architecture. It allows services to register themselves and discover each other without the need for hard-coded hostnames and ports. This is crucial for building and managing microservices, as it enables services to communicate with each other dynamically.

### Overview of Eureka Server

- **Service Registry**: Eureka Server acts as a service registry, where each microservice registers itself. This registration includes details such as the service's hostname, port, and health status.
- **Service Discovery**: Services can query Eureka Server to discover other services they need to communicate with. This is done without the need for the services to know each other's hostnames and ports.
- **Load Balancing**: Eureka Server can also provide client-side load balancing, distributing requests among multiple instances of a service.
- **Health Checks**: Eureka Server periodically checks the health of the registered services. If a service fails its health check, Eureka Server will remove it from the registry, preventing it from receiving traffic.

### Setting Up Eureka Server

To set up an Eureka Server, you typically create a Spring Boot application and include the `spring-cloud-starter-netflix-eureka-server` dependency in your `pom.xml` or `build.gradle` file. Here's an example of how to add the dependency using Maven:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

And for Gradle:

```gradle
implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-server'
```

### Configuring Eureka Server

In your Spring Boot application, you need to enable the Eureka Server by adding the `@EnableEurekaServer` annotation to one of your configuration classes. Additionally, you need to configure the Eureka Server properties in your `application.properties` or `application.yml` file. Here's an example configuration:

```yaml
server:
 port: 8761

eureka:
 instance:
    hostname: localhost
 client:
    registerWithEureka: false
    fetchRegistry: false
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```

This configuration sets the Eureka Server to run on port 8761 and disables the registration and fetching of the registry by the Eureka Server itself, which is typical for a standalone Eureka Server.

### Registering Services with Eureka Server

To register a service with the Eureka Server, you need to include the `spring-cloud-starter-netflix-eureka-client` dependency in your service's `pom.xml` or `build.gradle` file. Then, configure the Eureka Client properties in your service's `application.properties` or `application.yml` file to point to your Eureka Server. Here's an example:

```yaml
eureka:
 client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
```

This configuration tells the service where to find the Eureka Server and allows it to register itself with the server upon startup.

### Conclusion

Spring Cloud Netflix Eureka Server plays a vital role in microservices architecture by providing a service registry and discovery mechanism. It simplifies the process of managing and scaling microservices, allowing them to communicate with each other dynamically and efficiently. By setting up and configuring an Eureka Server, you can enhance the scalability and reliability of your microservices applications.