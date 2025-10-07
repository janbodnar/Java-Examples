
<h1>Java basics</h1>


 
<p>
In this article we cover some basic programming concepts of the Java language.
We begin with some simple programs. We work with variables, constants, and basic
data types. We read and write to console and we also mention string formatting.
</p>


<h2>Java simple example</h2>

<p>
We start with a very simple code example. The following code is placed into the
<code>Simple.java</code> file. The naming is important here. A public class of a
Java program must match the name of the file.
</p>

<div class="codehead">com/zetcode/Simple.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Simple {

    public static void main(String[] args) {

        System.out.println("This is Java");
    }
}
</pre>

<p>
Java code is strictly organized from the very beginning. A file of a Java code
may have one or more classes, out of which only one can be declared public.
</p>

<pre class="explanation">
package com.zetcode;
</pre>

<p>
Packages are used to organize Java classes into groups, which usually share
similar functionality. Packages are similar to namespaces and modules in other
programming languages. For a simple code example, a package declaration may
be omitted. This will create a so called <em>default package</em>. However, in
this tutorial we use a package for all examples. Another important thing is that
a directory structure must reflect the package name. In our case the source file
<code>Simple.java</code> with a package <code>com.zetcode</code> must be placed into
a directory named <code>com/zetcode/</code>. The <code>package</code> statement must
be the first line in the source file.
</p>

<pre class="explanation">
public class Simple {

   ...
}
</pre>

<p>
A class is a basic building block of a Java program. The
<code>public</code> keyword gives unrestricted access to this class. The above
code is a class definition. The definition has a body that starts with a left
curly brace { and ends with a right curly brace }. Only one class can be
declared <code>public</code> in a source file. 
</p>

<p>
Also note the name of the class. Its name must match the file name. The source
file is called <code>Simple.java</code> and the class <code>Simple</code>. It is
a convention that the names of classes start with an uppercase letter.
</p>

<pre class="explanation">
public static void main(String[] args) {
    ...
}
</pre>

<p>
The <code>main</code> is a method. A method is a piece of code created to do a
specific job. Instead of putting all code into one place, we divide it into
pieces called methods. This brings modularity to our application. Each method
has a body in which we place statements. The body of a method is enclosed by
curly brackets. The specific job for the <code>main</code> method is to start
the application. It is the entry point to each console Java program.
</p>

<p>
The method is declared to be <code>static</code>. This static method can be
called without the need to create an instance of the Java class. First we need
to start the application and after that we are able to create instances of
classes. The <code>void</code> keyword states that the method does not return a
value. Finally, the <code>public</code> keyword makes the <code>main</code>
method available to the outer world without restrictions. These topics will be
later explained in more detail.
</p>

<pre class="explanation">
System.out.println("This is Java");
</pre>

<p>
In the <code>main</code> method, we put one statement. The statement prints the
"This is Java", which is a string literal, to the console. Each statement must
be finished with a semicolon <code>;</code> character. This statement is a
method call. We call the <code>println</code> method of the <code>System</code>
class. The class represents the standard input, output, and error streams for
console applications. We specify the fully qualified name of the
<code>println</code> method.
</p>

<pre class="compact">
$ java Simple.java
This is Java
</pre>

<p>
We execute the program with the <code>java</code> tool. 
</p>

<div class="note">
<strong>Note: </strong> We execute the (single) source file with 
java tool. This feature was added in Java 11.
</div>


<h2>Java console reading values</h2>

<p>
The second example will show, how to read a value from a console.
</p>

<div class="codehead">com/zetcode/ReadLine.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

import java.util.Scanner;

public class ReadLine {

    public static void main(String[] args) {

        System.out.print("Write your name:");

        Scanner sc = new Scanner(System.in);
        String name = sc.nextLine();

        System.out.println("Hello " + name);
    }
}
</pre>

<p>
A prompt is shown on the terminal window. The user writes his name on the
terminal and the value is read and printed back to the terminal.
</p>

<pre class="explanation">
import java.util.Scanner;
</pre>

<p>
The Java standard library has a huge collection of classes available for
programmers. They are organized inside packages. The <code>Scanner</code> class
is one of them. When we import a class with the <code>import</code> keyword, we
can refer later to the class without the full package name. Otherwise, we must
use the fully qualified name. The <code>import</code> allows a shorthand
referring for classes. This is different from some other languages. For instance
in Python, the import keyword imports objects into the namespace of a script. In
Java, the <code>import</code> keyword only saves typing by allowing to refer to
types without specifying the full name.
</p>

<pre class="explanation">
System.out.print("Write your name:");
</pre>

<p>
We print a message to the user. We use the <code>print</code> method which does
not start a new line. The user then types his response next to the message.
</p>

<pre class="explanation">
Scanner sc = new Scanner(System.in);
</pre>

<p>
A new instance of the  <code>Scanner</code> class is created. New objects are
created with the <code>new</code> keyword. The constructor of the object follows
the <code>new</code> keyword. We put one parameter to the constructor of the
<code>Scanner</code> object. It is the standard input stream. This way we are
ready to read from the terminal. The <code>Scanner</code> is a simple text
scanner which can parse primitive types and strings.
</p>

<pre class="explanation">
String name = sc.nextLine();
</pre>

<p>
Objects have methods which perform certain tasks. The <code>nextLine</code>
method reads the next line from the terminal. It returns the result in a
<code>String</code> data type. The returned value is stored in the name
variable which we declare to be of <code>String</code> type.
</p>

<pre class="explanation">
System.out.println("Hello " + name);
</pre>

<p>
We print a message to the terminal. The message consists of two parts. The
"Hello " string and the name variable. We concatenate these two values into one
string using the <code>+</code> operator. This operator can concatenate two or
more strings.
</p>

<pre class="compact">
$ java ReadLine.java
Write your name:John Doe
Hello John Doe
</pre>

<p>
This is a sample execution of the second program.
</p>


<h2>Java command line arguments</h2>

<p>
Java programs can receive command line arguments. They follow the name of the
program when we run it.
</p>

<div class="codehead">com/zetcode/CommandLineArgs.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class CommandLineArgs {

    public static void main(String[] args) {

        for (String arg : args) {

            System.out.println(arg);
        }
    }
}
</pre>

<p>
Command line arguments can be passed to the <code>main</code> method.
</p>

<pre class="explanation">
public static void main(String[] args)
</pre>

<p>
The <code>main</code> method receives a string array of command line arguments.
Arrays are collections of data. An array is declared by a type followed by a
pair of square brackets <code>[]</code>. So the <code>String[] args</code>
construct declares an array of strings. The <code>args</code> is an parameter to
the <code>main</code> method. The method then can work with parameters which are
passed to it.
</p>

<pre class="explanation">
for (String arg : args) {

    System.out.println(arg);
}
</pre>

<p>
We go through the array of these arguments with a for loop and print them to the
console. The for loop consists of cycles. In this case, the number of cycles
equals to the number of parameters in the array. In each cycle, a new element is
passed to the <code>arg</code> variable from the <code>args</code> array. The
loop ends when all elements of the array were passed. The for statement has a
body enclosed by curly brackets <code>{}</code>. In this body, we place
statements that we want to be executed in each cycle. In our case, we simply
print the value of the <code>arg</code> variable to the terminal. Loops and
arrays will be described in more detail later.
</p>

<pre class="compact">
$ java CommandLineArgs.java 1 2 3 4 5
1
2
3
4
5
</pre>

<p>
We provide four numbers as command line arguments and these are
printed to the console.
</p>

<p>
When we launch programs from the command line, we specify the arguments right
after the name of the program. In Integrated Development Environments (IDE) such
as IntelliJ IDEA, we specify these parameters in a dialog. In IntelliJ IDEA, we 
select Edit configurations and add the values into the Program arguments option.
</p>




<h2>Java variables</h2>

<p>
A variable is a place to store data. A variable has a name and a data type. A
data type determines what values can be assigned to the variable. Integers,
strings, boolean values etc. Over the time of the program, variables can obtain
various values of the same data type. Variables in Java are always initialized
to the default value of their type before any reference to the variable can be
made.
</p>

<div class="codehead">com/zetcode/Variables.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Variables {

    public static void main(String[] args) {

        String city = "New York";
        String name = "Paul"; int age = 34;
        String nationality = "American";

        System.out.println(city);
        System.out.println(name);
        System.out.println(age);
        System.out.println(nationality);

        city = "London";
        System.out.println(city);
    }
}
</pre>

<p>
In the above example, we work with four variables. Three of the variables are
strings. The <code>age</code> variable is an integer. The <code>int</code>
keyword is used to declare an integer variable.
</p>

<pre class="explanation">
String city = "New York";
</pre>

<p>
We declare a city variable of the string type and initialize it to the "New
York" value.
</p>

<pre class="explanation">
String name = "Paul"; int age = 34;
</pre>

<p>
We declare and initialize two variables. We can put two statements into one
line. Since each statement is finished with a semicolon, the Java compiler knows
that there are two statements in one line. But for readability reasons, each
statement should be on a separate line.
</p>

<pre class="explanation">
System.out.println(city);
System.out.println(name);
System.out.println(age);
System.out.println(nationality);
</pre>

<p>
We print the values of the variables to the terminal.
</p>

<pre class="explanation">
city = "London";
System.out.println(city);
</pre>

<p>
We assign a new value to the city variable and later print it.
</p>

<pre class="compact">
$ java Variables.java
New York
Paul
34
American
London
</pre>


<h2>The var keyword</h2>

<p>
Since Java 10 for local variables with initializers we can use the
<code>var</code> keyword instead of the data type. The data type will be
inferred from the right side of the declaration.
</p>

<div class="codehead">com/zetcode/VarKeyword.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class VarKeyword {

    public static void main(String[] args) {

        var name = "John Doe";
        var age = 34;

        System.out.println(name + " is " + age  + " years old");
    }
}
</pre>

<p>
In the example, we use the <code>var</code> keyword for two variables.
</p>

<pre class="explanation">
var name = "John Doe";
var age = 34;
</pre>

<p>
We have one string variable and one integer variable. The data type is inferred
by the compiler from the right side of the declaration. For the inference to
work, the variables must be initialized.
</p>


<h2>Java constants</h2>

<p>
Unlike variables, constants cannot change their initial values. Once
initialized, they cannot be modified. Constants are created with the
<code>final</code> keyword.
</p>

<div class="codehead">com/zetcode/Constants.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Constants {

    public static void main(String[] args) {

        final int WIDTH = 100;
        final int HEIGHT = 150;
        int var = 40;

        var = 50;

        //WIDTH = 110;
    }
}
</pre>

<p>
In this example, we declare two constants and one variable.
</p>

<pre class="explanation">
final int WIDTH = 100;
final int HEIGHT = 150;
</pre>

<p>
We use the <code>final</code> keyword to inform the compiler that we
declare a constant. It is a convention to write constants in uppercase letters.
</p>

<pre class="explanation">
int var = 40;

var = 50;
</pre>

<p>
We declare and initialize a variable. Later, we assign a new value
to the variable. It is legal.
</p>

<pre class="explanation">
// WIDTH = 110;
</pre>

<p>
Assigning new values to constants is not possible. If we uncomment this line, we
will get a compilation error: "Uncompilable source code - cannot assign a value
to final variable WIDTH".
</p>


<h2>Java string formatting</h2>

<p>
Building strings from variables is a very common task in programming. Java
language has the  <code>String.format</code> method to format strings.
</p>

<p>
Some dynamic languages like Perl, PHP, or Ruby support variable interpolation.
<em>Variable interpolation</em> is replacing variables with their values inside
string literals. Java language does not allow this. It has string formatting
instead.
</p>

<div class="codehead">com/zetcode/StringFormatting.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class StringFormatting {

    public static void main(String[] args) {

        int age = 34;
        String name = "William";

        String output = String.format("%s is %d years old.", name, age);

        System.out.println(output);
    }
}
</pre>

<p>
In Java, strings are immutable. We cannot modify an existing string. We must
create a new string from existing strings and other types. In the code example,
we create a new string. We also use values from two variables.
</p>

<pre class="explanation">
int age = 34;
String name = "William";
</pre>

<p>
Here we have two variables, one integer and one string.
</p>

<pre class="explanation">
String output = String.format("%s is %d years old.", name, age);
</pre>

<p>
We use the <code>format</code> method of the built-in String class. The
<code>%s</code> and <code>%d</code> are control characters which are later
evaluated. The <code>%s</code> accepts string values, the <code>%d</code>
integer values.
</p>






