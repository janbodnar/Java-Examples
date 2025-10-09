# Java Loops

This guide demonstrates various looping constructs in Java, from basic to  
advanced patterns.  

## Basic for loop
This example demonstrates the classic `for` loop with an initializer, a condition, and an incrementor.
```java
void main() {

    for (var i = 0; i < 5; i++) {
        IO.println("Count: " + i);
    }
}
```
The loop initializes a counter `i` to 0, continues as long as `i` is less than 5,
and increments `i` after each iteration. This structure is ideal for situations
where the number of iterations is known beforehand.

## Enhanced for-each loop
This example shows how to iterate over a collection using the enhanced `for-each` loop.
```java
void main() {


    var fruits = List.of("apple", "banana", "cherry");
    
    for (var fruit : fruits) {
        IO.println("Fruit: " + fruit);
    }
}
```
The `for-each` loop provides a simpler and more readable way to access each
element in a collection, like a `List`. It handles the underlying iteration
mechanics, so you don't need to manage an index variable.

## While loop
This example demonstrates a `while` loop that continues as long as its condition is true.
```java
void main() {

    var count = 0;
    
    while (count < 5) {
        IO.println("Count: " + count);
        count++;
    }
}
```
The loop checks the condition `count < 5` before each iteration. It is useful
when the number of iterations is not known in advance, and the loop depends on a
state that changes within the loop body.

## Do-while loop
This example shows a `do-while` loop, which guarantees the loop body is executed at least once.
```java
void main() {

    var count = 0;
    
    do {
        IO.println("Count: " + count);
        count++;
    } while (count < 5);
}
```
The condition `count < 5` is checked after the loop body runs. This makes it
suitable for scenarios where an action must be performed at least once,
regardless of the condition.

## Loop with break
This example demonstrates using the `break` statement to exit a loop prematurely.
```java
void main() {

    for (var i = 0; i < 10; i++) {
        if (i == 5) {
            break;
        }
        IO.println("Number: " + i);
    }
}
```
The loop is designed to run ten times, but the `break` statement causes it to
terminate immediately when `i` equals 5. This is useful for stopping a loop
when a specific condition has been met.

## Loop with continue
This example shows using the `continue` statement to skip the current iteration of a loop.
```java
void main() {

    for (var i = 0; i < 5; i++) {
        if (i == 2) {
            continue;
        }
        IO.println("Number: " + i);
    }
}
```
When `i` is 2, the `continue` statement is executed, and the rest of the loop
body is skipped for that iteration. The loop then proceeds with the next value
of `i`, which is 3.

## Nested loops
This example demonstrates nested `for` loops to iterate over a two-dimensional space.
```java
void main() {

    for (var i = 1; i <= 3; i++) {
        for (var j = 1; j <= 3; j++) {
            IO.println("i=" + i + ", j=" + j);
        }
    }
}
```
The outer loop controls the rows (`i`), and the inner loop controls the columns (`j`).
This structure is commonly used for working with grids, matrices, or generating
combinations of values.

## Looping over a List
This example shows how to iterate over a `List` using a traditional `for` loop with an index.
```java
void main() {

    var numbers = List.of(10, 20, 30, 40, 50);
    
    for (var i = 0; i < numbers.size(); i++) {
        IO.println("Index " + i + ": " + numbers.get(i));
    }
}
```
This approach gives you access to the index of each element, which can be useful
if you need to know the position of an item. However, for simple iteration, the
enhanced for-each loop is often preferred.

## Looping over a Set
This example demonstrates iterating over a `Set` using an enhanced `for-each` loop.
```java
void main() {

    var colors = Set.of("red", "green", "blue");
    
    for (var color : colors) {
        IO.println("Color: " + color);
    }
}
```
Since a `Set` is an unordered collection and does not support index-based access,
the `for-each` loop is the standard way to process its elements. The order of
iteration is not guaranteed.

## Looping over a Map
This example shows how to iterate over the entries of a `Map`.
```java
void main() {

    var scores = Map.of("Alice", 95, "Bob", 87, "Charlie", 92);
    
    for (var entry : scores.entrySet()) {
        IO.println(entry.getKey() + ": " + entry.getValue());
    }
}
```
The `entrySet()` method returns a `Set` of key-value pairs, which can then be
iterated over. This approach provides access to both the key and the value for
each entry in the map.

## Labeled break
This example demonstrates using a labeled `break` to exit from a nested loop structure.
```java
void main() {

    outer: for (var i = 0; i < 3; i++) {
        for (var j = 0; j < 3; j++) {
            if (i == 1 && j == 1) {
                break outer;
            }
            IO.println("i=" + i + ", j=" + j);
        }
    }
}
```
The `outer:` label identifies the outer loop. When `break outer;` is executed,
it terminates not just the inner loop, but the labeled outer loop as well,
providing precise control over nested loop flow.

## Labeled continue
This example shows how a labeled `continue` can skip to the next iteration of an outer loop.
```java
void main() {

    outer: for (var i = 0; i < 3; i++) {
        for (var j = 0; j < 3; j++) {
            if (j == 1) {
                continue outer;
            }
            IO.println("i=" + i + ", j=" + j);
        }
    }
}
```
When `j` is 1, `continue outer;` is called, causing the inner loop to terminate
for the current `i` and execution to jump to the next iteration of the outer loop.
This is useful for skipping entire sub-iterations.

## Reverse iteration
This example demonstrates a `for` loop that counts down instead of up.
```java
void main() {

    for (var i = 5; i > 0; i--) {
        IO.println("Countdown: " + i);
    }
}
```
By initializing the counter to a higher value and decrementing it (`i--`), the
loop iterates in reverse order. This is useful for tasks like a countdown or
processing elements from end to start.

## Infinite loop with break
This example shows how to create an infinite loop that is terminated by a `break` statement.
```java
void main() {

    var count = 0;
    
    while (true) {
        IO.println("Count: " + count);
        count++;
        
        if (count >= 5) {
            break;
        }
    }
}
```
The `while (true)` creates a loop that would run forever on its own. An `if`
statement inside the loop provides a condition to `break` out, ensuring the
program does not get stuck.

## Step increment
This example demonstrates a `for` loop with a custom step increment.
```java
void main() {

    for (var i = 0; i <= 20; i += 5) {
        IO.println("Number: " + i);
    }
}
```
Instead of incrementing by one, the loop variable `i` is increased by 5 in each
iteration (`i += 5`). This is useful for processing elements at regular intervals
within a range.

## Factorial calculation
This example shows how to calculate the factorial of a number using a loop.
```java
void main() {

    var n = 5;
    var factorial = 1;
    
    for (var i = 1; i <= n; i++) {
        factorial *= i;
    }
    
    IO.println("Factorial of " + n + " is " + factorial);
}
```
The loop multiplies the numbers from 1 up to `n` to compute the factorial. This
is a classic example of using a loop to accumulate a result over a series of
iterations.

## Fibonacci sequence
This example demonstrates generating the Fibonacci sequence using a loop.
```java
void main() {

    var n = 10;
    var a = 0;
    var b = 1;
    
    IO.println("Fibonacci sequence:");
    for (var i = 0; i < n; i++) {
        IO.println(a);
        var next = a + b;
        a = b;
        b = next;
    }
}
```
The loop calculates each new number by summing the two preceding ones. It uses
three variables to keep track of the current number, the next number, and their
sum, progressively building the sequence.

## Sum of array elements
This example shows how to calculate the sum of elements in a collection.
```java
void main() {

    var numbers = List.of(5, 10, 15, 20, 25);
    var sum = 0;
    
    for (var number : numbers) {
        sum += number;
    }
    
    IO.println("Sum: " + sum);
}
```
The `for-each` loop iterates through each number in the list and adds it to a
running total. This is a fundamental looping pattern for aggregating data from
a collection.

## Finding maximum value
This example demonstrates how to find the maximum value in a list.
```java
void main() {

    var numbers = List.of(23, 45, 12, 67, 34);
    var max = numbers.get(0);
    
    for (var number : numbers) {
        if (number > max) {
            max = number;
        }
    }
    
    IO.println("Maximum: " + max);
}
```
The loop iterates through the numbers, comparing each one to the current maximum
found so far. If a larger number is found, it becomes the new maximum, ensuring
the largest value is identified.

## Multiplication table
This example shows how to generate a multiplication table using nested loops.
```java
void main() {

    var n = 5;
    
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= n; j++) {
            IO.print(i * j + "\t");
        }
        IO.println("");
    }
}
```
The outer loop iterates through the rows, and the inner loop iterates through the
columns. The product of the row and column numbers is printed, forming a grid-like
multiplication table.

## Prime number check
This example demonstrates how to check if a number is prime using a loop.
```java
void main() {

    var number = 17;
    var isPrime = number > 1;
    
    for (var i = 2; i <= Math.sqrt(number); i++) {
        if (number % i == 0) {
            isPrime = false;
            break;
        }
    }
    
    IO.println(number + " is prime: " + isPrime);
}
```
The loop tests for divisibility by numbers from 2 up to the square root of the
target number. If a divisor is found, the number is not prime; otherwise, it is.
This is an efficient algorithm for primality testing.

## Iterating with ArrayList
This example shows how to populate and then iterate over a mutable `ArrayList`.
```java
void main() {

    var numbers = new ArrayList<Integer>();
    
    for (var i = 1; i <= 5; i++) {
        numbers.add(i * 10);
    }
    
    for (var number : numbers) {
        IO.println("Number: " + number);
    }
}
```
First, a `for` loop is used to add elements to the `ArrayList`. Then, an enhanced
`for-each` loop is used to read and print each of the elements that were added.

## Pattern matching in loop
This example demonstrates using pattern matching with `instanceof` inside a loop.
```java
void main() {

    var items = List.of("hello", 42, 3.14, "world", 100);
    
    for (var item : items) {
        if (item instanceof String s) {
            IO.println("String: " + s.toUpperCase());
        } else if (item instanceof Integer i) {
            IO.println("Integer: " + (i * 2));
        } else if (item instanceof Double d) {
            IO.println("Double: " + (d * 2));
        }
    }
}
```
The loop iterates over a list of mixed-type `Object`s. Pattern matching simplifies
checking the type of each item and casting it to a variable of the correct type
in a single, concise step.

## Enhanced switch in loop
This example shows how to use an enhanced `switch` expression inside a loop.
```java
void main() {

    var days = List.of("Monday", "Saturday", "Wednesday", "Sunday");
    
    for (var day : days) {
        var type = switch (day) {
            case "Saturday", "Sunday" -> "Weekend";
            default -> "Weekday";
        };
        IO.println(day + " is a " + type);
    }
}
```
For each day in the list, the `switch` expression determines whether it is a
"Weekday" or "Weekend". This provides a clean and readable way to perform
conditional logic on elements during iteration.

## Iterator pattern
This example demonstrates using an explicit `Iterator` to traverse a collection.
```java
void main() {

    var fruits = List.of("apple", "banana", "cherry");
    var iterator = fruits.iterator();
    
    while (iterator.hasNext()) {
        var fruit = iterator.next();
        IO.println("Fruit: " + fruit);
    }
}
```
The `Iterator` pattern provides a standard way to loop through a collection's
elements. Using `hasNext()` and `next()` gives you fine-grained control, which is
necessary for operations like removing elements during iteration.