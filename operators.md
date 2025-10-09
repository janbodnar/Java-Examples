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
This section demonstrates the `+` and `-` operators for indicating a value's sign.
```java
void main() {
    IO.println(2);
    IO.println(+2);
    IO.println(-2);
}
```
This example shows how the `+` operator can explicitly mark a number as
positive, though it is usually omitted. The `-` operator is used to indicate
a negative number.
```java
void main() {
    var a = 1;
    IO.println(-a);
    IO.println(-(-a));
}
```
The unary minus operator inverts the sign of its operand. Applying it twice,
as in `-(-a)`, returns the number to its original sign, demonstrating
the concept of double negation.

## Multiple assignment
This example shows how to declare and initialize multiple variables.
```java
void main() {
    var x = 10;
    var y = 20;
    var z = 30;
    var sum = x + y + z;
    IO.println("Sum: " + sum);
}
```
Three integer variables are declared and assigned values in separate statements.
Their values are then used in an arithmetic expression to calculate their sum,
which is subsequently printed.

## Assignment operator
This section demonstrates the basic assignment operator (`=`).
```java
void main() {
    var x = 1;
    IO.println(x);
}
```
The `=` operator assigns the value on its right to the variable on its left.
Here, the integer literal `1` is stored in the variable `x`.
```java
void main() {
    var x = 1;
    x = x + 1;
    IO.println(x);
}
```
In programming, an assignment is an action, not a statement of equality.
The expression on the right (`x + 1`) is evaluated first, and its result is then
assigned back to the `x` variable.

## String concatenation
This section shows how the `+` operator is used to concatenate strings.
```java
void main() {
    IO.println("Return " + "of " + "the king.");
    IO.println("Return".concat(" of").concat(" the king."));
}
```
The `+` operator provides a convenient way to join string literals. An alternative
is to use the `concat()` method, which achieves the same result but can be chained
for multiple concatenations.
```java
void main() {
    var first = "Hello";
    var second = "World";
    var result = first + " " + second;
    IO.println(result);
}
```
String variables can also be concatenated with string literals to build a new string.
This example combines two variables and a space to form a complete greeting.

## Increment and decrement operators
This section demonstrates the `++` and `--` operators for incrementing and decrementing values.
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
The `++` operator increases the value of a variable by one, and the `--` operator
decreases it by one. These are common shortcuts for modifying counters in loops
or other iterative processes.
```java
void main() {
    var a = 5;
    var b = a++;
    var c = ++a;
    IO.println("a: " + a + ", b: " + b + ", c: " + c);
}
```
The post-increment `a++` uses the value of `a` first and then increments it.
The pre-increment `++a` increments `a` first and then uses the new value. This
distinction is important when the operation is part of a larger expression.

## Arithmetic operators
This section covers the basic arithmetic operators for mathematical calculations.
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
This example showcases the standard arithmetic operators: addition (`+`),
subtraction (`-`), multiplication (`*`), division (`/`), and remainder (`%`).
These operators form the basis of most numerical computations.
```java
void main() {
    var result = 9 % 4;
    IO.println("9 modulo 4 = " + result);
}
```
The modulo operator (`%`) calculates the remainder of a division. It is useful for
tasks like checking for even or odd numbers, or for constraining values within a range.

## Integer vs floating-point division
This section highlights the difference in behavior between integer and floating-point division.
```java
void main() {
    var intResult = 5 / 2;
    IO.println("Integer division: " + intResult);
    
    var floatResult = 5 / 2.0;
    IO.println("Floating-point division: " + floatResult);
}
```
When dividing two integers, Java performs integer division, which truncates any
fractional part. To get a precise floating-point result, at least one of the
operands must be a `double` or `float`.
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
Explicitly casting one of the integer operands to a `double` forces the operation
to be treated as floating-point division. This ensures that the result includes
any fractional part.

## Boolean operators
This section demonstrates the logical operators used with boolean values.
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
Logical operators are fundamental for decision-making in programs. They are used
with relational operators (`>`, `==`, etc.) to create conditions for `if` statements
and other control flow structures.
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
The logical AND (`&&`) operator evaluates to `true` only if both of its operands are `true`.
This is used to check if multiple conditions are met simultaneously.

## Logical OR operator
This section shows the logical OR (`||`) operator.
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
The logical OR (`||`) operator evaluates to `true` if at least one of its operands is `true`.
It is useful for checking if any one of several conditions is satisfied.

## Negation operator
This section demonstrates the negation operator (`!`), which inverts a boolean value.
```java
void main() {
    IO.println(!true);
    IO.println(!false);
    IO.println(!(4 < 3));
}
```
The `!` operator flips `true` to `false` and `false` to `true`. It is useful for
checking for the absence of a condition, which can sometimes make logic clearer.

## Short-circuit evaluation
This section explains how logical operators use short-circuiting to improve performance.
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
The second operand of `&&` is only evaluated if the first is `true`, and the second
operand of `||` is only evaluated if the first is `false`. This avoids unnecessary
computations and can be used to prevent errors, like checking a null object.

## Relational operators
This section covers relational operators, which compare two values.
```java
void main() {
    IO.println("3 < 4: " + (3 < 4));
    IO.println("3 == 4: " + (3 == 4));
    IO.println("4 >= 3: " + (4 >= 3));
    IO.println("4 != 3: " + (4 != 3));
}
```
Relational operators like `<`, `==`, and `!=` are used to compare operands and always
produce a `boolean` result. They are the building blocks of conditional logic in `if`
statements and loops.
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
This example combines relational and logical operators to check if a value falls
within a specific range. This is a very common pattern for data validation.

## String equality with operators
This section highlights the correct way to compare strings for equality.
```java
void main() {
    var str1 = "hello";
    var str2 = "hello";
    var str3 = new String("hello");
    
    IO.println("str1 == str2: " + (str1 == str2));
    IO.println("str1 == str3: " + (str1 == str3));
    IO.println("str1.equals(str3): " + str1.equals(str3));
}
```
The `==` operator compares object references (memory addresses), not their content.
To compare the actual character sequences of strings, the `equals()` method must be used.

## Bitwise operators
This section demonstrates bitwise operators that work on the individual bits of numbers.
```java
void main() {
    IO.println(~7);
    IO.println(~-8);
}
```
The bitwise NOT (`~`) operator inverts all the bits of its operand. This is a
low-level operation that is different from logical negation.
```java
void main() {
    var result1 = 6 & 3;
    var result2 = 6 | 3;
    var result3 = 6 ^ 3;
    
    IO.println("6 & 3 = " + result1);
    IO.println("6 | 3 = " + result2);
    IO.println("6 ^ 3 = " + result3);
}
```
This example shows the bitwise AND, OR, and XOR operators. These are used for tasks
like setting or clearing specific bits in a number, which is common in low-level
programming and hardware control.

## Bit shifting operators
This section covers bit shifting operators, which move the bits of a number left or right.
```java
void main() {
    var num = 8;
    var leftShift = num << 1;
    var rightShift = num >> 1;
    
    IO.println("8 << 1 = " + leftShift);
    IO.println("8 >> 1 = " + rightShift);
    IO.println("-8 >> 1 = " + (-8 >> 1));
    IO.println("-8 >>> 1 = " + (-8 >>> 1));
}
```
Shifting bits to the left (`<<`) is equivalent to multiplying by a power of 2, while
shifting right (`>>`) is like dividing. The `>>>` operator is an "unsigned" right shift
that fills with zeros, which is important for handling negative numbers as bit patterns.

## Compound assignment operators
This section shows compound assignment operators that combine an operation with an assignment.
```java
void main() {
    var a = 1;
    a = a + 1;
    IO.println(a);
    
    a += 5;
    IO.println(a);
    
    a *= 3;
    IO.println(a);
}
```
Operators like `+=` and `*=` provide a concise shorthand for modifying a variable's
value in place. They are equivalent to performing an operation and then assigning the
result back to the original variable.
```java
void main() {
    var count = 10;
    count -= 3;
    IO.println("After subtraction: " + count);
    
    count /= 2;
    IO.println("After division: " + count);
    
    count %= 2;
    IO.println("Remainder: " + count);
}
```
This example demonstrates other common compound assignment operators. They help to make
code more compact and can sometimes be slightly more efficient.

## instanceof operator
This section demonstrates the `instanceof` operator for runtime type checking.
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
The `instanceof` operator checks if an object is of a certain type, including any of its
parent types. This is fundamental to polymorphism, allowing code to react differently
based on an object's actual class at runtime.
```java
void main() {
    Object obj = "Hello";
    
    if (obj instanceof String str) {
        IO.println("String length: " + str.length());
    }
}
```
Modern Java includes pattern matching for `instanceof`, which combines the type check
and the cast into a single, safer operation. If the check succeeds, the object is
assigned to a new, strongly-typed variable.

## Lambda operator
This section introduces the lambda operator (`->`) used for creating lambda expressions.
```java
void main() {
    var words = new String[]{"kind", "massive", "atom", "car", "blue"};
    java.util.Arrays.sort(words, (s1, s2) -> s1.compareTo(s2));
    IO.println(java.util.Arrays.toString(words));
}
```
A lambda expression provides a concise way to implement a functional interface. In this
example, a lambda is used to provide a custom comparison logic for sorting an array
of strings.
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
This code defines a functional interface and then implements it using a lambda expression.
This allows behavior to be treated like data, passed as an argument, and stored in a variable.
```java
void main() {
    java.util.function.Function<Integer, Integer> square = x -> x * x;
    IO.println("5 squared: " + square.apply(5));
}
```
The `java.util.function` package provides a set of standard functional interfaces. Here,
a `Function` is used to create a simple lambda that calculates the square of a number.

## Method reference operator
This section demonstrates the method reference operator (`::`) as a shorthand for some lambdas.
```java
static void greet(String msg) {
    IO.println(msg);
}

void main() {
    java.util.function.Consumer<String> f = Main::greet;
    f.accept("Hello there");
}
```
A method reference provides a way to refer to a method without invoking it. It is often
used as a more readable alternative to a lambda expression that does nothing but call
an existing method.
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    numbers.forEach(IO::println);
}
```
This example uses a method reference with the `forEach` method to print each element in a
list. This is a very common and concise pattern in modern Java for stream processing.

## Operator precedence
This section explains how operator precedence determines the order of operations.
```java
void main() {
    var result1 = 3 + 5 * 5;
    var result2 = (3 + 5) * 5;
    
    IO.println("3 + 5 * 5 = " + result1);
    IO.println("(3 + 5) * 5 = " + result2);
}
```
Just like in mathematics, multiplication has a higher precedence than addition, so it is
performed first. Parentheses can be used to override the default order of operations.

## Operator precedence table
This table lists the precedence and associativity of common Java operators.
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
```java
void main() {
    IO.println(3 + 5 * 5);
    IO.println((3 + 5) * 5);
    IO.println(!true | true);
    IO.println(!(true | true));
}
```
This example further illustrates how precedence rules affect evaluation. Understanding
these rules is key to writing correct and predictable code, but using parentheses to make
the order explicit is often the clearest approach.

## Associativity rule
This section explains how associativity determines the order for operators with the same precedence.
```java
void main() {
    var result = 9 / 3 * 3;
    IO.println("9 / 3 * 3 = " + result);
}
```
Since division and multiplication have the same precedence and are left-associative, the
expression is evaluated from left to right as `(9 / 3) * 3`. This results in `9`, not `1`.
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
Assignment operators are right-associative, which allows for chained assignments like
`a = b = c = 0`. The rightmost assignment happens first, and its result is then assigned
to the next variable to the left.

## Ternary operator
This section demonstrates the ternary operator (`?:`), a concise conditional expression.
```java
void main() {
    var age = 31;
    var adult = age >= 18 ? true : false;
    IO.println("Adult: " + adult);
}
```
The ternary operator is a compact alternative to a simple `if-else` statement. It evaluates
a condition and returns one of two values based on whether the condition is true or false.
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
Ternary operators can be chained to create more complex conditional logic, similar to
an `if-else if` ladder. While powerful, deep nesting can become difficult to read and
should be used with caution.

## Null coalescing with ternary
This section shows how the ternary operator can be used to provide default values.
```java
void main() {
    String name = null;
    var displayName = name != null ? name : "Anonymous";
    IO.println("User: " + displayName);
    
    var score = 0;
    var message = score > 0 ? "Positive" : score < 0 ? "Negative" : "Zero";
    IO.println("Score status: " + message);
}
```
A common use for the ternary operator is to provide a fallback value when a variable might
be `null`. This pattern, often called null coalescing, helps to write more robust code
that gracefully handles the absence of data.

## Prime number calculation
This example combines multiple operators to find prime numbers.
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
This code demonstrates a practical application of various operators working together.
It uses relational (`==`), logical (`||`), arithmetic (`%`), and assignment operators
to implement a primality test algorithm.

## Combining multiple operators
This section shows a complex expression involving multiple operators.
```java
void main() {
    var a = 5;
    var b = 10;
    var c = 15;
    
    var result1 = a + b * c;
    var result2 = (a + b) * c;
    var result3 = a++ + ++b * c--;
    
    IO.println("5 + 10 * 15 = " + result1);
    IO.println("(5 + 10) * 15 = " + result2);
    IO.println("After complex expression:");
    IO.println("a = " + a + ", b = " + b + ", c = " + c);
}
```
This example underscores the importance of understanding both operator precedence and
the side effects of operators like pre/post-increment. The final values of the variables
depend on the precise order in which these operations are evaluated.

## Operators with collections
This section demonstrates using operators in the context of collections.
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    var sum = 0;
    var product = 1;
    
    for (var num : numbers) {
        sum += num;
        product *= num;
    }
    
    IO.println("Sum: " + sum);
    IO.println("Product: " + product);
    IO.println("Average: " + (sum / (double) numbers.size()));
}
```
Compound assignment operators are very convenient for accumulating values when iterating
over a collection. This example uses them to calculate the sum and product of a list of
numbers.

## Logical operators with predicates
This section shows how logical operators are used to build complex conditions.
```java
void main() {
    var age = 25;
    var hasLicense = true;
    var hasInsurance = true;
    
    var canDrive = age >= 18 && hasLicense && hasInsurance;
    IO.println("Can drive: " + canDrive);
    
    var needsAttention = !hasLicense || !hasInsurance;
    IO.println("Needs attention: " + needsAttention);
}
```
This example combines multiple boolean variables to create a predicate that represents
a complex rule. This is a common pattern in business logic and data validation, where
multiple criteria must be met.