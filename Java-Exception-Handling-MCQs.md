# Complete Java Exception Handling MCQs - 

## 1. Basic Exception Hierarchy
```java
public class Test {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;
        } catch (Exception e) {
            System.out.println(e.getClass().getSimpleName());
        }
    }
}
```
**What is the output?**
a) Exception  
b) RuntimeException  
c) ArithmeticException  
d) Compilation error  

**Answer: c) ArithmeticException**  
**Explanation:** Division by zero throws ArithmeticException, which is caught by the broader Exception catch block. getClass().getSimpleName() returns the actual exception class name.

---

## 2. Checked vs Unchecked Exceptions
```java
class Test {
    public static void method1() throws IOException {
        throw new FileNotFoundException("File not found");
    }

    public static void method2() {
        throw new NullPointerException("Null pointer");
    }

    public static void main(String[] args) {
        method1(); // Line A
        method2(); // Line B
    }
}
```
**What happens at compilation?**
a) Both lines compile successfully  
b) Compilation error at Line A only  
c) Compilation error at Line B only  
d) Compilation error at both lines  

**Answer: b) Compilation error at Line A only**  
**Explanation:** FileNotFoundException is a checked exception that must be handled or declared. NullPointerException is unchecked and doesn't require handling.

---

## 3. Multiple Catch Blocks Order
```java
public class Test {
    public static void main(String[] args) {
        try {
            String str = null;
            str.length();
        } catch (RuntimeException e) {
            System.out.print("Runtime ");
        } catch (NullPointerException e) {
            System.out.print("NullPointer ");
        } catch (Exception e) {
            System.out.print("Exception ");
        }
    }
}
```
**What happens?**
a) Prints: Runtime  
b) Prints: NullPointer  
c) Compilation error  
d) Prints: Exception  

**Answer: c) Compilation error**  
**Explanation:** NullPointerException is a subclass of RuntimeException. More specific exceptions must be caught before more general ones.

---

## 4. Try-With-Resources
```java
class MyResource implements AutoCloseable {
    String name;
    MyResource(String name) { this.name = name; }

    public void close() {
        System.out.print(name + "-Close ");
    }

    void use() {
        System.out.print(name + "-Use ");
    }
}

public class Test {
    public static void main(String[] args) {
        try (MyResource r1 = new MyResource("R1");
             MyResource r2 = new MyResource("R2")) {
            r1.use();
            r2.use();
        }
    }
}
```
**What is the output?**
a) R1-Use R2-Use R1-Close R2-Close  
b) R1-Use R2-Use R2-Close R1-Close  
c) R2-Use R1-Use R1-Close R2-Close  
d) R2-Use R1-Use R2-Close R1-Close  

**Answer: b) R1-Use R2-Use R2-Close R1-Close**  
**Explanation:** Resources are closed in reverse order of their declaration (LIFO - Last In, First Out).

---

## 5. Exception in Finally Block
```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.print("Try ");
            throw new RuntimeException("Try Exception");
        } catch (Exception e) {
            System.out.print("Catch ");
            throw new RuntimeException("Catch Exception");
        } finally {
            System.out.print("Finally ");
            throw new RuntimeException("Finally Exception");
        }
    }
}
```
**What happens?**
a) Prints: Try Catch Finally, then throws "Try Exception"  
b) Prints: Try Catch Finally, then throws "Finally Exception"  
c) Prints: Try Catch Finally, then throws "Catch Exception"  
d) Compilation error  

**Answer: b) Prints: Try Catch Finally, then throws "Finally Exception"**  
**Explanation:** Finally block always executes. If finally throws an exception, it suppresses any previous exceptions from try/catch blocks.

---

## 6. Custom Exception Hierarchy
```java
class CustomException extends Exception {
    CustomException(String msg) { super(msg); }
}

class SpecificException extends CustomException {
    SpecificException(String msg) { super(msg); }
}

class Test {
    static void method() throws CustomException {
        throw new SpecificException("Specific error");
    }

    public static void main(String[] args) {
        try {
            method();
        } catch (SpecificException e) {
            System.out.print("Specific ");
        } catch (CustomException e) {
            System.out.print("Custom ");
        }
    }
}
```
**What is the output?**
a) Specific  
b) Custom  
c) Compilation error  
d) Both Specific and Custom  

**Answer: a) Specific**  
**Explanation:** Most specific exception is caught first. SpecificException is more specific than CustomException.

---

## 7. Exception Propagation
```java
class Test {
    static void method1() {
        method2();
        System.out.print("Method1 ");
    }

    static void method2() {
        method3();
        System.out.print("Method2 ");
    }

    static void method3() {
        throw new RuntimeException("Error");
    }

    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.print("Caught ");
        }
    }
}
```
**What is the output?**
a) Method2 Method1 Caught  
b) Method1 Method2 Caught  
c) Caught  
d) Method3 Method2 Method1 Caught  

**Answer: c) Caught**  
**Explanation:** When method3() throws exception, it immediately propagates up the call stack without executing remaining statements in method2() and method1().

---

## 8. Suppressed Exceptions in Try-With-Resources
```java
class Resource implements AutoCloseable {
    public void close() {
        throw new RuntimeException("Close Exception");
    }
}

public class Test {
    public static void main(String[] args) {
        try (Resource r = new Resource()) {
            throw new RuntimeException("Try Exception");
        } catch (Exception e) {
            System.out.print(e.getMessage() + " ");
            System.out.print(e.getSuppressed().length);
        }
    }
}
```
**What is the output?**
a) Close Exception 0  
b) Try Exception 1  
c) Try Exception 0  
d) Close Exception 1  

**Answer: b) Try Exception 1**  
**Explanation:** Primary exception from try block is thrown, close() exception becomes suppressed and can be accessed via getSuppressed().

---

## 9. Method Overriding with Exceptions
```java
class Parent {
    void method() throws IOException {
        throw new IOException("Parent");
    }
}

class Child extends Parent {
    void method() throws FileNotFoundException {
        throw new FileNotFoundException("Child");
    }
}

public class Test {
    public static void main(String[] args) {
        try {
            Parent p = new Child();
            p.method();
        } catch (IOException e) {
            System.out.print(e.getMessage());
        }
    }
}
```
**What is the output?**
a) Parent  
b) Child  
c) Compilation error  
d) IOException  

**Answer: b) Child**  
**Explanation:** Child can throw same or subclass exceptions. FileNotFoundException is subclass of IOException. Runtime polymorphism calls Child's method.

---

## 10. Exception Chaining
```java
public class Test {
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.print(e.getMessage() + " ");
            System.out.print(e.getCause().getMessage());
        }
    }

    static void method1() throws Exception {
        try {
            method2();
        } catch (RuntimeException e) {
            throw new Exception("Method1 Exception", e);
        }
    }

    static void method2() {
        throw new NullPointerException("Method2 Exception");
    }
}
```
**What is the output?**
a) Method1 Exception Method2 Exception  
b) Method2 Exception Method1 Exception  
c) Method1 Exception null  
d) NullPointerException  

**Answer: a) Method1 Exception Method2 Exception**  
**Explanation:** Exception chaining allows preserving original exception as cause. getCause() returns the wrapped original exception.

---

## 11. Assert Statement with Exceptions
```java
public class Test {
    public static void main(String[] args) {
        try {
            int x = 5;
            assert x > 10 : "x should be greater than 10";
            System.out.print("After assert ");
        } catch (AssertionError e) {
            System.out.print("Assertion failed: " + e.getMessage());
        }
    }
}
```
**What happens when run with assertions enabled (-ea)?**
a) Prints: After assert  
b) Prints: Assertion failed: x should be greater than 10  
c) Compilation error  
d) No output  

**Answer: b) Prints: Assertion failed: x should be greater than 10**  
**Explanation:** When assertions are enabled and assertion fails, AssertionError is thrown with the specified message.

---

## 12. Return in Try-Catch-Finally
```java
public class Test {
    static int method() {
        try {
            return 1;
        } catch (Exception e) {
            return 2;
        } finally {
            return 3;
        }
    }

    public static void main(String[] args) {
        System.out.print(method());
    }
}
```
**What is the output?**
a) 1  
b) 2  
c) 3  
d) Compilation error  

**Answer: c) 3**  
**Explanation:** Finally block's return statement overrides any return from try or catch blocks.

---

## 13. Exception Translation
```java
class BusinessException extends Exception {
    BusinessException(String msg, Throwable cause) { super(msg, cause); }
}

class DataAccessLayer {
    void saveData() throws SQLException {
        throw new SQLException("Database connection failed");
    }
}

class BusinessLayer {
    DataAccessLayer dal = new DataAccessLayer();

    void processData() throws BusinessException {
        try {
            dal.saveData();
        } catch (SQLException e) {
            throw new BusinessException("Business operation failed", e);
        }
    }
}

public class Test {
    public static void main(String[] args) {
        try {
            new BusinessLayer().processData();
        } catch (BusinessException e) {
            System.out.print(e.getCause().getClass().getSimpleName());
        }
    }
}
```
**What is the output?**
a) BusinessException  
b) SQLException  
c) Exception  
d) Throwable  

**Answer: b) SQLException**  
**Explanation:** Exception translation wraps lower-level exceptions in higher-level exceptions. getCause() returns the original SQLException.

---

## 14. Multi-Catch Block
```java
public class Test {
    public static void main(String[] args) {
        try {
            String str = args[0];
            int num = Integer.parseInt(str);
            int result = 10 / num;
            System.out.print(result);
        } catch (ArrayIndexOutOfBoundsException | NumberFormatException e) {
            System.out.print("Input Error");
        } catch (ArithmeticException e) {
            System.out.print("Math Error");
        }
    }
}
```
**What happens when run with no arguments?**
a) Prints: Input Error  
b) Prints: Math Error  
c) Exception is thrown  
d) Compilation error  

**Answer: a) Prints: Input Error**  
**Explanation:** Accessing args[0] when no arguments provided throws ArrayIndexOutOfBoundsException, caught by multi-catch block.

---

## 15. Exception in Static Block
```java
public class Test {
    static {
        System.out.print("Static block ");
        if (true) {
            throw new RuntimeException("Static exception");
        }
    }

    public static void main(String[] args) {
        System.out.print("Main method");
    }
}
```
**What happens?**
a) Prints: Static block Main method  
b) Prints: Static block, then throws exception  
c) Prints: Main method  
d) Compilation error  

**Answer: b) Prints: Static block, then throws exception**  
**Explanation:** Exception in static block prevents class initialization and causes ExceptionInInitializerError to be thrown.

---

## 16. Nested Try-Catch Blocks
```java
public class Test {
    public static void main(String[] args) {
        try {
            try {
                int[] arr = {1, 2};
                System.out.print(arr[5]);
            } catch (NullPointerException e) {
                System.out.print("Inner NPE ");
            }
            System.out.print("After inner try ");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.print("Outer AIOBE ");
        }
    }
}
```
**What is the output?**
a) Inner NPE After inner try  
b) Outer AIOBE  
c) Inner NPE Outer AIOBE  
d) After inner try  

**Answer: b) Outer AIOBE**  
**Explanation:** ArrayIndexOutOfBoundsException is not caught by inner catch (which only catches NPE), so it propagates to outer catch.

---

## 17. Exception Handling in Constructor
```java
class MyClass {
    MyClass() throws Exception {
        System.out.print("Constructor ");
        throw new Exception("Constructor exception");
    }
}

public class Test {
    public static void main(String[] args) {
        try {
            MyClass obj = new MyClass();
            System.out.print("Object created ");
        } catch (Exception e) {
            System.out.print("Exception caught ");
        }
    }
}
```
**What is the output?**
a) Constructor Object created  
b) Constructor Exception caught  
c) Object created Exception caught  
d) Exception caught  

**Answer: b) Constructor Exception caught**  
**Explanation:** Constructor throws exception after printing, so object creation fails and exception is caught.

---

## 18. Checked Exception in Lambda
```java
import java.util.*;
import java.io.*;

public class Test {
    public static void main(String[] args) {
        List<String> files = Arrays.asList("file1.txt", "file2.txt");

        files.forEach(filename -> {
            try {
                throw new IOException("File error");
            } catch (IOException e) {
                System.out.print("Caught ");
            }
        });
    }
}
```
**What is the output?**
a) Caught  
b) Caught Caught  
c) Compilation error  
d) IOException  

**Answer: b) Caught Caught**  
**Explanation:** Lambda executes for each element in list (2 elements), each throwing and catching IOException.

---

## 19. Exception Handling with Inheritance
```java
class A {
    void method() throws IOException { }
}

class B extends A {
    void method() throws Exception { // Line X
        super.method();
    }
}
```
**What happens at Line X?**
a) Compiles successfully  
b) Compilation error - broader exception not allowed  
c) Runtime error  
d) Must use throws IOException  

**Answer: b) Compilation error - broader exception not allowed**  
**Explanation:** Overriding method cannot throw broader checked exceptions than the parent method declares.

---

## 20. Finally Block Execution
```java
public class Test {
    static boolean finallyExecuted = false;

    static int method() {
        try {
            System.exit(0);
            return 1;
        } finally {
            finallyExecuted = true;
            System.out.print("Finally ");
        }
    }

    public static void main(String[] args) {
        method();
        System.out.print(finallyExecuted);
    }
}
```
**What is the output?**
a) Finally true  
b) Finally false  
c) No output  
d) false  

**Answer: c) No output**  
**Explanation:** System.exit() terminates JVM immediately, preventing finally block execution.

---

## 21. Exception Matching Hierarchy
```java
public class Test {
    public static void main(String[] args) {
        try {
            throw new FileNotFoundException("File not found");
        } catch (IOException e) {
            System.out.print("IOException ");
        } catch (Exception e) {
            System.out.print("Exception ");
        } catch (FileNotFoundException e) {
            System.out.print("FileNotFoundException ");
        }
    }
}
```
**What happens?**
a) Prints: IOException  
b) Prints: FileNotFoundException  
c) Prints: Exception  
d) Compilation error  

**Answer: d) Compilation error**  
**Explanation:** FileNotFoundException catch block is unreachable because it's already handled by IOException catch block above it.

---

## 22. Resource Management with Exception
```java
class MyResource implements AutoCloseable {
    boolean closed = false;

    public void close() throws Exception {
        closed = true;
        System.out.print("Resource closed ");
        throw new Exception("Close failed");
    }

    public void use() throws Exception {
        if (closed) throw new IllegalStateException("Resource already closed");
        System.out.print("Using resource ");
    }
}

public class Test {
    public static void main(String[] args) {
        try (MyResource resource = new MyResource()) {
            resource.use();
            throw new RuntimeException("Use failed");
        } catch (Exception e) {
            System.out.print("Caught: " + e.getClass().getSimpleName());
        }
    }
}
```
**What is the output?**
a) Using resource Resource closed Caught: RuntimeException  
b) Using resource Resource closed Caught: Exception  
c) Using resource Caught: IllegalStateException  
d) Resource closed Caught: Exception  

**Answer: a) Using resource Resource closed Caught: RuntimeException**  
**Explanation:** Primary exception from try block (RuntimeException) is thrown, close() exception becomes suppressed.

---

## 23. Exception Handling in Thread
```java
class MyThread extends Thread {
    public void run() {
        try {
            Thread.sleep(1000);
            throw new RuntimeException("Thread exception");
        } catch (InterruptedException e) {
            System.out.print("Interrupted ");
        }
    }
}

public class Test {
    public static void main(String[] args) {
        try {
            MyThread t = new MyThread();
            t.start();
            t.join();
        } catch (Exception e) {
            System.out.print("Main caught: " + e.getClass().getSimpleName());
        }
    }
}
```
**What happens?**
a) Prints: Interrupted  
b) Prints: Main caught: RuntimeException  
c) Prints: Main caught: InterruptedException  
d) Thread terminates with uncaught exception  

**Answer: d) Thread terminates with uncaught exception**  
**Explanation:** RuntimeException in thread's run() method is not caught, causing thread to terminate. Main thread's catch block cannot catch exceptions from other threads.

---

## 24. Exception Re-throwing
```java
public class Test {
    static void method1() throws Exception {
        try {
            method2();
        } catch (RuntimeException e) {
            System.out.print("Caught in method1 ");
            throw e; // Re-throwing
        }
    }

    static void method2() {
        throw new IllegalArgumentException("Invalid argument");
    }

    public static void main(String[] args) {
        try {
            method1();
        } catch (IllegalArgumentException e) {
            System.out.print("Caught in main ");
        }
    }
}
```
**What is the output?**
a) Caught in method1  
b) Caught in main  
c) Caught in method1 Caught in main  
d) IllegalArgumentException  

**Answer: c) Caught in method1 Caught in main**  
**Explanation:** Exception is caught in method1, printed, then re-thrown and caught again in main.

---

## 25. Exception with Generic Methods
```java
class Test {
    static <T extends Exception> void throwException(T exception) throws T {
        throw exception;
    }

    public static void main(String[] args) {
        try {
            throwException(new IOException("IO Error"));
        } catch (IOException e) {
            System.out.print("Caught IOException");
        }
    }
}
```
**What happens?**
a) Prints: Caught IOException  
b) Compilation error in throwException method  
c) Compilation error in main method  
d) Runtime error  

**Answer: a) Prints: Caught IOException**  
**Explanation:** Generic method with bounded type parameter can throw the parameterized exception type.

---

## 26. Exception Handling with Switch Expression
```java
public class Test {
    static String handleError(int code) {
        return switch (code) {
            case 1 -> throw new IllegalArgumentException("Invalid code 1");
            case 2 -> {
                try {
                    throw new RuntimeException("Error 2");
                } catch (RuntimeException e) {
                    yield "Handled: " + e.getMessage();
                }
            }
            default -> "Unknown code";
        };
    }

    public static void main(String[] args) {
        try {
            System.out.print(handleError(2));
        } catch (Exception e) {
            System.out.print("Main caught: " + e.getMessage());
        }
    }
}
```
**What is the output?**
a) Handled: Error 2  
b) Main caught: Error 2  
c) Main caught: Invalid code 1  
d) Unknown code  

**Answer: a) Handled: Error 2**  
**Explanation:** Switch expression with case 2 handles exception internally and yields the result.

---

## 27. Exception Specification Mismatch
```java
interface Calculator {
    int divide(int a, int b) throws ArithmeticException;
}

class SimpleCalculator implements Calculator {
    public int divide(int a, int b) throws Exception { // Line X
        if (b == 0) throw new Exception("Division by zero");
        return a / b;
    }
}
```
**What happens at Line X?**
a) Compiles successfully  
b) Compilation error - broader exception not allowed  
c) Must remove throws clause  
d) Should throw ArithmeticException only  

**Answer: b) Compilation error - broader exception not allowed**  
**Explanation:** Interface method declares ArithmeticException (unchecked), but implementation cannot throw broader checked Exception.

---

## 28. Exception in Object Initialization
```java
class Test {
    static int value = getValue();

    static int getValue() {
        System.out.print("Getting value ");
        throw new RuntimeException("Initialization failed");
    }

    public static void main(String[] args) {
        try {
            System.out.print("Value: " + Test.value);
        } catch (Exception e) {
            System.out.print("Exception: " + e.getMessage());
        }
    }
}
```
**What is the output?**
a) Getting value Value: 0  
b) Getting value Exception: Initialization failed  
c) Exception: Initialization failed  
d) Getting value, then ExceptionInInitializerError  

**Answer: d) Getting value, then ExceptionInInitializerError**  
**Explanation:** Exception during static initialization causes ExceptionInInitializerError to wrap the original exception.

---

## 29. Checked Exception Erasure
```java
class Test {
    @SuppressWarnings("unchecked")
    static <T extends Throwable> void throwUnchecked(Throwable t) throws T {
        throw (T) t;
    }

    public static void main(String[] args) {
        try {
            throwUnchecked(new IOException("Checked exception"));
        } catch (RuntimeException e) {
            System.out.print("Caught runtime: " + e.getClass().getSimpleName());
        } catch (Exception e) {
            System.out.print("Caught checked: " + e.getClass().getSimpleName());
        }
    }
}
```
**What is the output?**
a) Caught runtime: IOException  
b) Caught checked: IOException  
c) Compilation error  
d) ClassCastException  

**Answer: b) Caught checked: IOException**  
**Explanation:** Generic type erasure allows throwing checked exceptions as if they were unchecked, but the actual exception type remains IOException.

---

## 30. Exception Handling in Stream Operations
```java
import java.util.*;
import java.util.function.*;

class Test {
    static void riskyMethod(String s) throws Exception {
        if (s.length() > 3) throw new Exception("Too long: " + s);
        System.out.print(s + " ");
    }

    public static void main(String[] args) {
        List<String> words = Arrays.asList("hi", "hello", "bye");

        words.forEach(word -> {
            try {
                riskyMethod(word);
            } catch (Exception e) {
                System.out.print("[" + e.getMessage() + "] ");
            }
        });
    }
}
```
**What is the output?**
a) hi hello bye  
b) hi [Too long: hello] bye  
c) hi bye [Too long: hello]  
d) Exception  

**Answer: b) hi [Too long: hello] bye**  
**Explanation:** forEach processes elements in order. "hi" prints normally, "hello" throws exception (caught and message printed), "bye" prints normally.

---

## 31. Exception Handling with Method References
```java
import java.util.*;

class Test {
    static void process(String s) throws RuntimeException {
        if (s == null) throw new NullPointerException("Null string");
        System.out.print(s.toUpperCase() + " ");
    }

    public static void main(String[] args) {
        List<String> items = Arrays.asList("hello", null, "world");

        try {
            items.forEach(Test::process);
        } catch (NullPointerException e) {
            System.out.print("Caught: " + e.getMessage());
        }
    }
}
```
**What is the output?**
a) HELLO NULL WORLD  
b) HELLO Caught: Null string  
c) HELLO WORLD  
d) Caught: Null string  

**Answer: b) HELLO Caught: Null string**  
**Explanation:** First element processes normally, second element throws exception which terminates the forEach and gets caught.

---

## 32. Exception Masking in Finally
```java
class Test {
    static void method() throws Exception {
        Exception tryException = null;
        Exception finallyException = null;

        try {
            tryException = new Exception("Try block exception");
            throw tryException;
        } finally {
            finallyException = new Exception("Finally block exception");
            throw finallyException;
        }
    }

    public static void main(String[] args) {
        try {
            method();
        } catch (Exception e) {
            System.out.print(e.getMessage() + " ");
            System.out.print("Suppressed: " + e.getSuppressed().length);
        }
    }
}
```
**What is the output?**
a) Try block exception Suppressed: 0  
b) Finally block exception Suppressed: 1  
c) Finally block exception Suppressed: 0  
d) Try block exception Suppressed: 1  

**Answer: b) Finally block exception Suppressed: 1**  
**Explanation:** Finally block exception masks try block exception. Try block exception becomes suppressed exception.

---

## 33. Exception Handling with Varargs
```java
class Test {
    static void process(String... args) throws Exception {
        for (String arg : args) {
            if (arg == null) throw new Exception("Null argument at position");
            System.out.print(arg + " ");
        }
    }

    public static void main(String[] args) {
        try {
            process("A", "B");
            process("C", null, "D");
        } catch (Exception e) {
            System.out.print("Exception caught");
        }
    }
}
```
**What is the output?**
a) A B C D Exception caught  
b) A B C Exception caught  
c) A B Exception caught  
d) A B C null D Exception caught  

**Answer: b) A B C Exception caught**  
**Explanation:** First call succeeds, second call processes "C" then throws exception on null, caught in main.

---

## 34. Exception Handling in Enum Constructor
```java
enum Status {
    ACTIVE("A") {
        void process() throws Exception {
            throw new Exception("Active processing failed");
        }
    },
    INACTIVE("I") {
        void process() {
            System.out.print("Inactive processed ");
        }
    };

    private String code;
    Status(String code) { this.code = code; }
    abstract void process() throws Exception;
}

public class Test {
    public static void main(String[] args) {
        try {
            Status.INACTIVE.process();
            Status.ACTIVE.process();
        } catch (Exception e) {
            System.out.print("Caught: " + e.getMessage());
        }
    }
}
```
**What is the output?**
a) Inactive processed Caught: Active processing failed  
b) Caught: Active processing failed  
c) Inactive processed  
d) Active processing failed  

**Answer: a) Inactive processed Caught: Active processing failed**  
**Explanation:** INACTIVE.process() executes successfully, then ACTIVE.process() throws exception which is caught.

---

## 35. Exception Handling with Record Classes
```java
record Person(String name, int age) {
    Person {
        if (name == null) throw new IllegalArgumentException("Name cannot be null");
        if (age < 0) throw new IllegalArgumentException("Age cannot be negative");
        System.out.print("Person created: " + name + " ");
    }
}

public class Test {
    public static void main(String[] args) {
        try {
            Person p1 = new Person("Alice", 25);
            Person p2 = new Person("Bob", -5);
        } catch (IllegalArgumentException e) {
            System.out.print("Error: " + e.getMessage());
        }
    }
}
```
**What is the output?**
a) Person created: Alice Person created: Bob  
b) Person created: Alice Error: Age cannot be negative  
c) Error: Name cannot be null  
d) Error: Age cannot be negative  

**Answer: b) Person created: Alice Error: Age cannot be negative**  
**Explanation:** First Person creates successfully, second Person fails validation in compact constructor.

---
