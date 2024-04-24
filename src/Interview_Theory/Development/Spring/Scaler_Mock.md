## 35 Questions in total
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
- There are 2 types of Dependency Injection:
  1. Constructor Injection: The dependencies are provided through the class constructor.
    - > The above `Car and Engine` example is an example of Constructor Injection.
  2. Setter Injection: The dependencies are provided through setter methods.
    - Example:
      ```java
      public class Car {
          private Engine engine;
          public Car() {
          }
          public void setEngine(Engine engine) {
              this.engine = engine;
          }
      }
      ```
      ```java
      public class Main {
          public static void main(String[] args) {
              Engine engine = new Engine();
              Car car = new Car();
              car.setEngine(engine);
          }
      }
      ```
      - > In the above example, the `Car` class is dependent on the `Engine` class.
        > - Instead of creating an object of the `Engine` class within the `Car` class, we are passing it as a parameter to the setter method of the `Car` class.
        >   - Instead of making the car compatible with only one kind of engine by hard-coding it, we just make a slot for the engine, define the major requirements for an engine to fit in the car and ask an outside entity to provide the engine.
        >     - This way, the `Engine` can have any kind of specs, while also following the requirements of the `Car` class.
        >     - This also allows for many different types of engines to be used in the `Car` class as long as they follow the requirements defined.
        > - This way, the `Car` class is loosely-coupled with the `Engine` class and it is easy to test, maintain and modify.
      
  #### _Difference between Constructor Injection and Setter Injection:_
    - Using the above analogies:
      > 1. **CONSTRUCTOR INJECTION:**
      >   - Imagine the car is a custom order car, where you specify that you want the car to come with a specific type of engine.
      >   - When the car is built, it's built with that engine already installed. You're essentially defining the requirements for the car upfront and the factory ensures those requirements are met during construction. 
      >     - > The factory doesn't care which specific engine brand or model you choose, it only ensures that the car is built with a slot for the engine, which will be filled by whatever engine you provide.
      >       > - The car can be fitted by any engine designed by any other company at the time of its construction.
      >   - This flexibility allows you to use any compatible engine at the time of construction.
      > 2. **SETTER INJECTION:**
      >   - Imagine the car is a standard car, where you can buy the car and then choose the engine you want to install in it.
      >   - The car is built without an engine and you can choose to install any compatible engine you want after you've bought the car.
      >     - > The car can be fitted by any engine designed by any other company after its construction.
      >   - This flexibility allows you to use any compatible engine after the car has been built.
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
  - **_Spring uses Dependency Injection to achieve IoC by injecting dependencies into objects rather than having the objects create their dependencies._**
    - Spring provides various ways to define and inject dependencies:
      1. XML-based configuration:
         - Spring allows defining beans and their dependencies in an XML configuration file, which is then loaded by the Spring IoC container.
      2. Annotation-based configuration:
         - Spring supports annotations like `@Autowired`, `@Component`, `@Service`, `@Repository`, etc., to define and inject dependencies.
      3. Java-based configuration:
         - Spring allows defining beans and their dependencies using Java configuration classes annotated with `@Configuration` and `@Bean`.
    - Spring uses annotations like `@Autowired`, `@Component`, `@Service`, `@Repository`, etc., to define and inject dependencies.
      - Spring also supports constructor injection, setter injection, and field injection for injecting dependencies.
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

### 4. Relation and Diff. b/w Spring & SpringBoot? What are the other Spring Boot Peers that rely on Spring Framework (ans- Spring Cloud , Spring WebFlux, Spring Batch etc.)
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
  - Spring boot simplifies commonly used spring dependencies and runs applications straight from a command line. It also doesn’t require an application container and it helps in monitoring several components and configures them externally.
- **Other Spring Boot Peers that rely on Spring Framework:**
  - **_Spring Cloud:_** 
    - Spring Cloud is a set of tools and libraries that helps in building cloud-native applications using the Spring Framework.
    - It provides tools for building distributed systems, microservices, and cloud-native applications, including service discovery, configuration management, circuit breakers, intelligent routing, and more.
  - **_Spring WebFlux:_**
    - Spring WebFlux is a reactive programming framework that is part of the Spring Framework.
    - It provides support for building reactive, non-blocking, and asynchronous applications using the Spring Framework.
  - **_Spring Batch:_**
    - Spring Batch is a framework for batch processing within the Spring Framework.
    - It provides reusable functions for processing large volumes of data, including reading, writing, and processing data in batches.
  - **_Spring Security:_**
    - Spring Security is a powerful and highly customizable authentication and access control framework within the Spring Framework.
    - It provides comprehensive security services for Java EE-based enterprise software applications.
  - **_Spring Data:_**
    - Spring Data is a part of the Spring Framework that provides a consistent and easy way to access different kinds of data stores, including relational databases, NoSQL databases, and cloud-based data services.
    - It provides a set of abstractions and templates to simplify data access and reduce boilerplate code.
  - **_Spring Integration:_**
    - Spring Integration is an extension of the Spring Framework that provides support for building enterprise integration solutions.
    - It enables the development of messaging and integration solutions using patterns like message channels, message endpoints, and message routing.
  - **_Spring HATEOAS:_**
    - Spring HATEOAS is a part of the Spring Framework that provides support for building RESTful web services that follow the HATEOAS (Hypermedia as the Engine of Application State) principle.
    - It enables the creation of hypermedia-driven RESTful APIs that provide links to related resources and actions.
  - **_Spring Session:_**
    - Spring Session is a part of the Spring Framework that provides support for managing HTTP session data in a distributed environment.
    - It enables the storage of session data in different data stores like Redis, MongoDB, and JDBC, and provides support for session replication and clustering.

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
  - These actuators include auditing, health, CPU usage, HTTP hits, and metric gathering, and many more that are automatically applied to your application.
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

### 12. What is @ComponentScan Annotation? Why is it used?

### 13. What is Swagger? Why is it used?

### 14. What is the Starting point of Spring Boot Application? What are the various Spring Boot starters?

### 15. How to create a customized starter in Spring Boot?

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

### 29. @Autoconfiguration? only definition wont work, you need to know the working , why it is used in springBoot , what it does. (All the discussions were like this only)

### 30. Health Monitoring

### 31. How u create scripts in CLI(Command Line Interface)

### 32. Authentication Vs Authorisation

### 33. How you use authentication and authorization in spring and name a few annotations to work with spring security.

### 34. How to create DI when there is a need to create 2 objects for a particular request

### 35. How to achieve SRP in Springboot