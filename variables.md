# Java Variables

This document demonstrates 30 progressively advanced Java examples showcasing  
different ways to declare, assign, and use variables in Java, utilizing  
modern Java 25 features.  

## Basic integer variable

```java
void main() {
    var count = 42;
    IO.println("Count: " + count);
}
```

Declares an integer variable using type inference with `var`.  

## Double precision variable

```java
void main() {
    var price = 19.99;
    IO.println("Price: $" + price);
}
```

Shows a double variable for decimal numbers with type inference.  

## Boolean variable

```java
void main() {
    var isActive = true;
    IO.println("Active: " + isActive);
}
```

Demonstrates a boolean variable for true/false values.  

## Character variable

```java
void main() {
    var initial = 'J';
    IO.println("Initial: " + initial);
}
```

Shows a character variable storing a single character.  

## String variable

```java
void main() {
    var name = "Java";
    IO.println("Language: " + name);
}
```

Declares a String variable to store text data.  

## Multiple variable declarations

```java
void main() {
    var x = 10;
    var y = 20;
    var z = 30;
    IO.println("Sum: " + (x + y + z));
}
```

Demonstrates declaring multiple variables of the same type.  

## Variable reassignment

```java
void main() {
    var counter = 0;
    IO.println("Initial: " + counter);
    counter = 10;
    IO.println("Updated: " + counter);
}
```

Shows how mutable variables can be reassigned new values.  

## Final variable

```java
void main() {
    final var maxAttempts = 3;
    IO.println("Maximum attempts: " + maxAttempts);
}
```

Demonstrates a constant variable using `final` that cannot be reassigned.  

## Compound assignment

```java
void main() {
    var total = 100;
    total += 50;
    total -= 20;
    total *= 2;
    IO.println("Final total: " + total);
}
```

Shows compound assignment operators for concise value updates.  

## Type inference with collections

```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    IO.println("Numbers: " + numbers);
}
```

Demonstrates `var` with collection types using implicit imports.  

## Map variable

```java
void main() {
    var scores = Map.of("Alice", 95, "Bob", 87, "Carol", 92);
    IO.println("Scores: " + scores);
}
```

Shows a Map variable storing key-value pairs with type inference.  

## Block scope variable

```java
void main() {
    var outer = "outer scope";
    {
        var inner = "inner scope";
        IO.println(inner);
    }
    IO.println(outer);
}
```

Demonstrates block-level scope where inner variables are isolated.  

## Variable shadowing

```java
void main() {
    var value = 10;
    IO.println("Outer: " + value);
    {
        var value = 20;
        IO.println("Inner: " + value);
    }
    IO.println("Outer again: " + value);
}
```

Shows variable shadowing where inner scope variables hide outer ones.  

## Loop variable scope

```java
void main() {
    for (var i = 0; i < 3; i++) {
        var loopVar = i * 10;
        IO.println("Loop var: " + loopVar);
    }
}
```

Demonstrates loop variable scope where variables exist only within the loop.  

## Conditional variable initialization

```java
void main() {
    var temperature = 25;
    var status = (temperature > 20) ? "warm" : "cold";
    IO.println("Status: " + status);
}
```

Shows conditional (ternary) operator for variable initialization.  

## Pattern matching variable

```java
void main() {
    Object obj = "Hello";
    if (obj instanceof String s) {
        IO.println("String length: " + s.length());
    }
}
```

Demonstrates pattern matching with instanceof creating a type-specific  
variable.  

## Multiple types with var

```java
void main() {
    var text = "Java";
    var number = 25;
    var decimal = 3.14;
    var flag = true;
    IO.println(text + " " + number + " " + decimal + " " + flag);
}
```

Shows `var` used with different types in the same scope.  

## Mutable ArrayList variable

```java
void main() {
    var items = new ArrayList<String>();
    items.add("first");
    items.add("second");
    IO.println("Items: " + items);
}
```

Demonstrates a mutable ArrayList variable that can be modified.  

## Immutable collection variable

```java
void main() {
    var colors = List.of("red", "green", "blue");
    IO.println("Colors: " + colors);
}
```

Shows an immutable collection created with `List.of`.  

## Variable in enhanced switch

```java
void main() {
    var day = "Monday";
    var type = switch (day) {
        case "Saturday", "Sunday" -> "Weekend";
        default -> "Weekday";
    };
    IO.println(day + " is a " + type);
}
```

Demonstrates variable assignment from a switch expression.  

## Numeric type variables

```java
void main() {
    var byteVal = (byte) 127;
    var shortVal = (short) 32000;
    var longVal = 9876543210L;
    IO.println(byteVal + " " + shortVal + " " + longVal);
}
```

Shows different numeric primitive types with explicit casting where needed.  

## String formatting with variables

```java
void main() {
    var name = "Alice";
    var age = 30;
    var message = "Name: " + name + ", Age: " + age;
    IO.println(message);
}
```

Demonstrates building formatted strings with multiple variables.  

## Variable increment and decrement

```java
void main() {
    var counter = 5;
    IO.println("Original: " + counter);
    IO.println("Post-increment: " + counter++);
    IO.println("After: " + counter);
    IO.println("Pre-decrement: " + --counter);
}
```

Shows increment and decrement operators with pre and post variations.  

## Default values and initialization

```java
void main() {
    var initialized = 10;
    var defaultInt = 0;
    var defaultBool = false;
    var defaultStr = "";
    IO.println(initialized + " " + defaultInt + " " + defaultBool + " " + 
        defaultStr);
}
```

Demonstrates explicit initialization versus default values.  

## Variable with Math operations

```java
void main() {
    var radius = 5.0;
    var area = Math.PI * radius * radius;
    IO.println("Circle area: " + area);
}
```

Shows variables used with Math operations and constants.  

## HashMap variable with mutations

```java
void main() {
    var map = new HashMap<String, Integer>();
    map.put("apple", 1);
    map.put("banana", 2);
    map.put("cherry", 3);
    IO.println("Map: " + map);
}
```

Demonstrates a mutable HashMap variable with dynamic additions.  

## Variable type casting

```java
void main() {
    var doubleVal = 3.14;
    var intVal = (int) doubleVal;
    IO.println("Double: " + doubleVal + ", Int: " + intVal);
}
```

Shows explicit type casting when assigning between numeric types.  

## Multi-value swap

```java
void main() {
    var a = 5;
    var b = 10;
    IO.println("Before: a=" + a + ", b=" + b);
    var temp = a;
    a = b;
    b = temp;
    IO.println("After: a=" + a + ", b=" + b);
}
```

Demonstrates swapping variable values using a temporary variable.  

## Computed variable values

```java
void main() {
    var base = 10;
    var exponent = 3;
    var result = Math.pow(base, exponent);
    IO.println(base + " raised to " + exponent + " = " + result);
}
```

Shows variables computed from other variables using methods.  

## Variable in record pattern

```java
record Point(int x, int y) {}

void main() {
    var point = new Point(10, 20);
    if (point instanceof Point(var x, var y)) {
        IO.println("Coordinates: x=" + x + ", y=" + y);
    }
}
```

Demonstrates pattern matching with records extracting values into variables.  
