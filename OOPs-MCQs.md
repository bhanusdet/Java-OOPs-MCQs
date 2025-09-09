# 🚀 Java OOPs MCQs - Tricky Questions

Welcome to the ultimate collection of Java Object-Oriented Programming MCQs! This comprehensive set of carefully crafted questions will test your understanding of core OOP concepts and prepare you for technical interviews.

## 1. Which of the following is NOT a pillar of Object-Oriented Programming?
a) Encapsulation  
b) Inheritance  
c) Compilation  
d) Polymorphism  

**Answer: c) Compilation**  
**Explanation:** The four pillars of OOP are Encapsulation, Inheritance, Polymorphism, and Abstraction.

---

## 2. What is the output of the following code?
```java
class Parent {
    void display() { System.out.println("Parent"); }
}
class Child extends Parent {
    void display() { System.out.println("Child"); }
}
public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.display();
    }
}
```
a) Parent  
b) Child  
c) Compilation Error  
d) Runtime Error  

**Answer: b) Child**  
**Explanation:** This demonstrates runtime polymorphism. The method called is determined by the actual object type (Child), not the reference type (Parent).

---

## 3. Which access modifier allows access within the same package and subclasses?
a) private  
b) default  
c) protected  
d) public  

**Answer: c) protected**  
**Explanation:** Protected members are accessible within the same package and by subclasses even if they're in different packages.

---

## 4. What will be the output?
```java
class A {
    static { System.out.print("A"); }
    { System.out.print("a"); }
}
class B extends A {
    static { System.out.print("B"); }
    { System.out.print("b"); }
}
public class Test {
    public static void main(String[] args) {
        new B();
    }
}
```
a) AaBb  
b) ABab  
c) aAbB  
d) BbAa  

**Answer: b) ABab**  
**Explanation:** Static blocks execute when class is loaded (parent first), then instance blocks during object creation (parent first).

---

## 5. Which of the following is true about abstract classes?
a) Cannot have constructors  
b) Cannot be instantiated directly  
c) Cannot have concrete methods  
d) Must have at least one abstract method  

**Answer: b) Cannot be instantiated directly**  
**Explanation:** Abstract classes can have constructors, concrete methods, and don't need abstract methods, but cannot be instantiated using new keyword.

---

## 6. What is the output?
```java
class Parent {
    Parent() { System.out.print("P"); }
}
class Child extends Parent {
    Child() { System.out.print("C"); }
}
public class Test {
    public static void main(String[] args) {
        new Child();
    }
}
```
a) PC  
b) CP  
c) P  
d) C  

**Answer: a) PC**  
**Explanation:** Parent constructor is called first (implicitly via super()), then child constructor executes.

---

## 7. Which keyword is used to prevent method overriding?
a) static  
b) final  
c) abstract  
d) synchronized  

**Answer: b) final**  
**Explanation:** Final methods cannot be overridden by subclasses.

---

## 8. What will happen when this code is compiled and run?
```java
interface A {
    default void method() { System.out.println("A"); }
}
interface B {
    default void method() { System.out.println("B"); }
}
class C implements A, B {
    // Empty class body
}
```
a) Compiles and runs successfully  
b) Compilation error due to ambiguous method  
c) Runtime error  
d) Prints both A and B  

**Answer: b) Compilation error due to ambiguous method**  
**Explanation:** When implementing multiple interfaces with same default method signature, the class must override the method to resolve ambiguity.

---

## 9. Which of the following demonstrates tight coupling?
a) Using interfaces  
b) Using composition  
c) Direct instantiation of concrete classes  
d) Using dependency injection  

**Answer: c) Direct instantiation of concrete classes**  
**Explanation:** Tight coupling occurs when classes are directly dependent on concrete implementations rather than abstractions.

---

## 10. What is the output?
```java
class Test {
    static int x = 10;
    static {
        x = 20;
        System.out.print(x + " ");
    }
    public static void main(String[] args) {
        System.out.print(x);
    }
}
```
a) 10 20  
b) 20 10  
c) 20 20  
d) 10 10  

**Answer: c) 20 20**  
**Explanation:** Static block executes first, setting x to 20, then main method prints the current value of x.

---

## 11. Which principle suggests "Program to interfaces, not implementations"?
a) Single Responsibility Principle  
b) Open/Closed Principle  
c) Dependency Inversion Principle  
d) Interface Segregation Principle  

**Answer: c) Dependency Inversion Principle**  
**Explanation:** DIP states that high-level modules should not depend on low-level modules; both should depend on abstractions.

---

## 12. What is the difference between method overloading and method overriding?
a) Overloading is compile-time, overriding is runtime  
b) Overloading is runtime, overriding is compile-time  
c) Both are compile-time  
d) Both are runtime  

**Answer: a) Overloading is compile-time, overriding is runtime**  
**Explanation:** Method overloading is resolved at compile time (static polymorphism), while method overriding is resolved at runtime (dynamic polymorphism).

---

## 13. What will be the output?
```java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}
class Dog extends Animal {
    void sound() { System.out.println("Bark"); }
    void sound(String type) { System.out.println("Loud bark"); }
}
public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        Dog d = new Dog();
        a.sound();
        d.sound("loud");
    }
}
```
a) Animal sound, Loud bark  
b) Bark, Loud bark  
c) Compilation error  
d) Animal sound, Bark  

**Answer: b) Bark, Loud bark**  
**Explanation:** First call uses overriding (runtime polymorphism), second call uses overloading (compile-time polymorphism).

---

## 14. Which of the following is true about interfaces in Java 8+?
a) Can have only abstract methods  
b) Can have default and static methods  
c) Cannot have variables  
d) Cannot extend other interfaces  

**Answer: b) Can have default and static methods**  
**Explanation:** Java 8 introduced default and static methods in interfaces, along with traditional abstract methods.

---

## 15. What is the output?
```java
class Outer {
    static int x = 10;
    static class Inner {
        static int x = 20;
        static void display() {
            System.out.println(x);
        }
    }
}
public class Test {
    public static void main(String[] args) {
        Outer.Inner.display();
    }
}
```
a) 10  
b) 20  
c) Compilation error  
d) 0  

**Answer: b) 20**  
**Explanation:** The inner class's x variable shadows the outer class's x variable within the inner class scope.

---

## 16. Which design pattern ensures only one instance of a class exists?
a) Factory  
b) Singleton  
c) Builder  
d) Observer  

**Answer: b) Singleton**  
**Explanation:** Singleton pattern ensures a class has only one instance and provides global access to it.

---

## 17. What will be the output?
```java
class Parent {
    static void method() { System.out.println("Parent static"); }
}
class Child extends Parent {
    static void method() { System.out.println("Child static"); }
}
public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.method();
    }
}
```
a) Parent static  
b) Child static  
c) Compilation error  
d) Runtime error  

**Answer: a) Parent static**  
**Explanation:** Static methods are resolved at compile time based on the reference type, not the object type. This is method hiding, not overriding.

---

## 18. Which of the following violates encapsulation?
a) Making fields private  
b) Providing public getter/setter methods  
c) Making fields public  
d) Using constructors to initialize fields  

**Answer: c) Making fields public**  
**Explanation:** Public fields directly expose internal state, violating encapsulation principles.

---

## 19. What is the output?
```java
interface I1 {
    default void method() { System.out.print("I1 "); }
}
interface I2 extends I1 {
    default void method() { System.out.print("I2 "); }
}
class Test implements I2 {
    public static void main(String[] args) {
        new Test().method();
    }
}
```
a) I1  
b) I2  
c) I1 I2  
d) Compilation error  

**Answer: b) I2**  
**Explanation:** When interfaces extend other interfaces, the subinterface's default method overrides the parent's default method.

---

## 20. Which keyword is used to call parent class constructor explicitly?
a) this  
b) super  
c) parent  
d) base  

**Answer: b) super**  
**Explanation:** super() is used to call the parent class constructor explicitly.

---

## 21. What will be the output?
```java
class Test {
    int x = 10;
    Test() {
        this(20);
        System.out.print(x + " ");
    }
    Test(int x) {
        this.x = x;
        System.out.print(x + " ");
    }
    public static void main(String[] args) {
        new Test();
    }
}
```
a) 10 20  
b) 20 20  
c) 20 10  
d) Compilation error  

**Answer: b) 20 20**  
**Explanation:** Constructor chaining: Test() calls Test(20), which sets x=20, then prints 20, then control returns to Test() which prints current x value (20).

---

## 22. Which of the following is true about composition vs inheritance?
a) Composition is "is-a" relationship  
b) Inheritance is "has-a" relationship  
c) Composition provides better flexibility  
d) Inheritance is always preferred  

**Answer: c) Composition provides better flexibility**  
**Explanation:** Composition allows changing behavior at runtime and avoids tight coupling issues of inheritance.

---

## 23. What is the output?
```java
abstract class Animal {
    abstract void sound();
    void sleep() { System.out.println("Sleeping"); }
}
class Dog extends Animal {
    void sound() { System.out.println("Bark"); }
}
public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound();
        a.sleep();
    }
}
```
a) Compilation error  
b) Bark, Sleeping  
c) Runtime error  
d) Sleeping, Bark  

**Answer: b) Bark, Sleeping**  
**Explanation:** Abstract classes can be referenced, and both abstract and concrete methods can be called on the subclass object.

---

## 24. Which access modifier provides the most restrictive access?
a) private  
b) default  
c) protected  
d) public  

**Answer: a) private**  
**Explanation:** Private members are accessible only within the same class, making it the most restrictive access level.

---

## 25. What will be the output?
```java
class Parent {
    void display() throws Exception {
        System.out.println("Parent");
    }
}
class Child extends Parent {
    void display() throws RuntimeException {
        System.out.println("Child");
    }
}
public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.display(); // Line X
    }
}
```
a) Parent  
b) Child  
c) Compilation error at Line X  
d) Runtime error  

**Answer: c) Compilation error at Line X**  
**Explanation:** The reference type (Parent) declares checked exception, so the call must be in try-catch or method must declare throws Exception.

---

## 26. Which principle states "Classes should be open for extension but closed for modification"?
a) Single Responsibility Principle  
b) Open/Closed Principle  
c) Liskov Substitution Principle  
d) Dependency Inversion Principle  

**Answer: b) Open/Closed Principle**  
**Explanation:** OCP states that software entities should be open for extension but closed for modification.

---

## 27. What is the output?
```java
class Test {
    Test() {
        System.out.print("A");
    }
    Test(int x) {
        this();
        System.out.print("B");
    }
    {
        System.out.print("C");
    }
    static {
        System.out.print("D");
    }
    public static void main(String[] args) {
        new Test(10);
    }
}
```
a) DCAB  
b) DACB  
c) DCBA  
d) CABD  

**Answer: a) DCAB**  
**Explanation:** Static block (D), then instance block (C), then Test() via this() (A), then Test(int) continues (B).

---

## 28. Which of the following allows multiple inheritance in Java?
a) Classes  
b) Abstract classes  
c) Interfaces  
d) None of the above  

**Answer: c) Interfaces**  
**Explanation:** A class can implement multiple interfaces, achieving multiple inheritance of type.

---

## 29. What will be the output?
```java
class Parent {
    int x = 10;
}
class Child extends Parent {
    int x = 20;
    void display() {
        System.out.println(x + " " + super.x);
    }
}
public class Test {
    public static void main(String[] args) {
        new Child().display();
    }
}
```
a) 10 10  
b) 20 20  
c) 20 10  
d) 10 20  

**Answer: c) 20 10**  
**Explanation:** x refers to child's field (20), super.x refers to parent's field (10). This is field hiding.

---

## 30. Which modifier prevents a class from being subclassed?
a) static  
b) final  
c) abstract  
d) private  

**Answer: b) final**  
**Explanation:** Final classes cannot be extended (e.g., String, Integer classes are final).

---

## 31. What is the output?
```java
interface A {
    int x = 10; // Line 1
}
class B implements A {
    public static void main(String[] args) {
        x = 20; // Line 2
        System.out.println(x);
    }
}
```
a) 20  
b) 10  
c) Compilation error at Line 1  
d) Compilation error at Line 2  

**Answer: d) Compilation error at Line 2**  
**Explanation:** Interface variables are implicitly public static final, so they cannot be reassigned.

---

## 32. Which concept allows treating objects of different types uniformly?
a) Encapsulation  
b) Inheritance  
c) Polymorphism  
d) Abstraction  

**Answer: c) Polymorphism**  
**Explanation:** Polymorphism allows objects of different types to be treated uniformly through a common interface or base class.

---

## 33. What will be the output?
```java
class Outer {
    int x = 10;
    class Inner {
        int x = 20;
        void display() {
            int x = 30;
            System.out.println(x + " " + this.x + " " + Outer.this.x);
        }
    }
}
public class Test {
    public static void main(String[] args) {
        new Outer().new Inner().display();
    }
}
```
a) 10 20 30  
b) 30 20 10  
c) 30 30 30  
d) 20 10 30  

**Answer: b) 30 20 10**  
**Explanation:** Local variable x (30), inner class field this.x (20), outer class field Outer.this.x (10).

---

## 34. Which of the following is NOT a valid way to achieve polymorphism?
a) Method overriding  
b) Method overloading  
c) Interface implementation  
d) Variable hiding  

**Answer: d) Variable hiding**  
**Explanation:** Variable hiding is not polymorphism. Polymorphism is achieved through method overriding, overloading, and interface implementation.

---

## 35. What is the output?
```java
class Test {
    static int count = 0;
    Test() {
        count++;
        System.out.print(count + " ");
    }
    public static void main(String[] args) {
        new Test();
        new Test();
        new Test();
    }
}
```
a) 1 1 1  
b) 3 3 3  
c) 1 2 3  
d) 0 1 2  

**Answer: c) 1 2 3**  
**Explanation:** Static variable count is shared among all instances and incremented each time a new object is created.

---

## 36. Which relationship is represented by composition?
a) is-a  
b) has-a  
c) uses-a  
d) implements-a  

**Answer: b) has-a**  
**Explanation:** Composition represents a "has-a" relationship where one object contains another object as part of its state.

---

## 37. What will be the output?
```java
class Parent {
    static void method() { System.out.print("Parent "); }
    void instance() { method(); }
}
class Child extends Parent {
    static void method() { System.out.print("Child "); }
}
public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.instance();
        p.method();
    }
}
```
a) Parent Parent  
b) Child Child  
c) Child Parent  
d) Parent Child  

**Answer: c) Child Parent**  
**Explanation:** instance() calls method() dynamically (Child), but p.method() calls statically based on reference type (Parent).

---

## 38. Which principle suggests that objects should be replaceable with instances of their subtypes?
a) Open/Closed Principle  
b) Liskov Substitution Principle  
c) Interface Segregation Principle  
d) Dependency Inversion Principle  

**Answer: b) Liskov Substitution Principle**  
**Explanation:** LSP states that objects of a superclass should be replaceable with objects of a subclass without affecting functionality.

---

## 39. What is the output?
```java
class Test {
    public Test() {
        System.out.print("Default ");
    }
    public Test(String s) {
        System.out.print("String ");
    }
    public static void main(String[] args) {
        new Test();
        new Test("Hello");
        new Test(null);
    }
}
```
a) Default String String  
b) Default String Default  
c) Compilation error  
d) Default String Compilation error  

**Answer: c) Compilation error**  
**Explanation:** new Test(null) is ambiguous because null can match both String and any other reference type parameter if there were another constructor.

---

## 40. Which of the following breaks encapsulation?
a) Using private fields with public getters  
b) Returning mutable objects directly from getters  
c) Using constructor injection  
d) Validating input in setters  

**Answer: b) Returning mutable objects directly from getters**  
**Explanation:** Returning mutable objects allows external modification of internal state, breaking encapsulation.

---

## 41. What will be the output?
```java
abstract class Animal {
    public Animal() { System.out.print("Animal "); }
}
class Dog extends Animal {
    public Dog() { System.out.print("Dog "); }
}
public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
    }
}
```
a) Animal Dog  
b) Dog Animal  
c) Dog  
d) Animal  

**Answer: a) Animal Dog**  
**Explanation:** Parent constructor (Animal) is called first, then child constructor (Dog).

---

## 42. Which keyword is used to refer to the current object?
a) self  
b) current  
c) this  
d) me  

**Answer: c) this**  
**Explanation:** 'this' keyword refers to the current object instance in Java.

---

## 43. What is the output?
```java
class Test {
    int x;
    Test(int x) {
        x = x; // Line 1
    }
    public static void main(String[] args) {
        Test t = new Test(10);
        System.out.println(t.x);
    }
}
```
a) 10  
b) 0  
c) Compilation error  
d) Runtime error  

**Answer: b) 0**  
**Explanation:** Line 1 assigns parameter x to itself, not to instance variable. Instance variable x remains 0 (default value).

---

## 44. Which of the following is true about method overriding?
a) Private methods can be overridden  
b) Static methods can be overridden  
c) Final methods can be overridden  
d) Protected methods can be overridden  

**Answer: d) Protected methods can be overridden**  
**Explanation:** Protected methods can be overridden. Private, static, and final methods cannot be overridden.

---

## 45. What will be the output?
```java
interface I {
    void method();
}
class A implements I {
    public void method() { System.out.print("A "); }
}
class B extends A {
    public void method() { System.out.print("B "); }
}
public class Test {
    public static void main(String[] args) {
        I i = new B();
        A a = new B();
        i.method();
        a.method();
    }
}
```
a) A A  
b) B B  
c) A B  
d) B A  

**Answer: b) B B**  
**Explanation:** Both calls use runtime polymorphism, calling B's overridden method regardless of reference type.

---

## 46. Which design pattern is used to create objects without specifying exact class?
a) Singleton  
b) Factory  
c) Observer  
d) Strategy  

**Answer: b) Factory**  
**Explanation:** Factory pattern creates objects without exposing creation logic and refers to newly created object using common interface.

---

## 47. What is the output?
```java
class Outer {
    static class Nested {
        void display() { System.out.print("Nested "); }
    }
    class Inner {
        void display() { System.out.print("Inner "); }
    }
}
public class Test {
    public static void main(String[] args) {
        new Outer.Nested().display();
        new Outer().new Inner().display();
    }
}
```
a) Nested Inner  
b) Inner Nested  
c) Compilation error  
d) Inner Inner  

**Answer: a) Nested Inner**  
**Explanation:** Static nested class can be instantiated without outer instance, but inner class needs outer instance.

---

## 48. Which principle suggests that a class should have only one reason to change?
a) Single Responsibility Principle  
b) Open/Closed Principle  
c) Liskov Substitution Principle  
d) Interface Segregation Principle  

**Answer: a) Single Responsibility Principle**  
**Explanation:** SRP states that a class should have only one reason to change, meaning it should have only one job or responsibility.

---

## 49. What will be the output?
```java
class Test {
    void method(Object o) { System.out.print("Object "); }
    void method(String s) { System.out.print("String "); }
    public static void main(String[] args) {
        Test t = new Test();
        t.method("Hello");
        t.method((Object)"Hello");
        t.method(null);
    }
}
```
a) String Object String  
b) String Object Object  
c) Object String String  
d) String String String  

**Answer: a) String Object String**  
**Explanation:** First call matches String (most specific), second call explicitly casts to Object, third call matches String (more specific than Object for null).

---

## 50. Which of the following best describes abstraction?
a) Hiding implementation details  
b) Creating multiple objects  
c) Inheriting from parent class  
d) Accessing private members  

**Answer: a) Hiding implementation details**  
**Explanation:** Abstraction is the concept of hiding complex implementation details while exposing only essential features of an object.

---

## What is the output of this code?
```java
class Parent {
    static String name = "Parent";
    static {
        name = getName();
    }
    static String getName() {
        return "ParentStatic";
    }
}
class Child extends Parent {
    static String name = "Child";
    static {
        name = getName();
    }
    static String getName() {
        return "ChildStatic";
    }
}
public class Test {
    public static void main(String[] args) {
        System.out.println(Parent.name + " " + Child.name);
    }
}
```
a) Parent Child  
b) ParentStatic ChildStatic  
c) ChildStatic ChildStatic  
d) ParentStatic ParentStatic  

**Answer: c) ChildStatic ChildStatic**  
**Explanation:** During Child loading, Parent's static block executes, but it calls getName(), which is resolved dynamically to Child.getName(). Hence both become "ChildStatic". This tests class loading + static initialization + method hiding.

---

## What is the output of this code?
```java
class A {
    int value = 10;
    A() {
        System.out.println("A constructor, value = " + value);
        print();
    }
    void print() {
        System.out.println("A print, value = " + value);
    }
}
class B extends A {
    int value = 20;
    B() {
        System.out.println("B constructor, value = " + value);
    }
    void print() {
        System.out.println("B print, value = " + value);
    }
}
public class Test {
    public static void main(String[] args) {
        new B();
    }
}
```
a) A constructor, value = 10  
   A print, value = 10  
   B constructor, value = 20  

b) A constructor, value = 10  
   B print, value = 0  
   B constructor, value = 20  

c) A constructor, value = 10  
   B print, value = 20  
   B constructor, value = 20  

d) Compilation error  

**Answer: b)**  
**Explanation:** During A's constructor, B.print() is invoked (dynamic dispatch). At this point, B.value is not initialized yet, so it prints 0. Later, B's constructor assigns 20. Classic constructor chaining + polymorphism + initialization order trap.

---

## What is the output of this code?
```java
class Base {
    String msg = "Base";
    Base() {
        show();
    }
    void show() {
        System.out.println(msg);
    }
}
class Derived extends Base {
    String msg = "Derived";
    Derived() {
        show();
    }
    void show() {
        System.out.println(msg);
    }
}
public class Test {
    public static void main(String[] args) {
        new Derived();
    }
}
```
a) Base  
   Derived  

b) null  
   Derived  

c) Derived  
   Derived  

d) Base  
   Base  

**Answer: b) null, Derived**  
**Explanation:** When Base constructor calls show(), it invokes Derived.show(). But Derived.msg is not yet initialized (defaults to null). Later, after initialization, second call prints "Derived". Tests field initialization order vs. polymorphism.

---

## What is the output of this code?
```java
class A {
    static void display() { System.out.println("A"); }
}
class B extends A {
    static void display() { System.out.println("B"); }
}
public class Test {
    public static void main(String[] args) {
        A obj = new B();
        obj.display();
    }
}
```
a) A  
b) B  
c) Compilation error  
d) Runtime error  

**Answer: a) A**  
**Explanation:** static methods are hidden, not overridden. Resolution happens at compile-time using reference type (A). A common method hiding vs. overriding interview trick.

---

## What is the output of this code?
```java
class Outer {
    private static String secret = "Hidden";
    static class Inner {
        void reveal() {
            System.out.println(secret);
        }
    }
}
public class Test {
    public static void main(String[] args) {
        new Outer.Inner().reveal();
    }
}
```
a) Compilation error  
b) null  
c) Hidden  
d) Runtime error  
**Answer: c) Hidden**  
**Explanation:** A static nested class can access private static members of the outer class. This tests nested class access rules.

---

## What is the output of this code?
```java
class A {
    final void foo() { System.out.println("A.foo"); }
}
class B extends A {
    void foo(int x) { System.out.println("B.foo"); }
}
public class Test {
    public static void main(String[] args) {
        new B().foo();
    }
}
```
a) A.foo  
b) B.foo  
c) Compilation error  
d) Runtime error  

**Answer: a) A.foo**  
**Explanation:** foo() in A is final and cannot be overridden. B only overloads it with foo(int). Hence call resolves to A.foo(). Tests overloading vs overriding with final methods.

---

## What is the output of this code?
```java
interface I1 {
    default void show() { System.out.println("I1"); }
}
interface I2 {
    default void show() { System.out.println("I2"); }
}
class Test implements I1, I2 {
    public void show() {
        I1.super.show();
    }
    public static void main(String[] args) {
        new Test().show();
    }
}
```
a) I1  
b) I2  
c) Compilation error  
d) Both I1 and I2  

**Answer: a) I1**  
**Explanation:** Multiple inheritance conflict is resolved explicitly. Here, I1.super.show() is chosen. This is default methods diamond problem in Java 8.

---

## What is the output of this code?
```java
class A {
    int x = 10;
}
class B extends A {
    int x = 20;
}
public class Test {
    public static void main(String[] args) {
        A obj = new B();
        System.out.println(obj.x);
    }
}
```
a) 10  
b) 20  
c) Compilation error  
d) Runtime error  

**Answer: a) 10**  
**Explanation:** Fields are not polymorphic. Resolution happens at compile-time by reference type (A). Tests field hiding vs method overriding.

---

## What is the output of this code?
```java
class A {
    static { System.out.println("A static"); }
    { System.out.println("A instance"); }
}
class B extends A {
    static { System.out.println("B static"); }
    { System.out.println("B instance"); }
}
public class Test {
    public static void main(String[] args) {
        new B();
        new B();
    }
}
```
a) A static  
   B static  
   A instance  
   B instance  
   A instance  
   B instance  

b) A static  
   A instance  
   B static  
   B instance  
   A instance  
   B instance  

c) A static  
   B static  
   A instance  
   B instance  

d) Compilation error  

**Answer: a)**  
**Explanation:** Static blocks run once per class load, instance blocks run every time an object is created. Classic class loading vs instance initialization.

---

## What is the output of this code?
```java
class Test {
    public static void main(String[] args) {
        String s1 = new String("Java");
        String s2 = "Java";
        String s3 = s1.intern();
        System.out.println(s1 == s2);
        System.out.println(s2 == s3);
    }
}
```
a) true  
   true  

b) false  
   true  

c) true  
   false  

d) false  
   false  

**Answer: b) false, true**  
**Explanation:** s1 points to heap object, s2 points to string pool. After intern(), s3 points to pool, same as s2. This checks string interning mechanism.

---

## 1. What is the output of this code?
```java
class Parent {
    static String name = "Parent";
    static {
        name = getName();
    }
    static String getName() {
        return "ParentStatic";
    }
}
class Child extends Parent {
    static String name = "Child";
    static {
        name = getName();
    }
    static String getName() {
        return "ChildStatic";
    }
}
public class Test {
    public static void main(String[] args) {
        System.out.println(Parent.name + " " + Child.name);
    }
}
```
a) Parent Child  
b) ParentStatic ChildStatic  
c) ChildStatic ChildStatic  
d) ParentStatic ParentStatic  

**Answer: c) ChildStatic ChildStatic**  
**Explanation:** When Child class is loaded, Parent's static block calls getName() which is overridden by Child, so both get "ChildStatic". This is a classic example of calling overridable methods during static initialization.

---

## 2. What will be the output?
```java
class Test {
    private void method() {
        System.out.println("Private method");
    }
    
    public static void main(String[] args) {
        Test t1 = new Test();
        Test t2 = new Test() {
            public void method() {
                System.out.println("Anonymous method");
            }
        };
        
        t1.method();
        t2.method();
    }
}
```
a) Private method, Anonymous method  
b) Private method, Private method  
c) Compilation error  
d) Anonymous method, Anonymous method  

**Answer: c) Compilation error**  
**Explanation:** Anonymous classes cannot override private methods as they're not inherited. The anonymous class creates a new method, but the call t2.method() tries to access the private method from outside the class.

---

## 3. What is the output?
```java
interface A {
    default void test() {
        System.out.print("A");
    }
}
interface B extends A {
    default void test() {
        System.out.print("B");
        A.super.test();
    }
}
interface C extends A {
    default void test() {
        System.out.print("C");
        A.super.test();
    }
}
class D implements B, C {
    public void test() {
        B.super.test();
        C.super.test();
    }
}
public class Test {
    public static void main(String[] args) {
        new D().test();
    }
}
```
a) BACA  
b) BCAA  
c) Compilation error  
d) ABAC  

**Answer: a) BACA**  
**Explanation:** D.test() calls B.super.test() (prints "B", then "A"), then C.super.test() (prints "C", then "A").

---

## 4. What will happen when this code runs?
```java
class Parent {
    Parent() throws Exception {
        throw new Exception("Parent exception");
    }
}
class Child extends Parent {
    Child() {
        super();
    }
}
public class Test {
    public static void main(String[] args) {
        try {
            new Child();
        } catch (Exception e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```
a) Prints: Caught: Parent exception  
b) Compilation error in Child constructor  
c) Runtime exception  
d) No output  

**Answer: b) Compilation error in Child constructor**  
**Explanation:** Child constructor must handle or declare the Exception thrown by Parent constructor, but it doesn't have throws clause or try-catch.

---

## 5. What is the output?
```java
class Outer {
    int x = 10;
    
    class Inner {
        int x = 20;
        
        class InnerInner {
            int x = 30;
            
            void display() {
                System.out.println(x + " " + Inner.this.x + " " + Outer.this.x);
            }
        }
    }
    
    public static void main(String[] args) {
        Outer.Inner.InnerInner obj = new Outer().new Inner().new InnerInner();
        obj.display();
    }
}
```
a) 10 20 30  
b) 30 20 10  
c) 30 30 30  
d) Compilation error  

**Answer: b) 30 20 10**  
**Explanation:** InnerInner's x (30), Inner's x via Inner.this.x (20), Outer's x via Outer.this.x (10).

---

## 6. What will be the output?
```java
class Test {
    static {
        System.out.print("1");
    }
    
    {
        System.out.print("2");
    }
    
    Test() {
        System.out.print("3");
    }
    
    Test(int x) {
        this();
        System.out.print("4");
    }
    
    public static void main(String[] args) {
        new Test(5);
        new Test();
    }
}
```
a) 123423  
b) 134123  
c) 123234  
d) 132342  

**Answer: c) 123234**  
**Explanation:** Static block (1), then first object: instance block (2), Test() via this() (3), Test(int) continues (4), then second object: instance block (2), Test() constructor (3).

---

## 7. What is the output?
```java
abstract class Animal {
    abstract void sound();
    
    Animal() {
        sound(); // Line X
    }
}

class Dog extends Animal {
    String breed = "Labrador";
    
    void sound() {
        System.out.println("Bark: " + breed);
    }
}

public class Test {
    public static void main(String[] args) {
        new Dog();
    }
}
```
a) Bark: Labrador  
b) Bark: null  
c) Compilation error at Line X  
d) Runtime exception  

**Answer: b) Bark: null**  
**Explanation:** During object construction, parent constructor runs first. At this time, Dog's instance variables haven't been initialized yet, so breed is null.

---

## 8. What will be the output?
```java
class Parent {
    void method() throws IOException {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    void method() throws FileNotFoundException {
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        try {
            p.method();
        } catch (IOException e) {
            System.out.println("IOException caught");
        }
    }
}
```
a) Child  
b) Parent  
c) IOException caught  
d) Compilation error  

**Answer: a) Child**  
**Explanation:** Method overriding with exception handling. Child's method throws a subtype of IOException (FileNotFoundException), which is valid. Runtime polymorphism calls Child's method.

---

## 9. What is the output?
```java
class Test {
    static Test instance = new Test();
    static int x = 10;
    
    Test() {
        System.out.print(x + " ");
    }
    
    public static void main(String[] args) {
        System.out.print(Test.x + " ");
        new Test();
    }
}
```
a) 0 10 10  
b) 10 10 10  
c) 0 0 10  
d) 10 0 10  

**Answer: a) 0 10 10**  
**Explanation:** Static variables are initialized in order. When `instance = new Test()` executes, x is still 0 (not yet initialized), so constructor prints 0. Then x becomes 10, main prints 10, new Test() prints 10.

---

## 10. What will happen?
```java
final class FinalClass {
    void method() {
        System.out.println("Final class method");
    }
}

class Test {
    public static void main(String[] args) {
        FinalClass obj = new FinalClass() {
            void method() {
                System.out.println("Anonymous method");
            }
        };
        obj.method();
    }
}
```
a) Final class method  
b) Anonymous method  
c) Compilation error  
d) Runtime error  

**Answer: c) Compilation error**  
**Explanation:** Final classes cannot be extended, not even by anonymous classes.

---

## 11. What is the output?
```java
interface I {
    int x = 10;
}

class A implements I {
    int x = 20;
}

class B extends A {
    void display() {
        System.out.println(x + " " + super.x + " " + I.x);
    }
}

public class Test {
    public static void main(String[] args) {
        new B().display();
    }
}
```
a) 20 20 10  
b) 10 20 10  
c) 20 10 10  
d) Compilation error  

**Answer: a) 20 20 10**  
**Explanation:** x refers to A's field (20), super.x also refers to A's field (20), I.x is interface constant (10).

---

## 12. What will be the output?
```java
class Parent {
    String name;
    Parent(String name) {
        this.name = name;
    }
    
    void display() {
        System.out.print(name + " ");
    }
}

class Child extends Parent {
    String name;
    Child(String parentName, String childName) {
        super(parentName);
        this.name = childName;
    }
    
    void display() {
        super.display();
        System.out.print(this.name + " ");
    }
}

public class Test {
    public static void main(String[] args) {
        Child c = new Child("Dad", "Son");
        c.display();
    }
}
```
a) Dad Son  
b) Son Dad  
c) Dad Dad  
d) Son Son  

**Answer: a) Dad Son**  
**Explanation:** super.display() prints parent's name field ("Dad"), then prints child's name field ("Son").

---

## 13. What is the output?
```java
class Test {
    void method(int... args) {
        System.out.print("Varargs ");
    }
    
    void method(int[] args) {
        System.out.print("Array ");
    }
    
    public static void main(String[] args) {
        Test t = new Test();
        t.method(new int[]{1, 2, 3});
        t.method(1, 2, 3);
    }
}
```
a) Array Varargs  
b) Varargs Array  
c) Compilation error  
d) Array Array  

**Answer: c) Compilation error**  
**Explanation:** Ambiguous method call. int[] and int... are equivalent at runtime, so the compiler cannot distinguish between them.

---

## 14. What will be the output?
```java
class Outer {
    private int x = 10;
    
    class Inner {
        private int x = 20;
        
        void test() {
            System.out.println("Inner x: " + this.x);
            System.out.println("Outer x: " + Outer.this.x);
        }
    }
    
    void createInner() {
        Inner inner = new Inner() {
            private int x = 30;
            void test() {
                System.out.println("Anonymous x: " + this.x);
                super.test();
            }
        };
        inner.test();
    }
    
    public static void main(String[] args) {
        new Outer().createInner();
    }
}
```
a) Anonymous x: 30, Inner x: 20, Outer x: 10  
b) Inner x: 20, Outer x: 10  
c) Anonymous x: 30, Inner x: 30, Outer x: 10  
d) Compilation error  

**Answer: a) Anonymous x: 30, Inner x: 20, Outer x: 10**  
**Explanation:** Anonymous class overrides test(), prints its own x (30), then calls super.test() which prints Inner's x (20) and Outer's x (10).

---

## 15. What is the output?
```java
class A {
    static void method() { System.out.print("A"); }
}

class B extends A {
    static void method() { System.out.print("B"); }
    
    static {
        method(); // Line 1
    }
}

class C extends B {
    static void method() { System.out.print("C"); }
    
    static {
        method(); // Line 2
    }
}

public class Test {
    public static void main(String[] args) {
        C c = new C();
    }
}
```
a) ABC  
b) CCC  
c) BCC  
d) BBC  

**Answer: d) BBC**  
**Explanation:** During class loading: B's static block executes and calls B.method() (prints B), then C's static block executes and calls C.method() (prints C), then C c = new C() triggers C.method() again (prints C).

Actually, correction: It should be **BC** - B's static block prints B, C's static block prints C. Object creation doesn't call static methods.

---

## 16. What will happen?
```java
interface Functional {
    void test();
    
    default void method() {
        test();
    }
}

public class Test {
    public static void main(String[] args) {
        Functional f = () -> System.out.println("Lambda");
        f.method();
    }
}
```
a) Lambda  
b) Compilation error  
c) Runtime error  
d) Nothing prints  

**Answer: a) Lambda**  
**Explanation:** Lambda expression implements the functional interface. The default method calls the lambda-implemented test() method.

---

## 17. What is the output?
```java
class Generic<T> {
    T data;
    
    Generic(T data) {
        this.data = data;
    }
    
    void method(T param) {
        System.out.println("Generic method: " + param);
    }
    
    void method(String param) {
        System.out.println("String method: " + param);
    }
}

public class Test {
    public static void main(String[] args) {
        Generic<String> g = new Generic<>("Hello");
        g.method("World");
    }
}
```
a) Generic method: World  
b) String method: World  
c) Compilation error  
d) Ambiguous method call  

**Answer: b) String method: World**  
**Explanation:** When T is String, method(T param) becomes method(String param), creating two identical methods. The explicitly declared method(String param) takes precedence due to method resolution rules.

---

## 18. What will be the output?
```java
abstract class Shape {
    abstract void draw();
    
    void display() {
        System.out.print("Shape ");
        draw();
    }
}

class Circle extends Shape {
    void draw() {
        System.out.print("Circle ");
    }
    
    void display() {
        System.out.print("Displaying ");
        super.display();
    }
}

public class Test {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.display();
    }
}
```
a) Shape Circle  
b) Displaying Shape Circle  
c) Circle Shape  
d) Displaying Circle Shape  

**Answer: b) Displaying Shape Circle**  
**Explanation:** Runtime polymorphism calls Circle's display() which prints "Displaying", then calls super.display() which prints "Shape", then calls draw() which is overridden to print "Circle".

---

## 19. What is the output?
```java
class Test {
    String str = "Instance";
    
    Test() {
        System.out.print(str + " ");
        str = "Constructor";
    }
    
    {
        System.out.print(str + " ");
        str = "Block";
    }
    
    public static void main(String[] args) {
        new Test();
        System.out.print(Test.class.getSimpleName());
    }
}
```
a) Instance Block Constructor Test  
b) null Block Constructor Test  
c) Instance Constructor Test  
d) null Instance Constructor Test  

**Answer: b) null Block Constructor Test**  
**Explanation:** Instance variable initialization, then instance block (prints "null" because str isn't initialized yet, then sets to "Block"), then constructor (prints "Block", then sets to "Constructor"), then main prints "Test".

Wait, let me reconsider: Instance variables are initialized before instance blocks. So it should be **Instance Block Constructor Test**.

Correction: **Answer: a) Instance Block Constructor Test**

---

## 20. What will happen?
```java
class Parent {
    static class Nested {
        void method() {
            System.out.println("Parent.Nested");
        }
    }
}

class Child extends Parent {
    static class Nested {
        void method() {
            System.out.println("Child.Nested");
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        Parent.Nested pn = new Parent.Nested();
        Child.Nested cn = new Child.Nested();
        pn.method();
        cn.method();
    }
}
```
a) Parent.Nested, Child.Nested  
b) Child.Nested, Child.Nested  
c) Parent.Nested, Parent.Nested  
d) Compilation error  

**Answer: a) Parent.Nested, Child.Nested**  
**Explanation:** Static nested classes don't participate in inheritance polymorphism. Each class has its own static nested class.

---

## 21. What is the output?
```java
enum Color {
    RED("Red Color") {
        public void display() {
            System.out.print("RED ");
        }
    },
    BLUE("Blue Color");
    
    private String description;
    
    Color(String description) {
        this.description = description;
    }
    
    public void display() {
        System.out.print(description + " ");
    }
}

public class Test {
    public static void main(String[] args) {
        Color.RED.display();
        Color.BLUE.display();
    }
}
```
a) Red Color Blue Color  
b) RED Blue Color  
c) Red Color BLUE  
d) RED BLUE  

**Answer: b) RED Blue Color**  
**Explanation:** RED has its own implementation of display() method (prints "RED"), while BLUE uses the default implementation (prints description "Blue Color").

---

## 22. What will be the output?
```java
class Test {
    int x = getValue();
    
    {
        System.out.print("Block: " + x + " ");
    }
    
    Test() {
        System.out.print("Constructor: " + x + " ");
    }
    
    int getValue() {
        System.out.print("getValue ");
        return 10;
    }
    
    public static void main(String[] args) {
        new Test();
    }
}
```
a) getValue Block: 10 Constructor: 10  
b) Block: 0 getValue Constructor: 10  
c) getValue Block: 0 Constructor: 10  
d) getValue getValue Block: 10 Constructor: 10  

**Answer: a) getValue Block: 10 Constructor: 10**  
**Explanation:** Instance variable initialization calls getValue() first, then instance block executes with x=10, then constructor executes with x=10.

---

## 23. What is the output?
```java
interface A {
    default void method() {
        System.out.print("A ");
    }
}

interface B {
    default void method() {
        System.out.print("B ");
    }
}

class C implements A, B {
    public void method() {
        A.super.method();
        B.super.method();
    }
}

class D extends C {
    public void method() {
        super.method();
        System.out.print("D ");
    }
}

public class Test {
    public static void main(String[] args) {
        new D().method();
    }
}
```
a) A B D  
b) D A B  
c) A D B  
d) B A D  

**Answer: a) A B D**  
**Explanation:** D's method() calls super.method() (which is C's method that prints "A B"), then prints "D".

---

## 24. What will happen when this code runs?
```java
class Parent {
    void method(Object obj) {
        System.out.print("Parent-Object ");
    }
}

class Child extends Parent {
    void method(String str) {
        System.out.print("Child-String ");
    }
    
    void method(Object obj) {
        System.out.print("Child-Object ");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.method("Hello");
        p.method((Object)"Hello");
    }
}
```
a) Child-String Child-Object  
b) Parent-Object Child-Object  
c) Child-Object Child-Object  
d) Parent-Object Parent-Object  

**Answer: c) Child-Object Child-Object**  
**Explanation:** Reference type is Parent, so only Parent's methods are accessible. Both calls resolve to method(Object), which is overridden in Child.

---

## 25. What is the output?
```java
class Test {
    static String str = "Static";
    String str2 = "Instance";
    
    static {
        System.out.print(str + " ");
        str = getStaticValue();
    }
    
    {
        System.out.print(str2 + " ");
        str2 = getInstanceValue();
    }
    
    Test() {
        System.out.print(str + " " + str2 + " ");
    }
    
    static String getStaticValue() {
        System.out.print("StaticMethod ");
        return "StaticValue";
    }
    
    String getInstanceValue() {
        System.out.print("InstanceMethod ");
        return "InstanceValue";
    }
    
    public static void main(String[] args) {
        new Test();
    }
}
```
a) Static StaticMethod Instance InstanceMethod StaticValue InstanceValue  
b) Static Instance StaticMethod InstanceMethod StaticValue InstanceValue  
c) StaticMethod Static Instance InstanceMethod StaticValue InstanceValue  
d) Static StaticMethod StaticValue Instance InstanceMethod InstanceValue  

**Answer: a) Static StaticMethod Instance InstanceMethod StaticValue InstanceValue**  
**Explanation:** Static initialization: print "Static", call getStaticValue() (prints "StaticMethod"), then instance initialization: print "Instance", call getInstanceValue() (prints "InstanceMethod"), then constructor prints current values.

---

## 26. What will be the output?
```java
class Singleton {
    private static Singleton instance = new Singleton();
    private static int counter = 0;
    
    private Singleton() {
        counter++;
        System.out.print("Counter: " + counter + " ");
    }
    
    public static Singleton getInstance() {
        return instance;
    }
    
    public static void main(String[] args) {
        System.out.print("Counter: " + counter + " ");
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.print("Counter: " + counter + " ");
    }
}
```
a) Counter: 1 Counter: 0 Counter: 1  
b) Counter: 0 Counter: 1 Counter: 1  
c) Counter: 1 Counter: 1 Counter: 1  
d) Counter: 0 Counter: 0 Counter: 1  

**Answer: a) Counter: 1 Counter: 0 Counter: 1**  
**Explanation:** Static variables initialize in order. `instance = new Singleton()` executes first (counter is still 0, constructor increments it to 1), then `counter = 0` resets it to 0. Main prints 0, then final print shows 1.

Wait, that's wrong. Let me reconsider: When `instance = new Singleton()` executes, counter is still 0 (not yet initialized), constructor increments to 1, then `counter = 0` sets it to 0.

**Correction: Answer is b) Counter: 0 Counter: 1 Counter: 1**

Actually, the order is: `instance` initialization calls constructor when counter is still 0 (uninitialized), constructor prints "Counter: 1", then counter is initialized to 0, then main prints "Counter: 0", finally prints "Counter: 0" again.

**Final Answer: Counter: 1 Counter: 0 Counter: 0**

---

## 27. What is the output?
```java
class Generic<T extends Number> {
    T value;
    
    Generic(T value) {
        this.value = value;
    }
    
    void compare(Generic<? super Integer> other) {
        System.out.print("Super ");
    }
    
    void compare(Generic<? extends Number> other) {
        System.out.print("Extends ");
    }
    
    public static void main(String[] args) {
        Generic<Integer> g1 = new Generic<>(10);
        Generic<Number> g2 = new Generic<>(20.5);
        g1.compare(g2);
    }
}
```
a) Super  
b) Extends  
c) Compilation error - ambiguous method  
d) Runtime error  

**Answer: c) Compilation error - ambiguous method**  
**Explanation:** Generic<Number> matches both ? super Integer (since Number is supertype of Integer) and ? extends Number, making the method call ambiguous.

---

## 28. What will be the output?
```java
class Parent {
    int x = 10;
    
    void display() {
        System.out.print("Parent: " + x + " ");
    }
}

class Child extends Parent {
    int x = 20;
    
    void display() {
        System.out.print("Child: " + x + " ");
        System.out.print("Super: " + super.x + " ");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p1 = new Parent();
        Parent p2 = new Child();
        Child c = new Child();
        
        p1.display();
        p2.display();
        c.display();
    }
}
```
a) Parent: 10 Child: 20 Super: 10 Child: 20 Super: 10  
b) Parent: 10 Parent: 10 Child: 20 Super: 10  
c) Parent: 10 Child: 20 Super: 10 Child: 20 Super: 10  
d) Parent: 10 Parent: 20 Child: 20 Super: 10  

**Answer: a) Parent: 10 Child: 20 Super: 10 Child: 20 Super: 10**  
**Explanation:** p1.display() calls Parent's method, p2.display() calls Child's overridden method (polymorphism), c.display() calls Child's method. All print their respective field values.

---

## 29. What is the output?
```java
class Test {
    void method() {
        System.out.print("Instance ");
    }
    
    static void method() {
        System.out.print("Static ");
    }
    
    public static void main(String[] args) {
        Test t = new Test();
        t.method();
        Test.method();
    }
}
```
a) Instance Static  
b) Static Instance  
c) Compilation error  
d) Static Static  

**Answer: c) Compilation error**  
**Explanation:** Cannot have both static and non-static methods with same signature in the same class.

---

## 30. What will be the output?
```java
class Outer {
    private static int x = 10;
    
    static class StaticNested {
        private static int x = 20;
        
        static void display() {
            System.out.print(x + " " + Outer.x + " ");
        }
    }
    
    class Inner {
        private int x = 30;
        
        void display() {
            System.out.print(x + " " + Outer.x + " ");
        }
    }
    
    public static void main(String[] args) {
        Outer.StaticNested.display();
        new Outer().new Inner().display();
    }
}
```
a) 20 10 30 10  
b) 10 20 10 30  
c) 20 20 30 30  
d) 10 10 10 10  

**Answer: a) 20 10 30 10**  
**Explanation:** StaticNested.display() prints its own x (20) and Outer.x (10). Inner.display() prints its own x (30) and Outer.x (10).

---

## 31. What is the output?
```java
interface Printable {
    default void print() {
        System.out.print("Interface ");
    }
}

abstract class Document implements Printable {
    public void print() {
        System.out.print("Abstract ");
    }
}

class PDF extends Document {
    // No print method defined
}

public class Test {
    public static void main(String[] args) {
        Printable p = new PDF();
        Document d = new PDF();
        PDF pdf = new PDF();
        
        p.print();
        d.print();
        pdf.print();
    }
}
```
a) Interface Abstract Abstract  
b) Abstract Abstract Abstract  
c) Interface Interface Abstract  
d) Abstract Interface Abstract  

**Answer: b) Abstract Abstract Abstract**  
**Explanation:** PDF inherits Document's print() method which overrides the interface default method. All three calls use the same method due to inheritance.

---

## 32. What will happen when this code runs?
```java
class Parent {
    final void method() {
        System.out.print("Parent ");
    }
}

class Child extends Parent {
    void method() {  // Line X
        System.out.print("Child ");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.method();
    }
}
```
a) Parent  
b) Child  
c) Compilation error at Line X  
d) Runtime error  

**Answer: c) Compilation error at Line X**  
**Explanation:** Final methods cannot be overridden.

---

## 33. What is the output?
```java
class Test {
    static int getValue() {
        System.out.print("Static ");
        return 5;
    }
    
    int getValue() {
        System.out.print("Instance ");
        return 10;
    }
    
    public static void main(String[] args) {
        Test t = null;
        System.out.print(t.getValue());
    }
}
```
a) Static 5  
b) Instance 10  
c) NullPointerException  
d) Compilation error  

**Answer: d) Compilation error**  
**Explanation:** Cannot have both static and instance methods with the same signature. The static method in Test conflicts with the instance method declaration.

---
