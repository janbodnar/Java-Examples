


<h1>Java ArrayList</h1>

 
<p>
In this article we show how to work with <code>ArrayList</code> collection in
Java. Located in the <code>java.util</code> package, <code>ArrayList</code>
is an important collection of the Java collections framework.
</p>

<p>
<dfn>Java collections framework</dfn> is a unified architecture for representing
and manipulating collections, enabling collections to be manipulated
independently of implementation details. A <dfn>collection</dfn> is an object
that represents a group of objects.
</p>

<h2>ArrayList definition</h2>

<p>
<code>ArrayList</code> is an ordered sequence of elements. It is dynamic and
resizable. It provides random access to its elements. Random access means that
we can grab any element at constant time. An <code>ArrayList</code>
automatically expands as data is added. Unlike simple arrays, an
<code>ArrayList</code> can hold data of multiple data types. It permits all
elements, including <code>null</code>.
</p>

<p>
Elements in the <code>ArrayList</code> are accessed via an integer index.
Indexes are zero-based. Indexing of elements and insertion and deletion at the
end of the <code>ArrayList</code> takes constant time.
</p>

<p>
An <code>ArrayList</code> instance has a capacity. The capacity is the size of
the array used to store the elements in the list. As elements are added to an
<code>ArrayList</code>, its capacity grows automatically. Choosing a proper
capacity can save some time.
</p>


<h2>The add method</h2>

<p>
Single elements can be added to an <code>ArrayList</code> with the
<code>add</code> method.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; langs = new ArrayList&lt;&gt;();

    langs.add("Java");
    langs.add("Python");
    langs.add(1, "C#");
    langs.add(0, "Ruby");

    for (String lang : langs) {

        System.out.printf("%s ", lang);
    }

    System.out.println();
}
</pre>

<p>
The example adds elements to an array list one by one.
</p>

<pre class="explanation">
List&lt;String&gt; langs = new ArrayList&lt;&gt;();
</pre>

<p>
An <code>ArrayList</code> is created. The data type specified inside
the diamond brackets (&lt; &gt;) restricts the elements to this data
type; in our case, we have a list of strings.
</p>

<pre class="explanation">
langs.add("Java");
</pre>

<p>
An element is appended at the end of the list with the <code>add</code>
method.
</p>

<pre class="explanation">
langs.add(1, "C#");
</pre>

<p>
This time the overloaded <code>add</code> method inserts the element at the
specified position; The "C#" string will be located at the second position of
the list; remember, the <code>ArrayList</code> is an ordered sequence of
elements.
</p>

<pre class="explanation">
for (String lang : langs) {

    System.out.printf("%s ", lang);
}
</pre>

<p>
With the <code>for</code> loop, we go through the <code>ArrayList</code>
list and print its elements.
</p>

<pre class="compact">
$ java Main.java
Ruby Java C# Python
</pre>

<p>
Note that the elements keep the order they were inserted.
</p>


<h2>The List.of method</h2>

<p>
Since Java 9, we have a couple of factory methods for creating lists having a
handful of elements. The created list is immutable.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.List;

void main() {

    var words = List.of("wood", "forest", "falcon", "eagle");
    System.out.println(words);

    var values = List.of(1, 2, 3);
    System.out.println(values);
}
</pre>

<p>
In the example, we create two lists that have four and three elements.
</p>


<h2>The get and size methods</h2>

<p>
The <code>get</code> returns the element at the specified position
in this list and the <code>size</code> returns the size of
the list.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; colours = new ArrayList&lt;&gt;();

    colours.add("blue");
    colours.add("orange");
    colours.add("red");
    colours.add("green");

    String col = colours.get(1);
    System.out.println(col);

    int size = colours.size();

    System.out.printf("The size of the ArrayList is: %d%n", size);
}
</pre>

<p>
The example uses the <code>get</code> and <code>size</code> methods
of the <code>ArrayList</code>
</p>

<pre class="explanation">
String col = colours.get(1);
</pre>

<p>
The <code>get</code> method returns the second element, which is "orange".
</p>

<pre class="explanation">
int size = colours.size();
</pre>

<p>
The <code>size</code> method determines the size of our
<code>colours</code> list; we have four elements.
</p>

<pre class="compact">
$ java Main.java
orange
The size of the ArrayList is: 4
</pre>


<h2>The copy method</h2>

<p>
A copy of a list can be generated with <code>List.copy</code> method.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.List;

void main() {

    var words = List.of("forest", "wood", "eagle", "sky", "cloud");
    System.out.println(words);

    var words2 = List.copyOf(words);
    System.out.println(words2);
}
</pre>

<p>
The example creates a copy of a list with <code>List.copy</code>.
</p>


<h2>Raw ArrayList</h2>

<p>
An <code>ArrayList</code> can contain various data types. These are called raw
lists.
</p>

<div class="note">
<strong>Note:</strong> It is generally not recommended to use raw lists.
</div>

<p>
Raw lists often require casts and they are not type safe.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

class Base {}

enum Level {

    EASY,
    MEDIUM,
    HARD
}

void main() {

    Level level = Level.EASY;

    List da = new ArrayList();

    da.add("Java");
    da.add(3.5);
    da.add(55);
    da.add(new Base());
    da.add(level);

    for (Object el : da) {

        System.out.println(el);
    }
}
</pre>

<p>
The example adds five different data types into an array list — a string,
double, integer, object, and enumeration.
</p>

<pre class="explanation">
List da = new ArrayList();
</pre>

<p>
When we add multiple data types to a list, we omit the angle brackets.
</p>

<pre class="compact">
$ java Main.java
Java
3.5
55
com.zetcode.Base@659e0bfd
EASY
</pre>


<h2>The addAll method</h2>

<p>
The following example uses the <code>addAll</code> method to add multiple
elements to a list in one step.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; colours1 = new ArrayList&lt;&gt;();

    colours1.add("blue");
    colours1.add("red");
    colours1.add("green");

    List&lt;String&gt; colours2 = new ArrayList&lt;&gt;();

    colours2.add("yellow");
    colours2.add("pink");
    colours2.add("brown");

    List&lt;String&gt; colours3 = new ArrayList&lt;&gt;();
    colours3.add("white");
    colours3.add("orange");

    colours3.addAll(colours1);
    colours3.addAll(2, colours2);

    for (String col : colours3) {

        System.out.println(col);
    }
}
</pre>

<p>
Two lists are created. Later, the elements of the lists are added to the
third list with the <code>addAll</code> method.
</p>

<pre class="explanation">
colours3.addAll(colours1);
</pre>

<p>
The <code>addAll</code> method adds all of the elements to the end of the list.
</p>

<pre class="explanation">
colours3.addAll(2, colours2);
</pre>

<p>
This overloaded method adds all of the elements starting at the specified
position.
</p>

<pre class="compact">
$ java Main.java
white
orange
yellow
pink
brown
blue
red
green
</pre>


<h2>Modifying elements</h2>

<p>
The next example uses methods to modify the <code>ArrayList</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; items = new ArrayList&lt;&gt;();
    fillList(items);

    items.set(3, "watch");
    items.add("bowl");
    items.remove(0);
    items.remove("pen");

    for (Object el : items) {

        System.out.println(el);
    }

    items.clear();

    if (items.isEmpty()) {

        System.out.println("The list is empty");
    } else {
        System.out.println("The list is not empty");
    }
}

void fillList(List&lt;String&gt; data) {

    data.add("coin");
    data.add("pen");
    data.add("pencil");
    data.add("clock");
    data.add("book");
    data.add("spectacles");
    data.add("glass");
}
</pre>

<p>
An <code>ArrayList</code> is created and modified with the <code>set</code>,
<code>add</code>, <code>remove</code>, and <code>clear</code> methods.
</p>

<pre class="explanation">
items.set(3, "watch");
</pre>

<p>
The <code>set</code> method replaces the fourth element with the "watch" item.
</p>

<pre class="explanation">
items.add("bowl");
</pre>

<p>
The <code>add</code> method adds a new element at the end of the list.
</p>

<pre class="explanation">
items.remove(0);
</pre>

<p>
The <code>remove</code> method removes the first element, having index 0.
</p>

<pre class="explanation">
items.remove("pen");
</pre>

<p>
The overloaded <code>remove</code> method remove the first occurrence
of the "pen" item.
</p>

<pre class="explanation">
items.clear();
</pre>

<p>
The <code>clear</code> method removes all elements from the list.
</p>

<pre class="explanation">
if (items.isEmpty()) {
</pre>

<p>
The <code>isEmpty</code> method determines if the list is empty.
</p>

<pre class="compact">
$ java Main.java
pencil
watch
book
spectacles
glass
bowl
The list is empty
</pre>


<h2>The removeIf method</h2>

<p>
The <code>removeIf</code> method removes all of the elements of a
collection that satisfy the given predicate.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;Integer&gt; values = new ArrayList&lt;&gt;();
    values.add(5);
    values.add(-3);
    values.add(2);
    values.add(8);
    values.add(-2);
    values.add(6);

    values.removeIf(val -&gt; val &lt; 0);

    System.out.println(values);
}
</pre>

<p>
In our example, we have an <code>ArrayList</code> of integers. We use
the <code>removeIf</code> method to delete all negative values.
</p>

<pre class="explanation">
values.removeIf(val -&gt; val &lt; 0);
</pre>

<p>
All negative numbers are removed from the array list.
</p>

<pre class="compact">
$ java Main.java
[5, 2, 8, 6]
</pre>


<h2>The removeAll method</h2>

<p>
The <code>removeAll</code> method removes from this list all of its elements
that are contained in the specified collection. Note that all elements are
removed with <code>clear</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

void main() {

    List&lt;String&gt; letters = new ArrayList&lt;&gt;();
    letters.add("a");
    letters.add("b");
    letters.add("c");
    letters.add("a");
    letters.add("d");

    System.out.println(letters);

    letters.removeAll(Collections.singleton("a"));
    System.out.println(letters);
}
</pre>

<p>
In the example, we remove all "a" letters from the list.
</p>


<h2>The replaceAll method</h2>

<p>
The <code>replaceAll</code> method replaces each element of a list with the
result of applying the operator to that element.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;
import java.util.function.UnaryOperator;

void main() {

    List&lt;String&gt; items = new ArrayList&lt;&gt;();
    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("class");

    UnaryOperator&lt;String&gt; uo = (x) -&gt; x.toUpperCase();

    items.replaceAll(uo);

    System.out.println(items);
}
</pre>

<p>
The example applies an operator on each of the list elements; the elements'
letters are transformed to uppercase.
</p>

<pre class="explanation">
UnaryOperator&lt;String&gt; uo = (x) -&gt; x.toUpperCase();
</pre>

<p>
A <code>UnaryOperator</code> that transforms letters to uppercase is created.
</p>

<pre class="explanation">
items.replaceAll(uo);
</pre>

<p>
The operator is applied on the list elements with the <code>replaceAll</code>
method.
</p>

<pre class="compact">
$ java Main.java
[COIN, PEN, CUP, NOTEBOOK, CLASS]
</pre>

<p>
The second example uses the <code>replaceAll</code> method to capitalize
string items.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;
import java.util.function.UnaryOperator;

class MyOperator&lt;T&gt; implements UnaryOperator&lt;String&gt; {

    @Override
    public String apply(String s) {

        if (s == null || s.length() == 0) {
            return s;
        }

        return s.substring(0, 1).toUpperCase() + s.substring(1);
    }
}

void main() {

    List&lt;String&gt; items = new ArrayList&lt;&gt;();

    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("glass");

    items.replaceAll(new MyOperator&lt;&gt;());

    System.out.println(items);
}
</pre>

<p>
We have a list of string items. These items are capitalized with the
help of the <code>replaceAll</code> method.
</p>

<pre class="explanation">
class MyOperator&lt;T&gt; implements UnaryOperator&lt;String&gt; {
</pre>

<p>
A custom <code>UnaryOperator</code> is created.
</p>

<pre class="explanation">
@Override
public String apply(String s) {

    if (s == null || s.length() == 0) {
        return s;
    }

    return s.substring(0, 1).toUpperCase() + s.substring(1);
}
</pre>

<p>
Inside the <code>UnaryOperator's</code> <code>apply</code> method, we retur the
string with its first letter in uppercase.
</p>

<pre class="explanation">
items.replaceAll(new MyOperator&lt;&gt;());
</pre>

<p>
The operator is applied on the list items.
</p>

<pre class="compact">
$ java Main.java
[Coin, Pen, Cup, Notebook, Glass]
</pre>


<h2>The contains method</h2>

<p>
The <code>contains</code> method returns true if a list contains the specified
element.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; items = new ArrayList&lt;&gt;();

    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("class");

    String item = "pen";

    if (items.contains(item)) {

        System.out.printf("There is a %s in the list%n", item);
    }
}
</pre>

<p>
The example checks if the specified item is in the list.
</p>

<pre class="explanation">
if (items.contains(item)) {

    System.out.printf("There is a %s in the list%n", item);
}
</pre>

<p>
The message is printed if the item is in the list.
</p>

<pre class="compact">
$ java Main.java
There is a pen in the list
</pre>


<h2>Getting index of elements</h2>

<p>
Each of the elements in an <code>ArrayList</code> has its own index number.
The <code>indexOf</code> returns the index of the first occurrence of the
specified element, or -1 if the list does not contain the element.
The <code>lasindexOf</code> returns the index of the last occurrence of the
specified element, or -1 if the list does not contain the element.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; colours = new ArrayList&lt;&gt;();

    colours.add(0, "blue");
    colours.add(1, "orange");
    colours.add(2, "red");
    colours.add(3, "green");
    colours.add(4, "orange");

    int idx1 = colours.indexOf("orange");
    System.out.println(idx1);

    int idx2 = colours.lastIndexOf("orange");
    System.out.println(idx2);
}
</pre>

<p>
The example prints the first and last index of the "orange" element.
</p>

<pre class="compact">
$ java Main.java
1
4
</pre>


<h2>List of lists</h2>

<p>
We can add other lists into a list.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;Integer&gt; l1 = new ArrayList&lt;&gt;();
    l1.add(1);
    l1.add(2);
    l1.add(3);

    List&lt;Integer&gt; l2 = new ArrayList&lt;&gt;();
    l2.add(4);
    l2.add(5);
    l2.add(6);

    List&lt;Integer&gt; l3 = new ArrayList&lt;&gt;();
    l3.add(7);
    l3.add(8);
    l3.add(9);

    List&lt;List&lt;Integer&gt;&gt; nums = new ArrayList&lt;&gt;();
    nums.add(l1);
    nums.add(l2);
    nums.add(l3);

    System.out.println(nums);

    for (List&lt;Integer&gt; list : nums) {

        for (Integer n : list) {

            System.out.printf("%d ", n);
        }

        System.out.println();
    }
}
</pre>

<p>
The example creates three lists of integers. Later, the lists are added into
another fourth list.
</p>

<pre class="explanation">
List&lt;Integer&gt; l1 = new ArrayList&lt;&gt;();
l1.add(1);
l1.add(2);
l1.add(3);
</pre>

<p>
A list of integers is created.
</p>

<pre class="explanation">
List&lt;List&gt; nums = new ArrayList&lt;&gt;();
nums.add(l1);
nums.add(l2);
nums.add(l3);
</pre>

<p>
A list of lists is created.
</p>

<pre class="explanation">
for (List&lt;Integer&gt; list : nums) {

    for (Integer n : list) {

        System.out.printf("%d ", n);
    }

    System.out.println();
}
</pre>

<p>
We use two for loops to go through all the elements.
</p>

<pre class="compact">
$ java Main.java
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
1 2 3
4 5 6
7 8 9
</pre>


<h2>The subList method</h2>

<p>
The <code>subList</code> method returns a view of the portion of a list
between the specified fromIndex, inclusive, and toIndex, exclusive. The changes
in a sublist are reflected in the original list.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;

void main() {

    List&lt;String&gt; items = new ArrayList&lt;&gt;();

    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("glass");
    items.add("chair");
    items.add("ball");
    items.add("bowl");

    List&lt;String&gt; items2 = items.subList(2, 5);

    System.out.println(items2);

    items2.set(0, "bottle");

    System.out.println(items2);
    System.out.println(items);
}
</pre>

<p>
The example creates a sublist from a list of items.
</p>

<pre class="explanation">
List&lt;String&gt; items2 = items.subList(2, 5);
</pre>

<p>
A sublist is created with the <code>subList</code> method; it contains
items with indexes 2, 3, and 4.
</p>

<pre class="explanation">
items2.set(0, "bottle");
</pre>

<p>
We replace the first item of the sublist; the modification is reflected
in the original list, too.
</p>

<pre class="compact">
$ java Main.java
[cup, notebook, glass]
[bottle, notebook, glass]
[coin, pen, bottle, notebook, glass, chair, ball, bowl]
</pre>


<h2>Traversing elements</h2>

<p>
In the following example, we show five ways to traverse an <code>ArrayList</code>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;

void main() {

    List&lt;Integer&gt; nums = new ArrayList&lt;&gt;();
    nums.add(2);
    nums.add(6);
    nums.add(7);
    nums.add(3);
    nums.add(1);
    nums.add(8);

    for (int i = 0; i &lt; nums.size(); i++) {

        System.out.printf("%d ", nums.get(i));
    }

    System.out.println();

    for (int num : nums) {

        System.out.printf("%d ", num);
    }

    System.out.println();

    int j = 0;
    while (j &lt; nums.size()) {

        System.out.printf("%d ", nums.get(j));
        j++;
    }

    System.out.println();

    ListIterator&lt;Integer&gt; it = nums.listIterator();

    while(it.hasNext()) {

        System.out.printf("%d ", it.next());
    }

    System.out.println();

    nums.forEach(e -&gt; System.out.printf("%d ", e));
    System.out.println();
}
</pre>

<p>
In the example, we traverse an array list of integers with for loops, while loop,
iterator, and <code>forEach</code> construct.
</p>

<pre class="explanation">
List&lt;Integer&gt; nums = new ArrayList&lt;&gt;();
nums.add(2);
nums.add(6);
nums.add(7);
nums.add(3);
nums.add(1);
nums.add(8);
</pre>

<p>
We have created an <code>ArrayList</code> of integers.
</p>

<pre class="explanation">
for (int i = 0; i &lt; nums.size(); i++) {

    System.out.printf("%d ", nums.get(i));
}
</pre>

<p>
Here, we use the classic for loop to iterate over the list.
</p>

<pre class="explanation">
for (int num : nums) {

    System.out.printf("%d ", num);
}
</pre>

<p>
The second way uses the enhanced-for loop, which was introduced
int Java 5.
</p>

<pre class="explanation">
int j = 0;
while (j &lt; nums.size()) {

    System.out.printf("%d ", nums.get(j));
    j++;
}
</pre>

<p>
The third way uses the while loop.
</p>

<pre class="explanation">
ListIterator&lt;Integer&gt; it = nums.listIterator();

while(it.hasNext()) {

    System.out.printf("%d ", it.next());
}
</pre>

<p>
Here, a <code>ListIterator</code> is used to traverse the list.
</p>

<pre class="explanation">
nums.forEach(e -&gt; System.out.printf("%d ", e));
</pre>

<p>
In the last way, we use the <code>forEach</code> method, which
was introduced in Java 8.
</p>

<pre class="compact">
$ java Main.java
2 6 7 3 1 8
2 6 7 3 1 8
2 6 7 3 1 8
2 6 7 3 1 8
2 6 7 3 1 8
</pre>


<h2>Sorting elements</h2>

<p>
There are different wasy to sort an <code>ArrayList</code>.
</p>

<h3>Sorting with the sort method</h3>

<p>
The <code>ArrayList's</code> <code>sort</code> method sorts a list
according to the order induced by the specified comparator.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;


void main() {

    List&lt;Person&gt; persons = createList();
    persons.sort(Comparator.comparing(Person::age).reversed());

    System.out.println(persons);

}

List&lt;Person&gt; createList() {

    List&lt;Person&gt; persons = new ArrayList&lt;&gt;();

    persons.add(new Person(17, "Jane"));
    persons.add(new Person(32, "Peter"));
    persons.add(new Person(47, "Patrick"));
    persons.add(new Person(22, "Mary"));
    persons.add(new Person(39, "Robert"));
    persons.add(new Person(54, "Greg"));

    return persons;
}

record Person(int age, String name) {}
</pre>

<p>
We have an <code>ArrayList</code> of custom <code>Person</code> classes.
We sort the persons according to their age in a reversed order.
</p>

<pre class="explanation">
persons.sort(Comparator.comparing(Person::age).reversed());
</pre>

<p>
This line sorts the persons by their age, from the oldest to the youngest.
</p>

<pre class="compact">
$ java Main.java
[Age: 54 Name: Greg, Age: 47 Name: Patrick, Age: 39 Name: Robert, Age: 32 Name: Peter,
    Age: 22 Name: Mary, Age: 17 Name: Jane]
</pre>


<h3>Sorting elements using stream</h3>

<p>
In the second example, we use Java stream to sort the <code>ArrayList</code>.
The Stream API allows a more powerful way to do sorting.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

void main() {

    List&lt;Country&gt; countries = createList();

    List&lt;Country&gt; sorted_countries = countries.stream()
            .sorted((e1, e2) -&gt; Integer.compare(e1.population,
                    e2.population))
            .collect(Collectors.toList());

    System.out.println(sorted_countries);
}

List&lt;Country&gt; createList() {

    List&lt;Country&gt; countries = new ArrayList&lt;&gt;();

    countries.add(new Country("Slovakia", 5424000));
    countries.add(new Country("Hungary", 9845000));
    countries.add(new Country("Poland", 38485000));
    countries.add(new Country("Germany", 81084000));
    countries.add(new Country("Latvia", 1978000));

    return countries;
}

record Country(String name, int population) {
}
</pre>

<p>
In this example, we have a list of countries. Each country has a name and
population. The countries are sorted by population.
</p>

<pre class="explanation">
List&lt;Country&gt; sorted_countries = countries.stream()
        .sorted((e1, e2) -&gt; Integer.compare(e1.population,
                e2.population))
        .collect(Collectors.toList());
</pre>

<p>
With the <code>stream</code> method, we create a stream from a list. The
<code>sorted</code> method sorts elements according to the provided
comparator. With <code>Integer.compare</code> we compare the populations of
countries. With <code>collect</code>, we transform the stream into a list of
countries.
</p>

<pre class="compact">
$ java Main.java
[Country{name=Latvia, population=1978000}, Country{name=Slovakia, population=5424000},
Country{name=Hungary, population=9845000}, Country{name=Poland, population=38485000},
Country{name=Germany, population=81084000}]
</pre>

<p>
The countries are sorted by their population in ascending mode.
</p>


<h2>Working with ArrayList and simple Java array</h2>

<p>
The following example uses an <code>ArrayList</code> with
a simple Java array.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;
import java.util.List;

void main() {

    String[] a = new String[] { "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Neptune" };

    List&lt;String&gt; planets = List.of(a);
    System.out.println(planets);

    String[] planets2 = planets.toArray(new String[0]);
    System.out.println(Arrays.toString(planets2));
}
</pre>

<p>
An <code>ArrayList</code> is converted to an array and vice versa.
</p>

<pre class="explanation">
String[] a = new String[] { "Mercury", "Venus", "Earth",
        "Mars", "Jupiter", "Saturn", "Uranus", "Neptune" };
</pre>

<p>
We have an array of strings.
</p>

<pre class="explanation">
List&lt;String&gt; planets = List.of(a);
</pre>

<p>
We generate an immutable list from the array with <code>List.of</code>;
</p>

<pre class="explanation">
String[] planets2 = planets.toArray(new String[0]);
</pre>

<p>
The <code>ArrayList's</code> <code>toArray</code> is used to convert a list to
an array.
</p>


<h2>Stream to list</h2>

<p>
Java streams can be converted to lists using collectors.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

void main() {

    var words = Stream.of("forest", "eagle", "river", "cloud", "sky");

    List&lt;String&gt; words2 = words.collect(Collectors.toList());
    System.out.println(words2.getClass());
}
</pre>

<p>
We have a stream of strings. We convert the stream to a list with
<code>Collectors.toList</code>.
</p>



<!-- TODO SplitIterator, arraylist hierarchy, reference, more sorting examples -->


