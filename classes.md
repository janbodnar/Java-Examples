# Java Classes

This document contains 60 progressively advanced Java examples demonstrating  
object-oriented programming with classes using modern Java 25 syntax.  

## Basic class definition

This example defines a simple class to represent a person.

```java
class Person {
    String name;
    int age;
}

void main() {

    var p = new Person();
    p.name = "Alice";
    p.age = 30;
    IO.println(p.name + " is " + p.age + " years old.");
}
```
The `Person` class has two fields, `name` and `age`, for storing data.
An instance of the class is created, its fields are populated, and the
information is printed to the console.

## Class with method

This example shows a class containing a method to perform an action.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }
}

void main() {

    var calc = new Calculator();
    var result = calc.add(5, 3);
    IO.println("Result: " + result);
}
```
The `Calculator` class includes an `add` method that takes two integers,
sums them, and returns the result. An instance of the calculator is used to
call the method and display the output.

## Constructor basics

This example demonstrates a constructor for initializing object state.

```java
class Book {
    String title;
    String author;
    
    Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
}

void main() {

    var book = new Book("1984", "George Orwell");
    IO.println(book.title + " by " + book.author);
}
```
The `Book` class has a constructor that accepts a title and author,
assigning them to the object's fields upon creation. This ensures that a
`Book` object is always in a valid state right after instantiation.

## Multiple constructors

This example shows how a class can have multiple constructors.

```java
class Point {
    int x;
    int y;
    
    Point() {
        this.x = 0;
        this.y = 0;
    }
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

void main() {

    var p1 = new Point();
    var p2 = new Point(5, 10);
    IO.println("p1: (" + p1.x + "," + p1.y + ")");
    IO.println("p2: (" + p2.x + "," + p2.y + ")");
}
```
The `Point` class provides two constructors: a default one that sets
coordinates to zero and a parameterized one to set them to specific values.
This flexibility, known as constructor overloading, allows for multiple ways to create an object.

## This keyword

This example illustrates the use of the `this` keyword to reference the current object.

```java
class Employee {
    String name;
    int salary;
    
    Employee(String name, int salary) {
        this.name = name;
        this.salary = salary;
    }
    
    void display() {
        IO.println(this.name + " earns " + this.salary);
    }
}

void main() {

    var emp = new Employee("Bob", 50000);
    emp.display();
}
```
The `this` keyword is used within the `Employee` constructor to distinguish
between the class fields and the constructor parameters. It is also used in the
`display` method to refer to the current instance's fields.

## Return this for chaining

This example demonstrates returning `this` to enable method chaining.

```java
class Builder {
    String value = "";
    
    Builder append(String str) {
        this.value += str;
        return this;
    }
    
    void print() {
        IO.println(this.value);
    }
}

void main() {

    var b = new Builder();
    b.append("Hello").append(" ").append("World").print();
}
```
The `Builder` class has an `append` method that returns the current instance (`this`).
This allows multiple `append` calls to be chained together in a single, fluent statement,
making the code more readable and expressive.

## Private fields

This example shows how to use private fields to encapsulate data.

```java
class Account {
    private int balance;
    
    Account(int initial) {
        this.balance = initial;
    }
    
    int getBalance() {
        return this.balance;
    }
}

void main() {

    var acc = new Account(1000);
    IO.println("Balance: " + acc.getBalance());
}
```
The `balance` field in the `Account` class is marked as `private`, meaning
it cannot be accessed directly from outside the class. This enforces encapsulation,
a core principle of object-oriented programming.

## Public methods with private fields

This example uses public methods to provide controlled access to private data.

```java
class BankAccount {
    private int balance;
    
    BankAccount(int initial) {
        this.balance = initial;
    }
    
    public void deposit(int amount) {
        this.balance += amount;
    }
    
    public int getBalance() {
        return this.balance;
    }
}

void main() {

    var acc = new BankAccount(100);
    acc.deposit(50);
    IO.println("Balance: " + acc.getBalance());
}
```
The `BankAccount` class exposes a public `deposit` method to modify the
private `balance` field. This ensures that the balance can only be changed
through a well-defined and controlled interface.

## Getter and setter methods

This example implements standard getter and setter methods for encapsulation.

```java
class User {
    private String username;
    private String email;
    
    public String getUsername() {
        return this.username;
    }
    
    public void setUsername(String username) {
        this.username = username;
    }
    
    public String getEmail() {
        return this.email;
    }
    
    public void setEmail(String email) {
        this.email = email;
    }
}

void main() {

    var user = new User();
    user.setUsername("alice");
    user.setEmail("alice@example.com");
    IO.println(user.getUsername() + ": " + user.getEmail());
}
```
The `User` class provides public "getter" and "setter" methods to access and
modify its private fields. This pattern gives full control over how the internal
data of an object is managed.

## Static fields

This example demonstrates `static` fields that are shared across all instances.

```java
class Counter {
    static int count = 0;
    int id;
    
    Counter() {
        count++;
        this.id = count;
    }
}

void main() {

    var c1 = new Counter();
    var c2 = new Counter();
    var c3 = new Counter();
    IO.println("Total counters: " + Counter.count);
}
```
The `count` field is `static`, so it belongs to the `Counter` class itself,
not to any individual instance. It is incremented each time a new object is
created, effectively tracking the total number of instances.

## Static methods

This example shows `static` methods that can be called on the class directly.

```java
class MathUtils {
    static int square(int n) {
        return n * n;
    }
    
    static int cube(int n) {
        return n * n * n;
    }
}

void main() {

    IO.println("Square of 5: " + MathUtils.square(5));
    IO.println("Cube of 3: " + MathUtils.cube(3));
}
```
The `MathUtils` class contains `static` methods that do not depend on any object's
state. They can be called directly on the class, making them ideal for utility
functions that operate on their inputs.

## Static and instance members

This example combines static and instance members in a single class.

```java
class Product {
    static int totalProducts = 0;
    String name;
    double price;
    
    Product(String name, double price) {
        this.name = name;
        this.price = price;
        totalProducts++;
    }
    
    void display() {
        IO.println(this.name + ": $" + this.price);
    }
}

void main() {

    var p1 = new Product("Laptop", 999.99);
    var p2 = new Product("Mouse", 29.99);
    p1.display();
    p2.display();
    IO.println("Total products: " + Product.totalProducts);
}
```
The `Product` class uses an instance field `name` for each product and a `static`
field `totalProducts` to track the total count. This shows how static and instance
members can work together to manage both class-level and object-level data.

## Basic inheritance

This example demonstrates simple inheritance with the `extends` keyword.

```java
class Animal {
    String name;
    
    Animal(String name) {
        this.name = name;
    }
    
    void makeSound() {
        IO.println(this.name + " makes a sound");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);
    }
}

void main() {

    var dog = new Dog("Buddy");
    dog.makeSound();
}
```
The `Dog` class inherits from the `Animal` class, gaining its fields and methods.
This allows the `Dog` object to call the `makeSound` method defined in its parent,
showcasing the "is-a" relationship.

## Method overriding

This example shows how a subclass can provide its own version of a parent method.

```java
class Vehicle {
    void start() {
        IO.println("Vehicle starting...");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        IO.println("Car engine starting...");
    }
}

void main() {

    var car = new Car();
    car.start();
}
```
The `Car` class overrides the `start` method of its `Vehicle` parent to provide a
more specific implementation. The `@Override` annotation is used to ensure the method
signature correctly matches the parent's method.

## Super keyword

This example uses the `super` keyword to interact with the parent class.

```java
class Shape {
    String color;
    
    Shape(String color) {
        this.color = color;
    }
    
    void display() {
        IO.println("Shape color: " + this.color);
    }
}

class Circle extends Shape {
    int radius;
    
    Circle(String color, int radius) {
        super(color);
        this.radius = radius;
    }
    
    @Override
    void display() {
        super.display();
        IO.println("Circle radius: " + this.radius);
    }
}

void main() {

    var circle = new Circle("Red", 5);
    circle.display();
}
```
The `Circle` class uses `super(color)` to call its parent's constructor and
`super.display()` to invoke the parent's method. This allows a subclass to extend,
rather than completely replace, the functionality of its parent.

## Protected members

This example demonstrates `protected` members accessible within a class and its subclasses.

```java
class Parent {
    protected String message = "Hello from parent";
    
    protected void greet() {
        IO.println(this.message);
    }
}

class Child extends Parent {
    void display() {
        IO.println("Accessing protected member: " + this.message);
        this.greet();
    }
}

void main() {

    var child = new Child();
    child.display();
}
```
The `message` field in `Parent` is `protected`, allowing the `Child` class to access
it directly. This access modifier is useful for sharing implementation details within an
inheritance hierarchy without making them public.

## Abstract class

This example shows an abstract class that cannot be instantiated directly.

```java
abstract class AbstractShape {
    abstract double area();
    
    void describe() {
        IO.println("Area: " + this.area());
    }
}

class Rectangle extends AbstractShape {
    double width;
    double height;
    
    Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    double area() {
        return this.width * this.height;
    }
}

void main() {

    var rect = new Rectangle(5, 3);
    rect.describe();
}
```
The `AbstractShape` class defines an `abstract` method `area`, which must be
implemented by any concrete subclass. This forces subclasses like `Rectangle` to
provide their own specific logic for the abstract behavior.

## Interface basics

This example demonstrates implementing an interface to define a contract.

```java
interface Drawable {
    void draw();
}

class Square implements Drawable {
    int size;
    
    Square(int size) {
        this.size = size;
    }
    
    @Override
    public void draw() {
        IO.println("Drawing square of size " + this.size);
    }
}

void main() {

    var square = new Square(10);
    square.draw();
}
```
The `Drawable` interface specifies a `draw` method that any implementing class must
provide. The `Square` class implements this interface, guaranteeing that it has a `draw`
method as defined by the contract.

## Multiple interfaces

This example shows a class that implements multiple interfaces.

```java
interface Printable {
    void print();
}

interface Scannable {
    void scan();
}

class Printer implements Printable, Scannable {
    @Override
    public void print() {
        IO.println("Printing document...");
    }
    
    @Override
    public void scan() {
        IO.println("Scanning document...");
    }
}

void main() {

    var printer = new Printer();
    printer.print();
    printer.scan();
}
```
The `Printer` class implements both `Printable` and `Scannable`, meaning it must
provide implementations for the methods defined in both interfaces. This allows a
class to adopt behaviors from several different contracts.

## Interface with default method

This example demonstrates an interface with a `default` method providing a base implementation.

```java
interface Logger {
    default void log(String message) {
        IO.println("[LOG] " + message);
    }
    
    void logError(String error);
}

class ConsoleLogger implements Logger {
    @Override
    public void logError(String error) {
        IO.println("[ERROR] " + error);
    }
}

void main() {

    var logger = new ConsoleLogger();
    logger.log("Application started");
    logger.logError("Something went wrong");
}
```
The `Logger` interface includes a `default` method `log`, which implementing classes
can use without providing their own version. This allows interfaces to evolve without
breaking existing implementations.

## Interface static method

This example shows an interface containing `static` utility methods.

```java
interface StringUtils {
    static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
    
    static boolean isEmpty(String str) {
        return str == null || str.isEmpty();
    }
}

void main() {

    IO.println(StringUtils.reverse("hello"));
    IO.println("Is empty: " + StringUtils.isEmpty(""));
}
```
The `StringUtils` interface provides `static` methods that can be called directly
on the interface itself. This is a common pattern for grouping related utility functions
without needing to create a separate helper class.

## Records basics

This example introduces `record` types for creating simple data carriers.

```java
record Person(String name, int age) {}

void main() {

    var person = new Person("Alice", 30);
    IO.println(person.name() + " is " + person.age() + " years old");
}
```
A `record` is a concise way to define an immutable data class, automatically
providing a constructor, getters, `equals`, `hashCode`, and `toString`.
This reduces boilerplate code for simple data objects.

## Records with methods

This example shows how to add custom methods to a `record`.

```java
record Point(int x, int y) {
    double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
}

void main() {

    var point = new Point(3, 4);
    IO.println("Distance: " + point.distanceFromOrigin());
}
```
While records are primarily for data, you can add instance methods to them,
such as `distanceFromOrigin`. This allows you to add behavior related to the
data that the record holds.

## Record validation

This example demonstrates adding validation logic to a `record`'s constructor.

```java
record Temperature(double celsius) {
    Temperature {
        if (celsius < -273.15) {
            throw new IllegalArgumentException("Below absolute zero");
        }
    }
    
    double fahrenheit() {
        return celsius * 9/5 + 32;
    }
}

void main() {

    var temp = new Temperature(25);
    IO.println(temp.celsius() + "C = " + temp.fahrenheit() + "F");
}
```
A compact constructor inside the `Temperature` record is used to validate the
input `celsius` value. This ensures that an instance of the record can never be
created in an invalid state.

## Equals and hashCode

This example shows how to override `equals` and `hashCode` for custom equality logic.

```java
class Item {
    String name;
    int code;
    
    Item(String name, int code) {
        this.name = name;
        this.code = code;
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Item other)) return false;
        return this.code == other.code && this.name.equals(other.name);
    }
    
    @Override
    public int hashCode() {
        return this.name.hashCode() + this.code;
    }
}

void main() {

    var item1 = new Item("Widget", 123);
    var item2 = new Item("Widget", 123);
    IO.println("Equal: " + item1.equals(item2));
}
```
The `Item` class provides its own `equals` and `hashCode` methods to define object
equality based on `name` and `code`. This is crucial for collections like `HashMap`
and `HashSet` to work correctly.

## ToString method

This example demonstrates overriding the `toString` method for a custom string representation.

```java
class Movie {
    String title;
    int year;
    
    Movie(String title, int year) {
        this.title = title;
        this.year = year;
    }
    
    @Override
    public String toString() {
        return this.title + " (" + this.year + ")";
    }
}

void main() {

    var movie = new Movie("Inception", 2010);
    IO.println(movie);
}
```
The `Movie` class overrides `toString` to return a formatted string with its title
and year. This is useful for debugging and logging, as it provides more meaningful
output when an object is printed.

## Inner class

This example shows a class defined within another class.

```java
class Outer {
    private String message = "Hello";
    
    class Inner {
        void display() {
            IO.println(message + " from inner class");
        }
    }
    
    void createInner() {
        var inner = new Inner();
        inner.display();
    }
}

void main() {

    var outer = new Outer();
    outer.createInner();
}
```
The `Inner` class is defined inside the `Outer` class and has direct access
to its private members, like the `message` field. An inner class is associated
with an instance of the outer class.

## Static nested class

This example demonstrates a `static` class nested within another class.

```java
class Container {
    static class Node {
        int value;
        
        Node(int value) {
            this.value = value;
        }
        
        void display() {
            IO.println("Node value: " + this.value);
        }
    }
}

void main() {

    var node = new Container.Node(42);
    node.display();
}
```
A `static` nested class like `Node` does not have access to the instance members of its
outer class. It is essentially a regular class that is namespaced within another,
often used for helper or implementation details.

## Anonymous class

This example shows how to create a one-time class without a name.

```java
interface Greeting {
    void greet(String name);
}

void main() {

    Greeting greeting = new Greeting() {
        @Override
        public void greet(String name) {
            IO.println("Hello, " + name + "!");
        }
    };
    
    greeting.greet("Alice");
}
```
An anonymous class is created to provide an inline implementation of the `Greeting`
interface. This is a concise way to create an object with a specific, one-off
implementation, often used for event listeners.

## Local class

This example demonstrates a class defined inside a method.

```java
void main() {

    class LocalCounter {
        int count = 0;
        
        void increment() {
            count++;
        }
        
        void display() {
            IO.println("Count: " + count);
        }
    }
    
    var counter = new LocalCounter();
    counter.increment();
    counter.increment();
    counter.display();
}
```
The `LocalCounter` class is defined within the scope of the `main` method and is only
visible inside it. This is useful for creating a small helper class that is only needed
for a short period within a single method.

## Pattern matching instanceof

This example uses pattern matching with `instanceof` for cleaner type checks.

```java
class Animal {}
class Dog extends Animal {
    void bark() {
        IO.println("Woof!");
    }
}
class Cat extends Animal {
    void meow() {
        IO.println("Meow!");
    }
}

void main() {

    Animal animal = new Dog();
    
    if (animal instanceof Dog dog) {
        dog.bark();
    } else if (animal instanceof Cat cat) {
        cat.meow();
    }
}
```
Pattern matching combines the type check and the cast into a single operation.
If `animal` is a `Dog`, it is automatically cast to the `dog` variable, making
the code more concise and less error-prone.

## Sealed classes

This example introduces `sealed` classes to restrict which other classes may extend them.

```java
sealed class Result permits Success, Failure {}

final class Success extends Result {
    String data;
    Success(String data) { this.data = data; }
}

final class Failure extends Result {
    String error;
    Failure(String error) { this.error = error; }
}

void main() {

    Result result = new Success("Data loaded");
    
    if (result instanceof Success s) {
        IO.println("Success: " + s.data);
    }
}
```
The `Result` class is `sealed` and only permits `Success` and `Failure` to extend it.
This provides more control over an inheritance hierarchy, which is especially useful
in combination with pattern matching.

## Immutable class

This example shows how to create a class whose state cannot be changed after creation.

```java
final class ImmutablePoint {
    private final int x;
    private final int y;
    
    ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    int getX() { return this.x; }
    int getY() { return this.y; }
    
    ImmutablePoint move(int dx, int dy) {
        return new ImmutablePoint(this.x + dx, this.y + dy);
    }
}

void main() {

    var p1 = new ImmutablePoint(0, 0);
    var p2 = p1.move(5, 10);
    IO.println("p1: (" + p1.getX() + "," + p1.getY() + ")");
    IO.println("p2: (" + p2.getX() + "," + p2.getY() + ")");
}
```
The `ImmutablePoint` class has `final` fields and its `move` method returns a new
instance instead of modifying the existing one. Immutability makes objects inherently
thread-safe and easier to reason about.

## Builder pattern

This example implements the Builder pattern for constructing complex objects.

```java
class Car {
    private String brand;
    private String model;
    private int year;
    
    private Car() {}
    
    static class Builder {
        private Car car = new Car();
        
        Builder brand(String brand) {
            car.brand = brand;
            return this;
        }
        
        Builder model(String model) {
            car.model = model;
            return this;
        }
        
        Builder year(int year) {
            car.year = year;
            return this;
        }
        
        Car build() {
            return car;
        }
    }
    
    @Override
    public String toString() {
        return year + " " + brand + " " + model;
    }
}

void main() {

    var car = new Car.Builder()
        .brand("Toyota")
        .model("Camry")
        .year(2024)
        .build();
    
    IO.println(car);
}
```
The `Builder` pattern provides a flexible way to create an object by separating the
construction process from its representation. This is especially useful when an object
has many optional parameters or a complex setup.

## Singleton pattern

This example demonstrates the Singleton pattern to ensure only one instance of a class exists.

```java
class Singleton {
    private static Singleton instance;
    private int value;
    
    private Singleton() {
        this.value = 0;
    }
    
    static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
    
    void increment() {
        this.value++;
    }
    
    int getValue() {
        return this.value;
    }
}

void main() {

    var s1 = Singleton.getInstance();
    var s2 = Singleton.getInstance();
    s1.increment();
    IO.println("s1 value: " + s1.getValue());
    IO.println("s2 value: " + s2.getValue());
    IO.println("Same instance: " + (s1 == s2));
}
```
The `Singleton` class has a private constructor and a static `getInstance` method that
returns the single, shared instance. This pattern is useful for managing resources like
database connections or configuration settings.

## Generic class

This example shows a generic class that can work with any data type.

```java
class Box<T> {
    private T item;
    
    void set(T item) {
        this.item = item;
    }
    
    T get() {
        return this.item;
    }
}

void main() {

    var stringBox = new Box<String>();
    stringBox.set("Hello");
    IO.println(stringBox.get());
    
    var intBox = new Box<Integer>();
    intBox.set(42);
    IO.println(intBox.get());
}
```
The `Box<T>` class uses a type parameter `T` to create a type-safe container. This
allows the same class to be used for storing a `String`, an `Integer`, or any other
object type without sacrificing type safety.

## Bounded type parameters

This example uses bounded type parameters to restrict the types that can be used.

```java
class NumberBox<T extends Number> {
    private T number;
    
    NumberBox(T number) {
        this.number = number;
    }
    
    double doubleValue() {
        return this.number.doubleValue();
    }
}

void main() {

    var intBox = new NumberBox<>(42);
    var doubleBox = new NumberBox<>(3.14);
    
    IO.println("Int as double: " + intBox.doubleValue());
    IO.println("Double value: " + doubleBox.doubleValue());
}
```
The `NumberBox` class uses `<T extends Number>` to specify that `T` must be a subclass
of `Number`. This allows the class to call methods defined in `Number`, like `doubleValue`,
while still maintaining generic flexibility.

## Composition over inheritance

This example demonstrates using composition as a flexible alternative to inheritance.

```java
class Engine {
    void start() {
        IO.println("Engine started");
    }
}

class Car {
    private Engine engine;
    
    Car() {
        this.engine = new Engine();
    }
    
    void start() {
        this.engine.start();
        IO.println("Car is ready to drive");
    }
}

void main() {

    var car = new Car();
    car.start();
}
```
Instead of inheriting from `Engine`, the `Car` class contains an `Engine` instance.
This "has-a" relationship is often more flexible than the "is-a" relationship of
inheritance, allowing for greater modularity.

## Interface segregation

This example applies the Interface Segregation Principle for more focused interfaces.

```java
interface Readable {
    String read();
}

interface Writable {
    void write(String data);
}

class File implements Readable, Writable {
    private String content = "";
    
    @Override
    public String read() {
        return this.content;
    }
    
    @Override
    public void write(String data) {
        this.content = data;
    }
}

void main() {

    var file = new File();
    file.write("Hello World");
    IO.println(file.read());
}
```
Instead of one large interface, `Readable` and `Writable` define separate behaviors.
This allows a class to implement only the functionalities it needs, leading to more
decoupled and maintainable code.

## Dependency injection

This example shows dependency injection to decouple components.

```java
interface MessageService {
    void send(String message);
}

class EmailService implements MessageService {
    @Override
    public void send(String message) {
        IO.println("Email: " + message);
    }
}

class Notification {
    private MessageService service;
    
    Notification(MessageService service) {
        this.service = service;
    }
    
    void notify(String message) {
        this.service.send(message);
    }
}

void main() {

    var emailService = new EmailService();
    var notification = new Notification(emailService);
    notification.notify("Hello!");
}
```
The `Notification` class receives its `MessageService` dependency through its constructor.
This decouples `Notification` from a specific implementation like `EmailService`, making
the system more modular and easier to test.

## Factory pattern

This example implements the Factory pattern to create objects.

```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        IO.println("Drawing Circle");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        IO.println("Drawing Square");
    }
}

class ShapeFactory {
    static Shape createShape(String type) {
        return switch (type) {
            case "circle" -> new Circle();
            case "square" -> new Square();
            default -> throw new IllegalArgumentException("Unknown shape");
        };
    }
}

void main() {

    var circle = ShapeFactory.createShape("circle");
    var square = ShapeFactory.createShape("square");
    circle.draw();
    square.draw();
}
```
The `ShapeFactory` centralizes the logic for creating different `Shape` objects.
This decouples the client code from the specific classes being instantiated, making it
easier to add new shapes in the future.

## Observer pattern

This example demonstrates the Observer pattern for event-driven notifications.

```java
interface Observer {
    void update(String message);
}

class Subject {
    private var observers = new ArrayList<Observer>();
    
    void attach(Observer observer) {
        this.observers.add(observer);
    }
    
    void notifyObservers(String message) {
        for (var observer : this.observers) {
            observer.update(message);
        }
    }
}

class ConcreteObserver implements Observer {
    private String name;
    
    ConcreteObserver(String name) {
        this.name = name;
    }
    
    @Override
    public void update(String message) {
        IO.println(this.name + " received: " + message);
    }
}

void main() {

    var subject = new Subject();
    subject.attach(new ConcreteObserver("Observer1"));
    subject.attach(new ConcreteObserver("Observer2"));
    subject.notifyObservers("Hello Observers!");
}
```
The `Subject` maintains a list of `Observer` objects and notifies them of any changes.
This creates a one-to-many dependency where observers are automatically updated, promoting
loose coupling between components.

## Strategy pattern

This example implements the Strategy pattern to make algorithms interchangeable.

```java
interface SortStrategy {
    void sort(int[] array);
}

class BubbleSort implements SortStrategy {
    @Override
    public void sort(int[] array) {
        IO.println("Sorting using Bubble Sort");
    }
}

class QuickSort implements SortStrategy {
    @Override
    public void sort(int[] array) {
        IO.println("Sorting using Quick Sort");
    }
}

class Sorter {
    private SortStrategy strategy;
    
    void setStrategy(SortStrategy strategy) {
        this.strategy = strategy;
    }
    
    void sort(int[] array) {
        this.strategy.sort(array);
    }
}

void main() {

    var sorter = new Sorter();
    sorter.setStrategy(new BubbleSort());
    sorter.sort(new int[]{5, 2, 8, 1});
    
    sorter.setStrategy(new QuickSort());
    sorter.sort(new int[]{5, 2, 8, 1});
}
```
The `Sorter` class can use different sorting algorithms (`BubbleSort`, `QuickSort`) by
swapping out its `SortStrategy` object. This pattern allows the algorithm to be selected
at runtime, independent of the client that uses it.

## Command pattern

This example shows the Command pattern to encapsulate a request as an object.

```java
interface Command {
    void execute();
}

class Light {
    void on() {
        IO.println("Light is ON");
    }
    
    void off() {
        IO.println("Light is OFF");
    }
}

class LightOnCommand implements Command {
    private Light light;
    
    LightOnCommand(Light light) {
        this.light = light;
    }
    
    @Override
    public void execute() {
        this.light.on();
    }
}

class LightOffCommand implements Command {
    private Light light;
    
    LightOffCommand(Light light) {
        this.light = light;
    }
    
    @Override
    public void execute() {
        this.light.off();
    }
}

void main() {

    var light = new Light();
    var onCommand = new LightOnCommand(light);
    var offCommand = new LightOffCommand(light);
    
    onCommand.execute();
    offCommand.execute();
}
```
The `LightOnCommand` and `LightOffCommand` objects encapsulate the action of turning a light
on or off. This allows requests to be passed around, queued, or logged, decoupling the
sender of a request from its receiver.

## Fluent interface

This example creates a fluent interface for more readable and chainable method calls.

```java
class Query {
    private String table;
    private String condition;
    private int limit;
    
    Query from(String table) {
        this.table = table;
        return this;
    }
    
    Query where(String condition) {
        this.condition = condition;
        return this;
    }
    
    Query limit(int limit) {
        this.limit = limit;
        return this;
    }
    
    void execute() {
        var sql = "SELECT * FROM " + table;
        if (condition != null) sql += " WHERE " + condition;
        if (limit > 0) sql += " LIMIT " + limit;
        IO.println(sql);
    }
}

void main() {

    new Query()
        .from("users")
        .where("age > 18")
        .limit(10)
        .execute();
}
```
The `Query` class methods return the instance itself, allowing calls to be chained
together in a natural, sentence-like way. This API style makes the code more intuitive
and easier to read.

## Enum with methods

This example demonstrates an `enum` with methods to add behavior.

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
    
    boolean isWeekend() {
        return this == SATURDAY || this == SUNDAY;
    }
    
    boolean isWeekday() {
        return !isWeekend();
    }
}

void main() {

    var today = Day.MONDAY;
    IO.println(today + " is weekend: " + today.isWeekend());
    IO.println(today + " is weekday: " + today.isWeekday());
}
```
The `Day` enum includes `isWeekend` and `isWeekday` methods, allowing it to encapsulate
not just values but also the logic associated with them. This makes enums more powerful
than simple collections of constants.

## Enum with fields and constructor

This example shows an `enum` with fields, a constructor, and methods.

```java
enum Planet {
    MERCURY(3.303e23, 2.4397e6),
    EARTH(5.976e24, 6.37814e6),
    MARS(6.421e23, 3.3972e6);
    
    private final double mass;
    private final double radius;
    
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }
    
    double surfaceGravity() {
        final double G = 6.67300E-11;
        return G * mass / (radius * radius);
    }
}

void main() {

    var earth = Planet.EARTH;
    IO.println("Earth gravity: " + earth.surfaceGravity());
}
```
The `Planet` enum stores data for each constant and uses a method to calculate a value.
This demonstrates how enums can represent a set of complex, constant objects, each with
its own state and behavior.

## Functional interface with lambda

This example uses a functional interface with a lambda expression to pass behavior.

```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

class Operations {
    static void perform(int a, int b, Calculator calc) {
        IO.println("Result: " + calc.calculate(a, b));
    }
}

void main() {

    Operations.perform(5, 3, (a, b) -> a + b);
    Operations.perform(5, 3, (a, b) -> a * b);
}
```
The `Calculator` interface is marked as `@FunctionalInterface`, allowing it to be
implemented by a lambda expression. This provides a concise way to pass behavior as if
it were data, a core concept of functional programming.

## Method reference

This example demonstrates method references as a shorthand for certain lambdas.

```java
class StringProcessor {
    static String toUpperCase(String str) {
        return str.toUpperCase();
    }
    
    void process(String str) {
        IO.println("Processing: " + str);
    }
}

void main() {

    var words = List.of("hello", "world", "java");
    
    words.stream()
        .map(StringProcessor::toUpperCase)
        .forEach(IO::println);
    
    var processor = new StringProcessor();
    words.forEach(processor::process);
}
```
Method references like `StringProcessor::toUpperCase` and `IO::println` provide a more
compact and readable way to write lambda expressions that simply call an existing method.
They make functional-style code even more concise.

## Record with List field

This example shows a `record` that contains a collection field.

```java
record ShoppingCart(List<String> items) {
    int itemCount() {
        return items.size();
    }
    
    void display() {
        IO.println("Cart contains " + itemCount() + " items:");
        items.forEach(item -> IO.println("- " + item));
    }
}

void main() {

    var cart = new ShoppingCart(
        List.of("Apple", "Banana", "Orange")
    );
    cart.display();
}
```
The `ShoppingCart` record holds a list of items, demonstrating that records can
manage complex data structures. Custom methods like `itemCount` can be added to provide
behavior related to the record's state.

## Nested records

This example demonstrates composition by nesting one `record` inside another.

```java
record Address(String street, String city) {}

record Person(String name, Address address) {
    String fullAddress() {
        return address.street() + ", " + address.city();
    }
}

void main() {

    var address = new Address("123 Main St", "New York");
    var person = new Person("Alice", address);
    IO.println(person.name() + " lives at " + person.fullAddress());
}
```
The `Person` record contains an `Address` record, showcasing how complex, immutable
data structures can be built by composing smaller records. This promotes a clean and
declarative style for modeling data.

## Class with varargs

This example uses varargs to create a method that accepts a variable number of arguments.

```java
class Statistics {
    static double average(int... numbers) {
        if (numbers.length == 0) return 0;
        
        var sum = 0;
        for (var num : numbers) {
            sum += num;
        }
        return (double) sum / numbers.length;
    }
}

void main() {

    IO.println("Average: " + Statistics.average(10, 20, 30, 40));
    IO.println("Average: " + Statistics.average(5, 15));
}
```
The `average` method's `int... numbers` parameter allows it to be called with any
number of integer arguments. This provides a convenient way to create flexible methods
that can handle varying numbers of inputs.

## Exception handling in class

This example demonstrates how to handle exceptions within a class method.

```java
class Validator {
    static void validateAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
        if (age > 150) {
            throw new IllegalArgumentException("Age is too high");
        }
        IO.println("Valid age: " + age);
    }
}

void main() {

    try {
        Validator.validateAge(25);
        Validator.validateAge(-5);
    } catch (IllegalArgumentException e) {
        IO.println("Error: " + e.getMessage());
    }
}
```
The `validateAge` method throws an `IllegalArgumentException` if the input is invalid.
The calling code in `main` uses a `try-catch` block to handle the potential error,
making the program more robust.

## Polymorphism with interfaces

This example shows runtime polymorphism using an interface reference.

```java
interface Payment {
    void pay(double amount);
}

class CreditCard implements Payment {
    @Override
    public void pay(double amount) {
        IO.println("Paid $" + amount + " with Credit Card");
    }
}

class PayPal implements Payment {
    @Override
    public void pay(double amount) {
        IO.println("Paid $" + amount + " with PayPal");
    }
}

void main() {

    var payments = List.<Payment>of(
        new CreditCard(),
        new PayPal()
    );
    
    for (var payment : payments) {
        payment.pay(100.0);
    }
}
```
A list of `Payment` objects can hold instances of both `CreditCard` and `PayPal`.
When the `pay` method is called, the correct implementation is chosen at runtime,
demonstrating the power of polymorphism.

## Class with static initialization block

This example uses a `static` initialization block for complex setup.

```java
class Configuration {
    static String environment;
    static int timeout;
    
    static {
        environment = "production";
        timeout = 5000;
        IO.println("Configuration initialized");
    }
    
    static void display() {
        IO.println("Env: " + environment + ", Timeout: " + timeout);
    }
}

void main() {

    Configuration.display();
}
```
The `static` block in the `Configuration` class runs once when the class is first loaded.
It is useful for performing complex initialization for static fields that cannot be
done in a single expression.

## Instance initialization block

This example demonstrates an instance initialization block.

```java
class Connection {
    private int id;
    private String status;
    
    {
        id = (int) (Math.random() * 1000);
        status = "initialized";
        IO.println("Instance block executed for ID: " + id);
    }
    
    Connection() {
        IO.println("Constructor executed");
    }
}

void main() {

    var conn1 = new Connection();
    var conn2 = new Connection();
}
```
The code inside the `{}` block runs every time an instance of `Connection` is created,
just before the constructor is called. It is useful for sharing setup logic between
multiple constructors.

## Copy constructor

This example implements a copy constructor to create a new object from an existing one.

```java
class Point {
    int x;
    int y;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    Point(Point other) {
        this.x = other.x;
        this.y = other.y;
    }
    
    @Override
    public String toString() {
        return "(" + x + "," + y + ")";
    }
}

void main() {

    var p1 = new Point(5, 10);
    var p2 = new Point(p1);
    IO.println("p1: " + p1);
    IO.println("p2: " + p2);
}
```
The `Point(Point other)` constructor creates a new `Point` object with the same state as
the one passed in. This is a common pattern for creating a deep copy of a mutable object,
ensuring the two instances are independent.

## Comparable interface

This example implements the `Comparable` interface to define a natural ordering.

```java
class Student implements Comparable<Student> {
    String name;
    int score;
    
    Student(String name, int score) {
        this.name = name;
        this.score = score;
    }
    
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.score, other.score);
    }
    
    @Override
    public String toString() {
        return name + ": " + score;
    }
}

void main() {

    var students = new ArrayList<Student>();
    students.add(new Student("Alice", 85));
    students.add(new Student("Bob", 92));
    students.add(new Student("Charlie", 78));
    
    students.sort(null);
    students.forEach(IO::println);
}
```
By implementing `Comparable<Student>`, the `Student` class defines how its instances should
be sorted, in this case by score. This allows collections of `Student` objects to be
sorted easily using methods like `Collections.sort()`.

## Pattern matching with sealed classes

This example combines `sealed` classes with pattern matching in a `switch`.

```java
sealed interface Payment permits CreditCardPayment, CashPayment {}

record CreditCardPayment(String cardNumber, double amount) 
    implements Payment {}

record CashPayment(double amount) implements Payment {}

class PaymentProcessor {
    static void process(Payment payment) {
        switch (payment) {
            case CreditCardPayment cc -> 
                IO.println("Card " + cc.cardNumber() + ": $" + cc.amount());
            case CashPayment cash -> 
                IO.println("Cash: $" + cash.amount());
        }
    }
}

void main() {

    PaymentProcessor.process(new CreditCardPayment("1234", 100.0));
    PaymentProcessor.process(new CashPayment(50.0));
}
```
Because `Payment` is a `sealed` interface, the compiler knows all possible subtypes.
This allows the `switch` statement to be exhaustive without a `default` case, making
the code safer and more expressive.

## Custom annotation

This example shows how to define and use a custom annotation.

```java
@interface Author {
    String name();
    String date();
}

@Author(name = "Alice", date = "2024-01-15")
class AnnotatedClass {
    void display() {
        var annotation = this.getClass().getAnnotation(Author.class);
        if (annotation != null) {
            IO.println("Author: " + annotation.name());
            IO.println("Date: " + annotation.date());
        }
    }
}

void main() {

    var obj = new AnnotatedClass();
    obj.display();
}
```
A custom annotation `@Author` is created to add metadata to the `AnnotatedClass`.
This metadata can then be read at runtime using reflection, allowing for powerful
frameworks and tools to be built.
