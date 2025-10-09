
# Java List Examples

This document contains progressively complex Java examples demonstrating  
various List operations, methods, and patterns using modern Java 25 syntax.  

Lists are fundamental data structures in Java that represent ordered sequences  
of elements. The Java Collections Framework provides several implementations,  
with `ArrayList` being the most commonly used. Lists allow dynamic resizing,  
provide index-based access, and support a wide range of operations for  
managing collections of data. Unlike arrays, lists can grow and shrink as  
needed, making them ideal for situations where the number of elements is  
unknown or changes frequently.  

The `ArrayList` implementation provides fast random access with constant-time  
positional access and amortized constant-time insertion at the end. It's  
backed by a dynamic array that automatically expands when needed. Lists  
maintain the insertion order of elements and allow duplicate values, including  
`null`. Java 9 introduced convenient factory methods like `List.of()` for  
creating immutable lists, while modern Java emphasizes type inference with  
`var` and simplified syntax through implicit imports.  
## Adding elements
This example demonstrates adding elements to a list one by one.  
```java
void main() {
    var langs = new ArrayList<String>();
    
    langs.add("Java");
    langs.add("Python");
    langs.add(1, "C#");
    langs.add(0, "Ruby");
    
    for (var lang : langs) {
        IO.print(lang + " ");
    }
    IO.println();
}
```
The `add` method appends elements to the end of the list by default. The  
overloaded version `add(index, element)` inserts an element at a specific  
position, shifting subsequent elements to the right. Lists maintain insertion  
order, so elements appear in the sequence they were added.  

## Creating immutable lists
This example shows how to create immutable lists using factory methods.  
```java
void main() {
    var words = List.of("wood", "forest", "falcon", "eagle");
    IO.println(words);
    
    var values = List.of(1, 2, 3);
    IO.println(values);
}
```
Since Java 9, the `List.of` factory method provides a convenient way to create  
immutable lists with a handful of elements. These lists are compact, efficient,  
and throw `UnsupportedOperationException` if you attempt to modify them.  

## Accessing elements
This example demonstrates retrieving elements and getting the list size.  
```java
void main() {
    var colours = new ArrayList<String>();
    
    colours.add("blue");
    colours.add("orange");
    colours.add("red");
    colours.add("green");
    
    var col = colours.get(1);
    IO.println(col);
    
    var size = colours.size();
    IO.println("The size of the list is: " + size);
}
```
The `get` method retrieves an element at a specified index (zero-based), while  
the `size` method returns the total number of elements in the list. These are  
fundamental operations for working with list data.  

## Copying lists
This example shows how to create a copy of a list.  
```java
void main() {
    var words = List.of("forest", "wood", "eagle", "sky", "cloud");
    IO.println(words);
    
    var words2 = List.copyOf(words);
    IO.println(words2);
}
```
The `List.copyOf` method creates an immutable copy of the given collection.  
This is useful when you need to protect a list from modifications while  
sharing it across different parts of your application.  

## Raw lists
This example demonstrates creating lists that can hold multiple data types.  
```java
class Base {}

enum Level {
    EASY,
    MEDIUM,
    HARD
}

void main() {
    var level = Level.EASY;
    
    var da = new ArrayList();
    
    da.add("Java");
    da.add(3.5);
    da.add(55);
    da.add(new Base());
    da.add(level);
    
    for (var el : da) {
        IO.println(el);
    }
}
```
Raw lists can contain various data types, but this approach is generally not  
recommended. Without type parameters, raw lists lack type safety and often  
require casting. Modern Java code should prefer generics for type safety.  

## Adding multiple elements
This example shows how to add multiple elements in one operation.  
```java
void main() {
    var colours1 = new ArrayList<String>();
    colours1.add("blue");
    colours1.add("red");
    colours1.add("green");
    
    var colours2 = new ArrayList<String>();
    colours2.add("yellow");
    colours2.add("pink");
    colours2.add("brown");
    
    var colours3 = new ArrayList<String>();
    colours3.add("white");
    colours3.add("orange");
    
    colours3.addAll(colours1);
    colours3.addAll(2, colours2);
    
    for (var col : colours3) {
        IO.println(col);
    }
}
```
The `addAll` method adds all elements from a collection to the end of the list.  
The overloaded version `addAll(index, collection)` inserts all elements at a  
specific position, shifting existing elements to make room.  

## Modifying elements
This example demonstrates various methods for modifying list contents.  
```java
void main() {
    var items = new ArrayList<String>();
    fillList(items);
    
    items.set(3, "watch");
    items.add("bowl");
    items.remove(0);
    items.remove("pen");
    
    for (var el : items) {
        IO.println(el);
    }
    
    items.clear();
    
    if (items.isEmpty()) {
        IO.println("The list is empty");
    } else {
        IO.println("The list is not empty");
    }
}

void fillList(ArrayList<String> data) {
    data.add("coin");
    data.add("pen");
    data.add("pencil");
    data.add("clock");
    data.add("book");
    data.add("spectacles");
    data.add("glass");
}
```
The `set` method replaces an element at a given index. The `remove` method  
can delete by index or by value, removing the first occurrence. The `clear`  
method removes all elements, and `isEmpty` checks if the list has no elements.  

## Removing with predicates
This example shows how to remove elements based on a condition.  
```java
void main() {
    var values = new ArrayList<Integer>();
    values.add(5);
    values.add(-3);
    values.add(2);
    values.add(8);
    values.add(-2);
    values.add(6);
    
    values.removeIf(val -> val < 0);
    
    IO.println(values);
}
```
The `removeIf` method removes all elements that satisfy a given predicate.  
This is more concise and readable than manually iterating and removing  
elements that match a condition.  

## Removing all occurrences
This example demonstrates removing all instances of specific elements.  
```java
void main() {
    var letters = new ArrayList<String>();
    letters.add("a");
    letters.add("b");
    letters.add("c");
    letters.add("a");
    letters.add("d");
    
    IO.println(letters);
    
    letters.removeAll(Set.of("a"));
    IO.println(letters);
}
```
The `removeAll` method removes all elements that are contained in the  
specified collection. This is useful for bulk removal operations. The `clear`  
method removes all elements, while `removeAll` removes only matching ones.  

## Replacing all elements
This example shows how to transform all elements using an operator.  
```java
void main() {
    var items = new ArrayList<String>();
    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("class");
    
    items.replaceAll(x -> x.toUpperCase());
    
    IO.println(items);
}
```
The `replaceAll` method applies a function to each element, replacing it with  
the result. This is useful for batch transformations like case conversion,  
string formatting, or mathematical operations on numeric lists.  

## Capitalizing elements
This example demonstrates capitalizing the first letter of each string.  
```java
void main() {
    var items = new ArrayList<String>();
    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("glass");
    
    items.replaceAll(s -> {
        if (s == null || s.isEmpty()) {
            return s;
        }
        return s.substring(0, 1).toUpperCase() + s.substring(1);
    });
    
    IO.println(items);
}
```
This example uses `replaceAll` with a more complex lambda expression to  
capitalize each string. The lambda handles edge cases like null or empty  
strings before performing the transformation.  

## Checking for elements
This example demonstrates checking if a list contains a specific element.  
```java
void main() {
    var items = new ArrayList<String>();
    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("class");
    
    var item = "pen";
    
    if (items.contains(item)) {
        IO.println("There is a " + item + " in the list");
    }
}
```
The `contains` method returns `true` if the list contains the specified  
element, using the element's `equals` method for comparison. This is useful  
for membership tests before performing operations.  

## Finding element indices
This example shows how to find the index of elements in a list.  
```java
void main() {
    var colours = new ArrayList<String>();
    colours.add(0, "blue");
    colours.add(1, "orange");
    colours.add(2, "red");
    colours.add(3, "green");
    colours.add(4, "orange");
    
    var idx1 = colours.indexOf("orange");
    IO.println(idx1);
    
    var idx2 = colours.lastIndexOf("orange");
    IO.println(idx2);
}
```
The `indexOf` method returns the index of the first occurrence of an element,  
or -1 if not found. The `lastIndexOf` method returns the index of the last  
occurrence, useful when lists contain duplicate values.  

## Nested lists
This example demonstrates creating and working with lists of lists.  
```java
void main() {
    var l1 = new ArrayList<Integer>();
    l1.add(1);
    l1.add(2);
    l1.add(3);
    
    var l2 = new ArrayList<Integer>();
    l2.add(4);
    l2.add(5);
    l2.add(6);
    
    var l3 = new ArrayList<Integer>();
    l3.add(7);
    l3.add(8);
    l3.add(9);
    
    var nums = new ArrayList<ArrayList<Integer>>();
    nums.add(l1);
    nums.add(l2);
    nums.add(l3);
    
    IO.println(nums);
    
    for (var list : nums) {
        for (var n : list) {
            IO.print(n + " ");
        }
        IO.println();
    }
}
```
Lists can contain other lists, creating a two-dimensional structure. This is  
useful for representing matrices, grouped data, or hierarchical information.  
Nested loops are typically used to traverse all elements.  

## Creating sublists
This example shows how to create a view of a portion of a list.  
```java
void main() {
    var items = new ArrayList<String>();
    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("glass");
    items.add("chair");
    items.add("ball");
    items.add("bowl");
    
    var items2 = items.subList(2, 5);
    IO.println(items2);
    
    items2.set(0, "bottle");
    
    IO.println(items2);
    IO.println(items);
}
```
The `subList` method returns a view (not a copy) of a portion of the list  
between specified indices. Changes to the sublist are reflected in the  
original list and vice versa. The indices are inclusive at start, exclusive  
at end.  

## Iterating through lists
This example demonstrates different ways to traverse a list.  
```java
void main() {
    var nums = new ArrayList<Integer>();
    nums.add(2);
    nums.add(6);
    nums.add(7);
    nums.add(3);
    nums.add(1);
    nums.add(8);
    
    // Classic for loop
    for (var i = 0; i < nums.size(); i++) {
        IO.print(nums.get(i) + " ");
    }
    IO.println();
    
    // Enhanced for loop
    for (var num : nums) {
        IO.print(num + " ");
    }
    IO.println();
    
    // While loop
    var j = 0;
    while (j < nums.size()) {
        IO.print(nums.get(j) + " ");
        j++;
    }
    IO.println();
    
    // Iterator
    var it = nums.iterator();
    while(it.hasNext()) {
        IO.print(it.next() + " ");
    }
    IO.println();
    
    // forEach method
    nums.forEach(e -> IO.print(e + " "));
    IO.println();
}
```
Java provides multiple ways to iterate through lists: classic for loop with  
index, enhanced for-each loop, while loop, Iterator, and the functional  
`forEach` method. Each approach has its use cases depending on the need for  
index access, modification during iteration, or functional style.  

## Sorting with comparator
This example shows how to sort a list using a comparator.  
```java
record Person(int age, String name) {}

void main() {
    var persons = new ArrayList<Person>();
    persons.add(new Person(17, "Jane"));
    persons.add(new Person(32, "Peter"));
    persons.add(new Person(47, "Patrick"));
    persons.add(new Person(22, "Mary"));
    persons.add(new Person(39, "Robert"));
    persons.add(new Person(54, "Greg"));
    
    persons.sort((p1, p2) -> Integer.compare(p2.age(), p1.age()));
    
    IO.println(persons);
}
```
The `sort` method sorts a list according to a provided comparator. This  
example sorts persons by age in descending order using a lambda expression  
that compares age values. Comparators provide flexible sorting logic.  

## Sorting with streams
This example demonstrates sorting using the Stream API.  
```java
record Country(String name, int population) {}

void main() {
    var countries = new ArrayList<Country>();
    countries.add(new Country("Slovakia", 5424000));
    countries.add(new Country("Hungary", 9845000));
    countries.add(new Country("Poland", 38485000));
    countries.add(new Country("Germany", 81084000));
    countries.add(new Country("Latvia", 1978000));
    
    var sortedCountries = countries.stream()
            .sorted((e1, e2) -> Integer.compare(e1.population(), 
                    e2.population()))
            .toList();
    
    IO.println(sortedCountries);
}
```
The Stream API provides a powerful way to sort collections. The `stream`  
method creates a stream, `sorted` applies a comparator, and `toList` collects  
the results into a new list. This approach is functional and composable.  

## Converting between arrays and lists
This example shows how to convert between arrays and lists.  
```java
void main() {
    var planets = new String[] { "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Neptune" };
    
    var planetList = List.of(planets);
    IO.println(planetList);
    
    var planets2 = planetList.toArray(new String[0]);
    IO.println(java.util.Arrays.toString(planets2));
}
```
The `List.of` method creates an immutable list from an array, while the  
`toArray` method converts a list back to an array. These conversions are  
useful when working with APIs that expect different collection types.  

## Converting streams to lists
This example shows how to convert a stream to a list.  
```java
void main() {
    var words = java.util.stream.Stream.of("forest", "eagle", "river", 
            "cloud", "sky");
    
    var wordList = words.toList();
    IO.println(wordList.getClass());
    IO.println(wordList);
}
```
Java streams can be converted to lists using the `toList` method (Java 16+).  
This creates an immutable list from the stream elements. For mutable lists,  
use `collect(Collectors.toCollection(ArrayList::new))` instead.  

## Filtering lists
This example demonstrates filtering list elements based on a condition.  
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var evenNumbers = numbers.stream()
            .filter(n -> n % 2 == 0)
            .toList();
    
    IO.println(evenNumbers);
}
```
The `filter` method creates a stream containing only elements that match the  
given predicate. Combined with `toList`, this provides a clean way to extract  
matching elements from a list without modifying the original.  

## Mapping list elements
This example shows how to transform each element in a list.  
```java
void main() {
    var names = List.of("alice", "bob", "charlie", "david");
    
    var upperNames = names.stream()
            .map(String::toUpperCase)
            .toList();
    
    IO.println(upperNames);
}
```
The `map` method transforms each element using a provided function. This is  
useful for converting data types, extracting properties, or applying  
transformations across all elements in a functional style.  

## Finding elements
This example demonstrates finding specific elements in a list.  
```java
void main() {
    var numbers = List.of(3, 7, 12, 5, 9, 15, 8);
    
    var first = numbers.stream()
            .filter(n -> n > 10)
            .findFirst();
    
    if (first.isPresent()) {
        IO.println("First number > 10: " + first.get());
    }
    
    var any = numbers.stream()
            .filter(n -> n < 5)
            .findAny();
    
    if (any.isPresent()) {
        IO.println("Any number < 5: " + any.get());
    }
}
```
The `findFirst` method returns the first matching element wrapped in an  
Optional, while `findAny` returns any matching element. These are useful for  
searching without processing the entire collection.  

## Reducing lists
This example shows how to reduce a list to a single value.  
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5);
    
    var sum = numbers.stream()
            .reduce(0, (a, b) -> a + b);
    
    IO.println("Sum: " + sum);
    
    var product = numbers.stream()
            .reduce(1, (a, b) -> a * b);
    
    IO.println("Product: " + product);
}
```
The `reduce` method combines all elements into a single result using a binary  
operator. It's commonly used for calculating sums, products, or other  
aggregate values from collection elements.  

## Checking list conditions
This example demonstrates checking if elements satisfy conditions.  
```java
void main() {
    var ages = List.of(18, 22, 17, 25, 30, 16);
    
    var allAdults = ages.stream().allMatch(age -> age >= 18);
    IO.println("All adults: " + allAdults);
    
    var anyMinor = ages.stream().anyMatch(age -> age < 18);
    IO.println("Any minors: " + anyMinor);
    
    var noneOver100 = ages.stream().noneMatch(age -> age > 100);
    IO.println("None over 100: " + noneOver100);
}
```
The `allMatch`, `anyMatch`, and `noneMatch` methods check if all, any, or no  
elements satisfy a predicate. These are terminal operations that return  
boolean values, useful for validation and conditional logic.  

## List partitioning
This example shows how to partition a list into groups.  
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var partitioned = numbers.stream()
            .collect(java.util.stream.Collectors.partitioningBy(n -> n % 2 == 0));
    
    IO.println("Even: " + partitioned.get(true));
    IO.println("Odd: " + partitioned.get(false));
}
```
The `partitioningBy` collector splits elements into two groups based on a  
predicate, returning a Map with boolean keys. This is useful for binary  
classification of data.  

## List grouping
This example demonstrates grouping list elements by a property.  
```java
void main() {
    var words = List.of("apple", "apricot", "banana", "blueberry", 
            "cherry", "cranberry");
    
    var grouped = words.stream()
            .collect(java.util.stream.Collectors.groupingBy(w -> w.charAt(0)));
    
    grouped.forEach((letter, group) -> 
        IO.println(letter + ": " + group));
}
```
The `groupingBy` collector organizes elements into groups based on a  
classifier function, returning a Map where keys are group identifiers and  
values are lists of matching elements.  

## Distinct elements
This example shows how to remove duplicates from a list.  
```java
void main() {
    var numbers = List.of(1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5);
    
    var unique = numbers.stream()
            .distinct()
            .toList();
    
    IO.println(unique);
}
```
The `distinct` method filters out duplicate elements, keeping only unique  
values. It uses the `equals` method to determine equality and maintains the  
encounter order of the first occurrence.  

## List concatenation
This example demonstrates combining multiple lists.  
```java
void main() {
    var list1 = List.of("a", "b", "c");
    var list2 = List.of("d", "e", "f");
    var list3 = List.of("g", "h", "i");
    
    var combined = java.util.stream.Stream.of(list1, list2, list3)
            .flatMap(List::stream)
            .toList();
    
    IO.println(combined);
}
```
The `flatMap` method flattens nested streams into a single stream. This is  
useful for combining multiple collections or processing nested data structures  
into a flat list.  

## Limiting and skipping
This example shows how to extract a portion of a list using streams.  
```java
void main() {
    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var firstThree = numbers.stream()
            .limit(3)
            .toList();
    IO.println("First three: " + firstThree);
    
    var skipFirstFive = numbers.stream()
            .skip(5)
            .toList();
    IO.println("After skipping five: " + skipFirstFive);
    
    var middleThree = numbers.stream()
            .skip(3)
            .limit(3)
            .toList();
    IO.println("Middle three: " + middleThree);
}
```
The `limit` method restricts the stream to the first n elements, while `skip`  
bypasses the first n elements. Combined, they provide efficient pagination and  
slicing capabilities.  

## Reversing lists
This example demonstrates reversing the order of list elements.  
```java
void main() {
    var letters = new ArrayList<>(List.of("a", "b", "c", "d", "e"));
    
    java.util.Collections.reverse(letters);
    IO.println(letters);
    
    var numbers = List.of(1, 2, 3, 4, 5);
    var reversed = new ArrayList<>(numbers);
    java.util.Collections.reverse(reversed);
    IO.println(reversed);
}
```
The `Collections.reverse` method reverses the element order in place. For  
immutable lists, create a mutable copy first. Note that this modifies the  
list directly rather than returning a new one.  

## Shuffling lists
This example shows how to randomize the order of list elements.  
```java
void main() {
    var cards = new ArrayList<>(List.of("A", "2", "3", "4", "5", "6", 
            "7", "8", "9", "10", "J", "Q", "K"));
    
    java.util.Collections.shuffle(cards);
    IO.println("Shuffled: " + cards);
    
    var random = new java.util.Random(42);
    java.util.Collections.shuffle(cards, random);
    IO.println("Seeded shuffle: " + cards);
}
```
The `Collections.shuffle` method randomly permutes the list elements. An  
optional Random instance can be provided for reproducible results. This is  
useful for card games, randomized testing, or data sampling.  

## Binary search
This example demonstrates searching in a sorted list.  
```java
void main() {
    var numbers = new ArrayList<>(List.of(2, 4, 6, 8, 10, 12, 14, 16, 18, 20));
    
    var index = java.util.Collections.binarySearch(numbers, 12);
    IO.println("Index of 12: " + index);
    
    var notFound = java.util.Collections.binarySearch(numbers, 7);
    IO.println("Index of 7 (not found): " + notFound);
}
```
The `Collections.binarySearch` method performs an efficient O(log n) search  
on a sorted list. It returns the index if found, or a negative value  
indicating the insertion point if not found. The list must be sorted first.  

## Frequency counting
This example shows how to count occurrences of elements.  
```java
void main() {
    var items = List.of("apple", "banana", "apple", "cherry", 
            "banana", "apple", "date");
    
    var appleCount = java.util.Collections.frequency(items, "apple");
    IO.println("Apple count: " + appleCount);
    
    var bananaCount = java.util.Collections.frequency(items, "banana");
    IO.println("Banana count: " + bananaCount);
}
```
The `Collections.frequency` method counts how many times a specific element  
appears in a collection. This is useful for analyzing data distributions or  
finding the most common elements.  

## Disjoint lists
This example demonstrates checking if two lists have no common elements.  
```java
void main() {
    var set1 = List.of(1, 2, 3, 4, 5);
    var set2 = List.of(6, 7, 8, 9, 10);
    var set3 = List.of(4, 5, 6, 7);
    
    var disjoint12 = java.util.Collections.disjoint(set1, set2);
    IO.println("Set1 and Set2 disjoint: " + disjoint12);
    
    var disjoint13 = java.util.Collections.disjoint(set1, set3);
    IO.println("Set1 and Set3 disjoint: " + disjoint13);
}
```
The `Collections.disjoint` method checks if two collections have no elements  
in common. It returns true if the collections share no elements, useful for  
set operations and validation.  

## Synchronized lists
This example shows how to create thread-safe lists.  
```java
void main() {
    var list = new ArrayList<String>();
    list.add("one");
    list.add("two");
    list.add("three");
    
    var syncList = java.util.Collections.synchronizedList(list);
    
    synchronized(syncList) {
        for (var item : syncList) {
            IO.println(item);
        }
    }
}
```
The `Collections.synchronizedList` method wraps a list to make it thread-safe.  
All access to the backing list should be through the synchronized wrapper.  
Manual synchronization is still needed for iteration.  

## Unmodifiable lists
This example demonstrates creating immutable views of lists.  
```java
void main() {
    var mutable = new ArrayList<String>();
    mutable.add("alpha");
    mutable.add("beta");
    mutable.add("gamma");
    
    var readonly = java.util.Collections.unmodifiableList(mutable);
    IO.println(readonly);
    
    mutable.add("delta");
    IO.println("After modifying original: " + readonly);
}
```
The `Collections.unmodifiableList` method creates a read-only view of a list.  
Attempts to modify it throw exceptions. Note that changes to the original  
list are reflected in the view, so it's not truly immutable.  

## Maximum and minimum
This example shows how to find the largest and smallest elements.  
```java
void main() {
    var numbers = List.of(23, 7, 42, 15, 8, 91, 33, 12);
    
    var max = java.util.Collections.max(numbers);
    IO.println("Maximum: " + max);
    
    var min = java.util.Collections.min(numbers);
    IO.println("Minimum: " + min);
    
    var words = List.of("zebra", "apple", "mango", "cherry");
    var maxWord = java.util.Collections.max(words);
    var minWord = java.util.Collections.min(words);
    IO.println("Max word: " + maxWord);
    IO.println("Min word: " + minWord);
}
```
The `Collections.max` and `min` methods find the maximum and minimum elements  
according to their natural ordering or a provided comparator. They work with  
any comparable elements, including numbers and strings.  

## Filling lists
This example demonstrates filling a list with a specific value.  
```java
void main() {
    var items = new ArrayList<String>();
    items.add("old1");
    items.add("old2");
    items.add("old3");
    items.add("old4");
    items.add("old5");
    
    IO.println("Before: " + items);
    
    java.util.Collections.fill(items, "new");
    IO.println("After: " + items);
}
```
The `Collections.fill` method replaces all elements in a list with a specified  
value. This is useful for resetting or initializing lists with a default  
value after creation.  
