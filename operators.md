# Java Operators

This document contains progressively complex Java examples demonstrating  
various operators, their usage, and patterns using modern Java 25 syntax.  

An **operator** is a special symbol indicating a specific operation to be  
performed. Operators in programming languages are derived from mathematics.  
An **operand** is one of the inputs (arguments) of an operator.  

Expressions are constructed from operands and operators. The order of  
evaluation is determined by **precedence** and **associativity** rules.  

Operators typically work with one or two operands. **Unary operators** work  
with one operand, while **binary operators** work with two operands. The  
**ternary operator** `?:` works with three operands.  

Some operators can be used in different contexts. For example, the `+`  
operator adds numbers, concatenates strings, or indicates sign. Such  
operators are called **overloaded**.  

## Sign operators

The sign operators `+` and `-` indicate or change the sign of a value.  

```java
void main() {
    IO.println(2);
    IO.println(+2);
    IO.println(-2);
}
```

The `+` sign indicates a positive number but is usually omitted. The `-`  
sign indicates a negative number.  

```java
void main() {
    var a = 1;
    IO.println(-a);
    IO.println(-(-a));
}
```

The minus operator changes the sign of a value. Double negation returns  
the original positive value.  

## Assignment operator

The assignment operator `=` assigns a value to a variable. A **variable**  
is a placeholder for a value. In mathematics, the `=` operator represents  
equality, but in programming it performs assignment.  

```java
void main() {
    var x = 1;
    IO.println(x);
}
```

The value 1 is assigned to the variable `x`.  

```java
void main() {
    var x = 1;
    x = x + 1;
    IO.println(x);
}
```

This expression adds 1 to the variable `x`. In programming, the right side  
is evaluated first and then assigned to the left side.  

## String concatenation

In Java, the `+` operator concatenates strings.  

```java
void main() {
    IO.println("Return " + "of " + "the king.");
    IO.println("Return".concat(" of").concat(" the king."));
}
```

Strings are joined using the `+` operator or the `concat` method.  

```java
void main() {
    var first = "Hello";
    var second = "World";
    var result = first + " " + second;
    IO.println(result);
}
```

Multiple strings can be combined using the concatenation operator.  

## Increment and decrement operators

Incrementing or decrementing by one is common in programming. Java provides  
the `++` and `--` operators for this purpose.  

```java
void main() {
    var x = 6;
    x++;
    x++;
    IO.println(x);
    
    x--;
    IO.println(x);
}
```

The `x++` operator increments `x` by 1. After two increments, `x` equals 8.  
The `x--` operator decrements `x` by 1, resulting in 7.  

```java
void main() {
    var a = 5;
    var b = a++;  // post-increment: b = 5, a = 6
    var c = ++a;  // pre-increment: c = 7, a = 7
    IO.println("a: " + a + ", b: " + b + ", c: " + c);
}
```

Post-increment `a++` returns the value before incrementing. Pre-increment  
`++a` increments first, then returns the new value.  

## Arithmetic operators

Java provides the following arithmetic operators:  

| Symbol | Name           |
|--------|----------------|
| `+`    | Addition       |
| `-`    | Subtraction    |
| `*`    | Multiplication |
| `/`    | Division       |
| `%`    | Remainder      |

```java
void main() {
    var a = 10;
    var b = 11;
    var c = 12;
    
    var add = a + b + c;
    var sub = c - a;
    var mult = a * b;
    var div = c / 3;
    var rem = c % a;
    
    IO.println("Addition: " + add);
    IO.println("Subtraction: " + sub);
    IO.println("Multiplication: " + mult);
    IO.println("Division: " + div);
    IO.println("Remainder: " + rem);
}
```

The example demonstrates basic arithmetic operations familiar from  
mathematics.  

```java
void main() {
    var result = 9 % 4;
    IO.println("9 modulo 4 = " + result);
}
```

The `%` operator (modulo) finds the remainder of division. For example,  
9 modulo 4 equals 1 because 4 goes into 9 twice with a remainder of 1.  

## Integer vs floating-point division

Division behaves differently for integers and floating-point numbers.  

```java
void main() {
    var intResult = 5 / 2;
    IO.println("Integer division: " + intResult);
    
    var floatResult = 5 / 2.0;
    IO.println("Floating-point division: " + floatResult);
}
```

Integer division truncates the decimal part, resulting in 2. When one  
operand is a double or float, floating-point division is performed,  
resulting in 2.5.  

```java
void main() {
    var a = 7;
    var b = 2;
    var intDiv = a / b;
    var floatDiv = (double) a / b;
    IO.println("7 / 2 (int): " + intDiv);
    IO.println("7 / 2 (double): " + floatDiv);
}
```

Casting one operand to `double` ensures floating-point division.  

## Boolean operators

Java has three logical (Boolean) operators:  

| Symbol | Name        |
|--------|-------------|
| `&&`   | logical and |
| `||`   | logical or  |
| `!`    | negation    |

```java
void main() {
    var x = 3;
    var y = 8;
    
    IO.println("x == y: " + (x == y));
    IO.println("y > x: " + (y > x));
    
    if (y > x) {
        IO.println("y is greater than x");
    }
}
```

Boolean values are often used in conditional statements. Relational  
operators like `>` and `==` always return boolean values.  

```java
void main() {
    var a = true && true;
    var b = true && false;
    var c = false && true;
    var d = false && false;
    
    IO.println("true && true: " + a);
    IO.println("true && false: " + b);
    IO.println("false && true: " + c);
    IO.println("false && false: " + d);
}
```

The logical and (`&&`) operator evaluates to `true` only when both  
operands are `true`.  


## Logical OR operator

The logical or (`||`) operator evaluates to `true` if either operand is  
`true`.  

```java
void main() {
    var a = true || true;
    var b = true || false;
    var c = false || true;
    var d = false || false;
    
    IO.println("true || true: " + a);
    IO.println("true || false: " + b);
    IO.println("false || true: " + c);
    IO.println("false || false: " + d);
}
```

Three of the four expressions evaluate to `true`. Only when both operands  
are `false` does the result become `false`.  

## Negation operator

The negation operator `!` reverses a boolean value: `true` becomes `false`  
and `false` becomes `true`.  

```java
void main() {
    IO.println(!true);
    IO.println(!false);
    IO.println(!(4 < 3));
}
```

The negation operator is useful for inverting conditions.  

## Short-circuit evaluation

The `||` and `&&` operators use **short-circuit evaluation**. The second  
operand is only evaluated if needed. For `&&`, if the first operand is  
`false`, the result is always `false`. For `||`, if the first operand is  
`true`, the result is always `true`. This improves performance.  

```java
boolean checkOne() {
    IO.println("Inside checkOne");
    return false;
}

boolean checkTwo() {
    IO.println("Inside checkTwo");
    return true;
}

void main() {
    IO.println("Testing AND:");
    if (checkOne() && checkTwo()) {
        IO.println("Pass");
    }
    
    IO.println("\nTesting OR:");
    if (checkTwo() || checkOne()) {
        IO.println("Pass");
    }
}
```

With `&&`, `checkTwo` is never called because `checkOne` returns `false`.  
With `||`, `checkOne` is never called because `checkTwo` returns `true`.  

## Relational operators

Relational operators compare values and always return a boolean value.  

| Symbol | Meaning                 |
|--------|-------------------------|
| `<`    | less than               |
| `<=`   | less than or equal to   |
| `>`    | greater than            |
| `>=`   | greater than or equal to|
| `==`   | equal to                |
| `!=`   | not equal to            |

```java
void main() {
    IO.println("3 < 4: " + (3 < 4));
    IO.println("3 == 4: " + (3 == 4));
    IO.println("4 >= 3: " + (4 >= 3));
    IO.println("4 != 3: " + (4 != 3));
}
```

These expressions compare integer values. In Java, `==` compares numerical  
values for equality (some languages use `=` for this purpose).  

```java
void main() {
    var age = 25;
    var minAge = 18;
    var maxAge = 65;
    
    if (age >= minAge && age <= maxAge) {
        IO.println("Age is within range");
    }
}
```

Relational operators can be combined with logical operators for complex  
conditions.  

## Bitwise operators

Bitwise operators work with individual bits of binary numbers. These  
operators are less commonly used in high-level programming.  

| Symbol | Meaning             |
|--------|---------------------|
| `~`    | bitwise negation    |
| `^`    | bitwise exclusive or|
| `&`    | bitwise and         |
| `|`    | bitwise or          |

```java
void main() {
    IO.println(~7);   // prints -8
    IO.println(~-8);  // prints 7
}
```

The bitwise negation operator changes each 1 to 0 and 0 to 1. One bit  
determines the sign; negating twice returns the original value.  

```java
void main() {
    var result1 = 6 & 3;  // bitwise AND
    var result2 = 6 | 3;  // bitwise OR
    var result3 = 6 ^ 3;  // bitwise XOR
    
    IO.println("6 & 3 = " + result1);
    IO.println("6 | 3 = " + result2);
    IO.println("6 ^ 3 = " + result3);
}
```

Bitwise AND: result is 1 only if both bits are 1. Bitwise OR: result is  
1 if either bit is 1. Bitwise XOR: result is 1 if bits differ.  

## Compound assignment operators

**Compound assignment operators** combine an operation with assignment,  
providing a shorthand notation.  

```java
void main() {
    var a = 1;
    a = a + 1;  // longhand
    IO.println(a);
    
    a += 5;  // shorthand for a = a + 5
    IO.println(a);
    
    a *= 3;  // shorthand for a = a * 3
    IO.println(a);
}
```

The `+=` operator adds a value to the variable. The `*=` operator  
multiplies the variable by a value.  

```java
void main() {
    var count = 10;
    count -= 3;  // count = count - 3
    IO.println("After subtraction: " + count);
    
    count /= 2;  // count = count / 2
    IO.println("After division: " + count);
    
    count %= 2;  // count = count % 2
    IO.println("Remainder: " + count);
}
```

Other compound operators include: `-=`, `*=`, `/=`, `%=`, `&=`, `|=`,  
`<<=`, `>>=`.  

## instanceof operator

The `instanceof` operator compares an object to a specified type, returning  
`true` if the object is an instance of that type.  

```java
class Base {}
class Derived extends Base {}

void main() {
    Base b = new Base();
    Derived d = new Derived();
    
    IO.println("d instanceof Base: " + (d instanceof Base));
    IO.println("b instanceof Derived: " + (b instanceof Derived));
    IO.println("d instanceof Object: " + (d instanceof Object));
}
```

The `Derived` class inherits from `Base`, so `d` is also an instance of  
`Base`. Every class inherits from `Object`, so `d` is also an instance of  
`Object`.  

```java
void main() {
    Object obj = "Hello";
    
    if (obj instanceof String str) {
        IO.println("String length: " + str.length());
    }
}
```

Pattern matching with `instanceof` (Java 16+) allows type checking and  
casting in one expression.  

## Lambda operator

Java 8 introduced the lambda operator `->` for creating lambda expressions.  

```
(parameters) -> expression
(parameters) -> { statements; }
```

Lambda expressions create concise inline implementations of functional  
interfaces. Type declaration is optional; the compiler infers types. For  
single parameters, parentheses are optional. For single expressions, curly  
braces and return keyword are optional.  

```java
void main() {
    var words = new String[]{"kind", "massive", "atom", "car", "blue"};
    java.util.Arrays.sort(words, (s1, s2) -> s1.compareTo(s2));
    IO.println(java.util.Arrays.toString(words));
}
```

Lambda expressions are commonly used for sorting and filtering operations.  

```java
interface GreetingService {
    void greet(String message);
}

void main() {
    GreetingService gs = (msg) -> IO.println(msg);
    gs.greet("Good night");
    gs.greet("Hello there");
}
```

Lambda expressions implement functional interfaces—interfaces with a single  
abstract method.  

```java
void main() {
    java.util.function.Function<Integer, Integer> square = x -> x * x;
    IO.println("5 squared: " + square.apply(5));
}
```

The `Function` interface accepts one argument and produces a result. This  
lambda computes the square of a number.  

## Method reference operator

The double colon operator `::` creates a method reference, providing a  
shorthand for lambda expressions that call a specific method.  

```java
static void greet(String msg) {
    IO.println(msg);
}

void main() {
    java.util.function.Consumer<String> f = Main::greet;
    f.accept("Hello there");
}
```

`Consumer` is a functional interface accepting one argument with no return  
value. The `::` operator creates a reference to the `greet` method.  

```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    numbers.forEach(IO::println);
}
```

Method references simplify code when passing methods as arguments. This  
example prints each number using a method reference.  

## Operator precedence

**Operator precedence** determines which operators are evaluated first.  
Precedence levels prevent ambiguity in expressions.  

```java
void main() {
    var result1 = 3 + 5 * 5;  // multiplication first
    var result2 = (3 + 5) * 5;  // parentheses first
    
    IO.println("3 + 5 * 5 = " + result1);
    IO.println("(3 + 5) * 5 = " + result2);
}
```

Multiplication has higher precedence than addition, so `3 + 5 * 5` equals  
28. Parentheses override precedence, so `(3 + 5) * 5` equals 40.  

## Operator precedence table

The following table shows common Java operators ordered by precedence  
(highest precedence first):  

| Operator                          | Meaning                                    | Associativity  |
|-----------------------------------|--------------------------------------------|----------------|
| `[] () .`                         | array access, method call, member access   | Left-to-right  |
| `++ -- + -`                       | increment, decrement, unary plus/minus     | Right-to-left  |
| `! ~ (type) new`                  | negation, bitwise NOT, cast, object create | Right-to-left  |
| `* / %`                           | multiplication, division, modulo           | Left-to-right  |
| `+ -`                             | addition, subtraction                      | Left-to-right  |
| `+`                               | string concatenation                       | Left-to-right  |
| `<< >> >>>`                       | shift                                      | Left-to-right  |
| `< <= > >=`                       | relational                                 | Left-to-right  |
| `instanceof`                      | type comparison                            | Left-to-right  |
| `== !=`                           | equality                                   | Left-to-right  |
| `&`                               | bitwise AND                                | Left-to-right  |
| `^`                               | bitwise XOR                                | Left-to-right  |
| `|`                               | bitwise OR                                 | Left-to-right  |
| `&&`                              | logical AND                                | Left-to-right  |
| `||`                              | logical OR                                 | Left-to-right  |
| `? :`                             | ternary                                    | Right-to-left  |
| `=`                               | simple assignment                          | Right-to-left  |
| `+= -= *= /= %= &=`               | compound assignment                        | Right-to-left  |
| `^= |= <<= >>= >>>=`              | compound assignment                        | Right-to-left  |

Operators on the same row have equal precedence. When operators have the  
same precedence, associativity determines evaluation order.  

```java
void main() {
    IO.println(3 + 5 * 5);
    IO.println((3 + 5) * 5);
    IO.println(!true | true);
    IO.println(!(true | true));
}
```


Multiplication has higher precedence than addition. Negation has higher  
precedence than bitwise OR. Use parentheses to control evaluation order.  

## Associativity rule

When operators have the same precedence, **associativity** determines the  
evaluation order.  

```java
void main() {
    var result = 9 / 3 * 3;
    IO.println("9 / 3 * 3 = " + result);
}
```

Multiplication, division, and modulo are left-to-right associated. The  
expression evaluates as `(9 / 3) * 3`, resulting in 9, not 1.  

Arithmetic, boolean, relational, and bitwise operators are left-to-right.  
Assignment, ternary, increment, decrement, unary, negation, bitwise NOT,  
cast, and object creation operators are right-to-left.  

```java
void main() {
    var a = 0;
    var b = 0;
    var c = 0;
    var d = 0;
    a = b = c = d = 0;
    
    IO.println(String.format("%d %d %d %d", a, b, c, d));
    
    var j = 0;
    j *= 3 + 1;
    IO.println(j);
}
```

Assignment is right-to-left associated, allowing chained assignments.  
Compound assignment is also right-to-left: the right side is evaluated  
first, then the compound operator is applied.  

## Ternary operator

The ternary operator `?:` is a conditional operator that selects one of two  
values based on a condition.  

```
condition ? value_if_true : value_if_false
```

If the condition is true, the first value is returned; otherwise, the  
second value is returned.  

```java
void main() {
    var age = 31;
    var adult = age >= 18 ? true : false;
    IO.println("Adult: " + adult);
}
```

This operator is convenient for simple conditional assignments. A person  
is considered an adult if their age is 18 or greater.  

```java
void main() {
    var score = 85;
    var grade = score >= 90 ? "A" :
                score >= 80 ? "B" :
                score >= 70 ? "C" :
                score >= 60 ? "D" : "F";
    IO.println("Grade: " + grade);
}
```

Ternary operators can be nested for multiple conditions, though readability  
may suffer with complex nesting.  

## Prime number calculation

This example demonstrates multiple operators working together to calculate  
prime numbers.  

```java
void main() {
    var nums = new int[]{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14,
                         15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26,  
                         27, 28};
    
    IO.print("Prime numbers: ");
    
    for (var num : nums) {
        if (num == 0 || num == 1) {
            continue;
        }
        
        if (num == 2 || num == 3) {
            IO.print(num + " ");
            continue;
        }
        
        var i = (int) Math.sqrt(num);
        var isPrime = true;
        
        while (i > 1) {
            if (num % i == 0) {
                isPrime = false;
            }
            i--;
        }
        
        if (isPrime) {
            IO.print(num + " ");
        }
    }
    IO.println();
}
```

A prime number has exactly two divisors: 1 and itself. We test divisibility  
by numbers up to the square root of the candidate number. The remainder  
operator `%` checks divisibility. Values 0 and 1 are not prime. Numbers 2  
and 3 are prime by definition. The `==` operator has higher precedence than  
`||`, so no parentheses are needed in `num == 2 || num == 3`.  
