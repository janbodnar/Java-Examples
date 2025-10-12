# Java Stream

This document contains progressively complex Java examples demonstrating  
various Stream operations, methods, and patterns using modern Java 25 syntax.  

Streams are a powerful abstraction in Java that enable functional-style  
operations on sequences of elements. Introduced in Java 8, streams provide a  
declarative approach to data processing, allowing you to express complex data  
manipulations concisely. Unlike collections that store all elements in memory,  
streams compute elements on demand, making them efficient for processing large  
datasets or infinite sequences.  

A stream is a sequence of elements from a source that supports sequential and  
parallel aggregate operations. Common operations include filter, map, reduce,  
find, match, and sort. The source can be a collection, array, I/O resource, or  
generator function. Streams handle iteration internally, eliminating the need  
for explicit loops and reducing boilerplate code.  

Key characteristics of streams include lazy evaluation, where intermediate  
operations are not executed until a terminal operation is invoked. This allows  
for automatic optimization and short-circuiting. Streams are also immutable—  
they never modify their source data. Instead, operations create new streams,  
preserving the original data. Once consumed by a terminal operation, a stream  
cannot be reused; you must create a new stream to process the same source  
again.  

Streams support both sequential and parallel processing. Parallel streams  
leverage multiple CPU cores to process data concurrently, potentially improving  
performance for computationally intensive operations. The Stream API integrates  
seamlessly with lambda expressions and method references, enabling expressive  
and readable code that clearly communicates intent.


## Creating streams from collections

This example demonstrates creating a stream from a list.  

```java
void main() {

    var words = List.of("pen", "coin", "desk", "chair");
    var word = words.stream().findFirst().get();
    
    IO.println(word);
}
```

The `stream` method creates a stream from a collection. The `findFirst` method  
returns the first element as an `Optional`, from which we retrieve the value  
using `get`. This is one of the most common ways to create streams in Java.  

## Creating streams from arrays

This example shows how to create a stream from an array.  

```java
void main() {

    var letters = new String[]{"a", "b", "c", "d", "e"};
    var count = Arrays.stream(letters).count();
    
    IO.println("There are " + count + " letters");
}
```

The `Arrays.stream` method creates a stream from an array. The `count` method  
is a terminal operation that returns the number of elements in the stream.  
Streams from arrays are useful when working with legacy code or APIs that  
return arrays.  

## Creating streams from strings

This example demonstrates creating a stream from a string's characters.  

```java
void main() {

    var day = "Sunday";
    var filtered = day.codePoints()
            .filter(e -> e != 'n')
            .collect(StringBuilder::new,
                    StringBuilder::appendCodePoint,
                    StringBuilder::append)
            .toString();
    
    IO.println(filtered);
}
```

The `codePoints` method returns an `IntStream` of Unicode code points from the  
string. We can filter out specific characters and collect the result back into  
a new string. This is useful for character-level string manipulation using the  
functional stream API.

## Stream specializations

This example demonstrates the three primitive stream specializations.  

```java
void main() {

    var integers = IntStream.rangeClosed(1, 16);
    var res = integers.average();
    
    res.ifPresent(IO::println);
    
    var doubles = DoubleStream.of(2.3, 33.1, 45.3);
    doubles.forEachOrdered(IO::println);
    
    var longs = LongStream.range(6, 25);
    IO.println("Count: " + longs.count());
}
```

There are three `Stream` specializations: `IntStream`, `DoubleStream`, and  
`LongStream`. These specialized streams provide better performance and  
specialized methods for primitive types. The `rangeClosed` method creates a  
stream of integers inclusive of both endpoints, while `range` excludes the end  
value.  

## Creating streams with Stream.of

This example shows using `Stream.of` to create streams with specific values.  

```java
void main() {

    var colours = Stream.of("red", "green", "blue");
    var col = colours.skip(2).findFirst();
    
    col.ifPresent(IO::println);
    
    var nums = Stream.of(3, 4, 5, 6, 7);
    var maxVal = nums.max(Comparator.naturalOrder());
    
    maxVal.ifPresent(IO::println);
}
```

The `Stream.of` method creates a sequential, ordered stream containing the  
specified values. The `skip` method skips the first n elements, and  
`findFirst` returns an `Optional` containing the next element. The `max` method  
finds the maximum value using natural ordering.  

## Creating infinite streams with iterate

This example demonstrates creating infinite streams using iteration.  

```java
void main() {

    var s1 = Stream.iterate(5, n -> n * 2).limit(10);
    s1.forEach(IO::println);
}
```

The `Stream.iterate` method returns an infinite sequential stream produced by  
iterative application of a function to an initial element (the seed). Each  
subsequent element is generated by applying the function to the previous  
element. The `limit` method restricts the stream to a specific number of  
elements, making it finite.  

## Creating infinite streams with generate

This example shows generating random values in a stream.  

```java
void main() {

    Stream.generate(new Random()::nextDouble)
            .map(e -> e * 10)
            .limit(5)
            .forEach(IO::println);
}
```

The `Stream.generate` method creates an infinite stream where each element is  
generated by a supplier function. In this case, random doubles are generated,  
multiplied by ten, and limited to five elements. This is useful for generating  
test data or creating streams from external sources.  

## Creating streams from files

This example demonstrates reading a file line by line using streams.  

```java
void main() throws java.io.IOException {

    var path = java.nio.file.Paths.get("data.txt");
    
    try (var stream = java.nio.file.Files.lines(path)) {
        stream.forEach(IO::println);
    }
}
```

The `Files.lines` method creates a stream where each element is a line from  
the file. The try-with-resources statement ensures the stream is properly  
closed after use. This approach is memory-efficient for large files since  
lines are read on demand rather than loading the entire file into memory.  


## External iteration with Iterator

This example demonstrates traditional external iteration.  

```java
void main() {

    var words = List.of("pen", "coin", "desk", "eye", "bottle");
    var it = words.iterator();
    
    while (it.hasNext()) {
        IO.println(it.next());
    }
}
```

External iteration, also known as explicit iteration, is handled by the  
programmer using `for` or `while` loops. The `Iterator` provides `hasNext` and  
`next` methods to manually traverse the collection. This was the standard  
approach before Java 8.  

## Internal iteration with forEach

This example shows internal iteration using streams.  

```java
void main() {

    var words = List.of("pen", "coin", "desk", "eye", "bottle");
    words.stream().forEach(IO::println);
}
```

Internal iteration, also called implicit iteration, is controlled by the  
stream itself. The `forEach` method handles the iteration logic internally,  
allowing you to focus on what to do with each element rather than how to  
iterate. This can be shortened to `words.forEach(IO::println)` when calling  
directly on a collection.  

## Filtering streams

This example demonstrates filtering elements based on a condition.  

```java
void main() {

    var nums = IntStream.rangeClosed(0, 25);
    var vals = nums.filter(e -> e > 15).toArray();
    
    IO.println(Arrays.toString(vals));
}
```

The `filter` method is an intermediate operation that returns a stream  
containing only elements matching the given predicate. A predicate is a  
function that returns a boolean value. The `toArray` method is a terminal  
operation that collects the stream elements into an array.  

## Filtering with method references

This example shows filtering using a custom method.  

```java
void main() {

    var nums = IntStream.rangeClosed(0, 30);
    nums.filter(this::isEven).forEach(IO::println);
}

boolean isEven(int e) {

    return e % 2 == 0;
}
```

Method references can be passed to `filter` using the double colon operator.  
This makes the code more readable and reusable. The `isEven` method is invoked  
for each element, and only elements that return true are included in the  
resulting stream.  

## Skipping elements

This example demonstrates skipping the first n elements of a stream.  

```java
void main() {

    var s = IntStream.range(0, 15);
    s.skip(3).limit(5).forEach(IO::println);
}
```

The `skip` method skips the first n elements of the stream, while `limit`  
restricts the number of elements to m. These operations are useful for  
pagination or processing specific subsets of data. Both are intermediate  
operations that can be chained together.  

## Sorting primitive streams

This example shows sorting a stream of integers.  

```java
void main() {

    var nums = IntStream.of(4, 3, 2, 1, 8, 6, 7, 5);
    var sorted = nums.sorted().toArray();
    
    IO.println("Sorted: " + Arrays.toString(sorted));
}
```

The `sorted` method sorts the elements of the stream in natural order. For  
primitive streams like `IntStream`, the natural order is ascending numerical  
order. This is an intermediate operation that returns a new sorted stream  
without modifying the original source.  

## Sorting objects with comparators

This example demonstrates sorting complex objects.  

```java
record Car(String name, int price) {}

void main() {

    var cars = List.of(
            new Car("Citroen", 23000),
            new Car("Porsche", 65000),
            new Car("Skoda", 18000),
            new Car("Volkswagen", 33000),
            new Car("Volvo", 47000)
    );
    
    cars.stream()
            .sorted(Comparator.comparing(Car::price))
            .forEach(IO::println);
}
```

The `sorted` method can accept a `Comparator` to define custom sorting logic.  
The `Comparator.comparing` method creates a comparator that extracts a sort key  
from objects using a method reference. In this case, cars are sorted by their  
price field in ascending order.  

## Removing duplicates

This example shows removing duplicate elements from a stream.  

```java
void main() {

    var nums = IntStream.of(1, 1, 3, 4, 4, 6, 7, 7);
    var unique = nums.distinct().toArray();
    
    IO.println(Arrays.toString(unique));
}
```

The `distinct` method returns a stream consisting of unique elements, removing  
all duplicates. For object streams, equality is determined by the `equals`  
method. This operation maintains the encounter order of the first occurrence of  
each element.  

## Mapping with lambda expressions

This example demonstrates transforming stream elements.  

```java
void main() {

    var nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    var squares = nums.map(e -> e * e).toArray();
    
    IO.println(Arrays.toString(squares));
}
```

The `map` method is an intermediate operation that transforms each element by  
applying a function. Here, a lambda expression squares each number. The  
original source is never modified; instead, a new stream with transformed  
values is created.  

## Mapping strings

This example shows transforming string elements.  

```java
void main() {

    var words = Stream.of("cardinal", "pen", "coin", "globe");
    words.map(this::capitalize).forEach(IO::println);
}

String capitalize(String word) {

    return word.substring(0, 1).toUpperCase() + 
           word.substring(1).toLowerCase();
}
```

Method references can be used with `map` to apply custom transformations. The  
`capitalize` method takes a string and returns a new string with the first  
letter uppercase and the rest lowercase. Each element in the stream is  
transformed independently.  

## Finding maximum values

This example demonstrates finding the maximum element in a stream.  

```java
void main() {

    var nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    var maxValue = nums.max();
    
    maxValue.ifPresent(val -> 
            IO.println("The maximum value is: " + val));
}
```

The `max` method is a terminal operation that finds the maximum element. It  
returns an `Optional` because the stream might be empty. The `ifPresent` method  
executes the provided action only if a value is present, avoiding null pointer  
exceptions.  

## Custom reductions

This example shows creating a custom reduction operation.  

```java
void main() {

    var nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    var product = nums.reduce((a, b) -> a * b);
    
    product.ifPresent(val -> 
            IO.println("The product is: " + val));
}
```

The `reduce` method performs a reduction on the stream elements using an  
associative accumulation function. It returns an `Optional` containing the  
result. Reductions are versatile and can implement operations like sum,  
product, concatenation, and more.  

## Collecting to lists

This example demonstrates collecting stream elements into a list.  

```java
record Car(String name, int price) {}

void main() {

    var cars = List.of(
            new Car("Citroen", 23000),
            new Car("Porsche", 65000),
            new Car("Skoda", 18000),
            new Car("Volkswagen", 33000),
            new Car("Volvo", 47000)
    );
    
    var names = cars.stream()
            .map(Car::name)
            .filter(name -> name.startsWith("Vo"))
            .toList();
    
    names.forEach(IO::println);
}
```

The `collect` method is a terminal reduction operation that accumulates stream  
elements into a collection. The `toList` method (Java 16+) provides a simpler  
way to collect elements into an immutable list. Filtering and mapping can be  
combined in a pipeline before collecting.  

## Grouping elements

This example shows grouping and counting elements.  

```java
void main() {

    var items = List.of("pen", "book", "pen", "coin",
            "book", "desk", "book", "pen", "book", "coin");
    
    var result = items.stream()
            .collect(Collectors.groupingBy(
                    function.Function.identity(),
                    Collectors.counting()
            ));
    
    result.forEach((key, value) -> 
            IO.println(key + ": " + value));
}
```

The `Collectors.groupingBy` method groups elements by a classifier function and  
applies a downstream collector to each group. `Function.identity` returns each  
element as its own key, and `counting` counts occurrences. This is useful for  
frequency analysis and data aggregation.  

Now I'll add 60 more diverse stream examples to reach the required total. Let me continue with more examples:

## Parallel streams

This example demonstrates using parallel processing.  

```java
void main() {

    var result = IntStream.rangeClosed(1, 100)
            .parallel()
            .filter(n -> n % 2 == 0)
            .sum();
    
    IO.println("Sum of even numbers: " + result);
}
```

The `parallel` method converts a sequential stream into a parallel stream that  
processes elements concurrently across multiple threads. This can improve  
performance for computationally intensive operations on large datasets, though  
overhead makes it less beneficial for small streams or simple operations.  

## Finding any element

This example shows finding any matching element in a parallel stream.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    var any = numbers.parallelStream()
            .filter(n -> n > 5)
            .findAny();
    
    any.ifPresent(val -> IO.println("Found: " + val));
}
```

The `findAny` method returns an arbitrary element from the stream. Unlike  
`findFirst`, it doesn't guarantee which element is returned, making it more  
efficient in parallel streams. It returns an `Optional` which may be empty if  
no elements match.  

## Checking if all match

This example demonstrates testing if all elements satisfy a predicate.  

```java
void main() {

    var numbers = List.of(2, 4, 6, 8, 10);
    var allEven = numbers.stream()
            .allMatch(n -> n % 2 == 0);
    
    IO.println("All even? " + allEven);
}
```

The `allMatch` method is a short-circuiting terminal operation that returns  
true if all elements match the given predicate. It stops processing as soon as  
it encounters an element that doesn't match, improving efficiency. It returns  
true for empty streams.  

## Checking if any match

This example shows testing if any element satisfies a condition.  

```java
void main() {

    var numbers = List.of(1, 3, 5, 7, 8);
    var hasEven = numbers.stream()
            .anyMatch(n -> n % 2 == 0);
    
    IO.println("Has even number? " + hasEven);
}
```

The `anyMatch` method returns true if at least one element matches the  
predicate. Like `allMatch`, it's short-circuiting and stops as soon as it  
finds a matching element. It returns false for empty streams.  

## Checking if none match

This example demonstrates verifying no elements match a condition.  

```java
void main() {

    var numbers = List.of(1, 3, 5, 7, 9);
    var noneEven = numbers.stream()
            .noneMatch(n -> n % 2 == 0);
    
    IO.println("None even? " + noneEven);
}
```

The `noneMatch` method returns true if no elements match the predicate. It's  
the opposite of `anyMatch` and is also short-circuiting. This is useful for  
validating that certain conditions are completely absent from a dataset.  

## Summing values

This example shows calculating the sum of stream elements.  

```java
void main() {

    var numbers = IntStream.rangeClosed(1, 10);
    var sum = numbers.sum();
    
    IO.println("Sum: " + sum);
}
```

The `sum` method is a terminal operation available on primitive streams that  
returns the sum of all elements. For object streams, use `reduce` or  
`Collectors.summingInt`. This provides a cleaner alternative to using reduce  
with addition.  

## Calculating averages

This example demonstrates computing the average of numbers.  

```java
void main() {

    var numbers = IntStream.of(10, 20, 30, 40, 50);
    var avg = numbers.average();
    
    avg.ifPresent(val -> IO.println("Average: " + val));
}
```

The `average` method returns an `OptionalDouble` containing the arithmetic mean  
of the stream elements. It's only available on primitive streams. The result is  
empty if the stream is empty, avoiding division by zero errors.  

## Getting statistics

This example shows collecting comprehensive statistics.  

```java
void main() {

    var numbers = IntStream.rangeClosed(1, 100);
    var stats = numbers.summaryStatistics();
    
    IO.println("Count: " + stats.getCount());
    IO.println("Sum: " + stats.getSum());
    IO.println("Min: " + stats.getMin());
    IO.println("Max: " + stats.getMax());
    IO.println("Average: " + stats.getAverage());
}
```

The `summaryStatistics` method returns an object containing count, sum, min,  
max, and average in a single pass through the stream. This is more efficient  
than calling each operation separately when you need multiple statistics.  

## FlatMapping nested collections

This example demonstrates flattening nested structures.  

```java
void main() {

    var lists = List.of(
            List.of(1, 2, 3),
            List.of(4, 5),
            List.of(6, 7, 8, 9)
    );
    
    var flattened = lists.stream()
            .flatMap(list -> list.stream())
            .toList();
    
    IO.println(flattened);
}
```

The `flatMap` method transforms each element into a stream and flattens all  
resulting streams into a single stream. This is essential for working with  
nested collections or when a mapping function returns multiple values per  
input element.  

## Peeking at elements

This example shows inspecting elements during stream processing.  

```java
void main() {

    var result = IntStream.rangeClosed(1, 5)
            .peek(n -> IO.println("Processing: " + n))
            .map(n -> n * 2)
            .peek(n -> IO.println("After mapping: " + n))
            .sum();
    
    IO.println("Final result: " + result);
}
```

The `peek` method performs an action on each element without modifying the  
stream. It's primarily used for debugging to observe elements as they flow  
through the pipeline. Unlike `forEach`, it's an intermediate operation that  
returns a stream.  

## Sorting in reverse order

This example demonstrates sorting in descending order.  

```java
void main() {

    var numbers = List.of(5, 2, 8, 1, 9, 3);
    var sorted = numbers.stream()
            .sorted(Comparator.reverseOrder())
            .toList();
    
    IO.println(sorted);
}
```

The `Comparator.reverseOrder` method creates a comparator that imposes the  
reverse of natural ordering. This is simpler than creating a custom comparator  
for descending sorts. It works with any comparable type.  

## Sorting with multiple criteria

This example shows sorting by multiple fields.  

```java
record Person(String name, int age) {}

void main() {

    var people = List.of(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Alice", 25),
            new Person("Charlie", 30)
    );
    
    var sorted = people.stream()
            .sorted(Comparator
                    .comparing(Person::name)
                    .thenComparing(Person::age))
            .toList();
    
    sorted.forEach(IO::println);
}
```

The `thenComparing` method allows chaining multiple comparison criteria. When  
the first criteria produces equal values, the next criteria is used. This  
enables sophisticated multi-level sorting without complex comparator  
implementations.  

## Partitioning elements

This example demonstrates splitting a stream into two groups.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    var partitioned = numbers.stream()
            .collect(Collectors.partitioningBy(
                    n -> n % 2 == 0));
    
    IO.println("Even: " + partitioned.get(true));
    IO.println("Odd: " + partitioned.get(false));
}
```

The `partitioningBy` collector divides elements into two groups based on a  
predicate, returning a map with boolean keys. This is more efficient than  
filtering twice and ensures all elements are categorized exactly once.  

## Joining strings

This example shows concatenating stream elements.  

```java
void main() {

    var words = List.of("Java", "is", "powerful", "and", "expressive");
    var sentence = words.stream()
            .collect(Collectors.joining(" "));
    
    IO.println(sentence);
}
```

The `joining` collector concatenates stream elements into a single string with  
optional delimiter, prefix, and suffix. This is cleaner than using reduce with  
string concatenation and handles edge cases like empty streams appropriately.  

## Collecting to sets

This example demonstrates collecting unique elements.  

```java
void main() {

    var numbers = List.of(1, 2, 2, 3, 3, 3, 4, 4, 5);
    var uniqueNumbers = numbers.stream()
            .collect(Collectors.toSet());
    
    IO.println(uniqueNumbers);
}
```

The `toSet` collector accumulates elements into a Set, automatically removing  
duplicates. The resulting set is mutable, unlike `toList` in recent Java  
versions. Use `distinct().toList()` if you need to preserve order while  
removing duplicates.  

## Collecting to maps

This example shows creating maps from stream elements.  

```java
void main() {

    var words = List.of("apple", "banana", "cherry");
    var lengthMap = words.stream()
            .collect(Collectors.toMap(
                    word -> word,
                    word -> word.length()
            ));
    
    lengthMap.forEach((key, value) -> 
            IO.println(key + " -> " + value));
}
```

The `toMap` collector creates a map from stream elements using key and value  
mapper functions. It throws an exception on duplicate keys unless you provide a  
merge function. This is useful for creating lookup tables or index structures.  

## Reducing with identity value

This example demonstrates reduction with an initial value.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    var sum = numbers.stream()
            .reduce(0, (a, b) -> a + b);
    
    IO.println("Sum: " + sum);
}
```

The `reduce` method with an identity value always returns a concrete result  
instead of an Optional. The identity value is used as the starting point and  
returned if the stream is empty. This form is useful when you always expect a  
result.  

## MinBy and MaxBy

This example shows finding minimum and maximum with custom comparators.  

```java
void main() {

    var words = List.of("apple", "pie", "banana", "cherry");
    var shortest = words.stream()
            .min(Comparator.comparing(String::length));
    
    shortest.ifPresent(word -> 
            IO.println("Shortest word: " + word));
}
```

The `min` method finds the minimum element according to a comparator. Like  
`max`, it returns an Optional since the stream might be empty. Comparators can  
be created using `comparing` for clean, readable code.  

## Teeing for dual collection

This example demonstrates collecting to two different collectors.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    var result = numbers.stream()
            .collect(Collectors.teeing(
                    Collectors.summingInt(n -> n),
                    Collectors.counting(),
                    (sum, count) -> "Sum: " + sum + ", Count: " + count
            ));
    
    IO.println(result);
}
```

The `teeing` collector (Java 12+) applies two collectors to the same stream and  
combines their results with a merger function. This processes the stream only  
once, which is more efficient than streaming twice for different aggregations.  

## Filtering with takeWhile

This example shows taking elements while a condition holds.  

```java
void main() {

    var numbers = List.of(2, 4, 6, 7, 8, 10);
    var taken = numbers.stream()
            .takeWhile(n -> n % 2 == 0)
            .toList();
    
    IO.println(taken);
}
```

The `takeWhile` method (Java 9+) takes elements from the stream while the  
predicate is true, stopping at the first false result. Unlike `filter`, it's  
order-dependent and stops processing once the condition fails, making it useful  
for sorted or ordered data.  

## Filtering with dropWhile

This example demonstrates dropping elements while a condition holds.  

```java
void main() {

    var numbers = List.of(2, 4, 6, 7, 8, 10);
    var dropped = numbers.stream()
            .dropWhile(n -> n % 2 == 0)
            .toList();
    
    IO.println(dropped);
}
```

The `dropWhile` method (Java 9+) is the complement of `takeWhile`. It skips  
elements while the predicate is true and includes all remaining elements once  
the predicate becomes false. This is useful for skipping headers or prefixes in  
ordered data.  

## Converting between primitive streams

This example shows boxing primitive streams to object streams.  

```java
void main() {

    var intStream = IntStream.rangeClosed(1, 5);
    var boxed = intStream.boxed()
            .map(n -> n * 10)
            .toList();
    
    IO.println(boxed);
}
```

The `boxed` method converts a primitive stream to its object wrapper equivalent  
(IntStream to Stream<Integer>). This is necessary when you need to use  
operations that aren't available on primitive streams or when collecting to  
object collections.  

## Creating streams with iterate and predicate

This example demonstrates bounded iteration with a condition.  

```java
void main() {

    var fibonacci = Stream
            .iterate(new int[]{0, 1}, f -> new int[]{f[1], f[0] + f[1]})
            .limit(10)
            .map(f -> f[0])
            .toList();
    
    IO.println(fibonacci);
}
```

The `iterate` method can generate complex sequences by maintaining state in the  
seed value. This example generates Fibonacci numbers by carrying forward the  
last two values in an array. The state is immutable, with each iteration  
creating new objects.  

## Creating streams with ofNullable

This example shows creating streams from potentially null values.  

```java
void main() {

    String value1 = "Hello";
    String value2 = null;
    
    var count = Stream.of(value1, value2)
            .flatMap(Stream::ofNullable)
            .count();
    
    IO.println("Non-null count: " + count);
}
```

The `Stream.ofNullable` method (Java 9+) creates a stream with a single  
element if the value is non-null, or an empty stream if null. Combined with  
`flatMap`, this cleanly filters out null values from a stream without explicit  
null checks.  

## MapToInt for primitive conversion

This example demonstrates converting to IntStream.  

```java
void main() {

    var words = List.of("apple", "banana", "cherry", "date");
    var totalLength = words.stream()
            .mapToInt(String::length)
            .sum();
    
    IO.println("Total length: " + totalLength);
}
```

The `mapToInt` method converts a stream to an IntStream by applying a function  
that returns int values. This enables use of primitive stream operations like  
`sum` and `average` which are more efficient than operating on boxed integers.  

## MapToDouble for floating point operations

This example shows converting to DoubleStream.  

```java
void main() {

    var prices = List.of(19.99, 29.99, 9.99, 49.99);
    var average = prices.stream()
            .mapToDouble(p -> p)
            .average();
    
    average.ifPresent(avg -> 
            IO.println("Average price: $" + avg));
}
```

The `mapToDouble` method converts a stream to a DoubleStream. This is useful  
for mathematical operations on decimal values. DoubleStream provides methods  
like `average` that return OptionalDouble for precise floating-point  
calculations.  

## MapToLong for large numbers

This example demonstrates converting to LongStream.  

```java
void main() {

    var timestamps = List.of(
            java.time.Instant.now(),
            java.time.Instant.now().plusSeconds(60),
            java.time.Instant.now().plusSeconds(120)
    );
    
    var epochSeconds = timestamps.stream()
            .mapToLong(java.time.Instant::getEpochSecond)
            .toArray();
    
    IO.println(Arrays.toString(epochSeconds));
}
```

The `mapToLong` method converts a stream to a LongStream. This is important  
when working with large integer values that exceed int range, such as  
timestamps, file sizes, or database IDs.  

## Reducing to boolean

This example shows custom reduction to a boolean result.  

```java
void main() {

    var numbers = List.of(2, 4, 6, 8, 10);
    var allEven = numbers.stream()
            .reduce(true, 
                    (acc, n) -> acc && (n % 2 == 0),
                    (a, b) -> a && b);
    
    IO.println("All even: " + allEven);
}
```

The three-argument `reduce` method works with parallel streams by providing a  
combiner function. The identity value is used for each parallel chunk, and the  
combiner merges results. This demonstrates reduction to boolean, though  
`allMatch` is simpler for this specific case.  

## FlatMapToInt for nested primitives

This example demonstrates flattening to primitive stream.  

```java
void main() {

    var lists = List.of(
            List.of(1, 2, 3),
            List.of(4, 5),
            List.of(6, 7, 8)
    );
    
    var sum = lists.stream()
            .flatMapToInt(list -> list.stream().mapToInt(i -> i))
            .sum();
    
    IO.println("Sum of all numbers: " + sum);
}
```

The `flatMapToInt` method flattens nested structures directly to an IntStream.  
This is more efficient than using `flatMap` followed by `mapToInt` when  
working with nested collections of numbers that need primitive stream  
operations.  

## Collecting with custom collector

This example shows creating a custom collection strategy.  

```java
void main() {

    var words = List.of("apple", "banana", "cherry", "date");
    var result = words.stream()
            .collect(
                    StringBuilder::new,
                    (sb, s) -> sb.append(s).append(" "),
                    StringBuilder::append
            );
    
    IO.println(result.toString().trim());
}
```

The three-argument `collect` method provides low-level control over collection.  
The first argument creates the container, the second accumulates elements, and  
the third combines containers for parallel streams. This offers maximum  
flexibility for custom collection logic.  

## Grouping with downstream collectors

This example demonstrates grouping with additional aggregation.  

```java
record Product(String category, double price) {}

void main() {

    var products = List.of(
            new Product("Electronics", 599.99),
            new Product("Electronics", 399.99),
            new Product("Books", 29.99),
            new Product("Books", 19.99)
    );
    
    var avgPricesByCategory = products.stream()
            .collect(Collectors.groupingBy(
                    Product::category,
                    Collectors.averagingDouble(Product::price)
            ));
    
    avgPricesByCategory.forEach((cat, avg) -> 
            IO.println(cat + ": $" + avg));
}
```

The `groupingBy` collector can accept a downstream collector to further process  
each group. Here, `averagingDouble` computes the average price within each  
category. This enables complex aggregations in a single stream pipeline.  

## Filtering after grouping

This example shows post-grouping filtering.  

```java
void main() {

    var items = List.of("apple", "apricot", "banana", "avocado", 
                        "cherry", "almond");
    
    var grouped = items.stream()
            .collect(Collectors.groupingBy(
                    s -> s.charAt(0),
                    Collectors.filtering(
                            s -> s.length() > 5,
                            Collectors.toList()
                    )
            ));
    
    grouped.forEach((letter, words) -> 
            IO.println(letter + ": " + words));
}
```

The `filtering` collector (Java 9+) applies a filter within the downstream  
collector of a grouping operation. This allows filtering elements within each  
group rather than filtering before grouping, which can produce different  
results.  

## Mapping after grouping

This example demonstrates transforming grouped elements.  

```java
void main() {

    var words = List.of("apple", "apricot", "banana", "cherry");
    
    var grouped = words.stream()
            .collect(Collectors.groupingBy(
                    s -> s.length(),
                    Collectors.mapping(
                            String::toUpperCase,
                            Collectors.toList()
                    )
            ));
    
    grouped.forEach((len, words_) -> 
            IO.println(len + ": " + words_));
}
```

The `mapping` collector applies a transformation function to elements before  
collecting them. When used with `groupingBy`, it transforms elements within  
each group. This is useful for extracting or converting data during the  
grouping process.  

## Flat mapping in collectors

This example shows flattening during collection.  

```java
void main() {

    var sentences = List.of(
            "Hello world",
            "Java streams",
            "Functional programming"
    );
    
    var wordsByLength = sentences.stream()
            .collect(Collectors.groupingBy(
                    String::length,
                    Collectors.flatMapping(
                            s -> Arrays.stream(s.split(" ")),
                            Collectors.toList()
                    )
            ));
    
    wordsByLength.forEach((len, words) -> 
            IO.println(len + ": " + words));
}
```

The `flatMapping` collector (Java 9+) applies a function that returns a stream  
and flattens the results. This is useful when grouping elements that themselves  
contain multiple values, such as splitting sentences into words while grouping  
by sentence length.  

## Finding minimum in grouped data

This example demonstrates finding minimums within groups.  

```java
record Sale(String product, double amount) {}

void main() {

    var sales = List.of(
            new Sale("Laptop", 999.99),
            new Sale("Laptop", 899.99),
            new Sale("Phone", 699.99),
            new Sale("Phone", 599.99)
    );
    
    var minPrices = sales.stream()
            .collect(Collectors.groupingBy(
                    Sale::product,
                    Collectors.minBy(
                            Comparator.comparing(Sale::amount)
                    )
            ));
    
    minPrices.forEach((product, sale) -> 
            sale.ifPresent(s -> 
                    IO.println(product + ": $" + s.amount())));
}
```

The `minBy` collector finds the minimum element in each group according to a  
comparator. It returns an Optional since a group might be empty. This is useful  
for finding best prices, earliest dates, or smallest values within categories.  

## Counting elements in groups

This example shows counting elements within each group.  

```java
void main() {

    var words = List.of("apple", "banana", "apricot", "cherry", 
                        "avocado", "blueberry");
    
    var counts = words.stream()
            .collect(Collectors.groupingBy(
                    s -> s.charAt(0),
                    Collectors.counting()
            ));
    
    counts.forEach((letter, count) -> 
            IO.println(letter + ": " + count + " words"));
}
```

The `counting` collector counts elements in each group created by `groupingBy`.  
This is more efficient than collecting to lists and calling `size`. It's useful  
for frequency analysis and understanding data distribution.  

## Summing in groups

This example demonstrates calculating sums within groups.  

```java
record Order(String customer, double amount) {}

void main() {

    var orders = List.of(
            new Order("Alice", 50.00),
            new Order("Bob", 75.00),
            new Order("Alice", 30.00),
            new Order("Bob", 45.00)
    );
    
    var totals = orders.stream()
            .collect(Collectors.groupingBy(
                    Order::customer,
                    Collectors.summingDouble(Order::amount)
            ));
    
    totals.forEach((customer, total) -> 
            IO.println(customer + ": $" + total));
}
```

The `summingDouble` collector calculates the sum of a numeric field within each  
group. Similar collectors exist for int and long values. This is ideal for  
aggregating financial data, counts, or other numeric metrics by category.  

## Concatenating strings in groups

This example shows joining strings within groups.  

```java
void main() {

    var words = List.of("apple", "apricot", "banana", "blueberry", 
                        "cherry");
    
    var grouped = words.stream()
            .collect(Collectors.groupingBy(
                    s -> s.charAt(0),
                    Collectors.joining(", ")
            ));
    
    grouped.forEach((letter, joined) -> 
            IO.println(letter + ": " + joined));
}
```

The `joining` collector concatenates strings within each group with a  
delimiter. This is cleaner than collecting to lists and manually joining. It's  
useful for creating comma-separated lists or formatted output from grouped  
text data.  

## Collecting to concurrent maps

This example demonstrates thread-safe collection.  

```java
void main() {

    var numbers = IntStream.rangeClosed(1, 100)
            .parallel()
            .boxed()
            .collect(Collectors.groupingByConcurrent(
                    n -> n % 10
            ));
    
    IO.println("Groups: " + numbers.size());
    numbers.forEach((key, values) -> 
            IO.println(key + ": " + values.size() + " elements"));
}
```

The `groupingByConcurrent` collector creates a ConcurrentMap, which is  
thread-safe for parallel streams. When using parallel processing with  
collectors, concurrent versions prevent synchronization overhead and potential  
race conditions.  

## Creating custom intermediate operations

This example shows chaining with custom logic.  

```java
void main() {

    var numbers = IntStream.rangeClosed(1, 20)
            .filter(n -> n % 2 == 0)
            .filter(n -> n % 3 == 0)
            .map(n -> n * n)
            .limit(3)
            .toArray();
    
    IO.println(Arrays.toString(numbers));
}
```

Multiple intermediate operations can be chained to create complex  
transformations. Each operation returns a new stream, allowing fluent method  
chaining. The operations are lazy and won't execute until a terminal operation  
is called.  

## Using reduce with complex objects

This example demonstrates reduction on custom types.  

```java
record Account(String name, double balance) {}

void main() {

    var accounts = List.of(
            new Account("Savings", 1000.00),
            new Account("Checking", 500.00),
            new Account("Investment", 2500.00)
    );
    
    var totalBalance = accounts.stream()
            .map(Account::balance)
            .reduce(0.0, Double::sum);
    
    IO.println("Total balance: $" + totalBalance);
}
```

Reduction can extract fields from objects and aggregate them. The `map`  
operation first extracts the numeric field, then `reduce` combines the values.  
This pattern is common for calculating totals, averages, or other aggregations  
from object properties.  

## Collecting with custom map supplier

This example shows using specific map implementations.  

```java
void main() {

    var words = List.of("banana", "apple", "cherry", "date");
    
    var sorted = words.stream()
            .collect(Collectors.toMap(
                    s -> s,
                    String::length,
                    (v1, v2) -> v1,
                    TreeMap::new
            ));
    
    sorted.forEach((word, length) -> 
            IO.println(word + ": " + length));
}
```

The `toMap` collector can accept a map supplier to specify the map  
implementation. Using TreeMap creates a sorted map, while LinkedHashMap  
preserves insertion order. This provides control over the resulting map's  
characteristics.  

## Handling null values in streams

This example demonstrates filtering null values.  

```java
void main() {

    var items = List.of("apple", null, "banana", null, "cherry");
    
    var nonNull = items.stream()
            .filter(Objects::nonNull)
            .toList();
    
    IO.println(nonNull);
}
```

The `Objects.nonNull` method reference is a clean way to filter null values  
from a stream. This is safer than using a lambda like `s -> s != null` and  
makes the intent clear. It's essential when dealing with potentially incomplete  
data.  

## Converting stream to array with type

This example shows creating typed arrays from streams.  

```java
void main() {

    var words = List.of("apple", "banana", "cherry");
    var array = words.stream()
            .filter(s -> s.length() > 5)
            .toArray(String[]::new);
    
    IO.println(Arrays.toString(array));
}
```

The `toArray` method can accept an IntFunction that creates an array of the  
desired type. Using a constructor reference like `String[]::new` creates a  
properly typed array instead of Object[]. This is important for type safety and  
avoiding ClassCastException.  

## Reversing stream order

This example demonstrates reversing element order.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    var reversed = numbers.stream()
            .sorted(Comparator.reverseOrder())
            .toList();
    
    IO.println(reversed);
}
```

Streams don't have a built-in reverse operation, but sorting with  
`reverseOrder` achieves the same effect. For maintaining original order while  
reversing, you could collect to a list and use Collections.reverse, though this  
requires two passes.  

## Stream from regex patterns

This example shows creating streams from pattern matches.  

```java
void main() {

    var text = "The quick brown fox jumps over the lazy dog";
    var pattern = Pattern.compile("\\w+");
    
    var words = pattern.matcher(text)
            .results()
            .map(MatchResult::group)
            .toList();
    
    IO.println(words);
}
```

The Pattern.matcher method combined with `results` creates a stream of match  
results. This provides a functional approach to regex matching instead of  
traditional while loops with Matcher.find. Each result can be further processed  
using stream operations.  

## Stream from CharSequence

This example demonstrates streaming characters.  

```java
void main() {

    var text = "Hello, World!";
    var vowelCount = text.chars()
            .mapToObj(c -> (char) c)
            .filter(c -> "AEIOUaeiou".indexOf(c) >= 0)
            .count();
    
    IO.println("Vowel count: " + vowelCount);
}
```

The `chars` method creates an IntStream of character values from a string.  
Converting to char with `mapToObj` allows character-level operations. This is  
useful for analyzing text, counting specific characters, or transforming  
strings character by character.  

## Conditional collection

This example shows collecting based on a condition.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    var useFilter = true;
    
    var result = numbers.stream();
    if (useFilter) {
        result = result.filter(n -> n % 2 == 0);
    }
    
    var collected = result.toList();
    IO.println(collected);
}
```

Stream operations can be conditionally applied by assigning the stream to a  
variable and adding operations based on conditions. This enables dynamic  
pipeline construction, though be careful not to reuse streams after terminal  
operations.  

## Generating ranges

This example demonstrates creating numeric ranges.  

```java
void main() {

    var range1 = IntStream.range(1, 10).toArray();
    IO.println("Exclusive: " + Arrays.toString(range1));
    
    var range2 = IntStream.rangeClosed(1, 10).toArray();
    IO.println("Inclusive: " + Arrays.toString(range2));
}
```

The `range` method creates a stream from start (inclusive) to end (exclusive),  
while `rangeClosed` includes both endpoints. This distinction is important for  
loop replacement and iteration. These methods are more expressive than  
traditional for loops for simple iterations.  

## Limiting infinite streams

This example shows controlling infinite stream size.  

```java
void main() {

    var random = new Random();
    var randomNumbers = Stream
            .generate(random::nextInt)
            .limit(10)
            .toList();
    
    IO.println(randomNumbers);
}
```

Infinite streams generated by `generate` or `iterate` must be limited to  
prevent endless processing. The `limit` operation makes the stream finite. This  
pattern is useful for generating test data, random sampling, or producing  
sequences on demand.  

## Merging multiple streams

This example demonstrates concatenating streams.  

```java
void main() {

    var stream1 = Stream.of(1, 2, 3);
    var stream2 = Stream.of(4, 5, 6);
    var stream3 = Stream.of(7, 8, 9);
    
    var merged = Stream.concat(
            Stream.concat(stream1, stream2),
            stream3
    ).toList();
    
    IO.println(merged);
}
```

The `Stream.concat` method merges two streams sequentially. For more than two  
streams, nest concat calls or use flatMap with a stream of streams. Note that  
streams can only be consumed once, so ensure source streams aren't reused.  

## Empty streams

This example shows creating and handling empty streams.  

```java
void main() {

    var empty = Stream.<String>empty();
    var count = empty.count();
    
    IO.println("Empty stream count: " + count);
    
    var result = Stream.<Integer>empty()
            .findFirst()
            .orElse(-1);
    
    IO.println("Default value: " + result);
}
```

The `Stream.empty` method creates an empty stream of a specified type. Empty  
streams are useful as defaults in methods that return streams, or for  
conditional logic. Terminal operations on empty streams return empty Optionals  
or default values.  

## Builder pattern for streams

This example demonstrates building streams incrementally.  

```java
void main() {

    var builder = Stream.<String>builder();
    builder.add("apple");
    builder.add("banana");
    builder.add("cherry");
    
    var stream = builder.build();
    stream.forEach(IO::println);
}
```

The Stream.Builder allows constructing streams by adding elements one at a  
time. After calling `build`, no more elements can be added. This is useful when  
generating streams programmatically where the elements aren't known upfront or  
come from different sources.

