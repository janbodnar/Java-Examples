# Java Optional Examples

`Optional` is a container object that may or may not contain a value, designed  
to eliminate null pointer exceptions and make code more robust. It provides  
methods to check value presence with `isPresent`, retrieve values with `get`,  
and perform operations only when a value exists. The type was inspired by  
similar constructs in Haskell and Scala. Other languages like C# and Groovy  
use null-safe operators (e.g., `.?`) for similar purposes.  

## Empty Optional

This example demonstrates creating an empty Optional container.  

```java
void main() {

    Optional<String> empty = Optional.empty();
    IO.println("Is empty: " + empty.isEmpty());
}
```

The `Optional.empty` method creates an empty Optional container. It is used  
instead of null references to represent the absence of a value. Using empty  
Optionals prevents NullPointerException errors and makes code more explicit  
about handling missing values.  

## Optional with value

This example shows creating an Optional with a guaranteed non-null value.  

```java
void main() {

    Optional<String> word = Optional.of("falcon");
    IO.println("Value: " + word.get());
}
```

The `Optional.of` method is used when we are certain that the parameter will  
not be null. If a null value is passed to `Optional.of`, it throws a  
NullPointerException. This method is ideal for scenarios where null values  
are not expected.  

## Optional ofNullable

This example demonstrates creating an Optional that may or may not contain a  
null value.  

```java
void main() {

    String value = null;
    Optional<String> word = Optional.ofNullable(value);
    IO.println("Is present: " + word.isPresent());
}
```

The `Optional.ofNullable` method is used when we don't know if the value will  
be null. If the parameter is null, it returns an empty Optional; otherwise, it  
returns an Optional containing the value. This is the safest way to create  
Optionals from potentially null sources.  

## Optional ifPresent

This example demonstrates processing values only when they are present.  

```java
void main() {

    var words = List.of("rock", null, "mountain", null, "falcon", "sky");

    for (var word : words) {
        Optional.ofNullable(word).ifPresent(IO::println);
    }
}
```

The `ifPresent` method executes the given action only if a value is present in  
the Optional. We wrap potentially null list elements with  
`Optional.ofNullable` to safely handle null values. If the Optional is empty,  
the action is simply skipped without throwing any exceptions.  

## Optional isPresent and get

This example demonstrates checking for value presence before retrieval.  

```java
void main() {

    if (getNullMessage().isPresent()) {
        IO.println(getNullMessage().get());
    } else {
        IO.println("n/a");
    }

    if (getEmptyMessage().isPresent()) {
        IO.println(getEmptyMessage().get());
    } else {
        IO.println("n/a");
    }

    if (getCustomMessage().isPresent()) {
        IO.println(getCustomMessage().get());
    } else {
        IO.println("n/a");
    }
}

Optional<String> getNullMessage() {
    return Optional.ofNullable(null);
}

Optional<String> getEmptyMessage() {
    return Optional.empty();
}

Optional<String> getCustomMessage() {
    return Optional.of("Hello there!");
}
```

The `isPresent` method checks if the Optional contains a value. If true, we  
retrieve the value with `get`. Otherwise, we provide an alternative action or  
message. This pattern is safe but verbose; the `orElse` method provides a more  
concise alternative.  

## Optional isEmpty

This example demonstrates checking if an Optional is empty.  

```java
void main() {

    var words = List.of("rock", null, "mountain", null, "falcon", "sky");

    for (var word : words) {
        var optional = Optional.ofNullable(word);
        
        if (optional.isEmpty()) {
            IO.println("n/a");
        } else {
            IO.println(optional.get());
        }
    }
}
```

The `isEmpty` method returns true if the Optional does not contain a value.  
This is the opposite of `isPresent` and can make code more readable when you  
need to handle the absence of a value explicitly. It was added in Java 11 as a  
more intuitive alternative to `!isPresent()`.  

## Optional orElse

This example shows providing a default value when an Optional is empty.  

```java
void main() {

    IO.println(getNullMessage().orElse("n/a"));
    IO.println(getEmptyMessage().orElse("n/a"));
    IO.println(getCustomMessage().orElse("n/a"));
}

Optional<String> getNullMessage() {
    return Optional.ofNullable(null);
}

Optional<String> getEmptyMessage() {
    return Optional.empty();
}

Optional<String> getCustomMessage() {
    return Optional.of("Hello there!");
}
```

The `orElse` method provides a concise way to return a default value when the  
Optional is empty. If the Optional contains a value, that value is returned;  
otherwise, the specified default value is returned. This simplifies code  
compared to the `isPresent` and `get` pattern.  

## Optional flatMap

This example demonstrates applying a function that returns an Optional.  

```java
void main() {

    var upperCase = (String s) -> Optional.of(s.toUpperCase());
    
    var words = List.of("rock", null, "mountain", null, "falcon", "sky");

    for (var word : words) {
        var result = Optional.ofNullable(word).flatMap(upperCase);
        result.ifPresent(IO::println);
    }
}
```

The `flatMap` method applies a mapping function that returns an Optional. If  
the original Optional is empty, it returns an empty Optional without invoking  
the function. If the result is already an Optional, `flatMap` doesn't wrap it  
in another Optional, preventing nested Optional structures.  

## Optional with JSoup

This example demonstrates using Optional with the JSoup HTML parsing library.  

```java
import org.jsoup.Jsoup;

void main() {

    var htmlString = """
            <html>
            <head>
            <title>My title</title>
            </head>
            <body>
            <main></main>
            </body>
            </html>
            """;

    var doc = Jsoup.parse(htmlString);
    var mainEl = Optional.ofNullable(doc.select("main").first());

    mainEl.ifPresent(e -> {
        e.append("<p>hello there!</p>");
        e.prepend("<h1>Heading</h1>");
    });

    IO.println(doc);
}
```

We parse an HTML string and search for the `main` tag using JSoup. The `first`  
method may return null if the element doesn't exist, so we use  
`Optional.ofNullable` to safely wrap the result. The `ifPresent` method  
ensures we only modify the document when the element is found.  

## Optional with JDBI

This example demonstrates using Optional with database queries using JDBI.  

```java
import org.jdbi.v3.core.Jdbi;

void main() {

    var jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    var user = "postgres";
    var password = "s$cret";

    var jdbi = Jdbi.create(jdbcUrl, user, password);
    var id = 3;

    var query = "SELECT name FROM cars WHERE id = ?";
    var result = jdbi.withHandle(handle -> 
        handle.select(query, id)
            .mapTo(String.class)
            .findOne()
    );

    result.ifPresentOrElse(IO::println, () -> IO.println("N/A"));
}
```

The JDBI `findOne` method returns an Optional containing the only row in the  
result set, if any. It returns `Optional.empty()` if zero rows are returned or  
if the row itself is null. The `ifPresentOrElse` method provides both success  
and failure handlers in a single call.  

## Optional orElseGet

This example shows providing a computed default value using a supplier.  

```java
void main() {

    var value = Optional.<String>empty();
    var result = value.orElseGet(() -> "Default value: " + Math.random());
    IO.println(result);
}
```

The `orElseGet` method accepts a Supplier function that is only invoked when  
the Optional is empty. This is more efficient than `orElse` when the default  
value is expensive to compute, as the computation only happens when needed.  

## Optional orElseThrow

This example demonstrates throwing an exception when a value is absent.  

```java
void main() {

    var value = Optional.<String>empty();
    
    try {
        var result = value.orElseThrow(() -> 
            new IllegalStateException("Value not found"));
        IO.println(result);
    } catch (IllegalStateException e) {
        IO.println("Error: " + e.getMessage());
    }
}
```

The `orElseThrow` method throws an exception if the Optional is empty. You can  
provide a custom exception supplier to create meaningful error messages. This  
is useful when the absence of a value represents an error condition that  
should halt normal program flow.  

## Optional filter

This example shows filtering Optional values based on a predicate.  

```java
void main() {

    var words = List.of("rock", "mountain", "falcon", "sky");

    for (var word : words) {
        Optional.of(word)
            .filter(w -> w.length() > 4)
            .ifPresent(IO::println);
    }
}
```

The `filter` method returns the Optional if it contains a value that matches  
the predicate, otherwise it returns an empty Optional. This allows for  
conditional processing of Optional values without explicitly checking the  
condition outside the Optional chain.  

## Optional map

This example demonstrates transforming Optional values with a mapping  
function.  

```java
void main() {

    var words = List.of("rock", "mountain", "falcon", "sky");

    for (var word : words) {
        var length = Optional.of(word)
            .map(String::length)
            .orElse(0);
        IO.println(word + " -> " + length);
    }
}
```

The `map` method applies a transformation function to the value if present,  
wrapping the result in an Optional. If the original Optional is empty, it  
returns an empty Optional without invoking the function. Unlike `flatMap`, the  
result is automatically wrapped in an Optional.  

## Optional ifPresentOrElse

This example shows executing different actions based on value presence.  

```java
void main() {

    var present = Optional.of("Hello");
    var absent = Optional.<String>empty();

    present.ifPresentOrElse(
        value -> IO.println("Found: " + value),
        () -> IO.println("Not found")
    );

    absent.ifPresentOrElse(
        value -> IO.println("Found: " + value),
        () -> IO.println("Not found")
    );
}
```

The `ifPresentOrElse` method takes two parameters: a Consumer for when the  
value is present and a Runnable for when it's absent. This provides a cleaner  
alternative to using separate `ifPresent` and `isEmpty` checks, handling both  
cases in a single method call.  

## Optional or

This example demonstrates providing an alternative Optional when empty.  

```java
void main() {

    var primary = Optional.<String>empty();
    var secondary = Optional.of("Secondary value");

    var result = primary.or(() -> secondary);
    IO.println(result.orElse("n/a"));
}
```

The `or` method returns the Optional if it contains a value, otherwise it  
returns the Optional produced by the supplier. This allows chaining multiple  
Optional sources, useful for implementing fallback logic when values might  
come from different sources.  

## Optional stream

This example shows converting an Optional to a Stream.  

```java
void main() {

    var values = List.of(
        Optional.of("apple"),
        Optional.<String>empty(),
        Optional.of("banana"),
        Optional.<String>empty(),
        Optional.of("cherry")
    );

    values.stream()
        .flatMap(Optional::stream)
        .forEach(IO::println);
}
```

The `stream` method, added in Java 9, converts an Optional to a Stream  
containing either zero or one element. This is particularly useful when  
working with collections of Optionals, as `flatMap(Optional::stream)`  
elegantly filters out empty values while extracting present values.  

## Optional with records

This example demonstrates using Optional with record types.  

```java
record Person(String name, Optional<String> email) {}

void main() {

    var people = List.of(
        new Person("John", Optional.of("john@example.com")),
        new Person("Jane", Optional.empty()),
        new Person("Bob", Optional.of("bob@example.com"))
    );

    for (var person : people) {
        var email = person.email().orElse("no email");
        IO.println(person.name() + ": " + email);
    }
}
```

Records work seamlessly with Optional fields to represent data that may or may  
not be present. This pattern is cleaner than using null and makes the  
optionality explicit in the type signature. The record constructor  
automatically handles the Optional parameter.  

## Optional equals and hashCode

This example shows how Optional implements equality and hashing.  

```java
void main() {

    var opt1 = Optional.of("test");
    var opt2 = Optional.of("test");
    var opt3 = Optional.of("other");
    var opt4 = Optional.<String>empty();
    var opt5 = Optional.<String>empty();

    IO.println("opt1 equals opt2: " + opt1.equals(opt2));
    IO.println("opt1 equals opt3: " + opt1.equals(opt3));
    IO.println("opt4 equals opt5: " + opt4.equals(opt5));
    IO.println("opt1 hashCode: " + opt1.hashCode());
    IO.println("opt4 hashCode: " + opt4.hashCode());
}
```

Optional properly implements `equals` and `hashCode`, making it safe to use in  
collections like Sets and as Map keys. Two Optionals are equal if both are  
empty or both contain equal values. All empty Optionals are equal to each  
other regardless of their type parameter.  

## Optional toString

This example demonstrates Optional's string representation.  

```java
void main() {

    var present = Optional.of("Hello World");
    var absent = Optional.empty();

    IO.println("Present: " + present);
    IO.println("Absent: " + absent);
}
```

The `toString` method provides a clear representation of the Optional's state.  
For present values, it shows `Optional[value]`, making the value visible. For  
empty Optionals, it shows `Optional.empty`, clearly indicating the absence of  
a value. This is helpful for debugging and logging.  


