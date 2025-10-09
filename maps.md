
<h1>Java HashMap</h1>


<p>
In this article we show how to use Java HashMap collection.
</p>

<p>
<dfn>HashMap</dfn> is a container that stores key-value pairs. Each key is
associated with one value. Keys in a <code>HashMap</code> must be unique.
<code>HashMap</code> is called an associative array or a dictionary in other
programming languages. <code>HashMaps</code> take more memory because for each
value there is also a key. Deletion and insertion operations take constant time.
<code>HashMaps</code> can store null values.
</p>

<p>
<code>HashMaps</code> do not maintain order.
</p>

<p>
<dfn>Map.Entry</dfn> represents a key-value pair in  <code>HashMap</code>.
<code>HashMap's</code> <code>entrySet</code> returns a <code>Set</code> view of
the mappings contained in the map. A set of keys is retrieved with the
<code>keySet</code>
method.
</p>

<p>
<code>HashMap</code> extends <code>AbstractMap</code> and implements
<code>Map</code>. The <code>Map</code> provides method signatures including
<code>get</code>, <code>put</code>, <code>size</code>, or <code>isEmpty</code>.
</p>


<h2>HashMap Constructors</h2>

<ul>
<li><code>HashMap</code> — constructs an empty <code>HashMap</code> with the default initial capacity (16)
and the default load factor (0.75).</li>
<li><code>HashMap(int initialCapacity)</code> — constructs an empty <code>HashMap</code> with the given initial capacity and the default load factor (0.75).
<li><code>HashMap(int initialCapacity, float loadFactor)</code> — constructs an empty <code>HashMap</code> with the given initial capacity and load factor.</li>
<li><code>HashMap(Map<? extends K,? extends V> m)</code> — constructs a new <code>HashMap</code> with the same mappings as the given <code>Map</code>.</li>
</ul>

<p>
<code>K</code> is the type of the map keys and <code>V</code> is the type of
mapped values.
</p>


<h2>HashMap methods</h2>

<p>
The following table provides a few <code>HashMap</code> methods.
</p>

<table>
<tbody>
<tr>
<th>Modifier and type</th>
<th>Method</th>
<th>Description</th>
</tr>
<tr>
<td>void</td>
<td>clear()</td>
<td>Removes all mappings from the map.</td>
</tr>
<tr>
<td>Object</td>
<td>clone()</td>
<td>Returns a shallow copy of the HashMap instance: the keys and values themselves are not cloned.</td>
</tr>
<tr>
<td>V boolean</td>
<td>containsKey(Object key)</td>
<td>Returns true if this map contains a mapping for the specified key.</td>
</tr>
<tr>
<td>Set<Map.Entry<K,V></td>
<td>entrySet()</td>
<td>Returns a Set view of the mappings contained in this map.</td>
</tr>
<tr>
<td>boolean</td>
<td>isEmpty()</td>
<td>Returns true if this map is empty.</td>
</tr>
<tr>
<td>Set<K></td>
<td>keySet()</td>
<td>Returns a Set view of the keys contained in this map.</td>
</tr>
<tr>
<td>V</td>
<td>put(K key, V value)</td>
<td>Adds new mapping to the map.</td>
</tr>
<tr>
<td>V</td>
<td>remove(Object key)</td>
<td>Removes the mapping for the specified key from this map if present.</td>
</tr>
<tr>
<td>V</td>
<td>get(Object key)</td>
<td>Returns the value to which the specified key is mapped, or null if this map contains no mapping for the key.</td>
</tr>
<tr>
<td>void</td>
<td>forEach(BiConsumer<? super K,? super V> action)</td>
<td>Performs the given action for each entry in this map until
all entries have been processed or the action throws an exception.</td>
</tr>
<tr>
<td>V</td>
<td>replace(K key, V value)</td>
<td>Replaces the entry for the specified key only if it is currently mapped to some value.</td>
</tr>
<tr>
<td>int</td>
<td>size()</td>
<td>Returns the number of key-value mappings in this map.</td>
</tr>
<tr>
<td>Collection<V></td>
<td>values()</td>
<td>Returns a Collection view of the values contained in this map.</td>
</tr>

</tbody>
</table>

<p>
In this article we work with several of these methods.
</p>


<h2>HashMap creation</h2>

<p>
<code>HashMap</code> is created with <code>new</code> keyword.
</p>

<pre class="compact">
Map<String, String> capitals = new HashMap<>();
</pre>

<p>
We specify the types of keys and values between angle brackets.
Thanks to <em>type inference</em>, it is not necessary to provide
types on the right side of the declaration.
</p>


<h2>The put method</h2>

<p>
The <code>put</code> method is used to add a new mapping to the map.
</p>

<pre class="compact">
capitals.put("svk", "Bratislava");
</pre>

<p>
The first parameter is the key, the second is the value.
</p>


<h2>The remove method</h2>

<p>
The <code>remove</code> method is used to delete a pair from the map.
</p>

<pre class="compact">
capitals.remove("pol");
</pre>

<p>
The parameter is the key whose mapping is to be removed from the map.
</p>

<h2>HashMap initialization</h2>

<p>
Since Java 9, we have factory methods for <code>HashMap</code> initialization.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Map;
import static java.util.Map.entry;

void main() {

    Map<Integer, String> colours = Map.of(1, "red", 2, "blue", 3, "brown");
    System.out.println(colours);

    Map<String, String> countries = Map.ofEntries(
            entry("de", "Germany"),
            entry("sk", "Slovakia"),
            entry("ru", "Russia"));

    System.out.println(countries);
}
</pre>

<p>
The example uses <code>Map.of</code> and <code>Map.ofEntries</code>
to initialize hashmaps. These two factory methods return <em>unmodifiable</em>
maps.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

// up to Java 8
void main() {

    Map<String, String> countries = new HashMap<>() {
        {
            put("de", "Germany");
            put("sk", "Slovakia");
            put("ru", "Russia");
        }
    };

    System.out.println(countries);
}
</pre>

<p>
In this example we create a modifiable hashmap. This way of initialization
is dubbed double-braced hashmap initialization.
</p>


<h2>The size method</h2>

<p>
The size of the <code>HashMap</code> is determined with the <code>size</code>
method.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    int size = capitals.size();

    System.out.printf("The size of the HashMap is %d%n", size);

    capitals.remove("pol");
    capitals.remove("ita");

    size = capitals.size();

    System.out.printf("The size of the HashMap is %d%n", size);
}
</pre>

<p>
In the code example, we create a <code>HashMap</code> and determine its size
with <code>size</code>. Then we remove some pairs and determine its size again.
We print the findings to the console.
</p>

<pre class="explanation">
capitals.put("svk", "Bratislava");
capitals.put("ger", "Berlin");
</pre>

<p>
With <code>put</code>, we add new pairs into the <code>HashMap</code>.
</p>

<pre class="explanation">
int size = capitals.size();
</pre>

<p>
Here we get the size of the map.
</p>

<pre class="explanation">
capitals.remove("pol");
capitals.remove("ita");
</pre>

<p>
With <code>remove</code>, we delete two pairs from the map.
</p>

<pre class="compact">
The size of the HashMap is 6
The size of the HashMap is 4
</pre>


<h2>The get method</h2>

<p>
To retrieve a value from a <code>HashMap</code>, we use the <code>get</code>
method. It takes a key as a parameter.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    String cap1 = capitals.get("ita");
    String cap2 = capitals.get("svk");

    System.out.println(cap1);
    System.out.println(cap2);
}
</pre>

<p>
In the example, we retrieve two values from the map.
</p>

<pre class="explanation">
String cap2 = capitals.get("svk");
</pre>

<p>
Here we get a value which has <code>"svk"</code> key.
</p>


<h2>The clear method</h2>

<p>
The <code>clear</code> method removes all pairs from the <code>HashMap</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.clear();

    if (capitals.isEmpty()) {

        System.out.println("The map is empty");
    } else {

        System.out.println("The map is not empty");
    }
}
</pre>

<p>
In the example, we remove all elements and print the size of the map to the
console.
</p>

<pre class="explanation">
capitals.clear();
</pre>

<p>
We remove all pairs with <code>clear</code>.
</p>

<pre class="explanation">
if (capitals.isEmpty()) {

    System.out.println("The map is empty");
} else {

    System.out.println("The map is not empty");
}
</pre>

<p>
With the <code>isEmpty</code> method, we check if the map
is empty.
</p>


<h2>The containsKey method</h2>

<p>
The <code>containsKey</code> method returns true if the map contains a mapping
for the specified key.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    String key1 = "ger";
    String key2 = "rus";

    if (capitals.containsKey(key1)) {

        System.out.printf("HashMap contains %s key%n", key1);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key1);
    }

    if (capitals.containsKey(key2)) {

        System.out.printf("HashMap contains %s key%n", key2);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key2);
    }
}
</pre>

<p>
In the example, we check if the map contains two keys.
</p>

<pre class="explanation">
if (capitals.containsKey(key1)) {

    System.out.printf("HashMap contains %s key%n", key1);
} else {

    System.out.printf("HashMap does not contain %s key%n", key1);
}
</pre>

<p>
This if statement prints a message depending on whether the map
contains the given key.
</p>

<pre class="compact">
HashMap contains ger key
HashMap does not contain rus key
</pre>


<h2>The replace method</h2>

<p>
There are <code>replace</code> methods which enable programmers to replace
entries.
</p>

<pre class="compact">
replace(K key, V value)
</pre>

<p>
This method replaces the entry for the specified key only if it is currently
mapped to some value.
</p>

<pre class="compact">
replace(K key, V oldValue, V newValue)
</pre>

<p>
This method replaces the entry for the specified key only if it is currently
mapped to the specified value.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("day", "Monday");
    capitals.put("country", "Poland");
    capitals.put("colour", "blue");

    capitals.replace("day", "Sunday");
    capitals.replace("country", "Russia", "Great Britain");
    capitals.replace("colour", "blue", "green");

    capitals.entrySet().forEach(System.out::println);
}
</pre>

<p>
In the example, we replace pairs in the map with <code>replace</code>.
</p>

<pre class="explanation">
capitals.replace("day", "Sunday");
</pre>

<p>
Here we replace a value for the <code>"day"</code> key.
</p>

<pre class="explanation">
capitals.replace("country", "Russia", "Great Britain");
</pre>

<p>
In this case, the value is not replaced because the key
is not currently set to <code>"Russia"</code>.
</p>

<pre class="explanation">
capitals.replace("colour", "blue", "green");
</pre>

<p>
Because the old value is correct, the value is replaced.
</p>

<pre class="compact">
country=Poland
colour=green
day=Sunday
</pre>


<h2>Convert HashMap to List</h2>

<p>
In the next example we convert <code>HashMap</code> entries to a list of
entries.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.Set;

void main() {

    Map&lt;String, String&gt; colours = Map.of(
            "AliceBlue", "#f0f8ff",
            "GreenYellow", "#adff2f",
            "IndianRed", "#cd5c5c",
            "khaki", "#f0e68c"
    );

    Set&lt;Map.Entry&lt;String, String&gt;&gt; entries = colours.entrySet();
    List&lt;Map.Entry&lt;String, String&gt;&gt; mylist = new ArrayList&lt;&gt;(entries);

    System.out.println(mylist);
}
</pre>

<p>
The <code>entrySet</code> returns a set view of mappings, which is later 
passed to the constructor of the <code>ArrayList</code>.
</p>


<h2>Iteration with forEach</h2>

<p>
We use the <code>forEach</code> method to iterate over the key-value pairs of
the <code>HashMap</code>. The <code>forEach</code> method performs the given
action for each element of the map until all elements have been processed or the
action throws an exception.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.forEach((k, v) -&gt; System.out.format("%s: %s%n", k, v));
}
</pre>

<p>
In the code example, we iterate over a <code>HashMap</code> with
<code>forEach</code> using a lambda expression.
</p>

<pre class="explanation">
capitals.forEach((k, v) -&gt; System.out.format("%s: %s%n", k, v));
</pre>

<p>
With <code>forEach</code> we iterate over all pairs of the map.
</p>


<h2>Iteration with enhanced for loop</h2>

<p>
The enhanced for loop can be used to iterate over a <code>HashMap</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    for (Map.Entry&lt;String, String&gt; pair: capitals.entrySet()) {

        System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
    }
}
</pre>

<p>
In the example we iterate over a <code>HashMap</code> with enhanced for loop.
</p>

<pre class="explanation">
for (Map.Entry&lt;String, String&gt; pair: capitals.entrySet()) {

    System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
}
</pre>

<p>
In each for cycle, a new key-value couple is assigned to the <code>pair</code>
variable.
</p>

<hr>

<p>
With type inference, we can shorten the code a bit. 
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    for (var pair: capitals.entrySet()) {

        System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
    }
}
</pre>

<p>
We shorten the code by using a <code>var</code> keyword in the for loop.
</p>


<h2>Iteration over keys</h2>

<p>
We might want to iterate only over keys of a <code>HashMap</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Set&lt;String&gt; keys = capitals.keySet();

    keys.forEach(System.out::println);
}
</pre>

<p>
The example iterates over keys of the <code>capitals</code> map.
</p>

<pre class="explanation">
Set<String> keys = capitals.keySet();
</pre>

<p>
The keys of a <code>HashMap</code> are retrieved with the <code>keySet</code>
method, which returns a <code>Set</code> of keys. Keys must be unique; therefore,
we have a <code>Set</code>. <code>Set</code> is a collection that contains no
duplicate elements.
</p>

<pre class="explanation">
keys.forEach(System.out::println);
</pre>

<p>
We go over the set of keys with <code>forEach</code>.
</p>


<h2>Iteration over values</h2>

<p>
We might want to iterate only over values of a <code>HashMap</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Collection&lt;String&gt; vals = capitals.values();

    vals.forEach(System.out::println);
}
</pre>

<p>
The example iterates over values of a <code>HashMap</code>.
</p>

<pre class="explanation">
Collection<String> vals = capitals.values();
</pre>

<p>
The values of a <code>HashMap</code> are retrieved with the <code>values</code>
method.
</p>

<pre class="explanation">
vals.forEach(System.out::println);
</pre>

<p>
We go over the collection with <code>forEach</code>.
</p>


<h2>Filtering HashMap</h2>

<p>
<code>HashMap</code> can be filtered with the <code>filter</code> method
of the Java Stream API.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.HashMap;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map&lt;String, String&gt; capitals = new HashMap&lt;&gt;();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Map&lt;String, String&gt; filteredCapitals = capitals.entrySet().stream()
            .filter(e -&gt; e.getValue().length() == 6)
            .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    filteredCapitals.entrySet().forEach(System.out::println);
}
</pre>

<p>
In the example, we filter the map to contain only pairs whose values' size is
equal to six.
</p>

<pre class="compact">
czk=Prague
ger=Berlin
pol=Warsaw
</pre>


<h2>List of maps</h2>

<p>
In the next example, we have a list of maps. 
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

void main() {

    Map&lt;String,Integer&gt; fruits1 = new HashMap&lt;&gt;();
    fruits1.put("oranges", 2);
    fruits1.put("bananas", 3);

    Map&lt;String,Integer&gt; fruits2 = new HashMap&lt;&gt;();
    fruits2.put("plums", 6);
    fruits2.put("apples", 7);

    List&lt;Map&lt;String,Integer&gt;&gt; all = new ArrayList&lt;&gt;();
    all.add(fruits1);
    all.add(fruits2);

    all.forEach(e -&gt; e.forEach((k, v) -&gt; System.out.printf("k: %s v %d%n", k, v)));
}
</pre>

<p>
We define two maps and insert them into a list. Then we interate over the list 
with two <code>forEach</code> loops.
</p>






