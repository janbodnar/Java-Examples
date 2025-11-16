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
