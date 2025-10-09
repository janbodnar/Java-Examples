# Java Data Types Examples

This document contains 80 progressively complex Java examples demonstrating  
various data types, type operations, and type-related patterns using modern  
Java 25 syntax.  

## Basic int type
This example declares an integer variable to store a whole number.
```java
void main() {
    var age = 30;
    IO.println("Age: " + age);
}
```
The `var` keyword infers the type of `age` as `int`, which is a 32-bit signed
integer. This is the most common data type for representing whole numbers in Java.

## Basic double type
This example declares a variable to store a floating-point number.
```java
void main() {
    var pi = 3.14159;
    IO.println("Pi: " + pi);
}
```
The `var` keyword infers the type of `pi` as `double`, a 64-bit floating-point
number used for decimal values. It provides a high degree of precision for
mathematical calculations.

## Basic boolean type
This example declares a boolean variable that can hold either `true` or `false`.
```java
void main() {
    var isActive = true;
    IO.println("Active: " + isActive);
}
```
Boolean variables are fundamental for controlling program flow. They are used in
conditional statements like `if` and loops to make decisions based on their value.

## Basic char type
This example declares a character variable to hold a single character.
```java
void main() {
    var initial = 'J';
    IO.println("Initial: " + initial);
}
```
A `char` is a 16-bit Unicode character, enclosed in single quotes. It is used
to store individual letters or symbols.

## Basic String type
This example declares a `String` variable to store a sequence of characters.
```java
void main() {
    var name = "Java";
    IO.println("Name: " + name);
}
```
`String` is a reference type, not a primitive, used for textual data. It is one
of the most commonly used types in Java for handling and manipulating text.

## Multiple primitive types
This example demonstrates declaring several different primitive types.
```java
void main() {
    var age = 30;
    var price = 19.99;
    var isAvailable = true;
    var grade = 'A';
    IO.println(age + ", " + price + ", " + isAvailable + ", " + grade);
}
```
This code showcases how `var` can infer different primitive types like `int`,
`double`, `boolean`, and `char`. It highlights Java's ability to handle various
kinds of data in a single program.

## Byte type
This example shows the `byte` data type for small integer values.
```java
void main() {
    byte smallNumber = 127;
    IO.println("Max byte: " + smallNumber);
}
```
A `byte` is an 8-bit signed integer with a range from -128 to 127. It is useful
for saving memory when working with large arrays of small integers.

## Short type
This example demonstrates the `short` data type for medium-sized integers.
```java
void main() {
    short mediumNumber = 32000;
    IO.println("Short value: " + mediumNumber);
}
```
A `short` is a 16-bit signed integer, with a range from -32,768 to 32,767. It serves
as a middle ground between the `byte` and `int` types in terms of memory and range.

## Long type
This example shows the `long` data type for very large integers.
```java
void main() {
    var largeNumber = 9876543210L;
    IO.println("Long value: " + largeNumber);
}
```
A `long` is a 64-bit signed integer, indicated by the `L` suffix. It is used when
an `int` is not large enough to hold the value, such as for timestamps or large IDs.

## Float type
This example demonstrates the `float` data type for single-precision decimals.
```java
void main() {
    var temperature = 36.6f;
    IO.println("Temperature: " + temperature);
}
```
A `float` is a 32-bit floating-point number, indicated by the `f` suffix. It is
less precise than `double` but uses half the memory, making it suitable for cases
where precision is not the top priority.

## Integer wrapper class
This example shows the `Integer` wrapper class for the `int` primitive.
```java
void main() {
    var num = Integer.valueOf(42);
    IO.println("Integer object: " + num);
}
```
The `Integer` class "wraps" a primitive `int` value in an object. This allows
primitive values to be used in contexts that require objects, such as in collections.

## Double wrapper class
This example demonstrates the `Double` wrapper class for the `double` primitive.
```java
void main() {
    var value = Double.valueOf(3.14);
    IO.println("Double object: " + value);
}
```
Similar to `Integer`, the `Double` class wraps a `double` value in an object.
Wrapper classes provide utility methods and constants related to their primitive type.

## Boolean wrapper class
This example shows the `Boolean` wrapper class for the `boolean` primitive.
```java
void main() {
    var flag = Boolean.valueOf(true);
    IO.println("Boolean object: " + flag);
}
```
The `Boolean` class provides an object representation for a `boolean` value.
This is necessary for storing booleans in generic collections like `List<Boolean>`.

## Character wrapper class
This example demonstrates the `Character` wrapper class for the `char` primitive.
```java
void main() {
    var letter = Character.valueOf('X');
    IO.println("Character object: " + letter);
}
```
The `Character` class wraps a `char` value in an object. It also provides a variety
of static methods for checking character properties, like whether it is a digit or a letter.

## Autoboxing
This example shows autoboxing, the automatic conversion from primitive to wrapper type.
```java
void main() {
    Integer num = 100;
    IO.println("Autoboxed: " + num);
}
```
The Java compiler automatically converts the primitive `int` literal `100` into an
`Integer` object. This feature simplifies code by removing the need for explicit
conversion calls like `Integer.valueOf()`.

## Unboxing
This example shows unboxing, the automatic conversion from wrapper to primitive type.
```java
void main() {
    Integer wrapped = 200;
    int primitive = wrapped;
    IO.println("Unboxed: " + primitive);
}
```
The `Integer` object `wrapped` is automatically converted back to a primitive `int`.
Unboxing simplifies operations where a primitive value is needed but an object is provided.

## Type casting int to double
This example demonstrates explicit type casting from an `int` to a `double`.
```java
void main() {
    var intValue = 10;
    var doubleValue = (double) intValue;
    IO.println("Casted: " + doubleValue);
}
```
Casting from `int` to `double` is a widening conversion, so it happens without data loss.
While often implicit, an explicit cast can be used to make the conversion clear.

## Type casting double to int
This example shows explicit type casting from a `double` to an `int`.
```java
void main() {
    var doubleValue = 9.99;
    var intValue = (int) doubleValue;
    IO.println("Truncated: " + intValue);
}
```
Casting from `double` to `int` is a narrowing conversion and results in data loss.
The fractional part of the `double` is truncated, not rounded.

## Widening conversion
This example illustrates implicit widening conversion between numeric types.
```java
void main() {
    byte b = 10;
    int i = b;
    long l = i;
    IO.println("Widened: " + l);
}
```
A value of a smaller numeric type can be assigned to a variable of a larger type
without an explicit cast. This is safe because there is no risk of data loss.

## Narrowing conversion
This example demonstrates explicit narrowing conversion that requires a cast.
```java
void main() {
    long l = 100;
    int i = (int) l;
    byte b = (byte) i;
    IO.println("Narrowed: " + b);
}
```
Converting from a larger to a smaller numeric type requires an explicit cast.
This tells the compiler that you are aware of the potential for data loss if the
value is outside the smaller type's range.

## String to int conversion
This example shows how to convert a `String` to an `int`.
```java
void main() {
    var str = "123";
    var num = Integer.parseInt(str);
    IO.println("Parsed: " + num);
}
```
The `Integer.parseInt()` method is used to parse a string containing a numeric value.
This is a common operation when reading user input or data from files.

## String to double conversion
This example demonstrates converting a `String` to a `double`.
```java
void main() {
    var str = "3.14";
    var num = Double.parseDouble(str);
    IO.println("Parsed: " + num);
}
```
Similar to `parseInt`, `Double.parseDouble()` converts a string representation of a
decimal number into a `double` primitive. It will throw an exception if the string
is not a valid number.

## Int to String conversion
This example shows how to convert an `int` to a `String`.
```java
void main() {
    var num = 42;
    var str = String.valueOf(num);
    IO.println("String: " + str);
}
```
The `String.valueOf()` method provides a standard way to get the string representation
of a primitive value. An alternative is to use string concatenation, like `"" + num`.

## Default int value
This example shows the default value for the `int` type.
```java
void main() {
    int[] numbers = new int[1];
    IO.println("Default int: " + numbers[0]);
}
```
When an array of `int` is created, its elements are automatically initialized to `0`.
This is the default value for all numeric primitive types.

## Default boolean value
This example demonstrates the default value for the `boolean` type.
```java
void main() {
    boolean[] flags = new boolean[1];
    IO.println("Default boolean: " + flags[0]);
}
```
The default value for a `boolean` variable is `false`. This ensures that boolean
fields and array elements have a predictable starting state.

## Default reference value
This example shows the default value for reference types.
```java
void main() {
    String[] strings = new String[1];
    IO.println("Default reference: " + strings[0]);
}
```
The default value for any reference type (like `String` or other objects) is `null`.
This indicates that the variable does not yet refer to an actual object.

## Integer array
This example demonstrates creating an array of integers.
```java
void main() {
    var numbers = new int[]{1, 2, 3, 4, 5};
    IO.println("First: " + numbers[0]);
}
```
An array is a fixed-size container for elements of the same type. This code
initializes an integer array and accesses its first element using an index.

## String array
This example shows how to create an array of `String` objects.
```java
void main() {
    var words = new String[]{"Hello", "World"};
    IO.println("Words: " + words[0] + " " + words[1]);
}
```
This demonstrates an array holding reference types. Each element in the array is a
reference to a `String` object.

## Array length
This example shows how to get the number of elements in an array.
```java
void main() {
    var numbers = new int[]{10, 20, 30};
    IO.println("Array length: " + numbers.length);
}
```
The `length` property of an array provides its size. Unlike method calls, it is a
final field accessed directly on the array object.

## Multidimensional array
This example demonstrates a two-dimensional array, or an array of arrays.
```java
void main() {
    var matrix = new int[][]{{1, 2}, {3, 4}};
    IO.println("Element: " + matrix[0][1]);
}
```
A 2D array is useful for representing grids or matrices. Elements are accessed
using two indices, one for the row and one for the column.

## List of integers
This example shows how to create an immutable list of integers.
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    IO.println("First: " + numbers.get(0));
}
```
The `List.of()` factory method creates a fixed-size, unmodifiable list. This is
a convenient way to define a small collection of data that should not change.

## List of strings
This example demonstrates creating an immutable list of strings.
```java
void main() {
    var names = List.of("Alice", "Bob", "Charlie");
    IO.println("Names: " + names);
}
```
This shows that `List.of()` can be used with any object type, including `String`.
The resulting list is compact and efficient for read-only access.

## ArrayList with type inference
This example shows how to create a mutable `ArrayList` using `var`.
```java
void main() {
    var list = new ArrayList<Integer>();
    list.add(10);
    list.add(20);
    IO.println("List: " + list);
}
```
An `ArrayList` is a resizable array that can grow as new elements are added.
Using `var` with the diamond operator (`<>`) simplifies the declaration while
maintaining type safety.

## Map with type inference
This example demonstrates creating an immutable `Map`.
```java
void main() {
    var map = Map.of("one", 1, "two", 2);
    IO.println("Value: " + map.get("one"));
}
```
The `Map.of()` factory method creates a fixed-size map from a series of key-value
pairs. It is a concise way to define a small, unmodifiable lookup table.

## HashMap with type inference
This example shows how to create a mutable `HashMap`.
```java
void main() {
    var map = new HashMap<String, Integer>();
    map.put("age", 25);
    IO.println("Age: " + map.get("age"));
}
```
A `HashMap` is a collection that stores key-value pairs and allows for efficient
retrieval of a value given its key. It is one of the most commonly used data
structures in Java.

## Set of integers
This example demonstrates creating a `Set` that stores unique elements.
```java
void main() {
    var numbers = Set.of(1, 2, 3, 2, 1);
    IO.println("Unique: " + numbers);
}
```
The `Set.of()` factory method creates an immutable set. Any duplicate elements provided
during creation are automatically discarded, as sets only store unique values.

## Null reference
This example shows how to assign `null` to a reference variable.
```java
void main() {
    String text = null;
    IO.println("Null text: " + text);
}
```
`null` is a special literal that represents the absence of a value. A variable that
is `null` does not point to any object in memory.

## Null check
This example demonstrates how to check if a variable is `null`.
```java
void main() {
    String text = null;
    if (text == null) {
        IO.println("Text is null");
    }
}
```
Comparing a reference variable with `== null` is the standard way to check if it
points to an object. This is crucial for avoiding `NullPointerException`.

## Optional empty
This example shows how to create an empty `Optional`.
```java
void main() {
    var optional = java.util.Optional.empty();
    IO.println("Present: " + optional.isPresent());
}
```
An empty `Optional` is a container object that explicitly represents the absence
of a value. It is a safer alternative to using `null` references.

## Optional with value
This example demonstrates creating an `Optional` that contains a value.
```java
void main() {
    var optional = java.util.Optional.of(42);
    IO.println("Value: " + optional.get());
}
```
The `Optional.of()` method creates an `Optional` with a guaranteed non-null value.
Attempting to pass `null` to `of()` will result in a `NullPointerException`.

## Optional nullable
This example shows how to create an `Optional` from a potentially null value.
```java
void main() {
    String text = null;
    var optional = java.util.Optional.ofNullable(text);
    IO.println("Present: " + optional.isPresent());
}
```
The `Optional.ofNullable()` method safely handles values that might be `null`.
If the provided value is `null`, it returns an empty `Optional`; otherwise, it returns
an `Optional` containing the value.

## Optional orElse
This example demonstrates providing a default value for an empty `Optional`.
```java
void main() {
    var optional = java.util.Optional.<String>empty();
    var result = optional.orElse("default");
    IO.println("Result: " + result);
}
```
The `orElse()` method returns the value from the `Optional` if it is present,
otherwise it returns the provided default value. This is a common pattern for
safely handling potentially missing data.

## Integer comparison
This example shows how to compare primitive integer values.
```java
void main() {
    var a = 10;
    var b = 20;
    IO.println("Equal: " + (a == b));
    IO.println("Less: " + (a < b));
}
```
Relational operators like `==` and `<` are used to compare primitive numeric types.
These comparisons are straightforward and evaluate to a `boolean` result.

## String equality
This example demonstrates the correct way to compare strings for equality.
```java
void main() {
    var s1 = "hello";
    var s2 = "hello";
    IO.println("Equals: " + s1.equals(s2));
}
```
The `equals()` method should always be used to compare the content of two strings.
Using `==` would compare their memory addresses, which is usually not the intended check.

## String reference comparison
This example highlights the difference between value and reference equality.
```java
void main() {
    var s1 = new String("hello");
    var s2 = new String("hello");
    IO.println("Same ref: " + (s1 == s2));
    IO.println("Equal: " + s1.equals(s2));
}
```
Even though `s1` and `s2` have the same content, they are different objects in memory,
so `s1 == s2` is false. The `equals()` method correctly returns true because it
compares the actual character sequences.

## Integer object comparison
This example shows how to compare `Integer` wrapper objects.
```java
void main() {
    var n1 = Integer.valueOf(100);
    var n2 = Integer.valueOf(100);
    IO.println("Equals: " + n1.equals(n2));
}
```
Just like with strings, the `equals()` method should be used to compare the values of
wrapper objects. Note that for small integers, Java's caching might make `==` return
true, but this behavior should not be relied upon.

## Comparing with null
This example demonstrates a safe comparison with a `null` reference.
```java
void main() {
    String text = null;
    var isNull = text == null;
    IO.println("Is null: " + isNull);
}
```
The `==` operator is the correct way to check if a reference is `null`.
This is a fundamental check for preventing `NullPointerException` before
attempting to access an object's members.

## Type checking with instanceof
This example shows how to check the runtime type of an object.
```java
void main() {
    Object obj = "Hello";
    var isString = obj instanceof String;
    IO.println("Is String: " + isString);
}
```
The `instanceof` operator returns `true` if the object is an instance of the
specified class or any of its subclasses. It is the standard way to perform
runtime type identification.

## Pattern matching instanceof
This example demonstrates modern pattern matching with `instanceof`.
```java
void main() {
    Object obj = 42;
    if (obj instanceof Integer num) {
        IO.println("Integer value: " + num);
    }
}
```
This enhanced `instanceof` combines the type check and the cast into one step.
If `obj` is an `Integer`, it is automatically cast to the new variable `num`,
making the code more concise and safe.

## Var with explicit type bounds
This example shows `var` used with a generic collection.
```java
void main() {
    var list = new ArrayList<String>();
    list.add("Java");
    String first = list.get(0);
    IO.println("First: " + first);
}
```
The `var` keyword infers the type of `list` as `ArrayList<String>`, including its
generic type parameter. This maintains full type safety while reducing boilerplate
code in the declaration.

## Number superclass
This example demonstrates using the `Number` superclass to hold different numeric types.
```java
void main() {
    Number num = Integer.valueOf(42);
    IO.println("Int value: " + num.intValue());
    IO.println("Double value: " + num.doubleValue());
}
```
All numeric wrapper classes like `Integer`, `Double`, and `Long` extend the `Number`
class. This allows you to treat different numeric types polymorphically and convert
between them.

## Constant values
This example shows how to access constant values from wrapper classes.
```java
void main() {
    IO.println("Max int: " + Integer.MAX_VALUE);
    IO.println("Min int: " + Integer.MIN_VALUE);
    IO.println("Max double: " + Double.MAX_VALUE);
}
```
Wrapper classes provide useful constants like `MAX_VALUE` and `MIN_VALUE`. These
define the range of values that their corresponding primitive types can hold.

## Byte array
This example demonstrates creating and using a `byte` array.
```java
void main() {
    var bytes = new byte[]{65, 66, 67};
    IO.println("Bytes: " + bytes[0] + ", " + bytes[1] + ", " + bytes[2]);
}
```
A `byte` array is often used for handling binary data, such as file I/O or network
streams. In this example, the byte values correspond to the ASCII characters 'A', 'B', and 'C'.

## Character array to String
This example shows how to create a `String` from a character array.
```java
void main() {
    var chars = new char[]{'J', 'a', 'v', 'a'};
    var str = new String(chars);
    IO.println("String: " + str);
}
```
The `String` class has a constructor that accepts a `char` array, which provides
a straightforward way to build a string from its individual characters.

## String to char array
This example demonstrates converting a `String` into a character array.
```java
void main() {
    var str = "Hello";
    var chars = str.toCharArray();
    IO.println("First char: " + chars[0]);
}
```
The `toCharArray()` method is useful when you need to process the individual
characters of a string, for example, by iterating through them or modifying them.

## Varargs with primitives
This example shows a method that accepts a variable number of primitive arguments.
```java
void main() {
    printNumbers(1, 2, 3, 4, 5);
}

void printNumbers(int... numbers) {
    for (var num : numbers) {
        IO.println(num);
    }
}
```
The `...` syntax, known as varargs, allows a method to be called with any number of
arguments of the specified type. Inside the method, the arguments are treated as an array.

## Generic type with bounds
This example demonstrates a generic method with a bounded type parameter.
```java
void main() {
    var result = max(10, 20);
    IO.println("Max: " + result);
}

<T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
}
```
The `<T extends Comparable<T>>` bound ensures that any type `T` used with this method
must implement the `Comparable` interface. This guarantees that the `compareTo` method
can be called safely.

## Wrapper class parsing
This example shows parsing strings into different wrapper types.
```java
void main() {
    var intVal = Integer.parseInt("100");
    var longVal = Long.parseLong("1000000");
    var boolVal = Boolean.parseBoolean("true");
    IO.println(intVal + ", " + longVal + ", " + boolVal);
}
```
Wrapper classes provide static `parse` methods to convert strings into their corresponding
primitive types. This is essential for handling data from text-based sources.

## Numeric type overflow
This example demonstrates what happens when a numeric type exceeds its maximum value.
```java
void main() {
    byte b = 127;
    b = (byte) (b + 1);
    IO.println("Overflow: " + b);
}
```
When a `byte` with the maximum value of 127 is incremented, it "wraps around" to the
minimum value of -128. This overflow behavior is important to understand to avoid
subtle bugs in numeric calculations.

## Division and type precision
This example highlights the difference between integer and floating-point division.
```java
void main() {
    var intResult = 5 / 2;
    var doubleResult = 5.0 / 2;
    IO.println("Int: " + intResult + ", Double: " + doubleResult);
}
```
When two integers are divided, the result is an integer, and the fractional part is
truncated. To get a precise result, at least one of the operands must be a
floating-point number.

## BigInteger for large numbers
This example uses `BigInteger` for calculations involving extremely large numbers.
```java
void main() {
    var big = new java.math.BigInteger("12345678901234567890");
    var result = big.add(big);
    IO.println("Result: " + result);
}
```
The `BigInteger` class can handle integers of any size, limited only by available
memory. It is essential for applications like cryptography or scientific computing
that require arbitrary-precision arithmetic.

## BigDecimal for precision
This example uses `BigDecimal` for precise decimal calculations.
```java
void main() {
    var a = new java.math.BigDecimal("0.1");
    var b = new java.math.BigDecimal("0.2");
    var sum = a.add(b);
    IO.println("Precise sum: " + sum);
}
```
Standard floating-point types like `double` can introduce rounding errors. `BigDecimal`
should be used for financial or other calculations where exact decimal precision is critical.

## Enum type
This example demonstrates defining and using an `enum` type.
```java
void main() {
    var day = Day.MONDAY;
    IO.println("Day: " + day);
}

enum Day {
    MONDAY, TUESDAY, WEDNESDAY
}
```
An `enum` is a special type that represents a fixed set of constants. It provides
type safety and is more expressive than using integer constants for the same purpose.

## Record type
This example introduces the `record` type for creating immutable data objects.
```java
void main() {
    var point = new Point(10, 20);
    IO.println("X: " + point.x() + ", Y: " + point.y());
}

record Point(int x, int y) {}
```
A `record` is a concise syntax for defining a class that is a simple data carrier.
The compiler automatically generates a constructor, getters, `equals`, `hashCode`,
and `toString` methods.

## Sealed interface
This example shows a `sealed` interface that restricts which classes can implement it.
```java
void main() {
    Shape shape = new Circle();
    IO.println("Shape: " + shape);
}

sealed interface Shape permits Circle {}
final class Circle implements Shape {}
```
The `sealed` keyword provides fine-grained control over inheritance. It ensures that
the `Shape` interface can only be implemented by the classes listed in the `permits`
clause, making the type hierarchy more predictable.

## Type switch with patterns
This example uses an enhanced `switch` with type patterns for cleaner type dispatch.
```java
void main() {
    Object obj = 42;
    var result = switch (obj) {
        case Integer i -> "Integer: " + i;
        case String s -> "String: " + s;
        case null -> "Null value";
        default -> "Unknown type";
    };
    IO.println(result);
}
```
Pattern matching in `switch` allows for a more declarative and readable way to handle
different types. It combines the type check and variable binding, reducing boilerplate
compared to a traditional `if-else if` chain.

## Primitive stream
This example demonstrates a primitive stream for efficient operations on numbers.
```java
void main() {
    var sum = java.util.stream.IntStream.of(1, 2, 3, 4, 5)
        .sum();
    IO.println("Sum: " + sum);
}
```
Java's Stream API includes specialized streams like `IntStream` for primitive types.
These are more efficient than using a `Stream<Integer>` because they avoid the overhead
of boxing and unboxing values.

## Boxing in collections
This example illustrates the automatic boxing and unboxing in collections.
```java
void main() {
    var list = new ArrayList<Integer>();
    list.add(1);
    list.add(2);
    int sum = list.get(0) + list.get(1);
    IO.println("Sum: " + sum);
}
```
When a primitive `int` is added to a `List<Integer>`, it is autoboxed into an `Integer`
object. When retrieved and used in an arithmetic operation, it is automatically unboxed
back to an `int`.

## Generic wildcard
This example uses a generic wildcard to create a flexible method.
```java
void main() {
    var list = List.of(1, 2, 3);
    printList(list);
}

void printList(List<?> list) {
    for (var item : list) {
        IO.println(item);
    }
}
```
The `?` wildcard, known as an unbounded wildcard, allows the `printList` method to
accept a list of any type. This makes the method more reusable, as it can operate on
`List<Integer>`, `List<String>`, and so on.

## Type inference in lambda
This example shows type inference for parameters in a lambda expression.
```java
void main() {
    var list = List.of(1, 2, 3, 4, 5);
    var evens = list.stream()
        .filter(n -> n % 2 == 0)
        .toList();
    IO.println("Evens: " + evens);
}
```
The type of the lambda parameter `n` is automatically inferred by the compiler as
`Integer` from the context of the stream. This allows for more concise and readable
functional code.

## Comparable interface
This example uses the `Comparable` interface to define a natural sorting order.
```java
void main() {
    var list = new ArrayList<>(List.of(3, 1, 2));
    list.sort(Integer::compareTo);
    IO.println("Sorted: " + list);
}
```
The `Integer` class implements `Comparable`, providing a `compareTo` method that
defines its natural order. This allows collections of integers to be sorted easily
using methods like `List.sort()`.

## Object type as universal type
This example demonstrates that `Object` is the superclass of all other types.
```java
void main() {
    Object obj1 = 42;
    Object obj2 = "Hello";
    Object obj3 = true;
    IO.println(obj1 + ", " + obj2 + ", " + obj3);
}
```
Any value in Java, whether it's a primitive (which gets autoboxed) or a reference type,
can be assigned to a variable of type `Object`. This makes it a universal container,
though you lose type-specific information.

## Type-safe heterogeneous container
This example shows a pattern for creating a type-safe container for different types.
```java
void main() {
    var map = new HashMap<Class<?>, Object>();
    map.put(Integer.class, 42);
    map.put(String.class, "Hello");
    IO.println("Int: " + map.get(Integer.class));
    IO.println("String: " + map.get(String.class));
}
```
By using a `Class` object as the key, this map can store different types while still
providing a way to retrieve them in a type-safe manner. This pattern is more robust
than simply using a `Map<String, Object>`.

## Primitive wrapper valueOf
This example demonstrates creating wrapper objects from strings using `valueOf`.
```java
void main() {
    var i = Integer.valueOf("100");
    var d = Double.valueOf("3.14");
    var b = Boolean.valueOf("true");
    IO.println(i + ", " + d + ", " + b);
}
```
The `valueOf()` methods are a flexible way to create wrapper objects. For `Integer`,
`valueOf()` is often preferred to the constructor because it may return a cached instance,
improving performance for frequently used values.

## Type conversion with Math
This example shows using the `Math` class for type-related conversions.
```java
void main() {
    var value = 3.9;
    var rounded = Math.round(value);
    var floor = Math.floor(value);
    var ceil = Math.ceil(value);
    IO.println("Round: " + rounded + ", Floor: " + floor + ", Ceil: " + ceil);
}
```
The `Math` class provides standard mathematical functions for rounding `double` values.
`round` returns a `long`, while `floor` and `ceil` return `double` values, showcasing
subtle differences in type handling.

## Immutable vs mutable collections
This example contrasts immutable and mutable collection types.
```java
void main() {
    var immutable = List.of(1, 2, 3);
    var mutable = new ArrayList<>(immutable);
    mutable.add(4);
    IO.println("Immutable: " + immutable);
    IO.println("Mutable: " + mutable);
}
```
`List.of()` creates an immutable list whose contents cannot be changed. `ArrayList`,
on the other hand, is mutable and allows for adding or removing elements. Choosing
between them depends on whether the collection's data needs to change.

## Type-specific operations
This example demonstrates operations that are specific to certain data types.
```java
void main() {
    var str = "Hello";
    var num = 42;
    IO.println("String length: " + str.length());
    IO.println("Int bitCount: " + Integer.bitCount(num));
}
```
Different types offer different methods. The `String` class has methods for text
manipulation like `length()`, while the `Integer` class has methods for bitwise
operations like `bitCount()`.

## Null-safe operations with Optional
This example shows how to perform null-safe operations using `Optional`.
```java
void main() {
    String value = null;
    var length = java.util.Optional.ofNullable(value)
        .map(String::length)
        .orElse(0);
    IO.println("Length: " + length);
}
```
Using `Optional` allows for a clean, fluent chain of operations that safely handles
the possibility of a `null` value. This avoids nested `if-null` checks and makes
the code more readable.

## Type erasure with generics
This example demonstrates the concept of type erasure in Java generics.
```java
void main() {
    var stringList = new ArrayList<String>();
    var intList = new ArrayList<Integer>();
    IO.println("Same class: " + 
        (stringList.getClass() == intList.getClass()));
}
```
At runtime, the generic type information (`<String>` and `<Integer>`) is erased.
This means that both lists are seen as just `ArrayList`, which is why their `getClass()`
methods return the same `Class` object.

## Atomic types for concurrency
This example introduces atomic types for thread-safe programming.
```java
void main() {
    var counter = new java.util.concurrent.atomic.AtomicInteger(0);
    counter.incrementAndGet();
    counter.addAndGet(5);
    IO.println("Counter: " + counter.get());
}
```
The `AtomicInteger` class provides methods for integer operations that are guaranteed
to be atomic. This is a crucial tool for managing shared state in a multi-threaded
environment without using explicit locks.