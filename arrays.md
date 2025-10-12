
<h1>Java array</h1>

<p class="last_mod">
last modified February 23, 2024
</p>
 
<p>
In this article we cover arrays. An array is a container object that holds a
fixed number of values of a single type. The length of an array is established
when the array is created. After creation, its length is fixed.
</p>

<p>
A scalar variable can hold only one item at a time. Arrays can hold multiple
items. These items are called elements of the array. Arrays store data of the
<em>same data type</em>. Each element can be referred to by an index. Arrays are
zero based. The index of the first element is zero.
</p>


<h2>Array definition</h2>

<p>
Arrays are used to store data of our applications. We declare arrays to be of a
certain data type. We specify their length. And we initialize arrays with data.
We have several methods for working with arrays. We can modify the elements,
sort them, copy them or search for them.
</p>

<pre class="compact">
int[] ages;
String[] names;
float[] weights;
</pre>

<p>
We have three array declarations. The declaration consists of two parts: the
type of the array and the array name. The type of an array has a data type
that determines the types of the elements within an array (<code>int</code>,
<code>String</code>, <code>float</code> in our case) and a pair of square brackets
<code>[]</code>. The brackets indicate that we have an array.
</p>

<p>
<em>Collections</em> serve a similar purpose like arrays. They are more powerful
than arrays. They will be described later in a separate chapter.
</p>


<h2>Initializing arrays</h2>

<p>
There are several ways how we can initialize an array in Java. In the first
example, an array is created and initialized in two steps.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] a = new int[5];

    a[0] = 1;
    a[1] = 2;
    a[2] = 3;
    a[3] = 4;
    a[4] = 5;

    System.out.println(Arrays.toString(a));
}
</pre>

<p>
We create and initialize a numerical array. The contents of the array are
printed to the console.
</p>

<pre class="explanation">
int[] a = new int[5];
</pre>

<p>
Here we create an array which can contain five elements. The statement allocates
memory for five integers.  The square brackets are used for declaring an array,
the type (<code>int</code> in our case) tells us what type of values the array
will hold. An array is an object and therefore it is created with the
<code>new</code>
keyword.
</p>

<pre class="explanation">
a[0] = 1;
a[1] = 2;
a[2] = 3;
a[3] = 4;
a[4] = 5;
</pre>

<p>
We initialize the array with some data. This is assignment initialization.
The indexes are in the square brackets. Number 1 is going to be the first
element of the array, number 2 is the second etc.
</p>

<pre class="explanation">
System.out.println(Arrays.toString(a));
</pre>

<p>
The <code>Arrays</code> class is a helper class which  contains various methods
for manipulating arrays. The <code>toString</code> method returns a string
representation of the contents of the specified array. This method is helpful in
debugging.
</p>

<pre class="compact">
$ java Main.java
[1, 2, 3, 4, 5]
</pre>


<p>
We can declare and initialize an array in one statement.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] a = new int[] { 2, 4, 5, 6, 7, 3, 2 };

    System.out.println(Arrays.toString(a));
}
</pre>

<p>
This is a modified version of the previous program.
</p>

<pre class="explanation">
int[] array = new int[] { 2, 4, 5, 6, 7, 3, 2 };
</pre>

<p>
An array is created and initialized in one step. The elements are specified in
curly brackets. We did not specify the length of the array. The compiler will do
it for us.
</p>

<p>
The one step creation and initialization can be further simplified by only
specifying the numbers between the curly brackets.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] a = { 2, 4, 5, 6, 7, 3, 2 };

    System.out.println(Arrays.toString(a));
}
</pre>

<p>
An array of integers is created using the most simple way
of array creation.
</p>

<pre class="explanation">
int[] a = { 2, 4, 5, 6, 7, 3, 2 };
</pre>

<p>
The <code>new int[]</code> construct can be omitted. The right side of the
statement is an <em>array literal</em> notation. It resembles the C/C++ style of
array initialization. Even if we drop the <code>new</code> keyword, the array is
created the same way as in previous two examples. This is just a convenient
shorthand notation.
</p>


<h2>Accessing array elements</h2>

<p>
After the array is created, its elements can be accessed by their index. The
index is a number placed inside square brackets which follow the array name.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    String[] names = {"Jane", "Thomas", "Lucy", "David"};

    System.out.println(names[0]);
    System.out.println(names[1]);
    System.out.println(names[2]);
    System.out.println(names[3]);
}
</pre>

<p>
In the example, we create an array of string names. We access each of the
elements by its index and print them to the terminal.
</p>

<pre class="explanation">
String[] names = {"Jane", "Thomas", "Lucy", "David"};
</pre>

<p>
An array of strings is created.
</p>

<pre class="explanation">
System.out.println(names[0]);
System.out.println(names[1]);
System.out.println(names[2]);
System.out.println(names[3]);
</pre>

<p>
Each of the elements of the array is printed to the console. With the
<code>names[0]</code> construct, we refer to the first element of the names
array.
</p>

<pre class="compact">
$ java Main.java
Jane
Thomas
Lucy
David
</pre>

<p>
Running the example we get the above output.
</p>

<p>
It is possible to change the elements of an array. The elements are not
immutable.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] vals = { 1, 2, 3 };

    vals[0] *= 2;
    vals[1] *= 2;
    vals[2] *= 2;

    System.out.println(Arrays.toString(vals));
}
</pre>

<p>
We have an array of three integers. Each of the values will be multiplied by
two.
</p>

<pre class="explanation">
int[] vals = { 1, 2, 3 };
</pre>

<p>
An array of three integers is created.
</p>

<pre class="explanation">
vals[0] *= 2;
vals[1] *= 2;
vals[2] *= 2;
</pre>

<p>
Using the element access, we multiply each value in the array by two.
</p>

<pre class="compact">
$ java Main.java
[2, 4, 6]
</pre>


<h2>Traversing arrays</h2>

<p>
We often need to go through all elements of an array. We show two common methods
for traversing an array.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    String[] planets = { "Mercury", "Venus", "Mars", "Earth", "Jupiter",
            "Saturn", "Uranus", "Neptune", "Pluto" };

    for (int i = 0; i &lt; planets.length; i++) {

        System.out.println(planets[i]);
    }

    for (String planet : planets) {

        System.out.println(planet);
    }
}
</pre>

<p>
An array of planet names is created. We use the for loop to print all the
values.
</p>

<pre class="explanation">
for (int i=0; i &lt; planets.length; i++) {

    System.out.println(planets[i]);
}
</pre>

<p>
In this loop, we utilize the fact that we can get the number of elements from
the array object. The number of elements is stored in the <code>length</code>
constant.
</p>

<pre class="explanation">
for (String planet : planets) {

    System.out.println(planet);
}
</pre>

<p>
An enhanced for keyword can be used to make the code more compact when
traversing arrays or other collections. In each cycle, the planet variable is
passed the next value from the planets array.
</p>


<h2>Passing arrays to methods</h2>

<p>
In the next example, we pass an array to a method.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] a = { 3, 4, 5, 6, 7 };
    int[] r = reverseArray(a);

    System.out.println(Arrays.toString(a));
    System.out.println(Arrays.toString(r));
}

int[] reverseArray(int[] b) {

    int[] c = new int[b.length];

    for (int i = b.length - 1, j = 0; i &gt;= 0; i--, j++) {

        c[j] = b[i];
    }

    return c;
}
</pre>

<p>
The example reorders the elements of an array. For this task, a
<code>reverseArray</code> method is created.
</p>

<pre class="explanation">
int[] reverseArray(int[] b) {
</pre>

<p>
The <code>reverseArray</code> method takes an array as a parameter and returns
an array. The method takes a copy of the passed array.
</p>

<pre class="explanation">
int[] c = new int[b.length];
</pre>

<p>
Inside the body of the method, a new array is created; it will contain the newly
ordered elements.
</p>

<pre class="explanation">
for (int i = b.length - 1, j = 0; i &gt;= 0; i--, j++) {

    c[j] = b[i];
}
</pre>

<p>
In this for loop, we fill the new array with the elements of the copied array.
The elements are reversed.
</p>

<pre class="explanation">
return c;
</pre>

<p>
The newly formed array is returned back to the caller.
</p>

<pre class="explanation">
System.out.println(Arrays.toString(a));
System.out.println(Arrays.toString(r));
</pre>

<p>
We print the elements of the original and the reversed array.
</p>

<pre class="compact">
$ java Main.java
[3, 4, 5, 6, 7]
[7, 6, 5, 4, 3]
</pre>


<h2>Multidimensional arrays</h2>

<p>
So far we have been working with one-dimensional arrays. In Java, we can create
multidimensional arrays. A multidimensional array is an array of arrays. In such
an array, the elements are themselves arrays. In multidimensional arrays, we use
two or more sets of brackets.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    int[][] twodim = new int[][] { { 1, 2, 3 }, { 1, 2, 3 } };

    int d1 = twodim.length;
    int d2 = twodim[1].length;

    for (int i = 0; i &lt; d1; i++) {

        for (int j = 0; j &lt; d2; j++) {

            System.out.println(twodim[i][j]);
        }
    }
}
</pre>

<p>
In this example, we create a two-dimensional array of integers.
</p>

<pre class="explanation">
int[][] twodim = new int[][] { { 1, 2, 3 }, { 1, 2, 3 } };
</pre>

<p>
Two pairs of square brackets are used to declare a two-dimensional array. Inside
the curly brackets, we have additional two pairs of curly brackets. They
represent two inner arrays.
</p>

<pre class="explanation">
int d1 = twodim.length;
int d2 = twodim[1].length;
</pre>

<p>
We determine the length of the outer array that
holds other two arrays and the second inner array.
</p>

<pre class="explanation">
for (int i = 0; i &lt; d1; i++) {

    for (int j = 0; j &lt; d2; j++) {

        System.out.println(twodim[i][j]);
    }
}
</pre>

<p>
Two for loops are used to print all the six values from the two-dimensional
array. The first index of the <code>twodim[i][j]</code> array refers to one of
the inner arrays. The second index refers to the element of the chosen inner
array.
</p>

<pre class="compact">
$ java Main.java
1
2
3
1
2
3
</pre>


<p>
In a similar fashion, we create a three-dimensional array of
integers.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    int[][][] n3 = {
            { { 12, 2, 8 }, { 0, 2, 1 } },
            { { 14, 5, 2 }, { 0, 5, 4 } },
            { { 3, 26, 9 }, { 8, 7, 1 } },
            { { 4, 11, 2 }, { 0, 9, 6 } }
    };

    int d1 = n3.length;
    int d2 = n3[0].length;
    int d3 = n3[0][0].length;

    for (int i = 0; i &lt; d1; i++) {

        for (int j = 0; j &lt; d2; j++) {

            for (int k = 0; k &lt; d3; k++) {

                System.out.print(n3[i][j][k] + " ");
            }
        }
    }
}
</pre>

<p>
A variable that holds a three-dimensional array is declared with three pairs of
square brackets. The values are place inside three pairs of curly brackets.
</p>

<pre class="explanation">
int[][][] n3 = {
    { { 12, 2, 8 }, { 0, 2, 1 } },
    { { 14, 5, 2 }, { 0, 5, 4 } },
    { { 3, 26, 9 }, { 8, 7, 1 } },
    { { 4, 11, 2 }, { 0, 9, 6 } }
};
</pre>

<p>
Three-dimensional array <code>n3</code> is created. It is an array that has
elements which are themselves arrays of arrays.
</p>

<pre class="explanation">
int d1 = n3.length;
int d2 = n3[0].length;
int d3 = n3[0][0].length;
</pre>

<p>
We get the length of all three dimensions.
</p>

<pre class="explanation">
for (int i = 0; i &lt; d1; i++) {

    for (int j = 0; j &lt; d2; j++) {

        for (int k = 0; k &lt; d3; k++) {

            System.out.print(n3[i][j][k] + " ");
        }
    }
}
</pre>

<p>
We need three for loops to traverse a three dimensional array.
</p>

<pre class="compact">
$ java Main.java
12 2 8 0 2 1 14 5 2 0 5 4 3 26 9 8 7 1 4 11 2 0 9 6
</pre>


<h2>Irregular arrays</h2>

<p>
Arrays that have elements of the same size are called rectangular arrays. It is
possible to create irregular arrays where the arrays have a different size. In
C# such arrays are called <em>jagged arrays</em>.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
void main() {

    int[][] ir = new int[][] {
            { 1, 2 },
            { 1, 2, 3 },
            { 1, 2, 3, 4 }
    };

    for (int[] a : ir) {
        for (int e : a) {
            System.out.print(e + " ");
        }
    }
}
</pre>

<p>
This is an example of an irregular array.
</p>

<pre class="explanation">
int[][] ir = new int[][] {
        { 1, 2 },
        { 1, 2, 3 },
        { 1, 2, 3, 4 }
};
</pre>

<p>
This is a declaration and initialization of an irregular array. The three inner
arrays have 2, 3, and 4 elements.
</p>

<pre class="explanation">
for (int[] a : ir) {
    for (int e : a) {
        System.out.print(e + " ");
    }
}
</pre>

<p>
The enhanced for loop is used to go through all the
elements of the array.
</p>

<pre class="compact">
$ java Main.java
1 2 1 2 3 1 2 3 4
</pre>


<h2>Array methods</h2>

<p>
The <code>Arrays</code> class, available in the <code>java.util</code>
package, is a helper class that contains methods for working with arrays. These
methods can be used for modifying, sorting, copying, or searching data. These
methods that we use are static methods of the <code>Array</code> class. (Static
methods are methods that can be called without creating an instance of a class.)
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] a = { 5, 2, 4, 3, 1 };

    Arrays.sort(a);

    System.out.println(Arrays.toString(a));

    Arrays.fill(a, 8);
    System.out.println(Arrays.toString(a));

    int[] b = Arrays.copyOf(a, 5);

    if (Arrays.equals(a, b)) {

        System.out.println("Arrays a, b are equal");
    } else {

        System.out.println("Arrays a, b are not equal");
    }
}
</pre>

<p>
In the code example, we present five methods of the <code>Arrays</code> class.
</p>

<pre class="explanation">
import java.util.Arrays;
</pre>

<p>
We will use the shorthand notation for the <code>Arrays</code> class.
</p>

<pre class="explanation">
int[] a = { 5, 2, 4, 3, 1 };
</pre>

<p>
We have an array of five integers.
</p>

<pre class="explanation">
Arrays.sort(a);
</pre>

<p>
The <code>sort</code> method sorts the integers in an ascending order.
</p>

<pre class="explanation">
System.out.println(Arrays.toString(a));
</pre>

<p>
The <code>toString</code> method returns a string representation
of the contents of the specified array.
</p>

<pre class="explanation">
Arrays.fill(a, 8);
</pre>

<p>
The <code>fill</code> method assigns the specified integer value to
each element of the array.
</p>

<pre class="explanation">
int[] b = Arrays.copyOf(a, 5);
</pre>

<p>
The <code>copyOf</code> method copies the specified number of elements
to a new array.
</p>

<pre class="explanation">
if (Arrays.equals(a, b)) {

    System.out.println("Arrays a, b are equal");
} else {

    System.out.println("Arrays a, b are not equal");
}
</pre>

<p>
The <code>equals</code> method compares the two arrays. Two arrays are equal
if they contain the same elements in the same order.
</p>

<pre class="compact">
$ java Main.java
[1, 2, 3, 4, 5]
[8, 8, 8, 8, 8]
Arrays a, b are equal
</pre>


<h2>Comparing arrays</h2>

<p>
There are two methods for comparing arrays. The <code>equals</code> method and
the <code>deepEquals</code> method. The <code>deepEquals</code> method
also compares references to arrays inside arrays.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    int[] a = { 1, 1, 2, 1, 1 };
    int[] b = { 0, 0, 3, 0, 0 };

    int[][] c = {
            { 1, 1, 2, 1, 1 },
            { 0, 0, 3, 0, 0 }
    };

    int[][] d = {
            a,
            b
    };

    System.out.print("equals() method: ");

    if (Arrays.equals(c, d)) {

        System.out.println("Arrays c, d are equal");
    } else {

        System.out.println("Arrays c, d are not equal");
    }

    System.out.print("deepEquals() method: ");

    if (Arrays.deepEquals(c, d)) {

        System.out.println("Arrays c, d are equal");
    } else {

        System.out.println("Arrays c, d are not equal");
    }
}
</pre>

<p>
The example explains the difference between the two methods.
</p>

<pre class="explanation">
int[] a = { 1, 1, 2, 1, 1 };
int[] b = { 0, 0, 3, 0, 0 };
</pre>

<p>
We have two arrays of integers.
</p>

<pre class="explanation">
int[][] c = {
    { 1, 1, 2, 1, 1 },
    { 0, 0, 3, 0, 0 }
};
</pre>

<p>
The c array has two inner arrays. The elements of the inner arrays are equal
to the <code>a</code> and <code>b</code> arrays.
</p>

<pre class="explanation">
int[][] d = {
    a,
    b
};
</pre>

<p>
The <code>d</code> array contains references to <code>a</code> and
<code>b</code> arrays.
</p>

<pre class="explanation">
System.out.print("equals() method: ");

if (Arrays.equals(c, d)) {

    System.out.println("Arrays c, d are equal");
} else {

    System.out.println("Arrays c, d are not equal");
}

System.out.print("deepEquals() method: ");

if (Arrays.deepEquals(c, d)) {

    System.out.println("Arrays c, d are equal");
} else {

    System.out.println("Arrays c, d are not equal");
}
</pre>

<p>
Now the <code>c</code> and <code>d</code> arrays are compared using both
methods. For the <code>equals</code> method, the arrays are not equal. The
<code>deepEquals</code> method goes deeper in the referenced arrays and
retrieves their elements for comparison. For this method, the <code>c</code> and
<code>d</code> arrays are equal.
</p>

<pre class="compact">
$ java Main.java
equals() method: Arrays c, d are not equal
deepEquals() method: Arrays c, d are equal
</pre>


<h2>Searching arrays</h2>

<p>
The <code>Arrays</code> class has a simple method for searching elements in an
array. It is called the <code>binarySearch</code>. The method searches for
elements using a binary search algorithm. The <code>binarySearch</code> method
only works on sorted arrays.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Arrays;

void main() {

    String[] planets = { "Mercury", "Venus", "Mars", "Earth", "Jupiter",
            "Saturn", "Uranus", "Neptune", "Pluto" };

    Arrays.sort(planets);

    String p = "Earth";
    int r = Arrays.binarySearch(planets, p);

    String msg = "";

    if (r &gt;= 0) {
        msg = STR."\{p} was found at position \{r} of the sorted array";
    } else {
        msg = STR."\{p} was not found";
    }

    System.out.println(msg);
}
</pre>

<p>
In the example, we search for the "Earth" string in an array of planets.
</p>

<pre class="explanation">
Arrays.sort(planets);
</pre>

<p>
Since the algorithm only works on sorted arrays, we must sort the array first.
</p>

<pre class="explanation">
String p = "Earth";
</pre>

<p>
We will be searching for the "Earth" element.
</p>

<pre class="explanation">
int r = Arrays.binarySearch(planets, p);
</pre>

<p>
The <code>binarySearch</code> method is called. The first parameter is the array
name, the second the element we are looking for. If the element is found, the
return value is greater or equal to zero. In such a case, it is the index of the
element in the sorted array.
</p>

<pre class="explanation">
if (r &gt;= 0) {
    msg = STR."\{p} was found at position \{r} of the sorted array";
} else {
    msg = STR."\{p} was not found";
}
</pre>

<p>
Depending on the returned value, we create a message.
</p>

<pre class="compact">
$ java Main.java
Earth was found at position 0 of the sorted array
</pre>


<h2>Download image</h2>

<p>
In the next example, we show how to download an image.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URI;
import java.net.URISyntaxException;

void main() throws IOException, URISyntaxException {

    String imageUrl = "https://something.com/favicon.ico";
    String destinationFile = "favicon.ico";

    var url = new URI(imageUrl).toURL();

    try (var is = url.openStream();
            var fos = new FileOutputStream(destinationFile)) {

        byte[] buf = new byte[1024];
        int noOfBytes;

        while ((noOfBytes = is.read(buf)) != -1) {

            fos.write(buf, 0, noOfBytes);
        }
    }
}
</pre>

<p>
The example downloads a small <code>favicon.ico</code> image.
</p>

<pre class="explanation">
byte[] buf = new byte[1024];
</pre>

<p>
An image is an array of bytes. We create an empty array of <code>byte</code>
values big enough to hold the icon.
</p>

<pre class="explanation">
while ((noOfBytes = is.read(buf)) != -1) {

    fos.write(buf, 0, noOfBytes);
}
</pre>

<p>
We read the binary data and write it to the file.
</p>




</html>

