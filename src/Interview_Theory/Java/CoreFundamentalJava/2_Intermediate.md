## 39 Questions in total:
### 1. Apart from the security aspect, what are the reasons behind making strings immutable in Java?

### 2. What is a singleton class in Java? And How to implement a singleton class?

### 3. Which of the below generates a compile-time error? State the reason.
###### 1. int[] n1 = new int[0];
###### 2. boolean[] n2 = new boolean[-200];
###### double[] n3 = new double[2241423798];
###### 4. char[] ch = new char[20];

### 4. How would you differentiate between a String, StringBuffer, and a StringBuilder?

### 5. Using relevant properties highlight the differences between interfaces and abstract classes.

### 6. Is this program giving a compile-time error? If Yes then state the reason and number of errors it will give. If not then state the reason.
```java
abstract final class InterviewBit{
  public abstract void printMessage();
}
class ScalarAcademy extends InterviewBit{
   public void printMessage(){
       System.out.println("Welcome to Scalar Academy By InterviewBit");
   }
}
class ScalarTopics extends ScalarAcademy{
   public void printMessage(){
       System.out.println("Welcome to Scalar Topics By Scalar Academy");
   }
}
public class Main{
	public static void main(String[] args) {
 	    InterviewBit ib = new ScalarTopics();
 	    ib.printMessage();
	}
}
```

### 7. What is a Comparator in java?

### 8. In Java, static as well as private method overriding is possible. Comment on the statement.

### 9. What makes a HashSet different from a TreeSet?

### 10. Why is the character array preferred over string for storing confidential information?

### 11. What do we get in the JDK file?

### 12. What are the differences between JVM, JRE and JDK in Java?

### 13. What are the differences between HashMap and HashTable in Java?

### 14. What is the importance of reflection in Java?

### 15. What are the different ways of threads usage?

### 16. What are the different types of Thread Priorities in Java? And what is the default priority of a thread assigned by JVM?

### 17. What is the difference between the program and the process?

### 18. What is the difference between the ‘throw’ and ‘throws’ keyword in java?

### 19. What are the differences between constructor and method of a class in Java?

### 20. Identify the output of the below java program and Justify your answer.
```java
class Main {
    public static void main(String args[]) {
        Scaler s = new Scaler(5);
    }
}
class InterviewBit{
    InterviewBit(){
        System.out.println(" Welcome to InterviewBit ");
    }
}
class Scaler extends InterviewBit{
    Scaler(){
        System.out.println(" Welcome to Scaler Academy ");
    }
    Scaler(int x){
        this();
        super();
        System.out.println(" Welcome to Scaler Academy 2");
    }
}
```

### 21. Java works as “pass by value” or “pass by reference” phenomenon?

### 22. What is the ‘IS-A ‘ relationship in OOPs java? 

### 23. Which among String or String Buffer should be preferred when there are lot of updates required to be done in the data?

### 24. How to not allow serialization of attributes of a class in Java?

### 25. What happens if the static modifier is not included in the main method signature in Java?

### 26. Consider the below program, identify the output, and also state the reason for that.
```java
public class Main{
public static void main(String[] args) {
 System.out.println(" Hello. Main Method. ");
}
public static void main(int[] args) {
 System.out.println(" Hello. Main Method2. ");
}
}
```

### 27. Can we make the main() thread a daemon thread?

### 28. What happens if there are multiple main methods inside one class in Java?

### 29. What do you understand by Object Cloning and how do you achieve it in Java?

### 30. How does an exception propagate in the code?

### 31. How do exceptions affect the program if it doesn't handle them?

### 32. Is it mandatory for a catch block to be followed after a try block?

### 33. Will the finally block get executed when the return statement is written at the end of try block and catch block as shown below?
```java
public int someMethod(int i){
   try{
       //some statement
       return 1;
   }catch(Exception e){
       //some statement
       return 999;
   }finally{
       //finally block statements
   }
}
```

### 34. Can you call a constructor of a class inside the another constructor?

### 35. Contiguous memory locations are usually used for storing actual values in an array but not in ArrayList. Explain.

### 36. Why does the java array index start with 0?

### 37. Why is the remove method faster in the linked list than in an array?

### 38. How many overloaded add() and addAll() methods are available in the List interface? Describe the need and uses.

### 39. How does the size of ArrayList grow dynamically? And also state how it is implemented internally.


