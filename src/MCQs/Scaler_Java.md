# Java Programming Questions and Answers

1. **What is the purpose of the `toList()` collector in the `collect()` method?**

2. **In the context of multithreading, what is a thread pool?**
    - **d. A group of threads that are reused to perform tasks**

3. **What is the significance of the wildcard "?" in generic types?**
    - **b. represents an unknown type**

4. **Method overloading achieves which type of polymorphism?**
    - **Compile-time polymorphism**

5. **Which type of copy is generally more suited for complex data structures with nested objects?**
    - **deep copy**

6. **In Java, which class provides the methods `wait()`, `notify()`, and `notifyAll()`?**
    - **Object**

7. **Which exception is thrown when Java is out of memory?**
    - **OutOfMemoryError**

8. **Which is true about concurrency and parallel execution?**
    - **b. Concurrency is the simultaneous execution of multiple tasks, while parallel execution involves tasks running at the same time on multiple processes**

9. **Which keyword is used to prevent a method from being overridden in a subclass?**
    - **final**

10. **What does the `get()` method of the `Future` interface do?**
    - **a. retrieves the result of the computation, blocking if necessary until it is ready**

11. **What is the output of the following code?**
    ```java
    class MyThread extends Thread {
        public void run() {
            for(int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getId() + " Value " + i);
            }
        }
    }

    public class TestThreads {
        public static void main(String[] args) {
            MyThread t1 = new MyThread();
            MyThread t2 = new MyThread();
            t1.start();
            t2.start();
        }
    }
    ```
    - **c. order of output is unpredictable**

12. **What does the term "concurrent" mean in the context of concurrent collections?**

13. **Can an interface have a static method?**
    - **d. Yes**

14. **Which method in `ConcurrentHashMap` is used for inserting a key-value pair if the key is not already associated with a value?**
    - **putIfAbsent**

15. **If a variable is declared as `volatile`, what guarantee does it provide regarding the order of execution of instructions involving that variable?**
    - **a. Guarantees no specific order of execution for instructions involving the variable**

16. **In the context of the thread lifecycle, what does the BLOCKED state indicate?**
    - **b. the thread is waiting for a resource that is currently held by another thread**

17. **What is the main function of the Java executor framework?**
    - **b. create and manage thread pools for concurrent execution**

18. **Which method is used to compare two strings for equality in a case-insensitive manner?**
    - **equalsIgnoreCase**

19. **What is the purpose of the `collect()` method in Java Streams?**
    - **c. terminate a stream and produce a result or a collection**

20. **In Java, what is the purpose of the `join` method in the `Thread` class?**
    - **a. to wait for the completion of a thread before proceeding with the main thread**

21. **Which is true regarding synchronized blocks in Java?**
    - **a. Synchronized blocks are more efficient than using the synchronized keyword on the entire method**

22. **Which is true regarding the `ReentrantLock` class?**
    - **c. provides more fine-grained control over lock acquisition and release**

23. **In the context of Java Streams, what is a parallel stream?**
    - **b. stream that is processed concurrently using multiple threads**

24. **Which modifiers are implicitly assumed for all variables declared in an interface?**
    - **public, static, and final (constants)**

25. **What are the states of a thread in Java?**

26. **What is the purpose of using `Collections.synchronizedMap` with a `HashMap` in Java?**
    - **a. to synchronize access to the `HashMap` for thread safety**

27. **Which method in the `ExecutorService` interface is used to schedule a task to run after a specified delay?**
    - **d. schedule()**

28. **What is the advantage of using a cached thread pool in the Java executor framework?**
    - **d. dynamically adjusts the number of threads based on the workload**

29. **What does it mean if a member is declared as "protected" in terms of encapsulation?**

30. **What is the role of the Banker's algorithm in preventing deadlocks?**
    - **b. allocates resources based on a safe sequence**

31. **What does the `volatile` keyword prevent?**
    - **a. race conditions in multithreaded programs**

32. **What is the root interface of the Java Collection Framework?**
    - **Collection**

33. **Which access modifier restricts the visibility of a member to the same class only?**
    - **private**

34. **Thread A acquires a semaphore with an initial count of 1, and then Thread B tries to acquire the same semaphore. What happens?**
    - **a. Thread B is blocked until Thread A releases the semaphore**

35. **Predict the output:**
    ```java
    public class MyClass {
        public static void main(String[] args) {
            MyClass obj = new MyClass();
            obj.display();
        }
        static void display() {
            System.out.println("Static method");
        }
    }
    ```
    - **c. Static method**

36. **What type of polymorphism is demonstrated in the following code?**
    ```java
    class Animal {
        void makeSound() {
            System.out.println("Some sound");
        }
    }

    class Dog extends Animal {
        void makeSound() {
            System.out.println("Woof");
        }
    }
    ```
    - **d. Runtime polymorphism**

37. **Predict the output:**
    ```java
    List<String> list = new ArrayList<>(List.of("apple", "mango", "guava"));
    Comparator<String> cmp = (s1, s2) -> s2.compareTo(s1);
    Collections.sort(list, cmp);
    System.out.println(list);
    ```
    - **b. [mango, guava, apple]**

38. **What does the following line of code do?**
    ```java
    int valueB = concurrentMap.compute("B", (key, oldValue) -> (oldValue == null) ? 1 : oldValue + 1);
    ```
    - **b. Computes value of B using given lambda expression and returns it**

39. **What is the output of the following code?**
    ```java
    public class LambdaExpressionTest {
        public static void main(String[] args) {
            int x = 10;
            Runnable r = () -> System.out.println(x);
            Thread t = new Thread(r);
            t.start();
        }
    }
    ```
    - **a. 10**

40. **What is the output of the following code?**
    ```java
    public class MyClass {
        static int x = 10;
        public static void main(String[] args) {
            MyClass obj1 = new MyClass();
            MyClass obj2 = new MyClass();
            obj1.x = 20;
            System.out.println(obj1.x + " " + obj2.x);
        }
    }
    ```
    - **a. 20 20**

41. **Predict the output:**
    ```java
    int sum = 0;
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    numbers.forEach(n -> sum += n);
    System.out.println(sum);
    ```
    - **b. compile error**


### Java Programming Questions and Answers

1. **What is the purpose of the toList() collector in the collect() method?**
    - **Answer:** To accumulate elements into a list.
    - **Explanation:** `Collectors.toList()` is a common collector that accumulates the input elements into a new `List`.

2. **In the context of multithreading, what is a thread pool?**
    - **Answer:** A collection of threads waiting for execution.
    - **Explanation:** A thread pool is a pool of worker threads that efficiently manage the execution of multiple tasks without creating new threads each time.

3. **What is the significance of the wildcard "?" in generic types?**
    - **Answer:** Represents an unknown type.
    - **Explanation:** The wildcard `?` in generics is used to denote an unknown type and can be used in various scenarios like upper and lower bounds.

4. **Method overloading achieves which type of polymorphism?**
    - **Answer:** Compile-time polymorphism.
    - **Explanation:** Method overloading is resolved at compile time and is thus considered compile-time polymorphism.

5. **Which type of copy is generally more suited for complex data structures with nested objects?**
    - **Answer:** Deep copy.
    - **Explanation:** Deep copy creates a new instance of the complex data structure, duplicating all nested objects to avoid shared references.

6. **In Java, which class provides the methods wait(), notify(), and notifyAll()?**
    - **Answer:** Object.
    - **Explanation:** These methods are defined in the `Object` class because they are fundamental to Java's intrinsic locking mechanism.

7. **Which exception is thrown when Java is out of memory?**
    - **Answer:** OutOfMemoryError.
    - **Explanation:** The `OutOfMemoryError` is thrown when the JVM cannot allocate an object due to insufficient memory.

8. **Which is true about concurrency and parallel execution?**
    - **Answer:** Concurrency is the simultaneous execution of multiple tasks, while parallel execution involves tasks running at the same time on multiple processors.
    - **Explanation:** Concurrency and parallel execution are distinct; concurrency refers to the task-level execution while parallel execution leverages multiple processors.

9. **Which keyword is used to prevent a method from being overridden in a subclass?**
    - **Answer:** final.
    - **Explanation:** The `final` keyword prevents a method from being overridden in any subclass.

10. **What does the get() method of the Future interface do?**
    - **Answer:** Retrieves the result of the computation, blocking if necessary until it is ready.
    - **Explanation:** The `get()` method waits if necessary for the computation to complete and then retrieves its result.

11. **What is the output of the following code?**
    ```java
    class MyThread extends Thread {
        public void run() {
            for(int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getId() + " Value " + i);
            }
        }
    }

    public class TestThreads {
        public static void main(String[] args) {
            MyThread t1 = new MyThread();
            MyThread t2 = new MyThread();
            t1.start();
            t2.start();
        }
    }
    ```
    - **Answer:** The order of output is unpredictable.
    - **Explanation:** The execution order of the threads is controlled by the thread scheduler, leading to an unpredictable output sequence.

12. **What does the term "concurrent" mean in the context of concurrent collections?**
    - **Answer:** Concurrent collections are designed to handle concurrent access by multiple threads without compromising data consistency.
    - **Explanation:** Concurrent collections provide thread-safe operations without the need for external synchronization.

13. **What is the output of the following code?**
    ```java
    public class MyClass {
        static int x = 10;
        public static void main(String[] args) {
            MyClass obj1 = new MyClass();
            MyClass obj2 = new MyClass();
            obj1.x = 20;
            System.out.println(obj1.x + " " + obj2.x);
        }
    }
    ```
    - **Answer:** 20 20
    - **Explanation:** Static variables are shared among all instances of a class, so changing `x` through `obj1` affects `obj2` as well.

14. **Can an interface have a static method?**
    - **Answer:** Yes.
    - **Explanation:** Since Java 8, interfaces can have static methods.

15. **Which method in ConcurrentHashMap is used for inserting a key-value pair if the key is not already associated with a value?**
    - **Answer:** putIfAbsent.
    - **Explanation:** The `putIfAbsent` method inserts the key-value pair only if the key is not already present in the map.

17. **If a variable is declared as volatile, what guarantee does it provide regarding the order of execution of instructions involving that variable?**
    - **Answer:** Guarantees the instructions will be executed in the order they appear in the code.
    - **Explanation:** The `volatile` keyword ensures visibility and ordering of variable changes across threads.

19. **In the context of the thread lifecycle, what does the BLOCKED state indicate?**
    - **Answer:** The thread is waiting for a resource that is currently held by another thread.
    - **Explanation:** A thread enters the BLOCKED state when it is waiting for a monitor lock to enter a synchronized block or method.

21. **What is the main function of the Java Executor framework?**
    - **Answer:** Create and manage thread pools for concurrent execution.
    - **Explanation:** The Executor framework provides tools for managing and controlling the execution of asynchronous tasks.

23. **Which method is used to compare two strings for equality in a case-insensitive manner?**
    - **Answer:** equalsIgnoreCase.
    - **Explanation:** The `equalsIgnoreCase` method compares two strings, ignoring differences in case.

24. **What is the purpose of the collect() method in Java Streams?**
    - **Answer:** Terminate a stream and produce a result or a collection.
    - **Explanation:** The `collect` method is a terminal operation that transforms the elements of a stream into a different form, usually a collection.

25. **In Java, what is the purpose of the join method in the Thread class?**
    - **Answer:** To wait for the completion of a thread before proceeding with the main thread.
    - **Explanation:** The `join` method allows one thread to wait for the completion of another.

26. **Which is true regarding synchronized blocks in Java?**
    - **Answer:** Synchronized blocks are more efficient than using the synchronized keyword on the entire method.
    - **Explanation:** Synchronized blocks provide more granular control over the synchronization scope, potentially reducing contention and improving performance.

28. **Predict the output:**
    ```java
    List<String> list = new ArrayList<>(List.of("apple", "mango", "guava"));
    Comparator<String> cmp = (s1, s2) -> s2.compareTo(s1);
    Collections.sort(list, cmp);
    System.out.println(list);
    ```
    - **Answer:** [mango, guava, apple]
    - **Explanation:** The comparator sorts the list in descending order.

29. **Which is true regarding the ReentrantLock class?**
    - **Answer:** Provides more fine-grained control over lock acquisition and release.
    - **Explanation:** `ReentrantLock` offers advanced capabilities such as timed and interruptible lock acquisition.

30. **In the context of Java streams, what is a parallel stream?**
    - **Answer:** A stream that is processed concurrently using multiple threads.
    - **Explanation:** Parallel streams divide the processing of elements among multiple threads to speed up the operation.

31. **Which modifiers are implicitly assumed for all variables declared in an interface?**
    - **Answer:** public, static, and final (constants).
    - **Explanation:** Variables in interfaces are implicitly `public`, `static`, and `final`.

32. **What are the states of a thread in Java?**
    - **Answer:** New, Runnable, Blocked, Waiting, Timed Waiting, and Terminated.
    - **Explanation:** These states represent the lifecycle stages of a thread.

33. **What is the purpose of using Collections.synchronizedMap with a HashMap in Java?**
    - **Answer:** To synchronize access to the HashMap for thread safety.
    - **Explanation:** `Collections.synchronizedMap` provides a synchronized (thread-safe) map.

35. **Which method in the ExecutorService interface is used to schedule a task to run after a specified delay?**
    - **Answer:** schedule().
    - **Explanation:** The `schedule` method in `ScheduledExecutorService` schedules a task to run after a specified delay.

36. **Predict the output:**
    ```java
    int sum = 0;
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    numbers.forEach(n -> sum += n);
    System.out.println(sum);
    ```
    - **Answer:** Compile error.
    - **Explanation:** The variable `sum` must be effectively final to be used in a lambda expression.

37. **What is the advantage of using a cached thread pool in the Java Executor framework?**
    - **Answer:** Dynamically adjusts the number of threads based on the workload.
    - **Explanation:** Cached thread pools create new threads as needed and reuse previously constructed threads when they are available.