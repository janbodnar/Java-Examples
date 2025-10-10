<h1>Java Optional</h1>

<p>
In this article we work with Optional type in Java.
</p>

<p>
<dfn>Optional</dfn> is a container object which may or may not contain a value.
We can check if a value is present with <code>isPresent</code> and then retrive
it with <code>get</code>. If the container does not contain a value it is then
called empty.
</p>

<p>
The goal of the <code>Optional</code> type is to avoid null references and all
the problems that are caused by them.
</p>

<p>
The <code>Optional</code> was inspired by similar types found in Haskell and
Scala. Other languages, such as C# or Groovy, use null-safe operators
<code>.?</code> for the same purpose.
</p>

<pre class="compact">
Optional&lt;String&gt; empty = Optional.empty();
</pre>

<p>
We create an empty <code>Optional</code> with <code>Optional.empty</code>.
It is used insted of null references.
</p>

<pre class="compact">
Optional&lt;String&gt; word = Optional.of("falcon");
</pre>

<p>
<code>Optional.of</code> is used when we are certain that the parameter will not 
be null.
</p>

<pre class="compact">
Optional&lt;String&gt; word = Optional.ofNullable(value);
</pre>

<p>
<code>Optional.ofNullable</code> is used when we don't know if there will be 
null.
</p>

<h2>Simple example</h2>

<p>
In the following example, we have a simple example with <code>Optional</code>
type.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;
import java.util.Optional;

void main() {

    var words = Arrays.asList("rock", null, "mountain",
            null, "falcon", "sky");

    for (int i = 0; i &lt; 5; i++) {

        Optional&lt;String&gt; word = Optional.ofNullable(words.get(i));
        word.ifPresent(System.out::println);
    }
}
</pre>

<p>
We have a list of words; the list also contains null values. We go through the
list and print the elements.
</p>

<pre class="explanation">
Optional&lt;String&gt; word = Optional.ofNullable(words.get(i));
</pre>

<p>
We know that we can get a null value from the list; therefore, we wrap the
element into <code>Optional</code> with <code>Optional.ofNullable</code>.
</p>

<pre class="explanation">
word.ifPresent(System.out::println);
</pre>

<p>
We check if there is some value in the <code>Optional</code> with
<code>ifPresent</code>. If case there is one, we print it.
</p>

<p>
In the following example, we have three methods that return an
<code>Optional</code> type.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Optional;

void main() {

    if (getNullMessage().isPresent()) {
        System.out.println(getNullMessage().get());
    } else {
        System.out.println("n/a");
    }

    if (getEmptyMessage().isPresent()) {
        System.out.println(getEmptyMessage().get());
    } else {
        System.out.println("n/a");
    }

    if (getCustomMessage().isPresent()) {
        System.out.println(getCustomMessage().get());
    } else {
        System.out.println("n/a");
    }
}

Optional&lt;String&gt; getNullMessage() {
    return Optional.ofNullable(null);
}

Optional&lt;String&gt; getEmptyMessage() {
    return Optional.empty();
}

Optional&lt;String&gt; getCustomMessage() {
    return Optional.of("Hello there!");
}
</pre>

<p>
The three methods return a null message, an empty message and a real message.
</p>

<pre class="explanation">
if (getNullMessage().isPresent()) {
    System.out.println(getNullMessage().get());
} else {
    System.out.println("n/a");
}
</pre>

<p>
First, we check if the value returned by the method contains a value with
<code>isPresent</code>. If true, we get the value with <code>get</code>.
Otherwise we print "n/a" message.
</p>


<h2>Optional ifEmpty</h2>

<p>
The <code>ifEmpty</code> returns true, if the value is not present. 
</p> 

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;
import java.util.Optional;

void main() {

    var words = Arrays.asList("rock", null, "mountain",
            null, "falcon", "sky");

    for (int i = 0; i &lt; 5; i++) {

        Optional&lt;String&gt; word = Optional.ofNullable(words.get(i));

        if (word.isEmpty()) {

            System.out.println("n/a");
        }

        word.ifPresent(System.out::println);
    }
}
</pre>

<p>
In the example, we print all valid values with <code>ifPresent</code>. All empty 
values are recognized via <code>isEmpty</code>.
</p>


<h2>Optional orElse</h2>

<p>
The <code>orElse</code> method allows us to quickly return a value if it is not
present.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Optional;

void main() {

    System.out.println(getNullMessage().orElse("n/a"));
    System.out.println(getEmptyMessage().orElse("n/a"));
    System.out.println(getCustomMessage().orElse("n/a"));
}

Optional&lt;String&gt; getNullMessage() {
    return Optional.ofNullable(null);
}

Optional&lt;String&gt; getEmptyMessage() {
    return Optional.empty();
}

Optional&lt;String&gt; getCustomMessage() {
    return Optional.of("Hello there!");
}
</pre>

<p>
We managed to shorten the example a bit with <code>orElse</code> method.
</p>

<p>
In this article we covered the <code>Optional</code> type in Java.
</p>


<h2>Optional flatMap</h2>

<p>
The <code>flatMap</code> method applies the provided  mapping function to a
value if it is present. It returns that result or otherwise an empty
<code>Optional</code>. If the result is already an <code>Optional</code>,
<code>flatMap</code> does not wrap it within an additional
<code>Optional</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;
import java.util.Optional;
import java.util.function.Function;

void main() {

    Function&lt;String, Optional&lt;String&gt;&gt; upperCase = s -&gt; Optional.of(s.toUpperCase());

    var words = Arrays.asList("rock", null, "mountain",
            null, "falcon", "sky");

    for (int i = 0; i &lt; 5; i++) {

        Optional&lt;String&gt; word = Optional.ofNullable(words.get(i));

        var res = word.flatMap(upperCase);
        res.ifPresent(System.out::println);
    }
}
</pre>


<h2>JSoup example</h2>

<p>
In the following example, we use JSoup library to parse and modify an HTML
document. 
</p>

<p>
For the project, we need the <code>jsoup</code> artifact. 
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import org.jsoup.Jsoup;
import org.jsoup.nodes.Element;

import java.util.Optional;


void main() {

    String htmlString = """
            &lt;html&gt;
            &lt;head&gt;
            &lt;title&gt;My title&lt;/title&gt;
            &lt;/head&gt;
            &lt;body&gt;
            &lt;main&gt;&lt;/main&gt;
            &lt;/body&gt;
            &lt;/html&gt;
            """;

    var doc = Jsoup.parse(htmlString);
    Optional&lt;Element&gt; mainEl = Optional.ofNullable(doc.select("main").first());

    mainEl.ifPresent(e -&gt; {
        e.append("&lt;p&gt;hello there!&lt;/p&gt;");
        e.prepend("&lt;h1&gt;Heading&lt;/h1&gt;");
    });

    System.out.println(doc);
}
</pre>

<p>
We parse an HTML string and look for the <code>main</code> tag. If it is
present, we append <code>p</code> and <code>h1</code> tags to the document.
</p>

<pre class="explanation">
var doc = Jsoup.parse(htmlString);
Optional&lt;Element&gt; mainEl = Optional.ofNullable(doc.select("main").first());
</pre>

<p>
The <code>main</code> tag might not be present and the <code>first</code> method 
in this case will return <code>null</code>. Therefore, we use the 
<code>Optional.ofNullable</code> method. 
</p>

<pre class="explanation">
mainEl.ifPresent(e -&gt; {
    e.append("&lt;p&gt;hello there!&lt;/p&gt;");
    e.prepend("&lt;h1&gt;Heading&lt;/h1&gt;");
});
</pre>

<p>
We only call <code>append</code> and <code>prepend</code> methods if the 
<code>Optional</code> contains the <code>main</code> tag.
</p>


<h2>Jdbi example</h2>

<p>
The <code>findOne</code> method returns the only row in the result set, if any.  
It returns <code>Optional.empty()</code> if zero rows are returned, or if the  
row itself is <code>null</code>.  
</p>

<p>
For the example, we need the <code>jdbi3-core</code> and the
<code>postgresql</code> artifacts.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import org.jdbi.v3.core.Jdbi;

import java.util.Optional;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    int id = 3;

    String query = "SELECT name FROM cars WHERE id = ?";
    Optional&lt;String&gt; res = jdbi.withHandle(handle -&gt; handle.select(query, id)
            .mapTo(String.class)
            .findOne());

    res.ifPresentOrElse(System.out::println, () -&gt; System.out.println("N/A"));
}
</pre>

<p>
In the example, we select a single cell from a row in a table. We print the data  
if it is present or <code>N/A</code> if not.
</p>



</html>

