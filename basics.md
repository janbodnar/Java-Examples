# Java Basics

This document demonstrates Java fundamentals using modern Java 25 syntax,  
including compact source files, instance main methods, and implicit imports.  

## Simple console output
This example shows how to print a line of text to the console.

```java
void main() {
    IO.println("This is Java");
}
```

The `main` function serves as the entry point of the program.
It uses the `IO.println` method, a simplified way to print output,
which is available in Java 25 through implicit imports.

## String variable
This example demonstrates declaring and initializing a string variable.

```java
void main() {
    var message = "Hello, World!";
    IO.println(message);
}
```

The `var` keyword allows the compiler to infer the type of the variable,
making the code more concise. Here, `message` is inferred as a `String`
and its value is printed to the console.

## Integer variable
This example shows how to declare an integer variable and print its value.

```java
void main() {
    var count = 42;
    IO.println("Count: " + count);
}
```

The `var` keyword infers the type of `count` as an `int`.
The program then prints the integer value concatenated with a string label,
demonstrating basic string and number combination.

## Multiple variables
This example illustrates declaring multiple variables of different types.

```java
void main() {
    var city = "New York";
    var name = "Paul";
    var age = 34;
    var nationality = "American";
    
    IO.println(city);
    IO.println(name);
    IO.println(age);
    IO.println(nationality);
}
```

This code declares four variables using `var` for different data types:
`String` and `int`. Each variable's value is then printed on a new line,
showcasing how multiple pieces of data can be managed.

## Variable reassignment
This example demonstrates how to change the value of a mutable variable.

```java
void main() {
    var city = "New York";
    IO.println(city);
    
    city = "London";
    IO.println(city);
}
```

The `city` variable is first initialized to "New York" and printed.
It is then reassigned a new value, "London", which is also printed,
showing that variables declared with `var` are mutable by default.

## Type inference with var
This example highlights how `var` infers different data types automatically.

```java
void main() {
    var name = "John Doe";
    var age = 34;
    
    IO.println(name + " is " + age + " years old");
}
```

The compiler infers that `name` is a `String` and `age` is an `int`.
This allows developers to write less boilerplate code while maintaining
strong typing, as shown by the combined output string.

## Final constants
This example shows how to declare constants that cannot be changed.

```java
void main() {
    final var WIDTH = 100;
    final var HEIGHT = 150;
    var variable = 40;
    
    variable = 50;
    IO.println("Width: " + WIDTH);
    IO.println("Height: " + HEIGHT);
    IO.println("Variable: " + variable);
}
```

The `final` keyword makes a variable immutable, so its value cannot be
reassigned after initialization. The example contrasts this with a regular
mutable variable that can be changed.

## String formatting
This example demonstrates creating formatted strings using placeholders.

```java
void main() {
    var age = 34;
    var name = "William";
    
    var output = String.format("%s is %d years old.", name, age);
    IO.println(output);
}
```

The `String.format` method allows for creating complex strings by inserting
variables into a template. `%s` is a placeholder for a string, and `%d` is
for an integer, making the code readable and maintainable.

## Console input with Scanner
This example shows how to read input from the user in the console.

```java
void main() {
    var scanner = new java.util.Scanner(System.in);
    
    IO.print("Enter your name: ");
    var name = scanner.nextLine();
    
    IO.println("Hello " + name);
}
```

The `Scanner` class is used to handle user input from `System.in`.
This program prompts the user to enter their name and then reads the
entire line of text, greeting them with their input.

## Command line arguments
This example demonstrates how to access command-line arguments.

```java
void main(String[] args) {
    for (var arg : args) {
        IO.println(arg);
    }
}
```

The `main` function can accept an array of strings, which represent
arguments passed when running the program from the command line.
This code iterates through the arguments and prints each one.

## Boolean variable
This example shows how to declare and use boolean variables.

```java
void main() {
    var isJavaFun = true;
    var isEasy = false;
    
    IO.println("Java is fun: " + isJavaFun);
    IO.println("Java is easy: " + isEasy);
}
```

Boolean variables can only hold two values: `true` or `false`.
They are fundamental for controlling program flow and making decisions
in conditional statements.

## Character variable
This example demonstrates the use of character variables.

```java
void main() {
    var initial = 'J';
    var grade = 'A';
    
    IO.println("Initial: " + initial);
    IO.println("Grade: " + grade);
}
```

A `char` variable stores a single character, enclosed in single quotes.
This is useful for handling individual letters or symbols, distinct from
multi-character strings.

## Double precision numbers
This example shows how to work with floating-point numbers.

```java
void main() {
    var price = 19.99;
    var taxRate = 0.08;
    var total = price + (price * taxRate);
    
    IO.println("Total: $" + total);
}
```

The `double` type is used for decimal numbers that require high precision.
This example calculates the total cost by adding tax to a price,
demonstrating basic arithmetic with `double` values.

## Long integer values
This example demonstrates how to use integers that exceed the normal range.

```java
void main() {
    var largeNumber = 9876543210L;
    var milliseconds = System.currentTimeMillis();
    
    IO.println("Large number: " + largeNumber);
    IO.println("Current time: " + milliseconds);
}
```

The `long` type stores 64-bit integers, indicated by the `L` suffix.
It is necessary for numbers larger than what a standard `int` can hold,
such as timestamps or large counters.

## Basic arithmetic
This example covers fundamental arithmetic operations.

```java
void main() {
    var a = 10;
    var b = 3;
    
    IO.println("Sum: " + (a + b));
    IO.println("Difference: " + (a - b));
    IO.println("Product: " + (a * b));
    IO.println("Quotient: " + (a / b));
    IO.println("Remainder: " + (a % b));
}
```

This code performs addition, subtraction, multiplication, division, and
modulo operations. The results show how Java handles integer arithmetic,
including truncation in division.

## String concatenation
This example shows how to combine strings and other data types.

```java
void main() {
    var firstName = "John";
    var lastName = "Doe";
    var age = 30;
    
    var fullInfo = firstName + " " + lastName + " is " + age;
    IO.println(fullInfo);
}
```

The `+` operator can be used to concatenate strings with other strings or
variables. Java automatically converts the non-string types to their
string representation to create a single combined string.

## Increment and decrement
This example demonstrates operators for increasing or decreasing a value by one.

```java
void main() {
    var counter = 5;
    
    IO.println("Original: " + counter);
    counter++;
    IO.println("After increment: " + counter);
    counter--;
    IO.println("After decrement: " + counter);
}
```

The `++` operator increments a numeric variable by one, while `--`
decrements it. These are common shortcuts for modifying counters
or iterating through values.

## Compound assignment
This example shows shorthand operators for arithmetic and assignment.

```java
void main() {
    var value = 10;
    
    value += 5;
    IO.println("After += 5: " + value);
    
    value -= 3;
    IO.println("After -= 3: " + value);
    
    value *= 2;
    IO.println("After *= 2: " + value);
}
```

Compound assignment operators like `+=`, `-=`, and `*=` combine an
arithmetic operation with an assignment. They provide a more concise way
to modify a variable's value in place.

## Type casting
This example demonstrates how to convert a value from one type to another.

```java
void main() {
    var doubleVal = 9.8;
    var intVal = (int) doubleVal;
    
    IO.println("Double: " + doubleVal);
    IO.println("Integer: " + intVal);
}
```

Explicit type casting is required when converting a value to a type that
might lose information, such as from `double` to `int`. The fractional part
is truncated during the conversion.

## Math operations
This example shows how to use common mathematical functions from the `Math` class.

```java
void main() {
    var x = 16.0;
    
    IO.println("Square root: " + Math.sqrt(x));
    IO.println("Power of 2: " + Math.pow(x, 2));
    IO.println("Absolute: " + Math.abs(-x));
    IO.println("Max of 10,20: " + Math.max(10, 20));
}
```

The `Math` class provides a wide range of static methods for operations
like square root, exponentiation, and finding the maximum of two numbers.
These are essential for scientific and mathematical calculations.

## String template-like formatting
This example shows how to build formatted strings by concatenating values.

```java
void main() {
    var product = "Laptop";
    var price = 999.99;
    var quantity = 2;
    
    var message = "Product: " + product + 
                  ", Price: $" + price + 
                  ", Quantity: " + quantity;
    IO.println(message);
}
```

This code demonstrates creating a descriptive string by joining multiple
variables and literals. While simple, for more complex formatting,
`String.format` or templates are often preferred.

## Implicit collection types
This example demonstrates creating immutable lists with implicit imports.

```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    var names = List.of("Alice", "Bob", "Charlie");
    
    IO.println("Numbers: " + numbers);
    IO.println("Names: " + names);
}
```

Java 25 allows for implicit imports of common collection types like `List`.
The `List.of` factory method creates a compact, unmodifiable list, which is
useful for defining fixed collections of data.

## Working with arrays
This example demonstrates array creation, element access, and iteration.

```java
void main() {
    var numbers = new int[]{1, 2, 3, 4, 5};
    
    IO.println("First element: " + numbers[0]);
    IO.println("Length: " + numbers.length);
    
    for (var num : numbers) {
        IO.println(num);
    }
}
```

Arrays provide a way to store a fixed-size sequence of elements of the
same type. This code shows how to access elements by index and loop
through all elements using an enhanced for-loop.

## String methods
This example showcases common methods for string manipulation.

```java
void main() {
    var text = "  Java Programming  ";
    
    IO.println("Original: [" + text + "]");
    IO.println("Trimmed: [" + text.trim() + "]");
    IO.println("Uppercase: [" + text.toUpperCase() + "]");
    IO.println("Length: " + text.length());
}
```

The `String` class offers many useful methods for text processing.
This example demonstrates removing whitespace, changing case, and getting
the length of a string.