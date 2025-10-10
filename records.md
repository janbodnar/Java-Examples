# Java Records

This document contains 60 progressively advanced Java examples demonstrating  
various record features and patterns using modern Java 25 syntax.  

## Basic record declaration

```java
record Point(int x, int y) {}

void main() {

    var p = new Point(3, 4);
    IO.println("Point: (" + p.x() + ", " + p.y() + ")");
}
```

Defines a simple record `Point` with two components and prints them.  

## Record with single component

```java
record Temperature(double celsius) {}

void main() {

    var temp = new Temperature(23.5);
    IO.println("Temperature: " + temp.celsius() + "°C");
}
```

Creates a record with a single component to represent temperature data.  

## Record with String component

```java
record Person(String name) {}

void main() {

    var person = new Person("Alice");
    IO.println("Name: " + person.name());
}
```

Demonstrates a record with a String component for storing text data.  

## Record with multiple types

```java
record Product(String name, double price, int quantity) {}

void main() {

    var product = new Product("Laptop", 999.99, 5);
    IO.println(product.name() + ": $" + product.price());
}
```

Shows a record with different component types: String, double, and int.  

## Record toString method

```java
record Book(String title, String author) {}

void main() {

    var book = new Book("1984", "George Orwell");
    IO.println(book);
}
```

Records automatically generate a `toString` method for easy output.  

## Record equality

```java
record Coordinate(int x, int y) {}

void main() {

    var c1 = new Coordinate(1, 2);
    var c2 = new Coordinate(1, 2);
    IO.println("Equal: " + c1.equals(c2));
}
```

Records implement `equals` method based on component values automatically.  

## Record hashCode

```java
record User(String username, int id) {}

void main() {

    var user = new User("alice", 101);
    IO.println("Hash: " + user.hashCode());
}
```

Records generate consistent `hashCode` implementations based on components.  

## Record in a List

```java
record City(String name, int population) {}

void main() {

    var cities = List.of(
        new City("Tokyo", 13960000),
        new City("Delhi", 32900000)
    );
    cities.forEach(IO::println);
}
```

Demonstrates storing record instances in a List collection.  

## Iterating over records

```java
record Color(int r, int g, int b) {}

void main() {

    var colors = List.of(
        new Color(255, 0, 0),
        new Color(0, 255, 0)
    );
    for (var color : colors) {
        IO.println("RGB: " + color.r() + "," + color.g() + "," + color.b());
    }
}
```

Shows iteration over a collection of records with component access.  

## Record as Map key

```java
record Position(int row, int col) {}

void main() {

    var grid = Map.of(
        new Position(0, 0), "Start",
        new Position(5, 5), "End"
    );
    IO.println(grid.get(new Position(0, 0)));
}
```

Records work well as Map keys due to proper `equals` and `hashCode`.  

## Record as Map value

```java
record Score(int value, String grade) {}

void main() {

    var scores = Map.of(
        "Alice", new Score(95, "A"),
        "Bob", new Score(87, "B")
    );
    IO.println(scores.get("Alice"));
}
```

Stores record instances as values in a Map for structured data.  

## Nested records

```java
record Address(String street, String city) {}
record Employee(String name, Address address) {}

void main() {

    var addr = new Address("Main St", "Springfield");
    var emp = new Employee("John", addr);
    IO.println(emp.name() + " lives in " + emp.address().city());
}
```

Demonstrates records containing other records as components.  

## Record with List component

```java
record Team(String name, List<String> members) {}

void main() {

    var team = new Team("Alpha", List.of("Alice", "Bob", "Charlie"));
    IO.println(team.name() + ": " + team.members().size() + " members");
}
```

Shows a record component that holds a collection of values.  

## Record with array component

```java
record Matrix(int[][] values) {}

void main() {

    var matrix = new Matrix(new int[][]{{1, 2}, {3, 4}});
    IO.println("First element: " + matrix.values()[0][0]);
}
```

Records can have array components for structured data storage.  

## Record with boolean component

```java
record Account(String username, boolean active) {}

void main() {

    var account = new Account("alice", true);
    IO.println(account.username() + " active: " + account.active());
}
```

Demonstrates using boolean components in records for flags and states.  

## Compact constructor validation

```java
record Age(int years) {
    public Age {
        if (years < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }
}

void main() {

    var age = new Age(25);
    IO.println("Age: " + age.years());
}
```

Uses compact constructor syntax to validate record component values.  

## Compact constructor normalization

```java
record Email(String address) {
    public Email {
        address = address.toLowerCase().trim();
    }
}

void main() {

    var email = new Email("  USER@EXAMPLE.COM  ");
    IO.println(email.address());
}
```

Normalizes component values in compact constructor before assignment.  

## Canonical constructor

```java
record Rectangle(double width, double height) {
    public Rectangle(double width, double height) {
        if (width <= 0 || height <= 0) {
            throw new IllegalArgumentException("Invalid dimensions");
        }
        this.width = width;
        this.height = height;
    }
}

void main() {

    var rect = new Rectangle(10, 5);
    IO.println("Width: " + rect.width());
}
```

Demonstrates explicit canonical constructor with full validation logic.  

## Custom constructor

```java
record Circle(double radius) {
    public Circle(double diameter, boolean isDiameter) {
        this(isDiameter ? diameter / 2.0 : diameter);
    }
}

void main() {

    var c1 = new Circle(10.0, true);
    IO.println("Radius from diameter: " + c1.radius());
}
```

Adds alternative constructor that delegates to canonical constructor.  

## Record with custom method

```java
record Point(int x, int y) {
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
}

void main() {

    var p = new Point(3, 4);
    IO.println("Distance: " + p.distanceFromOrigin());
}
```

Records can have custom instance methods for computed properties.  

## Record with static method

```java
record Temperature(double celsius) {
    public static Temperature fromFahrenheit(double f) {
        return new Temperature((f - 32) * 5 / 9);
    }
}

void main() {

    var temp = Temperature.fromFahrenheit(98.6);
    IO.println("Body temp: " + temp.celsius() + "°C");
}
```

Static factory methods provide alternative ways to create record instances.  

## Record with multiple methods

```java
record Money(double amount, String currency) {
    public String formatted() {
        return currency + " " + String.format("%.2f", amount);
    }
    
    public Money add(Money other) {
        if (!currency.equals(other.currency)) {
            throw new IllegalArgumentException("Currency mismatch");
        }
        return new Money(amount + other.amount, currency);
    }
}

void main() {

    var m1 = new Money(100.50, "USD");
    var m2 = new Money(50.25, "USD");
    IO.println(m1.add(m2).formatted());
}
```

Records can contain multiple custom methods for rich domain behavior.  

## Record with static field

```java
record Config(String value) {
    public static final String DEFAULT_VALUE = "default";
    
    public static Config getDefault() {
        return new Config(DEFAULT_VALUE);
    }
}

void main() {

    var config = Config.getDefault();
    IO.println("Config: " + config.value());
}
```

Records can have static fields and methods for shared constants.  

## Pattern matching with instanceof

```java
record Point(int x, int y) {}

void main() {

    Object obj = new Point(5, 10);
    
    if (obj instanceof Point p) {
        IO.println("Point at: " + p.x() + ", " + p.y());
    }
}
```

Pattern matching extracts record reference with type checking in one step.  

## Record pattern deconstruction

```java
record Point(int x, int y) {}

void main() {

    Object obj = new Point(5, 10);
    
    if (obj instanceof Point(int x, int y)) {
        IO.println("Coordinates: x=" + x + ", y=" + y);
        IO.println("Sum: " + (x + y));
    }
}
```

Record patterns extract components directly in pattern matching.  

## Nested record pattern

```java
record Point(int x, int y) {}
record Circle(Point center, double radius) {}

void main() {

    Object obj = new Circle(new Point(0, 0), 5.0);
    
    if (obj instanceof Circle(Point(int x, int y), double r)) {
        IO.println("Circle at (" + x + "," + y + ") radius: " + r);
    }
}
```

Deconstructs nested records in a single pattern matching expression.  

## Switch with record patterns

```java
record Point(int x, int y) {}
record Circle(double radius) {}

void main() {

    Object shape = new Circle(5.0);
    
    var description = switch (shape) {
        case Point(int x, int y) -> "Point at " + x + "," + y;
        case Circle(double r) -> "Circle with radius " + r;
        default -> "Unknown shape";
    };
    IO.println(description);
}
```

Uses record patterns in switch expressions for type-based dispatch.  

## Guarded record patterns

```java
record Point(int x, int y) {}

void main() {

    Object obj = new Point(5, 10);
    
    var quadrant = switch (obj) {
        case Point(int x, int y) when x > 0 && y > 0 -> "Q1";
        case Point(int x, int y) when x < 0 && y > 0 -> "Q2";
        case Point(int x, int y) when x < 0 && y < 0 -> "Q3";
        case Point(int x, int y) when x > 0 && y < 0 -> "Q4";
        default -> "Origin or axis";
    };
    IO.println("Quadrant: " + quadrant);
}
```

Combines record patterns with guards for conditional matching logic.  

## Record in switch with yield

```java
record Success(String message) {}
record Error(String message) {}

void main() {

    Object result = new Success("Operation completed");
    
    var output = switch (result) {
        case Success(String msg) -> {
            yield "✓ " + msg;
        }
        case Error(String msg) -> {
            yield "✗ " + msg;
        }
        default -> "Unknown result";
    };
    IO.println(output);
}
```

Uses yield in switch branches when working with record patterns.  

## Generic record

```java
record Box<T>(T value) {}

void main() {

    var intBox = new Box<>(42);
    var strBox = new Box<>("Hello");
    IO.println("Int: " + intBox.value());
    IO.println("String: " + strBox.value());
}
```

Records support type parameters for generic data containers.  

## Generic record with multiple types

```java
record Pair<K, V>(K key, V value) {}

void main() {

    var pair = new Pair<>("age", 25);
    IO.println(pair.key() + " = " + pair.value());
}
```

Demonstrates a record with multiple generic type parameters.  

## Generic record with bounds

```java
record NumberBox<T extends Number>(T value) {
    public double asDouble() {
        return value.doubleValue();
    }
}

void main() {

    var box = new NumberBox<>(42);
    IO.println("As double: " + box.asDouble());
}
```

Uses bounded type parameters to restrict generic record components.  

## Record with Optional component

```java
record Profile(String name, java.util.Optional<String> email) {}

void main() {

    var p1 = new Profile("Alice", java.util.Optional.of("alice@example.com"));
    var p2 = new Profile("Bob", java.util.Optional.empty());
    p1.email().ifPresent(e -> IO.println("Email: " + e));
    IO.println("Bob has email: " + p2.email().isPresent());
}
```

Optional components model nullable or missing values in records.  

## Record stream operations

```java
record Product(String name, double price) {}

void main() {

    var products = List.of(
        new Product("Apple", 1.5),
        new Product("Banana", 0.8),
        new Product("Cherry", 3.0)
    );
    
    var total = products.stream()
        .mapToDouble(Product::price)
        .sum();
    IO.println("Total: $" + total);
}
```

Process record collections using stream operations and method references.  

## Filtering records

```java
record Employee(String name, int age, double salary) {}

void main() {

    var employees = List.of(
        new Employee("Alice", 30, 75000),
        new Employee("Bob", 25, 65000),
        new Employee("Charlie", 35, 85000)
    );
    
    employees.stream()
        .filter(e -> e.salary() > 70000)
        .forEach(e -> IO.println(e.name() + ": $" + e.salary()));
}
```

Filters record streams based on component values and predicates.  

## Sorting records

```java
record Student(String name, int grade) {}

void main() {

    var students = List.of(
        new Student("Charlie", 85),
        new Student("Alice", 95),
        new Student("Bob", 90)
    );
    
    students.stream()
        .sorted((s1, s2) -> Integer.compare(s2.grade(), s1.grade()))
        .forEach(s -> IO.println(s.name() + ": " + s.grade()));
}
```

Sorts records using comparators based on component values.  

## Grouping records

```java
record Order(String product, String category) {}

void main() {

    var orders = List.of(
        new Order("Apple", "Fruit"),
        new Order("Carrot", "Vegetable"),
        new Order("Banana", "Fruit")
    );
    
    var grouped = orders.stream()
        .collect(java.util.stream.Collectors.groupingBy(Order::category));
    
    grouped.forEach((cat, items) -> 
        IO.println(cat + ": " + items.size() + " items")
    );
}
```

Groups records by component values using stream collectors.  

## Record with sealed hierarchy

```java
sealed interface Shape permits Circle, Square {}
record Circle(double radius) implements Shape {}
record Square(double side) implements Shape {}

void main() {

    Shape shape = new Circle(5.0);
    var area = switch (shape) {
        case Circle(double r) -> Math.PI * r * r;
        case Square(double s) -> s * s;
    };
    IO.println("Area: " + area);
}
```

Combines sealed interfaces with records for exhaustive type hierarchies.  

## Immutable data structure

```java
record Node(int value, Node next) {}

void main() {

    var list = new Node(1, new Node(2, new Node(3, null)));
    var current = list;
    while (current != null) {
        IO.println(current.value());
        current = current.next();
    }
}
```

Records create immutable linked structures with recursive components.  

## Record with computed property

```java
record Rectangle(double width, double height) {
    public double area() {
        return width * height;
    }
    
    public double perimeter() {
        return 2 * (width + height);
    }
}

void main() {

    var rect = new Rectangle(5, 3);
    IO.println("Area: " + rect.area());
    IO.println("Perimeter: " + rect.perimeter());
}
```

Adds methods to compute derived properties from record components.  

## Record builder pattern

```java
record Person(String name, int age, String email) {
    public static Builder builder() {
        return new Builder();
    }
    
    public static class Builder {
        private String name;
        private int age;
        private String email;
        
        public Builder name(String name) {
            this.name = name;
            return this;
        }
        
        public Builder age(int age) {
            this.age = age;
            return this;
        }
        
        public Builder email(String email) {
            this.email = email;
            return this;
        }
        
        public Person build() {
            return new Person(name, age, email);
        }
    }
}

void main() {

    var person = Person.builder()
        .name("Alice")
        .age(30)
        .email("alice@example.com")
        .build();
    IO.println(person);
}
```

Implements builder pattern with records for flexible object construction.  

## Record with custom equals

```java
record CaseInsensitiveString(String value) {
    @Override
    public boolean equals(Object obj) {
        if (obj instanceof CaseInsensitiveString other) {
            return value.equalsIgnoreCase(other.value);
        }
        return false;
    }
    
    @Override
    public int hashCode() {
        return value.toLowerCase().hashCode();
    }
}

void main() {

    var s1 = new CaseInsensitiveString("Hello");
    var s2 = new CaseInsensitiveString("HELLO");
    IO.println("Equal: " + s1.equals(s2));
}
```

Overrides equals and hashCode for custom equality semantics in records.  

## Record serialization

```java
record Data(String name, int value) implements java.io.Serializable {}

void main() {

    var data = new Data("test", 42);
    IO.println("Record: " + data);
    IO.println("Serializable: " + (data instanceof java.io.Serializable));
}
```

Records can implement Serializable for object serialization support.  

## Record with annotation

```java
record User(
    @Deprecated String username,
    String email
) {}

void main() {

    var user = new User("old_user", "user@example.com");
    IO.println("User: " + user.username());
}
```

Demonstrates applying annotations to individual record components.  

## Record copying with wither pattern

```java
record Point(int x, int y) {
    public Point withX(int newX) {
        return new Point(newX, y);
    }
    
    public Point withY(int newY) {
        return new Point(x, newY);
    }
}

void main() {

    var p1 = new Point(3, 4);
    var p2 = p1.withX(10);
    IO.println("Original: " + p1);
    IO.println("Modified: " + p2);
}
```

Creates modified copies of immutable records using wither methods.  

## Record with validation method

```java
record Email(String address) {
    public boolean isValid() {
        return address.contains("@") && address.contains(".");
    }
}

void main() {

    var email1 = new Email("user@example.com");
    var email2 = new Email("invalid");
    IO.println(email1.address() + " valid: " + email1.isValid());
    IO.println(email2.address() + " valid: " + email2.isValid());
}
```

Adds validation methods to check record component constraints.  

## Record comparison

```java
record Version(int major, int minor, int patch) 
    implements Comparable<Version> {
    
    @Override
    public int compareTo(Version other) {
        int result = Integer.compare(major, other.major);
        if (result == 0) {
            result = Integer.compare(minor, other.minor);
        }
        if (result == 0) {
            result = Integer.compare(patch, other.patch);
        }
        return result;
    }
}

void main() {

    var v1 = new Version(1, 2, 3);
    var v2 = new Version(1, 3, 0);
    IO.println("v1 < v2: " + (v1.compareTo(v2) < 0));
}
```

Implements Comparable interface for natural ordering of record instances.  

## Record with default values

```java
record Config(String host, int port) {
    public Config(String host) {
        this(host, 8080);
    }
    
    public Config() {
        this("localhost", 8080);
    }
}

void main() {

    var c1 = new Config();
    var c2 = new Config("example.com");
    IO.println("Default: " + c1);
    IO.println("Custom: " + c2);
}
```

Provides default values through additional constructors for convenience.  

## Record vs class comparison

```java
record RecordPerson(String name, int age) {}

class ClassPerson {
    private final String name;
    private final int age;
    
    public ClassPerson(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String name() { return name; }
    public int age() { return age; }
    
    @Override
    public boolean equals(Object obj) {
        if (obj instanceof ClassPerson other) {
            return name.equals(other.name) && age == other.age;
        }
        return false;
    }
    
    @Override
    public int hashCode() {
        return java.util.Objects.hash(name, age);
    }
    
    @Override
    public String toString() {
        return "ClassPerson[name=" + name + ", age=" + age + "]";
    }
}

void main() {

    var r = new RecordPerson("Alice", 30);
    var c = new ClassPerson("Alice", 30);
    
    IO.println("Record: " + r);
    IO.println("Class: " + c);
    IO.println("Record is more concise for immutable data carriers");
}
```

Compares records with traditional classes showing conciseness benefits.  

## Record with interface implementation

```java
interface Drawable {
    void draw();
}

record Circle(int x, int y, double radius) implements Drawable {
    @Override
    public void draw() {
        IO.println("Drawing circle at (" + x + "," + y + 
                   ") with radius " + radius);
    }
}

void main() {

    var circle = new Circle(10, 20, 5.0);
    circle.draw();
}
```

Records can implement interfaces with custom method implementations.  

## Record in concurrent collections

```java
record Event(String type, long timestamp) {}

void main() {

    var events = new java.util.concurrent.ConcurrentLinkedQueue<Event>();
    events.add(new Event("login", System.currentTimeMillis()));
    events.add(new Event("logout", System.currentTimeMillis()));
    
    events.forEach(e -> IO.println(e.type() + " at " + e.timestamp()));
}
```

Records work seamlessly in concurrent collections for thread-safe data.  

## Record with multiple validations

```java
record Range(int min, int max) {
    public Range {
        if (min > max) {
            throw new IllegalArgumentException(
                "min must be <= max: " + min + " > " + max
            );
        }
        if (min < 0) {
            throw new IllegalArgumentException("min cannot be negative");
        }
    }
    
    public boolean contains(int value) {
        return value >= min && value <= max;
    }
}

void main() {

    var range = new Range(1, 10);
    IO.println("Contains 5: " + range.contains(5));
    IO.println("Contains 15: " + range.contains(15));
}
```

Demonstrates complex validation logic in compact constructor with checks.  

## Record with factory methods

```java
record Color(int r, int g, int b) {
    public static Color red() {
        return new Color(255, 0, 0);
    }
    
    public static Color green() {
        return new Color(0, 255, 0);
    }
    
    public static Color blue() {
        return new Color(0, 0, 255);
    }
    
    public static Color rgb(int r, int g, int b) {
        return new Color(r, g, b);
    }
}

void main() {

    var red = Color.red();
    var custom = Color.rgb(128, 128, 128);
    IO.println("Red: " + red);
    IO.println("Custom: " + custom);
}
```

Uses static factory methods for common record instances and named creation.  

## Complex record hierarchy

```java
sealed interface Result<T> permits Success, Failure {}
record Success<T>(T value) implements Result<T> {}
record Failure<T>(String error) implements Result<T> {}

void main() {

    Result<Integer> r1 = new Success<>(42);
    Result<Integer> r2 = new Failure<>("Error occurred");
    
    var message = switch (r1) {
        case Success<Integer>(Integer val) -> "Success: " + val;
        case Failure<Integer>(String err) -> "Failure: " + err;
    };
    IO.println(message);
}
```

Combines sealed interfaces, generics, and records for type-safe results.  

## Record with transformation method

```java
record Temperature(double celsius) {
    public Temperature toFahrenheit() {
        return new Temperature((celsius * 9 / 5) + 32);
    }
    
    public Temperature toKelvin() {
        return new Temperature(celsius + 273.15);
    }
}

void main() {

    var celsius = new Temperature(25);
    var fahrenheit = celsius.toFahrenheit();
    IO.println("25°C = " + fahrenheit.celsius() + "°F");
}
```

Transformation methods create new record instances with converted values.  

## Record with Map transformation

```java
record Person(String name, int age) {}

void main() {

    var people = List.of(
        new Person("Alice", 30),
        new Person("Bob", 25)
    );
    
    var nameMap = people.stream()
        .collect(java.util.stream.Collectors.toMap(
            Person::name,
            Person::age
        ));
    
    IO.println(nameMap);
}
```

Transforms record collections into maps using stream collectors.  

## Record with reduce operation

```java
record Transaction(String id, double amount) {}

void main() {

    var transactions = List.of(
        new Transaction("T1", 100.50),
        new Transaction("T2", 250.75),
        new Transaction("T3", 75.25)
    );
    
    var total = transactions.stream()
        .map(Transaction::amount)
        .reduce(0.0, Double::sum);
    
    IO.println("Total: $" + total);
}
```

Uses reduce operations to aggregate values from record components.  

## Record with flatMap

```java
record Department(String name, List<String> employees) {}

void main() {

    var departments = List.of(
        new Department("IT", List.of("Alice", "Bob")),
        new Department("HR", List.of("Charlie", "Diana"))
    );
    
    departments.stream()
        .flatMap(d -> d.employees().stream())
        .forEach(IO::println);
}
```

FlatMaps nested collections from record components into single stream.  

## Record with partitioning

```java
record Score(String name, int points) {}

void main() {

    var scores = List.of(
        new Score("Alice", 85),
        new Score("Bob", 92),
        new Score("Charlie", 78)
    );
    
    var partitioned = scores.stream()
        .collect(java.util.stream.Collectors.partitioningBy(
            s -> s.points() >= 80
        ));
    
    IO.println("Passed: " + partitioned.get(true).size());
    IO.println("Failed: " + partitioned.get(false).size());
}
```

Partitions record streams into groups based on predicate conditions.  

## Record with reflection

```java
record Data(String name, int value) {}

void main() {

    var data = new Data("test", 42);
    var components = data.getClass().getRecordComponents();
    
    for (var comp : components) {
        IO.println("Component: " + comp.getName() + 
                   " (" + comp.getType().getSimpleName() + ")");
    }
}
```

Inspects record structure at runtime using Java reflection API.