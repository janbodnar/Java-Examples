<h1>Java Stream</h1>


<p>
This article explores how Java Streams enable efficient data processing. You
will learn how to create streams from various sources and apply essential
operations to improve performance and readability in Java programs.
</p>


<h2>Java stream definition</h2>

<p>
<dfn>Stream</dfn> is a sequence of elements from a source that supports
sequential and parallel aggregate operations. Common aggregate operations
include filter, map, reduce, find, match, and sort. The source can be a
collection, IO operation, or array, which provides data to the stream.
</p>

<p>
A Java collection is an in-memory data structure containing all elements, while
a stream computes elements on demand. Unlike collections, which require explicit
(external) iteration, streams handle iteration internally. Since Java 8,
collections have a <code>stream</code> method that returns a stream from the
collection.
</p>

<p>
The <code>Stream</code> interface is defined in the
<code>java.util.stream</code> package.
</p>

<p>
Stream operations produce results without modifying their source.
</p>


<h2>Characteristics of a stream</h2>

<ul>
<li>Streams do not store data; they provide data from a source such as a
collection, array, or IO channel.</li>
<li>Streams do not modify the data source. They transform data into a new
stream, for example, when filtering.</li>
<li>Many stream operations are lazily evaluated, allowing for automatic
optimizations and short-circuiting.</li>
<li>Streams can be infinite. Methods such as <code>limit</code> allow you to
retrieve results from infinite streams.</li>
<li>Stream elements can be accessed only once during the stream's lifetime. Like
an <code>Iterator</code>, you must generate a new stream to revisit the same
elements.</li>
<li>Streams provide methods such as <code>forEach</code> and
<code>forEachOrdered</code> for internal iteration.</li>
<li>Streams support SQL-like and common functional operations, such as filter,
map, reduce, find, match, and sorted.</li>
</ul>


<h2>Stream pipeline</h2>

<p>
A stream pipeline consists of a source, intermediate operations, and a terminal
operation. Intermediate operations return a new, modified stream, allowing you
to chain multiple operations. Terminal operations return a value or void. After
a terminal operation, the stream cannot be used further. Short-circuiting a
terminal operation means the stream may terminate before processing all values,
which is useful for infinite streams.
</p>

<p>
Intermediate operations are lazy; they are not invoked until a terminal
operation is executed. This improves performance when processing large data
streams.
</p>


<h2>Creating streams</h2>

<p>
Streams can be created from collections, arrays, strings, IO resources, or
generators.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    List&lt;String&gt; words = List.of("pen", "coin", "desk", "chair");

    String word = words.stream().findFirst().get();
    System.out.println(word);

    Stream&lt;String&gt; letters = Arrays.stream(new String[]{"a", "b", "c"});
    System.out.printf("There are %d letters%n", letters.count());

    String day = "Sunday";
    IntStream istr = day.codePoints();

    String s = istr.filter(e -&gt; e != 'n').collect(StringBuilder::new,
            StringBuilder::appendCodePoint, StringBuilder::append).toString();
    System.out.println(s);
}
</pre>

<p>
This example demonstrates working with streams created from a list, an array,
and a string.
</p>

<pre class="explanation">
List&lt;String&gt; words = List.of("pen", "coin", "desk", "chair");
</pre>

<p>
A list of strings is created.
</p>

<pre class="explanation">
String word = words.stream().findFirst().get();
</pre>

<p>
We use the <code>stream</code> method to create a stream from a list. The
<code>findFirst</code> method returns the first element as an
<code>Optional</code>, from which we retrieve the value using <code>get</code>.
</p>

<pre class="explanation">
Stream&lt;String&gt; letters = Arrays.stream(new String[]{ "a", "b", "c"});
System.out.printf("There are %d letters%n", letters.count());
</pre>

<p>
We create a stream from an array. The <code>count</code> method returns the
number of elements in the stream.
</p>

<pre class="explanation">
String day = "Sunday";
IntStream istr = day.codePoints();

String s = istr.filter(e -&gt; e != 'n').collect(StringBuilder::new,
        StringBuilder::appendCodePoint, StringBuilder::append).toString();
System.out.println(s);
</pre>

<p>
Here, we create a stream from a string, filter its characters, and build a new
string from the filtered characters.
</p>

<pre class="compact">
$ java Main.java
pen
There are 3 letters
Suday
</pre>

<p>
There are three <code>Stream</code> specializations: <code>IntStream</code>,
<code>DoubleStream</code>, and <code>LongStream</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream integers = IntStream.rangeClosed(1, 16);
    var res = integers.average();

    if (res.isPresent()) {
        System.out.println(res.getAsDouble());
    }

    DoubleStream doubles = DoubleStream.of(2.3, 33.1, 45.3);
    doubles.forEachOrdered(System.out::println);

    LongStream longs = LongStream.range(6, 25);
    System.out.println(longs.count());
}
</pre>

<p>
This example demonstrates the use of the three stream specializations.
</p>

<pre class="explanation">
IntStream integers = IntStream.rangeClosed(1, 16);
System.out.println(integers.average().getAsDouble());
</pre>

<p>
A stream of integers is created with the <code>IntStream.rangeClosed</code> method.
</p>

<pre class="explanation">
if (res.isPresent()) {
    System.out.println(res.getAsDouble());
}
</pre>

<p>
If the value is present, we print the average to the console.
</p>

<pre class="explanation">
DoubleStream doubles = DoubleStream.of(2.3, 33.1, 45.3);
doubles.forEachOrdered(System.out::println);
</pre>

<p>
A stream of double values is created with the <code>DoubleStream.of</code>
method. The <code>forEachOrdered</code> method prints the elements in order.
</p>

<pre class="explanation">
LongStream longs = LongStream.range(6, 25);
System.out.println(longs.count());
</pre>

<p>
A stream of long integers is created with the <code>LongStream.range</code>
method. We print the count of elements using the <code>count</code> method.
</p>

<pre class="compact">
$ java Main.java
8.5
2.3
33.1
45.3
19
</pre>


<p>
The <code>Stream.of</code> method creates a sequential, ordered stream
containing the specified values.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    Stream&lt;String&gt; colours = Stream.of("red", "green", "blue");
    Optional&lt;String&gt; col = colours.skip(2).findFirst();

    col.ifPresent(System.out::println);

    Stream&lt;Integer&gt; nums = Stream.of(3, 4, 5, 6, 7);
    Optional&lt;Integer&gt; maxVal = nums.max(Comparator.naturalOrder());

    maxVal.ifPresent(System.out::println);
}
</pre>

<p>
This example shows how to use <code>Stream.of</code> to create two different
streams.
</p>

<pre class="explanation">
Stream&lt;String&gt; colours = Stream.of("red", "green", "blue");
</pre>

<p>
A stream of three strings is created.
</p>

<pre class="explanation">
Optional&lt;String&gt; col = colours.skip(2).findFirst();
</pre>

<p>
Using the <code>skip</code> method, we skip two elements and find the next one
with <code>findFirst</code>. The <code>findFirst</code> method returns an
<code>Optional&lt;String&gt;</code>.
</p>

<pre class="explanation">
col.ifPresent(System.out::println);
</pre>

<p>
We print the value if it is present.
</p>

<pre class="explanation">
Stream&lt;Integer&gt; nums = Stream.of(3, 4, 5, 6, 7);
Optional&lt;Integer&gt; maxVal = nums.max(Comparator.naturalOrder());

maxVal.ifPresent(System.out::println);
</pre>

<p>
We create a stream of integers and find its maximum value.
</p>

<pre class="compact">
$ java Main.java
blue
7
</pre>

<p>
Other ways to create streams include <code>Stream.iterate</code> and
<code>Stream.generate</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    Stream&lt;Integer&gt; s1 = Stream.iterate(5, n -&gt; n * 2).limit(10);
    s1.forEach(System.out::println);

    Stream.generate(new Random()::nextDouble)
            .map(e -&gt; (e * 10))
            .limit(5)
            .forEach(System.out::println);
}
</pre>

<p>
This example creates two streams using <code>Stream.iterate</code> and
<code>Stream.generate</code>.
</p>

<pre class="explanation">
Stream&lt;Integer&gt; s1 = Stream.iterate(5, n -&gt; n * 2).limit(10);
s1.forEach(System.out::println);
</pre>

<p>
The <code>Stream.iterate</code> method returns an infinite, sequential, ordered
stream produced by iterative application of a function to an initial element
(the seed). Each subsequent element is generated by applying the function to the
previous element.
</p>

<pre class="explanation">
Stream.generate(new Random()::nextDouble)
        .map(e -&gt; (e * 10))
        .limit(5)
        .forEach(System.out::println);
</pre>

<p>
A stream of five random doubles is created with <code>Stream.generate</code>.
Each element is multiplied by ten, and the results are printed to the console.
</p>

<pre class="compact">
$ java Main.java
5
10
20
40
80
160
320
640
1280
2560
8.704675577530493
5.732011478196306
3.8978402578067515
3.6986033299500933
6.0976417139147205
</pre>


<p>
You can also create a stream from a file.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() throws IOException {

    Path path = Paths.get("/home/janbodnar/myfile.txt");

    try (Stream&lt;String&gt; stream = Files.lines(path)) {

        stream.forEach(System.out::println);
    }
}
</pre>

<p>
This example reads a file and prints its contents using streams.
</p>

<pre class="explanation">
Path path = Paths.get("/home/janbodnar/myfile.txt");
</pre>

<p>
A <code>Path</code> object is created with <code>Paths.get</code>. A
<code>Path</code> object locates a file in the file system.
</p>

<pre class="explanation">
try (Stream&lt;String&gt; stream = Files.lines(path)) {
    ...
}
</pre>

<p>
From the path, we create a stream using <code>Files.lines</code>; each element
of the stream is a line from the file.
</p>

<pre class="explanation">
stream.forEach(System.out::println);
</pre>

<p>
We iterate through the stream and print each line to the console.
</p>


<h2>Internal and external iteration</h2>

<p>
Depending on who controls the iteration process, we distinguish between
<em>external</em> and <em>internal</em> iteration. External iteration, also
known as explicit iteration, is handled by the programmer and was the only type
available before Java 8. For external iteration, we use for and while loops.
Internal iteration, also called implicit iteration, is controlled by the
iterator itself and is available in Java streams.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    var words = List.of("pen", "coin", "desk", "eye", "bottle");

    Iterator&lt;String&gt; it = words.iterator();

    while (it.hasNext()) {

        System.out.println(it.next());
    }
}
</pre>

<p>
In this code example, we retrieve an iterator from a list of strings. Using the
iterator's <code>hasNext</code> and <code>next</code> methods in a while loop,
we iterate over the list elements.
</p>

<p>
In the following example, we iterate over the same list using internal
iteration.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    var words = List.of("pen", "coin", "desk", "eye", "bottle");
    words.stream().forEach(System.out::println);
}
</pre>

<p>
Here, we create a stream from a list and use the stream's <code>forEach</code>
method to iterate over its elements internally.
</p>

<pre class="explanation">
words.stream().forEach(System.out::println);
</pre>

<p>
This can be shortened to <code>words.forEach(System.out::println);</code>.
</p>


<h2>Stream filtering</h2>

<p>
Filtering data is one of the most important features of streams. The
<code>filter</code> method is an intermediate operation that returns a stream
containing only elements that match the given predicate. A predicate is a method
that returns a boolean value.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.rangeClosed(0, 25);
    int[] vals = nums.filter(e -&gt; e &gt; 15).toArray();

    System.out.println(Arrays.toString(vals));
}
</pre>

<p>
This code example creates a stream of integers and filters it to contain only
values greater than fifteen.
</p>

<pre class="explanation">
IntStream nums = IntStream.rangeClosed(0, 25);
</pre>

<p>
With <code>IntStream</code>, a stream of twenty-six integers is created. The
<code>rangeClosed</code> method creates a stream of integers from a start to an
end value, both inclusive.
</p>

<pre class="explanation">
int[] vals = nums.filter(e -&gt; e &gt; 15).toArray();
</pre>

<p>
We pass a lambda expression (<code>e -&gt; e &gt; 15</code>) to the
<code>filter</code> function; it returns true for values greater than 15. The
<code>toArray</code> method is a terminal operation that transforms the stream
into an array of integers.
</p>

<pre class="explanation">
System.out.println(Arrays.toString(vals));
</pre>

<p>
The array is printed to the console.
</p>

<pre class="compact">
$ java Main.java
[16, 17, 18, 19, 20, 21, 22, 23, 24, 25]
</pre>

<p>
The next example produces a list of even numbers.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.rangeClosed(0, 30);
    nums.filter(this::isEven).forEach(System.out::println);
}

boolean isEven(int e) {

    return e % 2 == 0;
}
</pre>

<p>
To get even numbers from a stream, we pass an <code>isEven</code> method
reference to the <code>filter</code> method.
</p>

<pre class="explanation">
nums.filter(this::isEven).forEach(System.out::println);
</pre>

<p>
The double colon (::) operator is used to pass a method reference. The
<code>forEach</code> method is a terminal operation that iterates over the
stream elements and takes a method reference to <code>System.out.println</code>.
</p>



<h2>Skipping and limiting elements</h2>

<p>
The <code>skip(n)</code> method skips the first n elements of the stream, and
the <code>limit(m)</code> method limits the number of elements in the stream to
m.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream s = IntStream.range(0, 15);
    s.skip(3).limit(5).forEach(System.out::println);
}
</pre>

<p>
This example creates a stream of fifteen integers, skips the first three
elements with <code>skip</code>, and limits the number of elements to five with
<code>limit</code>.
</p>

<pre class="compact">
$ java Main.java
3
4
5
6
7
</pre>


<h2>Sorting elements</h2>

<p>
The <code>sorted</code> method sorts the elements of the stream according to the
provided <code>Comparator</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.of(4, 3, 2, 1, 8, 6, 7, 5);
    int[] sorted = nums.sorted().toArray();

    System.out.println("Sorted: " + Arrays.toString(sorted));
}
</pre>

<p>
This example sorts integer elements in descending order. The <code>boxed</code>
method converts an <code>IntStream</code> to a
<code>Stream&lt;Integer&gt;</code>.
</p>

<pre class="compact">
$ java Main.java
8
7
6
5
4
3
2
1
</pre>


<p>
The next example shows how to sort a stream of objects.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
record Car(String name, int price) {
}

void main() {

    List&lt;Car&gt; cars = List.of(new Car("Citroen", 23000),
            new Car("Porsche", 65000), new Car("Skoda", 18000),
            new Car("Volkswagen", 33000), new Car("Volvo", 47000));

    cars.stream().sorted(Comparator.comparing(Car::price))
            .forEach(System.out::println);
}
</pre>

<p>
The example sorts cars by their price.
</p>

<pre class="explanation">
List&lt;Car&gt; cars = List.of(new Car("Citroen", 23000),
    new Car("Porsche", 65000), new Car("Skoda", 18000),
    new Car("Volkswagen", 33000), new Car("Volvo", 47000));
</pre>

<p>
A list of cars is created.
</p>

<pre class="explanation">
cars.stream().sorted(Comparator.comparing(Car::price))
    .forEach(System.out::println);
</pre>

<p>
A stream is generated from the list using the <code>stream</code> method. We
pass a reference to the <code>price</code> method of <code>Car</code>, which is
used for comparison.
</p>

<pre class="compact">
$ java Main.java
Car{name=Skoda, price=18000}
Car{name=Citroen, price=23000}
Car{name=Volkswagen, price=33000}
Car{name=Volvo, price=47000}
Car{name=Porsche, price=65000}
</pre>


<h2>Unique values</h2>

<p>
The <code>distinct</code> method returns a stream consisting of unique elements.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.of(1, 1, 3, 4, 4, 6, 7, 7);
    int[] a = nums.distinct().toArray();

    System.out.println(Arrays.toString(a));
}
</pre>

<p>
This example removes duplicate values from a stream of integers.
</p>

<pre class="explanation">
IntStream nums = IntStream.of(1, 1, 3, 4, 4, 6, 7, 7);
</pre>

<p>
There are three duplicate values in the stream.
</p>

<pre class="explanation">
int[] a = nums.distinct().toArray();
</pre>

<p>
We remove the duplicates with the <code>distinct</code> method.
</p>

<pre class="compact">
$ java Main.java
[1, 3, 4, 6, 7]
</pre>


<h2>Mapping operations</h2>

<p>
It is possible to transform elements into a new stream; the original source is
not modified. The <code>map</code> method returns a stream consisting of the
results of applying a given function to the elements of a stream.
<code>map</code> is an intermediate operation.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    int[] squares = nums.map(e -&gt; e * e).toArray();

    System.out.println(Arrays.toString(squares));
}
</pre>

<p>
We map a transformation function onto each element of the stream.
</p>

<pre class="explanation">
int[] squares = nums.map(e -&gt; e * e).toArray();
</pre>

<p>
We apply a lambda expression (<code>e -&gt; e * e</code>) to the stream: each
element is squared. A new stream is created and transformed into an array with
the <code>toArray</code> method.
</p>

<pre class="compact">
$ java Main.java
[1, 4, 9, 16, 25, 36, 49, 64]
</pre>


<p>
In the next example, we transform a stream of strings.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    Stream&lt;String&gt; words = Stream.of("cardinal", "pen", "coin", "globe");
    words.map(this::capitalize).forEach(System.out::println);
}

String capitalize(String word) {

    word = word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
    return word;
}
</pre>

<p>
We have a stream of strings and capitalize each string in the stream.
</p>

<pre class="explanation">
words.map(this::capitalize).forEach(System.out::println);
</pre>

<p>
We pass a reference to the <code>capitalize</code> method to the
<code>map</code> method.
</p>

<pre class="compact">
$ java Main.java
Cardinal
Pen
Coin
Globe
</pre>


<h2>Stream reductions</h2>

<p>
A <dfn>reduction</dfn> is a terminal operation that aggregates a stream into a
single value or primitive.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    OptionalInt maxValue = nums.max();

    if (maxValue.isPresent()) {
        System.out.printf("The maximum value is: %d%n", maxValue.getAsInt());
    }
}
</pre>

<p>
This example demonstrates a reduction operation that finds the maximum value in
a stream of integers.
</p>

<pre class="explanation">
OptionalInt maxValue = nums.max();
</pre>

<p>
With the <code>max</code> method, we get the maximum element of the stream. The
method returns an <code>OptionalInt</code>, from which we retrieve the integer
using <code>getAsInt</code>.
</p>

<pre class="explanation">
if (maxValue.isPresent()) {
    System.out.printf("The maximum value is: %d%n", maxValue.getAsInt());
}
</pre>

<p>
We print the value if it is present.
</p>

<pre class="compact">
$ java Main.java
The maximum value is: 8
</pre>


<p>
A custom reduction can be created with the <code>reduce</code> method.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    IntStream nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    OptionalInt product = nums.reduce((a, b) -&gt; a * b);
    
    if (product.isPresent()) {
        System.out.printf("The product is: %d%n", product.getAsInt());

    }
}
</pre>

<p>
This example returns the product of the integer elements in the stream.
</p>

<pre class="compact">
$ java Main.java
The product is: 40320
</pre>


<h2>Collection operations</h2>

<p>
A <dfn>collection</dfn> is a terminal reduction operation that reduces elements
of a stream into a Java collection, string, value, or specific grouping.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
record Car(String name, int price) {
}

void main() {

    List&lt;Car&gt; cars = List.of(new Car("Citroen", 23000),
            new Car("Porsche", 65000), new Car("Skoda", 18000),
            new Car("Volkswagen", 33000), new Car("Volvo", 47000));

    List&lt;String&gt; names = cars.stream().map(Car::name)
            .filter(name -&gt; name.startsWith("Vo"))
            .collect(Collectors.toList());

    for (String name : names) {
        
        System.out.println(name);
    }
}
</pre>

<p>
This example creates a stream from a list of car objects, filters the cars by
their name, and returns a list of matching car names.
</p>

<pre class="explanation">
List&lt;String&gt; names = cars.stream().map(Car::name)
    .filter(name -&gt; name.startsWith("Vo"))
    .collect(Collectors.toList());
</pre>

<p>
At the end of the pipeline, we use the <code>collect</code> method to transform
the stream into a list.
</p>

<pre class="compact">
$ java Main.java
Volkswagen
Volvo
</pre>

<p>
In the next example, we use the <code>collect</code> method to group data.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    List&lt;String&gt; items = List.of("pen", "book", "pen", "coin",
            "book", "desk", "book", "pen", "book", "coin");

    Map&lt;String, Long&gt; result = items.stream().collect(
            Collectors.groupingBy(
                    Function.identity(), Collectors.counting()
            ));

    for (Map.Entry&lt;String, Long&gt; entry : result.entrySet()) {

        String key = entry.getKey();
        Long value = entry.getValue();

        System.out.format("%s: %d%n", key, value);
    }
}
</pre>

<p>
This code example groups elements by their occurrence in a stream.
</p>

<pre class="explanation">
Map&lt;String, Long&gt; result = items.stream().collect(
        Collectors.groupingBy(
                Function.identity(), Collectors.counting()
        ));
</pre>

<p>
With the <code>Collectors.groupingBy</code> method, we count the occurrences of
elements in the stream. The operation returns a map.
</p>

<pre class="explanation">
for (Map.Entry&lt;String, Long&gt; entry : result.entrySet()) {

    String key = entry.getKey();
    Long value = entry.getValue();

    System.out.format("%s: %d%n", key, value);
}
</pre>

<p>
We iterate through the map and print its key/value pairs.
</p>



<!--
TODO Optional, create stream from pattern, builder, suppliers
statistics, finding, matching, infinite streams
short-circuit https://goo.gl/uwDalH
-->





</html>

