## 26 Questions in total:
### 1. Although inheritance is a popular OOPs concept, it is less advantageous than composition. Explain.

### 2. What is the difference between ‘>>’ and ‘>>>’ operators in java?

### 3. What are Composition and Aggregation? State the difference.

### 4. How is the creation of a String using new() different from that of a literal?

### 5. How is the ‘new’ operator different from the ‘newInstance()’ operator in java?

### 6. Is exceeding the memory limit possible in a program despite having a garbage collector?

### 7. Why is synchronization necessary? Explain with the help of a relevant example.

### 8. In the given code below, what is the significance of ... ?
```java
public void fooBarMethod(String... variables){
   // method code
}
```

### 9. What will be the output of the below java program and define the steps of Execution of the java program with the help of the below code?
```javaclass InterviewBit{
    int i;
    static int j;
    {
        System.out.println(" Instance Block 1. Value of i = "+i);
    }
    static{
        System.out.println(" Static Block 1. Value of j = "+j);
        method_2();
    }
    {
        i = 5;
    }
    static{
        j = 10;
    }
    InterviewBit(){
        System.out.println(" Welcome to InterviewBit ");
    }
    public static void main(String[] args){
        InterviewBit ib = new InterviewBit();
    }
    public void method_1(){
        System.out.println(" Instance method. ");
    }
    static{
        System.out.println(" Static Block 2. Value of j = "+j);
    }
    {
        System.out.println(" Instance Block 2. Value of i = "+i);
        method_1();
    }
    public static void method_2(){
        System.out.println(" Static method. ");
    }
}
```

### 10. Define System.out.println().

### 11. Can you explain the Java thread lifecycle?

### 12. What could be the tradeoff between the usage of an unordered array versus the usage of an ordered array?

### 13. Is it possible to import the same class or package twice in Java and what happens to it during runtime?

### 14. In case a package has sub packages, will it suffice to import only the main package? e.g. Does importing of com.myMainPackage.* also import com.myMainPackage.mySubPackage.*?

### 15. Will the finally block be executed if the code System.exit(0) is written at the end of try block?

### 16. What do you understand by marker interfaces in Java?

### 17. Explain the term “Double Brace Initialisation” in Java?

### 18. Why is it said that the length() method of String class doesn't return accurate results?

### 19. What is the output of the below code and why?
```java
public class InterviewBit{
   public static void main(String[] args)
   {
       System.out.println('b' + 'i' + 't');
   }
}
```

### 20. What are the possible ways of making object eligible for garbage collection (GC) in Java?

### 21. In the below Java Program, how many objects are eligible for garbage collection?
```java
class Main{
   public static void main(String[] args){
       int[][] num = new int[3][];
       num[0] = new int[5];
       num[1] = new int[2];
       num[2] = new int[3];
       
       num[2] = new int[5];
       num[0] = new int[4];
       num[1] = new int[3];
       
       num = new int[2][];
   }
}
```

### 22. What is the best way to inject dependency? Also, state the reason.

### 23. How we can set the spring bean scope. And what supported scopes does it have?

### 24. What are the different categories of Java Design patterns?

### 25. What is a Memory Leak? Discuss some common causes of it.

### 26. Assume a thread has a lock on it, calling the sleep() method on that thread will release the lock?