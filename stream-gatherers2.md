# Stream gatherers


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

## Running max

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


## Scan 

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

Alternative using `reduce`.

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


## Pairwise

```java
vimport java.util.stream.Collectors;
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



## Window

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

### Sliding pairs

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

## Stateful validation

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

## TakeWhile/fold/window

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
    //     .gather(Gatherers.windowFixed(3))
    //     .limit(100)
    //     .collect(Collectors.toList());

    // System.out.println(res);    


    var res11 = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10).stream()
        .gather(Gatherers.windowFixed(2))
        .gather(Gatherers.fold(() -> 0, (total, next) -> total + next.get(0) * next.get(1)))
        .findFirst().orElse(0);


    System.out.println(res11);


    List<String> words = List.of("the", "be", "two", "of", "and", "a", "war", "in", "that");
    // var res2 = words.stream()                  
    //     .gather(Gatherers.windowFixed(3))  
    //     .toList(); 

    // System.out.println(res2);
,
    var res3 = words.stream()
        .gather(takeWhile(e -> !e.startsWith("w")))
        .toList();

    System.out.println(res3);
}

// Predicate<String> p = e -> !e.startsWith("w");

<T> Gatherer<T, ?, T> takeWhile(Predicate<? super T> predicate) {
    return Gatherer.ofSequential(
        (nothing, e, downstream) ->
            predicate.test(e) && downstream.push(e)
    );
}



// <T> Gatherer<T, ?, T> takeWhile(Predicate<? super T> predicate) {
//     return Gatherer.ofSequential(
//         () -> null,
//         (nothing, e, downstream) ->
//             predicate.test(e) && downstream.push(e),
//         // (l, r) -> l,
//         // (l, r) -> l,
//         (nothing, downstream) -> {}
//     );
// }

















// @FunctionalInterface
// public interface Integrator<A, T, R> {
//   boolean integrate(A state, T element, Downstream<? super R> downstream);
// }

// @FunctionalInterface
// public interface Downstream<T> {
//   boolean push(T element);
// }

// public <T, R> Gatherer<T, Void, R> mapping(Function<T, R> mapper) {
//   return Gatherer.of(
//       Integrator.ofGreedy(
//           (state, element, downstream) -> {
//             R mappedElement = mapper.apply(element);
//             return downstream.push(mappedElement);
//           }));
// }

// public List<Integer> toLengths(List<String> words) {
//   return words.stream()
//       .gather(mapping(String::length))
//       .toList();
// }

```

## Mapfilter

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

## Distinct ignore case

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

## Filter evens

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

## Filter & transform

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

## Custom mapping

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

## Running sum

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

---

```java
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

## limit

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



## Batch processing

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




## Deduplicate

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

---

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

## Ratelimit

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

---

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


## Mapmulti

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

---


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

---

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


