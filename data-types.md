# Java Data Types Examples

This document contains 80 progressively complex Java examples demonstrating  
various data types, type operations, and type-related patterns using modern  
Java 25 syntax.  

## Basic int type

```java
void main() {
    var age = 30;
    IO.println("Age: " + age);
}
```

Declares an integer variable using type inference with `var`.  

## Basic double type

```java
void main() {
    var pi = 3.14159;
    IO.println("Pi: " + pi);
}
```

Declares a double-precision floating-point number using `var`.  

## Basic boolean type

```java
void main() {
    var isActive = true;
    IO.println("Active: " + isActive);
}
```

Declares a boolean variable with a true/false value.  

## Basic char type

```java
void main() {
    var initial = 'J';
    IO.println("Initial: " + initial);
}
```

Declares a character variable to hold a single Unicode character.  

## Basic String type

```java
void main() {
    var name = "Java";
    IO.println("Name: " + name);
}
```

Declares a String reference type for textual data.  

## Multiple primitive types

```java
void main() {
    var age = 30;
    var price = 19.99;
    var isAvailable = true;
    var grade = 'A';
    IO.println(age + ", " + price + ", " + isAvailable + ", " + grade);
}
```

Demonstrates using multiple primitive types together in one program.  

## Byte type

```java
void main() {
    byte smallNumber = 127;
    IO.println("Max byte: " + smallNumber);
}
```

Uses byte type for 8-bit signed integers ranging from -128 to 127.  

## Short type

```java
void main() {
    short mediumNumber = 32000;
    IO.println("Short value: " + mediumNumber);
}
```

Uses short type for 16-bit signed integers.  

## Long type

```java
void main() {
    var largeNumber = 9876543210L;
    IO.println("Long value: " + largeNumber);
}
```

Uses long type for 64-bit integers, indicated by L suffix.  

## Float type

```java
void main() {
    var temperature = 36.6f;
    IO.println("Temperature: " + temperature);
}
```

Uses float type for 32-bit floating-point numbers, indicated by f suffix.  

## Integer wrapper class

```java
void main() {
    var num = Integer.valueOf(42);
    IO.println("Integer object: " + num);
}
```

Creates an Integer wrapper object from a primitive int value.  

## Double wrapper class

```java
void main() {
    var value = Double.valueOf(3.14);
    IO.println("Double object: " + value);
}
```

Creates a Double wrapper object from a primitive double value.  

## Boolean wrapper class

```java
void main() {
    var flag = Boolean.valueOf(true);
    IO.println("Boolean object: " + flag);
}
```

Creates a Boolean wrapper object from a primitive boolean value.  

## Character wrapper class

```java
void main() {
    var letter = Character.valueOf('X');
    IO.println("Character object: " + letter);
}
```

Creates a Character wrapper object from a primitive char value.  

## Autoboxing

```java
void main() {
    Integer num = 100;
    IO.println("Autoboxed: " + num);
}
```

Demonstrates automatic conversion from primitive int to Integer wrapper.  

## Unboxing

```java
void main() {
    Integer wrapped = 200;
    int primitive = wrapped;
    IO.println("Unboxed: " + primitive);
}
```

Demonstrates automatic conversion from Integer wrapper to primitive int.  

## Type casting int to double

```java
void main() {
    var intValue = 10;
    var doubleValue = (double) intValue;
    IO.println("Casted: " + doubleValue);
}
```

Explicitly casts an integer to a double-precision floating-point number.  

## Type casting double to int

```java
void main() {
    var doubleValue = 9.99;
    var intValue = (int) doubleValue;
    IO.println("Truncated: " + intValue);
}
```

Explicitly casts a double to int, truncating the decimal part.  

## Widening conversion

```java
void main() {
    byte b = 10;
    int i = b;
    long l = i;
    IO.println("Widened: " + l);
}
```

Demonstrates implicit widening conversion from smaller to larger types.  

## Narrowing conversion

```java
void main() {
    long l = 100;
    int i = (int) l;
    byte b = (byte) i;
    IO.println("Narrowed: " + b);
}
```

Demonstrates explicit narrowing conversion requiring type casting.  

## String to int conversion

```java
void main() {
    var str = "123";
    var num = Integer.parseInt(str);
    IO.println("Parsed: " + num);
}
```

Converts a String to an int using the `parseInt` method.  

## String to double conversion

```java
void main() {
    var str = "3.14";
    var num = Double.parseDouble(str);
    IO.println("Parsed: " + num);
}
```

Converts a String to a double using the `parseDouble` method.  

## Int to String conversion

```java
void main() {
    var num = 42;
    var str = String.valueOf(num);
    IO.println("String: " + str);
}
```

Converts an int to String using the `valueOf` method.  

## Default int value

```java
void main() {
    int[] numbers = new int[1];
    IO.println("Default int: " + numbers[0]);
}
```

Shows that the default value for int type is 0.  

## Default boolean value

```java
void main() {
    boolean[] flags = new boolean[1];
    IO.println("Default boolean: " + flags[0]);
}
```

Shows that the default value for boolean type is false.  

## Default reference value

```java
void main() {
    String[] strings = new String[1];
    IO.println("Default reference: " + strings[0]);
}
```

Shows that the default value for reference types is null.  

## Integer array

```java
void main() {
    var numbers = new int[]{1, 2, 3, 4, 5};
    IO.println("First: " + numbers[0]);
}
```

Creates an integer array with initialized values.  

## String array

```java
void main() {
    var words = new String[]{"Hello", "World"};
    IO.println("Words: " + words[0] + " " + words[1]);
}
```

Creates a String array with multiple elements.  

## Array length

```java
void main() {
    var numbers = new int[]{10, 20, 30};
    IO.println("Array length: " + numbers.length);
}
```

Accesses the length property of an array.  

## Multidimensional array

```java
void main() {
    var matrix = new int[][]{{1, 2}, {3, 4}};
    IO.println("Element: " + matrix[0][1]);
}
```

Creates and accesses a two-dimensional integer array.  

## List of integers

```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    IO.println("First: " + numbers.get(0));
}
```

Creates an immutable list of integers using `List.of`.  

## List of strings

```java
void main() {
    var names = List.of("Alice", "Bob", "Charlie");
    IO.println("Names: " + names);
}
```

Creates an immutable list of strings.  

## ArrayList with type inference

```java
void main() {
    var list = new ArrayList<Integer>();
    list.add(10);
    list.add(20);
    IO.println("List: " + list);
}
```

Creates a mutable ArrayList using type inference with `var`.  

## Map with type inference

```java
void main() {
    var map = Map.of("one", 1, "two", 2);
    IO.println("Value: " + map.get("one"));
}
```

Creates an immutable map with String keys and Integer values.  

## HashMap with type inference

```java
void main() {
    var map = new HashMap<String, Integer>();
    map.put("age", 25);
    IO.println("Age: " + map.get("age"));
}
```

Creates a mutable HashMap using type inference.  

## Set of integers

```java
void main() {
    var numbers = Set.of(1, 2, 3, 2, 1);
    IO.println("Unique: " + numbers);
}
```

Creates an immutable set that automatically removes duplicates.  

## Null reference

```java
void main() {
    String text = null;
    IO.println("Null text: " + text);
}
```

Demonstrates assigning null to a reference type variable.  

## Null check

```java
void main() {
    String text = null;
    if (text == null) {
        IO.println("Text is null");
    }
}
```

Shows how to check if a reference is null using comparison.  

## Optional empty

```java
void main() {
    var optional = java.util.Optional.empty();
    IO.println("Present: " + optional.isPresent());
}
```

Creates an empty Optional to represent absence of a value.  

## Optional with value

```java
void main() {
    var optional = java.util.Optional.of(42);
    IO.println("Value: " + optional.get());
}
```

Creates an Optional containing a non-null value.  

## Optional nullable

```java
void main() {
    String text = null;
    var optional = java.util.Optional.ofNullable(text);
    IO.println("Present: " + optional.isPresent());
}
```

Creates an Optional from a potentially null value using `ofNullable`.  

## Optional orElse

```java
void main() {
    var optional = java.util.Optional.<String>empty();
    var result = optional.orElse("default");
    IO.println("Result: " + result);
}
```

Provides a default value when Optional is empty using `orElse`.  

## Integer comparison

```java
void main() {
    var a = 10;
    var b = 20;
    IO.println("Equal: " + (a == b));
    IO.println("Less: " + (a < b));
}
```

Compares primitive integers using relational operators.  

## String equality

```java
void main() {
    var s1 = "hello";
    var s2 = "hello";
    IO.println("Equals: " + s1.equals(s2));
}
```

Compares strings for equality using the `equals` method.  

## String reference comparison

```java
void main() {
    var s1 = new String("hello");
    var s2 = new String("hello");
    IO.println("Same ref: " + (s1 == s2));
    IO.println("Equal: " + s1.equals(s2));
}
```

Demonstrates difference between reference equality and value equality.  

## Integer object comparison

```java
void main() {
    var n1 = Integer.valueOf(100);
    var n2 = Integer.valueOf(100);
    IO.println("Equals: " + n1.equals(n2));
}
```

Compares Integer wrapper objects using the `equals` method.  

## Comparing with null

```java
void main() {
    String text = null;
    var isNull = text == null;
    IO.println("Is null: " + isNull);
}
```

Safely compares a reference with null to check for absence.  

## Type checking with instanceof

```java
void main() {
    Object obj = "Hello";
    var isString = obj instanceof String;
    IO.println("Is String: " + isString);
}
```

Checks the runtime type of an object using `instanceof` operator.  

## Pattern matching instanceof

```java
void main() {
    Object obj = 42;
    if (obj instanceof Integer num) {
        IO.println("Integer value: " + num);
    }
}
```

Uses pattern matching with `instanceof` for type checking and casting.  

## Var with explicit type bounds

```java
void main() {
    var list = new ArrayList<String>();
    list.add("Java");
    String first = list.get(0);
    IO.println("First: " + first);
}
```

Demonstrates `var` with generic type inference in collections.  

## Number superclass

```java
void main() {
    Number num = Integer.valueOf(42);
    IO.println("Int value: " + num.intValue());
    IO.println("Double value: " + num.doubleValue());
}
```

Uses Number superclass to hold different numeric wrapper types.  

## Constant values

```java
void main() {
    IO.println("Max int: " + Integer.MAX_VALUE);
    IO.println("Min int: " + Integer.MIN_VALUE);
    IO.println("Max double: " + Double.MAX_VALUE);
}
```

Accesses constant values defined in wrapper classes.  

## Byte array

```java
void main() {
    var bytes = new byte[]{65, 66, 67};
    IO.println("Bytes: " + bytes[0] + ", " + bytes[1] + ", " + bytes[2]);
}
```

Creates a byte array for binary data representation.  

## Character array to String

```java
void main() {
    var chars = new char[]{'J', 'a', 'v', 'a'};
    var str = new String(chars);
    IO.println("String: " + str);
}
```

Converts a character array to a String object.  

## String to char array

```java
void main() {
    var str = "Hello";
    var chars = str.toCharArray();
    IO.println("First char: " + chars[0]);
}
```

Converts a String to a character array using `toCharArray`.  

## Varargs with primitives

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

Demonstrates variable arguments (varargs) with primitive types.  

## Generic type with bounds

```java
void main() {
    var result = max(10, 20);
    IO.println("Max: " + result);
}

<T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
}
```

Uses bounded type parameters to ensure type safety in generic methods.  

## Wrapper class parsing

```java
void main() {
    var intVal = Integer.parseInt("100");
    var longVal = Long.parseLong("1000000");
    var boolVal = Boolean.parseBoolean("true");
    IO.println(intVal + ", " + longVal + ", " + boolVal);
}
```

Parses strings to various primitive types using wrapper class methods.  

## Numeric type overflow

```java
void main() {
    byte b = 127;
    b = (byte) (b + 1);
    IO.println("Overflow: " + b);
}
```

Demonstrates numeric overflow when exceeding type capacity.  

## Division and type precision

```java
void main() {
    var intResult = 5 / 2;
    var doubleResult = 5.0 / 2;
    IO.println("Int: " + intResult + ", Double: " + doubleResult);
}
```

Shows difference in precision between integer and floating-point division.  

## BigInteger for large numbers

```java
void main() {
    var big = new java.math.BigInteger("12345678901234567890");
    var result = big.add(big);
    IO.println("Result: " + result);
}
```

Uses BigInteger for arbitrary-precision integer arithmetic.  

## BigDecimal for precision

```java
void main() {
    var a = new java.math.BigDecimal("0.1");
    var b = new java.math.BigDecimal("0.2");
    var sum = a.add(b);
    IO.println("Precise sum: " + sum);
}
```

Uses BigDecimal for precise decimal arithmetic without rounding errors.  

## Enum type

```java
void main() {
    var day = Day.MONDAY;
    IO.println("Day: " + day);
}

enum Day {
    MONDAY, TUESDAY, WEDNESDAY
}
```

Defines and uses an enumeration type for a fixed set of constants.  

## Record type

```java
void main() {
    var point = new Point(10, 20);
    IO.println("X: " + point.x() + ", Y: " + point.y());
}

record Point(int x, int y) {}
```

Uses a record type for immutable data carriers with auto-generated methods.  

## Sealed interface

```java
void main() {
    Shape shape = new Circle();
    IO.println("Shape: " + shape);
}

sealed interface Shape permits Circle {}
final class Circle implements Shape {}
```

Demonstrates sealed types to restrict which classes can implement an  
interface.  

## Type switch with patterns

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

Uses enhanced switch with type patterns for type-based dispatching.  

## Primitive stream

```java
void main() {
    var sum = java.util.stream.IntStream.of(1, 2, 3, 4, 5)
        .sum();
    IO.println("Sum: " + sum);
}
```

Uses primitive streams (IntStream) for efficient numeric operations.  

## Boxing in collections

```java
void main() {
    var list = new ArrayList<Integer>();
    list.add(1);
    list.add(2);
    int sum = list.get(0) + list.get(1);
    IO.println("Sum: " + sum);
}
```

Demonstrates automatic boxing and unboxing when working with collections.  

## Generic wildcard

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

Uses wildcard generics to accept lists of any type.  

## Type inference in lambda

```java
void main() {
    var list = List.of(1, 2, 3, 4, 5);
    var evens = list.stream()
        .filter(n -> n % 2 == 0)
        .toList();
    IO.println("Evens: " + evens);
}
```

Demonstrates type inference in lambda expressions for concise code.  

## Comparable interface

```java
void main() {
    var list = new ArrayList<>(List.of(3, 1, 2));
    list.sort(Integer::compareTo);
    IO.println("Sorted: " + list);
}
```

Uses Comparable interface for natural ordering of elements.  

## Object type as universal type

```java
void main() {
    Object obj1 = 42;
    Object obj2 = "Hello";
    Object obj3 = true;
    IO.println(obj1 + ", " + obj2 + ", " + obj3);
}
```

Demonstrates Object as the universal supertype for all Java types.  

## Type-safe heterogeneous container

```java
void main() {
    var map = new HashMap<Class<?>, Object>();
    map.put(Integer.class, 42);
    map.put(String.class, "Hello");
    IO.println("Int: " + map.get(Integer.class));
    IO.println("String: " + map.get(String.class));
}
```

Creates a type-safe container holding different types using Class objects as  
keys for runtime type safety.  

## Primitive wrapper valueOf

```java
void main() {
    var i = Integer.valueOf("100");
    var d = Double.valueOf("3.14");
    var b = Boolean.valueOf("true");
    IO.println(i + ", " + d + ", " + b);
}
```

Creates wrapper objects from string representations using `valueOf` methods.  

## Type conversion with Math

```java
void main() {
    var value = 3.9;
    var rounded = Math.round(value);
    var floor = Math.floor(value);
    var ceil = Math.ceil(value);
    IO.println("Round: " + rounded + ", Floor: " + floor + ", Ceil: " + ceil);
}
```

Performs type-related mathematical operations for rounding and conversion.  

## Immutable vs mutable collections

```java
void main() {
    var immutable = List.of(1, 2, 3);
    var mutable = new ArrayList<>(immutable);
    mutable.add(4);
    IO.println("Immutable: " + immutable);
    IO.println("Mutable: " + mutable);
}
```

Contrasts immutable and mutable collection types for data storage.  

## Type-specific operations

```java
void main() {
    var str = "Hello";
    var num = 42;
    IO.println("String length: " + str.length());
    IO.println("Int bitCount: " + Integer.bitCount(num));
}
```

Demonstrates type-specific operations available on different data types.  

## Null-safe operations with Optional

```java
void main() {
    String value = null;
    var length = java.util.Optional.ofNullable(value)
        .map(String::length)
        .orElse(0);
    IO.println("Length: " + length);
}
```

Uses Optional for null-safe operations with method chaining.  

## Type erasure with generics

```java
void main() {
    var stringList = new ArrayList<String>();
    var intList = new ArrayList<Integer>();
    IO.println("Same class: " + 
        (stringList.getClass() == intList.getClass()));
}
```

Demonstrates type erasure where generic type information is removed at  
runtime.  

## Atomic types for concurrency

```java
void main() {
    var counter = new java.util.concurrent.atomic.AtomicInteger(0);
    counter.incrementAndGet();
    counter.addAndGet(5);
    IO.println("Counter: " + counter.get());
}
```

Uses atomic types for thread-safe operations without explicit locking.  
  

