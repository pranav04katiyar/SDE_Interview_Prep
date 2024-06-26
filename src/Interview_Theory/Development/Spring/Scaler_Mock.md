## 35 Questions in total
1. What is Dependency Injection?
   1. Types of Dependency Injection, their use cases and differences.
   2. Which is Better to achieve loose coupling among them?
2. How does Spring Framework implement Dependency Injection?
3. How framework helps?
4. Relation and Diff. b/w Spring & SpringBoot? What are the other Spring Boot Peers that rely on Spring Framework?
5. What are Spring Profiles - spring.profiles.active? Why are they used?
6. Spring actuator and its importance.
7. Logging and Levels of Logging.
8. Spring boot actuator endpoints and logging level with priority.
9. Necessity of configuration in Spring Boot.
10. What are Beans? How are they created in Spring Boot?
11. What are Annotations? Explain the various annotations used in Spring Boot.
12. What is @ComponentScan Annotation? Why is it used?
13. What is Swagger? Why is it used?
14. What is the Starting point of Spring Boot Application? What are the various Spring Boot starters?
15. How to create a customized starter in Spring Boot?
16. What is Singleton DP. Are Spring Beans thread safe?
17. Can we create Non-Web applications in Spring Boot?
18. Default Application Server of Spring Boot. Can we replace Apache Tomcat with some other App Server?
19. Flow of API requests in Spring
20. Give a use case and asked to design the  backend API implementation for one particular API request
21. Diff b/w @RequestMapping and @GetMapping
22. Diff b/w @RequestController and @Controller
23. What are the Build Tools use are aware of?
24. Adding dependencies in Maven
25. Transaction management annotation and how to enable it?
26. How is Transaction Handling in Spring Boot achieved?
27. Transactions, Isolation levels, Concurrency
28. Optimistic and passive-locking
29. Explain @Autoconfiguration? why it is used in springBoot & what it does?
30. Health Monitoring
31. How to create scripts in CLI(Command Line Interface)?
32. Authentication Vs Authorisation
33. How do you use authentication and authorization in spring and name a few annotations to work with spring security?
34. How to create DI when there is a need to create 2 objects for a particular request?
35. How to achieve SRP in Springboot?

### 1. What is Dependency Injection?
- Dependency Injection is a design pattern which says "Whenever a class is dependent on another class, instead of creating an object of the dependency within the class, we should pass it as a parameter to a constructor or through a setter method, so that the class is loosely-coupled, easy to test and maintain."
  - It is used to remove the hard-coded dependencies and make the application loosely-coupled and easy to maintain.
  - It also facilitates the reusability of the dependencies and makes the application easy to test and modify.
- The main idea in Dependency Injection is that you don’t have to create your objects but you just have to describe how they should be created.
  - Example:
    ```java
    public class Car {
        private Engine engine;
        public Car(Engine engine) {
            this.engine = engine;
        }
    }
    ```
    ```java
    public class Engine {
        public void start() {
            System.out.println("Engine started");
        }
    }
    ```
    ```java
    public class Main {
        public static void main(String[] args) {
            Engine engine = new Engine();
            Car car = new Car(engine);
        }
    }
    ```
      - > In the above example, the `Car` class is dependent on the `Engine` class.
        > - Instead of creating an object of the `Engine` class within the `Car` class, we are passing it as a parameter to the constructor of the `Car` class.
        >   - Instead of making the car compatible with only one kind of engine by hard-coding it, we just make a slot for the engine, define the major requirements for an engine to fit in the car and ask an outside entity to provide the engine.
        >     - This way, the `Engine` can have any kind of specs, while also following the requirements of the `Car` class.
        >     - This also allows for many different types of engines to be used in the `Car` class as long as they follow the requirements defined.
        >     - So if we want to change the `Engine` object, we can easily do it by passing a different `Engine` object to the `Car` class.
        > - This way, the `Car` class is loosely-coupled with the `Engine` class and it is easy to test, maintain and modify.
        > - This is the main idea behind Dependency Injection.
- There are 3 types of Dependency Injection:
  1. Constructor Injection: The dependencies are provided through the class constructor.
    - > The above `Car and Engine` example is an example of Constructor Injection.
  2. Setter Injection: The dependencies are provided through setter methods.
    - Example:
      ```java
      public class Car {
          private PowerOutlet powerOutlet;
          public Car() {
          }
          public void setPowerOutlet(PowerOutlet powerOutlet) {
              this.powerOutlet = powerOutlet;
          }
      }
      ```
      ```java
      public class PowerOutlet {
          public void On() {
             System.out.println("Power Outlet is switched ON");
          }
      }
      ```
      ```java
      public class Main {
          public static void main(String[] args) {
              PowerOutlet powerOutlet = new PowerOutlet();
              Car car = new Car();
              car.setPowerOutlet(powerOutlet);
          }
      }
      ```
      - > In the above example, the `Car` class is dependent on the `PowerOutlet` class.
        > - Instead of creating an object of the `PowerOutlet` class within the `Car` class, we are passing it through a setter method `setPowerOutlet`.
        >   - This way, the `PowerOutlet` dependency can be provided to the `Car` object after it has been constructed.
        >   - This allows for user of the car to change the power outlet after the car is constructed as per their requirements. 
        > - This way, the `Car` class is loosely-coupled with the `PowerOutlet` class and it is easy to test, maintain and modify.
  
  3. Field Injection: The dependencies are provided through public fields.
    - > Field Injection is not recommended as it violates the principle of OOPS (encapsulation) and makes the class tightly coupled with the dependency.
    - Example:
      ```java
      public class Car {
          @Autowired
          private Engine engine;
      }
      ```
      ```java
      public class Main {
          public static void main(String[] args) {
              ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
              Car car = context.getBean(Car.class);
            }
        }
      ```
        ```java
        @Configuration
        @ComponentScan(basePackages = "com.example")
        public class AppConfig {
        }
        ```
        - > The above example uses Field Injection to inject the `Engine` dependency into the `Car` class.
          > - The `Car` class has a field `engine` annotated with `@Autowired` to indicate that the `Engine` dependency should be injected by Spring.
          > - The `AppConfig` class is annotated with `@Configuration` and `@ComponentScan` to enable component scanning and auto-detection of Spring beans.
          > - Since these annotations are used in the "field", i.e. directly on the field, it is called Field Injection.
  
  #### _Difference between Constructor Injection and Setter Injection:_
   - Using the above analogies:
      > 1. **CONSTRUCTOR INJECTION:**
      >   - Imagine the car is a custom order car, where you specify that you want the car to come with a specific type of engine.
      >   - When the car is built, it's built with that engine already installed. You're essentially defining the requirements for the car upfront and the factory ensures those requirements are met during construction. 
      >    - > The factory doesn't care which specific engine brand or model you choose, it only ensures that the car is built with a slot for the engine, which will be filled by whatever engine you provide.
      >       > - The car can be fitted by any engine designed by any other company at the time of its construction.
      >   - This flexibility allows you to use any compatible engine at the time of construction.
      > 2. **SETTER INJECTION:**
      >   - Imagine the car is a standard car, where you can buy the car and choose the power outlet you want to install in it.
      >   - The car is built without an power outlet pre-fitted and you can choose to install any compatible power outlet you want after you've bought the car.
      >    - > The car can be fitted by any power outlet designed by any other company after its construction.
      >   - This flexibility allows you to use any compatible power outlet after the car has been built.
   1. So, the main difference between Constructor Injection and Setter Injection is when the dependency is provided.
       - In Constructor Injection, the dependency is provided during the construction of the object.
       - In Setter Injection, the dependency is provided after the object has been constructed.
   2. In constructor injection, partial injection is not allowed whereas it is allowed in setter injection.
   3. The constructor injection doesn’t override the setter property, as they are immutable whereas the same is not true for setter injection.
   4. Constructor injection creates a new instance if any modification is done. The creation of a new instance is not possible in setter injection.
   5. In case the bean has many properties, then constructor injection is preferred. If it has few properties, then setter injection is preferred.
    
  #### _Which is Better to achieve loose coupling: Constructor Injection or Setter Injection?_
  - Depends on the specific use case and design preferences. Both techniques have their advantages:
   - Constructor Injection:
     1. Provides clarity and ensures that required dependencies are provided upfront during object creation. 
     2. Encourages immutability, as the dependencies cannot be changed once the object is created. 
     3. Typically used when the dependency is required for the object to function properly.
     - In general, constructor injection is often preferred when the dependency is mandatory for the object's functionality and should be provided during object creation.
     - Example: Car and tyres, Car and Engine etc.
   - Setter Injection:
     1. Offers more flexibility by allowing dependencies to be set or changed after object creation.
     2. Useful when the dependency is optional or can change during the object's lifecycle. 
     3. Can lead to more complex initialization logic and potential runtime errors if dependencies are not set correctly.
     - In general, setter injection is more suitable when the dependency is optional or can change dynamically.
     - Example: Car and power outlet, Car and older Music System etc.
  
### 2. How does Spring Framework implement Dependency Injection?
- Spring Framework implements Dependency Injection through Inversion of Control (IoC) container.
  - Inversion of Control (IoC) is a design principle where the control of object creation and lifecycle is inverted from the application code to a container or framework.
    - > In simple terms, instead of the application creating objects and managing their dependencies, the framework creates objects and manages their dependencies, providing them to the application when needed.
      > - Whenever a framework does DI for us, it is called Inversion of Control (IoC).
  - In Spring, the IoC container is responsible for managing the lifecycle of objects, creating and wiring dependencies, and providing them to the application when needed.
    - > Spring provides a very easy way to inject the dependencies using beans.
      > - A bean is an object that is instantiated, assembled, and managed by the Spring IoC container.
      > - When we start a Spring application, Spring creates objects of all beans and puts them in the Spring container.
  - **_Spring uses Dependency Injection to implement IoC by injecting dependencies into objects rather than having the objects create their dependencies._**
    
- Example:
  ```java
    @Component
    public class Car {
        private Engine engine;
        @Autowired
        public Car(Engine engine) {
            this.engine = engine;
        }
    }
    ```
    ```java
    @Component
    public class Engine {
        public void start() {
            System.out.println("Engine started");
        }
    }
    ```
    ```java
    public class Main {
        public static void main(String[] args) {
            ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            Car car = context.getBean(Car.class);
            car.start();
        }
    }
    ```
    ```java
    @Configuration
    @ComponentScan(basePackages = "com.example")
    public class AppConfig {
    }
    ```
    - > In the above example, the `Car` class is annotated with `@Component` to indicate that it is a Spring bean.
      > - The `Engine` class is also annotated with `@Component` to indicate that it is a Spring bean.
      > - The `Car` class has a constructor that takes an `Engine` object as a parameter and is annotated with `@Autowired` to indicate that the `Engine` dependency should be injected by Spring.
      > - The `AppConfig` class is annotated with `@Configuration` and `@ComponentScan` to enable component scanning and auto-detection of Spring beans.
    - > The `Main` class creates an `ApplicationContext` using the `AppConfig` class and retrieves the `Car` bean from the context.
      > - When the `Car` bean is retrieved from the context, Spring automatically injects the `Engine` dependency into the `Car` object.
      > - This way, Spring manages the lifecycle of the `Car` and `Engine` objects, creates and wires the dependencies, and provides them to the application when needed. 

### 3. How framework helps?
- A framework provides a structure and standardized way as well as set of tools, libraries and modules to streamline the development process of an application.
  1. **Boilerplate code abstraction:** 
     > Frameworks provide pre-built low-level code details to handle common tasks, like handling HTTP requests, database interactions, transaction management, security etc., allowing developers to focus more on implementing business logics rather than writing repetitive code.
  2. **Consistency and standardization:**
     > Frameworks enforce certain set of conventions and best practices, ensuring that the codebase is consistent and maintainable across the application. This makes it easier for developers to understand each other's code, collaborate effectively, and maintain the application over time.
  3. **Modularity and reusability:**
     > Frameworks promote modular design by breaking down the application into smaller components or modules, which can be reused across the application or in other projects. For example, in Spring, modular development through Dependency Injection mechanism is promoted, encouraging breaking down of application into smaller components like controllers, services, repositories etc., which can be easily reused in different parts of the application.
  4. **Scalability and performance:**
     > Frameworks often provide built-in features, tools and architectural patterns for scalability and performance optimization, both vertically (by adding more resources to a single server and improving its performance efficiency using techniques like caching, lazy loading, connection pooling, etc.) and horizontally (by distributing the workload and optimizing interactions across multiple servers like load balancing, data partitioning, etc.), to ensure that the application can handle increased traffic and maintain high performance.
  5. **Security and reliability:**
     > Frameworks often come with built-in security features and mechanisms to protect the application from common security threats like SQL injection, cross-site scripting, etc. They also provide tools for authentication, authorization, encryption, and other security measures to ensure that the application is secure and reliable.
  6. **Testing and debugging:**
     > Frameworks provide tools and libraries for automated testing, debugging, and profiling of the application, making it easier for developers to write unit tests, integration tests, and perform debugging to identify and fix issues in the codebase. This helps in ensuring the quality and reliability of the application.
  7. **Community support and documentation:**
     > Frameworks often have a large community of developers, contributors, and users who actively contribute to the framework, provide support, share knowledge, and create documentation, tutorials, and resources to help developers learn and use the framework effectively. This community support helps developers to quickly resolve issues, learn new features, and stay updated with the latest trends and best practices in the development community.

### 4. Relation and Diff. b/w Spring & SpringBoot? What are the other Spring Boot Peers that rely on Spring Framework?
- **Spring Framework:**
  - Spring is an open-source lightweight framework that is used to develop loosely-coupled enterprise level Java applications.
  - Spring handles all the infrastructure-related aspects which lets the programmer focus mostly on application development. 
  - Spring works on the principle of Dependency Injection, which allows us to create beans that are automatically created as well as injected into other objects.
  - Spring provides various modules like Spring Core, Spring AOP, Spring ORM, Spring DAO, Spring MVC, Spring Security, etc., to support different aspects of enterprise application development.
- **Spring Boot:**
  - Spring Boot is a project built on top of the Spring Framework that aims to simplify the development of production-ready Spring applications.
  - Spring Boot is a project that is built on top of the Spring Framework. It provides a simpler and faster way to set up, configure, and run both simple and web-based applications.
    - It eliminates the need to write any configuration files, annotations, or boilerplate code.
    - It also automatically configures a project with all the known best practices and a set of defaults.
- **Difference between Spring and Spring Boot:**
  - The Spring Framework provides multiple features like dependency injection, data binding, aspect-oriented programming (AOP), data access, and many more that help ease development of web applications whereas Spring Boot helps in easier usage of the Spring Framework by simplifying or managing various loosely coupled blocks of Spring which are tedious and have a potential of becoming messy.
  - Spring Boot is an opinionated view of the Spring platform and third-party libraries, which makes it easy to create stand-alone, production-grade Spring-based Applications that you can "just run", whereas Spring Framework is a comprehensive programming and configuration model.
  - Spring Boot follows conventions over configurations, meaning it provides a set of starter dependencies that can be added to the project to automatically configure common features like logging, security, data access, etc., without the need for manual configuration, whereas Spring Framework requires manual configuration of these features.
- **Other Spring Boot Peers that rely on Spring Framework:**
  - **_Spring Cloud:_** 
    > - Spring Cloud is a set of tools and libraries that helps in building cloud-native applications using the Spring Framework.
    > - It provides tools for building distributed systems, microservices, and cloud-native applications, including service discovery, configuration management, circuit breakers, intelligent routing, and more.
  - **_Spring WebFlux:_**
    > - Spring WebFlux is a reactive programming framework that is part of the Spring Framework.
    > - It provides support for building reactive, non-blocking, and asynchronous applications using the Spring Framework.
  - **_Spring Batch:_**
    > - Spring Batch is a framework for batch processing within the Spring Framework.
    > - It provides reusable functions for processing large volumes of data, including reading, writing, and processing data in batches.
  - **_Spring Security:_**
    > - Spring Security is a powerful and highly customizable authentication and access control framework within the Spring Framework.
    > - It provides comprehensive security services for Java EE-based enterprise software applications.
  - **_Spring Data:_**
    > - Spring Data is a part of the Spring Framework that provides a consistent and easy way to access different kinds of data stores, including relational databases, NoSQL databases, and cloud-based data services.
    > - It provides a set of abstractions and templates to simplify data access and reduce boilerplate code.
  - **_Spring Integration:_**
    > - Spring Integration is an extension of the Spring Framework that provides support for building enterprise integration solutions.
    > - It enables the development of messaging and integration solutions using patterns like message channels, message endpoints, and message routing.
  - **_Spring HATEOAS:_**
    > - Spring HATEOAS is a part of the Spring Framework that provides support for building RESTful web services that follow the HATEOAS (Hypermedia as the Engine of Application State) principle.
    > - It enables the creation of hypermedia-driven RESTful APIs that provide links to related resources and actions.
  - **_Spring Session:_**
    > - Spring Session is a part of the Spring Framework that provides support for managing HTTP session data in a distributed environment.
    > - It enables the storage of session data in different data stores like Redis, MongoDB, and JDBC, and provides support for session replication and clustering.

### 5. What are Spring Profiles - spring.profiles.active? Why are they used?
- While developing the application we deal with multiple environments such as dev, QA, Prod, and each environment requires a different configuration. 
  - For eg., we might be using an embedded H2 database for dev but for prod, we might have proprietary Oracle or DB2. Even if DBMS is the same across the environment, the URLs will be different.
  - To make this easy and clean, Spring has the provision of Profiles to keep the separate configuration of environments.
- Spring Profiles are a feature in the Spring Framework that allow you to define and manage different configurations for your application based on different environments or conditions. The spring.profiles.active property is a key part of this feature.
- Spring Profiles provide a flexible and convenient way to manage configurations for your Spring applications across different environments.
- Here's how it works:
  > - **Defining Profiles:** You can define different profiles in your Spring application, each representing a specific set of configurations. For example, you might have a "development" profile for your local development environment, a "production" profile for your live production environment, and so on.
  > - **Activating Profiles:** By setting the spring.profiles.active property in your application's configuration (such as in application.properties or application.yml), you specify which profiles should be active for the current runtime environment. You can specify multiple profiles separated by commas if needed.
  > - **Profile-specific Configurations:** You can then provide profile-specific configurations, such as database settings, logging levels, or any other Spring beans, by creating separate configuration files for each profile. These files are typically named using the convention application-{profile}.properties or application-{profile}.yml.
  > - **Dynamic Configuration:** Spring will automatically load the configurations from the files corresponding to the active profiles at runtime. This allows your application to adapt to different environments without needing to change code or rebuild the application.
- Spring Profiles are used for several reasons:
  - **Environment-specific Configurations:**
    > Different environments (such as development, testing, staging, production) often require different configurations. Profiles allow you to manage these configurations cleanly without cluttering your codebase with environment-specific logic.
  - **Ease of Deployment:**
    > Profiles make it easier to deploy your application to different environments by allowing you to specify the necessary configurations for each environment separately.
  - **Testing:**
    > Profiles facilitate testing by allowing you to easily switch between different configurations, making it simpler to test your application in different environments.

### 6. Spring actuator and its importance.
- An actuator is an additional feature of Spring that helps you to monitor and manage your application when you push it to production. 
  > These actuators include auditing, health, CPU usage, HTTP hits, and metric gathering, and many more that are automatically applied to your application.
- **Spring Boot Actuator** is a sub-project of Spring Boot that provides production-ready features to help you monitor and manage your application.
  - It provides a set of built-in endpoints that expose information about your application, such as health status, metrics, environment details, and more.
  - Actuator endpoints can be accessed over HTTP or JMX, and they provide valuable insights into the runtime behavior of your application.
  - Some of the common actuator endpoints include:
    - **/actuator/health:** Provides information about the health status of your application, including details about the database, disk space, and other dependencies.
    - **/actuator/info:** Displays arbitrary application info, such as the application name, version, and description.
    - **/actuator/metrics:** Exposes metrics about your application, such as memory usage, garbage collection, and HTTP request counts.
    - **/actuator/env:** Displays information about the application's environment, including system properties, environment variables, and configuration properties.
    - **/actuator/loggers:** Allows you to view and configure logging levels for different loggers in your application.
    - **/actuator/beans:** Provides a list of all Spring beans in your application.
    - **/actuator/mappings:** Displays a list of all request mappings in your application.
  - Actuator endpoints can be customized and secured using Spring Security to restrict access to sensitive information.
  - Actuator is a powerful tool for monitoring and managing your Spring Boot application in production, providing valuable insights into the application's health, performance, and behavior.

### 7. Logging and Levels of Logging
- Logging is a crucial aspect of software development, particularly in understanding the behavior of an application, diagnosing issues, and monitoring its performance in production environments. Spring Boot, like many modern frameworks, supports logging extensively, and it utilizes popular logging frameworks such as Logback, Log4j2, and JUL (Java Util Logging). Here's an overview of logging and its levels:
- **Levels of Logging:**
  1. **TRACE:** The lowest and most detailed level of logging. It's used for extremely fine-grained information, typically only useful during development or debugging sessions. Trace messages can include method entry/exit points, variable values, and other detailed information.
  2. **DEBUG:** A level above trace, used for debugging purposes. Debug messages provide more information than trace messages and are typically used to log detailed information about the application's state, such as variable values or the flow of control within methods.
  3. **INFO:** The default level for logging in most production environments. Info messages are used to provide general information about the application's operation, such as application startup, major configuration changes, or significant events.
  4. **WARN:** Indicates potentially harmful situations or unexpected behaviors that are not necessarily errors but may require attention. Warn messages are used to alert developers or administrators about conditions that may lead to errors or degraded performance.
  5. **ERROR:** Indicates errors or exceptional conditions that require immediate attention. Error messages are used to log critical errors that may impact the application's functionality or stability, such as unhandled exceptions or failed operations.
  6. **FATAL:** The highest level of logging, used to indicate severe errors that lead to the application's termination or failure. Fatal messages are typically logged when the application encounters unrecoverable errors or conditions that prevent it from continuing normal operation.
- Importance of Logging Levels:
  - Debugging: Logging levels allow developers to control the amount of information logged during development and debugging. Developers can increase the logging level to trace or debug to gain insights into the application's behavior and identify issues.
  - Monitoring: In production environments, logging levels help administrators monitor the application's health and performance. By configuring appropriate log levels, administrators can ensure that relevant information is logged without overwhelming the logs with excessive details.
  - Troubleshooting: When issues arise in production, logging levels help troubleshoot and diagnose problems quickly. Administrators can adjust the logging level dynamically to capture more detailed information about the issue without restarting the application.
  - Performance: Logging can impact application performance, especially when logging at lower levels (e.g., debug or trace). By controlling the logging level, developers can minimize the performance overhead of logging while still capturing essential information.
- Overall, logging levels provide a flexible mechanism for controlling the amount and granularity of information logged by an application, making it easier to develop, deploy, monitor, and troubleshoot software systems effectively.

### 8. Spring boot actuator endpoints and logging level with priority
- Some of the common actuator endpoints include:
    - **/actuator/health:** Provides information about the health status of your application, including details about the database, disk space, and other dependencies.
    - **/actuator/info:** Displays arbitrary application info, such as the application name, version, and description.
    - **/actuator/metrics:** Exposes metrics about your application, such as memory usage, garbage collection, and HTTP request counts.
    - **/actuator/env:** Displays information about the application's environment, including system properties, environment variables, and configuration properties.
    - **/actuator/loggers:** Allows you to view and configure logging levels for different loggers in your application.
    - **/actuator/beans:** Provides a list of all Spring beans in your application.
    - **/actuator/mappings:** Displays a list of all request mappings in your application.
- Regarding logging levels and priorities, here's a typical hierarchy:
    1. TRACE: The lowest and most detailed level. Typically used for extremely fine-grained information useful during development or debugging. 
    2. DEBUG: Used for debugging purposes. Debug messages provide more information than trace messages and are helpful for troubleshooting issues.
    3. INFO: The default level for logging in most production environments. Used to provide general information about the application's operation.
    4. WARN: Indicates potentially harmful situations or unexpected behaviors that may require attention.
    5. ERROR: Indicates errors or exceptional conditions that require immediate attention.
    6. FATAL: The highest level, used to indicate severe errors that lead to the application's termination or failure.

### 9. Necessity of configuration in Spring Boot.
- Configuration in Spring Boot allows developers to fine-tune their applications to meet specific requirements and adapt to changing environments seamlessly.
- It is necessary for tailoring application behavior, externalizing properties, supporting different environments, integrating with external services, ensuring security, optimizing performance, and managing dependencies effectively. 
- It is essential for several reasons:
  1. Application Behavior Customization:
     > Spring Boot provides sensible defaults for many configurations, but every application has its unique requirements. Configuration allows developers to customize the behavior of their Spring Boot applications according to specific needs, such as database settings, security configurations, logging levels, etc.
  2. Externalizing Properties:
     > Spring Boot allows you to externalize configuration properties from the application code. This means that properties like database connection details, API keys, environment-specific settings, etc., can be configured externally without changing the code. It enhances maintainability, as configuration changes can be made without rebuilding or redeploying the application.
  3. Profile-based Configuration:
     > Spring Boot supports the concept of profiles, allowing you to define configurations specific to different environments (e.g., development, testing, production). Profiles enable seamless switching between configurations based on the runtime environment, ensuring consistency and portability across environments.
  4. Third-party Integrations:
     > Many Spring Boot applications integrate with external services, frameworks, or libraries. Configuration is often required to set up and configure these integrations properly. For example, configuring a database connection pool, setting up messaging queues, or configuring caching mechanisms.
  5. Security Configuration:
     > Security is a critical aspect of modern applications. Spring Boot provides robust security features, but configuring them correctly according to the application's security requirements is essential. Configuration allows developers to define authentication mechanisms, access control policies, encryption settings, etc., to ensure the application's security.
  6. Logging Configuration:
     > Logging is vital for monitoring application behavior, diagnosing issues, and auditing activities. Spring Boot offers flexible logging configurations, allowing developers to specify logging levels, appenders, log formats, etc., based on the application's logging requirements.
  7. Performance Tuning:
     > Configuration plays a significant role in optimizing application performance. Fine-tuning configurations related to database connections, caching, thread pools, etc., can significantly impact the application's performance and scalability.
  8. Dependency Injection and Bean Configuration:
     > Spring Boot heavily relies on the concept of dependency injection and inversion of control. Configuration is essential for defining and configuring beans, setting up dependencies, and managing component lifecycles.


### 10. What are Beans? How are they created in Spring Boot?
- A bean is an object that Spring will automatically create as well as inject the dependencies for you whenever and wherever needed and manage the lifecycle of the object.
- They are the objects forming the backbone of the user’s application and are managed by the Spring IoC container.
- A Spring Bean is instantiated, configured, wired and managed by the Spring IoC container.
- Think of a bean as a special object that you give to Spring, so that it can inject the dependencies for you automatically whenever needed and manage the lifecycle of the object.
- When we start a Spring application, Spring creates objects of all beans and puts them in the Spring container.
- Beans are created with the configuration metadata that the users supply to the container (by means of XML or java annotations configurations.)

### 11. What are Annotations? Explain the various annotations used in Spring Boot.
- Annotations in Java are a form of metadata that provide data about a program that is not part of the program itself. 
    - They can be attached to classes, methods, fields, parameters, and other program elements to provide additional information to the compiler, runtime, or other tools.
- In Spring Boot, annotations play a crucial role in configuring and controlling the behavior of various components within the application. 
    - They help in reducing the amount of configuration code and provide a more declarative way of defining the application's structure and behavior.
    - Spring Boot provides a rich set of annotations that help streamline configuration, dependency injection, MVC web development, data access, and many other aspects of building enterprise-grade applications.
    - Some commonly used annotations in Spring Boot are:
      1. `@SpringBootApplication`: 
         This annotation is used to mark the main class of a Spring Boot application. It combines three other annotations:
          - `@Configuration`:
            > Indicates that the class is a source of bean definitions for the application context. Spring Boot uses this annotation to bootstrap the application context and configure various components.
          - `@EnableAutoConfiguration`:
            > Tells Spring Boot to automatically configure the Spring application context based on the classpath and other configuration properties. It enables Spring Boot's auto-configuration feature, which automatically configures beans and components based on conventions, dependencies, and settings. 
          - `@ComponentScan`.
            > Instructs Spring Boot to scan the specified base packages and their sub-packages for Spring components such as @Component, @Service, @Repository, and others. This allows Spring Boot to detect and register Spring-managed beans within the application context.
         
         It essentially tells Spring Boot to enable auto-configuration, component scanning, and other features necessary to bootstrap the application. 
      2. `@Controller`:
         Used to mark a class as a Spring MVC controller. Controllers handle incoming HTTP requests and return appropriate responses.
      3. `@RestController`: 
         Similar to `@Controller`, but specifically used for RESTful web services. 
         
         It combines `@Controller` and `@ResponseBody`, meaning that the return value of methods will be serialized directly to the HTTP response body.
      4. `@RequestMapping`: Used to map web requests to specific handler methods within `@Controller` or `@RestController` classes. 
      
         It allows you to specify the URL path and HTTP method that should trigger the method.
      5. `@Autowired`: Used to inject dependencies automatically into Spring-managed beans. 
         It can be applied to fields, constructors, or setter methods.
      6. `@Service`: Used to mark a class as a service component in the Spring application context.
         Service components typically contain business logic and are used to perform specific tasks.
      7. `@Repository`: Marks a class as a Spring Data repository, typically used for database access.
         It serves as a marker for the persistence layer and enables Spring's exception translation mechanism for database-related exceptions.
      8. `@Component`: A generic stereotype annotation used to mark a class as a Spring component.
         It indicates that the class is a candidate for auto-detection and bean instantiation by Spring's component scanning mechanism.
      9. `@Configuration`: Indicates that a class declares one or more @Bean methods and may be processed by the Spring container to generate bean definitions and service requests for those beans.
      10. `@Bean`: Used to define a bean explicitly in a Spring configuration class. 
          It tells Spring that a method annotated with `@Bean` will return an object that should be registered as a bean in the Spring application context.
      11. `@Value`: Used to inject values from properties files or environment variables into Spring components.
          It can be applied to fields, constructor parameters, or setter methods.
      12. `@Qualifier`: Used in conjunction with @Autowired to specify which bean to inject when multiple beans of the same type are available.
      13. `@RequestMapping` variations:
          - `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`: Convenience annotations for mapping HTTP GET, POST, PUT, and DELETE requests, respectively.
          - `@PatchMapping`: Maps HTTP PATCH requests to handler methods.
      14. `@PathVariable`: Used to extract values from URI template variables in `@RequestMapping` methods.
      15. `@RequestParam`: Binds HTTP request parameters to method parameters in `@RequestMapping` methods.
      16. `@ModelAttribute`: Binds method parameters or method return values to model attributes, which can be used in views.
      17. `@ExceptionHandler`: Defines methods to handle exceptions thrown by request handler methods.
      18. `@ResponseStatus`: Specifies the HTTP status code to be returned by a controller method in case of successful invocation.
      19. `@ResponseStatus` variants:
          - `@ResponseStatus(HttpStatus.CREATED)`: Marks a controller method to return HTTP status code 201 (Created).
          - `@ResponseStatus(HttpStatus.NO_CONTENT)`: Marks a controller method to return HTTP status code 204 (No Content).
      20. `@RequestBody`: Used to bind the HTTP request body to a method parameter in `@RequestMapping` methods.
      21. `@ResponseBody`: Indicates that the return value of a method should be serialized directly to the HTTP response body in `@RequestMapping` methods.
      22. `@CrossOrigin`: Configures cross-origin resource sharing (CORS) for web endpoints, allowing resources to be accessed from different domains.
      23. `@Transactional`: Marks a method, class, or interface as transactional, allowing Spring to manage transactions declaratively.
      24. `@Async`: Indicates that a method should be executed asynchronously, allowing Spring to manage the execution of the method in a separate thread.
      25. `@Scheduled`: Used to schedule the execution of a method at fixed intervals or according to a cron expression.
      26. `@EnableScheduling`: Enables Spring's scheduled task execution infrastructure, allowing the use of `@Scheduled` annotations.
      27. `@EnableAsync`: Enables Spring's asynchronous method execution infrastructure, allowing the use of `@Async` annotations.

### 12. What is @ComponentScan Annotation? Why is it used?
- Spring Boot application scans all the beans and package declarations when the application initializes. 
- You need to add the @ComponentScan annotation for your class file to scan your components added to your project.
- The @ComponentScan annotation is used in Spring applications to specify the base packages to scan for Spring-managed components such as @Component, @Service, @Repository, and others. 
- When Spring Boot starts up, it automatically performs component scanning to discover and register beans within the application context.

### 13. What is Swagger? Why is it used?
- Swagger is an open-source framework used for designing, documenting, and testing RESTful APIs.
- It provides a set of tools and specifications for developers to generate interactive API documentation, allowing consumers to understand and interact with the API more easily.
- Use cases:
  - To streamline the development process of designing, documenting, and consuming RESTful APIs. 
  - Improving developer productivity, collaboration and communication between stakeholders.
  - Enhancing the adoption and overall quality of APIs by providing a standardized and user-friendly documentation format.

### 14. What is the Starting point of Spring Boot Application? What are the various Spring Boot starters?
1. The starting point of a Spring Boot application is typically the main class annotated with @SpringBootApplication. 
    - This annotation is a meta-annotation that combines several other annotations, including @Configuration, @EnableAutoConfiguration, and @ComponentScan
- Here's how it works:
    1. `@Configuration`: Indicates that the class is a source of bean definitions for the application context.
    2. `@EnableAutoConfiguration`: Tells Spring Boot to automatically configure the Spring application context based on the classpath and other configuration properties.
    3. `@ComponentScan`: Instructs Spring Boot to scan the specified base packages and their sub-packages for Spring components such as @Component, @Service, @Repository, and others.
- The main class annotated with @SpringBootApplication serves as the entry point for the Spring Boot application. It typically contains the main method, which is the starting point for the application's execution.
2. Spring Boot starters are a set of dependency descriptors that are designed to simplify the process of adding dependencies to a Spring Boot application. 
   - Starters provide pre-configured sets of dependencies for specific functionalities or use cases, making it easy to bootstrap Spring Boot projects with minimal configuration.
   - Some common Spring Boot starters include:
     1. `spring-boot-starter-web`: Includes dependencies for building web applications with Spring MVC, including embedded Tomcat as the default servlet container.
     2. `spring-boot-starter-data-jpa`: Provides dependencies for using Spring Data JPA for data access, including Hibernate as the default JPA provider.
     3. `spring-boot-starter-security`: Includes dependencies for integrating Spring Security into the application, providing features such as authentication, authorization, and CSRF protection.
     4. `spring-boot-starter-test`: Contains dependencies for writing unit and integration tests with Spring Boot, including JUnit, Mockito, and Spring Test.
     5. `spring-boot-starter-actuator`: Provides dependencies for integrating Spring Boot Actuator, which offers production-ready features for monitoring and managing the application.
     6. `spring-boot-starter-log4j2`, `spring-boot-starter-logging`: Provides dependencies for logging in Spring Boot applications, including Log4j2, Logback, or JDK Logging.

### 15. How to create a customized starter in Spring Boot?
1. **Define Dependencies**: Identify the dependencies and configurations that you want to include in your starter. These could be libraries, frameworks, or custom components that provide specific functionalities. 
2. **Create a New Maven or Gradle Project**: Start by creating a new Maven or Gradle project for your custom starter. You can use tools like Maven Archetype or Spring Initializr to generate the project structure.
3. **Configure Project Structure**: Organize your project structure according to Maven/Gradle conventions. You typically need to include the following directories:
   - **src/main/java**: 
        > Contains Java source code.
   - **src/main/resources**:
        > Contains configuration files and resources.
   - **src/test/java**:
        > Contains test source code.
   - **src/test/resources**:
        > Contains test configuration files and resources.
4. **Implement Configuration**: Write the necessary configuration classes to configure the dependencies and components included in your starter. This may involve creating Spring @Configuration classes, @Bean methods, or other configuration mechanisms.
5. **Package Dependencies**: Package your dependencies and configurations into a reusable module. This typically involves creating a JAR file containing the compiled classes and resources.
6. **Create Spring Boot Auto-Configuration**: If your starter requires custom auto-configuration, you can create a Spring Boot auto-configuration class. This class should be annotated with @Configuration and @ConditionalOnClass or @ConditionalOnMissingBean annotations to ensure that it's only applied when specific conditions are met.
7. **Define Starter Metadata**: Create a spring.factories file in the src/main/resources/META-INF directory to specify the auto-configuration classes included in your starter. This file should contain entries in the format org.springframework.boot.autoconfigure.EnableAutoConfiguration=com.example.CustomAutoConfiguration.
8. **Publish Your Starter**: Publish your customized starter to a Maven repository or a local repository so that it can be consumed by other Spring Boot projects. You can use tools like Maven or Gradle to publish your artifact.
9. **Use Your Starter**: To use your custom starter in a Spring Boot project, include it as a dependency in the project's pom.xml (Maven) or build.gradle (Gradle) file. Once added, Spring Boot will automatically apply the configurations and dependencies included in your starter.

### 16. What is Singleton DP. Are Spring Beans thread safe?

### 17. Can we create Non-Web applications in Spring Boot?

### 18. Default Application Server of Spring Boot. Can we replace Apache Tomcat with some other App Server?

### 19. Flow of API requests in Spring

### 20. Give a use case and asked to design the  backend API implementation for one particular API request

### 21. Diff b/w @RequestMapping and @GetMapping

### 22. Diff b/w @RequestController and @Controller

### 23. What are the Build Tools use are aware of?

### 24. Adding dependencies in Maven

### 25. Transaction management annotation and how to enable it? 

### 26. How is Transaction Handling in Spring Boot achieved?

### 27. Transactions, Isolation levels, Concurrency

### 28. Optimistic and passive-locking

### 29. Explain @Autoconfiguration? why it is used in springBoot & what it does?

### 30. Health Monitoring

### 31. How u create scripts in CLI(Command Line Interface)

### 32. Authentication Vs Authorisation

### 33. How you use authentication and authorization in spring and name a few annotations to work with spring security.

### 34. How to create DI when there is a need to create 2 objects for a particular request

### 35. How to achieve SRP in Springboot