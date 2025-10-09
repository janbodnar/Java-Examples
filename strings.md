# Java String Examples

This document contains 60 progressively complex Java examples demonstrating  
various String operations, methods, and patterns using modern Java 25 syntax.  

## Basic string creation
This example shows the most common way to create a string.
```java
void main() {
    var greeting = "Hello, world!";
    IO.println(greeting);
}
```
A string literal, enclosed in double quotes, is used to create a `String` object.
This is the simplest and most direct method for defining a string in Java.

## String length
This example demonstrates how to find the number of characters in a string.
```java
void main() {
    var text = "Java";
    IO.println("Length: " + text.length());
}
```
The `length()` method is called on a `String` object to get its length.
It returns an integer representing the total number of characters in the string.

## String concatenation
This example shows how to combine multiple strings into one.
```java
void main() {
    var first = "Hello";
    var second = "World";
    var result = first + " " + second;
    IO.println(result);
}
```
The `+` operator is used to concatenate strings. In this case, it joins two string
variables and a space literal to form a single, complete sentence.

## String uppercase
This example demonstrates converting a string to all uppercase letters.
```java
void main() {
    var message = "hello world";
    IO.println(message.toUpperCase());
}
```
The `toUpperCase()` method returns a new string where all characters from the
original string have been converted to their uppercase equivalents.

## String lowercase
This example shows how to convert a string to all lowercase letters.
```java
void main() {
    var message = "HELLO WORLD";
    IO.println(message.toLowerCase());
}
```
The `toLowerCase()` method creates a new string with all characters converted
to their lowercase form. This is useful for case-insensitive comparisons.

## String trimming
This example demonstrates removing leading and trailing whitespace from a string.
```java
void main() {
    var text = "   spaces   ";
    IO.println("[" + text.trim() + "]");
}
```
The `trim()` method returns a new string with any whitespace at the beginning or
end of the original string removed. It does not affect whitespace in the middle.

## String equality
This example shows how to compare two strings for exact equality.
```java
void main() {
    var str1 = "apple";
    var str2 = "apple";
    var str3 = "APPLE";
    IO.println(str1.equals(str2));
    IO.println(str1.equals(str3));
}
```
The `equals()` method is used for case-sensitive comparison of string content.
It returns `true` if the strings are identical, and `false` otherwise.

## Case-insensitive comparison
This example demonstrates comparing two strings while ignoring their case.
```java
void main() {
    var str1 = "Apple";
    var str2 = "APPLE";
    IO.println(str1.equalsIgnoreCase(str2));
}
```
The `equalsIgnoreCase()` method compares the content of two strings without regard
to whether the characters are uppercase or lowercase.

## String contains
This example shows how to check if a string contains a specific sequence of characters.
```java
void main() {
    var text = "The quick brown fox";
    IO.println(text.contains("quick"));
    IO.println(text.contains("slow"));
}
```
The `contains()` method returns `true` if the specified substring is found anywhere
within the string, and `false` otherwise.

## String starts with
This example demonstrates checking if a string begins with a certain prefix.
```java
void main() {
    var url = "https://example.com";
    IO.println(url.startsWith("https://"));
    IO.println(url.startsWith("http://"));
}
```
The `startsWith()` method is useful for validating input or identifying the type
of data a string represents based on its beginning.

## String ends with
This example shows how to check if a string ends with a particular suffix.
```java
void main() {
    var filename = "document.pdf";
    IO.println(filename.endsWith(".pdf"));
    IO.println(filename.endsWith(".doc"));
}
```
The `endsWith()` method is often used to check file extensions or other patterns
that are expected at the end of a string.

## Character at index
This example demonstrates retrieving a character at a specific position in a string.
```java
void main() {
    var word = "Java";
    IO.println(word.charAt(0));
    IO.println(word.charAt(2));
}
```
The `charAt()` method returns the character at the given index, where the first
character is at index 0. This is useful for character-level processing.

## Index of substring
This example shows how to find the starting position of a substring.
```java
void main() {
    var text = "Hello World";
    IO.println(text.indexOf("World"));
    IO.println(text.indexOf("Java"));
}
```
The `indexOf()` method returns the index of the first occurrence of the specified
substring. If the substring is not found, it returns -1.

## Last index of
This example demonstrates finding the last occurrence of a substring.
```java
void main() {
    var text = "banana";
    IO.println(text.lastIndexOf("a"));
    IO.println(text.lastIndexOf("n"));
}
```
The `lastIndexOf()` method searches for a substring from the end of the string
and returns the index of its last occurrence.

## Substring extraction
This example shows how to extract a part of a string.
```java
void main() {
    var text = "Hello World";
    IO.println(text.substring(0, 5));
    IO.println(text.substring(6));
}
```
The `substring()` method returns a new string that is a portion of the original.
It can be called with a start and end index, or just a start index to go to the end.

## String replacement
This example demonstrates replacing all occurrences of a substring.
```java
void main() {
    var text = "Hello World";
    IO.println(text.replace("World", "Java"));
    IO.println(text.replace("l", "L"));
}
```
The `replace()` method creates a new string where all instances of a target substring
or character are replaced with a new one.

## Replace first occurrence
This example shows how to replace only the first occurrence of a pattern.
```java
void main() {
    var text = "one two one three";
    IO.println(text.replaceFirst("one", "1"));
}
```
The `replaceFirst()` method is useful when you only want to change the initial match
of a substring or regular expression, leaving subsequent matches untouched.

## Replace all with regex
This example demonstrates replacing all matches of a regular expression.
```java
void main() {
    var text = "apple123banana456cherry";
    IO.println(text.replaceAll("\\d+", " "));
}
```
The `replaceAll()` method uses a regular expression to find all matching parts of the
string and replaces them. Here, `\\d+` matches any sequence of digits.

## String splitting
This example shows how to split a string into an array of substrings.
```java
void main() {
    var csv = "apple,banana,cherry";
    var fruits = csv.split(",");
    for (var fruit : fruits) {
        IO.println(fruit);
    }
}
```
The `split()` method breaks a string apart based on a specified delimiter. It is
very useful for parsing structured data like comma-separated values (CSV).

## String joining
This example demonstrates how to join a collection of strings into a single string.
```java
void main() {
    var fruits = List.of("apple", "banana", "cherry");
    var result = String.join(", ", fruits);
    IO.println(result);
}
```
The `String.join()` static method is a convenient way to concatenate elements from a
collection, inserting a specified delimiter between each element.

## String format
This example shows how to create a formatted string using placeholders.
```java
void main() {
    var name = "Alice";
    var age = 30;
    var message = String.format("Name: %s, Age: %d", name, age);
    IO.println(message);
}
```
The `String.format()` method allows you to create a string from a template with
placeholders (`%s` for string, `%d` for integer) that are filled in by variables.

## String formatted
This example demonstrates the `formatted()` instance method for string formatting.
```java
void main() {
    var product = "Laptop";
    var price = 999.99;
    var text = "%s costs $%.2f".formatted(product, price);
    IO.println(text);
}
```
Introduced in Java 15, the `formatted()` method provides a more concise, instance-level
way to perform the same formatting as `String.format()`.

## String repeat
This example shows how to repeat a string a specified number of times.
```java
void main() {
    var star = "*";
    IO.println(star.repeat(10));
    IO.println("Ha".repeat(3));
}
```
The `repeat()` method, added in Java 11, creates a new string by concatenating the
original string with itself a given number of times.

## String is blank
This example demonstrates checking if a string is empty or contains only whitespace.
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
The `isBlank()` method is useful for validation, as it considers strings with only
whitespace characters (like spaces or tabs) to be "blank".

## String is empty
This example shows how to check if a string has a length of zero.
```java
void main() {
    var empty = "";
    var spaces = "   ";
    IO.println(empty.isEmpty());
    IO.println(spaces.isEmpty());
}
```
The `isEmpty()` method is a simple check for whether a string contains any characters
at all. It returns `false` for a string that contains only whitespace.

## String strip
This example demonstrates removing whitespace with Unicode support.
```java
void main() {
    var text = "  \t Hello \n  ";
    IO.println("[" + text.strip() + "]");
    IO.println("[" + text.stripLeading() + "]");
    IO.println("[" + text.stripTrailing() + "]");
}
```
The `strip()` methods are a modern alternative to `trim()` that are aware of a wider
range of Unicode whitespace characters. You can strip from both ends, or just the
leading or trailing whitespace.

## String lines
This example shows how to split a string into a stream of lines.
```java
void main() {
    var multiline = "Line 1\nLine 2\nLine 3";
    multiline.lines().forEach(IO::println);
}
```
The `lines()` method provides a convenient, functional way to process a multi-line
string. It returns a `Stream<String>`, which can then be used with other stream operations.

## String indent
This example demonstrates adding a specified amount of indentation to a string.
```java
void main() {
    var text = "Hello\nWorld";
    IO.println(text.indent(4));
}
```
The `indent()` method adds a given number of spaces to the beginning of each line
in the string. A negative argument can be used to remove indentation.

## Text blocks
This example introduces text blocks for creating multi-line string literals.
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
Text blocks, enclosed in triple double-quotes, make it much easier to write and read
multi-line strings like JSON, SQL, or HTML. They preserve indentation and newlines,
reducing the need for escape sequences.

## String compareTo
This example shows how to compare two strings lexicographically.
```java
void main() {
    var str1 = "apple";
    var str2 = "banana";
    var str3 = "apple";
    IO.println(str1.compareTo(str2));
    IO.println(str1.compareTo(str3));
}
```
The `compareTo()` method returns a negative integer, zero, or a positive integer if the
string is less than, equal to, or greater than the other string. This is fundamental
for sorting strings.

## String intern
This example demonstrates using the `intern()` method to get a string from the string pool.
```java
void main() {
    var s1 = new String("hello");
    var s2 = "hello";
    var s3 = s1.intern();
    IO.println(s2 == s3);
}
```
The `intern()` method returns the canonical representation of the string from a shared pool.
This allows for reference comparison (`==`) of interned strings, which can be faster than
`equals()`, though its use is generally discouraged in modern code.

## String to char array
This example shows how to convert a string into an array of characters.
```java
void main() {
    var word = "Java";
    var chars = word.toCharArray();
    for (var ch : chars) {
        IO.println(ch);
    }
}
```
The `toCharArray()` method is useful when you need to perform operations on the individual
characters of a string, such as iterating through them or modifying them in an array.

## String from char array
This example demonstrates creating a new string from an array of characters.
```java
void main() {
    var chars = new char[]{'J', 'a', 'v', 'a'};
    var word = new String(chars);
    IO.println(word);
}
```
The `String` class provides a constructor that accepts a `char` array, which is a common
way to build a string after manipulating its individual characters.

## String codePoints
This example shows how to iterate over the Unicode code points of a string.
```java
void main() {
    var emoji = "Hello 👋";
    emoji.codePoints().forEach(cp -> 
        IO.println(Integer.toHexString(cp))
    );
}
```
The `codePoints()` method returns a stream of integer code points, which correctly handles
Unicode characters that are represented by more than one `char`, like many emojis.

## String matches regex
This example demonstrates testing if a string matches a regular expression.
```java
void main() {
    var email = "user@example.com";
    var pattern = "^[\\w.]+@[\\w.]+\\.[a-z]{2,}$";
    IO.println(email.matches(pattern));
}
```
The `matches()` method is a simple way to validate a string against a regex pattern. It
returns `true` only if the entire string matches the pattern.

## StringBuilder basics
This example introduces `StringBuilder` for efficient, mutable string construction.
```java
void main() {
    var sb = new StringBuilder();
    sb.append("Hello");
    sb.append(" ");
    sb.append("World");
    IO.println(sb.toString());
}
```
When you need to build a string through many concatenations, `StringBuilder` is much more
performant than using the `+` operator. It modifies an internal buffer instead of creating
a new `String` object for each operation.

## StringBuilder insert
This example shows how to insert text into a `StringBuilder` at a specific position.
```java
void main() {
    var sb = new StringBuilder("Hello World");
    sb.insert(6, "Beautiful ");
    IO.println(sb.toString());
}
```
The `insert()` method allows you to add characters at any point within the `StringBuilder`,
shifting the existing characters to make room.

## StringBuilder delete
This example demonstrates deleting a range of characters from a `StringBuilder`.
```java
void main() {
    var sb = new StringBuilder("Hello Beautiful World");
    sb.delete(6, 16);
    IO.println(sb.toString());
}
```
The `delete()` method removes the characters in a specified range. This is another example
of the powerful in-place modifications that `StringBuilder` allows.

## StringBuilder reverse
This example shows how to reverse the contents of a `StringBuilder`.
```java
void main() {
    var sb = new StringBuilder("Hello");
    sb.reverse();
    IO.println(sb.toString());
}
```
The `reverse()` method provides a simple way to reverse the entire sequence of characters
in the `StringBuilder`, which can be useful for certain algorithms.

## StringBuffer thread-safe
This example introduces `StringBuffer`, a thread-safe alternative to `StringBuilder`.
```java
void main() {
    var buffer = new StringBuffer();
    buffer.append("Thread");
    buffer.append("-");
    buffer.append("Safe");
    IO.println(buffer.toString());
}
```
`StringBuffer` has the same API as `StringBuilder`, but its methods are synchronized. This
makes it safe to use in multi-threaded environments, though it comes with a performance cost.

## String valueOf
This example demonstrates converting various data types into their string representations.
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
The static `String.valueOf()` method is a versatile tool for converting primitives and
objects into strings. It handles `null` gracefully, returning the string "null" instead
of throwing an exception.

## String concat method
This example shows the `concat()` method as an alternative to the `+` operator.
```java
void main() {
    var str1 = "Hello";
    var str2 = " World";
    var result = str1.concat(str2);
    IO.println(result);
}
```
The `concat()` method appends one string to another, returning a new `String` object.
While functionally similar to `+`, the operator is generally preferred for its readability
and ability to handle non-string types.

## String regionMatches
This example demonstrates comparing specific regions of two strings.
```java
void main() {
    var str1 = "Hello World";
    var str2 = "world";
    IO.println(str1.regionMatches(true, 6, str2, 0, 5));
}
```
The `regionMatches()` method is a powerful tool for checking if a substring from one string
matches a substring from another. It allows for specifying offsets and an optional
case-insensitive flag.

## String getBytes
This example shows how to convert a string into a byte array.
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
The `getBytes()` method encodes the string into a sequence of bytes using the platform's
default character set. This is fundamental for file I/O and network communication.

## String with encoding
This example demonstrates encoding and decoding a string with a specific character set.
```java
void main() {
    var text = "Hello 世界";
    var utf8Bytes = text.getBytes(java.nio.charset.StandardCharsets.UTF_8);
    var restored = new String(utf8Bytes, 
        java.nio.charset.StandardCharsets.UTF_8);
    IO.println(restored);
}
```
To ensure consistency across different systems, it is best practice to specify an encoding
like UTF-8 when converting strings to and from bytes. This avoids issues with international
characters.

## Pattern and Matcher
This example uses the `Pattern` and `Matcher` classes for advanced regex operations.
```java
void main() {
    var pattern = java.util.regex.Pattern.compile("\\d+");
    var matcher = pattern.matcher("abc123def456");
    while (matcher.find()) {
        IO.println(matcher.group());
    }
}
```
For complex or repeated regex operations, compiling a `Pattern` object is more efficient.
The `Matcher` object can then be used to find multiple matches or access capture groups
within the target string.

## String split with limit
This example shows how to limit the number of splits performed on a string.
```java
void main() {
    var text = "a:b:c:d:e";
    var parts = text.split(":", 3);
    for (var part : parts) {
        IO.println(part);
    }
}
```
The `split()` method can take a limit parameter. When a positive limit is provided, the
split is applied at most `limit - 1` times, and the last element of the array contains
the rest of the unsplit string.

## String contentEquals
This example demonstrates comparing a `String` with another `CharSequence`.
```java
void main() {
    var str = "Hello";
    var sb = new StringBuilder("Hello");
    IO.println(str.contentEquals(sb));
}
```
The `contentEquals()` method is useful for comparing the content of a `String` with any
`CharSequence`, like a `StringBuilder` or `StringBuffer`, without first converting it to a `String`.

## String transform
This example shows the `transform()` method for applying a function to a string.
```java
void main() {
    var result = "hello"
        .transform(String::toUpperCase)
        .transform(s -> s + "!");
    IO.println(result);
}
```
Introduced in Java 12, `transform()` provides a concise way to apply a function to a string,
making it easy to chain multiple transformations in a fluent, readable style.

## String with streams
This example demonstrates integrating string operations with the Stream API.
```java
void main() {
    var words = List.of("apple", "banana", "cherry");
    var upper = words.stream()
        .map(String::toUpperCase)
        .toList();
    IO.println(upper);
}
```
The Stream API allows for powerful, functional-style processing of collections. Here,
`map()` is used to apply the `toUpperCase()` method to every string in a list.

## String filtering
This example shows how to filter a collection of strings using a stream.
```java
void main() {
    var words = List.of("apple", "apricot", "banana", "avocado");
    words.stream()
        .filter(w -> w.startsWith("a"))
        .forEach(IO::println);
}
```
The `filter()` operation creates a new stream containing only the elements that match a
given predicate. This is a declarative and readable way to select data from a collection.

## String collectors joining
This example demonstrates using a `Collector` to join strings from a stream.
```java
void main() {
    var words = List.of("Java", "is", "awesome");
    var sentence = words.stream()
        .collect(java.util.stream.Collectors.joining(" "));
    IO.println(sentence);
}
```
`Collectors.joining()` is a powerful terminal operation that concatenates the elements of a
stream into a single string, with an optional delimiter, prefix, and suffix.

## String partition
This example shows how to split a string using multiple delimiters.
```java
void main() {
    var text = "apple,banana;cherry,date;elderberry";
    var result = text.split("[,;]");
    IO.println(String.join(" | ", result));
}
```
The `split()` method accepts a regular expression, so you can use a character class `[]`
to specify multiple possible delimiters. This is a flexible way to parse data from various formats.

## String template literals
This example demonstrates a basic way to create template-like strings.
```java
void main() {
    var name = "Alice";
    var age = 30;
    var message = "Name: " + name + ", Age: " + age;
    IO.println(message);
}
```
While Java doesn't have native template literals like some other languages, string
concatenation or formatting methods are commonly used to achieve the same result of
embedding variables within a string.

## String case conversion
This example showcases the basic case conversion methods.
```java
void main() {
    var text = "hElLo WoRlD";
    IO.println(text.toLowerCase());
    IO.println(text.toUpperCase());
}
```
These methods are essential for standardizing string input for case-insensitive
comparisons or for formatting text for display.

## String null handling
This example shows a safe way to handle a potentially `null` string.
```java
void main() {
    String nullStr = null;
    var safe = String.valueOf(nullStr);
    IO.println("Result: " + safe);
}
```
Unlike calling a method on a `null` reference, which would throw an exception,
`String.valueOf()` safely handles `null` by returning the string "null".

## String character replacement
This example demonstrates replacing individual characters in a string.
```java
void main() {
    var text = "Hello World";
    var result = text.replace('o', '0').replace('l', '1');
    IO.println(result);
}
```
The `replace()` method can be used with `char` arguments to swap single characters.
Multiple replacements can be chained together to perform a series of substitutions.

## Advanced pattern matching
This example uses a complex regex to extract multiple types of data from a string.
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
This demonstrates the power of the `Pattern` and `Matcher` classes for finding and
extracting information that matches several different formats within a single pass.

## String formatting with locale
This example shows how to format strings based on a specific locale.
```java
void main() {
    var price = 1234.56;
    var us = String.format(java.util.Locale.US, "$%.2f", price);
    var de = String.format(java.util.Locale.GERMANY, "%.2f€", price);
    IO.println(us);
    IO.println(de);
}
```
Providing a `Locale` to `String.format()` ensures that numbers, dates, and currency
are formatted according to the conventions of a specific region, which is crucial for
internationalization.

## String Unicode normalization
This example demonstrates Unicode normalization for consistent string comparison.
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
Some Unicode characters can be represented in multiple ways. `Normalizer.normalize()`
converts a string to a standard canonical form, which is essential for ensuring that
semantically identical strings are also considered equal.