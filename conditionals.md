# Java Conditionals

This document demonstrates various conditional logic patterns in modern Java,  
using compact source files and Java 25 features.  

## Basic if statement
This example shows a simple `if` statement that executes code based on a condition.
```java
void main() {

    var temperature = 25;
    if (temperature > 20) {
        IO.println("It's a warm day!");
    }
}
```

The code inside the `if` block runs only if the `temperature` is greater than 20.
This is the most fundamental way to control program flow, allowing code to
react differently to various conditions.

## If-else branching
This example demonstrates an `if-else` statement to handle two possible outcomes.
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

If the condition `age >= 18` is true, the first block executes; otherwise,
the `else` block runs. This structure ensures that one of the two blocks
is always executed, providing a clear binary choice.

## Multiple conditions with else if
This example shows how to chain multiple conditions using `else if`.
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

This structure evaluates conditions sequentially until one is found to be true.
It is useful for implementing logic with multiple distinct cases, such as
assigning grades based on a score.

## Boolean logical operators
This example demonstrates combining conditions with the logical AND (`&&`) operator.
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

The `&&` operator requires both conditions to be true for the entire
expression to be true. This is useful for situations where multiple criteria
must be met simultaneously.

## Logical OR operator
This example shows how to use the logical OR (`||`) operator to check for multiple possibilities.
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

The `||` operator returns true if at least one of the conditions is met.
This is ideal for checking if a value matches any of several possibilities,
such as identifying if a day is part of the weekend.

## Switch statement
This example demonstrates a modern `switch` statement with arrow syntax.
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

The arrow syntax (`->`) provides a concise way to handle different cases
without fall-through, making the code safer and easier to read.
Multiple values can be grouped in a single case, such as for the weekend.

## Switch expression
This example shows how a `switch` expression can return a value.
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

Unlike a `switch` statement, a `switch` expression evaluates to a single value,
which can be assigned to a variable. This makes it a powerful tool for
conditional assignments in a clean and readable way.

## Switch with yield
This example demonstrates using `yield` in a `switch` expression for more complex logic.
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

The `yield` keyword is used to return a value from a block within a `switch`
expression. This is necessary when a case requires more than a single
expression to compute its result.

## Switch on strings
This example shows how a `switch` statement can be used with `String` values.
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

`switch` statements can directly compare strings, making them a convenient
alternative to a chain of `if-else if` statements for string-based logic.
This results in cleaner and more intuitive code.

## Switch with null handling
This example demonstrates how modern `switch` can handle `null` values explicitly.
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

A `case null` label allows `switch` expressions to safely handle `null` inputs
without throwing a `NullPointerException`. This feature makes conditional
logic more robust and expressive.

## Ternary operator
This example shows the ternary operator for concise conditional assignment.
```java
void main() {

    var number = 15;
    var result = (number % 2 == 0) ? "even" : "odd";
    IO.println(number + " is " + result);
}
```

The ternary operator (`? :`) is a compact alternative to a simple `if-else`
statement that assigns a value to a variable. It evaluates a boolean condition
and chooses one of two expressions to execute.

## Nested ternary operators
This example demonstrates nesting ternary operators for multi-level conditions.
```java
void main() {

    var score = 85;
    var grade = score >= 90 ? "A" : 
                score >= 80 ? "B" : 
                score >= 70 ? "C" : "F";
    IO.println("Grade: " + grade);
}
```

While possible, nesting ternary operators can quickly become difficult to
read and maintain. They are best used for simple, clear-cut conditions;
for more complex logic, `if-else` or `switch` is often preferred.

## Negation operator
This example shows the logical NOT (`!`) operator to invert a boolean expression.
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

The `!` operator flips a boolean value from `true` to `false` or vice versa.
It is useful for checking if a condition is not met, making the code's
intent clearer than a comparison like `isRaining == false`.

## Complex boolean expressions
This example demonstrates combining multiple conditions with grouping.
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

Parentheses are used to group logical expressions, ensuring they are
evaluated in the intended order. This is crucial for building complex
conditions that accurately reflect the desired logic.

## Short-circuit evaluation
This example shows how short-circuiting avoids potential errors.
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

In a logical AND (`&&`) expression, if the first operand is false, the second
is not evaluated. This "short-circuit" behavior is essential for preventing
errors like a `NullPointerException` when checking object properties.

## Pattern matching for instanceof
This example demonstrates modern `instanceof` with pattern matching.
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

Pattern matching with `instanceof` checks the type of an object and, if it
matches, assigns it to a new variable (`s`). This avoids the need for an
explicit cast, making the code more concise and safe.

## Pattern matching with multiple types
This example shows using pattern matching across several `if-else if` checks.
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

This pattern allows for cleanly handling different data types. Each block
can safely use the type-specific variable, as the compiler guarantees the
cast is valid within that scope.

## Pattern matching in switch
This example integrates pattern matching directly into a `switch` expression.
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

Using pattern matching in `switch` provides a highly expressive and readable
way to handle different types. It combines the type check and variable binding
in a single, elegant structure.

## Guarded patterns
This example demonstrates guarded patterns with a `when` clause in a `switch`.
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

A `when` clause adds a secondary condition to a `case` label, allowing for
more refined pattern matching. This enables `switch` to handle complex logic
that depends on both the type and the properties of a value.

## Record pattern matching
This example shows how to deconstruct records using pattern matching.
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

Record patterns allow you to match an object's type and simultaneously extract
its components into local variables. This simplifies working with immutable
data carriers, making the code more declarative.

## Conditionals with collections
This example demonstrates conditional logic based on collection properties.
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

You can control program flow by checking properties of collections, such as
whether a list is empty or its size. This is a common pattern for handling
data collections safely and effectively.

## Conditionals in streams
This example shows using conditional logic within stream operations.
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

The `filter` operation in streams takes a predicate—a function that returns
a boolean—to selectively process elements. This allows for powerful,
declarative data processing based on conditional logic.

## Map with conditional logic
This example demonstrates applying conditional logic during map iteration.
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

Conditional logic can be used inside a `forEach` loop to process map entries
differently based on their values. Here, a ternary operator is used to
assign a grade for each student's score.

## Guard clauses
This example illustrates the guard clause pattern for cleaner code.
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

Guard clauses are `if` statements at the beginning of a function that check
for preconditions and exit early if they are not met. This pattern reduces
nesting and makes the main logic path clearer.

## Nested conditionals
This example demonstrates nested `if` statements for multi-level checks.
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

Nesting conditionals allows for complex, hierarchical logic, but it can
also make code harder to read. It is often better to refactor deep nesting
into guard clauses or separate functions.

## Conditionals with optional values
This example shows how to handle `Optional` values conditionally.
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

The `Optional` type is a container that may or may not hold a value. Using
`isPresent()` allows you to safely check for a value before attempting to
access it, preventing `NullPointerException`.

## Conditional variable initialization
This example demonstrates initializing a variable using a conditional expression.
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

This feature is not yet available in Java. The example shows a hypothetical
use of an `if` expression to assign a value, which would be a more powerful
alternative to the ternary operator for complex initializations.

## Range checking with conditionals
This example shows how to check if a value falls within a specific range.
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

Combining comparison operators with logical AND (`&&`) is a standard way to
determine if a number lies between two bounds. This is a common task in
data validation and processing.

## Conditional execution in loops
This example demonstrates using conditional logic inside a loop.
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

An `if` statement inside a loop allows for processing elements differently
based on their properties. The `break` statement provides a way to exit the
loop early when a specific condition is met.

## Combining switch and pattern matching
This example showcases a powerful combination of `switch`, pattern matching, and guards.
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

This advanced `switch` expression handles multiple types and conditions in a
structured and readable way. It demonstrates how modern Java features can be
combined to create highly expressive and robust conditional logic.