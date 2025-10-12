# Java Stream Gatherers

This document contains 60 progressively complex Java examples demonstrating  
the usage of Stream Gatherers using modern Java 25 syntax.  

Stream Gatherers are a powerful preview feature introduced in Java 22 (JEP  
461) and refined in subsequent versions. They provide a way to create custom  
intermediate stream operations that can maintain state and transform stream  
elements in sophisticated ways. Gatherers bridge the gap between simple  
intermediate operations like `map` and `filter`, and complex terminal  
operations like `collect`.  

A gatherer is defined by four components: an initializer that creates the  
initial state, an integrator that processes each element and updates the  
state, a combiner for parallel execution, and a finisher that produces the  
final output. This design allows gatherers to implement operations like  
windowing, batching, stateful filtering, and custom transformations that  
would be difficult or impossible with standard stream operations.  

Gatherers are particularly useful for operations that require looking at  
multiple elements together, maintaining running state across elements, or  
implementing custom data transformations. They can be combined with other  
stream operations and gatherers, making them composable building blocks for  
complex data processing pipelines. The `Gatherers` class  
provides several built-in gatherers for common patterns like fixed-size  
windows, sliding windows, and custom scanning operations.  

## Basic gatherer usage

This example demonstrates using a built-in gatherer to create fixed windows.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9);
    
    var windows = numbers.stream()
            .gather(Gatherers.windowFixed(3))
            .toList();
    
    windows.forEach(IO::println);
}
```

The `windowFixed` gatherer groups consecutive elements into fixed-size  
windows. Each window is a list containing the specified number of elements.  
This is useful for batch processing or analyzing data in chunks.  

## Sliding window

This example shows creating overlapping windows that slide across elements.  

```java
void main() {

    var data = List.of(1, 2, 3, 4, 5, 6, 7);
    
    var sliding = data.stream()
            .gather(Gatherers.windowSliding(3))
            .toList();
    
    sliding.forEach(IO::println);
}
```

The `windowSliding` gatherer creates overlapping windows where each window  
shifts by one element. This is useful for moving averages, pattern detection,  
or analyzing consecutive sequences of data.  

## Fold operation

This example demonstrates using fold to accumulate values with state.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    
    var result = numbers.stream()
            .gather(Gatherers.fold(
                    () -> 0,
                    (sum, num) -> sum + num))
            .toList();
    
    result.forEach(IO::println);
}
```

The `fold` gatherer maintains a running accumulation of values, emitting the  
current state after processing each element. Unlike `reduce`, it produces  
intermediate results, making it useful for cumulative calculations.  

## Scan operation

This example shows using scan to produce running totals.  

```java
void main() {

    var values = List.of(1, 2, 3, 4, 5);
    
    var runningSum = values.stream()
            .gather(Gatherers.scan(
                    () -> 0,
                    (acc, val) -> acc + val))
            .toList();
    
    runningSum.forEach(IO::println);
}
```

The `scan` gatherer is similar to fold but includes the initial value in its  
output. It's particularly useful for generating sequences where each element  
depends on the previous computation.  

## Fixed window with mapping

This example combines windowing with transformation operations.  

```java
void main() {

    var words = List.of("a", "b", "c", "d", "e", "f");
    
    var batches = words.stream()
            .gather(Gatherers.windowFixed(2))
            .map(window -> String.join("-", window))
            .toList();
    
    batches.forEach(IO::println);
}
```

Gatherers can be combined with standard stream operations like `map`. Here,  
we group elements into pairs and then join each pair into a single string.  
This demonstrates the composability of gatherers.  

## Sliding window for moving average

This example calculates a moving average using sliding windows.  

```java
void main() {

    var prices = List.of(10.0, 12.0, 11.0, 13.0, 15.0, 14.0);
    
    var movingAvg = prices.stream()
            .gather(Gatherers.windowSliding(3))
            .map(window -> window.stream()
                    .mapToDouble(Double::doubleValue)
                    .average()
                    .orElse(0.0))
            .toList();
    
    movingAvg.forEach(avg -> IO.println("Avg: " + avg));
}
```

Sliding windows are ideal for calculating moving averages. Each window  
contains consecutive elements, and we compute the average for each window.  
This is commonly used in financial and statistical analysis.  

## Window with filtering

This example shows filtering elements before windowing.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var evenWindows = numbers.stream()
            .filter(n -> n % 2 == 0)
            .gather(Gatherers.windowFixed(2))
            .toList();
    
    evenWindows.forEach(IO::println);
}
```

Gatherers integrate seamlessly with other stream operations. Here, we filter  
for even numbers before grouping them into fixed-size windows. The order of  
operations matters for efficiency and correctness.  

## Batch processing

This example demonstrates processing data in batches.  

```java
void main() {

    var items = List.of("item1", "item2", "item3", "item4", "item5");
    
    var batches = items.stream()
            .gather(Gatherers.windowFixed(2))
            .peek(batch -> IO.println("Processing batch: " + batch))
            .flatMap(List::stream)
            .toList();
    
    IO.println("Final result: " + batches);
}
```

Windowing is useful for batch processing where you want to handle multiple  
items together. The `flatMap` operation can then flatten the results back  
into a single stream if needed.  

## Cumulative sum

This example shows calculating cumulative sums using scan.  

```java
void main() {

    var transactions = List.of(100, -50, 200, -30, 150);
    
    var balance = transactions.stream()
            .gather(Gatherers.scan(
                    () -> 0,
                    (sum, amount) -> sum + amount))
            .toList();
    
    IO.println("Running balance: " + balance);
}
```

The `scan` gatherer is perfect for tracking running totals, such as account  
balances. Each element in the output represents the cumulative sum up to that  
point in the stream.  

## Window with size validation

This example handles cases where the stream size is not divisible by window.  

```java
void main() {

    var data = List.of(1, 2, 3, 4, 5, 6, 7);
    
    var windows = data.stream()
            .gather(Gatherers.windowFixed(3))
            .toList();
    
    windows.forEach(window -> 
            IO.println("Window size: " + window.size() + " - " + window));
}
```

When using fixed-size windows with streams whose size isn't a multiple of the  
window size, the last window contains the remaining elements. This example  
shows how to handle such cases.  

## Combining multiple gatherers

This example shows chaining multiple gatherer operations.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8);
    
    var result = numbers.stream()
            .gather(Gatherers.windowFixed(2))
            .map(window -> window.stream()
                    .mapToInt(Integer::intValue)
                    .sum())
            .gather(Gatherers.windowFixed(2))
            .toList();
    
    result.forEach(IO::println);
}
```

Gatherers can be chained together to create complex transformations. Here,  
we first group into pairs, sum each pair, then group those sums into new  
windows. This demonstrates the composability of gatherers.  

## Sliding window overlap

This example demonstrates the overlap in sliding windows.  

```java
void main() {

    var letters = List.of("A", "B", "C", "D", "E");
    
    var windows = letters.stream()
            .gather(Gatherers.windowSliding(2))
            .toList();
    
    IO.println("Sliding windows of size 2:");
    windows.forEach(IO::println);
}
```

Sliding windows of size 2 create pairs where consecutive pairs share one  
element. This is useful for detecting patterns or relationships between  
adjacent elements in a sequence.  

## Fold with string accumulation

This example uses fold to build a cumulative string.  

```java
void main() {

    var words = List.of("Java", "Stream", "Gatherers", "Example");
    
    var accumulated = words.stream()
            .gather(Gatherers.fold(
                    () -> "",
                    (acc, word) -> acc.isEmpty() ? word : acc + " " + word))
            .toList();
    
    accumulated.forEach(IO::println);
}
```

The `fold` gatherer can accumulate strings, showing how the string grows with  
each word. The last element contains the complete accumulated result, while  
intermediate elements show the progression.  

## Window with transformation

This example transforms elements within each window.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6);
    
    var transformed = numbers.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> window.stream()
                    .map(n -> n * n)
                    .toList())
            .toList();
    
    transformed.forEach(IO::println);
}
```

Windows can be transformed before being collected. Here, we square each  
number within its window. This pattern is useful for applying operations to  
groups of related elements.  

## Scan with multiplication

This example demonstrates scan with a multiplicative operation.  

```java
void main() {

    var factors = List.of(2, 3, 4, 5);
    
    var products = factors.stream()
            .gather(Gatherers.scan(
                    () -> 1,
                    (product, factor) -> product * factor))
            .toList();
    
    IO.println("Running products: " + products);
}
```

The `scan` gatherer works with any binary operation. Here, we compute running  
products, showing how values multiply cumulatively. This is useful for  
compound interest calculations or factorial-like computations.  

## Sliding window for pairs

This example creates consecutive pairs using sliding windows.  

```java
void main() {

    var sequence = List.of(10, 20, 30, 40, 50);
    
    var pairs = sequence.stream()
            .gather(Gatherers.windowSliding(2))
            .map(window -> "(" + window.get(0) + ", " + 
                    window.get(1) + ")")
            .toList();
    
    pairs.forEach(IO::println);
}
```

Sliding windows of size 2 are particularly useful for creating pairs of  
consecutive elements. This is common when comparing adjacent items or  
calculating differences between consecutive values.  

## Fixed window with records

This example uses windowing with record types.  

```java
record Temperature(String city, double celsius) {}

void main() {

    var temps = List.of(
            new Temperature("NYC", 20.5),
            new Temperature("LA", 25.0),
            new Temperature("Chicago", 18.0),
            new Temperature("Miami", 30.0));
    
    var batches = temps.stream()
            .gather(Gatherers.windowFixed(2))
            .toList();
    
    batches.forEach(batch -> IO.println("Batch: " + batch));
}
```

Gatherers work seamlessly with records and custom types. This example batches  
temperature readings, which could be useful for processing weather data in  
groups for analysis or reporting.  

## Fold with max tracking

This example tracks the running maximum using fold.  

```java
void main() {

    var values = List.of(3, 1, 4, 1, 5, 9, 2, 6);
    
    var runningMax = values.stream()
            .gather(Gatherers.fold(
                    () -> Integer.MIN_VALUE,
                    (max, val) -> Math.max(max, val)))
            .toList();
    
    IO.println("Running maximum: " + runningMax);
}
```

The `fold` gatherer can track running statistics like the maximum value seen  
so far. Each element shows the highest value encountered up to that point in  
the stream.  

## Window with filtering empty

This example filters out incomplete windows.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7);
    
    var fullWindows = numbers.stream()
            .gather(Gatherers.windowFixed(3))
            .filter(window -> window.size() == 3)
            .toList();
    
    fullWindows.forEach(IO::println);
}
```

Sometimes you only want complete windows. Filtering after windowing lets you  
discard partial windows that occur when the stream size isn't a multiple of  
the window size.  

## Scan with string building

This example builds strings incrementally using scan.  

```java
void main() {

    var chars = List.of("J", "a", "v", "a");
    
    var progressive = chars.stream()
            .gather(Gatherers.scan(
                    () -> "",
                    (str, ch) -> str + ch))
            .toList();
    
    progressive.forEach(IO::println);
}
```

The `scan` gatherer incrementally builds output, showing the progression at  
each step. This example shows how a string is built character by character,  
displaying each intermediate state.  

## Sliding window with calculation

This example calculates differences between consecutive elements.  

```java
void main() {

    var prices = List.of(100, 105, 103, 108, 110);
    
    var changes = prices.stream()
            .gather(Gatherers.windowSliding(2))
            .map(window -> window.get(1) - window.get(0))
            .toList();
    
    IO.println("Price changes: " + changes);
}
```

Sliding windows are perfect for calculating changes between consecutive  
values. This pattern is common in financial analysis for tracking price  
movements or computing rates of change.  

## Fixed window with aggregation

This example aggregates data within each window.  

```java
void main() {

    var scores = List.of(85, 90, 78, 92, 88, 95, 82, 87);
    
    var avgPerBatch = scores.stream()
            .gather(Gatherers.windowFixed(4))
            .map(window -> window.stream()
                    .mapToInt(Integer::intValue)
                    .average()
                    .orElse(0.0))
            .toList();
    
    avgPerBatch.forEach(avg -> IO.println("Batch average: " + avg));
}
```

Windows can be aggregated to compute statistics for each group. Here, we  
calculate the average score for each batch of test results, useful for  
analyzing performance across different groups.  

## Fold with list accumulation

This example accumulates elements into a growing list using fold.  

```java
void main() {

    var items = List.of("apple", "banana", "cherry");
    
    var growing = items.stream()
            .gather(Gatherers.fold(
                    () -> new ArrayList<String>(),
                    (list, item) -> {
                        list.add(item);
                        return new ArrayList<>(list);
                    }))
            .toList();
    
    growing.forEach(IO::println);
}
```

The `fold` gatherer can accumulate elements into collections, showing how the  
collection grows with each addition. Each output is a snapshot of the  
accumulated state at that point.  

## Sliding window with all combinations

This example shows all overlapping triplets in a sequence.  

```java
void main() {

    var sequence = List.of(1, 2, 3, 4, 5);
    
    var triplets = sequence.stream()
            .gather(Gatherers.windowSliding(3))
            .map(window -> "[" + window.get(0) + ", " + 
                    window.get(1) + ", " + window.get(2) + "]")
            .toList();
    
    triplets.forEach(IO::println);
}
```

Sliding windows of size 3 create all consecutive triplets. This is useful for  
pattern matching, sequence analysis, or detecting trends that require looking  
at multiple consecutive elements.  

## Window with custom processing

This example processes windows with custom logic.  

```java
void main() {

    var numbers = List.of(2, 4, 6, 8, 10, 12);
    
    var results = numbers.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> {
                var sum = window.stream().mapToInt(Integer::intValue).sum();
                var avg = sum / window.size();
                return "Sum: " + sum + ", Avg: " + avg;
            })
            .toList();
    
    results.forEach(IO::println);
}
```

Each window can be processed with custom logic that computes multiple values.  
This example calculates both sum and average for each window, demonstrating  
complex per-window processing.  

## Scan with conditional logic

This example uses scan with conditional accumulation.  

```java
void main() {

    var numbers = List.of(5, -3, 7, -2, 4, -1);
    
    var positiveSum = numbers.stream()
            .gather(Gatherers.scan(
                    () -> 0,
                    (sum, num) -> num > 0 ? sum + num : sum))
            .toList();
    
    IO.println("Running sum (positives only): " + positiveSum);
}
```

The `scan` gatherer can include conditional logic in its accumulation  
function. Here, we only add positive numbers to the running sum, ignoring  
negative values.  

## Fixed window with empty stream

This example shows how windowing handles empty streams.  

```java
void main() {

    var empty = List.<Integer>of();
    
    var windows = empty.stream()
            .gather(Gatherers.windowFixed(3))
            .toList();
    
    IO.println("Windows from empty stream: " + windows);
    IO.println("Is empty: " + windows.isEmpty());
}
```

When gathering an empty stream, the result is an empty list. This example  
demonstrates defensive programming and edge case handling when working with  
gatherers.  

## Sliding window for trend detection

This example detects increasing trends in data.  

```java
void main() {

    var values = List.of(1, 3, 2, 4, 5, 6, 4, 7);
    
    var increasing = values.stream()
            .gather(Gatherers.windowSliding(2))
            .map(window -> window.get(1) > window.get(0))
            .toList();
    
    IO.println("Increasing trends: " + increasing);
}
```

Sliding windows can detect patterns like increasing or decreasing trends.  
Each boolean indicates whether the value increased compared to the previous  
one, useful for trend analysis.  

## Fold with complex state

This example maintains complex state across elements.  

```java
record Stats(int count, int sum) {
    Stats add(int value) {
        return new Stats(count + 1, sum + value);
    }
    double average() {
        return count == 0 ? 0.0 : (double) sum / count;
    }
}

void main() {

    var numbers = List.of(10, 20, 30, 40, 50);
    
    var runningStats = numbers.stream()
            .gather(Gatherers.fold(
                    () -> new Stats(0, 0),
                    (stats, num) -> stats.add(num)))
            .map(Stats::average)
            .toList();
    
    IO.println("Running averages: " + runningStats);
}
```

The `fold` gatherer can maintain complex state objects. This example tracks  
count and sum to compute running averages, demonstrating stateful  
transformations with records.  

## Window with flatMap

This example flattens windows into individual elements.  

```java
void main() {

    var data = List.of(1, 2, 3, 4, 5, 6);
    
    var processed = data.stream()
            .gather(Gatherers.windowFixed(2))
            .flatMap(window -> window.stream()
                    .map(n -> n * 10))
            .toList();
    
    IO.println("Processed: " + processed);
}
```

Windows can be processed and flattened back into a stream of individual  
elements. This combines windowing with transformation and flattening,  
showcasing the flexibility of gatherers.  

## Scan with alternating operation

This example alternates operations in scan.  

```java
void main() {

    var numbers = List.of(10, 5, 8, 3, 12);
    
    var result = numbers.stream()
            .gather(Gatherers.scan(
                    () -> new int[]{0, 0},
                    (state, num) -> {
                        state[1]++;
                        state[0] = state[1] % 2 == 0 ? 
                                state[0] + num : state[0] - num;
                        return new int[]{state[0], state[1]};
                    }))
            .map(state -> state[0])
            .toList();
    
    IO.println("Alternating sum/diff: " + result);
}
```

Complex state can include counters and computed values. This example  
alternates between adding and subtracting values, showing sophisticated  
stateful transformations.  

## Sliding window with filtering

This example filters windows based on their content.  

```java
void main() {

    var numbers = List.of(1, 5, 3, 8, 2, 9, 4);
    
    var highWindows = numbers.stream()
            .gather(Gatherers.windowSliding(3))
            .filter(window -> window.stream()
                    .mapToInt(Integer::intValue)
                    .average()
                    .orElse(0.0) > 4.0)
            .toList();
    
    IO.println("Windows with avg > 4: " + highWindows);
}
```

Windows can be filtered based on aggregate properties. This example only  
keeps windows whose average exceeds a threshold, useful for identifying  
interesting segments in data.  

## Fixed window with counting

This example counts elements in each window.  

```java
void main() {

    var items = List.of("a", "b", "c", "d", "e", "f", "g");
    
    var counts = items.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> "Window size: " + window.size() + 
                    " - " + window)
            .toList();
    
    counts.forEach(IO::println);
}
```

Each window can be analyzed for its properties. This example shows window  
sizes, which helps understand how data is partitioned, especially when the  
last window may be smaller.  

## Fold with min tracking

This example tracks the running minimum value.  

```java
void main() {

    var temperatures = List.of(25, 22, 28, 19, 30, 18);
    
    var runningMin = temperatures.stream()
            .gather(Gatherers.fold(
                    () -> Integer.MAX_VALUE,
                    (min, temp) -> Math.min(min, temp)))
            .toList();
    
    IO.println("Running minimum: " + runningMin);
}
```

The `fold` gatherer can track running minimums, showing the lowest value  
encountered so far at each step. This is useful for monitoring thresholds or  
finding records.  

## Sliding window with sum comparison

This example compares sums of consecutive windows.  

```java
void main() {

    var sales = List.of(100, 150, 120, 180, 200);
    
    var windowSums = sales.stream()
            .gather(Gatherers.windowSliding(2))
            .map(window -> window.stream()
                    .mapToInt(Integer::intValue)
                    .sum())
            .toList();
    
    IO.println("Consecutive pair sums: " + windowSums);
}
```

Sliding windows can be aggregated to show how values change across the  
sequence. Here, we sum consecutive pairs, which could represent combined  
sales periods or aggregated metrics.  

## Window with record transformation

This example transforms records within windows.  

```java
record Sale(String product, int quantity) {}

void main() {

    var sales = List.of(
            new Sale("Widget", 10),
            new Sale("Gadget", 15),
            new Sale("Widget", 8),
            new Sale("Gadget", 12));
    
    var batches = sales.stream()
            .gather(Gatherers.windowFixed(2))
            .map(window -> window.stream()
                    .mapToInt(Sale::quantity)
                    .sum())
            .toList();
    
    IO.println("Batch totals: " + batches);
}
```

Records can be processed within windows to extract and aggregate data. This  
example sums quantities within each batch of sales, demonstrating business  
logic applied to grouped data.  

## Scan with toggle state

This example uses scan to toggle between states.  

```java
void main() {

    var events = List.of("click", "click", "click", "click");
    
    var states = events.stream()
            .gather(Gatherers.scan(
                    () -> false,
                    (state, event) -> !state))
            .toList();
    
    IO.println("Toggle states: " + states);
}
```

The `scan` gatherer can implement state machines. This example toggles a  
boolean state with each event, useful for tracking on/off states or  
alternating behaviors.  

## Fixed window with distinct elements

This example finds distinct elements within each window.  

```java
void main() {

    var numbers = List.of(1, 1, 2, 3, 3, 4, 5, 5, 6);
    
    var distinctPerWindow = numbers.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> window.stream()
                    .distinct()
                    .toList())
            .toList();
    
    distinctPerWindow.forEach(IO::println);
}
```

Windows can be processed to find unique elements. This example removes  
duplicates within each window, useful for deduplication or analyzing unique  
values in segments.  

## Sliding window with pattern matching

This example detects specific patterns in consecutive elements.  

```java
void main() {

    var sequence = List.of(1, 2, 3, 2, 3, 4, 3, 4, 5);
    
    var ascending = sequence.stream()
            .gather(Gatherers.windowSliding(3))
            .filter(window -> window.get(0) < window.get(1) && 
                    window.get(1) < window.get(2))
            .toList();
    
    IO.println("Ascending triplets: " + ascending);
}
```

Sliding windows enable pattern detection across consecutive elements. This  
example finds all triplets where values increase sequentially, useful for  
identifying trends or specific sequences.  

## Fold with map accumulation

This example builds a map incrementally using fold.  

```java
void main() {

    var pairs = List.of(
            new String[]{"a", "1"},
            new String[]{"b", "2"},
            new String[]{"c", "3"});
    
    var maps = pairs.stream()
            .gather(Gatherers.fold(
                    () -> new HashMap<String, String>(),
                    (map, pair) -> {
                        map.put(pair[0], pair[1]);
                        return new HashMap<>(map);
                    }))
            .toList();
    
    maps.forEach(IO::println);
}
```

The `fold` gatherer can build complex collections like maps. Each step shows  
the map as it grows, demonstrating how data structures evolve during stream  
processing.  

## Window with sorting

This example sorts elements within each window.  

```java
void main() {

    var numbers = List.of(3, 1, 4, 1, 5, 9, 2, 6);
    
    var sortedWindows = numbers.stream()
            .gather(Gatherers.windowFixed(4))
            .map(window -> window.stream()
                    .sorted()
                    .toList())
            .toList();
    
    sortedWindows.forEach(IO::println);
}
```

Elements within each window can be sorted independently. This is useful when  
you need to process groups of data where order matters within each group but  
not across groups.  

## Scan with counting

This example counts elements seen so far using scan.  

```java
void main() {

    var items = List.of("apple", "banana", "cherry", "date");
    
    var positions = items.stream()
            .gather(Gatherers.scan(
                    () -> 0,
                    (count, item) -> count + 1))
            .toList();
    
    IO.println("Element positions: " + positions);
}
```

The `scan` gatherer can generate sequences like indices or positions. Each  
output represents how many elements have been processed, useful for numbering  
or tracking progress.  

## Sliding window with all pairs

This example processes all consecutive pairs for comparison.  

```java
void main() {

    var grades = List.of(85, 90, 78, 92, 88);
    
    var comparisons = grades.stream()
            .gather(Gatherers.windowSliding(2))
            .map(window -> {
                var first = window.get(0);
                var second = window.get(1);
                return second > first ? "increased" : 
                        second < first ? "decreased" : "same";
            })
            .toList();
    
    IO.println("Grade changes: " + comparisons);
}
```

Consecutive pairs can be compared to detect changes. This example categorizes  
each transition as an increase, decrease, or no change, useful for analyzing  
sequential data trends.  

## Fixed window with filtering content

This example filters windows based on element properties.  

```java
void main() {

    var words = List.of("cat", "dog", "elephant", "fox", 
            "giraffe", "hippo");
    
    var longWordBatches = words.stream()
            .gather(Gatherers.windowFixed(2))
            .filter(window -> window.stream()
                    .allMatch(w -> w.length() > 3))
            .toList();
    
    IO.println("Batches with all long words: " + longWordBatches);
}
```

Windows can be filtered based on whether all elements meet certain criteria.  
This example only keeps windows where all words are longer than 3 characters,  
demonstrating predicate-based window selection.  

## Fold with average tracking

This example maintains a running average using fold.  

```java
record Average(double sum, int count) {
    Average add(double value) {
        return new Average(sum + value, count + 1);
    }
    double value() {
        return count == 0 ? 0.0 : sum / count;
    }
}

void main() {

    var scores = List.of(85.0, 90.0, 78.0, 92.0, 88.0);
    
    var runningAvg = scores.stream()
            .gather(Gatherers.fold(
                    () -> new Average(0.0, 0),
                    (avg, score) -> avg.add(score)))
            .map(Average::value)
            .toList();
    
    IO.println("Running averages: " + runningAvg);
}
```

Complex statistics like running averages can be computed using fold with  
custom state records. Each step shows the average of all values seen so far,  
useful for progressive data analysis.  

## Sliding window with range checking

This example checks if values fall within ranges across windows.  

```java
void main() {

    var measurements = List.of(15, 20, 25, 18, 22, 30);
    
    var inRange = measurements.stream()
            .gather(Gatherers.windowSliding(2))
            .map(window -> {
                var diff = Math.abs(window.get(1) - window.get(0));
                return diff <= 5 ? "stable" : "volatile";
            })
            .toList();
    
    IO.println("Stability: " + inRange);
}
```

Sliding windows can detect stability or volatility by comparing consecutive  
values. This example classifies each transition based on the magnitude of  
change, useful for quality control or anomaly detection.  

## Window with grouping

This example groups elements within windows by properties.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9);
    
    var grouped = numbers.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> window.stream()
                    .collect(Collectors.groupingBy(
                            n -> n % 2 == 0 ? "even" : "odd")))
            .toList();
    
    grouped.forEach(IO::println);
}
```

Elements within each window can be grouped by properties. This example  
separates even and odd numbers within each window, demonstrating nested  
grouping operations.  

## Scan with conditional reset

This example resets the accumulator based on conditions.  

```java
void main() {

    var values = List.of(1, 2, 3, -1, 4, 5, -1, 6);
    
    var segments = values.stream()
            .gather(Gatherers.scan(
                    () -> 0,
                    (sum, val) -> val < 0 ? 0 : sum + val))
            .toList();
    
    IO.println("Segmented sums: " + segments);
}
```

The `scan` gatherer can implement conditional logic that resets state based  
on special values. This example resets the running sum when encountering  
negative values, useful for segmented processing.  

## Fixed window with parallel processing

This example shows how windows can be processed independently.  

```java
void main() {

    var data = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12);
    
    var results = data.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> {
                var sum = window.stream()
                        .mapToInt(Integer::intValue)
                        .sum();
                return "Window sum: " + sum;
            })
            .toList();
    
    results.forEach(IO::println);
}
```

Fixed windows create independent groups that can be processed in parallel or  
separately. Each window's processing doesn't affect others, making this  
pattern ideal for divide-and-conquer approaches.  

## Sliding window with variance calculation

This example calculates variance within sliding windows.  

```java
void main() {

    var values = List.of(10.0, 12.0, 11.0, 15.0, 13.0);
    
    var variances = values.stream()
            .gather(Gatherers.windowSliding(3))
            .map(window -> {
                var avg = window.stream()
                        .mapToDouble(Double::doubleValue)
                        .average()
                        .orElse(0.0);
                var variance = window.stream()
                        .mapToDouble(v -> Math.pow(v - avg, 2))
                        .average()
                        .orElse(0.0);
                return variance;
            })
            .toList();
    
    IO.println("Sliding variances: " + variances);
}
```

Complex statistical calculations can be performed on each window. This  
example computes variance for each sliding window, useful for detecting  
changes in data distribution or identifying anomalies.  

## Fold with multiple accumulators

This example maintains multiple running values simultaneously.  

```java
record MultiStats(int sum, int max, int min, int count) {
    MultiStats update(int value) {
        return new MultiStats(
                sum + value,
                Math.max(max, value),
                Math.min(min, value),
                count + 1);
    }
}

void main() {

    var numbers = List.of(5, 3, 8, 1, 9, 2);
    
    var stats = numbers.stream()
            .gather(Gatherers.fold(
                    () -> new MultiStats(0, Integer.MIN_VALUE, 
                            Integer.MAX_VALUE, 0),
                    (s, n) -> s.update(n)))
            .toList();
    
    stats.forEach(IO::println);
}
```

The `fold` gatherer can track multiple statistics simultaneously. This  
example computes sum, max, min, and count in parallel, showing the power of  
maintaining complex state during stream processing.  

## Window with nested streams

This example processes windows with nested stream operations.  

```java
void main() {

    var matrix = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9);
    
    var processed = matrix.stream()
            .gather(Gatherers.windowFixed(3))
            .map(row -> row.stream()
                    .filter(n -> n % 2 == 0)
                    .map(n -> n * n)
                    .toList())
            .toList();
    
    processed.forEach(IO::println);
}
```

Windows can be processed with complex nested stream operations. This example  
filters and transforms elements within each window, demonstrating the  
composability of stream operations with gatherers.  

## Scan with fibonacci-like sequence

This example generates a fibonacci-like sequence using scan.  

```java
void main() {

    var triggers = List.of(1, 1, 1, 1, 1, 1, 1, 1);
    
    var fibonacci = triggers.stream()
            .gather(Gatherers.scan(
                    () -> new int[]{0, 1},
                    (state, trigger) -> {
                        var next = state[0] + state[1];
                        return new int[]{state[1], next};
                    }))
            .map(state -> state[1])
            .toList();
    
    IO.println("Fibonacci-like: " + fibonacci);
}
```

The `scan` gatherer can generate sequences where each element depends on  
previous values. This example produces a fibonacci-like sequence,  
demonstrating how gatherers enable complex sequence generation.  

## Sliding window with multi-element comparison

This example compares multiple elements within each window.  

```java
void main() {

    var sequence = List.of(5, 3, 8, 2, 9, 1, 7);
    
    var analysis = sequence.stream()
            .gather(Gatherers.windowSliding(3))
            .map(window -> {
                var first = window.get(0);
                var middle = window.get(1);
                var last = window.get(2);
                var isVShaped = first > middle && middle < last;
                return isVShaped ? "V-pattern" : "no pattern";
            })
            .toList();
    
    IO.println("Patterns: " + analysis);
}
```

Sliding windows enable complex pattern detection across multiple elements.  
This example detects V-shaped patterns where the middle value is lower than  
both surrounding values, useful for identifying local minima.  

## Fixed window with custom objects

This example uses windows with complex custom objects.  

```java
record Event(String type, long timestamp, String data) {}

void main() {

    var events = List.of(
            new Event("login", 1000L, "user1"),
            new Event("action", 2000L, "click"),
            new Event("logout", 3000L, "user1"),
            new Event("login", 4000L, "user2"));
    
    var batches = events.stream()
            .gather(Gatherers.windowFixed(2))
            .map(batch -> batch.stream()
                    .map(Event::type)
                    .toList())
            .toList();
    
    batches.forEach(types -> IO.println("Event types: " + types));
}
```

Gatherers work with complex domain objects. This example batches events and  
extracts their types, demonstrating how gatherers fit into real-world event  
processing and log analysis scenarios.  

## Combining gatherers with parallel streams

This example shows gatherers can work with parallel processing.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12);
    
    var windowSums = numbers.parallelStream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> window.stream()
                    .mapToInt(Integer::intValue)
                    .sum())
            .toList();
    
    IO.println("Window sums: " + windowSums);
}
```

Gatherers can be used with parallel streams for performance. Fixed-size  
windows are particularly suitable for parallelization since each window can  
be processed independently without inter-window dependencies.  

## Advanced stateful transformation

This example demonstrates a sophisticated stateful gatherer pattern.  

```java
record State(int prev, List<String> results) {
    State process(int value) {
        var newResults = new ArrayList<>(results);
        if (prev != -1 && value > prev * 2) {
            newResults.add("Spike at " + value);
        }
        return new State(value, newResults);
    }
}

void main() {

    var metrics = List.of(10, 12, 30, 15, 50, 20);
    
    var analysis = metrics.stream()
            .gather(Gatherers.fold(
                    () -> new State(-1, new ArrayList<>()),
                    (state, value) -> state.process(value)))
            .map(State::results)
            .toList();
    
    analysis.forEach(IO::println);
}
```

Complex stateful analysis can be implemented using fold with rich state  
objects. This example detects spikes where values more than double, showing  
how gatherers enable sophisticated stream analytics and anomaly detection.  

## Window with partitioning

This example partitions elements within windows based on predicates.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12);
    
    var partitioned = numbers.stream()
            .gather(Gatherers.windowFixed(4))
            .map(window -> window.stream()
                    .collect(Collectors.partitioningBy(
                            n -> n % 2 == 0)))
            .toList();
    
    partitioned.forEach(IO::println);
}
```

The `partitioningBy` collector can be applied within windows to split  
elements into two groups. This example separates even and odd numbers within  
each window, creating a map with boolean keys for each partition.  

## Scan with running difference

This example calculates running differences from the first element.  

```java
void main() {

    var baseline = List.of(100, 105, 98, 110, 95);
    
    var differences = baseline.stream()
            .gather(Gatherers.scan(
                    () -> new int[]{-1, 0},
                    (state, value) -> {
                        if (state[0] == -1) {
                            return new int[]{value, 0};
                        }
                        return new int[]{state[0], value - state[0]};
                    }))
            .map(state -> state[1])
            .toList();
    
    IO.println("Differences from baseline: " + differences);
}
```

The `scan` gatherer can maintain reference values for comparison. This  
example tracks differences from the first element, useful for analyzing  
deviations from a baseline or starting point in sequential data.  

## Fixed window with statistics summary

This example computes comprehensive statistics for each window.  

```java
record WindowStats(int count, double sum, double avg, int min, int max) {}

void main() {

    var values = List.of(10, 20, 15, 25, 30, 18, 22, 28);
    
    var stats = values.stream()
            .gather(Gatherers.windowFixed(4))
            .map(window -> {
                var count = window.size();
                var sum = window.stream().mapToInt(Integer::intValue).sum();
                var avg = sum / (double) count;
                var min = window.stream().mapToInt(Integer::intValue).min()
                        .orElse(0);
                var max = window.stream().mapToInt(Integer::intValue).max()
                        .orElse(0);
                return new WindowStats(count, sum, avg, min, max);
            })
            .toList();
    
    stats.forEach(IO::println);
}
```

Multiple statistics can be computed for each window to create comprehensive  
summaries. This example calculates count, sum, average, minimum, and maximum  
for each window, providing a complete statistical profile useful for data  
analysis and reporting.
