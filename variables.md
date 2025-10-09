# Java Variables

This document demonstrates 30 progressively advanced Java examples showcasing  
different ways to declare, assign, and use variables in Java, utilizing  
modern Java 25 features.  

## Basic integer variable
This example declares an integer variable using type inference.
```java
void main() {

    var count = 42;
    IO.println("Count: " + count);
}
```
The `var` keyword is used to declare the `count` variable, and the compiler
infers its type as `int`. This is a modern and concise way to declare variables
when the type is clear from the initializer.

## Double precision variable
This example shows a variable for storing a double-precision decimal number.
```java
void main() {

    var price = 19.99;
    IO.println("Price: $" + price);
}
```
The `price` variable is inferred as a `double`, which is the standard type for
floating-point numbers in Java. It is suitable for calculations requiring high
precision.

## Boolean variable
This example demonstrates declaring a variable that holds a true or false value.
```java
void main() {

    var isActive = true;
    IO.println("Active: " + isActive);
}
```
The `isActive` variable is inferred as a `boolean`. Boolean variables are
essential for controlling program flow in conditional statements and loops.

## Character variable
This example shows a variable that stores a single character.
```java
void main() {

    var initial = 'J';
    IO.println("Initial: " + initial);
}
```
The `initial` variable is inferred as a `char` and is initialized with a
character literal in single quotes. Characters are used to represent individual
letters, symbols, or numbers.

## String variable
This example declares a variable to store a sequence of characters.
```java
void main() {

    var name = "Java";
    IO.println("Language: " + name);
}
```
The `name` variable is inferred as a `String`, which is a reference type for
handling textual data. Strings are one of the most commonly used types in Java.

## Multiple variable declarations
This example demonstrates declaring multiple variables in the same scope.
```java
void main() {

    var x = 10;
    var y = 20;
    var z = 30;
    IO.println("Sum: " + (x + y + z));
}
```
Three integer variables are declared and initialized separately. This shows how
multiple pieces of data can be managed and used together in expressions.

## Variable reassignment
This example shows how the value of a mutable variable can be changed.
```java
void main() {

    var counter = 0;
    IO.println("Initial: " + counter);
    counter = 10;
    IO.println("Updated: " + counter);
}
```
The `counter` variable is first initialized to 0 and then reassigned the value
10. Variables declared with `var` are mutable by default unless marked `final`.

## Final variable
This example demonstrates a `final` variable, which cannot be reassigned.
```java
void main() {

    final var maxAttempts = 3;
    IO.println("Maximum attempts: " + maxAttempts);
}
```
The `final` keyword makes a variable a constant. Once `maxAttempts` is assigned
a value, it cannot be changed, which helps prevent accidental modifications.

## Compound assignment
This example shows compound assignment operators for concise value updates.
```java
void main() {

    var total = 100;
    total += 50;
    total -= 20;
    total *= 2;
    IO.println("Final total: " + total);
}
```
Operators like `+=`, `-=`, and `*=` combine an arithmetic operation with an
assignment. They provide a shorthand for modifying a variable's value in place.

## Type inference with collections
This example demonstrates `var` with a generic collection type.
```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    IO.println("Numbers: " + numbers);
}
```
The `var` keyword infers the type of `numbers` as `List<Integer>`. This reduces
boilerplate code while maintaining full type safety for the collection.

## Map variable
This example shows a `Map` variable for storing key-value pairs.
```java
void main() {

    var scores = Map.of("Alice", 95, "Bob", 87, "Carol", 92);
    IO.println("Scores: " + scores);
}
```
The `scores` variable is inferred as a `Map<String, Integer>`. Maps are powerful
data structures for efficient lookups based on a unique key.

## Block scope variable
This example demonstrates block-level scope for variables.
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
The `inner` variable is declared within a block (`{...}`) and is only accessible
inside that block. The `outer` variable remains visible both inside and outside.

## Variable shadowing
This example shows how an inner variable can "shadow" an outer variable.
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
A variable named `value` is declared in both the outer and inner scopes.
Inside the inner block, the inner `value` takes precedence, hiding the outer one.

## Loop variable scope
This example demonstrates the scope of a variable declared in a `for` loop.
```java
void main() {

    for (var i = 0; i < 3; i++) {
        var loopVar = i * 10;
        IO.println("Loop var: " + loopVar);
    }
}
```
The loop control variable `i` and the `loopVar` declared inside the loop only
exist for the duration of that loop. They cannot be accessed from outside.

## Conditional variable initialization
This example shows using the ternary operator to initialize a variable.
```java
void main() {

    var temperature = 25;
    var status = (temperature > 20) ? "warm" : "cold";
    IO.println("Status: " + status);
}
```
The ternary operator (`? :`) provides a compact way to assign a value to a
variable based on a boolean condition. It is a concise alternative to an `if-else` statement.

## Pattern matching variable
This example demonstrates a variable created through pattern matching.
```java
void main() {

    Object obj = "Hello";
    if (obj instanceof String s) {
        IO.println("String length: " + s.length());
    }
}
```
The enhanced `instanceof` check not only verifies the type of `obj` but also
creates a new, strongly-typed variable `s` if the check succeeds.

## Multiple types with var
This example shows `var` being used with several different types in the same scope.
```java
void main() {

    var text = "Java";
    var number = 25;
    var decimal = 3.14;
    var flag = true;
    IO.println(text + " " + number + " " + decimal + " " + flag);
}
```
The `var` keyword can infer `String`, `int`, `double`, and `boolean` types from their
initializers. This highlights its flexibility in handling various data types.

## Mutable ArrayList variable
This example demonstrates a variable holding a mutable `ArrayList`.
```java
void main() {

    var items = new ArrayList<String>();
    items.add("first");
    items.add("second");
    IO.println("Items: " + items);
}
```
The `items` variable refers to an `ArrayList`, which can be modified by adding
or removing elements after its creation.

## Immutable collection variable
This example shows a variable holding an immutable collection from `List.of()`.
```java
void main() {

    var colors = List.of("red", "green", "blue");
    IO.println("Colors: " + colors);
}
```
The `colors` variable refers to a list created by `List.of()`, which cannot be
modified. Attempting to add or remove elements would result in an exception.

## Variable in enhanced switch
This example demonstrates assigning a value to a variable from a `switch` expression.
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
A `switch` expression evaluates to a single value, which can be directly assigned
to a variable. This provides a clean and powerful way to handle conditional assignments.

## Numeric type variables
This example shows variables of different primitive numeric types.
```java
void main() {

    var byteVal = (byte) 127;
    var shortVal = (short) 32000;
    var longVal = 9876543210L;
    IO.println(byteVal + " " + shortVal + " " + longVal);
}
```
Java provides several numeric types (`byte`, `short`, `long`, etc.) to accommodate
numbers of different sizes. Explicit casting is needed when converting from a larger
type to a smaller one.

## String formatting with variables
This example demonstrates building a formatted string from multiple variables.
```java
void main() {

    var name = "Alice";
    var age = 30;
    var message = "Name: " + name + ", Age: " + age;
    IO.println(message);
}
```
String concatenation (`+`) is a common way to combine variables and literals into
a single descriptive string. For more complex formatting, `String.format()` is often used.

## Variable increment and decrement
This example shows the pre- and post-increment and decrement operators.
```java
void main() {

    var counter = 5;
    IO.println("Original: " + counter);
    IO.println("Post-increment: " + counter++);
    IO.println("After: " + counter);
    IO.println("Pre-decrement: " + --counter);
}
```
`counter++` (post-increment) uses the variable's value before incrementing it.
`--counter` (pre-decrement) decrements the value first and then uses the new value.

## Default values and initialization
This example contrasts explicit initialization with default variable values.
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
Local variables must be explicitly initialized before use. The example uses literal
values to simulate the default values that member variables would receive if not initialized.

## Variable with Math operations
This example shows a variable being used in a mathematical calculation.
```java
void main() {

    var radius = 5.0;
    var area = Math.PI * radius * radius;
    IO.println("Circle area: " + area);
}
```
The `area` variable is calculated using the `radius` variable and the `Math.PI`
constant. This demonstrates how variables store values for use in expressions.

## HashMap variable with mutations
This example demonstrates a mutable `HashMap` variable being modified.
```java
void main() {

    var map = new HashMap<String, Integer>();
    map.put("apple", 1);
    map.put("banana", 2);
    map.put("cherry", 3);
    IO.println("Map: " + map);
}
```
The `map` variable holds a `HashMap`, and the `put()` method is used to add new
key-value pairs to it after its creation, showing its mutable nature.

## Variable type casting
This example shows explicit type casting between numeric types.
```java
void main() {

    var doubleVal = 3.14;
    var intVal = (int) doubleVal;
    IO.println("Double: " + doubleVal + ", Int: " + intVal);
}
```
When assigning a `double` to an `int`, an explicit cast `(int)` is required.
This is a narrowing conversion, and the fractional part of the `double` is truncated.

## Multi-value swap
This example demonstrates the classic algorithm for swapping the values of two variables.
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
A third, temporary variable (`temp`) is used to hold one of the values while the
swap is performed. This ensures that no data is lost during the exchange.

## Computed variable values
This example shows a variable whose value is computed by a method call.
```java
void main() {

    var base = 10;
    var exponent = 3;
    var result = Math.pow(base, exponent);
    IO.println(base + " raised to " + exponent + " = " + result);
}
```
The `result` variable is assigned the value returned by the `Math.pow()` method.
This illustrates how variables can store the outcome of complex computations.

## Variable in record pattern
This example demonstrates extracting record components into variables via pattern matching.
```java
record Point(int x, int y) {}

void main() {

    var point = new Point(10, 20);
    if (point instanceof Point(var x, var y)) {
        IO.println("Coordinates: x=" + x + ", y=" + y);
    }
}
```
A record pattern `Point(var x, var y)` is used to deconstruct the `point` object.
This declaratively extracts the `x` and `y` components into new local variables.