# Java Conditionals

This document demonstrates various conditional logic patterns in modern Java,  
using compact source files and Java 25 features.  

## Basic if statement

```java
void main() {

    var temperature = 25;
    if (temperature > 20) {
        IO.println("It's a warm day!");
    }
}
```

Demonstrates a simple if statement that checks a numeric condition.  

## If-else branching

```java
void main() {

    var age = 16;
    if (age >= 18) {
        IO.println("You are an adult");
    } else {
        IO.println("You are a minor");
    }
}
```

Shows basic if-else branching based on a boolean condition.  

## Multiple conditions with else if

```java
void main() {

    var score = 85;
    if (score >= 90) {
        IO.println("Grade: A");
    } else if (score >= 80) {
        IO.println("Grade: B");
    } else if (score >= 70) {
        IO.println("Grade: C");
    } else {
        IO.println("Grade: D or F");
    }
}
```

Demonstrates multiple conditional branches with else if for range checking.  

## Boolean logical operators

```java
void main() {

    var age = 25;
    var hasLicense = true;
    
    if (age >= 18 && hasLicense) {
        IO.println("You can drive");
    } else {
        IO.println("You cannot drive");
    }
}
```

Shows the use of logical AND operator in conditional expressions.  

## Logical OR operator

```java
void main() {

    var day = "Saturday";
    
    if (day.equals("Saturday") || day.equals("Sunday")) {
        IO.println("It's the weekend!");
    } else {
        IO.println("It's a weekday");
    }
}
```

Demonstrates the logical OR operator for checking multiple conditions.  

## Switch statement

```java
void main() {

    var dayNumber = 3;
    
    switch (dayNumber) {
        case 1 -> IO.println("Monday");
        case 2 -> IO.println("Tuesday");
        case 3 -> IO.println("Wednesday");
        case 4 -> IO.println("Thursday");
        case 5 -> IO.println("Friday");
        case 6, 7 -> IO.println("Weekend");
        default -> IO.println("Invalid day");
    }
}
```

Shows modern switch statement with arrow syntax and multiple case values.  

## Switch expression

```java
void main() {

    var month = 4;
    
    var season = switch (month) {
        case 12, 1, 2 -> "Winter";
        case 3, 4, 5 -> "Spring";
        case 6, 7, 8 -> "Summer";
        case 9, 10, 11 -> "Fall";
        default -> "Unknown";
    };
    
    IO.println("Season: " + season);
}
```

Demonstrates switch expression that returns a value directly.  

## Switch with yield

```java
void main() {

    var score = 85;
    
    var grade = switch (score / 10) {
        case 10, 9 -> "A";
        case 8 -> "B";
        case 7 -> "C";
        case 6 -> "D";
        default -> {
            if (score >= 0) {
                yield "F";
            } else {
                yield "Invalid";
            }
        }
    };
    
    IO.println("Grade: " + grade);
}
```

Shows switch expression with yield keyword for complex cases.  

## Switch on strings

```java
void main() {

    var fruit = "apple";
    
    var color = switch (fruit) {
        case "apple" -> "red";
        case "banana" -> "yellow";
        case "orange" -> "orange";
        case "grape" -> "purple";
        default -> "unknown";
    };
    
    IO.println("Color: " + color);
}
```

Demonstrates switch statement working with string values.  

## Switch with null handling

```java
void main() {

    String value = null;
    
    var result = switch (value) {
        case null -> "Value is null";
        case "hello" -> "Greeting";
        case "bye" -> "Farewell";
        default -> "Other: " + value;
    };
    
    IO.println(result);
}
```

Shows modern switch handling null values explicitly.  

## Ternary operator

```java
void main() {

    var number = 15;
    var result = (number % 2 == 0) ? "even" : "odd";
    IO.println(number + " is " + result);
}
```

Demonstrates the ternary conditional operator for concise if-else logic.  

## Nested ternary operators

```java
void main() {

    var score = 85;
    var grade = score >= 90 ? "A" : 
                score >= 80 ? "B" : 
                score >= 70 ? "C" : "F";
    IO.println("Grade: " + grade);
}
```

Shows nested ternary operators for multiple conditions (use sparingly).  

## Negation operator

```java
void main() {

    var isRaining = false;
    
    if (!isRaining) {
        IO.println("You don't need an umbrella");
    } else {
        IO.println("Take an umbrella");
    }
}
```

Demonstrates the logical NOT operator in conditional expressions.  

## Complex boolean expressions

```java
void main() {

    var temperature = 25;
    var humidity = 60;
    var isSunny = true;
    
    if ((temperature > 20 && temperature < 30) && 
        (humidity < 70) && isSunny) {
        IO.println("Perfect weather for outdoor activities!");
    } else {
        IO.println("Maybe stay indoors");
    }
}
```

Shows combining multiple boolean conditions with proper grouping.  

## Short-circuit evaluation

```java
void main() {

    String text = null;
    
    if (text != null && text.length() > 0) {
        IO.println("Text: " + text);
    } else {
        IO.println("Text is null or empty");
    }
}
```

Demonstrates short-circuit evaluation to avoid NullPointerException.  

## Pattern matching for instanceof

```java
void main() {

    Object obj = "Hello, World!";
    
    if (obj instanceof String s) {
        IO.println("String length: " + s.length());
        IO.println("Uppercase: " + s.toUpperCase());
    } else {
        IO.println("Not a string");
    }
}
```

Shows pattern matching with instanceof and type pattern variable.  

## Pattern matching with multiple types

```java
void main() {

    Object value = 42;
    
    if (value instanceof Integer i) {
        IO.println("Integer: " + i * 2);
    } else if (value instanceof String s) {
        IO.println("String: " + s.toUpperCase());
    } else if (value instanceof Double d) {
        IO.println("Double: " + d * 2.0);
    } else {
        IO.println("Unknown type");
    }
}
```

Demonstrates pattern matching across multiple type checks.  

## Pattern matching in switch

```java
void main() {

    Object obj = 100;
    
    var result = switch (obj) {
        case Integer i -> "Integer: " + i;
        case String s -> "String: " + s;
        case Double d -> "Double: " + d;
        case null -> "Null value";
        default -> "Unknown type";
    };
    
    IO.println(result);
}
```

Shows pattern matching integrated with switch expressions.  

## Guarded patterns

```java
void main() {

    Object obj = 15;
    
    var result = switch (obj) {
        case Integer i when i > 10 -> "Large integer: " + i;
        case Integer i when i > 0 -> "Small integer: " + i;
        case Integer i -> "Zero or negative: " + i;
        default -> "Not an integer";
    };
    
    IO.println(result);
}
```

Demonstrates guarded patterns with when clause in switch expressions.  

## Record pattern matching

```java
record Point(int x, int y) {}

void main() {

    Object obj = new Point(5, 10);
    
    if (obj instanceof Point(int x, int y)) {
        IO.println("Point coordinates: x=" + x + ", y=" + y);
        IO.println("Sum: " + (x + y));
    }
}
```

Shows pattern matching with record patterns for deconstruction.  

## Conditionals with collections

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    
    if (numbers.isEmpty()) {
        IO.println("List is empty");
    } else if (numbers.size() == 1) {
        IO.println("List has one element: " + numbers.get(0));
    } else {
        IO.println("List has " + numbers.size() + " elements");
    }
}
```

Demonstrates conditional logic based on collection properties.  

## Conditionals in streams

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var evens = numbers.stream()
        .filter(n -> n % 2 == 0)
        .toList();
    
    var odds = numbers.stream()
        .filter(n -> n % 2 != 0)
        .toList();
    
    IO.println("Even numbers: " + evens);
    IO.println("Odd numbers: " + odds);
}
```

Shows using conditional logic with stream filtering operations.  

## Map with conditional logic

```java
void main() {

    var scores = Map.of("Alice", 85, "Bob", 92, "Charlie", 78);
    
    scores.forEach((name, score) -> {
        var grade = score >= 90 ? "A" : 
                    score >= 80 ? "B" : 
                    score >= 70 ? "C" : "F";
        IO.println(name + ": " + grade);
    });
}
```

Demonstrates conditional logic within map iteration and processing.  

## Guard clauses

```java
void main() {

    var age = -5;
    
    if (age < 0) {
        IO.println("Invalid age");
        return;
    }
    
    if (age < 18) {
        IO.println("Minor");
        return;
    }
    
    IO.println("Adult");
}
```

Shows guard clause pattern for early returns and cleaner code flow.  

## Nested conditionals

```java
void main() {

    var hasAccount = true;
    var isVerified = true;
    var balance = 100;
    
    if (hasAccount) {
        if (isVerified) {
            if (balance > 0) {
                IO.println("You can make a purchase");
            } else {
                IO.println("Insufficient balance");
            }
        } else {
            IO.println("Account not verified");
        }
    } else {
        IO.println("No account found");
    }
}
```

Demonstrates nested conditional structures (prefer flattening when possible).  

## Conditionals with optional values

```java
void main() {

    var values = List.of(1, 2, 3, 4, 5);
    
    var max = values.stream()
        .max(Integer::compareTo);
    
    if (max.isPresent()) {
        IO.println("Maximum value: " + max.get());
    } else {
        IO.println("No values found");
    }
}
```

Shows conditional handling of Optional values from stream operations.  

## Conditional variable initialization

```java
void main() {

    var temperature = 18;
    
    var clothing = if (temperature < 10) {
        yield "heavy coat";
    } else if (temperature < 20) {
        yield "light jacket";
    } else {
        yield "t-shirt";
    };
    
    IO.println("Wear: " + clothing);
}
```

Demonstrates using conditionals for variable initialization with yield.  

## Range checking with conditionals

```java
void main() {

    var value = 50;
    
    if (value >= 0 && value <= 25) {
        IO.println("Low range");
    } else if (value > 25 && value <= 75) {
        IO.println("Medium range");
    } else if (value > 75 && value <= 100) {
        IO.println("High range");
    } else {
        IO.println("Out of range");
    }
}
```

Shows conditional logic for checking numeric ranges effectively.  

## Conditional execution in loops

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    for (var num : numbers) {
        if (num % 2 == 0) {
            IO.println(num + " is even");
        } else {
            IO.println(num + " is odd");
        }
        
        if (num == 5) {
            IO.println("Found 5! Stopping...");
            break;
        }
    }
}
```

Demonstrates conditional logic within loops with break statements.  

## Combining switch and pattern matching

```java
void main() {

    Object[] values = {42, "hello", 3.14, true, null};
    
    for (var value : values) {
        var description = switch (value) {
            case null -> "null value";
            case Integer i when i < 0 -> "negative integer";
            case Integer i when i == 0 -> "zero";
            case Integer i -> "positive integer: " + i;
            case String s when s.isEmpty() -> "empty string";
            case String s -> "string: " + s;
            case Double d -> "double: " + d;
            case Boolean b -> "boolean: " + b;
            default -> "unknown type";
        };
        
        IO.println(description);
    }
}
```

Demonstrates combining switch expressions with pattern matching and guards  
for comprehensive type and value checking.  
