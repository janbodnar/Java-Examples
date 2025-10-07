# Java Basics

This document demonstrates Java fundamentals using modern Java 25 syntax,  
including compact source files, instance main methods, and implicit imports.  

## Simple console output

```java
void main() {
    IO.println("This is Java");
}
```

Prints a message to the console using the simplified `IO` class from Java 25.  

## String variable

```java
void main() {
    var message = "Hello, World!";
    IO.println(message);
}
```

Declares a string variable using type inference with the `var` keyword.  

## Integer variable

```java
void main() {
    var count = 42;
    IO.println("Count: " + count);
}
```

Shows an integer variable with type inference and string concatenation.  

## Multiple variables

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

Demonstrates declaring multiple variables of different types.  

## Variable reassignment

```java
void main() {
    var city = "New York";
    IO.println(city);
    
    city = "London";
    IO.println(city);
}
```

Shows how mutable variables can be reassigned to new values.  

## Type inference with var

```java
void main() {
    var name = "John Doe";
    var age = 34;
    
    IO.println(name + " is " + age + " years old");
}
```

The `var` keyword infers types from the initializer expressions.  

## Final constants

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

Constants declared with `final` cannot be reassigned after initialization.  

## String formatting

```java
void main() {
    var age = 34;
    var name = "William";
    
    var output = String.format("%s is %d years old.", name, age);
    IO.println(output);
}
```

The `String.format` method creates formatted strings with placeholders.  

## Console input with Scanner

```java
void main() {
    var scanner = new java.util.Scanner(System.in);
    
    IO.print("Enter your name: ");
    var name = scanner.nextLine();
    
    IO.println("Hello " + name);
}
```

Reads user input from the console using Scanner class.  

## Command line arguments

```java
void main(String[] args) {
    for (var arg : args) {
        IO.println(arg);
    }
}
```

Processes command line arguments passed to the program.  

## Boolean variable

```java
void main() {
    var isJavaFun = true;
    var isEasy = false;
    
    IO.println("Java is fun: " + isJavaFun);
    IO.println("Java is easy: " + isEasy);
}
```

Boolean variables store true or false values.  

## Character variable

```java
void main() {
    var initial = 'J';
    var grade = 'A';
    
    IO.println("Initial: " + initial);
    IO.println("Grade: " + grade);
}
```

Character variables store single characters enclosed in single quotes.  

## Double precision numbers

```java
void main() {
    var price = 19.99;
    var taxRate = 0.08;
    var total = price + (price * taxRate);
    
    IO.println("Total: $" + total);
}
```

Double variables store decimal numbers with floating-point precision.  

## Long integer values

```java
void main() {
    var largeNumber = 9876543210L;
    var milliseconds = System.currentTimeMillis();
    
    IO.println("Large number: " + largeNumber);
    IO.println("Current time: " + milliseconds);
}
```

Long integers store larger whole numbers using the `L` suffix.  

## Basic arithmetic

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

Demonstrates basic arithmetic operations on numeric values.  

## String concatenation

```java
void main() {
    var firstName = "John";
    var lastName = "Doe";
    var age = 30;
    
    var fullInfo = firstName + " " + lastName + " is " + age;
    IO.println(fullInfo);
}
```

Combines multiple strings and values using the concatenation operator.  

## Increment and decrement

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

Shows increment and decrement operators for numeric variables.  

## Compound assignment

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

Compound assignment operators combine arithmetic with assignment.  

## Type casting

```java
void main() {
    var doubleVal = 9.8;
    var intVal = (int) doubleVal;
    
    IO.println("Double: " + doubleVal);
    IO.println("Integer: " + intVal);
}
```

Explicit type casting converts values between compatible types.  

## Math operations

```java
void main() {
    var x = 16.0;
    
    IO.println("Square root: " + Math.sqrt(x));
    IO.println("Power of 2: " + Math.pow(x, 2));
    IO.println("Absolute: " + Math.abs(-x));
    IO.println("Max of 10,20: " + Math.max(10, 20));
}
```

The `Math` class provides common mathematical functions.  

## String template-like formatting

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

Builds formatted strings by concatenating multiple values together.  

## Implicit collection types

```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    var names = List.of("Alice", "Bob", "Charlie");
    
    IO.println("Numbers: " + numbers);
    IO.println("Names: " + names);
}
```

Creates immutable lists using `List.of` with implicit imports.  

## Working with arrays

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

Demonstrates array creation, access, and iteration.  

## String methods

```java
void main() {
    var text = "  Java Programming  ";
    
    IO.println("Original: [" + text + "]");
    IO.println("Trimmed: [" + text.trim() + "]");
    IO.println("Uppercase: [" + text.toUpperCase() + "]");
    IO.println("Length: " + text.length());
}
```

Shows common string manipulation methods for text processing.  


