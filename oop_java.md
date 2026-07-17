# Java OOP Interview Questions & Answers (Q1–Q40)

---

# Q1. What happens internally when you create an object using the `new` keyword?

## Answer

When an object is created using the `new` keyword, Java performs the following steps:

1. Allocates memory in the Heap.
2. Initializes instance variables with default values.
3. Invokes the constructor.
4. Returns the object reference.

### One-Line Summary

> `new` = Allocate Memory → Initialize Defaults → Call Constructor → Return Reference

---

# Q2. Can we create an object without using the `new` keyword?

## Answer

Yes. Objects can be created using:

- `clone()`
- Reflection API
- Deserialization
- Factory Methods

---

# Q3. Can a class be declared without any variables or methods?

## Answer

Yes.

Java still:

- Creates a `.class` file
- Provides a default constructor (if none is defined)
- Allows object creation

Such classes are often called **Marker Classes**.

---

# Q4. What is the difference between an Object and an Object Reference?

| Object | Object Reference |
|---------|------------------|
| Actual data stored in Heap Memory | Variable that stores object's address |
| Created using `new` | Stored in Stack Memory |
| Contains state and behavior | Used to access the object |

### Example

```java
Student s = new Student();
```

- `new Student()` → Object
- `s` → Reference

---

# Q5. Does assigning `null` to a reference delete the object?

## Answer

No.

Assigning `null` only removes the reference.

```java
Student s = new Student();
s = null;
```

The object becomes **eligible for Garbage Collection**, but it is **not deleted immediately**.

---

# Q6. Can a class contain only static members? Is it still Object-Oriented?

## Answer

Yes.

A class may contain only static members.

However:

- Static members belong to the class, not objects.
- Such classes follow a procedural style rather than pure Object-Oriented Programming.

---

# Q7. Is Encapsulation only about making variables private?

## Answer

No.

Encapsulation means:

- Hiding data
- Restricting direct access
- Providing controlled access through methods

Usually achieved using:

- Private fields
- Getters
- Setters
- Validation

---

# Q8. Is a class with private fields and public setters truly encapsulated?

## Answer

Not necessarily.

If setters allow any value:

```java
setAge(-10);
```

then data integrity is broken.

True encapsulation requires validation.

### Example

```java
public void setAge(int age) {
    if (age > 0) {
        this.age = age;
    }
}
```

---

# Q9. Why do we use getters and setters instead of public fields?

## Answer

Benefits:

- Data hiding
- Validation
- Security
- Maintainability
- Business rule enforcement

---

# Q10. What is an Anonymous Class?

## Answer

An Anonymous Class is a class without a name.

It is created and instantiated at the same time.

Used for one-time implementations.

### Example

```java
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running");
    }
};
```

---

# Q11. What is the difference between Encapsulation and Abstraction?

| Encapsulation | Abstraction |
|--------------|-------------|
| Hides data | Hides implementation |
| Protects object state | Reduces complexity |
| Uses private fields | Uses abstract classes/interfaces |

### Example

- **Encapsulation:** Bank account hides balance.
- **Abstraction:** TV remote hides internal electronics.

---

# Q12. What problem does Abstraction solve that Encapsulation does not?

## Answer

Encapsulation protects data.

Abstraction hides complexity and exposes only necessary functionality.

### Example

Driving a car without knowing how the engine works.

---

# Q13. Why do we need Abstract Classes when we already have Interfaces?

## Answer

Both Abstract Classes and Interfaces provide abstraction, but they serve different purposes.

### Use an Abstract Class when:

- Classes are closely related.
- Common code needs to be shared.
- Constructors are required.
- Instance variables are needed.

### Example

```java
abstract class Vehicle {

    void start() {
        System.out.println("Vehicle Started");
    }

}
```

### Use an Interface when:

- Unrelated classes need to follow the same contract.
- Multiple inheritance of type is required.

### Example

```java
interface Payment {
    void pay();
}
```

Card Payment, UPI Payment, and Net Banking can all implement the `Payment` interface.

### Interview Tip

Since Java 8, interfaces support **default** and **static** methods, and Java 9 added **private methods**.

However, interfaces still **cannot have constructors or instance variables**.

---

# Q14. Can an Abstract Class exist without any Abstract Methods?

## Answer

Yes.

An abstract class can have zero abstract methods.

Such classes are mainly used to:

- Prevent object creation.
- Provide common implementation to subclasses.

### Example

```java
abstract class Animal {

    void eat() {
        System.out.println("Eating");
    }

}
```

---

# Q15. Why can't an Interface have Instance Variables?

## Answer

Interfaces define a contract, not an object's state.

Instance variables belong to objects, but interfaces cannot create objects.

Therefore, all interface variables are implicitly:

- `public`
- `static`
- `final`

### Example

```java
interface Test {

    int VALUE = 10;

}
```

Equivalent to:

```java
public static final int VALUE = 10;
```

---

# Q16. Why were Default, Static, and Private Methods introduced in Interfaces?

## Default Methods (Java 8)

### Purpose

To add new methods to existing interfaces without breaking existing implementations.

```java
interface Vehicle {

    default void start() {
        System.out.println("Started");
    }

}
```

---

## Static Methods (Java 8)

### Purpose

To provide utility/helper methods inside interfaces.

```java
interface MathUtil {

    static int square(int n) {
        return n * n;
    }

}
```

---

## Private Methods (Java 9)

### Purpose

To avoid code duplication between default methods.

```java
interface Demo {

    default void m1() {
        common();
    }

    default void m2() {
        common();
    }

    private void common() {
        System.out.println("Common Logic");
    }

}
```

---

# Q17. Why does Java support Multiple Inheritance using Interfaces but not Classes?

## Answer

Java does not allow multiple inheritance with classes because it causes the **Diamond Problem**.

### Example

```java
class A {
    void show() {}
}

class B extends A {}

class C extends A {}

// Invalid
class D extends B, C {}
```

Java cannot determine which implementation to use.

Interfaces avoid this issue because:

- They primarily define method declarations.
- If two interfaces provide the same default method, the implementing class must explicitly override it.

This eliminates ambiguity.

---

# Q18. Can an Interface exist without any Methods?

## Answer

Yes.

Such interfaces are called **Marker Interfaces**.

They provide metadata to the JVM or frameworks.

### Examples

- Serializable
- Cloneable
- Remote

---

# Q19. What makes an Interface a Functional Interface?

## Answer

A Functional Interface contains exactly **one abstract method**.

It is commonly used with Lambda Expressions.

### Example

```java
@FunctionalInterface
interface Calculator {

    int add(int a, int b);

}
```

---

# Q20. Can a Functional Interface have Default and Static Methods?

## Answer

Yes.

Default and static methods do **not** count as abstract methods.

### Example

```java
@FunctionalInterface
interface Test {

    void display();

    default void show() {}

    static void print() {}

}
```

The interface is still considered functional because it has only **one abstract method**.

---

# Q21. Why is `@FunctionalInterface` optional but recommended?

## Answer

The annotation is optional because the compiler can automatically recognize a functional interface.

However, it is recommended because it:

- Improves readability.
- Clearly communicates intent.
- Generates a compile-time error if another abstract method is added accidentally.

---

# Q22. Can a Functional Interface extend another Interface?

## Answer

Yes, but only if the total number of abstract methods remains **one**.

### Valid Example

```java
interface A {
    void display();
}

@FunctionalInterface
interface B extends A {

}
```

### Invalid Example

```java
interface A {
    void display();
}

interface C {
    void show();
}

@FunctionalInterface
interface D extends A, C {

}
```

This is invalid because `D` has **two abstract methods**.

---

# Q23. Why can't Private Methods be Overridden?

## Answer

Private methods are accessible only within the class where they are declared.

Since child classes cannot access them, they cannot override them.

```java
class Parent {

    private void show() {}

}

class Child extends Parent {

    // Not overriding
    void show() {}

}
```

---

# Q24. Why can't Static Methods be Overridden?

## Answer

Static methods belong to the class, not the object.

They are resolved at compile time.

When a child class defines a static method with the same signature, it **hides** the parent method rather than overriding it.

### Example

```java
class Parent {

    static void show() {
        System.out.println("Parent");
    }

}

class Child extends Parent {

    static void show() {
        System.out.println("Child");
    }

}
```

This is **Method Hiding**, not Method Overriding.

---

# Q25. What is Covariant Return Type?

## Answer

Covariant Return Type allows an overridden method to return a **more specific subtype** than the method in the parent class.

### Example

```java
class Animal {}

class Dog extends Animal {}

class Parent {

    Animal getAnimal() {
        return new Animal();
    }

}

class Child extends Parent {

    @Override
    Dog getAnimal() {
        return new Dog();
    }

}
```

This is allowed because `Dog` is a subclass of `Animal`.

---

# Q26. Can we override the `main()` method?

## Answer

No.

The `main()` method is static, and static methods cannot be overridden.

A child class may declare its own `main()` method, but this is **method hiding**, not overriding.

```java
class Parent {

    public static void main(String[] args) {
        System.out.println("Parent");
    }

}

class Child extends Parent {

    public static void main(String[] args) {
        System.out.println("Child");
    }

}
```

### Interview Tip

The JVM always invokes the `main()` method of the class you execute.

---

# Q27. Why is Method Overloading resolved at Compile Time but Overriding at Runtime?

## Answer

### Method Overloading

- Based on method signature.
- Compiler determines which method to call.
- Compile-Time Polymorphism.

```java
display(int);
display(String);
```

### Method Overriding

- Depends on the actual object.
- JVM decides at runtime.

```java
Animal a = new Dog();
a.sound();
```

Output:

```
Dog Sound
```

Hence, Runtime Polymorphism.

---

# Q28. Can we overload a method by changing only the return type?

## Answer

No.

Method overloading requires a different parameter list.

Changing only the return type causes a compile-time error.

### Invalid

```java
int add(int a, int b)

double add(int a, int b)
```

Compiler Error:

```
Duplicate Method
```

---

# Q29. Can Static Methods be Overloaded?

## Answer

Yes.

Static methods can be overloaded because overloading depends only on the parameter list.

```java
class Demo {

    static void show() {}

    static void show(int a) {}

    static void show(String s) {}

}
```

---

# Q30. Can we overload the `main()` method?

## Answer

Yes.

```java
public class Demo {

    public static void main(String[] args) {
        main(10);
    }

    public static void main(int x) {
        System.out.println(x);
    }

}
```

The JVM only calls:

```java
public static void main(String[] args)
```

Other overloaded versions must be invoked manually.

---

# Q31. Can Private Methods be Overloaded?

## Answer

Yes.

Overloading occurs within the same class.

Access modifiers do not matter.

```java
class Demo {

    private void show() {}

    private void show(int a) {}

}
```

---

# Q32. Can Constructors be Overridden?

## Answer

No.

Constructors are not inherited, so they cannot be overridden.

They belong only to the class in which they are declared.

---

# Q33. Can an Abstract Class have Constructors?

## Answer

Yes.

Although abstract classes cannot be instantiated directly, their constructors are executed when a subclass object is created.

```java
abstract class Animal {

    Animal() {
        System.out.println("Animal Constructor");
    }

}

class Dog extends Animal {

}
```

Creating:

```java
new Dog();
```

Output:

```
Animal Constructor
```

---

# Q34. Why doesn't Java allow Static Constructors?

## Answer

Static members belong to the class.

Objects are not required.

Java already provides:

- Static blocks
- Static variable initialization

### Example

```java
class Demo {

    static {
        System.out.println("Loaded");
    }

}
```

Hence, static constructors are unnecessary.

---

# Q35. Can a Constructor call another Constructor using `this()` and `super()`?

## Answer

Yes.

### Using `this()`

```java
class Demo {

    Demo() {
        this(10);
    }

    Demo(int x) {

    }

}
```

### Using `super()`

```java
class Parent {

    Parent() {}

}

class Child extends Parent {

    Child() {
        super();
    }

}
```

### Rule

- Only one of them can appear.
- Both must be the **first statement**.

---

# Q36. Why are Constructors not inherited but accessible using `super()`?

## Answer

Constructors initialize the object of their own class.

They are not inherited.

However, a child object contains a parent portion.

Therefore,

```java
super();
```

is used to initialize the parent part.

---

# Q37. What happens if all Constructors are Private?

## Answer

Objects cannot be created outside the class.

Common use cases:

- Singleton Pattern
- Utility Classes
- Factory Pattern

### Example

```java
class Singleton {

    private Singleton() {}

}
```

Outside:

```java
new Singleton();
```

Compile Error.

---

# Q38. What problems arise with too many Constructors?

## Answer

Problems include:

- Confusing API
- Difficult maintenance
- Duplicate initialization logic
- Poor readability

### Better Approach

Use:

- Builder Pattern
- Factory Pattern

instead of creating many overloaded constructors.

---

# Q39. Can a Subclass in another Package access Protected Members through an Object Reference?

## Answer

No.

A subclass outside the package can access protected members only through inheritance, not via a parent object reference.

### Not Allowed

```java
Parent p = new Parent();

p.show();
```

### Allowed

```java
class Child extends Parent {

    void display() {
        show();
    }

}
```

---

# Q40. Why are Interface Methods always Public?

## Answer

Interfaces define contracts.

Every implementing class must be able to access the methods.

Hence, all interface methods are implicitly:

- `public`
- `abstract` (unless `default`, `static`, or `private`)

### Example

```java
interface Demo {

    void display();

}
```

Compiler interprets it as:

```java
public abstract void display();
```

# Q41. What happens if a class has no Access Modifier in a Multi-Module Project?

## Answer

If a class has no access modifier, it has **package-private (default)** access.

This means:

- It is accessible only within the same package.
- Classes from other packages or modules cannot access it.

### Example

```java
class Employee {

}
```

Equivalent to:

- Package-private class
- Accessible only within its package

---

# Q42. Why can't a Top-Level Class be `private` or `protected`?

## Answer

A top-level class must be visible outside its source file.

Therefore, Java allows only:

- `public`
- Package-private (default)

`private` and `protected` are only valid for **nested (inner) classes**.

---

# Q43. Can fields be `public` and still maintain Encapsulation?

## Answer

Generally, **No**.

Public fields allow direct modification.

```java
employee.salary = -5000;
```

This breaks encapsulation.

However, **public final immutable fields** are acceptable because their values cannot be changed after initialization.

### Example

```java
public final String COUNTRY = "India";
```

---

# Q44. What is the difference between `this` and `super`?

| `this` | `super` |
|--------|---------|
| Refers to current object | Refers to parent class |
| Calls current class constructor | Calls parent constructor |
| Accesses current class members | Accesses parent class members |

### Example

```java
class Parent {

    int x = 10;

}

class Child extends Parent {

    int x = 20;

    void display() {

        System.out.println(this.x);

        System.out.println(super.x);

    }

}
```

### Output

```
20
10
```

---

# Q45. Can `this()` and `super()` be used together in the same Constructor?

## Answer

No.

Only **one constructor call** is allowed.

Also, it must be the **first statement**.

### Invalid

```java
Child() {

    this();

    super();

}
```

**Compiler Error**

---

# Q46. Can `this` or `super` be used inside a Static Method?

## Answer

No.

Static methods belong to the class, not an object.

Since there is no current object:

- `this` is unavailable.
- `super` is unavailable.

### Example

```java
static void show() {

    this.display();   // Error

}
```

---

# Q47. Can `super` access Private Members of the Parent Class?

## Answer

No.

Private members belong only to the class where they are declared.

### Example

```java
class Parent {

    private int age = 20;

}

class Child extends Parent {

    void display() {

        System.out.println(super.age);

    }

}
```

**Compile-time Error**

---

# Q48. Can `this` and `super` be used together in the same Method?

## Answer

Yes.

They can be used together to access current and parent class members.

### Example

```java
class Car {

    int speed = 100;

}

class SportsCar extends Car {

    int speed = 200;

    void display() {

        System.out.println(this.speed);

        System.out.println(super.speed);

    }

}
```

### Output

```
200
100
```

---

# Q49. What is the difference between Cohesion and Coupling?

| Cohesion | Coupling |
|-----------|----------|
| Measures how closely related responsibilities are within a class | Measures dependency between classes |
| High cohesion is good | Low coupling is good |
| Focuses on one class | Focuses on interaction between classes |

### Interview Tip

> **High Cohesion + Low Coupling = Good Software Design**

---

# Q50. Can a Class have High Cohesion but still be Tightly Coupled?

## Answer

Yes.

### Example

A `PaymentService` performs only payment-related operations.

So it has:

- ✔ High Cohesion

However, if it directly depends on:

- Bank API
- SMS API
- Database API

then it becomes **tightly coupled**.

Changing any dependency requires modifying the class.

---

# Q51. Is it possible to increase both Cohesion and Coupling simultaneously?

## Answer

Yes.

Suppose a large `OrderService` is divided into:

- `OrderValidator`
- `OrderSaver`
- `OrderNotifier`

Each class now performs one specific task.

✔ Higher Cohesion

However, these classes now communicate with one another.

✔ Coupling also increases.

The goal is to minimize unnecessary coupling by using:

- Interfaces
- Dependency Injection

---

# Q52. What is the difference between Association, Aggregation, and Composition?

| Association | Aggregation | Composition |
|-------------|-------------|-------------|
| Simple relationship | Has-a relationship | Strong Has-a relationship |
| Independent objects | Weak ownership | Strong ownership |
| Objects exist independently | Part exists without whole | Part cannot exist without whole |

### Examples

- **Association:** Doctor ↔ Patient
- **Aggregation:** School → Teacher
- **Composition:** House → Room

---

# Q53. Can Aggregation exist without Association?

## Answer

No.

Aggregation is a **specialized form of Association**.

Every Aggregation is an Association.

But every Association is **not** Aggregation.

### Relationship Hierarchy

```text
Association
      │
      ▼
Aggregation
      │
      ▼
Composition
```

---

# Q54. What design problems occur if Composition is used everywhere?

## Answer

Composition creates strong ownership.

If used unnecessarily:

- Classes become tightly connected.
- Reusability decreases.
- Maintenance becomes difficult.
- Small changes affect many classes.

Use Composition only when the child object's lifecycle depends on the parent.

---

# Q55. Give a real-world example where Aggregation is better than Composition.

## Answer

### School and Teacher

A school has teachers.

If the school closes,

teachers still exist and can join another school.

Hence,

**Aggregation** is the correct relationship.

---

# Q56. What is the best software design principle regarding Cohesion and Coupling?

## Answer

Aim for:

- High Cohesion
- Low Coupling

### Benefits

- Easier maintenance
- Better testing
- Improved reusability
- Greater flexibility

---

# Q57. When should you choose Composition over Inheritance?

## Answer

Use Composition when:

- You need flexibility.
- Relationships can change at runtime.
- Code reuse is preferred over inheritance.
- You want loose coupling.

### Interview Tip

> **Favor Composition over Inheritance**, as recommended by the GoF (Gang of Four) design principles.

---

# Q58. What are the real-world examples of OOP Relationships?

| Relationship | Example |
|--------------|---------|
| Association | Doctor ↔ Patient |
| Aggregation | Department → Employee |
| Composition | House → Room |
| Inheritance | Animal → Dog |
| Interface | Payment → UPI, Card, Net Banking |

---

