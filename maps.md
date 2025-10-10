# Java HashMap

This document demonstrates how to work with the Java `HashMap` collection,  
providing comprehensive examples using modern Java 25 syntax with implicit  
imports and type inference.  

A **HashMap** is a hash table-based implementation of the `Map` interface that  
stores key-value pairs. Each key in a `HashMap` must be unique and is mapped to  
exactly one value. HashMaps are known as associative arrays or dictionaries in  
other programming languages. They provide constant-time performance for basic  
operations like `get` and `put`, assuming the hash function disperses elements  
properly among the buckets. HashMaps can store `null` values and one `null`  
key, and they do not maintain any specific ordering of elements.  

The `Map.Entry` interface represents a key-value pair within a `HashMap`. The  
`entrySet` method returns a `Set` view of all mappings in the map, while the  
`keySet` method retrieves a `Set` of all keys. The `HashMap` class extends  
`AbstractMap` and implements the `Map` interface, which provides essential  
method signatures including `get`, `put`, `size`, `isEmpty`, and many more for  
comprehensive map manipulation.  

## HashMap constructors 


The `HashMap` class provides several constructors for creating map instances:  

- `HashMap()` — constructs an empty `HashMap` with the default initial capacity  
  (16) and the default load factor (0.75)  
- `HashMap(int initialCapacity)` — constructs an empty `HashMap` with the given  
  initial capacity and the default load factor (0.75)  
- `HashMap(int initialCapacity, float loadFactor)` — constructs an empty  
  `HashMap` with the given initial capacity and load factor  
- `HashMap(Map<? extends K,? extends V> m)` — constructs a new `HashMap` with  
  the same mappings as the given `Map`  

In these constructors, `K` represents the type of the map keys and `V`  
represents the type of the mapped values.  

## HashMap methods 


The following table lists commonly used `HashMap` methods:  

| Modifier and type | Method | Description |
|-------------------|--------|-------------|
| void | clear() | Removes all mappings from the map |
| Object | clone() | Returns a shallow copy of the HashMap instance |
| boolean | containsKey(Object key) | Returns true if map contains the specified key |
| Set<Map.Entry<K,V>> | entrySet() | Returns a Set view of the mappings |
| boolean | isEmpty() | Returns true if this map is empty |
| Set<K> | keySet() | Returns a Set view of the keys |
| V | put(K key, V value) | Adds new mapping to the map |
| V | remove(Object key) | Removes the mapping for the specified key |
| V | get(Object key) | Returns the value mapped to the specified key |
| void | forEach(BiConsumer<K,V> action) | Performs action for each entry |
| V | replace(K key, V value) | Replaces entry for the specified key |
| int | size() | Returns the number of key-value mappings |
| Collection<V> | values() | Returns a Collection view of the values |

This document demonstrates several of these methods with practical examples.  

## HashMap creation 

This example shows how to create a basic HashMap instance.  

```java
void main() {

    var capitals = new HashMap<String, String>();
    
    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    
    IO.println(capitals);
}
```

A `HashMap` is created using the `new` keyword with type parameters specifying  
key and value types. Thanks to type inference with `var`, we don't need to  
repeat the type parameters on the left side of the declaration. The `put`  
method adds key-value pairs to the map, where the first parameter is the key  
and the second is the value.  

## HashMap initialization 

This example demonstrates factory methods for initializing maps efficiently.  

```java
void main() {

    var colours = Map.of(1, "red", 2, "blue", 3, "brown");
    IO.println(colours);

    var countries = Map.ofEntries(
        Map.entry("de", "Germany"),
        Map.entry("sk", "Slovakia"),
        Map.entry("ru", "Russia")
    );

    IO.println(countries);
}
```

Since Java 9, the `Map.of` and `Map.ofEntries` factory methods provide a  
convenient way to create immutable maps. The `Map.of` method works well for up  
to 10 key-value pairs, while `Map.ofEntries` is useful for larger maps. Both  
methods return unmodifiable maps that cannot be changed after creation.  

For cases where a modifiable map is needed, the double-brace initialization  
pattern can be used:  

```java
void main() {

    var countries = new HashMap<String, String>() {{
        put("de", "Germany");
        put("sk", "Slovakia");
        put("ru", "Russia");
    }};

    IO.println(countries);
}
```

This approach creates an anonymous subclass and uses an instance initializer  
block to populate the map. While convenient, it creates an extra class and  
should be used judiciously.  

## The size method 

This example demonstrates determining the number of entries in a HashMap.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    var size = capitals.size();
    IO.println("The size of the HashMap is " + size);

    capitals.remove("pol");
    capitals.remove("ita");

    size = capitals.size();
    IO.println("The size of the HashMap is " + size);
}
```

The `size` method returns the number of key-value mappings currently stored in  
the map. After adding six entries, the size is 6. The `remove` method deletes  
entries by their keys, reducing the size to 4 after removing two pairs.  

## The get method 

This example shows how to retrieve values from a HashMap using keys.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    var cap1 = capitals.get("ita");
    var cap2 = capitals.get("svk");

    IO.println(cap1);
    IO.println(cap2);
}
```

The `get` method retrieves the value associated with a specified key. It takes  
a key as a parameter and returns the corresponding value. If the key doesn't  
exist in the map, the method returns `null`.  

## The clear method 

This example demonstrates removing all entries from a HashMap.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.clear();

    if (capitals.isEmpty()) {
        IO.println("The map is empty");
    } else {
        IO.println("The map is not empty");
    }
}
```

The `clear` method removes all key-value mappings from the map, leaving it  
empty. The `isEmpty` method checks whether the map contains any entries,  
returning `true` if the map has no mappings and `false` otherwise.  

## The containsKey method 

This example shows how to check if a map contains a specific key.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    var key1 = "ger";
    var key2 = "rus";

    if (capitals.containsKey(key1)) {
        IO.println("HashMap contains " + key1 + " key");
    } else {
        IO.println("HashMap does not contain " + key1 + " key");
    }

    if (capitals.containsKey(key2)) {
        IO.println("HashMap contains " + key2 + " key");
    } else {
        IO.println("HashMap does not contain " + key2 + " key");
    }
}
```

The `containsKey` method returns `true` if the map contains a mapping for the  
specified key, and `false` otherwise. This is useful for checking key existence  
before attempting to retrieve or modify values, preventing potential `null`  
reference issues.  

## The replace method 

This example demonstrates replacing values in a HashMap.  

```java
void main() {

    var data = new HashMap<String, String>();

    data.put("day", "Monday");
    data.put("country", "Poland");
    data.put("colour", "blue");

    data.replace("day", "Sunday");
    data.replace("country", "Russia", "Great Britain");
    data.replace("colour", "blue", "green");

    data.entrySet().forEach(IO::println);
}
```

The `replace` method comes in two forms. The first form, `replace(K key, V  value)`,  
replaces the entry for the specified key only if it's currently  
mapped to some value. The second form, `replace(K key, V oldValue, V  newValue)`,  
replaces the entry only if the current value matches the specified  
old value. In the example, the first replacement succeeds unconditionally, the  
second fails because "country" isn't mapped to "Russia", and the third succeeds  
because the old value matches.  

## Convert HashMap to List 

This example shows how to convert HashMap entries into a list.  

```java
void main() {

    var colours = Map.of(
        "AliceBlue", "#f0f8ff",
        "GreenYellow", "#adff2f",
        "IndianRed", "#cd5c5c",
        "khaki", "#f0e68c"
    );

    var entries = colours.entrySet();
    var mylist = new ArrayList<>(entries);

    IO.println(mylist);
}
```

The `entrySet` method returns a `Set` view of all mappings in the map. This  
set can be passed directly to the `ArrayList` constructor to create a list of  
entries. This conversion is useful when you need list-specific operations like  
indexed access or sorting on map entries.  

## Iteration with forEach 

This example demonstrates iterating over map entries using forEach.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.forEach((k, v) -> IO.println(k + ": " + v));
}
```

The `forEach` method accepts a `BiConsumer` that processes each key-value pair  
in the map. The lambda expression `(k, v) -> IO.println(k + ": " + v)` is  
executed for each entry, making it a concise way to iterate over all mappings.  

## Iteration with enhanced for loop 

This example shows iterating over a HashMap with an enhanced for loop.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    for (var pair : capitals.entrySet()) {
        IO.println(pair.getKey() + ": " + pair.getValue());
    }
}
```

The enhanced for loop iterates over the entry set returned by `entrySet`. In  
each iteration, a `Map.Entry` object is assigned to the `pair` variable. The  
`getKey` and `getValue` methods extract the key and value from each entry. The  
`var` keyword simplifies the code by inferring the entry type automatically.  

## Iteration over keys 

This example demonstrates iterating over only the keys of a HashMap.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    var keys = capitals.keySet();
    keys.forEach(IO::println);
}
```

The `keySet` method returns a `Set` view of all keys in the map. Since keys  
must be unique, they are returned as a `Set` rather than a collection that  
allows duplicates. The `forEach` method then iterates over this set, printing  
each key to the console.  

## Iteration over values 

This example shows how to iterate over only the values of a HashMap.  

```java
void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    var vals = capitals.values();
    vals.forEach(IO::println);
}
```

The `values` method returns a `Collection` view of all values in the map.  
Unlike keys, values don't need to be unique, so they're returned as a  
`Collection` rather than a `Set`. This allows multiple keys to map to the same  
value without restriction.  

## Filtering HashMap 

This example demonstrates filtering a HashMap using the Stream API.  

```java
import java.util.stream.Collectors;

void main() {

    var capitals = new HashMap<String, String>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    var filteredCapitals = capitals.entrySet().stream()
        .filter(e -> e.getValue().length() == 6)
        .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    filteredCapitals.entrySet().forEach(IO::println);
}
```

The Stream API's `filter` method allows selective processing of map entries.  
First, `entrySet().stream()` creates a stream of entries. The `filter` method  
keeps only entries whose values have a length of 6 characters. Finally,  
`Collectors.toMap` collects the filtered entries back into a new HashMap.  

## List of maps 

This example demonstrates creating and working with a list of HashMap objects.  

```java
void main() {

    var fruits1 = new HashMap<String, Integer>();
    fruits1.put("oranges", 2);
    fruits1.put("bananas", 3);

    var fruits2 = new HashMap<String, Integer>();
    fruits2.put("plums", 6);
    fruits2.put("apples", 7);

    var allFruits = new ArrayList<Map<String, Integer>>();
    allFruits.add(fruits1);
    allFruits.add(fruits2);

    allFruits.forEach(map -> 
        map.forEach((k, v) -> IO.println("key: " + k + " value: " + v))
    );
}
```

A list can contain multiple maps, enabling organization of related data groups.  
The example creates two separate fruit maps and adds them to an ArrayList. The  
nested `forEach` loops iterate first over each map in the list, then over each  
key-value pair within those maps, demonstrating how to work with collections of  
maps effectively.  

## Merging maps 

This example shows how to combine multiple maps into one.  

```java
void main() {

    var map1 = new HashMap<String, String>();
    map1.put("a", "apple");
    map1.put("b", "ball");
    
    var map2 = new HashMap<String, String>();
    map2.put("c", "cat");
    map2.put("d", "dog");
    
    var merged = new HashMap<String, String>();
    merged.putAll(map1);
    merged.putAll(map2);
    
    IO.println("Merged map:");
    merged.forEach((k, v) -> IO.println(k + " = " + v));
}
```

The `putAll` method copies all mappings from one map to another. This is useful  
for combining multiple maps into a single map. If both maps contain the same  
key, the value from the second map overwrites the value from the first map.  

## The getOrDefault method 

This example demonstrates safely retrieving values with a default fallback.  

```java
void main() {

    var scores = new HashMap<String, Integer>();
    scores.put("Alice", 95);
    scores.put("Bob", 87);
    scores.put("Charlie", 92);
    
    IO.println("Alice's score: " + scores.getOrDefault("Alice", 0));
    IO.println("David's score: " + scores.getOrDefault("David", 0));
    IO.println("Eve's score: " + scores.getOrDefault("Eve", -1));
}
```

The `getOrDefault` method returns the value associated with a key if it exists,  
or a specified default value if the key is not found. This prevents `null`  
pointer issues and provides a cleaner alternative to checking key existence  
before retrieval. Different default values can be used based on the context.  

## Compute methods 

This example shows advanced value computation using compute methods.  

```java
void main() {

    var inventory = new HashMap<String, Integer>();
    inventory.put("apples", 10);
    inventory.put("bananas", 5);
    
    // Add 3 to existing value or set to 3 if absent
    inventory.computeIfAbsent("oranges", k -> 3);
    
    // Double the value if present
    inventory.computeIfPresent("apples", (k, v) -> v * 2);
    
    // Compute new value based on key and existing value
    inventory.compute("bananas", (k, v) -> v == null ? 1 : v + 5);
    
    inventory.forEach((k, v) -> IO.println(k + ": " + v));
}
```

The compute methods provide powerful ways to update map values. The  
`computeIfAbsent` method adds a mapping only if the key is absent. The  
`computeIfPresent` method updates a value only if the key exists. The `compute`  
method handles both cases, allowing conditional logic based on the current  
value and key.  

## Removing entries with removeIf 

This example demonstrates conditional removal of map entries.  

```java
void main() {

    var prices = new HashMap<String, Double>();
    prices.put("apple", 1.50);
    prices.put("banana", 0.75);
    prices.put("orange", 2.00);
    prices.put("grape", 3.50);
    
    // Remove entries with price greater than 2.0
    prices.entrySet().removeIf(entry -> entry.getValue() > 2.0);
    
    IO.println("Items under $2.00:");
    prices.forEach((k, v) -> IO.println(k + ": $" + v));
}
```

The `removeIf` method on the entry set allows removal of entries based on a  
predicate condition. The predicate receives each entry and returns `true` for  
entries to remove. This is more concise than manually iterating and removing  
entries, and it's safer than modifying the map during iteration.  

## Sorting HashMap 

This example shows how to sort HashMap entries by keys or values.  

```java
import java.util.LinkedHashMap;
import java.util.stream.Collectors;

void main() {

    var populations = new HashMap<String, Integer>();
    populations.put("Tokyo", 37400000);
    populations.put("Delhi", 28514000);
    populations.put("Shanghai", 25582000);
    populations.put("São Paulo", 21650000);
    
    // Sort by key
    var sortedByKey = populations.entrySet().stream()
        .sorted(Map.Entry.comparingByKey())
        .collect(Collectors.toMap(
            Map.Entry::getKey,
            Map.Entry::getValue,
            (e1, e2) -> e1,
            LinkedHashMap::new
        ));
    
    IO.println("Sorted by city name:");
    sortedByKey.forEach((k, v) -> IO.println(k + ": " + v));
    
    // Sort by value (descending)
    var sortedByValue = populations.entrySet().stream()
        .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
        .collect(Collectors.toMap(
            Map.Entry::getKey,
            Map.Entry::getValue,
            (e1, e2) -> e1,
            LinkedHashMap::new
        ));
    
    IO.println("\nSorted by population (descending):");
    sortedByValue.forEach((k, v) -> IO.println(k + ": " + v));
}
```

HashMaps don't maintain order, so sorting requires converting to a stream,  
applying sort operations, and collecting into a `LinkedHashMap` to preserve the  
order. The `comparingByKey` and `comparingByValue` methods create comparators  
for sorting. The `reversed` method inverts the sort order for descending  
results. The `LinkedHashMap` maintains insertion order, preserving the sorted  
sequence.