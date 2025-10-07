# Java Loops

This guide demonstrates various looping constructs in Java, from basic to  
advanced patterns.  

## Basic for loop

Demonstrates the classic for loop with initialization, condition, and  
increment.  

```java
void main() {
    for (var i = 0; i < 5; i++) {
        IO.println("Count: " + i);
    }
}
```

The basic for loop iterates from 0 to 4, printing each value.  

## Enhanced for-each loop

Shows iteration over a collection using the enhanced for-each syntax.  

```java
void main() {
    var fruits = List.of("apple", "banana", "cherry");
    
    for (var fruit : fruits) {
        IO.println("Fruit: " + fruit);
    }
}
```

The enhanced for-each loop simplifies iteration over collections without  
needing explicit index management.  

## While loop

Demonstrates a while loop with a condition checked before each iteration.  

```java
void main() {
    var count = 0;
    
    while (count < 5) {
        IO.println("Count: " + count);
        count++;
    }
}
```

The while loop continues as long as the condition remains true.  

## Do-while loop

Shows a do-while loop that executes at least once before checking the  
condition.  

```java
void main() {
    var count = 0;
    
    do {
        IO.println("Count: " + count);
        count++;
    } while (count < 5);
}
```

The do-while loop guarantees at least one execution before evaluating the  
condition.  

## Loop with break

Demonstrates using break to exit a loop early.  

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

The break statement immediately exits the loop when the condition is met.  

## Loop with continue

Shows using continue to skip the current iteration.  

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

The continue statement skips the rest of the current iteration and proceeds  
to the next one.  

## Nested loops

Demonstrates nested loops for multi-dimensional iteration.  

```java
void main() {
    for (var i = 1; i <= 3; i++) {
        for (var j = 1; j <= 3; j++) {
            IO.println("i=" + i + ", j=" + j);
        }
    }
}
```

Nested loops allow iteration over multiple dimensions or combinations.  

## Looping over a List

Shows iteration over a List using different approaches.  

```java
void main() {
    var numbers = List.of(10, 20, 30, 40, 50);
    
    for (var i = 0; i < numbers.size(); i++) {
        IO.println("Index " + i + ": " + numbers.get(i));
    }
}
```

This example demonstrates indexed access to List elements within a loop.  

## Looping over a Set

Demonstrates iteration over a Set using for-each loop.  

```java
void main() {
    var colors = Set.of("red", "green", "blue");
    
    for (var color : colors) {
        IO.println("Color: " + color);
    }
}
```

Sets are iterated using for-each loops since they don't support indexed  
access.  

## Looping over a Map

Shows iteration over Map entries using for-each loop.  

```java
void main() {
    var scores = Map.of("Alice", 95, "Bob", 87, "Charlie", 92);
    
    for (var entry : scores.entrySet()) {
        IO.println(entry.getKey() + ": " + entry.getValue());
    }
}
```

Map iteration accesses both keys and values through entry objects.  

## Labeled break

Demonstrates using labeled break to exit from nested loops.  

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

Labeled break allows breaking out of a specific outer loop from within  
nested loops.  

## Labeled continue

Shows using labeled continue to skip to the next iteration of an outer loop.  

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

Labeled continue skips to the next iteration of the specified outer loop.  

## Reverse iteration

Demonstrates iterating in reverse order.  

```java
void main() {
    for (var i = 5; i > 0; i--) {
        IO.println("Countdown: " + i);
    }
}
```

Reverse iteration counts down by decrementing the loop variable.  

## Infinite loop with break

Shows an infinite loop with an explicit exit condition.  

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

Infinite loops use explicit break conditions to terminate execution.  

## Step increment

Demonstrates looping with custom step increments.  

```java
void main() {
    for (var i = 0; i <= 20; i += 5) {
        IO.println("Number: " + i);
    }
}
```

Custom step increments allow skipping values in a predictable pattern.  

## Factorial calculation

Shows calculating factorial using a loop.  

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

The factorial algorithm multiplies consecutive integers from 1 to n.  

## Fibonacci sequence

Demonstrates generating Fibonacci numbers using a loop.  

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

The Fibonacci loop generates each number by summing the previous two.  

## Sum of array elements

Shows calculating the sum of array elements.  

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

This pattern accumulates values from a collection into a single result.  

## Finding maximum value

Demonstrates finding the maximum value in a collection.  

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

The maximum-finding algorithm compares each element to track the largest  
value.  

## Multiplication table

Shows generating a multiplication table using nested loops.  

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

Nested loops create a two-dimensional multiplication table.  

## Prime number check

Demonstrates checking if a number is prime using a loop.  

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

The prime check loop tests divisibility up to the square root of the number.  

## Iterating with ArrayList

Shows modifying a mutable list during iteration.  

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

This example demonstrates populating and iterating over a mutable ArrayList.  

## Pattern matching in loop

Demonstrates using pattern matching with instanceof in a loop.  

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

Pattern matching with instanceof simplifies type-checking and casting within  
loops.  

## Enhanced switch in loop

Shows using enhanced switch expressions within a loop.  

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

Enhanced switch expressions provide concise value assignments based on  
conditions.  

## Iterator pattern

Demonstrates explicit iterator usage for collection traversal.  

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

Explicit iterators provide fine-grained control over collection traversal.
