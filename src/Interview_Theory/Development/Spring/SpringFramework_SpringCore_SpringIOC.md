## 13 Questions in total
### 1. What is Spring Framework?
- Spring is an open-source lightweight framework used to reduce the complexities in developing loosely-coupled enterprise level Java applications.
- Spring handles all the infrastructure-related aspects which lets the programmer to focus mostly on application development.
- Spring has a core framework that provides essential core set of functionalities + additional modules that provide additional functionality based on the application requirements.(Web, Data, Cloud, Authentication, etc.)
- There are around 20 modules which are generalized into the following types:
  1. Core Container
  2. Data Access/Integration
  3. Web
  4. AOP (Aspect Oriented Programming)
  5. Instrumentation
  6. Messaging
  7. Test

### 2. What are the features of Spring Framework?
- Spring framework follows layered architecture pattern that helps in the necessary components selection along with providing a robust and cohesive framework for J2EE applications development.
- The AOP (Aspect Oriented Programming) part of Spring supports unified development by ensuring separation of application’s business logic from other system services.
- Spring provides highly configurable MVC web application framework which has the ability to switch to other frameworks easily.
- Provides provision of creation and management of the configurations and defining the lifecycle of application objects.
- Spring has a special design principle which is known as IoC (Inversion of Control) that supports objects to give their dependencies rather than looking for creating dependent objects.
- Spring is a lightweight, java based, loosely coupled framework.
- Spring provides generic abstraction layer for transaction management that is also very useful for container-less environments.
- Spring provides a convenient API to translate technology-specific exceptions (thrown by JDBC, Hibernate or other frameworks) into consistent, unchecked exceptions. This introduces abstraction and greatly simplifies exception handling.

### 3. What is a Spring configuration file?
- A Spring configuration file is basically an XML file that mainly contains the classes information and describes how those classes are configured and linked to each other. The XML configuration files are verbose and cleaner.

### 4. What do you mean by IoC (Inversion of Control) Container?
- Spring container forms the core of the Spring Framework. The Spring container uses Dependency Injection (DI) for managing the application components by creating objects, wiring them together along with configuring and managing their overall life cycles. The instructions for the spring container to do the tasks can be provided either by XML configuration, Java annotations, or Java code.

### 5. What do you understand by Dependency Injection?
- The main idea in Dependency Injection is that you don’t have to create your objects but you just have to describe how they should be created.
  - The components and services need not be connected by us in the code directly. We have to describe which services are needed by which components in the configuration file. The IoC container present in Spring will wire them up together.
  - In Java, the 2 major ways of achieving dependency injection are:
    - Constructor injection: Here, the IoC container invokes the class constructor with a number of arguments where each argument represents a dependency on the other class.
    - Setter injection: Here, the spring container calls the setter methods on the beans after invoking a no-argument static factory method or default constructor to instantiate the bean.

### 6. Explain the difference between constructor and setter injection?
- In constructor injection, partial injection is not allowed whereas it is allowed in setter injection.
- The constructor injection doesn’t override the setter property whereas the same is not true for setter injection.
- Constructor injection creates a new instance if any modification is done. The creation of a new instance is not possible in setter injection.
- In case the bean has many properties, then constructor injection is preferred. If it has few properties, then setter injection is preferred.

### 7. What are Spring Beans?
- They are the objects forming the backbone of the user’s application and are managed by the Spring IoC container.
- Spring beans are instantiated, configured, wired, and managed by IoC container.
- Beans are created with the configuration metadata that the users supply to the container (by means of XML or java annotations configurations.)

### 8. How is the configuration meta data provided to the spring container?
- The configuration metadata can be provided to the Spring container in the following ways:
  - XML based configuration:  The bean configurations and their dependencies are specified in XML configuration files. This starts with a bean tag as shown below:
  - ``` 
    <bean id="interviewBitBean" class="org.intervuewBit.firstSpring.InterviewBitBean">
    <property name="name" value="InterviewBit"></property>
    </bean> 
    ```
  - Annotation-based configuration: Instead of the XML approach, the beans can be configured into the component class itself by using annotations on the relevant class, method, or field declaration.
    - Annotation wiring is not active in the Spring container by default. This has to be enabled in the Spring XML configuration file as shown below
    - ```
      <beans>
      <context:annotation-config/>
      <!-- bean definitions go here -->
      </beans>
      ```
  - Java-based configuration: Spring Framework introduced key features as part of new Java configuration support. This makes use of the @Configuration annotated classes and @Bean annotated methods. 
    - Note that:
      - @Bean annotation has the same role as the <bean/> element.
      - Classes annotated with @Configuration allow to define inter-bean dependencies by simply calling other @Bean methods in the same class.

### 9. What are the bean scopes available in Spring?
- The Spring Framework has five scope supports. They are:

  1. Singleton: The scope of bean definition while using this would be a single instance per IoC container.
  2. Prototype: Here, the scope for a single bean definition can be any number of object instances.
  3. Request: The scope of the bean definition is an HTTP request.
  4. Session: Here, the scope of the bean definition is HTTP-session.
  5. Global-session: The scope of the bean definition here is a Global HTTP session. 
  - Note: The last three scopes are available only if the users use web-aware ApplicationContext containers.

### 10. Explain Bean life cycle in Spring Bean Factory Container.
- The Bean life cycle is as follows:
  - The IoC container instantiates the bean from the bean’s definition in the XML file.
  - Spring then populates all of the properties using the dependency injection as specified in the bean definition.
  - The bean factory container calls `setBeanName()` which take the bean ID and the corresponding bean has to implement `BeanNameAware` interface.
  - The factory then calls `setBeanFactory()` by passing an instance of itself (if BeanFactoryAware interface is implemented in the bean).
  - If `BeanPostProcessors` is associated with a bean, then the `preProcessBeforeInitialization()` methods are invoked.
  - If an init-method is specified, then it will be called.
  - Lastly, `postProcessAfterInitialization()` methods will be called if there are any `BeanPostProcessors` associated with the bean that needs to be run post creation.

### 11. What do you understand by Bean Wiring.

### 12. What is autowiring and name the different modes of it?

### 13. What are the limitations of autowiring?