# Code 


## Reading lines

Reading lines from a file via pipe. 

```java
void main() {

  try (var scanner = new Scanner(System.in)) {

    while (scanner.hasNextLine()) {
      String input = scanner.nextLine();

      String word = Optional.of(input).map(String::trim)
          .filter(s -> !s.isBlank()).orElse("-empty line-");
          
      IO.println(word);
    }

  }
}
```

 `java ListJar.java < words.txt`


## CompletableFuture

```java

void main() {

  var res = CompletableFuture
      .supplyAsync((Supplier<String>) this::getText) // casting not needed, just for clarity
      .thenApply((Function<String, List<String>>) this::cutToWords)
      .join();

  res.forEach(IO::println);

}

List<String> cutToWords(String text) {
  return List.of(text.split(" "));
}

String getText() {

  try {
    Thread.sleep(Duration.ofMillis(1500));
  } catch (InterruptedException e) {
    e.printStackTrace();
  }

  return "an old falton in the rain";
}
```

## Comparing empty list

```java
void main() {

    List<Integer> vals1 = List.of(); // returns a shared immutable empty list
    List<Integer> vals2 = List.of();

    IO.println(vals1 == vals2);

    IO.println(System.identityHashCode(vals1));
    IO.println(System.identityHashCode(vals2));

    List<Integer> vals3 = Collections.emptyList();
    List<Integer> vals4 = Collections.emptyList();

    IO.println(vals3 == vals4); // true, shared instance

    IO.println(System.identityHashCode(vals3));
    IO.println(System.identityHashCode(vals4));
}
```
