# Spring

* IoC Container
* Reduce or replace configuration
* The original concept was how to work better with EJBs
* Enterprise Development without Application Server
* Tomcat is a Standard Java Development Container
* Completely POJO-based
* Is for better, cleaner code with POJO (plain old java objects) & Interface Driven
* Used Best Practices

## Spring Framework 5

> Spring is a *lightweight* framework. It can be thought of as a *framework of frameworks* because it provides support to various frameworks such as [Struts](https://www.javatpoint.com/struts-2-tutorial), [Hibernate](https://www.javatpoint.com/hibernate-tutorial), Tapestry, [EJB](https://www.javatpoint.com/ejb-tutorial), [JSF](https://www.javatpoint.com/jsf-tutorial)
>
> 

### Spring Core

#### Architecture
![image-20200917022705577](Spring.assets/image-20200917022705577.png)

![image-20200917104746920](Spring.assets/image-20200917104746920.png)

**Core Container**
The Core Container consists of the Core, Beans, Context, and Expression Language modules the details of which are as follows −
* The Core module provides the fundamental parts of the framework, including the IoC and Dependency Injection features.
* The Bean module provides BeanFactory, which is a sophisticated implementation of the factory pattern.
* The Context module builds on the solid base provided by the Core and Beans modules and it is a medium to access any objects defined and configured. The ApplicationContext interface is the focal point of the Context module.
* The SpEL module provides a powerful expression language for querying and manipulating an object graph at runtime.

**Data Access/Integration**
The Data Access/Integration layer consists of the JDBC, ORM, OXM, JMS and Transaction modules whose detail is as follows −

* The JDBC module provides a JDBC-abstraction layer that removes the need for tedious JDBC related coding.
* The ORM module provides integration layers for popular object-relational mapping APIs, including JPA, JDO, Hibernate, and iBatis.
* The OXM module provides an abstraction layer that supports Object/XML mapping implementations for JAXB, Castor, XMLBeans, JiBX and XStream.
* The Java Messaging Service JMS module contains features for producing and consuming messages.
* The Transaction module supports programmatic and declarative transaction management for classes that implement special interfaces and for all your POJOs.

**Web**
The Web layer consists of the Web, Web-MVC, Web-Socket, and Web-Portlet modules the details of which are as follows −

* The Web module provides basic web-oriented integration features such as multipart file-upload functionality and the initialization of the IoC container using servlet listeners and a web-oriented application context.
* The Web-MVC module contains Spring's Model-View-Controller (MVC) implementation for web applications.
* The Web-Socket module provides support for WebSocket-based, two-way communication between the client and the server in web applications.
* The Web-Portlet module provides the MVC implementation to be used in a portlet environment and mirrors the functionality of Web-Servlet module.

**Miscellaneous**
There are few other important modules like AOP, Aspects, Instrumentation, Web and Test modules the details of which are as follows −

* The AOP module provides an aspect-oriented programming implementation allowing you to define method-interceptors and pointcuts to cleanly decouple code that implements functionality that should be separated.
* The Aspects module provides integration with AspectJ, which is again a powerful and mature AOP framework.
* The Instrumentation module provides class instrumentation support and class loader implementations to be used in certain application servers.
* The Messaging module provides support for STOMP as the WebSocket sub-protocol to use in applications. It also supports an annotation programming model for routing and processing STOMP messages from WebSocket clients.
* The Test module supports the testing of Spring components with JUnit or TestNG frameworks.

#### IoC Container & Lifecycle
The Spring container is at the core of the Spring Framework. The container will create the objects, wire them together, configure them, and manage their complete life cycle from creation till destruction. The Spring container uses DI to manage the components that make up an application. These objects are called Spring Beans, which we will discuss in the next chapter.

The container gets its instructions on what objects to instantiate, configure, and assemble by reading the configuration metadata provided. The configuration metadata can be represented either by XML, Java annotations, or Java code. The following diagram represents a high-level view of how Spring works. The Spring IoC container makes use of Java POJO classes and configuration metadata to produce a fully configured and executable system or application.

* Responsible for instantiating, configuring & assembling the beans
* The container is instructed through configuration metadata
* The configuration metadata is represented as XML or Java Annotations
* It allows to express objects that compose your application & rich interdependencies between those objects
* Dependency Injection (DI)

Spring IoC container is totally decoupled from the format in which this configuration metadata is actually written. Following are the three important methods to provide configuration metadata to the Spring Container −

XML based configuration file.
Annotation-based configuration
Java-based configuration

##### Dependency Injection (DI)
When writing a complex Java application, application classes should be as independent as possible of other Java classes to increase the possibility to reuse these classes and to test them independently of other classes while unit testing. Dependency Injection (or sometime called wiring) helps in gluing these classes together and at the same time keeping them independent.

Two methods to achieve DI:
1. Constructor-based dependency injection
Constructor-based DI is accomplished when the container invokes a class constructor with a number of arguments, each representing a dependency on the other class.

```java
public class TextEditor {
   private SpellChecker spellChecker;
   
   public TextEditor() {
      spellChecker = new SpellChecker();
   }
}
```
What we've done here is, create a dependency between the TextEditor and the SpellChecker. In an inversion of control scenario, we would instead do something like this −
```java
public class TextEditor {
   private SpellChecker spellChecker;
   
   public TextEditor(SpellChecker spellChecker) {
      this.spellChecker = spellChecker;
   }
}
```
Here, the TextEditor should not worry about SpellChecker implementation. The SpellChecker will be implemented independently and will be provided to the TextEditor at the time of TextEditor instantiation. This entire procedure is controlled by the Spring Framework.

Here, we have removed total control from the TextEditor and kept it somewhere else (i.e. XML configuration file) and the dependency (i.e. class SpellChecker) is being injected into the class TextEditor through a Class Constructor. Thus the flow of control has been "inverted" by Dependency Injection (DI) because you have effectively delegated dependances to some external system.

2. Setter-based dependency injection
Setter-based DI is accomplished by the container calling setter methods on your beans after invoking a no-argument constructor or no-argument static factory method to instantiate your bean.

You can mix both, Constructor-based and Setter-based DI but it is a good rule of thumb to use constructor arguments for mandatory dependencies and setters for optional dependencies.

The code is cleaner with the DI principle and decoupling is more effective when objects are provided with their dependencies. The object does not look up its dependencies and does not know the location or class of the dependencies, rather everything is taken care by the Spring Framework.

**DI is one of the implementation mechanism for IoC, where objects define their dependent objects with which they work. This is done by an assembler rather than by the objects themselves**
* Methods of DI 
  * Setter methods
  * Constructor Arguments
* Advantages
  * The object does not lookup its dependencies
  * The object does not know the location of the dependencies **(Location Transparency)**

#### Spring XML Configuration
applicationContext.xml
* Name doesn’t matter
* Spring context sort of a HashMap
* Can simply be a registry
* XML Configuration begins with this file Namespaces aid in configuration/validation

#### Java Configuration
Java-based configuration option enables you to write most of your Spring configuration without XML.

**@Configuration & @Bean**
Annotating a class with the @Configuration indicates that the class can be used by the Spring IoC container as a source of bean definitions. The @Bean annotation tells Spring that a method annotated with @Bean will return an object that should be registered as a bean in the Spring application context. The simplest possible @Configuration class would be as follows −
```java
package com.tutorialspoint;
import org.springframework.context.annotation.*;

@Configuration
public class HelloWorldConfig {
   @Bean 
   public HelloWorld helloWorld(){
      return new HelloWorld();
   }
}
```
**Injecting Bean Dependencies**
When @Beans have dependencies on one another, expressing that the dependency is as simple as having one bean method calling another as follows −
```java
package com.tutorialspoint;
import org.springframework.context.annotation.*;

@Configuration
public class AppConfig {
   @Bean
   public Foo foo() {
      return new Foo(bar());
   }
   @Bean
   public Bar bar() {
      return new Bar();
   }
}
```
Here, the foo bean receives a reference to bar via the constructor injection.

**@Import**
The @Import annotation allows for loading @Bean definitions from another configuration class. Consider a ConfigA class as follows −
```java
@Configuration
public class ConfigA {
   @Bean
   public A a() {
      return new A(); 
   }
}
```
You can import above Bean declaration in another Bean Declaration as follows −
```java
@Configuration
@Import(ConfigA.class)
public class ConfigB {
   @Bean
   public B b() {
      return new B(); 
   }
}
```

**Specifying Bean Scope Using @Scope**
The default scope is singleton, but you can override this with the @Scope annotation as follows −
```java
@Configuration
public class AppConfig {
   @Bean
   @Scope("prototype")
   public Foo foo() {
      return new Foo();
   }
}
```
#### Annotation Based Configuration
**@Required**
The @Required annotation applies to bean property setter methods.
**@Autowired**
The @Autowired annotation can apply to bean property setter methods, non-setter methods, constructor and properties.
**@Qualifier**
The @Qualifier annotation along with @Autowired can be used to remove the confusion by specifiying which exact bean will be wired.
**JSR-250 Annotations**
Spring supports JSR-250 based annotations which include @Resource, @PostConstruct and @PreDestroy annotations.

#### Bean

##### Bean Definition
The objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container. These beans are created with the configuration metadata that you supply to the container.

Bean definition contains the information called configuration metadata, which is needed for the container to know the following −
- How to create a bean
- Bean's lifecycle details
- Bean's dependencies

##### Bean Scopes
Beans
* Essentially Classes 
* Replaces keyword ‘new’ 
* Define Class, use Interface

When defining a \<bean> you have the option of declaring a scope for that bean. For example, to force Spring to produce a new bean instance each time one is needed, you should declare the bean's scope attribute to be prototype. Similarly, if you want Spring to return the same bean instance each time one is needed, you should declare the bean's scope attribute to be singleton.

The Spring Framework supports the following five scopes, three of which are available only if you use a web-aware ApplicationContext.

![image-20200918031121161](Spring.assets/image-20200918031121161.png)

**singleton**
This scopes the bean definition to a single instance per Spring IoC container (default).
If a scope is set to singleton, the Spring IoC container creates exactly one instance of the object defined by that bean definition. This single instance is stored in a cache of such singleton beans, and all subsequent requests and references for that named bean return the cached object.

The default scope is always singleton. However, when you need one and only one instance of a bean, you can set the scope property to singleton in the bean configuration file, as shown in the following code snippet −
```xml
<!-- A bean definition with singleton scope -->
<bean id = "..." class = "..." scope = "singleton">
   <!-- collaborators and configuration for this bean go here -->
</bean>
```

Summary: Singleton in Java
- Single Instance per JVM Instance 
- Lazy / Eager types

Singleton Bean in Spring
- One Instantiation
- Default Bean Scope
- Single Instance per Spring Container


**prototype**
This scopes a single bean definition to have any number of object instances.
If the scope is set to prototype, the Spring IoC container creates a new bean instance of the object every time a request for that specific bean is made. As a rule, use the prototype scope for all state-full beans and the singleton scope for stateless beans.

**request**
This scopes a bean definition to an HTTP request. Only valid in the context of a web-aware Spring ApplicationContext.

**session**
This scopes a bean definition to an HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.

**global-session**
This scopes a bean definition to a global HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.

##### Bean Life Cycle
The life cycle of a Spring bean is easy to understand. When a bean is instantiated, it may be required to perform some initialization to get it into a usable state. Similarly, when the bean is no longer required and is removed from the container, some cleanup may be required.

Two important bean life cycle callback methods, which are required at the time of bean initialization and its destruction.

**Initialization callbacks**
The org.springframework.beans.factory.InitializingBean interface specifies a single method −
```java
void afterPropertiesSet() throws Exception;
```
Thus, you can simply implement the above interface and initialization work can be done inside afterPropertiesSet() method as follows −
```java
public class ExampleBean implements InitializingBean {
   public void afterPropertiesSet() {
      // do some initialization work
   }
}
```
In the case of XML-based configuration metadata, you can use the init-method attribute to specify the name of the method that has a void no-argument signature. For example −
```xml
<bean id = "exampleBean" class = "examples.ExampleBean" init-method = "init"/>
```
Following is the class definition −
```java
public class ExampleBean {
   public void init() {
      // do some initialization work
   }
}
```

**Destruction callbacks**
The org.springframework.beans.factory.DisposableBean interface specifies a single method −
```java
void destroy() throws Exception;
```
Thus, you can simply implement the above interface and finalization work can be done inside destroy() method as follows −
```java
public class ExampleBean implements DisposableBean {
   public void destroy() {
      // do some destruction work
   }
}
```
In the case of XML-based configuration metadata, you can use the destroy-method attribute to specify the name of the method that has a void no-argument signature. For example −

```xml
<bean id = "exampleBean" class = "examples.ExampleBean" destroy-method = "destroy"/>
```
Following is the class definition −
```java
public class ExampleBean {
   public void destroy() {
      // do some destruction work
   }
}
```
If you are using Spring's IoC container in a non-web application environment; for example, in a rich client desktop environment, you register a shutdown hook with the JVM. Doing so ensures a graceful shutdown and calls the relevant destroy methods on your singleton beans so that all resources are released.

It is recommended that you do not use the InitializingBean or DisposableBean callbacks, because XML configuration gives much flexibility in terms of naming your method.
##### Bean Post Processor
The BeanPostProcessor interface defines callback methods that you can implement to provide your own instantiation logic, dependency-resolution logic, etc.
##### Bean Definition Inheritance
A bean definition can contain a lot of configuration information, including constructor arguments, property values, and container-specific information such as initialization method, static factory method name, and so on.

A child bean definition inherits configuration data from a parent definition. The child definition can override some values, or add others, as needed.

Spring Bean definition inheritance has nothing to do with Java class inheritance but the inheritance concept is same. You can define a parent bean definition as a template and other child beans can inherit the required configuration from the parent bean.

When you use XML-based configuration metadata, you indicate a child bean definition by using the parent attribute, specifying the parent bean as the value of this attribute.
#### Annotation

##### Stereotype Annotation
@Component, @Service, @Repository Semantically the same
@Component - any POJO
@Service - business logic layer 
@Repository - data layer

@Component is one Stereotype annotation used to mark a Class as a Component 
@Service & @Repository annotations inherit @Component
All these 3 annotations are complimentary to each other

**@Component vs @Service vs @Repository vs @Controller**
**@Component**
Is the most generic stereotype and marks a bean as a Spring-managed component. The @Component annotation marks a java class as a bean so the component-scanning mechanism of
spring can pick it up and pull it into the application context. To use this annotation, apply it over class. Both @Service and @Repository annotations are the specializations over the @Component annotation

**@Repository**
Although above use of @Component is good enough but you can use more suitable annotation that
provides additional benefits specifically for DAOs i.e. @Repository annotation. The @Repository annotation is a specialization of the @Component annotation with similar use and functionality. In addition to importing the DAOs into the DI container, it also makes the unchecked exceptions (thrown from DAO methods) eligible for translation into Spring DataAccessException.
Is a stereotype used for persistence layer. It translates any persistence related exceptions into a Spring’s DataAccessException

**@Service**
The @Service annotation is also a specialization of the component annotation. It doesn’t currently
provide any additional behavior over the @Component annotation, but it’s a good idea to use @Service over @Component in service-layer classes because it specifies intent better.
Is used for the beans at the service layer. Currently, it doesn’t offer any additional functionality over @Component

**@Controller**
@Controller annotation marks a class as a Spring Web MVC controller. It too is a @Component
specialization, so beans marked with it are automatically imported into the DI container. When you add the @Controller annotation to a class, you can use another annotation i.e. @RequestMapping; to map URLs to instance methods of a class.

It’s always preferable to use @Repository and @Service annotations over @Component, wherever applicable. It communicates the bean’s intent more clearly

##### Autowired Annotation
Better with Annotations 
Tied to location 
Member Variables 
Constructor
Setter

The @Autowired annotation provides more fine-grained control over where and how autowiring should be accomplished. The @Autowired annotation can be used to autowire bean on the setter method just like @Required annotation, constructor, a property or methods with arbitrary names and/or multiple arguments.

**@Autowired on Setter Methods**
You can use @Autowired annotation on setter methods to get rid of the \<property\> element in XML configuration file. When Spring finds an @Autowired annotation used with setter methods, it tries to perform byType autowiring on the method.
**@Autowired on Properties/Member Variable**
You can use @Autowired annotation on properties to get rid of the setter methods. When you will pass values of autowired properties using \<property\> Spring will automatically assign those properties with the passed values or references.



#### Properties

#### Spring EL

#### Spring AOP & AspectJ

### Spring ORM
#### Introduction
#### Spring MVC + ORM + XML
#### Spring MVC + ORM + Annotations

### Spring JDBC
#### Understanding JdbcTemplate
#### Implementing CRUD ops
#### Spring Transactions

### Spring MVC
#### Architecture
#### ModelAndView
#### Form Validations

### Design Patterns in Spring5
#### Understanding the role of Design Patterns
#### Spring Modules & Design Patterns

### Spring JPA/Hibernate
#### Introduction
#### Architecture Walkthrough
#### Spring Data JPA

### Spring REST
#### Introduction
#### Spring MVC + Jackson
#### Spring REST Template
#### Testing

### Spring Security
#### Architecture
#### User storage in DB
#### Spring Security Client Integration
#### Password Storage
#### Customizing Spring Security
#### Authentication using LDAP
#### Handling HTTPS
#### Security using JWT
#### Security using SAML
#### Security with OAuth2

### Spring SOAP
#### Overview
#### Producing & Consuming WSDL

### JMS
#### Overview of Message Brokers
#### Apache ActiveMQ
#### Apache Kafka

## Spring Boot 2

### Spring Boot Fundamentals
Introduction & Architecture
Leveraging Initializr & Dev Tools
Custom Auto Configurations
GET, POST, PUT & DELETE
Spring Boot with Security

### Spring Boot JMS
Spring Boot + ActiveMQ
Spring Boot + Kafka
Spring Boot + RabbitMQ

### Spring Thymeleaf
Overview
Walkthrough & Demo

### Docker
Docker Images & Containers
Docker Commands
Docker Hub & Repository

### Microservices
Introduction & Architecture
Spring Boot for Microservices

### Jenkins
Introduction
Installation & Configuration
Building & Packaging Java/ Maven Apps
Deployment of Java Apps to Remote Servers
Deploy Spring Boot Microservice on a Docker Container
Jenkins, Delivery & Build Pipelines

### Spring Cloud using Netflix OSS
Overview & Architecture
Microservices Co-ordination Scenarios
Locating Services at Runtime
Protecting Systems with Circuit Breakers
Traffic routing of Microservices

### Spring Cloud Streams
Spring Cloud with RabbitMQ

### Spring 5 Features
Spring Core Enhancements
Reactive Programming using WebFlux

### Spring Boot Security
Introduction
Security Forms

### Spring Thymeleaf
Overview
View Templates

### Spring Data JPA + Caching
Spring Boot + JPA
Spring Boot with Caching

### OWASP
Introduction
OWASP Top 10

## DevOps & Cloud

### Jenkins
Introduction
Installation & Configuration
Building & Packaging Java/ Maven Apps
Deployment of Java Apps to Remote Servers
Deploy Spring Boot Microservice on a Docker Container
Jenkins, Delivery & Build Pipelines

### AWS
Overview on Cloud Platform
AWS Basics
IAM, VPC, EC2
ELB, EBS, S3
Lambda, API Gateway
DynamoDB

### SDLC, CI/CD & Testing
Understanding SDLC
Unit Testing
Understanding CI/CD, DevOps
JUnit & Mockito



















