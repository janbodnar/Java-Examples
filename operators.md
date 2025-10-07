<h1>Java operator</h1>

<p>
An <em>operator</em> is a special symbol which indicates a certain process is
carried out. Operators in programming languages are taken from mathematics.
Programmers work with data. The operators are used to process data. An
<em>operand</em> is one of the inputs (arguments) of an operator.
</p>

<p>
Expressions are constructed from operands and operators. The operators of an
expression indicate which operations to apply to the operands. The order of
evaluation of operators in an expression is determined by the
<em>precedence</em> and <em>associativity</em> of the operators.
</p>

<p>
An operator usually has one or two operands. Those operators that work with only
one operand are called <em>unary operators</em>. Those who work with two
operands are called <em>binary operators</em>. There is also one ternary
operator <code>?:</code> which works with three operands.
</p>

<p>
Certain operators may be used in different contexts. For example the
<code>+</code> operator. It can be used in different cases. It adds numbers,
concatenates strings, or indicates the sign of a number. We say that the
operator is <em>overloaded</em>.
</p>


<h2>Java sign operators</h2>

<p>
There are two sign operators: <code>+</code> and <code>-</code>. They are used
to indicate or change the sign of a value.
</p>

<div class="codehead">com/zetcode/SignOperators.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class SignOperators {

    public static void main(String[] args) {

        System.out.println(2);
        System.out.println(+2);
        System.out.println(-2);
    }
}
</pre>

<p>
The <code>+</code> and <code>-</code> signs indicate the sign of a value.
The plus sign can be used to signal that we have a positive number. It
can be omitted and it is mostly done so.
</p>

<div class="codehead">com/zetcode/MinusSign.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class MinusSign {

    public static void main(String[] args) {

        int a = 1;

        System.out.println(-a);
        System.out.println(-(-a));
    }
}
</pre>

<p>
The minus sign changes the sign of a value.
</p>


<h2>Java assignment operator</h2>

<p>
The assignment operator <code>=</code> assigns a value to a variable. A
<em>variable</em> is a placeholder for a value. In mathematics, the = operator
has a different meaning. In an equation, the <code>=</code> operator is an
equality operator. The left side of the equation is equal to the right one.
</p>

<pre class="compact">
int x = 1;
</pre>

<p>
Here we assign a number to the <code>x</code> variable.
</p>

<pre class="compact">
x = x + 1;
</pre>

<p>
This expression does not make sense in mathematics, but it is legal in
programming. The expression adds 1 to the x variable. The right side is equal to
2 and 2 is assigned to x.
</p>

<pre class="compact">
3 = x;
</pre>

<p>
This code line results in syntax error. We cannot assign a value to a literal.
</p>


<h2>Java concatenating strings</h2>

<p>
In Java the + operator is also used to concatenate strings.
</p>

<div class="codehead">com/zetcode/ConcatenateStrings.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class ConcatenateStrings {

    public static void main(String[] args) {

        System.out.println("Return " + "of " + "the king.");
        System.out.println("Return".concat(" of").concat(" the king."));
    }
}
</pre>

<p>
We join three strings together.
</p>

<pre class="explanation">
System.out.println("Return " + "of " + "the king.");
</pre>

<p>
Strings are joined with the <code>+</code> operator.
</p>

<pre class="explanation">
System.out.println("Return".concat(" of").concat(" the king."));
</pre>

<p>
An alternative method for concatenating strings is the <code>concat</code>
method.
</p>

<pre class="compact">
$ java ConcatenateStrings.java
Return of the king.
Return of the king.
</pre>


<h2>Java increment and decrement operators</h2>

<p>
Incrementing or decrementing a value by one is a common task in
programming. Java has two convenient operators for this: <code>++</code>
and <code>--</code>.
</p>

<pre class="compact">
x++;
x = x + 1;
...
y--;
y = y - 1;
</pre>

<p>
The above two pairs of expressions do the same.
</p>

<div class="codehead">com/zetcode/IncDec.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class IncDec {

    public static void main(String[] args) {

        int x = 6;

        x++;
        x++;

        System.out.println(x);

        x--;
        System.out.println(x);
    }
}
</pre>

<p>
In the above example, we demonstrate the usage of both operators.
</p>

<pre class="explanation">
int x = 6;

x++;
x++;
</pre>

<p>
We initiate the <code>x</code> variable to 6. Then we increment
<code>x</code> two times. Now the variable equals to 8.
</p>

<pre class="explanation">
x--;
</pre>

<p>
We use the decrement operator. Now the variable equals to 7.
</p>

<pre class="compact">
$ java IncDec.java
8
7
</pre>

<p>
And here is the output of the example.
</p>


<h2>Java arithmetic operators</h2>

<p>
The following is a table of arithmetic operators in Java.
</p>

<table>
<tr>
<th>Symbol</th><th>Name</th>
</tr>
<tr><td><code>+</code></td><td>Addition</td></tr>
<tr><td><code>-</code></td><td>Subtraction</td></tr>
<tr><td><code>*</code></td><td>Multiplication</td></tr>
<tr><td><code>/</code></td><td>Division</td></tr>
<tr><td><code>%</code></td><td>Remainder</td></tr>
</table>


<p>
The following example shows arithmetic operations.
</p>

<div class="codehead">com/zetcode/Arithmetic.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Arithmetic {

    public static void main(String[] args) {

        int a = 10;
        int b = 11;
        int c = 12;

        int add = a + b + c;
        int sb = c - a;
        int mult = a * b;
        int div = c / 3;
        int rem = c % a;

        System.out.println(add);
        System.out.println(sb);
        System.out.println(mult);
        System.out.println(div);
        System.out.println(rem);
    }
}
</pre>

<p>
In the preceding example, we use addition, subtraction, multiplication,
division, and remainder operations. This is all familiar from the mathematics.
</p>

<pre class="explanation">
int rem = c % a;
</pre>

<p>
The <code>%</code> operator is called the remainder or the modulo operator.
It finds the remainder of division of one number by another. For example,
<code>9 % 4</code>, 9 modulo 4 is 1, because 4 goes into 9 twice with a
remainder of 1.
</p>

<pre class="compact">
$ java Arithmetic.java
33
2
110
4
2
</pre>


<p>
Next we show the distinction between integer and floating
point division.
</p>

<div class="codehead">com/zetcode/Division.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Division {

    public static void main(String[] args) {

        int c = 5 / 2;
        System.out.println(c);

        double d = 5 / 2.0;
        System.out.println(d);
    }
}
</pre>

<p>
In the preceding example, we divide two numbers.
</p>

<pre class="explanation">
int c = 5 / 2;
</pre>

<p>
In this code, we have done integer division. The returned value of the division
operation is an integer. When we divide two integers the result is an integer.
</p>

<pre class="explanation">
double d = 5 / 2.0;
</pre>

<p>
If one of the values is a double or a float, we perform a floating point
division. In our case, the second operand is a double so the result is a double.
</p>

<pre class="compact">
$ java Division.java
2
2.5
</pre>

<p>
We see the result of the program.
</p>


<h2>Java Boolean operators</h2>

<p>
In Java we have three logical operators. The <code>boolean</code> keyword
is used to declare a Boolean value.
</p>

<table>
<tr>
<th>Symbol</th><th>Name</th>
</tr>
<tr><td><code>&amp;&amp;</code></td><td>logical and</td></tr>
<tr><td><code>||</code></td><td>logical or</td></tr>
<tr><td><code>!</code></td><td>negation</td></tr>
</table>

<p>
Boolean operators are also called logical.
</p>

<div class="codehead">com/zetcode/BooleanOperators.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class BooleanOperators {

    public static void main(String[] args) {

        int x = 3;
        int y = 8;

        System.out.println(x == y);
        System.out.println(y &gt; x);

        if (y &gt; x) {

            System.out.println("y is greater than x");
        }
    }
}
</pre>

<p>
Many expressions result in a boolean value. For instance, boolean values are
used in conditional statements.
</p>

<pre class="explanation">
System.out.println(x == y);
System.out.println(y &gt; x);
</pre>

<p>
Relational operators always result in a boolean value. These two lines
print false and true.
</p>

<pre class="explanation">
if (y &gt; x) {

    System.out.println("y is greater than x");
}
</pre>

<p>
The body of the <code>if</code> statement is executed only if the condition
inside the parentheses is met. The <code>y > x</code> returns true, so the message
"y is greater than x" is printed to the terminal.
</p>

<p>
The <code>true</code> and <code>false</code> keywords represent
boolean literals in Java.
</p>

<div class="codehead">com/zetcode/AndOperator.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class AndOperator {

    public static void main(String[] args) {

        boolean a = true &amp;&amp; true;
        boolean b = true &amp;&amp; false;
        boolean c = false &amp;&amp; true;
        boolean d = false &amp;&amp; false;

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
        System.out.println(d);
    }
}
</pre>

<p>
The code example shows the logical and (&amp;&amp;) operator.
It evaluates to true only if both operands are true.
</p>

<pre class="compact">
$ java AndOperator.java
true
false
false
false
</pre>

<p>
Only one expression results in <code>true</code>.
</p>

<p>
The logical or (<code>||</code>) operator evaluates to <code>true</code>
if either of the operands is true.
</p>

<div class="codehead">com/zetcode/OrOperator.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class OrOperator {

    public static void main(String[] args) {

        boolean a = true || true;
        boolean b = true || false;
        boolean c = false || true;
        boolean d = false || false;

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
        System.out.println(d);
    }
}
</pre>

<p>
If one of the sides of the operator is true, the outcome of
the operation is true.
</p>

<pre class="compact">
$ java OrOperator.java
true
true
true
false
</pre>

<p>
Three of four expressions result in <code>true</code>.
</p>

<p>
The negation operator <code>!</code> makes true false and false true.
</p>

<div class="codehead">com/zetcode/Negation.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Negation {

    public static void main(String[] args) {

        System.out.println(! true);
        System.out.println(! false);
        System.out.println(! (4 &lt; 3));
    }
}
</pre>

<p>
The example shows the negation operator in action.
</p>

<pre class="compact">
$ java Negation.java
false
true
true
</pre>


<p>
The <code>||</code>, and <code>&amp;&amp;</code> operators are short circuit
evaluated. <em>Short circuit evaluation</em> means that the second argument is
only evaluated if the first argument does not suffice to determine the value of
the expression: when the first argument of the logical and evaluates to false,
the overall value must be false; and when the first argument of logical or
evaluates to true, the overall value must be true. Short circuit evaluation is
used mainly to improve performance.
</p>

<p>
An example may clarify this a bit more.
</p>

<div class="codehead">com/zetcode/ShortCircuit.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class ShortCircuit {

    public static boolean One() {

        System.out.println("Inside one");
        return false;
    }

    public static boolean Two() {

        System.out.println("Inside two");
        return true;
    }

    public static void main(String[] args) {

        System.out.println("Short circuit");

        if (One() &amp;&amp; Two()) {

            System.out.println("Pass");
        }

        System.out.println("#############");

        if (Two() || One()) {

            System.out.println("Pass");
        }
    }
}
</pre>

<p>
We have two methods in the example. They are used as operands
in boolean expressions. We will see if they are called.
</p>

<pre class="explanation">
if (One() &amp;&amp; Two()) {

    System.out.println("Pass");
}
</pre>

<p>
The <code>One</code> method returns false. The short circuit &amp;&amp; does not
evaluate the second method. It is not necessary. Once an operand is false, the
result of the logical conclusion is always false. Only "Inside one" is only
printed to the console.
</p>

<pre class="explanation">
if (Two() || One()) {

    System.out.println("Pass");
}
</pre>

<p>
In the second case, we use the <code>||</code> operator and use the
<code>Two</code> method as the first operand. In this case, "Inside two" and
"Pass" strings are printed to the terminal. It is again not necessary to
evaluate the second operand, since once the first operand evaluates to true, the
logical or is always true.
</p>

<pre class="compact">
$ java ShortCircuit.java
Short circuit
Inside one
#############
Inside two
Pass
</pre>

<p>
We see the result of the program.
</p>


<h2>Java relational operators</h2>

<p>
Relational operators are used to compare values. These operators always
result in a boolean value.
</p>

<table>
<tr>
<th>Symbol</th><th>Meaning</th>
</tr>
<tr><td><code>&lt;</code></td><td>less than</td></tr>
<tr><td><code>&lt;=</code></td><td>less than or equal to</td></tr>
<tr><td><code>&gt;</code></td><td>greater than</td></tr>
<tr><td><code>&gt;=</code></td><td>greater than or equal to</td></tr>
<tr><td><code>==</code></td><td>equal to</td></tr>
<tr><td><code>!=</code></td><td>not equal to</td></tr>
</table>

<p>
Relational operators are also called comparison operators.
</p>

<div class="codehead">com/zetcode/Relational.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Relational {

    public static void main(String[] args) {

        System.out.println(3 &lt; 4);
        System.out.println(3 == 4);
        System.out.println(4 &gt;= 3);
        System.out.println(4 != 3);
    }
}
</pre>

<p>
In the code example, we have four expressions. These expressions compare
integer values. The result of each of the expressions is either true or false.
In Java we use the <code>==</code> to compare numbers. (Some languages like
Ada, Visual Basic, or Pascal use <code>=</code> for comparing numbers.)
</p>




<h2>Java bitwise operators</h2>

<p>
Decimal numbers are natural to humans. Binary numbers are native to computers.
Binary, octal, decimal, or hexadecimal symbols are only notations of a number.
Bitwise operators work with bits of a binary number. Bitwise operators are
seldom used in higher level languages like Java.
</p>

<table>
<tr>
<th>Symbol</th><th>Meaning</th>
</tr>
<tr><td><code>~</code></td><td>bitwise negation</td></tr>
<tr><td><code>^</code></td><td>bitwise exclusive or</td></tr>
<tr><td><code>&amp;</code></td><td>bitwise and</td></tr>
<tr><td><code>|</code></td><td>bitwise or</td></tr>
</table>

<p>
The <em>bitwise negation operator</em> changes each 1 to 0 and 0 to 1.
</p>

<pre class="compact">
System.out.println(~7); // prints -8
System.out.println(~ -8); // prints 7
</pre>

<p>
The operator reverts all bits of a number 7. One of the bits also determines
whether the number is negative or not. If we negate all the bits one more time,
we get number 7 again.
</p>

<p>
The <em>bitwise and operator</em> performs bit-by-bit comparison between two
numbers. The result for a bit position is 1 only if both corresponding bits in
the operands are 1.
</p>

<pre class="compact">
      00110
   &amp;  00011
   =  00010
</pre>

<p>
The first number is a binary notation of 6, the second is 3 and the result is 2.
</p>

<pre class="compact">
System.out.println(6 &amp; 3); // prints 2
System.out.println(3 &amp; 6); // prints 2
</pre>

<p>
The <em>bitwise or operator</em> performs bit-by-bit comparison between
two numbers. The result for a bit position is 1 if either of the
corresponding bits in the operands is 1.
</p>

<pre class="compact">
     00110
   | 00011
   = 00111
</pre>

<p>
The result is <code>00110</code> or decimal 7.
</p>

<pre class="compact">
System.out.println(6 | 3); // prints 7
System.out.println(3 | 6); // prints 7
</pre>

<p>
The <em>bitwise exclusive or operator</em> performs bit-by-bit comparison
between two numbers. The result for a bit position is 1 if one or the
other (but not both) of the corresponding bits in the operands is 1.
</p>

<pre class="compact">
      00110
   ^  00011
   =  00101
</pre>

<p>
The result is <code>00101</code> or decimal 5.
</p>

<pre class="compact">
System.out.println(6 ^ 3); // prints 5
System.out.println(3 ^ 6); // prints 5
</pre>


<h2>Java compound assignment operators</h2>

<p>
<dfn>Compound assignment operators</dfn> are shorthand operators which
consist of two operators.
<p>

<pre class="compact">
a = a + 3;
a += 3;
</pre>

<p>
The <code>+=</code> compound operator is one of these shorthand operators.
The above two expressions are equal. Value 3 is added to the
a variable.
</p>

<p>
Other compound operators are:
</p>

<pre class="compact">
-=   *=   /=   %=   &amp;=   |=   &lt;&lt;=   &gt;&gt;=
</pre>

<p>
The following example uses two compound operators.
</p>

<div class="codehead">com/zetcode/CompoundOperators.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class CompoundOperators {

    public static void main(String[] args) {

        int a = 1;
        a = a + 1;

        System.out.println(a);

        a += 5;
        System.out.println(a);

        a *= 3;
        System.out.println(a);
    }
}
</pre>

<p>
We use the <code>+=</code> and <code>*=</code> compound operators.
</p>

<pre class="explanation">
int a = 1;
a = a + 1;
</pre>

<p>
The <code>a</code> variable is initiated to one. Value 1 is added to the
variable using the non-shorthand notation.
</p>

<pre class="explanation">
a += 5;
</pre>

<p>
Using a <code>+=</code> compound operator, we add 5 to the a variable.
The statement is equal to <code>a = a + 5;</code>.
</p>

<pre class="explanation">
a *= 3;
</pre>

<p>
Using the <code>*=</code> operator, the a is multiplied by 3. The statement
is equal to <code>a = a * 3;</code>.
</p>

<pre class="compact">
$ java CompoundOperators.java
2
7
21
</pre>


<h2>Java instanceof operator</h2>

<p>
The <code>instanceof</code> operator compares an object to a specified type.
</p>

<div class="codehead">com/zetcode/InstanceofOperator.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

class Base {}
class Derived extends Base {}

public class InstanceofOperator {

    public static void main(String[] args) {

        Base b = new Base();
        Derived d = new Derived();

        System.out.println(d instanceof Base);
        System.out.println(b instanceof Derived);
        System.out.println(d instanceof Object);
    }
}
</pre>

<p>
In the example, we have two classes: one base and one derived from
the base.
</p>

<pre class="explanation">
System.out.println(d instanceof Base);
</pre>

<p>
This line checks if the variable <code>d</code> points to the class that is an
instance of the <code>Base</code> class. Since the <code>Derived</code>
class inherits from the <code>Base</code> class, it is also an instance of the
<code>Base</code> class too. The line prints true.
</p>

<pre class="explanation">
System.out.println(b instanceof Derived);
</pre>

<p>
The <code>b</code> object is not an instance of the <code>Derived</code> class.
This line prints false.
</p>

<pre class="explanation">
System.out.println(d instanceof Object);
</pre>

<p>
Every class has <code>Object</code> as a superclass. Therefore, the
<code>d</code> object is also an instance of the <code>Object</code> class.
</p>

<pre class="compact">
$ java InstanceofOperator.java
true
false
true
</pre>


<h2>Java lambda operator</h2>

<p>
Java 8 introduced the lambda operator (<code>-&gt;</code>).
</p>

<pre class="compact">
(parameters) -&gt; expression
(parameters) -&gt; { statements; }
</pre>

<p>
This is the basic syntax for a lambda expression in Java. Lambda expression
allow to create more concise code in Java.
</p>

<p>
The declaration of the type of the parameter is optional; the compiler can infer
the type from the value of the parameter. For a single parameter the parentheses
are optional; for multiple parameters, they are required. 
</p>

<p>
The curly braces are optional if there is only one statement in an expression
body. Finally, the return keyword is optional if the body has a single
expression to return a value; curly braces are required to indicate that the
expression returns a value.
</p>

<div class="codehead">com/zetcode/LambdaExpression.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

import java.util.Arrays;

public class LambdaExpression {

    public static void main(String[] args) {

        String[] words = { "kind", "massive", "atom", "car", "blue" };

        Arrays.sort(words, (String s1, String s2) -&gt; (s1.compareTo(s2)));

        System.out.println(Arrays.toString(words));
    }
}
</pre>

<p>
In the example, we define an array of strings. The array is sorted using
the <code>Arrays.sort</code> method and a lambda expression.
</p>

<pre class="compact">
$ java LambdaExpression.java
[atom, blue, car, kind, massive]
</pre>


<p>
Lambda expressions are used primarily to define an inline implementation of a
functional interface, i.e., an interface with a single method only.
Interfaces are abstract types that are used to enforce a contract.
</p>

<div class="codehead">com/zetcode/LambdaExpression2.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

interface GreetingService {

    void greet(String message);
}

public class LambdaExpression2 {

    public static void main(String[] args) {

        GreetingService gs = (String msg) -&gt; {
            System.out.println(msg);
        };

        gs.greet("Good night");
        gs.greet("Hello there");
    }
}
</pre>

<p>
In the example, we create a greeting service with the help
of a lambda expression.
</p>

<pre class="explanation">
interface GreetingService {

    void greet(String message);
}
</pre>

<p>
Interface <code>GreetingService</code> is created. All objects implementing
this interface must implement the <code>greet</code> method.
</p>

<pre class="explanation">
GreetingService gs = (String msg) -&gt; {
    System.out.println(msg);
};
</pre>

<p>
We create an object that implements <code>GreetingService</code> with
a lambda expression. The object has a method that prints a message to the console.
</p>

<pre class="explanation">
gs.greet("Good night");
</pre>

<p>
We call the object's <code>greet</code> method, which prints a give message
to the console.
</p>

<pre class="compact">
$ java LambdaExpression2.java
Good night
Hello there
</pre>


<p>
There are some common functional interfaces, such as <code>Function</code>,
<code>Consumer</code>, or <code>Supplier</code>.
</p>

<div class="codehead">com/zetcode/LambdaExpression3.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

import java.util.function.Function;

public class LambdaExpression3 {

    public static void main(String[] args) {

        Function&lt;Integer, Integer&gt; square = (Integer x) -&gt; x * x;
        System.out.println(square.apply(5));
    }
}
</pre>

<p>
The example uses a lambda expression to compute squares of integers.
</p>

<pre class="explanation">
Function&lt;Integer, Integer&gt; square = (Integer x) -&gt; x * x;
System.out.println(square.apply(5));
</pre>

<p>
<code>Function</code> is a function that accepts one argument and produces a
result. The operation of the lamda expression produces a square of the given
integer.
</p>


<h2>Java double colon operator</h2>

<p>
The double colon operator (::) is used to create a reference to a method.
</p>

<div class="codehead">com/zetcode/DoubleColonOperator.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

import java.util.function.Consumer;

public class DoubleColonOperator {

    private static void greet(String msg) {

        System.out.println(msg);
    }

    public static void main(String[] args) {

        Consumer&lt;String&gt; f = DoubleColonOperator::greet;
        f.accept("Hello there");
    }
}
</pre>

<p>
In the code example, we create a reference to a static method
with the double colon operator.
</p>

<pre class="explanation">
private static void greet(String msg) {

    System.out.println(msg);
}
</pre>

<p>
We have a static method that prints a greeting to the console.
</p>

<pre class="explanation">
Consumer&lt;String&gt; f = DoubleColonOperator::greet;
</pre>

<p>
<code>Consumer</code> is a functional interface that represents an
operation that accepts a single input argument and returns no result.
With the double colon operator, we create a reference to the
<code>greet</code> method.
</p>

<pre class="explanation">
f.accept("Hello there");
</pre>

<p>
We perform the functional operation with the <code>accept</code> method.
</p>


<h2>Java operator precedence</h2>

<p>
The <em>operator precedence</em> tells us which operators are evaluated first.
The precedence level is necessary to avoid ambiguity in expressions.
</p>

<p>
What is the outcome of the following expression, 28 or 40?
</p>

<pre class="compact">
3 + 5 * 5
</pre>

<p>
Like in mathematics, the multiplication operator has a higher precedence than
addition operator. So the outcome is 28.
</p>

<pre class="compact">
(3 + 5) * 5
</pre>

<p>
To change the order of evaluation, we can use parentheses. Expressions inside
parentheses are always evaluated first. The result of the above expression is
40.
</p>


<h2>Java operators precedence list</h2>

<p>
The following table shows common Java operators ordered by
precedence (highest precedence first):
</p>

<table>
  <tr>
    <th>Operator</th>
    <th>Meaning</th>
    <th>Associativity</th>
  </tr>
  <tr>
    <td><code>[] () .</code></td>
    <td>array access, method invoke, object member access</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>++ -- + -</code></td>
    <td>increment, decrement, unary plus and minus</td>
    <td>Right-to-left</td>
  </tr>
  <tr>
    <td><code>! ~ (type) new</code></td>
    <td>negation, bitwise NOT, type cast, object creation</td>
    <td>Right-to-left</td>
  </tr>
  <tr>
    <td><code>* / %</code></td>
    <td>multiplication, division, modulo</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>+ - </code></td>
    <td>addition, subtraction</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>+</code></td>
    <td>string concatenation</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>&lt;&lt; &gt;&gt; &gt;&gt;&gt;</code></td>
    <td>shift</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>&lt; &lt;= &gt; &gt;=</code></td>
    <td>relational</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>instanceof</code></td>
    <td>type comparison</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>== !=</code></td>
    <td>equality</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>&amp;</code></td>
    <td>bitwise AND</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>^</code></td>
    <td>bitwise XOR</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>|</code></td>
    <td>bitwise OR</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>&amp;&amp;</code></td>
    <td>logical AND</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>||</code></td>
    <td>logical OR</td>
    <td>Left-to-right</td>
  </tr>
  <tr>
    <td><code>? :</code></td>
    <td>ternary</td>
    <td>Right-to-left</td>
  </tr>
  <tr>
    <td><code>=</code></td>
    <td>simple assignment</td>
    <td>Right-to-left</td>
  </tr>
  <tr>
    <td><code>+= -=  *= /= %=  &amp;=</code></td>
    <td>compound assignment</td>
    <td>Right-to-left</td>
  </tr>
  <tr>
    <td><code>^=  |= &lt;&lt;= &gt;&gt;= &gt;&gt;&gt;=</code></td>
    <td>compound assignment</td>
    <td>Right-to-left</td>
  </tr>
</table>

<div class="figure">Table: Operator precedence and associativity</div>

<p>
Operators on the same row of the table have the same precedence. If we use
operators with the same precedence, then the associativity rule is applied.
</p>

<div class="codehead">com/zetcode/Precedence.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Precedence {

    public static void main(String[] args) {

        System.out.println(3 + 5 * 5);
        System.out.println((3 + 5) * 5);

        System.out.println(! true | true);
        System.out.println(! (true | true));
    }
}
</pre>

<p>
In this code example, we show a few expressions.
The outcome of each expression is dependent on the precedence level.
</p>

<pre class="explanation">
System.out.println(3 + 5 * 5);
</pre>

<p>
This line prints 28. The multiplication operator has a higher precedence
than addition. First, the product of <code>5*5</code> is calculated,
then 3 is added.
</p>

<pre class="explanation">
System.out.println(! true | true);
</pre>

<p>
In this case, the negation operator has a higher precedence than the
bitwise OR. First, the initial true value is negated to false, then the
<code>|</code> operator combines false and true, which gives true in the end.
</p>

<pre class="compact">
$ java Precedence.java
28
40
true
false
</pre>


<h2>Java associativity rule</h2>

<p>
Sometimes the precedence is not satisfactory to determine the outcome
of an expression. There is another rule called
<em>associativity</em>. The associativity of operators determines
the order of evaluation of operators with the same precedence level.
</p>

<pre class="compact">
9 / 3 * 3
</pre>

<p>
What is the outcome of this expression, 9 or 1? The multiplication, deletion,
and the modulo operator are left to right associated. So the expression is
evaluated this way: <code>(9 / 3) * 3</code> and the result is 9.
</p>

<p>
Arithmetic, boolean, relational, and bitwise operators are all left to right
associated. The assignment operators, ternary operator, increment, decrement,
unary plus and minus, negation, bitwise NOT, type cast, object creation
operators are right to left associated.
</p>

<div class="codehead">com/zetcode/Associativity.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class Associativity {

    public static void main(String[] args) {

        int a, b, c, d;
        a = b = c = d = 0;

        String str = String.format("%d %d %d %d", a, b, c, d);
        System.out.println(str);

        int j = 0;
        j *= 3 + 1;
        System.out.println(j);
    }
}
</pre>

<p>
In the example, we have two cases where the associativity rule determines the
expression.
</p>

<pre class="explanation">
int a, b, c, d;
a = b = c = d = 0;
</pre>

<p>
The assignment operator is right to left associated. If the associativity was
left to right, the previous expression would not be possible.
</p>

<pre class="explanation">
int j = 0;
j *= 3 + 1;
</pre>

<p>
The compound assignment operators are right to left associated. We might expect
the result to be 1. But the actual result is 0. Because of the associativity.
The expression on the right is evaluated first and then the compound assignment
operator is applied.
</p>

<pre class="compact">
$ java Associativity.java
0 0 0 0
0
</pre>


<h2>Java ternary operator</h2>

<p>
The ternary operator <code>?:</code> is a conditional operator. It is a
convenient operator for cases where we want to pick up one of two values,
depending on the conditional expression.
</p>

<pre class="compact">
cond-exp ? exp1 : exp2
</pre>

<p>
If cond-exp is true, exp1 is evaluated and the result is returned. If the
cond-exp is false, exp2 is evaluated and its result is returned.
</p>

<div class="codehead">com/zetcode/TernaryOperator.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class TernaryOperator {

    public static void main(String[] args) {

        int age = 31;

        boolean adult = age >= 18 ? true : false;

        System.out.println(String.format("Adult: %s", adult));
    }
}
</pre>

<p>
In most countries the adulthood is based on the age. You are adult if you are
older than a certain age. This is a situation for a ternary operator.
</p>

<pre class="explanation">
boolean adult = age >= 18 ? true : false;
</pre>

<p>
First the expression on the right side of the assignment operator is evaluated.
The first phase of the ternary operator is the condition expression evaluation.
So if the age is greater or equal to 18, the value following the <code>?</code>
character is returned. If not, the value following the <code>:</code> character
is returned. The returned value is then assigned to the adult variable.
</p>

<pre class="compact">
$ java TernaryOperator.java
Adult: true
</pre>

<p>
A 31 years old person is adult.
</p>


<h2>Calculating prime numbers</h2>

<p>
In the following example, we are going to calculate prime numbers.
</p>

<div class="codehead">com/zetcode/PrimeNumbers.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
package com.zetcode;

public class PrimeNumbers {

    public static void main(String[] args) {

        int[] nums = { 0, 1, 2, 3, 4, 5, 6, 7, 8,
            9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
            19, 20, 21, 22, 23, 24, 25, 26, 27, 28 };

        System.out.print("Prime numbers: ");

        for (int num : nums) {

            if (num == 0 || num == 1) {
                continue;
            }

            if (num == 2 || num == 3) {

                System.out.print(num + " ");
                continue;
            }

            int i = (int) Math.sqrt(num);

            boolean isPrime = true;

            while (i &gt; 1) {

                if (num % i == 0) {

                    isPrime = false;
                }

                i--;
            }

            if (isPrime) {

                System.out.print(num + " ");
            }
        }

        System.out.print('\n');
    }
}
</pre>

<p>
In the above example, we deal with several operators. A prime number (or a
prime) is a natural number that has exactly two distinct natural number
divisors: 1 and itself. We pick up a number and divide it by numbers from 1 to
the selected number. Actually, we do not have to try all smaller numbers; we can
divide by numbers up to the square root of the chosen number. The formula will
work. We use the remainder division operator.
</p>

<pre class="explanation">
int[] nums = { 0, 1, 2, 3, 4, 5, 6, 7, 8,
    9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
    19, 20, 21, 22, 23, 24, 25, 26, 27, 28 };
</pre>

<p>
We will calculate primes from these numbers.
</p>

<pre class="explanation">
if (num == 0 || num == 1) {
    continue;
}
</pre>

<p>
Values 0 and 1 are not considered to be primes.
</p>

<pre class="explanation">
if (num == 2 || num == 3) {

    System.out.print(num + " ");
    continue;
}
</pre>

<p>
We skip the calculations for 2 and 3. They are primes. Note the usage of the
equality and conditional or operators. The <code>==</code> has a higher
precedence than the <code>||</code> operator. So we do not need to use parentheses.
</p>

<pre class="explanation">
int i = (int) Math.sqrt(num);
</pre>

<p>
We are OK if we only try numbers smaller than the square root of
a number in question.
</p>

<pre class="explanation">
while (i &gt; 1) {
    ...
    i--;
}
</pre>

<p>
This is a while loop. The <code>i</code> is the calculated square root
of the number. We use the decrement operator to decrease <code>i</code>
by one each loop cycle. When i is smaller than 1, we terminate the loop.
For example, we have number 9. The square root of 9 is 3. We will divide
the 9 number by 3 and 2. This is sufficient for our calculation.
</p>

<pre class="explanation">
if (num % i == 0) {

    isPrime = false;
}
</pre>

<p>
If the remainder division operator returns 0 for any of the i values,
then the number in question is not a prime.
</p>



</html>

