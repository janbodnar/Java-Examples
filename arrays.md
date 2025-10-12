# Java Arrays

This document provides comprehensive coverage of Java arrays using modern  
Java 25 syntax, including compact source files, instance main methods, and  
implicit imports.  

Arrays are fundamental data structures that hold a fixed number of values of  
a single type. Unlike scalar variables that store only one value, arrays can  
store multiple items called elements. Each element is accessed by its index,  
with array indices starting at zero. Once created, an array's length is fixed  
and cannot be changed, making arrays ideal for situations where the number of  
elements is known in advance.  

Java arrays are objects, allocated on the heap, and accessed through  
references. They provide fast constant-time access to elements by index,  
making them efficient for random access operations. Arrays can store both  
primitive types (int, double, char, etc.) and reference types (String,  
custom objects). Multi-dimensional arrays are supported through arrays of  
arrays, enabling representation of matrices, tables, and complex data  
structures.  

The `Arrays` class in `java.util` provides numerous utility methods for  
working with arrays, including sorting, searching, comparing, filling, and  
copying. Modern Java encourages using the `var` keyword for type inference  
and the `IO` class for simplified input/output. While arrays are powerful,  
collections like `ArrayList` offer more flexibility for dynamic data  
structures, though arrays remain essential for performance-critical code and  
interoperability with legacy systems.  

## Creating arrays with new keyword

This example demonstrates creating an array with the new keyword and  
initializing it element by element.  

```java
void main() {

    var numbers = new int[5];
    
    numbers[0] = 1;
    numbers[1] = 2;
    numbers[2] = 3;
    numbers[3] = 4;
    numbers[4] = 5;
    
    IO.println(Arrays.toString(numbers));
}
```

Arrays are created using the `new` keyword followed by the type and size in  
brackets. Each element is then assigned a value using its zero-based index.  
The `Arrays.toString` method converts the array to a readable string format,  
which is useful for debugging and displaying array contents.  

## Array literal initialization

This example shows how to create and initialize an array in one statement  
using array literals.  

```java
void main() {

    var values = new int[] { 2, 4, 5, 6, 7, 3, 2 };
    IO.println(Arrays.toString(values));
    
    var simplified = { 10, 20, 30, 40, 50 };
    IO.println(Arrays.toString(simplified));
}
```

Array literals use curly braces to specify elements at creation time. The  
first form explicitly states the type with `new int[]`, while the simplified  
form omits this when the type can be inferred. Both approaches create the  
array in a single statement, making the code more concise and readable.  

## Accessing array elements

This example demonstrates accessing individual array elements by their index.  

```java
void main() {

    var names = new String[] {"Jane", "Thomas", "Lucy", "David"};
    
    IO.println(names[0]);
    IO.println(names[1]);
    IO.println(names[2]);
    IO.println(names[3]);
}
```

Array elements are accessed using square brackets with a zero-based index.  
The first element is at index 0, the second at index 1, and so on. Attempting  
to access an index outside the valid range (0 to length-1) throws an  
`ArrayIndexOutOfBoundsException`.  

## Modifying array elements

This example shows how to change values stored in an array.  

```java
void main() {

    var values = new int[] { 1, 2, 3 };
    
    values[0] *= 2;
    values[1] *= 2;
    values[2] *= 2;
    
    IO.println(Arrays.toString(values));
}
```

Array elements are mutable and can be modified after creation. Using index  
notation, each element is accessed and updated with a new value. This example  
demonstrates in-place modification by doubling each value, showing that  
arrays support both read and write operations.  

## Traversing with for loop

This example shows how to iterate through an array using a traditional for  
loop and an enhanced for-each loop.  

```java
void main() {

    var planets = new String[] { "Mercury", "Venus", "Mars", "Earth", 
            "Jupiter", "Saturn", "Uranus", "Neptune", "Pluto" };
    
    for (int i = 0; i < planets.length; i++) {
        IO.println(planets[i]);
    }
    
    IO.println("---");
    
    for (var planet : planets) {
        IO.println(planet);
    }
}
```

The traditional for loop uses an index variable to access each element,  
leveraging the array's `length` property. The enhanced for-each loop provides  
a more concise syntax for iteration, automatically handling the index. The  
for-each loop is preferred when you don't need the index value itself.  

## Passing arrays to functions

This example demonstrates passing an array to a function and returning a new  
array.  

```java
void main() {

    var original = new int[] { 3, 4, 5, 6, 7 };
    var reversed = reverseArray(original);
    
    IO.println(Arrays.toString(original));
    IO.println(Arrays.toString(reversed));
}

int[] reverseArray(int[] input) {

    var result = new int[input.length];
    
    for (int i = input.length - 1, j = 0; i >= 0; i--, j++) {
        result[j] = input[i];
    }
    
    return result;
}
```

Arrays can be passed to functions as parameters and returned as results.  
When an array is passed, the function receives a reference to the original  
array, not a copy. This example creates a new array to avoid modifying the  
original, demonstrating defensive programming when reversing elements.  

## Two-dimensional arrays

This example demonstrates creating and traversing a two-dimensional array.  

```java
void main() {

    var matrix = new int[][] { { 1, 2, 3 }, { 4, 5, 6 } };
    
    var rows = matrix.length;
    var cols = matrix[0].length;
    
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            IO.print(matrix[i][j] + " ");
        }
        IO.println();
    }
}
```

Two-dimensional arrays are arrays of arrays, creating a matrix-like structure.  
Each element is accessed using two indices: the first for the row and the  
second for the column. Nested loops are commonly used to iterate through all  
elements in a 2D array.  

## Three-dimensional arrays

This example shows how to work with three-dimensional arrays.  

```java
void main() {

    var cube = new int[][][] {
        { { 12, 2, 8 }, { 0, 2, 1 } },
        { { 14, 5, 2 }, { 0, 5, 4 } },
        { { 3, 26, 9 }, { 8, 7, 1 } },
        { { 4, 11, 2 }, { 0, 9, 6 } }
    };
    
    var dim1 = cube.length;
    var dim2 = cube[0].length;
    var dim3 = cube[0][0].length;
    
    for (int i = 0; i < dim1; i++) {
        for (int j = 0; j < dim2; j++) {
            for (int k = 0; k < dim3; k++) {
                IO.print(cube[i][j][k] + " ");
            }
        }
    }
    IO.println();
}
```

Three-dimensional arrays extend the concept further, creating cube-like  
structures useful for representing 3D space, RGB color data, or complex  
scientific datasets. Three nested loops are required to access all elements,  
with each index representing a different dimension of the data structure.  

## Jagged arrays

This example demonstrates creating arrays with rows of different lengths.  

```java
void main() {

    var jagged = new int[][] {
        { 1, 2 },
        { 1, 2, 3 },
        { 1, 2, 3, 4 }
    };
    
    for (var row : jagged) {
        for (var element : row) {
            IO.print(element + " ");
        }
        IO.println();
    }
}
```

Jagged arrays (also called irregular arrays) have rows of varying lengths,  
unlike rectangular arrays where all rows have the same size. This is possible  
because Java implements multi-dimensional arrays as arrays of arrays, allowing  
each sub-array to have its own independent length.  

## Sorting arrays

This example shows how to sort array elements in ascending order.  

```java
void main() {

    var numbers = new int[] { 5, 2, 4, 3, 1 };
    
    Arrays.sort(numbers);
    IO.println(Arrays.toString(numbers));
    
    var words = new String[] { "zebra", "apple", "mango", "cherry" };
    Arrays.sort(words);
    IO.println(Arrays.toString(words));
}
```

The `Arrays.sort` method arranges elements in ascending natural order. For  
numbers, this means from smallest to largest; for strings, it means  
alphabetical order. The sort happens in-place, modifying the original array  
without creating a new one.  

## Filling arrays

This example demonstrates filling an array with a specific value.  

```java
void main() {

    var data = new int[10];
    
    Arrays.fill(data, 7);
    IO.println(Arrays.toString(data));
    
    Arrays.fill(data, 2, 5, 99);
    IO.println(Arrays.toString(data));
}
```

The `Arrays.fill` method sets all elements to a specified value. The  
overloaded version allows filling a specific range by specifying start  
(inclusive) and end (exclusive) indices. This is useful for initializing  
arrays with default values or resetting portions of an array.  

## Copying arrays

This example shows different ways to copy array data.  

```java
void main() {

    var original = new int[] { 1, 2, 3, 4, 5 };
    
    var copy1 = Arrays.copyOf(original, 5);
    IO.println(Arrays.toString(copy1));
    
    var copy2 = Arrays.copyOf(original, 8);
    IO.println(Arrays.toString(copy2));
    
    var copy3 = Arrays.copyOfRange(original, 1, 4);
    IO.println(Arrays.toString(copy3));
}
```

The `Arrays.copyOf` method creates a new array with the specified length,  
copying elements from the source. If the new length exceeds the original,  
extra positions are filled with default values (0 for integers). The  
`copyOfRange` method copies a specific portion of the array.  

## Comparing arrays

This example demonstrates comparing arrays for equality.  

```java
void main() {

    var arr1 = new int[] { 1, 2, 3, 4, 5 };
    var arr2 = new int[] { 1, 2, 3, 4, 5 };
    var arr3 = new int[] { 5, 4, 3, 2, 1 };
    
    IO.println("arr1 equals arr2: " + Arrays.equals(arr1, arr2));
    IO.println("arr1 equals arr3: " + Arrays.equals(arr1, arr3));
}
```

The `Arrays.equals` method compares two arrays element by element, returning  
true only if both arrays have the same length and all corresponding elements  
are equal. This is different from using `==`, which only checks if both  
variables reference the exact same array object.  

## Deep comparison of nested arrays

This example shows how to compare multi-dimensional arrays.  

```java
void main() {

    var array1 = new int[][] { { 1, 1, 2 }, { 0, 0, 3 } };
    var refs = new int[] { 1, 1, 2 };
    var refs2 = new int[] { 0, 0, 3 };
    var array2 = new int[][] { refs, refs2 };
    
    IO.println("equals: " + Arrays.equals(array1, array2));
    IO.println("deepEquals: " + Arrays.deepEquals(array1, array2));
}
```

The `Arrays.deepEquals` method recursively compares nested arrays, checking  
the actual element values rather than just array references. This is essential  
for multi-dimensional arrays where `equals` only compares the first level of  
references, not the actual contained data.  

## Binary search in sorted arrays

This example demonstrates searching for elements using binary search.  

```java
void main() {

    var planets = new String[] { "Mercury", "Venus", "Mars", "Earth", 
            "Jupiter", "Saturn", "Uranus", "Neptune", "Pluto" };
    
    Arrays.sort(planets);
    
    var target = "Earth";
    var index = Arrays.binarySearch(planets, target);
    
    if (index >= 0) {
        IO.println(target + " found at index " + index);
    } else {
        IO.println(target + " not found");
    }
}
```

The `Arrays.binarySearch` method efficiently searches sorted arrays using the  
binary search algorithm, which has O(log n) time complexity. The array must be  
sorted before searching. If found, it returns the element's index; otherwise,  
it returns a negative value indicating the insertion point.  

## Array length property

This example shows how to get the size of an array.  

```java
void main() {

    var colors = new String[] { "red", "green", "blue", "yellow" };
    
    IO.println("Array length: " + colors.length);
    
    var matrix = new int[][] { { 1, 2, 3 }, { 4, 5, 6 } };
    IO.println("Rows: " + matrix.length);
    IO.println("Columns: " + matrix[0].length);
}
```

Arrays have a `length` property (not a method) that returns the number of  
elements. For multi-dimensional arrays, each level has its own length. This  
is commonly used in loops to iterate through all elements without hardcoding  
the size.  

## Converting arrays to strings

This example demonstrates different ways to display array contents.  

```java
void main() {

    var numbers = new int[] { 10, 20, 30, 40, 50 };
    
    IO.println(Arrays.toString(numbers));
    
    var matrix = new int[][] { { 1, 2 }, { 3, 4 }, { 5, 6 } };
    IO.println(Arrays.deepToString(matrix));
}
```

The `Arrays.toString` method creates a readable string representation of a  
one-dimensional array. For multi-dimensional arrays, use `deepToString` to  
recursively convert nested arrays. These methods are invaluable for debugging  
and logging array contents.  

## Finding minimum and maximum values

This example shows how to find the smallest and largest elements in an array.  

```java
void main() {

    var values = new int[] { 23, 7, 42, 15, 8, 91, 33 };
    
    var min = Arrays.stream(values).min().getAsInt();
    var max = Arrays.stream(values).max().getAsInt();
    
    IO.println("Minimum: " + min);
    IO.println("Maximum: " + max);
}
```

Using streams, we can efficiently find minimum and maximum values. The  
`Arrays.stream` method converts an array to a stream, enabling functional  
operations like `min` and `max`. The `getAsInt` method extracts the value from  
the OptionalInt result.  

## Checking if array contains element

This example demonstrates searching for a specific value in an array.  

```java
void main() {

    var fruits = new String[] { "apple", "banana", "cherry", "date" };
    
    var searchTerm = "banana";
    var found = Arrays.asList(fruits).contains(searchTerm);
    
    IO.println("Contains " + searchTerm + ": " + found);
}
```

Converting an array to a list with `Arrays.asList` provides access to the  
`contains` method for simple existence checks. Alternatively, streams can be  
used with `anyMatch` for more complex conditions. This approach is simpler  
than manually looping through the array.  

## Summing array elements

This example shows how to calculate the sum of array elements.  

```java
void main() {

    var numbers = new int[] { 10, 20, 30, 40, 50 };
    
    var sum = Arrays.stream(numbers).sum();
    IO.println("Sum: " + sum);
    
    var average = Arrays.stream(numbers).average().getAsDouble();
    IO.println("Average: " + average);
}
```

Streams provide convenient methods for numeric operations. The `sum` method  
adds all elements, while `average` computes the mean value. These functional  
approaches are more concise and expressive than traditional loop-based  
calculations.  

## Filtering array elements

This example demonstrates selecting elements that match a condition.  

```java
void main() {

    var numbers = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    
    var evens = Arrays.stream(numbers)
        .filter(n -> n % 2 == 0)
        .toArray();
    
    IO.println(Arrays.toString(evens));
}
```

The `filter` method creates a stream containing only elements matching the  
predicate. This example extracts even numbers using a lambda expression. The  
`toArray` method converts the filtered stream back to an array. Stream  
filtering is more readable than manual loop-based selection.  

## Mapping array elements

This example shows how to transform each element in an array.  

```java
void main() {

    var numbers = new int[] { 1, 2, 3, 4, 5 };
    
    var squared = Arrays.stream(numbers)
        .map(n -> n * n)
        .toArray();
    
    IO.println(Arrays.toString(squared));
}
```

The `map` method applies a transformation function to each element, creating a  
new stream with the transformed values. This example squares each number. The  
functional approach separates the transformation logic from the iteration  
mechanism, improving code clarity.  

## Creating arrays with default values

This example demonstrates initializing arrays with computed default values.  

```java
void main() {

    var sequence = new int[10];
    for (int i = 0; i < sequence.length; i++) {
        sequence[i] = i * 2;
    }
    IO.println(Arrays.toString(sequence));
    
    var powers = IntStream.range(0, 5)
        .map(i -> (int) Math.pow(2, i))
        .toArray();
    IO.println(Arrays.toString(powers));
}
```

Arrays can be initialized with computed values using loops or streams. The  
traditional loop approach provides direct index access, while the stream  
approach using `IntStream.range` offers a more functional style. Both methods  
are useful depending on the complexity of the initialization logic.  

## Reversing array elements

This example shows how to reverse the order of elements in an array.  

```java
void main() {

    var letters = new String[] { "a", "b", "c", "d", "e" };
    
    var reversed = IntStream.rangeClosed(1, letters.length)
        .mapToObj(i -> letters[letters.length - i])
        .toArray(String[]::new);
    
    IO.println(Arrays.toString(reversed));
}
```

Reversing an array can be done by iterating from the end to the beginning.  
This stream-based approach uses `rangeClosed` to generate indices in reverse  
order. The `mapToObj` method maps each index to the corresponding element,  
creating a reversed copy without modifying the original.  

## Removing duplicates from arrays

This example demonstrates creating an array with only unique elements.  

```java
void main() {

    var numbers = new int[] { 1, 2, 2, 3, 3, 3, 4, 4, 5 };
    
    var unique = Arrays.stream(numbers)
        .distinct()
        .toArray();
    
    IO.println(Arrays.toString(unique));
}
```

The `distinct` method removes duplicate elements, keeping only the first  
occurrence of each value. This uses the element's `equals` method to determine  
equality. The result maintains the original order of first occurrences,  
providing a clean way to eliminate redundancy.  

## Partitioning arrays

This example shows how to split an array into chunks of a specific size.  

```java
void main() {

    var data = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    var chunkSize = 3;
    
    for (int i = 0; i < data.length; i += chunkSize) {
        var end = Math.min(i + chunkSize, data.length);
        var chunk = Arrays.copyOfRange(data, i, end);
        IO.println(Arrays.toString(chunk));
    }
}
```

Partitioning divides an array into smaller segments of a specified size. The  
loop advances by the chunk size, using `copyOfRange` to extract each segment.  
The `Math.min` ensures the last chunk doesn't exceed the array bounds. This  
is useful for batch processing or pagination.  

## Concatenating arrays

This example demonstrates combining multiple arrays into one.  

```java
void main() {

    var first = new int[] { 1, 2, 3 };
    var second = new int[] { 4, 5, 6 };
    
    var combined = IntStream.concat(
        Arrays.stream(first),
        Arrays.stream(second)
    ).toArray();
    
    IO.println(Arrays.toString(combined));
}
```

The `IntStream.concat` method merges two streams sequentially. This creates a  
new array containing all elements from both source arrays in order. For  
concatenating more than two arrays, nest `concat` calls or use `flatMap` with  
a stream of streams.  

## Rotating array elements

This example shows how to rotate array elements by a specified number of  
positions.  

```java
void main() {

    var items = new String[] { "a", "b", "c", "d", "e" };
    var rotations = 2;
    
    var rotated = IntStream.range(0, items.length)
        .mapToObj(i -> items[(i + rotations) % items.length])
        .toArray(String[]::new);
    
    IO.println(Arrays.toString(rotated));
}
```

Rotation shifts elements cyclically by a specified number of positions. The  
modulo operator wraps indices around when they exceed the array length. This  
technique is useful in circular buffers, scheduling algorithms, and various  
data processing tasks.  

## Swapping array elements

This example demonstrates exchanging the positions of two elements.  

```java
void main() {

    var values = new int[] { 10, 20, 30, 40, 50 };
    
    var index1 = 1;
    var index2 = 3;
    
    var temp = values[index1];
    values[index1] = values[index2];
    values[index2] = temp;
    
    IO.println(Arrays.toString(values));
}
```

Swapping requires a temporary variable to hold one value while the exchange  
occurs. This is a fundamental operation used in sorting algorithms and data  
manipulation. The three-step process ensures neither value is lost during the  
swap.  

## Finding array index of element

This example shows how to find the position of a specific value.  

```java
void main() {

    var colors = new String[] { "red", "green", "blue", "yellow" };
    var search = "blue";
    
    var index = IntStream.range(0, colors.length)
        .filter(i -> colors[i].equals(search))
        .findFirst()
        .orElse(-1);
    
    IO.println("Index of " + search + ": " + index);
}
```

Finding an element's index requires iterating until a match is found. This  
stream-based approach uses `filter` to find matching indices and `findFirst`  
to get the first occurrence. The `orElse(-1)` provides a default value when  
the element isn't found, following common convention.  

## Counting occurrences in arrays

This example demonstrates counting how many times a value appears.  

```java
void main() {

    var letters = new String[] { "a", "b", "a", "c", "a", "b" };
    var target = "a";
    
    var count = Arrays.stream(letters)
        .filter(s -> s.equals(target))
        .count();
    
    IO.println("Occurrences of " + target + ": " + count);
}
```

The `filter` method selects matching elements, and `count` returns the number  
of elements in the filtered stream. This provides an elegant way to count  
occurrences without manually maintaining a counter variable in a loop.  

## Shuffling array elements

This example shows how to randomly reorder array elements.  

```java
void main() {

    var cards = new String[] { "A", "2", "3", "4", "5", "6", "7", "8", 
            "9", "10", "J", "Q", "K" };
    
    var list = Arrays.asList(cards);
    java.util.Collections.shuffle(list);
    
    IO.println(Arrays.toString(cards));
}
```

Shuffling randomizes element order, useful for games, random sampling, and  
testing. Since arrays don't have a built-in shuffle method, we convert to a  
list, shuffle using `Collections.shuffle`, and the original array is modified  
since `asList` returns a view backed by the array.  

## Merging sorted arrays

This example demonstrates combining two sorted arrays into one sorted array.  

```java
void main() {

    var arr1 = new int[] { 1, 3, 5, 7 };
    var arr2 = new int[] { 2, 4, 6, 8 };
    
    var merged = IntStream.concat(
        Arrays.stream(arr1),
        Arrays.stream(arr2)
    ).sorted().toArray();
    
    IO.println(Arrays.toString(merged));
}
```

Merging sorted arrays can be done by concatenating them and then sorting. For  
better efficiency with large arrays, a manual merge algorithm that takes  
advantage of the pre-sorted order would be faster. This approach prioritizes  
simplicity and readability.  

## Array as function parameter with varargs

This example shows using variable-length argument lists.  

```java
void main() {

    printValues(1, 2, 3);
    printValues(10, 20, 30, 40, 50);
    
    var array = new int[] { 100, 200, 300 };
    printValues(array);
}

void printValues(int... numbers) {

    IO.println("Count: " + numbers.length);
    IO.println(Arrays.toString(numbers));
}
```

Varargs (variable arguments) allow passing any number of arguments of the same  
type. Java treats them as arrays internally. This provides flexibility for  
functions that need to accept varying numbers of parameters without requiring  
explicit array creation at the call site.  

## Cloning arrays

This example demonstrates creating a shallow copy of an array.  

```java
void main() {

    var original = new int[] { 1, 2, 3, 4, 5 };
    var cloned = original.clone();
    
    cloned[0] = 99;
    
    IO.println("Original: " + Arrays.toString(original));
    IO.println("Cloned: " + Arrays.toString(cloned));
}
```

The `clone` method creates a shallow copy of an array. For primitive arrays,  
this creates an independent copy. For arrays of objects, only the references  
are copied, not the objects themselves. Modifying the cloned array doesn't  
affect the original (for primitives).  

## Working with byte arrays

This example shows operations specific to byte arrays.  

```java
void main() {

    var text = "Hello, World!";
    var bytes = text.getBytes();
    
    IO.println("Byte array length: " + bytes.length);
    IO.println(Arrays.toString(bytes));
    
    var decoded = new String(bytes);
    IO.println("Decoded: " + decoded);
}
```

Byte arrays are commonly used for binary data, file I/O, and network  
communication. Strings can be converted to byte arrays using `getBytes`, and  
byte arrays can be converted back to strings using the String constructor.  
This is essential for character encoding operations.  

