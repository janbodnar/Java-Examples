
<h1>Java enum type</h1>

 
<p>
In this article we show how to work with enum type in Java.
</p>

<p>
An <dfn>enum type</dfn> is built-in Java data type that defines a fixed set of
named constants. The set of constants cannot be changed afterwards. Variables
having an enum type can be assigned any of the enumerators as a value. 
</p>

<p>
The enum type provides a more robust and readable way to handle constant values
compared to using primitive data types like integers. Enemerations enforce type
safety by guaranteeing that the variable can only hold one of the predefined
values.
</p>


<p>
We should use enum types any time we need to represent a fixed set of constants.
There are many natural enum types such as the planets in our solar system,
seasons, or days of week. These are data sets where we know all possible values
at compile time.
</p>

<pre class="compact">
public enum Size {
    SMALL, MEDIUM, LARGE
}
</pre>

<p>
We use the <code>enum</code> keyword to define an enumeration in Java. It is 
a good programming practice to name the constants with uppercase letters.
</p>

<h2>Simple example</h2>

<p>
We have a simple code example with an enumeration.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}

void main() {

    Day day = Day.MONDAY;

    if (day == Day.MONDAY) {

        System.out.println("It is Monday");
    }

    System.out.println(day);

    for (Day d : Day.values()) {

        System.out.println(d);
    }
}
</pre>

<p>
We define the <code>Day</code> enum that represents a fixed set of seven 
day names. 
</p>

<pre class="explanation">
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}
</pre>

<p>
An enum type is created with the <code>enum</code> keyword. By convention,
constants are written in uppercase letters.
</p>

<pre class="explanation">
Day day = Day.MONDAY;
</pre>

<p>
We have a variable called day which is of enumerated type <code>Day</code>. It
is initialized to <code>Day.Monday</code>.
</p>

<pre class="explanation">
for (Day d : Day.values()) {

    System.out.println(d);
}
</pre>

<p>
This loop prints all days to the console. The <code>values</code> method returns
an array containing the constants of this enum type, in the order they are
declared. This method may be used to iterate over the constants with the
enhanced for statement. The enhanced for goes through the array, element by
element, and prints them to the terminal.
</p>

<pre class="compact">
$ java Main.java
It is Monday
MONDAY
MONDAY
TUESDAY
WEDNESDAY
THURSDAY
FRIDAY
SATURDAY
SUNDAY
</pre>


<h2>Providing values to enum constants</h2>

<p>
We can explicitly provide some values to the enumeration constants.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
enum Season {

    SPRING(10),
    SUMMER(20),
    AUTUMN(30),
    WINTER(40);

    private int value;

    private Season(int value) {
        this.value = value;
    }

    public int getValue() {

        return value;
    }
}

void main() {

    for (Season season : Season.values()) {

        System.out.println(STR."\{season} \{season.getValue()}");
    }
}
</pre>

<p>
The example contains a <code>Season</code> enumeration which has four constants.
</p>

<pre class="explanation">
SPRING(10),
SUMMER(20),
AUTUMN(30),
WINTER(40);
</pre>

<p>
Here we define four constants of the enum. The constants are given specific values.
</p>

<pre class="compact">
$ java Main.java
SPRING 10
SUMMER 20
AUTUMN 30
WINTER 40
</pre>


<h2>Toss a coin</h2>

<p>
Enumeration is a type of a class. We can define our own methods.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Random;

public enum Coin {
    HEADS,
    TAILS;

    public static Coin toss() {

        var rand = new Random();
        int rdx = rand.nextInt(Coin.values().length);
        return Coin.values()[rdx];
    }
}

void main() {

    for (int i = 1; i &lt;= 15; i++) {

        System.out.print(STR."\{Coin.toss()} ");
    }
}
</pre>

<p>
The example defines the <code>toss</code> method, which randomly chooses one 
of the constants: <code>HEADS</code> or <code>TAILS</code>. Later in the for loop 
we call <code>toss</code> fifteen times.
</p>

<pre class="compact">
$ java Main.java
HEADS TAILS HEADS TAILS HEADS HEADS TAILS HEADS HEADS HEADS TAILS TAILS HEADS TAILS TAILS 
</pre>


<h2>Enum type with switch expressions</h2>

<p>
Enums can be effectively used with switch expressions.
</p>

<div class="codehead">Main.java
  <i class="fas fa-copy copy-icon" onclick="copyCode(this)"></i>
</div>
<pre class="code">
import java.util.Random;

void main() {

    Season season = Season.randomSeason();

    String msg = switch (season) {

        case Season.SPRING -&gt; "Spring";
        case Season.SUMMER -&gt; "Summer";
        case Season.AUTUMN -&gt; "Autumn";
        case Season.WINTER -&gt; "Winter";
    };

    System.out.println(msg);
}

enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER;

    public static Season randomSeason() {
        
        var random = new Random();
        int ridx = random.nextInt(Season.values().length);
        return Season.values()[ridx];
    }
}
</pre>

<p>
We define a <code>Season</code> enumeration. The enumeration contains a
<code>randomSeason</code> method which creates a <code>Season</code> value
randomly. Depending on the chosen value, we print a message.
</p>

<pre class="explanation">
var msg = switch (season) {

    case Season.Spring -&gt; "Spring";
    case Season.Summer -&gt; "Summer";
    case Season.Autumn -&gt; "Autumn";
    case Season.Winter -&gt; "Winter";
};

System.out.println(msg);
</pre>

<p>
We check the value against the switch expression. The expression returns the
string representation of the enum. Since the compiler knows all the possible
constants beforehand, the switch expression is exhaustive, that is, we do not
have to define the <code>default</code> arm.
</p>




</body>
</html>
