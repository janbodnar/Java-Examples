# Java String Examples

This document contains 60 progressively complex Java examples demonstrating  
various String operations, methods, and patterns using modern Java 25 syntax.  

## Basic string creation

```java
void main() {
    var greeting = "Hello, world!";
    IO.println(greeting);
}
```

Creates a simple string literal and prints it to the console.  

## String length

```java
void main() {
    var text = "Java";
    IO.println("Length: " + text.length());
}
```

The `length` method returns the number of characters in a string.  

## String concatenation

```java
void main() {
    var first = "Hello";
    var second = "World";
    var result = first + " " + second;
    IO.println(result);
}
```

Combines multiple strings using the concatenation operator `+`.  

## String uppercase

```java
void main() {
    var message = "hello world";
    IO.println(message.toUpperCase());
}
```

Converts all characters in a string to uppercase using `toUpperCase`.  

## String lowercase

```java
void main() {
    var message = "HELLO WORLD";
    IO.println(message.toLowerCase());
}
```

Converts all characters in a string to lowercase using `toLowerCase`.  

## String trimming

```java
void main() {
    var text = "   spaces   ";
    IO.println("[" + text.trim() + "]");
}
```

Removes leading and trailing whitespace from a string using `trim`.  

## String equality

```java
void main() {
    var str1 = "apple";
    var str2 = "apple";
    var str3 = "APPLE";
    IO.println(str1.equals(str2));
    IO.println(str1.equals(str3));
}
```

Compares strings for exact equality using the `equals` method.  

## Case-insensitive comparison

```java
void main() {
    var str1 = "Apple";
    var str2 = "APPLE";
    IO.println(str1.equalsIgnoreCase(str2));
}
```

Compares strings ignoring case differences using `equalsIgnoreCase`.  

## String contains

```java
void main() {
    var text = "The quick brown fox";
    IO.println(text.contains("quick"));
    IO.println(text.contains("slow"));
}
```

Checks if a string contains a specific substring using `contains`.  

## String starts with

```java
void main() {
    var url = "https://example.com";
    IO.println(url.startsWith("https://"));
    IO.println(url.startsWith("http://"));
}
```

Determines if a string begins with a specified prefix using `startsWith`.  

## String ends with

```java
void main() {
    var filename = "document.pdf";
    IO.println(filename.endsWith(".pdf"));
    IO.println(filename.endsWith(".doc"));
}
```

Checks if a string ends with a specified suffix using `endsWith`.  

## Character at index

```java
void main() {
    var word = "Java";
    IO.println(word.charAt(0));
    IO.println(word.charAt(2));
}
```

Retrieves the character at a specific index position using `charAt`.  

## Index of substring

```java
void main() {
    var text = "Hello World";
    IO.println(text.indexOf("World"));
    IO.println(text.indexOf("Java"));
}
```

Finds the first occurrence index of a substring using `indexOf`.  

## Last index of

```java
void main() {
    var text = "banana";
    IO.println(text.lastIndexOf("a"));
    IO.println(text.lastIndexOf("n"));
}
```

Finds the last occurrence index of a substring using `lastIndexOf`.  

## Substring extraction

```java
void main() {
    var text = "Hello World";
    IO.println(text.substring(0, 5));
    IO.println(text.substring(6));
}
```

Extracts a portion of a string using `substring` with start and end indices.  

## String replacement

```java
void main() {
    var text = "Hello World";
    IO.println(text.replace("World", "Java"));
    IO.println(text.replace("l", "L"));
}
```

Replaces all occurrences of a substring with another using `replace`.  

## Replace first occurrence

```java
void main() {
    var text = "one two one three";
    IO.println(text.replaceFirst("one", "1"));
}
```

Replaces only the first occurrence of a pattern using `replaceFirst`.  

## Replace all with regex

```java
void main() {
    var text = "apple123banana456cherry";
    IO.println(text.replaceAll("\\d+", " "));
}
```

Replaces all matches of a regular expression pattern using `replaceAll`.  

## String splitting

```java
void main() {
    var csv = "apple,banana,cherry";
    var fruits = csv.split(",");
    for (var fruit : fruits) {
        IO.println(fruit);
    }
}
```

Splits a string into an array based on a delimiter using `split`.  

## String joining

```java
void main() {
    var fruits = List.of("apple", "banana", "cherry");
    var result = String.join(", ", fruits);
    IO.println(result);
}
```

Joins multiple strings with a delimiter using the static `join` method.  

## String format

```java
void main() {
    var name = "Alice";
    var age = 30;
    var message = String.format("Name: %s, Age: %d", name, age);
    IO.println(message);
}
```

Formats strings with placeholders using `String.format` method.  

## String formatted

```java
void main() {
    var product = "Laptop";
    var price = 999.99;
    var text = "%s costs $%.2f".formatted(product, price);
    IO.println(text);
}
```

Instance method `formatted` provides concise string formatting in Java 15+.  

## String repeat

```java
void main() {
    var star = "*";
    IO.println(star.repeat(10));
    IO.println("Ha".repeat(3));
}
```

Repeats a string multiple times using the `repeat` method from Java 11.  

## String is blank

```java
void main() {
    var empty = "";
    var spaces = "   ";
    var text = "Hello";
    IO.println(empty.isBlank());
    IO.println(spaces.isBlank());
    IO.println(text.isBlank());
}
```

Checks if a string is empty or contains only whitespace using `isBlank`.  

## String is empty

```java
void main() {
    var empty = "";
    var spaces = "   ";
    IO.println(empty.isEmpty());
    IO.println(spaces.isEmpty());
}
```

Checks if a string has zero length using the `isEmpty` method.  

## String strip

```java
void main() {
    var text = "  \t Hello \n  ";
    IO.println("[" + text.strip() + "]");
    IO.println("[" + text.stripLeading() + "]");
    IO.println("[" + text.stripTrailing() + "]");
}
```

Removes whitespace including Unicode spaces using `strip` methods.  

## String lines

```java
void main() {
    var multiline = "Line 1\nLine 2\nLine 3";
    multiline.lines().forEach(IO::println);
}
```

Splits a string into a stream of lines using the `lines` method.  

## String indent

```java
void main() {
    var text = "Hello\nWorld";
    IO.println(text.indent(4));
}
```

Adds indentation to each line of a string using the `indent` method.  

## Text blocks

```java
void main() {
    var json = """
        {
            "name": "Alice",
            "age": 30
        }
        """;
    IO.println(json);
}
```

Text blocks provide multi-line string literals with preserved formatting.  

## String compareTo

```java
void main() {
    var str1 = "apple";
    var str2 = "banana";
    var str3 = "apple";
    IO.println(str1.compareTo(str2));
    IO.println(str1.compareTo(str3));
}
```

Compares strings lexicographically using `compareTo` method.  

## String intern

```java
void main() {
    var s1 = new String("hello");
    var s2 = "hello";
    var s3 = s1.intern();
    IO.println(s2 == s3);
}
```

The `intern` method returns canonical string from the string pool.  

## String to char array

```java
void main() {
    var word = "Java";
    var chars = word.toCharArray();
    for (var ch : chars) {
        IO.println(ch);
    }
}
```

Converts a string to a character array using `toCharArray` method.  

## String from char array

```java
void main() {
    var chars = new char[]{'J', 'a', 'v', 'a'};
    var word = new String(chars);
    IO.println(word);
}
```

Creates a string from a character array using String constructor.  

## String codePoints

```java
void main() {
    var emoji = "Hello 👋";
    emoji.codePoints().forEach(cp -> 
        IO.println(Integer.toHexString(cp))
    );
}
```

Iterates over Unicode code points in a string using `codePoints`.  

## String matches regex

```java
void main() {
    var email = "user@example.com";
    var pattern = "^[\\w.]+@[\\w.]+\\.[a-z]{2,}$";
    IO.println(email.matches(pattern));
}
```

Tests if a string matches a regular expression using `matches`.  

## StringBuilder basics

```java
void main() {
    var sb = new StringBuilder();
    sb.append("Hello");
    sb.append(" ");
    sb.append("World");
    IO.println(sb.toString());
}
```

StringBuilder provides mutable string construction for better performance.  

## StringBuilder insert

```java
void main() {
    var sb = new StringBuilder("Hello World");
    sb.insert(6, "Beautiful ");
    IO.println(sb.toString());
}
```

Inserts text at a specific position using StringBuilder's `insert` method.  

## StringBuilder delete

```java
void main() {
    var sb = new StringBuilder("Hello Beautiful World");
    sb.delete(6, 16);
    IO.println(sb.toString());
}
```

Removes a range of characters using StringBuilder's `delete` method.  

## StringBuilder reverse

```java
void main() {
    var sb = new StringBuilder("Hello");
    sb.reverse();
    IO.println(sb.toString());
}
```

Reverses the character sequence using StringBuilder's `reverse` method.  

## StringBuffer thread-safe

```java
void main() {
    var buffer = new StringBuffer();
    buffer.append("Thread");
    buffer.append("-");
    buffer.append("Safe");
    IO.println(buffer.toString());
}
```

StringBuffer is synchronized for thread-safe string operations.  

## String valueOf

```java
void main() {
    var num = 42;
    var bool = true;
    var arr = new int[]{1, 2, 3};
    IO.println(String.valueOf(num));
    IO.println(String.valueOf(bool));
    IO.println(String.valueOf(arr));
}
```

Converts various types to their string representation using `valueOf`.  

## String concat method

```java
void main() {
    var str1 = "Hello";
    var str2 = " World";
    var result = str1.concat(str2);
    IO.println(result);
}
```

Concatenates strings using the `concat` method as an alternative to `+`.  

## String regionMatches

```java
void main() {
    var str1 = "Hello World";
    var str2 = "world";
    IO.println(str1.regionMatches(true, 6, str2, 0, 5));
}
```

Compares regions of two strings with optional case-insensitive matching.  

## String getBytes

```java
void main() {
    var text = "Hello";
    var bytes = text.getBytes();
    IO.println("Byte count: " + bytes.length);
    for (var b : bytes) {
        IO.println(b);
    }
}
```

Converts a string to a byte array using default character encoding.  

## String with encoding

```java
void main() {
    var text = "Hello 世界";
    var utf8Bytes = text.getBytes(java.nio.charset.StandardCharsets.UTF_8);
    var restored = new String(utf8Bytes, 
        java.nio.charset.StandardCharsets.UTF_8);
    IO.println(restored);
}
```

Encodes and decodes strings with specific character encoding like UTF-8.  

## Pattern and Matcher

```java
void main() {
    var pattern = java.util.regex.Pattern.compile("\\d+");
    var matcher = pattern.matcher("abc123def456");
    while (matcher.find()) {
        IO.println(matcher.group());
    }
}
```

Uses Pattern and Matcher for advanced regex operations and extraction.  

## String split with limit

```java
void main() {
    var text = "a:b:c:d:e";
    var parts = text.split(":", 3);
    for (var part : parts) {
        IO.println(part);
    }
}
```

Limits the number of splits using the limit parameter in `split`.  

## String contentEquals

```java
void main() {
    var str = "Hello";
    var sb = new StringBuilder("Hello");
    IO.println(str.contentEquals(sb));
}
```

Compares string content with any CharSequence using `contentEquals`.  

## String transform

```java
void main() {
    var result = "hello"
        .transform(String::toUpperCase)
        .transform(s -> s + "!");
    IO.println(result);
}
```

Applies transformations using the `transform` method introduced in Java 12.  

## String with streams

```java
void main() {
    var words = List.of("apple", "banana", "cherry");
    var upper = words.stream()
        .map(String::toUpperCase)
        .toList();
    IO.println(upper);
}
```

Integrates strings with streams for functional-style transformations.  

## String filtering

```java
void main() {
    var words = List.of("apple", "apricot", "banana", "avocado");
    words.stream()
        .filter(w -> w.startsWith("a"))
        .forEach(IO::println);
}
```

Filters strings based on conditions using stream operations.  

## String collectors joining

```java
void main() {
    var words = List.of("Java", "is", "awesome");
    var sentence = words.stream()
        .collect(java.util.stream.Collectors.joining(" "));
    IO.println(sentence);
}
```

Joins stream elements into a string using Collectors.joining method.  

## String partition

```java
void main() {
    var text = "apple,banana;cherry,date;elderberry";
    var result = text.split("[,;]");
    IO.println(String.join(" | ", result));
}
```

Splits strings using multiple delimiters with character class regex.  

## String template literals

```java
void main() {
    var name = "Alice";
    var age = 30;
    var message = "Name: " + name + ", Age: " + age;
    IO.println(message);
}
```

Demonstrates string composition with variables for template-like behavior.  

## String case conversion

```java
void main() {
    var text = "hElLo WoRlD";
    IO.println(text.toLowerCase());
    IO.println(text.toUpperCase());
}
```

Shows case conversion methods for mixed-case strings.  

## String null handling

```java
void main() {
    String nullStr = null;
    var safe = String.valueOf(nullStr);
    IO.println("Result: " + safe);
}
```

Safely converts null to string "null" using `String.valueOf` method.  

## String character replacement

```java
void main() {
    var text = "Hello World";
    var result = text.replace('o', '0').replace('l', '1');
    IO.println(result);
}
```

Replaces individual characters using the `replace` method with chars.  

## Advanced pattern matching

```java
void main() {
    var text = "Phone: 123-456-7890, Email: user@example.com";
    var pattern = java.util.regex.Pattern.compile(
        "(\\d{3}-\\d{3}-\\d{4})|(\\w+@\\w+\\.\\w+)"
    );
    var matcher = pattern.matcher(text);
    while (matcher.find()) {
        IO.println("Found: " + matcher.group());
    }
}
```

Extracts multiple patterns from text using grouped regular expressions.  

## String formatting with locale

```java
void main() {
    var price = 1234.56;
    var us = String.format(java.util.Locale.US, "$%.2f", price);
    var de = String.format(java.util.Locale.GERMANY, "%.2f€", price);
    IO.println(us);
    IO.println(de);
}
```

Formats numbers with locale-specific formatting using String.format.  

## String Unicode normalization

```java
void main() {
    var str1 = "café";
    var str2 = "café";
    IO.println(str1.equals(str2));
    var norm1 = java.text.Normalizer.normalize(str1, 
        java.text.Normalizer.Form.NFC);
    var norm2 = java.text.Normalizer.normalize(str2, 
        java.text.Normalizer.Form.NFC);
    IO.println(norm1.equals(norm2));
}
```

Normalizes Unicode strings for consistent comparison and processing.  
