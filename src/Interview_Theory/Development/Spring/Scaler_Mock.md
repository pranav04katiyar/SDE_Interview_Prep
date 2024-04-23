## 34 Questions in total
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
      
  #### Difference between Constructor Injection and Setter Injection:
    - Using the above analogies:
      1. Constructor Injection:
        - Imagine the car is a custom order car, where you specify that you want the car to come with a specific type of engine.
        - When the car is built, it's built with that engine already installed. You're essentially defining the requirements for the car upfront and the factory ensures those requirements are met during construction. 
          - > The factory doesn't care which specific engine brand or model you choose, it only ensures that the car is built with a slot for the engine, which will be filled by whatever engine you provide.
            > - The car can be fitted by any engine designed by any other company at the time of its construction.
        - This flexibility allows you to use any compatible engine at the time of construction.
      2. Setter Injection:
        - Imagine the car is a standard car, where you can buy the car and then choose the engine you want to install in it.
        - The car is built without an engine and you can choose to install any compatible engine you want after you've bought the car.
          - > The car can be fitted by any engine designed by any other company after its construction.
        - This flexibility allows you to use any compatible engine after the car has been built.
    - So, the main difference between Constructor Injection and Setter Injection is when the dependency is provided.
      - In Constructor Injection, the dependency is provided during the construction of the object.
      - In Setter Injection, the dependency is provided after the object has been constructed.
    
  #### Which is Better to achieve loose coupling: Constructor Injection or Setter Injection?
  - Depends on the specific use case and design preferences. Both techniques have their advantages:
    - Constructor Injection:
      1. Provides clarity and ensures that required dependencies are provided upfront during object creation. 
      2. Encourages immutability, as the dependencies cannot be changed once the object is created. 
      3. Typically used when the dependency is required for the object to function properly.
      - In general, constructor injection is often preferred when the dependency is mandatory for the object's functionality and should be provided during object creation.
    - Setter Injection:
      1. Offers more flexibility by allowing dependencies to be set or changed after object creation.
      2. Useful when the dependency is optional or can change during the object's lifecycle. 
      3. Can lead to more complex initialization logic and potential runtime errors if dependencies are not set correctly.
      - In general, setter injection is more suitable when the dependency is optional or can change dynamically. 

### 2. How framework helps?

### 3. Relation and Diff. b/w Spring & SpringBoot? Explain other Spring Boot Peers that relies on Spring Framework - Spring Cloud , Spring WebFlux, Spring Batch etc.

### 4. What are Spring Profiles - spring.profiles.active? Why are they used?

### 5. Spring actuator and its importance.

### 6. Logging and Levels of Logging

### 7. Spring boot actuator endpoints and logging level with priority

### 8. Necessity of configuration in Spring Boot.

### 9. What are Beans? How are they created in Spring Boot?

### 10. What are Annotations? Explain the various annotations used in Spring Boot.

### 11. What is @ComponentScan Annotation? Why is it used?

### 12. What is Swagger? Why is it used?

### 13. What is the Starting point of Spring Boot Application? What are the various Spring Boot starters?

### 14. How to create a customized starter in Spring Boot?

### 15. What is Singleton DP. Are Spring Beans thread safe?

### 16. Can we create Non-Web applications in Spring Boot?

### 17. Default Application Server of Spring Boot. Can we replace Apache Tomcat with some other App Server?

### 18. Flow of API requests in Spring

### 19. Give a use case and asked to design the  backend API implementation for one particular API request

### 20. Diff b/w @RequestMapping and @GetMapping

### 21. Diff b/w @RequestController and @Controller

### 22. What are the Build Tools use are aware of?

### 23. Adding dependencies in Maven

### 24. Transaction management annotation and how to enable it? 

### 25. How is Transaction Handling in Spring Boot achieved?

### 26. Transactions, Isolation levels, Concurrency

### 27. Optimistic and passive-locking

### 28. @Autoconfiguration? only definition wont work, you need to know the working , why it is used in springBoot , what it does. (All the discussions were like this only)

### 29. Health Monitoring

### 30. How u create scripts in CLI(Command Line Interface)

### 31. Authentication Vs Authorisation

### 32. How you use authentication and authorization in spring and name a few annotations to work with spring security.

### 33. How to create DI when there is a need to create 2 objects for a particular request

### 34. How to achieve SRP in Springboot