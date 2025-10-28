# Stream gatherers


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

## MapMutli

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

