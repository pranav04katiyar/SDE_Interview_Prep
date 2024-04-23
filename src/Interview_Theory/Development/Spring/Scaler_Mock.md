## 20 Questions in total
### 1. What is Dependency Injection
- Dependency Injection is a design pattern which says "Whenever a class is dependent on another class, instead of creating an object of the dependency within the class, we should pass it as a parameter to a constructor or through a setter method, keeping the class loosely-coupled, easy to test and maintain."
  - It is used to remove the hard-coded dependencies and make the application loosely-coupled and easy to maintain.
  - It also facilitates the reusability of the dependencies and makes the application easy to test and modify.
- There are 2 types of Dependency Injection:
  - Constructor Injection: The dependencies are provided through the class constructor.
  - Setter Injection: The dependencies are provided through setter methods.
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
    - In the above example, the `Car` class is dependent on the `Engine` class. 
    - Instead of creating an object of the `Engine` class within the `Car` class, we are passing it as a parameter to the constructor of the `Car` class.

### 2. Diff b/w Spring & SpringBoot

### 3. Spring Profiles

### 4. Logging and Levels of Logging

### 5. What are Beans

### 6. What are Annotations

### 7. Component Scan Annotation

### 8. Swagger

### 9. Starting point of Spring Boot Application

### 10. What is Singleton DP. Are Spring Beans thread safe?

### 11. Can we create Non-Web applications in Spring Boot?

### 12. Default Application Server of Spring Boot. Can we replace Apache Tomcat with some other App Server?

### 13. Flow of API requests in Spring

### 14. Give a use case and asked to design the  backend API implementation for one particular API request

### 15. Diff b/w @RequestMapping and @GetMapping

### 16. Diff b/w @RequestController and @Controller

### 17. What are the Build Tools use are aware of?

### 18. Adding dependencies in Maven

### 19. Transaction management annotation and how to enable it 

### 20. Spring boot actuator endpoints and logging level with priority