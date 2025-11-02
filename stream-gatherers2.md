# Stream Gatherers

This document contains progressively complex Java examples demonstrating  
advanced Stream Gatherers usage with custom implementations and sophisticated  
patterns using modern Java 25 syntax.  

Stream Gatherers are a powerful preview feature introduced in Java 22 (JEP  
461) that extend the Stream API with custom intermediate operations. While  
standard stream operations like `map`, `filter`, and `reduce` cover many use  
cases, gatherers enable complex transformations that maintain state, look at  
multiple elements together, or implement custom windowing and batching logic  
that would be difficult or impossible with existing operations.  

A gatherer is defined by four key components working together. First, the  
initializer creates the initial state object that will be maintained  
throughout the stream processing. Second, the integrator is a function that  
processes each element, updates the state, and decides what values to emit  
downstream. Third, the combiner merges states from parallel processing  
(optional for sequential-only gatherers). Finally, the finisher produces any  
final output after all elements have been processed. This architecture allows  
gatherers to implement sophisticated operations while maintaining the  
composability and declarative style of the Stream API.  

Gatherers bridge the gap between simple stateless operations and complex  
stateful transformations. They excel at tasks like windowing operations that  
group consecutive elements, maintaining running calculations like cumulative  
sums or moving averages, implementing custom filtering logic that depends on  
previous elements, and creating batches or groups with specific criteria.  
Unlike collectors that operate at the end of a stream pipeline, gatherers are  
intermediate operations that can be combined with other stream operations and  
chained with other gatherers.  

The `Gatherer` interface provides factory methods like `ofSequential` for  
creating sequential gatherers and `of` for parallel-capable gatherers. The  
built-in `Gatherers` class offers common patterns like `windowFixed` for  
fixed-size windows, `windowSliding` for overlapping windows, `scan` for  
cumulative operations, and `fold` for stateful accumulation. Custom gatherers  
can implement domain-specific logic, making them powerful tools for data  
processing pipelines in modern Java applications.




## Custom sum gatherer

This example demonstrates creating a custom gatherer for summing integers.  

```java
void main() {
  // Create a gatherer that accumulates the sum using a custom approach
  Gatherer<Integer, ?, Integer> sumGatherer = Gatherer
      .ofSequential(
          () -> new AtomicInteger(0),
          (state, element, downstream) -> {
            // Accumulate the sum in state
            state.addAndGet(element);
            return !downstream.isRejecting();
          },
          (state, downstream) -> {
            // Finisher: push the final sum downstream
            downstream.push(state.get());
          });

  List<Integer> numbers = List.of(1, 2, 3, 4, 5);
  numbers.stream().gather(sumGatherer).findFirst().ifPresent(IO::println);
}
```

The custom sum gatherer uses `AtomicInteger` for mutable state accumulation.  
The integrator adds each element to the state, and the finisher pushes the  
final sum downstream. This demonstrates the basic structure of a gatherer with  
initialization, integration, and finalization phases.  

## Running maximum

This example tracks the maximum value seen so far in the stream.  

```java
void main() {
    List<Integer> runningMax = Stream.of(3, 1, 4, 1, 5, 9)
            .gather(runningMaxGatherer())
            .toList();

    System.out.println("Running Maximum: " + runningMax);
}

// Gatherer<InputType, StateType, OutputType>
// InputType: Integer (elements processed)
// StateType: int[] (internal state for running max)
// OutputType: Integer (values emitted downstream)
Gatherer<Integer, int[], Integer> runningMaxGatherer() {
    return Gatherer.ofSequential(
            () -> new int[]{Integer.MIN_VALUE}, // Use an array to store state
            // integrator: updates state and emits results
            // downstream: receives values emitted by the gatherer for further processing or collection
            (state, element, downstream) -> {
                state[0] = Math.max(state[0], element); // Compute max
                downstream.push(state[0]); // Emit running max to downstream
                return true;
            });
}
```

The running max gatherer maintains state using an array to track the current  
maximum. For each element, it computes the new maximum and emits it  
downstream. This pattern is useful for tracking running statistics or  
monitoring thresholds in sequential data.  

## Counting with scan

This example uses the built-in scan gatherer to count positive and negative  
numbers.  

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Gatherers;

// Simple class to hold the counts of positive and negative numbers
class Count {
    public int positive;
    public int negative;

    public Count() {}

    public Count(int pos, int neg) {
        this.positive = pos;
        this.negative = neg;
    }
}

// Main method demonstrating counting positives and negatives using Gatherers.scan
void main() {
    // Sample list of integers with both positive and negative values
    var numbers = List.of(1, -2, 3, -4, 5, -3, 4, -9, 8);

    // Gatherers.scan applies the function cumulatively: starts with initial
    // Count(0,0), then updates it for each element, producing intermediate
    // states in the stream Count positive and negative elements using
    // Gatherers.scan; reuses a mutable Count object for memory efficiency,
    // though scan produces intermediate stream elements
    var count = numbers.stream()
            .gather(Gatherers.scan(Count::new, (c, elem) -> {
                c.positive += elem > 0 ? 1 : 0;
                c.negative += elem < 0 ? 1 : 0;
                return c;
            })).collect(Collectors.toList()).getFirst();

    // Output the final counts
    IO.println("Positive count: " + count.positive);
    IO.println("Negative count: " + count.negative);
}
```

The `Gatherers.scan` method applies a function cumulatively to each element  
with an initial state. This example counts positive and negative numbers by  
updating a mutable Count object. The scan produces intermediate states at each  
step, making it useful for tracking running totals or statistics.  

### Alternative using reduce

This example shows the same counting logic using the standard reduce  
operation.  

```java
import java.util.List;

// Immutable record to hold the counts of positive and negative numbers
record Count(int positive, int negative) {}

// Main method demonstrating counting positives and negatives using Stream.reduce
void main() {
    // Sample list of integers with both positive and negative values
    var numbers = List.of(1, -2, 3, -4, 5, -3, 4, -9, 8);

    // Use reduce to accumulate counts of positive and negative numbers into a final Count object
    var count = numbers.stream()
            .reduce(new Count(0, 0), 
                // Accumulator: for each element, increment positive or negative count
                (c, elem) -> new Count(
                    c.positive + (elem > 0 ? 1 : 0),
                    c.negative + (elem < 0 ? 1 : 0)
                ), 
                // Combiner: merge counts from parallel sub-streams (not used in sequential streams)
                (c1, c2) -> new Count(c1.positive + c2.positive, c1.negative + c2.negative));

    // Output the final counts
    System.out.println("Positive count: " + count.positive);
    System.out.println("Negative count: " + count.negative);
}
```

Using `reduce` instead of scan provides the final result only, without  
intermediate states. The immutable record approach with reduce is more  
functional, creating new Count instances rather than mutating state. This  
comparison shows different approaches to stateful stream operations.  

## Pairwise combinations

This example creates pairwise combinations using fixed windows.  

```java
import java.util.stream.Collectors;
import java.util.stream.Gatherers;
import java.util.stream.Stream;

// Example demonstrating how to create pairwise combinations from a stream using
// Gatherers.windowFixed
void main(String[] args) {

    // Create a stream of integers
    Stream<Integer> numbers = Stream.of(1, 2, 3, 4, 5, 6);

    // Use windowFixed(2) to group elements into pairs, then format each pair as a string
    String pairs = numbers.gather(Gatherers.windowFixed(2))
        .map(list -> "(" + list.get(0) + "," + list.get(1) + ")") // Format each pair as (a,b)
        .collect(Collectors.joining(" | ")); // Join all formatted pairs with " | "

    IO.println(pairs); // Output: (1,2) | (3,4) | (5,6)
}
```

Fixed windows of size 2 create non-overlapping pairs from the stream. Each  
window becomes a separate list that can be processed independently. This is  
useful for batch processing or grouping related items together.  

## Fixed window grouping

This example demonstrates grouping elements into fixed-size windows.  

```java
import java.util.List;
import java.util.stream.Gatherers;


void main() {

    var words = List.of("sky", "blue", "corn", "war", "coin", 
        "cloud", "stream", "Java", "Scala");

    var res = gthree(words);
    System.out.println(res);
}

List<List<String>> gthree(List<String> words) {
    return words.stream()                  // ⟵ Source
        .gather(Gatherers.windowFixed(3))  // ⟵ Intermediate operation
        .toList();                         // ⟵ Terminal operation
}
```


## Running sum

```java
import java.util.List;
import java.util.stream.Stream;


void main() {
    // Example 1: Gatherer to calculate running sum
    List<Integer> runningSums = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
            .gather(runningSumGatherer())
            .toList();
    System.out.println("Running Sums: " + runningSums);
}

Gatherer<Integer, int[], Integer> runningSumGatherer() {
    return Gatherer.ofSequential(
            () -> new int[] { 0 },
            (state, element, downstream) -> {
                state[0] += element;
                downstream.push(state[0]);
                return true;
            },
            Gatherer.defaultFinisher()
    // (state, downstream) -> {}
    );
}
```

This gatherer uses an int array to maintain mutable state for the running sum.  
Each element is added to the accumulated total, and the current sum is emitted  
downstream. The default finisher is used since no final cleanup is needed.  

### Running sum with peek

This example adds a peek function to observe intermediate states.  

```java
import java.util.List;
import java.util.function.Consumer;
import java.util.stream.Stream;

// Main class demonstrating custom Gatherer usage for calculating running sums
// with peek functionality
void main() {
    // Example: Calculate running sums of numbers 1-10, with peek to observe each
    // element
    List<Integer> runningSums = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
            .gather(runningSumGatherer(System.out::println)) // Apply gatherer with peek that prints each element
            .toList(); // Collect results into a list
    IO.println("Running Sums: " + runningSums);
}

/**
 * Creates a Gatherer that computes running sums while allowing observation of
 * elements via peek.
 * 
 * @param peek A Consumer that will be called for each element, allowing side
 *             effects like logging
 * @return A Gatherer that accumulates running sums
 */
Gatherer<Integer, int[], Integer> runningSumGatherer(Consumer<Integer> peek) {
    return Gatherer.ofSequential(
            // Initializer: Creates state to hold the current sum, starting at 0
            () -> new int[] { 0 },

            // Integrator: Processes each element, updates state, and pushes result
            // downstream
            (state, element, downstream) -> {
                peek.accept(state[0]); // Perform peek action on the current state (e.g., print it)
                state[0] += element; // Add current element to the running sum
                downstream.push(state[0]); // Push the updated sum to the downstream consumer
                return true; // Continue processing (return false to short-circuit)
            },

            // Finisher: Default finisher handles any final state cleanup (none needed here)
            Gatherer.defaultFinisher());
}
```

Adding a peek consumer allows observation of the running sum at each step  
without affecting the computation. This is useful for debugging, logging, or  
triggering side effects during stream processing while maintaining the  
functional pipeline structure.  

## Sliding pairs window

This example creates overlapping pairs using a custom gatherer.  

```java
void main() {

    List<List<Integer>> pairs = Stream.of(1, 2, 3, 4, 5)
            .gather(pairWindowGatherer())
            .toList();
    System.out.println("Sliding Window Pairs: " + pairs);

}

Gatherer<Integer, List<Integer>, List<Integer>> pairWindowGatherer() {
    return Gatherer.ofSequential(
            () -> new ArrayList<>(),
            (state, element, downstream) -> {
                state.add(element);
                if (state.size() == 2) {
                    downstream.push(List.copyOf(state));
                    state.clear();
                    state.add(element); // For overlapping, use: state.remove(0);
                }
                return true;
            },
            (state, downstream) -> {
            });
}

```

This custom gatherer creates non-overlapping pairs by maintaining a buffer. To  
create overlapping pairs, you would use `state.remove(0)` instead of  
`state.clear()`. This demonstrates stateful buffering for windowing operations.  

## Stateful transaction validation

This example validates transactions with running balance tracking.  

```java
import java.util.ArrayList;
import java.util.List;

public class StatefulValidationGatherer {
    public static void main(String[] args) {
        List<String> transactions = List.of(
            "DEPOSIT 100",
            "WITHDRAW 50",
            "WITHDRAW 200",  // Invalid - insufficient balance
            "DEPOSIT 75",
            "WITHDRAW 125"   // Valid after deposit
        );

        List<String> validTransactions = validateTransactions(transactions, 100);

        System.out.println("Valid Transactions:");
        validTransactions.forEach(System.out::println);
    }

    static List<String> validateTransactions(List<String> transactions, double initialBalance) {
        List<String> validTransactions = new ArrayList<>();
        double balance = initialBalance;

        for (String transaction : transactions) {
            String[] parts = transaction.split(" ");
            double amount = Double.parseDouble(parts[1]);

            if (parts[0].equals("DEPOSIT")) {
                balance += amount;
                validTransactions.add(transaction);
            } else if (parts[0].equals("WITHDRAW") && balance >= amount) {
                balance -= amount;
                validTransactions.add(transaction);
            }
        }

        return validTransactions;
    }
}
```

This example demonstrates stateful validation where each transaction's validity  
depends on the current balance. While this could be implemented as a gatherer,  
the traditional loop approach is shown for comparison. A gatherer version would  
maintain balance as state and filter invalid transactions.  

## Complex gatherer composition

This example combines multiple gatherer operations including takeWhile, fold,  
and window.  

```java

import java.util.List;
import java.util.Arrays;
import java.util.function.BiFunction;
import java.util.function.Predicate;
import java.util.stream.Stream;
import java.util.stream.Gatherers;
import java.util.stream.Gatherer;
import java.util.stream.Collectors;

//  BiFunction<Integer, Integer, Integer> func3 = (total, next) -> total + next[0] * next[1];

BiFunction<Integer, Integer, Integer> addFun = (x, y) -> x + y;

void main() {

    // var res = Stream.iterate(0, i -> i + 1)
    // .gather(Gatherers.windowFixed(3))
    // .limit(100)
    // .collect(Collectors.toList());

    // System.out.println(res);

    var res11 = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10).stream()
            .gather(Gatherers.windowFixed(2))
            .gather(Gatherers.fold(() -> 0, (total, next) -> total + next.get(0) * next.get(1)))
            .findFirst().orElse(0);

    System.out.println(res11);

    List<String> words = List.of("the", "be", "two", "of", "and",
            "a", "war", "in", "that");
    // var res2 = words.stream()
    // .gather(Gatherers.windowFixed(3))
    // .toList();

    // System.out.println(res2);

    var res3 = words.stream()
            .gather(takeWhile(e -> !e.startsWith("w")))
            .toList();

    System.out.println(res3);

    // Example using custom mapping gatherer and toLengths
    var lengths = toLengths(words);
    System.out.println("Word lengths: " + lengths);

    // Example demonstrating custom Integrator and Downstream interfaces
    var upperCased = words.stream()
            .gather(mapping(String::toUpperCase))
            .toList();
    System.out.println("Uppercased: " + upperCased);
}

// Predicate<String> p = e -> !e.startsWith("w");

<T> Gatherer<T, ?, T> takeWhile(Predicate<? super T> predicate) {
    return Gatherer.ofSequential(
            () -> null,
            (nothing, e, downstream) -> predicate.test(e) && downstream.push(e),
            // (l, r) -> l,
            // (l, r) -> l,
            (nothing, downstream) -> {
            });
}

// @FunctionalInterface
// public interface Integrator<A, T, R> {
//     boolean integrate(A state, T element, Downstream<? super R> downstream);
// }

// @FunctionalInterface
// public interface Downstream<T> {
//     boolean push(T element);
// }

public <T, R> Gatherer<T, Void, R> mapping(Function<T, R> mapper) {
    return Gatherer.ofSequential(
            Gatherer.Integrator.ofGreedy(
                    (_, element, downstream) -> {
                        R mappedElement = mapper.apply(element);
                        return downstream.push(mappedElement);
                    }));
}

public List<Integer> toLengths(List<String> words) {
    return words.stream()
            .gather(mapping(String::length))
            .toList();
}

```

This example demonstrates the composition of multiple gatherers and custom  
implementations. The `takeWhile` custom gatherer short-circuits processing  
when the predicate fails. The `mapping` gatherer transforms elements, and  
`fold` accumulates results. This showcases the power of combining gatherers  
for complex transformations.  

## Map and filter combination

This example creates a gatherer that combines mapping and filtering.  

```java
// Map Filter Gatherer
<T, R> Gatherer<T, ?, R> mapFilter(
        Function<? super T, ? extends R> mapper,
        Predicate<? super R> filter) {

    return Gatherer.of(
            (_, element, downstream) -> {
                R mappedElement = mapper.apply(element);
                if (filter.test(mappedElement)) {
                    return downstream.push(mappedElement);
                }
                return true;
            });
}

void main() {
    var stream = Stream.of("one", "two", "three", "four", "five");
    var result = stream
            .gather(mapFilter(String::length, length -> length > 3))
            .toList();
    System.out.println("result = " + result);

}
```

The `mapFilter` gatherer combines two operations into one efficient pass.  
Elements are first transformed by the mapper, then the filter is applied to  
the mapped result. Only elements passing the filter are emitted downstream,  
reducing unnecessary processing.  

## Case-insensitive distinct

This example implements case-insensitive deduplication.  

```java
// Distinct Ignore Case Gatherer
Gatherer<String, ?, String> distinctIgnoreCase() {

    return Gatherer.ofSequential(
            HashSet::new,
            (set, element, downstream) -> {
                if (set.add(element.toLowerCase())) {
                    return downstream.push(element);
                }
                return true;
            });
}

void main() {
    var stream = Stream.of("one", "One", "ONE", "Two", "two", "tWo");
    var result = stream.gather(distinctIgnoreCase()).toList();
    System.out.println("result = " + result);
}
```

The distinct ignore case gatherer uses a HashSet to track seen values in  
lowercase form. Each element's lowercase version is checked against the set;  
if new, the original element is emitted. This demonstrates custom  
deduplication logic beyond the standard `distinct` operation.  

## Filtering even numbers

This example creates a gatherer that filters even numbers.  

```java
import java.util.stream.Gatherer;

void main() {
    List<Integer> evens = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
            .gather(evenGatherer())
            .toList();
    System.out.println("Even Numbers: " + evens);
}

Gatherer<Integer, Void, Integer> evenGatherer() {
    return Gatherer.ofSequential(
            // () -> null,
            Gatherer.defaultInitializer(),
            integrator(),
            // (_, element, downstream) -> {
            //     if (element % 2 == 0)
            //         downstream.push(element);
            //     return true;
            // },
            Gatherer.defaultFinisher());
}

Gatherer.Integrator<Void, Integer, Integer> integrator() {
    return Gatherer.Integrator.ofGreedy((_, element, downstream) -> {
        if (element % 2 == 0) {
            downstream.push(element);
        }
        return true; // Continue processing
    });
}
```

This gatherer demonstrates filtering with explicit integrator creation. The  
`ofGreedy` integrator processes all elements eagerly. Only even numbers are  
pushed downstream. The default initializer and finisher are used since no  
state maintenance or cleanup is required.  

## Filter and transform combination

This example combines filtering and transformation in a single gatherer.  

```java
void main() {

    List<String> filteredTransformed = Stream.of("apple", "bat", "cat", "dog", "elephant")
            .gather(filterAndTransformGatherer(s -> s.length() > 3, String::toUpperCase))
            .toList();
    System.out.println("Filtered and Transformed: " + filteredTransformed);
}

// Gatherer that combines filtering and transformation
<T, R> Gatherer<T, ?, R> filterAndTransformGatherer(
        Predicate<T> predicate,
        Function<T, R> mapper) {
    return Gatherer.of(
            Gatherer.Integrator.ofGreedy((_, element, downstream) -> {
                if (predicate.test(element)) {
                    downstream.push(mapper.apply(element));
                }
                return true; // Continue processing
            }));
}
```

This gatherer implements a common pattern of filtering based on a predicate  
and transforming matching elements. Elements that pass the filter are  
transformed and emitted. This is more efficient than separate filter and map  
operations since it combines both in a single pass.  

## Custom mapping gatherer

This example demonstrates a custom mapping implementation.  

```java
import java.util.List;
import java.util.function.Function;
import java.util.stream.Gatherer;
import java.util.stream.Gatherers;
import java.util.stream.Stream;

void main() {

    List<List<Integer>> groups = Stream.iterate(1, i -> i + 1)
            .limit(8)
            .gather(Gatherers.windowFixed(3))
            .toList();

    System.out.println(groups);

    Stream.of(1, 2, 3, 4, 5)
            .gather(Gatherers.windowSliding(2))
            .forEach(System.out::println);

    List<String> result = List.of("hello", "java", "stream")
            .stream()
            .gather(customMapping(String::toUpperCase))
            .toList();

    System.out.println(result);

}

<T, R> Gatherer<T, ?, R> customMapping(Function<T, R> mapper) {
    Gatherer.Integrator<Void, T, R> integrator = (_, element, downstream) -> {
        downstream.push(mapper.apply(element));
        return true;
    };
    return Gatherer.of(integrator);
}
```

The custom mapping gatherer shows how to create a simple transformation  
gatherer using just an integrator. The `Gatherer.of` factory method is used  
for stateless operations. This demonstrates building reusable stream operation  
components.  

### Running sum with AtomicInteger

This alternative implementation uses AtomicInteger for state.  

```java
void main(String[] args) {
    List<Integer> runningSums = Stream.of(1, 2, 3, 4, 5)
            .gather(runningSumGatherer())
            .toList();
    System.out.println("Running Sums: " + runningSums); // Expected: [1, 3, 6, 10, 15]
}

// Gatherer that maintains a running sum using AtomicInteger
static Gatherer<Integer, AtomicInteger, Integer> runningSumGatherer() {
    return Gatherer.ofSequential(
            AtomicInteger::new, // Use AtomicInteger for mutable state
            Gatherer.Integrator.ofGreedy((state, element, downstream) -> {
                downstream.push(state.addAndGet(element)); // Atomic update and emit current sum
                return true; // Continue processing
            }),
            (state, downstream) -> {
            } // No additional final output needed
    );
}
```

AtomicInteger provides a thread-safe mutable state holder. The `addAndGet`  
method atomically updates and returns the new sum. This approach is cleaner  
than using arrays for simple numeric state and works well in concurrent  
scenarios.  

### Running sum alternative

Another running sum implementation with explicit integrator.  
import java.util.List;
import java.util.stream.Gatherer;
import java.util.stream.Stream;

void main(String[] args) {
    // Example 1: Gatherer to calculate running sum
    List<Integer> runningSums = Stream.of(1, 2, 3, 4, 5)
            .gather(runningSumGatherer())
            .toList();
    System.out.println("Running Sums: " + runningSums);

}

// Gatherer that maintains a running sum of numbers
Gatherer<Integer, int[], Integer> runningSumGatherer() {
    return Gatherer.ofSequential(
            () -> new int[]{0}, // Initial state
            Gatherer.Integrator.ofGreedy((state, element, downstream) -> {
                state[0] += element;
                downstream.push(state[0]);
                return true; // Continue processing
            }),
            (state, downstream) -> {} // Finisher emits final state
    );
}
```

This variant explicitly uses `Integrator.ofGreedy` to create the integrator  
function. The pattern remains the same: maintain state in an array, accumulate  
values, and emit running totals. Multiple implementations show different  
coding styles for the same operation.  

## Limiting with custom gatherer

This example implements a custom limit operation.  

```java

// Limit Gatherer
<T> Gatherer<T, ?, T> limit(long limit) {
    return Gatherer.ofSequential(
            () -> new Object() {
                long counter = 0L;
            },
            (counter, element, downstream) -> {
                if (counter.counter >= limit) {
                    return false;
                } else {
                    counter.counter++;
                    return downstream.push(element);
                }
            });
}

void main() {
    var stream = Stream.of(1, 2, 3, 4, 5);
    var result = stream.gather(limit(3L)).toList();
    System.out.println("result = " + result);

}

```

The custom limit gatherer demonstrates short-circuiting by returning false  
when the limit is reached. An anonymous object with a counter field tracks how  
many elements have been processed. This shows how to implement operations that  
stop processing early.  

## Batch processing with transformation

This example processes elements in batches with custom transformations.  

```java
import java.util.*;
import java.util.stream.*;
import java.util.function.*;

public class BatchProcessGatherer {
    public static void main(String[] args) {
        List<List<Integer>> batches = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
            .gather(batchAndProcess(
                3,
                list -> {
                    int sum = list.stream().mapToInt(i -> i).sum();
                    return "Sum of " + list + " = " + sum;
                }
            ))
            .toList();
        
        System.out.println("Batch Processing Results:");
        batches.forEach(System.out::println);
        // Output:
        // Sum of [1, 2, 3] = 6
        // Sum of [4, 5, 6] = 15
        // Sum of [7, 8, 9] = 24
        // Sum of [10] = 10
    }

    static <T, R> Gatherer<T, ?, R> batchAndProcess(
            int batchSize,
            Function<List<T>, R> processor) {
        return Gatherer.of(
            () -> new ArrayList<T>(batchSize),
            (state, element, downstream) -> {
                state.add(element);
                if (state.size() >= batchSize) {
                    downstream.push(processor.apply(state));
                    state.clear();
                }
                return true;
            },
            (state, downstream) -> {
                if (!state.isEmpty()) {
                    downstream.push(processor.apply(state));
                }
            }
        );
    }
}
```

The batch processing gatherer accumulates elements into batches of a specified  
size, applies a processing function to each complete batch, and emits the  
results. The finisher handles any remaining incomplete batch. This pattern is  
useful for bulk operations or when processing requires groups of elements.  

## Deduplication with HashSet

This example removes consecutive duplicates from a stream.  

```java
void main() {

    List<String> deduplicated = Stream.of("apple", "apple", "banana",
            "banana", "banana", "cherry", "apple")
            .gather(deduplicationGatherer())
            .toList();

    System.out.println("Deduplicated List: " + deduplicated); // Expected: [apple, banana, cherry, apple]
}

// removes all duplcates from the stream, keeping the first occurrence of each
// element
Gatherer<String, HashSet<String>, String> deduplicationGatherer() {
    return Gatherer.ofSequential(
            HashSet::new, // Initial state as a HashSet to track seen elements
            Gatherer.Integrator.ofGreedy((seen, element, downstream) -> {
                if (seen.add(element)) { // Only push if element is new
                    downstream.push(element);
                }
                return true; // Continue processing
            }));
}
```

The first deduplication gatherer uses a HashSet to track all seen elements,  
emitting only new values. This provides global deduplication across the entire  
stream. Elements are kept in their first-encountered order, with duplicates  
removed regardless of position.  

### Consecutive deduplication

This alternative removes only consecutive duplicates.  

```java
import java.util.stream.Gatherer;
import java.util.stream.Stream;

class State {
    String previous;
}

void main() {

    Gatherer<String, State, String> deduplicate = Gatherer.ofSequential(
            State::new, // Initial state (no previous element)
            (state, element, downstream) -> {
                if (state.previous == null || !state.previous.equals(element)) {
                    downstream.push(element); // Push if different from previous
                }
                state.previous = element; // Update state to current element
                return true; // Continue processing
            },
            Gatherer.defaultFinisher());

    Stream<String> words = Stream.of("a", "a", "b", "b", "c", "a");
    var result = words.gather(deduplicate).toList();
    System.out.println(result); // Output: [a, b, c, a]
}
```

The consecutive deduplication gatherer only removes elements that immediately  
follow an identical element. State tracks just the previous element, not all  
seen values. This is useful for cleaning up runs of duplicates while  
preserving non-consecutive repeats.  

## Rate limiting gatherer

This example implements rate limiting to control emission speed.  

```java
void main() throws InterruptedException {
    Stream.generate(() -> (char) ('A' + Math.random() * 26))
            .map(String::valueOf)
            .limit(50) // Generate 10 random characters
            .gather(rateLimitingGatherer(1000)) // 1 item per second
            .forEach(e -> System.out.println(e + " " + System.currentTimeMillis()));
}

// Limits the stream to emit at most one element per specified milliseconds
Gatherer<String, Long, String> rateLimitingGatherer(long millis) {
    return Gatherer.ofSequential(
            () -> 0L, // Last emission time
            (lastTime, element, downstream) -> {
                long now = System.currentTimeMillis();
                long sleepTime = lastTime + millis - now;
                if (sleepTime > 0) {
                    try {
                        Thread.sleep(sleepTime);
                    } catch (InterruptedException e) {
                        return false;
                    }
                }
                downstream.push(element);
                return true;
            });
}
```

The first rate limiting gatherer ensures elements are emitted at most once per  
specified interval. It calculates required sleep time based on the last  
emission and current time. This is useful for controlling API call rates or  
managing resource consumption.  

### Rate limiting alternative

An alternative rate limiting implementation with improved timing.  

```java

void main(String[] args) throws InterruptedException {
    Stream.generate(() -> (char) ('A' + Math.random() * 26))
            .map(String::valueOf)
            .limit(10) // Generate 10 random characters
            .gather(rateLimitingGatherer(1000)) // Emit every 1 second
            .forEach(e -> System.out.println(e + " " + System.currentTimeMillis()));
}

Gatherer<String, long[], String> rateLimitingGatherer(long millis) {
    return Gatherer.ofSequential(
            () -> new long[] { System.currentTimeMillis() }, // Track last emission time
            Gatherer.Integrator.ofGreedy((state, element, downstream) -> {
                long now = System.currentTimeMillis();
                long elapsed = now - state[0];

                if (elapsed >= millis) { // Ensure emission happens with correct delay
                    downstream.push(element);
                    state[0] = System.currentTimeMillis(); // Update last emission time
                } else {
                    try {
                        Thread.sleep(millis - elapsed); // Sleep only for the remaining time
                    } catch (InterruptedException e) {
                        return false;
                    }
                    downstream.push(element);
                    state[0] = System.currentTimeMillis();
                }

                return true;
            }),
            (state, downstream) -> {
            } // No final output needed
    );
}
```

This alternative tracks the last emission time in an array and calculates  
elapsed time more precisely. It only sleeps for the remaining time needed,  
providing more accurate rate limiting. Both approaches work but this one  
handles timing more efficiently.  

## MapMulti for flattening

This example demonstrates using mapMulti to flatten nested structures.  

```java
void main() {

    String data = """
            one,two
            falcon,eagle
            spy,hunter
            string,number
            nest,tree
            cup,table
            cloud,rain
            war,artillery
            water,buck
            risk,gain
            """;

    List<String> res = data.lines()
            .map(line -> line.split(",")) // Map each line to an array of words
            .flatMap(Arrays::stream) // Flatten arrays into a single stream
            .toList();

    System.out.println(res);

    var res2 = data.lines().<String>mapMulti((line, consumer) -> {

        for (var c : line.split(",")) {

            consumer.accept(c);
        }

    }).toList();

    System.out.println(res2);
}
```

The `mapMulti` operation is an alternative to flatMap that can be more  
efficient for certain use cases. It accepts each element and a consumer,  
allowing you to emit zero or more elements. This first example compares  
flatMap with mapMulti for splitting CSV lines.  

### MapMulti with records

This example uses mapMulti to flatten nested record structures.  

```java
import java.util.List;

record Country(String name, List<City> cities) {
}

record City(String name, String country, int population) {
}

void main() {

    List<Country> countries = List.of(
            new Country("USA", List.of(
                    new City("New York", "USA", 8419600),
                    new City("Los Angeles", "USA", 3980400))),
            new Country("Canada", List.of(
                    new City("Toronto", "Canada", 2930000),
                    new City("Vancouver", "Canada", 631486))),
            new Country("Mexico", List.of(
                    new City("Mexico City", "Mexico", 9209944),
                    new City("Guadalajara", "Mexico", 5295915))));

    List<Object> cities = countries.stream()
            .mapMulti((country, downstream) -> country.cities().forEach(downstream::accept)).toList();
    System.out.println(cities);

    List<City> cities2 = countries.stream()
            .<City>mapMulti((country, downstream) -> country.cities().forEach(downstream::accept)).toList();
    System.out.println(cities2);


    List<String> colors = List.of("Red", "Green", "Blue");
    List<String> sizes = List.of("S", "M", "L");
    
    List<String> res = colors.stream().<String>mapMulti((color, downstream) -> {
        sizes.forEach(size -> downstream.accept(color + " " + size));
    }).toList();

    System.out.println(res);



    // Stream<String> products = colors.stream()
    //     .flatMap(color -> 
    //         sizes.stream()
    //             .map(size -> color + " " + size)
    //     );
    
    // products.forEach(System.out::println);
}
```

---

```java
void main() {
    List<String> words = List.of("hello", "world");

    List<Character> characters = words.stream()
            .<Character>mapMulti((word, consumer) -> {
                for (char c : word.toCharArray()) {
                    consumer.accept(c);
                }
            })
            .collect(Collectors.toList());

    System.out.println(characters);
}
```

MapMulti efficiently expands each string into its constituent characters. The  
consumer is called for each character, emitting them as individual elements.  
This is more efficient than using flatMap with streams for simple expansion  
operations.  

### MapMulti with conditional emission

This example demonstrates conditional element emission with mapMulti.  

```java
import java.util.stream.Stream;

void main() {

    Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
            .mapMulti((num, consumer) -> {
                if (num % 2 == 0) {
                    consumer.accept(num * 10);
                }
                if (num % 3 == 0) {
                    consumer.accept(num * 100);
                }
            })
            .forEach(System.out::println);
}
```

MapMulti allows conditional emission where each input can produce zero, one,  
or multiple outputs. This example emits different transformations based on  
divisibility rules. Elements divisible by 2 or 3 generate different outputs,  
showcasing the flexibility of mapMulti for complex transformations.  

## Zip gatherer

This example implements a zip operation to combine two streams.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    var letters = List.of("a", "b", "c", "d", "e");
    
    record Pair<T, U>(T first, U second) {}
    
    var zipped = numbers.stream()
            .gather(zip(letters.iterator()))
            .toList();
    
    zipped.forEach(IO::println);
}

<T, U> Gatherer<T, ?, Pair<T, U>> zip(Iterator<U> other) {
    return Gatherer.ofSequential(
            () -> other,
            Gatherer.Integrator.ofGreedy((state, element, downstream) -> {
                if (state.hasNext()) {
                    downstream.push(new Pair<>(element, state.next()));
                    return true;
                }
                return false;
            }));
}
```

The zip gatherer combines elements from two sequences into pairs. It maintains  
an iterator as state and stops when either sequence is exhausted. This is  
useful for parallel iteration over multiple collections.  

## Partition by predicate

This example partitions elements into two groups based on a predicate.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    record Partitioned<T>(List<T> matching, List<T> nonMatching) {}
    
    var result = numbers.stream()
            .gather(partition(n -> n % 2 == 0))
            .findFirst()
            .orElse(null);
    
    IO.println("Even: " + result.matching());
    IO.println("Odd: " + result.nonMatching());
}

<T> Gatherer<T, ?, Partitioned<T>> partition(Predicate<T> predicate) {
    record State<T>(List<T> matching, List<T> nonMatching) {}
    
    return Gatherer.ofSequential(
            () -> new State<>(new ArrayList<>(), new ArrayList<>()),
            (state, element, downstream) -> {
                if (predicate.test(element)) {
                    state.matching.add(element);
                } else {
                    state.nonMatching.add(element);
                }
                return true;
            },
            (state, downstream) -> {
                downstream.push(new Partitioned<>(state.matching, state.nonMatching));
            });
}
```

The partition gatherer splits elements into two lists based on a predicate.  
All elements are accumulated during processing, then the final partitioned  
result is emitted. This is useful for categorizing data into two groups.  

## Group by key

This example groups elements by a key function.  

```java
void main() {

    var words = List.of("apple", "apricot", "banana", "blueberry", "cherry");
    
    var grouped = words.stream()
            .gather(groupBy(word -> word.charAt(0)))
            .findFirst()
            .orElse(Map.of());
    
    grouped.forEach((key, values) -> 
            IO.println(key + ": " + values));
}

<T, K> Gatherer<T, ?, Map<K, List<T>>> groupBy(Function<T, K> keyMapper) {
    return Gatherer.ofSequential(
            HashMap::new,
            (map, element, downstream) -> {
                K key = keyMapper.apply(element);
                map.computeIfAbsent(key, k -> new ArrayList<>()).add(element);
                return true;
            },
            (map, downstream) -> {
                downstream.push(new HashMap<>(map));
            });
}
```

The groupBy gatherer organizes elements into a map based on a key extraction  
function. It accumulates elements into lists associated with their keys, then  
emits the complete map. This provides custom grouping logic beyond standard  
collectors.  

## Take until predicate

This example takes elements until a predicate becomes true.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var taken = numbers.stream()
            .gather(takeUntil(n -> n > 5))
            .toList();
    
    IO.println(taken);
}

<T> Gatherer<T, ?, T> takeUntil(Predicate<T> predicate) {
    return Gatherer.ofSequential(
            () -> new boolean[]{true},
            (state, element, downstream) -> {
                if (state[0]) {
                    downstream.push(element);
                    if (predicate.test(element)) {
                        state[0] = false;
                    }
                    return true;
                }
                return false;
            });
}
```

The takeUntil gatherer emits elements until the predicate becomes true,  
including the matching element. It uses a boolean array to track whether to  
continue processing. This differs from takeWhile by including the boundary  
element.  

## Drop while predicate

This example drops elements while a predicate is true.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var dropped = numbers.stream()
            .gather(dropWhile(n -> n < 5))
            .toList();
    
    IO.println(dropped);
}

<T> Gatherer<T, ?, T> dropWhile(Predicate<T> predicate) {
    return Gatherer.ofSequential(
            () -> new boolean[]{false},
            (state, element, downstream) -> {
                if (state[0] || !predicate.test(element)) {
                    state[0] = true;
                    downstream.push(element);
                }
                return true;
            });
}
```

The dropWhile gatherer skips elements while the predicate is true, then emits  
all remaining elements. A boolean flag tracks whether dropping has finished.  
This is useful for skipping a header or prefix in sequential data.  

## Interleave streams

This example interleaves elements from two streams.  

```java
void main() {

    var first = List.of(1, 3, 5);
    var second = List.of(2, 4, 6);
    
    var interleaved = first.stream()
            .gather(interleave(second.iterator()))
            .toList();
    
    IO.println(interleaved);
}

<T> Gatherer<T, ?, T> interleave(Iterator<T> other) {
    return Gatherer.ofSequential(
            () -> other,
            (state, element, downstream) -> {
                downstream.push(element);
                if (state.hasNext()) {
                    downstream.push(state.next());
                }
                return true;
            });
}
```

The interleave gatherer alternates elements from two sources. For each element  
from the main stream, it emits that element followed by one from the other  
iterator. This creates an alternating pattern useful for merging sequences.  

## Enumerate with index

This example adds indices to stream elements.  

```java
void main() {

    var words = List.of("apple", "banana", "cherry");
    
    record Indexed<T>(int index, T value) {}
    
    var indexed = words.stream()
            .gather(enumerate())
            .toList();
    
    indexed.forEach(item -> 
            IO.println(item.index() + ": " + item.value()));
}

<T> Gatherer<T, ?, Indexed<T>> enumerate() {
    return Gatherer.ofSequential(
            () -> new int[]{0},
            (state, element, downstream) -> {
                downstream.push(new Indexed<>(state[0]++, element));
                return true;
            });
}
```

The enumerate gatherer pairs each element with its zero-based index. An int  
array maintains the current index counter. This is useful when you need both  
the element and its position in the stream.  

## Distinct by key

This example removes duplicates based on a key function.  

```java
void main() {

    record Person(String name, int age) {}
    
    var people = List.of(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Alice", 35));
    
    var distinct = people.stream()
            .gather(distinctBy(Person::name))
            .toList();
    
    distinct.forEach(IO::println);
}

<T, K> Gatherer<T, ?, T> distinctBy(Function<T, K> keyExtractor) {
    return Gatherer.ofSequential(
            HashSet::new,
            (seen, element, downstream) -> {
                K key = keyExtractor.apply(element);
                if (seen.add(key)) {
                    downstream.push(element);
                }
                return true;
            });
}
```

The distinctBy gatherer removes duplicates based on a key extraction function  
rather than object equality. It tracks seen keys in a HashSet and only emits  
elements with new keys. This provides flexible deduplication logic.  

## Chunking by delimiter

This example chunks elements based on a delimiter predicate.  

```java
void main() {

    var data = List.of("a", "b", "|", "c", "d", "|", "e");
    
    var chunks = data.stream()
            .gather(chunkBy(s -> s.equals("|")))
            .toList();
    
    chunks.forEach(IO::println);
}

<T> Gatherer<T, ?, List<T>> chunkBy(Predicate<T> isDelimiter) {
    return Gatherer.ofSequential(
            ArrayList::new,
            (buffer, element, downstream) -> {
                if (isDelimiter.test(element)) {
                    if (!buffer.isEmpty()) {
                        downstream.push(new ArrayList<>(buffer));
                        buffer.clear();
                    }
                } else {
                    buffer.add(element);
                }
                return true;
            },
            (buffer, downstream) -> {
                if (!buffer.isEmpty()) {
                    downstream.push(new ArrayList<>(buffer));
                }
            });
}
```

The chunkBy gatherer splits elements into chunks based on delimiter elements.  
Non-delimiter elements accumulate in a buffer, which is emitted when a  
delimiter is encountered. The finisher handles any remaining elements.  

## Max by comparator

This example finds the maximum element using a custom comparator.  

```java
void main() {

    record Product(String name, double price) {}
    
    var products = List.of(
            new Product("Widget", 29.99),
            new Product("Gadget", 49.99),
            new Product("Doohickey", 19.99));
    
    var mostExpensive = products.stream()
            .gather(maxBy((a, b) -> Double.compare(a.price(), b.price())))
            .findFirst()
            .orElse(null);
    
    IO.println(mostExpensive);
}

<T> Gatherer<T, ?, T> maxBy(Comparator<T> comparator) {
    record State<T>(T max) {}
    
    return Gatherer.ofSequential(
            () -> new State<T>(null),
            (state, element, downstream) -> {
                if (state.max == null || comparator.compare(element, state.max) > 0) {
                    return new State<>(element);
                }
                return state;
            },
            (state, downstream) -> {
                if (state.max != null) {
                    downstream.push(state.max);
                }
            });
}
```

The maxBy gatherer finds the maximum element according to a custom comparator.  
It maintains the current maximum in state and updates it when a larger element  
is found. The finisher emits the final maximum.  

## Min by comparator

This example finds the minimum element using a custom comparator.  

```java
void main() {

    record Product(String name, double price) {}
    
    var products = List.of(
            new Product("Widget", 29.99),
            new Product("Gadget", 49.99),
            new Product("Doohickey", 19.99));
    
    var cheapest = products.stream()
            .gather(minBy((a, b) -> Double.compare(a.price(), b.price())))
            .findFirst()
            .orElse(null);
    
    IO.println(cheapest);
}

<T> Gatherer<T, ?, T> minBy(Comparator<T> comparator) {
    record State<T>(T min) {}
    
    return Gatherer.ofSequential(
            () -> new State<T>(null),
            (state, element, downstream) -> {
                if (state.min == null || comparator.compare(element, state.min) < 0) {
                    return new State<>(element);
                }
                return state;
            },
            (state, downstream) -> {
                if (state.min != null) {
                    downstream.push(state.min);
                }
            });
}
```

The minBy gatherer finds the minimum element according to a custom comparator.  
Similar to maxBy but with reversed comparison logic. It tracks the smallest  
element seen and emits it at the end.  

## Running product

This example calculates running products of numbers.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    
    var products = numbers.stream()
            .gather(runningProduct())
            .toList();
    
    IO.println(products);
}

Gatherer<Integer, ?, Integer> runningProduct() {
    return Gatherer.ofSequential(
            () -> new int[]{1},
            (state, element, downstream) -> {
                state[0] *= element;
                downstream.push(state[0]);
                return true;
            });
}
```

The running product gatherer multiplies each element with the accumulated  
product and emits the result. Starting with 1, each element contributes to the  
growing product. This is useful for compound calculations or factorial-like  
operations.  

## Sample every nth

This example samples every nth element from the stream.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var sampled = numbers.stream()
            .gather(sampleEvery(3))
            .toList();
    
    IO.println(sampled);
}

<T> Gatherer<T, ?, T> sampleEvery(int n) {
    return Gatherer.ofSequential(
            () -> new int[]{0},
            (state, element, downstream) -> {
                state[0]++;
                if (state[0] % n == 0) {
                    downstream.push(element);
                }
                return true;
            });
}
```

The sampleEvery gatherer emits every nth element, skipping the rest. A counter  
tracks position and only elements at multiples of n are emitted. This is  
useful for downsampling data or extracting periodic samples.  

## Reverse accumulation

This example accumulates elements in reverse order.  

```java
void main() {

    var items = List.of("first", "second", "third");
    
    var reversed = items.stream()
            .gather(reverse())
            .findFirst()
            .orElse(List.of());
    
    reversed.forEach(IO::println);
}

<T> Gatherer<T, ?, List<T>> reverse() {
    return Gatherer.ofSequential(
            ArrayList::new,
            (list, element, downstream) -> {
                list.addFirst(element);
                return true;
            },
            (list, downstream) -> {
                downstream.push(new ArrayList<>(list));
            });
}
```

The reverse gatherer accumulates all elements in reverse order by prepending  
each to a list. The finisher emits the reversed list. This provides stream-  
based reversal without converting to an intermediate collection first.  

## Flatten nested lists

This example flattens nested list structures.  

```java
void main() {

    var nested = List.of(
            List.of(1, 2),
            List.of(3, 4, 5),
            List.of(6));
    
    var flattened = nested.stream()
            .gather(flatten())
            .toList();
    
    IO.println(flattened);
}

<T> Gatherer<List<T>, ?, T> flatten() {
    return Gatherer.ofSequential(
            Gatherer.Integrator.ofGreedy((nothing, list, downstream) -> {
                list.forEach(downstream::push);
                return true;
            }));
}
```

The flatten gatherer expands nested lists into a flat stream of elements. Each  
list is iterated and its elements are pushed downstream individually. This  
simplifies working with nested collection structures.  

## Running average

This example calculates running averages.  

```java
void main() {

    var values = List.of(10.0, 20.0, 30.0, 40.0, 50.0);
    
    var averages = values.stream()
            .gather(runningAverage())
            .toList();
    
    averages.forEach(avg -> IO.println("Avg: " + avg));
}

Gatherer<Double, ?, Double> runningAverage() {
    record State(double sum, int count) {}
    
    return Gatherer.ofSequential(
            () -> new State(0.0, 0),
            (state, element, downstream) -> {
                var newState = new State(state.sum + element, state.count + 1);
                downstream.push(newState.sum / newState.count);
                return newState;
            });
}
```

The running average gatherer maintains both sum and count in state. For each  
element, it calculates and emits the current average. This provides  
progressive average calculations useful for data analysis.  

## Pairwise operation

This example applies an operation to consecutive pairs.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    
    var differences = numbers.stream()
            .gather(pairwise((a, b) -> b - a))
            .toList();
    
    IO.println(differences);
}

<T, R> Gatherer<T, ?, R> pairwise(BiFunction<T, T, R> operation) {
    record State<T>(T previous) {}
    
    return Gatherer.ofSequential(
            () -> new State<T>(null),
            (state, element, downstream) -> {
                if (state.previous != null) {
                    downstream.push(operation.apply(state.previous, element));
                }
                return new State<>(element);
            });
}
```

The pairwise gatherer applies a binary operation to consecutive element pairs.  
It maintains the previous element in state and combines it with the current  
one. This is useful for calculating differences, ratios, or other pair-wise  
metrics.  

## Count by predicate

This example counts elements matching different predicates.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    record Counts(int even, int odd, int greaterThan5) {}
    
    var counts = numbers.stream()
            .gather(countBy())
            .findFirst()
            .orElse(null);
    
    IO.println(counts);
}

Gatherer<Integer, ?, Counts> countBy() {
    record State(int even, int odd, int greaterThan5) {}
    
    return Gatherer.ofSequential(
            () -> new State(0, 0, 0),
            (state, element, downstream) -> {
                return new State(
                        state.even + (element % 2 == 0 ? 1 : 0),
                        state.odd + (element % 2 != 0 ? 1 : 0),
                        state.greaterThan5 + (element > 5 ? 1 : 0));
            },
            (state, downstream) -> {
                downstream.push(new Counts(state.even, state.odd, state.greaterThan5));
            });
}
```

The countBy gatherer tracks multiple counts simultaneously based on different  
conditions. State accumulates counts for each predicate, and the finisher  
emits the complete statistics. This enables multi-dimensional counting in one  
pass.  

## Skip every nth

This example skips every nth element.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var filtered = numbers.stream()
            .gather(skipEvery(3))
            .toList();
    
    IO.println(filtered);
}

<T> Gatherer<T, ?, T> skipEvery(int n) {
    return Gatherer.ofSequential(
            () -> new int[]{0},
            (state, element, downstream) -> {
                state[0]++;
                if (state[0] % n != 0) {
                    downstream.push(element);
                }
                return true;
            });
}
```

The skipEvery gatherer removes every nth element while keeping the rest. A  
counter tracks position and elements at multiples of n are skipped. This is  
the inverse of sampleEvery, useful for thinning data while keeping most  
elements.  

## Moving window sum

This example calculates sums over a moving window.  

```java
void main() {

    var data = List.of(1, 2, 3, 4, 5, 6, 7, 8);
    
    var windowSums = data.stream()
            .gather(Gatherers.windowSliding(3))
            .map(window -> window.stream()
                    .mapToInt(Integer::intValue)
                    .sum())
            .toList();
    
    IO.println(windowSums);
}
```

The moving window sum combines sliding windows with summation. Each window  
represents consecutive elements, and we compute the sum for each window. This  
is useful for smoothing data or detecting trends in time series.  

## Conditional accumulation

This example accumulates elements based on dynamic conditions.  

```java
void main() {

    var values = List.of(1, -1, 2, -2, 3, -3, 4);
    
    var accumulated = values.stream()
            .gather(conditionalAccumulate())
            .toList();
    
    IO.println(accumulated);
}

Gatherer<Integer, ?, Integer> conditionalAccumulate() {
    record State(int sum, boolean accumulating) {}
    
    return Gatherer.ofSequential(
            () -> new State(0, true),
            (state, element, downstream) -> {
                var newAccumulating = element >= 0;
                var newSum = newAccumulating ? state.sum + element : 0;
                downstream.push(newSum);
                return new State(newSum, newAccumulating);
            });
}
```

The conditional accumulation gatherer accumulates values only when conditions  
are met, resetting otherwise. This example accumulates positive numbers but  
resets the sum when encountering negatives. This enables complex stateful  
logic.  

## Collect adjacent duplicates

This example groups consecutive duplicate elements.  

```java
void main() {

    var data = List.of("a", "a", "b", "c", "c", "c", "d");
    
    var groups = data.stream()
            .gather(collectAdjacent())
            .toList();
    
    groups.forEach(IO::println);
}

<T> Gatherer<T, ?, List<T>> collectAdjacent() {
    record State<T>(List<T> current, T last) {}
    
    return Gatherer.ofSequential(
            () -> new State<>(new ArrayList<>(), null),
            (state, element, downstream) -> {
                if (state.last != null && !state.last.equals(element)) {
                    downstream.push(new ArrayList<>(state.current));
                    state.current.clear();
                }
                state.current.add(element);
                return new State<>(state.current, element);
            },
            (state, downstream) -> {
                if (!state.current.isEmpty()) {
                    downstream.push(new ArrayList<>(state.current));
                }
            });
}
```

The collectAdjacent gatherer groups consecutive identical elements into lists.  
When an element differs from the previous one, the current group is emitted  
and a new group starts. This is useful for run-length encoding or analyzing  
sequences.  

## Round robin distribution

This example distributes elements across multiple buckets in round-robin  
fashion.  

```java
void main() {

    var items = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9);
    
    var distributed = items.stream()
            .gather(roundRobin(3))
            .findFirst()
            .orElse(null);
    
    IO.println(distributed);
}

<T> Gatherer<T, ?, List<List<T>>> roundRobin(int buckets) {
    return Gatherer.ofSequential(
            () -> {
                var lists = new ArrayList<List<T>>();
                for (int i = 0; i < buckets; i++) {
                    lists.add(new ArrayList<>());
                }
                return new Object() {
                    List<List<T>> bucketList = lists;
                    int index = 0;
                };
            },
            (state, element, downstream) -> {
                state.bucketList.get(state.index).add(element);
                state.index = (state.index + 1) % state.bucketList.size();
                return true;
            },
            (state, downstream) -> {
                downstream.push(state.bucketList);
            });
}
```

The roundRobin gatherer distributes elements across multiple buckets  
cyclically. Each element goes to the next bucket in sequence, wrapping around.  
This is useful for load balancing or partitioning data evenly.  

## Interpose separator

This example inserts a separator between elements.  

```java
void main() {

    var words = List.of("apple", "banana", "cherry");
    
    var withSeparators = words.stream()
            .gather(interpose(", "))
            .toList();
    
    IO.println(String.join("", withSeparators));
}

<T> Gatherer<T, ?, T> interpose(T separator) {
    return Gatherer.ofSequential(
            () -> new boolean[]{true},
            (state, element, downstream) -> {
                if (!state[0]) {
                    downstream.push(separator);
                }
                downstream.push(element);
                state[0] = false;
                return true;
            });
}
```

The interpose gatherer inserts a separator element between each pair of  
elements. The first element flag tracks whether to emit a separator. This is  
useful for creating delimited output or adding visual separators.  

## Take last n elements

This example keeps only the last n elements from the stream.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var lastThree = numbers.stream()
            .gather(takeLast(3))
            .findFirst()
            .orElse(List.of());
    
    IO.println(lastThree);
}

<T> Gatherer<T, ?, List<T>> takeLast(int n) {
    return Gatherer.ofSequential(
            () -> new ArrayDeque<T>(n),
            (deque, element, downstream) -> {
                if (deque.size() >= n) {
                    deque.removeFirst();
                }
                deque.addLast(element);
                return true;
            },
            (deque, downstream) -> {
                downstream.push(new ArrayList<>(deque));
            });
}
```

The takeLast gatherer maintains a fixed-size buffer of the most recent  
elements using a deque. When full, old elements are removed. The finisher  
emits the final buffer contents. This is useful for keeping trailing context.  

## Skip last n elements

This example skips the last n elements from the stream.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var withoutLast = numbers.stream()
            .gather(skipLast(3))
            .toList();
    
    IO.println(withoutLast);
}

<T> Gatherer<T, ?, T> skipLast(int n) {
    return Gatherer.ofSequential(
            () -> new ArrayDeque<T>(n + 1),
            (deque, element, downstream) -> {
                deque.addLast(element);
                if (deque.size() > n) {
                    downstream.push(deque.removeFirst());
                }
                return true;
            });
}
```

The skipLast gatherer uses a buffer to delay emission by n elements. Elements  
are only emitted once there are more than n elements in the buffer. This  
effectively removes the last n elements without needing the full stream in  
memory.  

## Sliding aggregate

This example computes aggregates over sliding windows.  

```java
void main() {

    var temperatures = List.of(20, 22, 21, 23, 25, 24, 26);
    
    var ranges = temperatures.stream()
            .gather(Gatherers.windowSliding(3))
            .map(window -> {
                var min = window.stream().mapToInt(Integer::intValue).min().orElse(0);
                var max = window.stream().mapToInt(Integer::intValue).max().orElse(0);
                return max - min;
            })
            .toList();
    
    IO.println("Temperature ranges: " + ranges);
}
```

The sliding aggregate pattern combines sliding windows with custom aggregate  
functions. This example calculates the range (max - min) for each window.  
This is useful for analyzing local variations or detecting patterns in  
sequential data.  

## Batch with predicate

This example creates batches based on a predicate rather than fixed size.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 10, 11, 12, 20, 21);
    
    var batches = numbers.stream()
            .gather(batchWhile((prev, curr) -> curr - prev <= 5))
            .toList();
    
    batches.forEach(IO::println);
}

<T> Gatherer<T, ?, List<T>> batchWhile(BiPredicate<T, T> continueCondition) {
    record State<T>(List<T> batch, T last) {}
    
    return Gatherer.ofSequential(
            () -> new State<>(new ArrayList<>(), null),
            (state, element, downstream) -> {
                if (state.last != null && !continueCondition.test(state.last, element)) {
                    downstream.push(new ArrayList<>(state.batch));
                    state.batch.clear();
                }
                state.batch.add(element);
                return new State<>(state.batch, element);
            },
            (state, downstream) -> {
                if (!state.batch.isEmpty()) {
                    downstream.push(new ArrayList<>(state.batch));
                }
            });
}
```

The batchWhile gatherer creates variable-size batches based on a condition  
between consecutive elements. When the condition fails, the current batch is  
emitted and a new one starts. This enables context-aware batching.  

## Longest increasing subsequence

This example finds the longest increasing subsequence.  

```java
void main() {

    var numbers = List.of(1, 3, 2, 4, 5, 3, 7, 8);
    
    var longest = numbers.stream()
            .gather(longestIncreasing())
            .findFirst()
            .orElse(List.of());
    
    IO.println(longest);
}

Gatherer<Integer, ?, List<Integer>> longestIncreasing() {
    record State(List<Integer> current, List<Integer> longest) {}
    
    return Gatherer.ofSequential(
            () -> new State(new ArrayList<>(), new ArrayList<>()),
            (state, element, downstream) -> {
                if (state.current.isEmpty() || element > state.current.getLast()) {
                    state.current.add(element);
                } else {
                    if (state.current.size() > state.longest.size()) {
                        state.longest = new ArrayList<>(state.current);
                    }
                    state.current.clear();
                    state.current.add(element);
                }
                return new State(state.current, state.longest);
            },
            (state, downstream) -> {
                var result = state.current.size() > state.longest.size() 
                        ? state.current : state.longest;
                downstream.push(new ArrayList<>(result));
            });
}
```

The longest increasing subsequence gatherer tracks both the current increasing  
sequence and the longest one found so far. When a decrease is detected, it  
compares lengths and potentially updates the longest. This demonstrates  
complex sequential pattern detection.  

## Frequency counter

This example counts element frequencies.  

```java
void main() {

    var letters = List.of("a", "b", "a", "c", "b", "a", "d");
    
    var frequencies = letters.stream()
            .gather(countFrequencies())
            .findFirst()
            .orElse(Map.of());
    
    frequencies.forEach((letter, count) -> 
            IO.println(letter + ": " + count));
}

<T> Gatherer<T, ?, Map<T, Integer>> countFrequencies() {
    return Gatherer.ofSequential(
            HashMap::new,
            (map, element, downstream) -> {
                map.merge(element, 1, Integer::sum);
                return true;
            },
            (map, downstream) -> {
                downstream.push(new HashMap<>(map));
            });
}
```

The frequency counter gatherer builds a map of element occurrences. The  
`merge` method elegantly handles both new keys and updates. This provides  
stream-based frequency analysis without intermediate collection conversions.  

## Running median approximation

This example maintains an approximate running median.  

```java
void main() {

    var values = List.of(3, 1, 4, 1, 5, 9, 2, 6);
    
    var medians = values.stream()
            .gather(runningMedian())
            .toList();
    
    IO.println(medians);
}

Gatherer<Integer, ?, Double> runningMedian() {
    return Gatherer.ofSequential(
            ArrayList::new,
            (list, element, downstream) -> {
                list.add(element);
                var sorted = new ArrayList<>(list);
                sorted.sort(Integer::compareTo);
                int size = sorted.size();
                double median = size % 2 == 0
                        ? (sorted.get(size / 2 - 1) + sorted.get(size / 2)) / 2.0
                        : sorted.get(size / 2);
                downstream.push(median);
                return true;
            });
}
```

The running median gatherer maintains all seen elements and computes the  
median for each step by sorting. While not optimal for large streams, it  
demonstrates stateful statistical calculations. The median is the middle value  
or average of two middle values.  

## Expand with function

This example expands each element into multiple elements.  

```java
void main() {

    var numbers = List.of(1, 2, 3);
    
    var expanded = numbers.stream()
            .gather(expand(n -> List.of(n, n * 10, n * 100)))
            .toList();
    
    IO.println(expanded);
}

<T, R> Gatherer<T, ?, R> expand(Function<T, List<R>> expander) {
    return Gatherer.ofSequential(
            Gatherer.Integrator.ofGreedy((nothing, element, downstream) -> {
                expander.apply(element).forEach(downstream::push);
                return true;
            }));
}
```

The expand gatherer transforms each element into multiple output elements  
using a function that returns a list. All expansion results are emitted  
downstream. This provides flexible one-to-many transformations.  

## Toggle filter

This example alternates between filtering and passing elements.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var toggled = numbers.stream()
            .gather(toggleFilter())
            .toList();
    
    IO.println(toggled);
}

<T> Gatherer<T, ?, T> toggleFilter() {
    return Gatherer.ofSequential(
            () -> new boolean[]{true},
            (state, element, downstream) -> {
                if (state[0]) {
                    downstream.push(element);
                }
                state[0] = !state[0];
                return true;
            });
}
```

The toggle filter gatherer alternates between emitting and skipping elements.  
A boolean flag flips with each element. This creates an alternating pattern  
useful for extracting every other element or creating striped data.  

## Scan with custom binary operator

This example demonstrates scan with a custom accumulation operation.  

```java
void main() {

    var words = List.of("Stream", "Gatherers", "Are", "Powerful");
    
    var accumulated = words.stream()
            .gather(Gatherers.scan(
                    () -> "",
                    (acc, word) -> acc.isEmpty() 
                            ? word 
                            : acc + "-" + word))
            .toList();
    
    accumulated.forEach(IO::println);
}
```

The scan operation with a custom binary operator builds cumulative results. This  
example concatenates words with dashes, showing progressive accumulation. Each  
step shows the accumulated result so far, demonstrating how scan differs from  
reduce.  

## Duplicate n times

This example duplicates each element n times.  

```java
void main() {

    var items = List.of("a", "b", "c");
    
    var duplicated = items.stream()
            .gather(duplicateEach(3))
            .toList();
    
    IO.println(duplicated);
}

<T> Gatherer<T, ?, T> duplicateEach(int times) {
    return Gatherer.ofSequential(
            Gatherer.Integrator.ofGreedy((nothing, element, downstream) -> {
                for (int i = 0; i < times; i++) {
                    downstream.push(element);
                }
                return true;
            }));
}
```

The duplicate gatherer repeats each element a specified number of times. The  
integrator emits the element multiple times before processing the next one.  
This is useful for data expansion or testing.  

## Windowed statistics

This example calculates comprehensive statistics for each window.  

```java
void main() {

    var data = List.of(10, 15, 20, 25, 30, 35);
    
    record Stats(double min, double max, double avg) {}
    
    var stats = data.stream()
            .gather(Gatherers.windowFixed(3))
            .map(window -> {
                var values = window.stream().mapToInt(Integer::intValue);
                return new Stats(
                        values.min().orElse(0),
                        values.max().orElse(0),
                        window.stream().mapToInt(Integer::intValue)
                                .average().orElse(0.0));
            })
            .toList();
    
    stats.forEach(IO::println);
}
```

The windowed statistics pattern applies multiple aggregations to each window.  
This example calculates minimum, maximum, and average for each fixed window.  
This provides comprehensive window-level analysis in a single pass.  

## Conditional window

This example creates windows based on a condition rather than size.  

```java
void main() {

    var values = List.of(1, 2, 3, 10, 11, 12, 20, 21, 22);
    
    var windows = values.stream()
            .gather(conditionalWindow((prev, curr) -> curr - prev < 5))
            .toList();
    
    windows.forEach(IO::println);
}

<T> Gatherer<T, ?, List<T>> conditionalWindow(BiPredicate<T, T> shouldContinue) {
    record State<T>(List<T> window, T last) {}
    
    return Gatherer.ofSequential(
            () -> new State<>(new ArrayList<>(), null),
            (state, element, downstream) -> {
                if (state.last != null && !shouldContinue.test(state.last, element)) {
                    downstream.push(new ArrayList<>(state.window));
                    state.window.clear();
                }
                state.window.add(element);
                return new State<>(state.window, element);
            },
            (state, downstream) -> {
                if (!state.window.isEmpty()) {
                    downstream.push(new ArrayList<>(state.window));
                }
            });
}
```

The conditional window gatherer creates variable-size windows based on a  
predicate between consecutive elements. Windows break when the condition  
fails. This enables semantic grouping based on element relationships rather  
than fixed boundaries.  

## Prefix sum with offset

This example calculates prefix sums with an initial offset.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5);
    var initialSum = 100;
    
    var prefixSums = numbers.stream()
            .gather(prefixSum(initialSum))
            .toList();
    
    IO.println(prefixSums);
}

Gatherer<Integer, ?, Integer> prefixSum(int initial) {
    return Gatherer.ofSequential(
            () -> new int[]{initial},
            (state, element, downstream) -> {
                state[0] += element;
                downstream.push(state[0]);
                return true;
            });
}
```

The prefix sum gatherer calculates cumulative sums starting from an initial  
value. Each element is added to the running total which is then emitted. This  
is useful for offset calculations or maintaining running balances.  

## Split on predicate

This example splits the stream into two based on a predicate.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    record Split<T>(List<T> before, List<T> after) {}
    
    var split = numbers.stream()
            .gather(splitOn(n -> n == 5))
            .findFirst()
            .orElse(null);
    
    IO.println("Before: " + split.before());
    IO.println("After: " + split.after());
}

<T> Gatherer<T, ?, Split<T>> splitOn(Predicate<T> splitter) {
    record State<T>(List<T> before, List<T> after, boolean afterSplit) {}
    
    return Gatherer.ofSequential(
            () -> new State<>(new ArrayList<>(), new ArrayList<>(), false),
            (state, element, downstream) -> {
                if (!state.afterSplit && splitter.test(element)) {
                    return new State<>(state.before, state.after, true);
                }
                if (state.afterSplit) {
                    state.after.add(element);
                } else {
                    state.before.add(element);
                }
                return new State<>(state.before, state.after, state.afterSplit);
            },
            (state, downstream) -> {
                downstream.push(new Split<>(state.before, state.after));
            });
}
```

The splitOn gatherer divides the stream into before and after sections based  
on a splitting predicate. Elements are accumulated into two lists separated by  
the split point. This is useful for partitioning data at a semantic boundary.  

## Accumulate with limit

This example accumulates elements up to a limit.  

```java
void main() {

    var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    var limited = numbers.stream()
            .gather(accumulateUpTo(15))
            .toList();
    
    IO.println(limited);
}

Gatherer<Integer, ?, Integer> accumulateUpTo(int limit) {
    return Gatherer.ofSequential(
            () -> new int[]{0},
            (state, element, downstream) -> {
                if (state[0] + element <= limit) {
                    state[0] += element;
                    downstream.push(element);
                    return true;
                }
                return false;
            });
}
```

The accumulateUpTo gatherer emits elements while keeping a running sum below a  
threshold. Processing stops when adding the next element would exceed the  
limit. This demonstrates conditional short-circuiting based on accumulated  
state.  

## First n unique

This example finds the first n unique elements.  

```java
void main() {

    var numbers = List.of(1, 2, 2, 3, 3, 3, 4, 5, 5, 6, 7, 8);
    
    var firstUnique = numbers.stream()
            .gather(firstNUnique(5))
            .toList();
    
    IO.println(firstUnique);
}

<T> Gatherer<T, ?, T> firstNUnique(int n) {
    record State<T>(Set<T> seen, int count) {}
    
    return Gatherer.ofSequential(
            () -> new State<>(new HashSet<>(), 0),
            (state, element, downstream) -> {
                if (state.count >= n) {
                    return false;
                }
                if (state.seen.add(element)) {
                    downstream.push(element);
                    return new State<>(state.seen, state.count + 1);
                }
                return state;
            });
}
```

The firstNUnique gatherer emits only unique elements and stops after finding n  
unique values. It tracks both seen elements and the count of unique ones  
emitted. This combines deduplication with limiting for efficient unique  
element extraction.  

## Links

- https://github.com/tginsberg/gatherers4j/tree/main
- https://docs.oracle.com/en/java/javase/22/core/stream-gatherers.html#GUID-9A9B143F-8EA8-4A48-88FF-C00E46B9D1C4
- https://www.infoq.com/news/2023/12/stream-api-evolution/
- https://softwaremill.com/stream-gatherers-in-practice-part-1/
- https://download.java.net/java/early_access/jdk23/docs/api/java.base/java/util/stream/Gatherers.html#scan(java.util.function.Supplier,java.util.function.BiFunction)
- https://www.morling.dev/blog/zipping-gatherer/
- https://cr.openjdk.org/~vklang/Gatherers.html
- https://openjdk.org/jeps/461
- https://www.happycoders.eu/java/stream-gatherers/
- https://www.youtube.com/watch?v=epgJm2dZTSg
- https://blog.payara.fish/introducing-stream-gatherers-jep-461-for-enhanced-java-stream-operations

