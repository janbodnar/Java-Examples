# Java Classes

This document contains 60 progressively advanced Java examples demonstrating  
object-oriented programming with classes using modern Java 25 syntax.  

## Basic class definition

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

Defines a simple class with fields and demonstrates object instantiation.  

## Class with method

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

Shows a class with a method that performs a calculation and returns a value.  

## Constructor basics

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

Demonstrates a parameterized constructor to initialize object fields.  

## Multiple constructors

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

Demonstrates constructor overloading with default and parameterized versions.  

## This keyword

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

Uses the `this` keyword to reference current object instance fields.  

## Return this for chaining

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

Returns `this` from methods to enable method chaining pattern.  

## Private fields

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

Demonstrates private access modifier for field encapsulation.  

## Public methods with private fields

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

Uses public methods to provide controlled access to private fields.  

## Getter and setter methods

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

Implements standard getter and setter pattern for data encapsulation.  

## Static fields

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

Uses static fields to share data across all instances of a class.  

## Static methods

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

Demonstrates static methods that can be called without object instantiation.  

## Static and instance members

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

Combines static and instance members to track object creation.  

## Basic inheritance

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

Demonstrates basic inheritance using the `extends` keyword.  

## Method overriding

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

Shows method overriding with the `@Override` annotation.  

## Super keyword

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

Uses `super` to call parent class constructor and methods.  

## Protected members

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

Demonstrates protected access modifier for inheritance hierarchies.  

## Abstract class

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

Shows abstract class with abstract and concrete methods.  

## Interface basics

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

Demonstrates basic interface implementation.  

## Multiple interfaces

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

Shows a class implementing multiple interfaces.  

## Interface with default method

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

Demonstrates interface default methods introduced in Java 8.  

## Interface static method

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

Shows static methods in interfaces for utility functions.  

## Records basics

```java
record Person(String name, int age) {}

void main() {
    var person = new Person("Alice", 30);
    IO.println(person.name() + " is " + person.age() + " years old");
}
```

Demonstrates Java records for immutable data carriers.  

## Records with methods

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

Shows records with custom methods while maintaining immutability.  

## Record validation

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

Demonstrates compact constructor validation in records.  

## Equals and hashCode

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

Implements `equals` and `hashCode` for proper object comparison.  

## ToString method

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

Overrides `toString` to provide meaningful string representation.  

## Inner class

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

Demonstrates inner class with access to outer class members.  

## Static nested class

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

Shows static nested class that doesn't require outer instance.  

## Anonymous class

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

Creates an anonymous class implementing an interface inline.  

## Local class

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

Demonstrates a local class defined within a method.  

## Pattern matching instanceof

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

Uses pattern matching with `instanceof` for type testing and casting.  

## Sealed classes

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

Demonstrates sealed classes for restricted inheritance hierarchies.  

## Immutable class

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

Creates an immutable class using final fields and defensive copying.  

## Builder pattern

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

Implements the builder pattern for flexible object construction.  

## Singleton pattern

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

Demonstrates singleton pattern ensuring single instance per class.  

## Generic class

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

Shows generic class for type-safe containers.  

## Bounded type parameters

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

Uses bounded type parameters to restrict generic types.  

## Composition over inheritance

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

Demonstrates composition as an alternative to inheritance.  

## Interface segregation

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

Applies interface segregation principle with focused interfaces.  

## Dependency injection

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

Shows constructor-based dependency injection for loose coupling.  

## Factory pattern

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

Implements factory pattern using enhanced switch expressions.  

## Observer pattern

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

Demonstrates observer pattern for event notification system.  

## Strategy pattern

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

Implements strategy pattern for interchangeable algorithms.  

## Command pattern

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

Shows command pattern for encapsulating requests as objects.  

## Fluent interface

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

Creates a fluent interface for readable method chaining.  

## Enum with methods

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

Demonstrates enums with instance methods for behavior.  

## Enum with fields and constructor

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

Shows enums with fields, constructor, and calculated properties.  

## Functional interface with lambda

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

Uses functional interface with lambda expressions for behavior passing.  

## Method reference

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

Demonstrates method references for concise functional programming.  

## Record with List field

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

Creates a record with collection field and custom methods.  

## Nested records

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

Demonstrates composition using nested record types.  

## Class with varargs

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

Uses varargs for methods accepting variable number of arguments.  

## Exception handling in class

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

Demonstrates exception handling within class methods.  

## Polymorphism with interfaces

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

Shows runtime polymorphism through interface references.  

## Class with static initialization block

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

Uses static initialization block for complex static setup.  

## Instance initialization block

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

Demonstrates instance initialization blocks executed before constructors.  

## Copy constructor

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

Implements copy constructor for creating object duplicates.  

## Comparable interface

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

Implements `Comparable` interface for natural ordering of objects.  

## Pattern matching with sealed classes

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

Combines sealed classes with pattern matching in switch expressions.  

## Custom annotation

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

Defines and uses custom annotations for metadata on classes.  
