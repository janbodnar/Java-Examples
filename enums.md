
# Java Enum Type

This document provides comprehensive examples demonstrating the use of enum  
types in Java. An enum type is a special data type that defines a fixed set  
of named constants, providing type safety and improved code readability.  

Enums are particularly useful when representing a fixed collection of related  
constants such as days of the week, seasons, directions, or status codes.  
Unlike primitive integers, enums enforce compile-time type safety, ensuring  
that variables can only hold predefined values. This prevents invalid values  
from being assigned and makes code more self-documenting and maintainable.  

Java enums are more powerful than enums in many other languages. They can  
have fields, constructors, and methods, making them full-fledged classes with  
special properties. Enums can implement interfaces, contain abstract methods,  
and even have constant-specific method implementations. This flexibility  
allows enums to encapsulate both data and behavior related to each constant.  

The `enum` keyword is used to define an enumeration in Java. By convention,  
enum constants are written in uppercase letters. Each enum type implicitly  
extends `java.lang.Enum` and cannot extend any other class. However, enums  
can implement multiple interfaces, providing great flexibility in design.  

## Basic enum definition

This example demonstrates defining and using a simple enum type.

```java
enum Day {
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}

void main() {

    var day = Day.MONDAY;

    if (day == Day.MONDAY) {
        IO.println("It is Monday");
    }

    IO.println(day);

    for (var d : Day.values()) {
        IO.println(d);
    }
}
```
The `Day` enum defines seven constants representing days of the week. The  
`values` method returns an array of all enum constants in declaration order,  
allowing iteration with an enhanced for loop. Enum constants can be compared  
using the `==` operator since each constant is a singleton instance.  


## Enum with fields and constructor

This example shows how to associate values with enum constants.

```java
enum Season {
    SPRING(10),
    SUMMER(20),
    AUTUMN(30),
    WINTER(40);

    private int value;

    Season(int value) {
        this.value = value;
    }

    int getValue() {
        return value;
    }
}

void main() {

    for (var season : Season.values()) {
        IO.println(season + " " + season.getValue());
    }
}
```
Each enum constant can be initialized with specific values by defining a  
constructor. The constructor is private by default and is called when the  
enum constants are declared. This allows each constant to have its own  
associated data, making enums useful for representing complex constant sets.  


## Enum with custom methods

This example demonstrates adding custom methods to an enum type.

```java
enum Coin {
    HEADS,
    TAILS;

    static Coin toss() {
        var rand = new Random();
        var values = Coin.values();
        return values[rand.nextInt(values.length)];
    }
}

void main() {

    for (int i = 1; i <= 15; i++) {
        IO.print(Coin.toss() + " ");
    }
    
    IO.println();
}
```
Enums can define static methods that operate on the enum type itself. The  
`toss` method randomly selects one of the two coin values using Java's  
`Random` class. This demonstrates how enums can encapsulate behavior related  
to their constants, making the code more object-oriented and maintainable.  


## Enum with switch expressions

This example demonstrates using enums with modern switch expressions.

```java
enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER;

    static Season randomSeason() {
        var random = new Random();
        var values = Season.values();
        return values[random.nextInt(values.length)];
    }
}

void main() {

    var season = Season.randomSeason();

    var msg = switch (season) {
        case SPRING -> "Spring";
        case SUMMER -> "Summer";
        case AUTUMN -> "Autumn";
        case WINTER -> "Winter";
    };

    IO.println(msg);
}
```
Switch expressions work seamlessly with enums. Since the compiler knows all  
possible enum constants at compile time, the switch is exhaustive without  
needing a `default` case. This makes the code safer and more maintainable,  
as adding new enum constants will cause a compilation error if not handled.  

## Enum with instance methods

This example shows how to add instance methods to enum constants.

```java
enum TrafficLight {
    RED,
    YELLOW,
    GREEN;

    boolean canGo() {
        return this == GREEN;
    }

    boolean shouldStop() {
        return this == RED;
    }

    boolean shouldSlowDown() {
        return this == YELLOW;
    }
}

void main() {

    var light = TrafficLight.RED;
    IO.println(light + " - Can go: " + light.canGo());
    IO.println(light + " - Should stop: " + light.shouldStop());
    
    light = TrafficLight.GREEN;
    IO.println(light + " - Can go: " + light.canGo());
}
```
Instance methods in enums allow each constant to have behavior based on its  
identity. The methods use the `this` keyword to compare against specific  
constants. This pattern is useful for creating enums with logic that depends  
on which constant is being used, improving code readability and organization.  

## Enum implementing interfaces

This example demonstrates how enums can implement interfaces.

```java
interface Describable {
    String getDescription();
}

enum Priority implements Describable {
    LOW {
        public String getDescription() {
            return "Low priority - can wait";
        }
    },
    MEDIUM {
        public String getDescription() {
            return "Medium priority - schedule soon";
        }
    },
    HIGH {
        public String getDescription() {
            return "High priority - urgent attention needed";
        }
    };
}

void main() {

    for (var priority : Priority.values()) {
        IO.println(priority + ": " + priority.getDescription());
    }
}
```
Enums can implement interfaces just like regular classes. Each constant can  
provide its own implementation of interface methods, allowing for  
constant-specific behavior. This is a powerful feature that enables polymorphic  
behavior while maintaining the type safety and fixed nature of enums.  

## Enum with abstract methods

This example shows enums with abstract methods for constant-specific behavior.

```java
enum Operation {
    PLUS {
        double apply(double x, double y) {
            return x + y;
        }
    },
    MINUS {
        double apply(double x, double y) {
            return x - y;
        }
    },
    MULTIPLY {
        double apply(double x, double y) {
            return x * y;
        }
    },
    DIVIDE {
        double apply(double x, double y) {
            return x / y;
        }
    };

    abstract double apply(double x, double y);
}

void main() {

    var x = 10.0;
    var y = 5.0;
    
    for (var op : Operation.values()) {
        IO.println(x + " " + op + " " + y + " = " + op.apply(x, y));
    }
}
```
Enums can declare abstract methods that each constant must implement. This  
pattern is known as the constant-specific method implementation. It allows  
each enum constant to have its own unique behavior while sharing a common  
interface. This is particularly useful for implementing the Strategy pattern.  

## Using EnumSet

This example demonstrates the efficient `EnumSet` collection for enums.

```java
enum Weekday {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

void main() {

    var workdays = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);
    var weekend = EnumSet.of(Weekday.SATURDAY, Weekday.SUNDAY);
    var allDays = EnumSet.allOf(Weekday.class);

    IO.println("Workdays: " + workdays);
    IO.println("Weekend: " + weekend);
    IO.println("All days: " + allDays);
    
    IO.println("Friday is workday: " + workdays.contains(Weekday.FRIDAY));
    IO.println("Saturday is workday: " + workdays.contains(Weekday.SATURDAY));
}
```
`EnumSet` is a specialized `Set` implementation designed for use with enum  
types. It is extremely efficient, using bit vectors internally for compact  
storage and fast operations. The class provides factory methods like `range`,  
`of`, and `allOf` for convenient set creation with enum constants.  

## Using EnumMap

This example shows the efficient `EnumMap` collection for mapping enums to values.

```java
enum Size {
    SMALL, MEDIUM, LARGE, EXTRA_LARGE
}

void main() {

    var prices = new EnumMap<Size, Double>(Size.class);
    prices.put(Size.SMALL, 9.99);
    prices.put(Size.MEDIUM, 12.99);
    prices.put(Size.LARGE, 15.99);
    prices.put(Size.EXTRA_LARGE, 18.99);

    for (var entry : prices.entrySet()) {
        IO.println(entry.getKey() + ": $" + entry.getValue());
    }
    
    IO.println("Medium price: $" + prices.get(Size.MEDIUM));
}
```
`EnumMap` is a specialized `Map` implementation for enum keys. It is more  
efficient than regular hash maps because it uses an array internally, indexed  
by enum ordinal values. All keys in an `EnumMap` must come from the same enum  
type, specified when the map is created. This provides excellent performance.  

## Enum with complex fields

This example demonstrates enums with multiple fields and computed properties.

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
    
    double surfaceWeight(double otherMass) {
        return otherMass * surfaceGravity();
    }
}

void main() {

    var earthWeight = 75.0;
    var mass = earthWeight / Planet.EARTH.surfaceGravity();
    
    for (var planet : Planet.values()) {
        IO.println("Weight on " + planet + ": " + 
                   String.format("%.2f", planet.surfaceWeight(mass)) + " kg");
    }
}
```
This example shows how enums can contain multiple fields and methods that  
perform calculations using those fields. Each constant stores its own mass  
and radius, and the methods compute gravity and weight based on these values.  
This demonstrates how enums can represent complex, constant objects with both  
state and behavior, making them powerful tools for domain modeling.  
