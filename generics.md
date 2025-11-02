# Java Generics

Generics are a powerful feature in Java that enable types (classes and  
interfaces) to be parameters when defining classes, interfaces, and methods.  
They provide a way to write flexible, reusable code that can work with  
different types while maintaining compile-time type safety. Generics were  
introduced in Java 5 to eliminate the need for casting and to provide  
stronger type checks at compile time.  

The primary purpose of generics is to enable programmers to write more  
general-purpose code without sacrificing type safety. Before generics,  
collections and other generic data structures used `Object` as the element  
type, requiring explicit casting and offering no compile-time type checking.  
This often led to `ClassCastException` errors at runtime. Generics solve this  
problem by allowing you to specify the exact type of elements a collection  
can hold, moving type checking from runtime to compile time.  

Generics work through a mechanism called type erasure. During compilation,  
generic type information is erased and replaced with actual types (usually  
`Object` for unbounded types). This ensures backward compatibility with  
pre-generics Java code. However, it also means that generic type information  
is not available at runtime, which has important implications for how  
generics can be used with arrays and reflection.  

The generic syntax uses angle brackets `<>` to specify type parameters. By  
convention, type parameter names are single uppercase letters: `T` for type,  
`E` for element, `K` for key, `V` for value, and `N` for number. Generic  
types can be bounded using `extends` keyword to restrict the types that can  
be used as type arguments. Wildcards (`?`) provide additional flexibility  
when working with unknown types in method parameters and return values.  

Java generics support variance through bounded wildcards: upper bounds using  
`? extends Type` for covariance (read-only scenarios) and lower bounds using  
`? super Type` for contravariance (write-only scenarios). Understanding these  
concepts is crucial for writing flexible APIs and working effectively with  
Java's collections framework, which makes extensive use of generics.  


## Generic method with Consumer

This example demonstrates creating a generic method that accepts a type  
parameter and uses it with functional interfaces.  



```java

void main() {

  var data = List.of(1, 2, 3, 4, 5, 6, 7);

  // Consumer<Integer> consumer = (Integer x) -> IO::println(x);
  Consumer<Integer> consumer = IO::println;
  forEach(data, consumer);

  IO.println("--------------------------");
  forEach(data, IO::println);

  IO.println("--------------------------");
  
  var words = List.of("sky", "mark", "better", "rock");
  forEach(words, IO::println);
}

<T> void forEach(List<T> data, Consumer<T> consumer) {

  for (T t : data) {
    consumer.accept(t);
  }
}
```
The `forEach` method is a generic method that can work with any type `T`. It  
takes a `List<T>` and a `Consumer<T>` functional interface to process each  
element. The type parameter `<T>` before the return type indicates this is a  
generic method. The compiler infers the type from the arguments, allowing the  
same method to work with integers, strings, or any other type. Method  
references like `IO::println` can be used as consumers for concise code.  


## Generic method with mapping function

This example shows a generic method that transforms an array to a list using  
a mapping function.  



```java
void main() {

  Integer[] vals = { 2, 4, 6, 8, 10, 12 };
  Float[] vals2 = { 2.4f, 4.2f, 6.1f, 8.4f, 10.2f, 12.1f };

  var myList = mapArrayToList(vals, e -> e * e);
  System.out.println(myList);

  var myList2 = mapArrayToList(vals2, e -> e * e);
  System.out.println(myList2);
}

<T, R> List<R> mapArrayToList(T[] a, Function<T, R> mapFun) {

  return Arrays.stream(a).map(mapFun).collect(Collectors.toList());
}
```
The `mapArrayToList` method demonstrates using multiple type parameters. It  
takes an array of type `T` and transforms it to a `List<R>` using a  
`Function<T, R>`. This shows how generics enable writing highly reusable code  
that works with different input and output types. The method uses streams to  
apply the mapping function and collect results into a list. The compiler  
infers both `T` and `R` from the method arguments and return type context.  


## Bounded type parameters with multiple bounds

This example demonstrates using bounded type parameters that must satisfy  
multiple interface constraints.  



```java

interface Item {

  String info();
}

interface Plant {

  String getColor();
}

class Bike implements Item {

  @Override
  public String info() {

    return "This is a bike";
  }
}

class Chair implements Item {

  @Override
  public String info() {

    return "This is a chair";
  }
}

class Flower implements Item, Plant {

  private String color;

  public Flower(String color) {
    this.color = color;
  }

  public void setColor(String color) {
    this.color = color;
  }

  @Override
  public String getColor() {
    return this.color;
  }

  @Override
  public String info() {

    return String.format("This is %s flower", this.color);
  }
}

// Generic bounded example

void main() {

  Chair chair = new Chair();
  doInform2(chair);

  Flower flower = new Flower("red");
  doInform(flower);
}

<T extends Item & Plant> void doInform(T item) {

  System.out.println(item.info());
}

<T extends Item> void doInform2(T item) {

  System.out.println(item.info());
}
```
This example shows bounded type parameters using the `extends` keyword. The  
`doInform` method requires a type that implements both `Item` and `Plant`  
interfaces using `<T extends Item & Plant>`. This ensures the parameter has  
all methods from both interfaces. The `doInform2` method shows a single bound  
with `<T extends Item>`. Bounded type parameters enable generic methods to  
call specific methods on their parameters, not just `Object` methods.  


## Varargs with generics

This example demonstrates using varargs (variable arguments) with generic  
methods to accept multiple lists.  



```java

void main() {

  var vals1 = List.of(1, 2, 3);
  var vals2 = List.of(4, 5, 6);
  var vals3 = List.of(7, 8, 9);

  var vals = concatenate(vals1, vals2, vals3);

  IO.println(vals);

  var words1 = List.of("pen", "paper", "ink");
  var words2 = List.of("sky", "cloud", "wind");
  var words3 = List.of("tree", "forest", "wood");

  var words = concatenate(words1, words2, words3);

  IO.println(words);
}

@SafeVarargs
final <T> List<T> concatenate(List<T>... lists) {
  return new ArrayList<>() {
    {

      for (List<T> mylist : lists) {

        addAll(mylist);
      }
    }
  };
}
```
The `concatenate` method accepts multiple lists using varargs `List<T>...`  
and combines them into a single list. The `@SafeVarargs` annotation  
suppresses compiler warnings about potential heap pollution when using  
generic varargs. The method uses an anonymous `ArrayList` subclass with an  
instance initializer block to add all elements from all input lists. This  
pattern is useful for combining collections of the same generic type.  


## Generic method for set union

This example shows a generic method that performs set union operations on any  
element type.  



```java
class Car {

  private String name;
  private int price;

  public Car(String name, int price) {
    this.name = name;
    this.price = price;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getPrice() {
    return price;
  }

  public void setPrice(int price) {
    this.price = price;
  }

  @Override
  public String toString() {
    return "Car{" + "name=" + name + ", price=" + price + '}';
  }

  @Override
  public int hashCode() {
    int hash = 5;
    hash = 79 * hash + Objects.hashCode(this.name);
    hash = 79 * hash + this.price;
    return hash;
  }

  @Override
  public boolean equals(Object obj) {
    if (this == obj) {
      return true;
    }
    if (obj == null) {
      return false;
    }
    if (getClass() != obj.getClass()) {
      return false;
    }
    final Car other = (Car) obj;
    if (this.price != other.price) {
      return false;
    }
    return Objects.equals(this.name, other.name);
  }

}

// Generic method

void main() {

  Set<String> words = new HashSet<>();
  words.add("blue");
  words.add("pen");
  words.add("dog");
  words.add("narrow");

  Set<String> words2 = new HashSet<>();
  words.add("blue");
  words.add("pencil");
  words.add("forest");
  words.add("narrow");

  Set<String> res = union(words, words2);
  IO.println(res);

  Set<Car> cars = new HashSet<>();
  cars.add(new Car("Volvo", 23144));
  cars.add(new Car("Mazda", 20500));
  cars.add(new Car("Mercedes", 50000));

  Set<Car> cars2 = new HashSet<>();
  cars.add(new Car("Volvo", 23144));
  cars.add(new Car("Mazda", 20500));
  cars.add(new Car("Skoda", 9800));

  Set<Car> res2 = union(cars, cars2);
  res2.forEach(IO::println);

}

<E> Set<E> union(Set<E> s1, Set<E> s2) {

  Set<E> result = new HashSet<>(s1);
  result.addAll(s2);

  return result;
}
```
The `union` method is a generic method that creates a union of two sets. The  
type parameter `E` ensures both input sets and the result set have the same  
element type. The method works with any type that properly implements  
`equals` and `hashCode` methods, as shown with both `String` and custom `Car`  
objects. This demonstrates how generics enable writing reusable algorithms  
that work with different data types while maintaining type safety.  


## Generic method for random selection

This example demonstrates a generic method that selects a random element from  
a list.  



```java

void main() {

  var words = List.of("rock", "sky", "blue", "ocean", "falcon");
  var vals = List.of(2, 3, 4, 5, 6, 7, 8);

  var e1 = getRandomElement(words);
  IO.println(e1);

  var e2 = getRandomElement(vals);
  IO.println(e2);
}

<T> T getRandomElement(List<T> list) {

  var random = new Random();
  int idx = random.nextInt(list.size());
  return list.get(idx);
}
```
The `getRandomElement` method demonstrates a simple generic method that  
returns a value of the generic type `T`. It generates a random index and  
returns the element at that position. The return type matches the list's  
element type, ensuring type safety. This method works with lists of any type,  
whether strings, integers, or custom objects. The compiler ensures the  
returned value matches the expected type at the call site.  


## Wildcards with upper bounds

This example shows using wildcard types with upper bounds to accept lists of  
subclasses.  



```java
abstract class Shape {

  abstract void draw();
}

class Rectangle extends Shape {

  @Override
  void draw() {
    IO.println("Drawing rectangle");
  }
}

class Circle extends Shape {

  @Override
  void draw() {
    IO.println("Drawing circle");
  }
}

// Generic wildcard example
void main() {

  List<Rectangle> shapes1 = new ArrayList<>();
  shapes1.add(new Rectangle());

  List<Circle> shapes2 = new ArrayList<>();
  shapes2.add(new Circle());
  shapes2.add(new Circle());

  drawShapes(shapes1);
  drawShapes(shapes2);
}

void drawShapes(List<? extends Shape> lists) {

  for (Shape s : lists) {
    s.draw();
  }
}
```
The `drawShapes` method uses a bounded wildcard `? extends Shape` to accept  
lists of any type that extends `Shape`. This demonstrates covariance - the  
method can accept `List<Rectangle>`, `List<Circle>`, or `List<Shape>`. The  
wildcard makes the method more flexible than `List<Shape>` alone, which would  
not accept lists of subtypes. This is useful for read-only operations where  
you need to process elements polymorphically without adding new elements.  


## Basic generic class

This example demonstrates creating a simple generic class that can hold any  
type of value.  

```java
class Box<T> {

  private T content;

  public void set(T content) {
    this.content = content;
  }

  public T get() {
    return content;
  }

  public boolean isEmpty() {
    return content == null;
  }
}

void main() {

  var intBox = new Box<Integer>();
  intBox.set(42);
  IO.println("Integer box: " + intBox.get());

  var strBox = new Box<String>();
  strBox.set("Hello Generics");
  IO.println("String box: " + strBox.get());

  var doubleBox = new Box<Double>();
  IO.println("Is empty: " + doubleBox.isEmpty());
}
```
The `Box<T>` class is a simple generic container that can hold any type. The  
type parameter `T` is specified when creating an instance, determining what  
type of objects the box can hold. This eliminates the need for casting and  
provides compile-time type safety. The same class definition works for  
integers, strings, doubles, or any other type, demonstrating the reusability  
benefit of generics.  


## Generic class with multiple type parameters

This example shows a generic class with two type parameters for key-value  
pairs.  

```java
class Pair<K, V> {

  private K key;
  private V value;

  public Pair(K key, V value) {
    this.key = key;
    this.value = value;
  }

  public K getKey() {
    return key;
  }

  public V getValue() {
    return value;
  }

  @Override
  public String toString() {
    return key + "=" + value;
  }
}

void main() {

  var p1 = new Pair<String, Integer>("age", 25);
  IO.println(p1);

  var p2 = new Pair<Integer, String>(1, "first");
  IO.println(p2);

  var p3 = new Pair<String, List<Integer>>("numbers", List.of(1, 2, 3));
  IO.println(p3.getKey() + ": " + p3.getValue());
}
```
The `Pair<K, V>` class demonstrates using multiple type parameters. `K`  
represents the key type and `V` represents the value type. Each can be any  
type independently, allowing flexible combinations like `String` keys with  
`Integer` values or vice versa. This pattern is commonly used in map entries  
and other paired data structures. The example also shows nesting generics  
with `Pair<String, List<Integer>>`.  


## Generic interface

This example demonstrates creating and implementing a generic interface.  

```java
interface Container<T> {

  void add(T item);
  T get(int index);
  int size();
}

class SimpleList<T> implements Container<T> {

  private List<T> items = new ArrayList<>();

  @Override
  public void add(T item) {
    items.add(item);
  }

  @Override
  public T get(int index) {
    return items.get(index);
  }

  @Override
  public int size() {
    return items.size();
  }
}

void main() {

  Container<String> words = new SimpleList<>();
  words.add("apple");
  words.add("banana");
  words.add("cherry");

  for (int i = 0; i < words.size(); i++) {
    IO.println(words.get(i));
  }
}
```
Generic interfaces allow defining contracts that work with any type. The  
`Container<T>` interface defines methods for adding and retrieving items of  
type `T`. The `SimpleList<T>` class implements this interface, specifying the  
same type parameter. When creating an instance, the type parameter is  
specified (e.g., `Container<String>`), ensuring all methods work with that  
specific type throughout the object's lifetime.  


## Generic method in non-generic class

This example shows defining generic methods in regular (non-generic) classes.  

```java
class Utils {

  static <T> void printArray(T[] array) {
    for (T element : array) {
      IO.print(element + " ");
    }
    IO.println();
  }

  static <T> T firstElement(T[] array) {
    return array.length > 0 ? array[0] : null;
  }

  static <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
  }
}

void main() {

  Integer[] numbers = {5, 2, 8, 1, 9};
  Utils.printArray(numbers);
  IO.println("First: " + Utils.firstElement(numbers));
  IO.println("Max: " + Utils.max(5, 10));

  String[] words = {"apple", "banana", "cherry"};
  Utils.printArray(words);
  IO.println("First: " + Utils.firstElement(words));
  IO.println("Max: " + Utils.max("apple", "banana"));
}
```
Generic methods can be defined in non-generic classes by specifying the type  
parameter before the return type. The `Utils` class shows three generic  
methods: `printArray` works with any type, `firstElement` returns the  
appropriate type, and `max` uses a bounded type parameter requiring  
`Comparable`. Static generic methods are particularly useful for utility  
functions that work across different types.  


## Bounded type parameter with Comparable

This example demonstrates using bounded type parameters to ensure types  
support comparison.  

```java
class MinMax<T extends Comparable<T>> {

  private T min;
  private T max;

  public MinMax(T first) {
    min = max = first;
  }

  public void update(T value) {
    if (value.compareTo(min) < 0) {
      min = value;
    }
    if (value.compareTo(max) > 0) {
      max = value;
    }
  }

  public T getMin() {
    return min;
  }

  public T getMax() {
    return max;
  }
}

void main() {

  var intMinMax = new MinMax<>(5);
  intMinMax.update(2);
  intMinMax.update(8);
  intMinMax.update(1);
  intMinMax.update(9);
  IO.println("Int min: " + intMinMax.getMin() + ", max: " + 
             intMinMax.getMax());

  var strMinMax = new MinMax<>("middle");
  strMinMax.update("apple");
  strMinMax.update("zebra");
  IO.println("String min: " + strMinMax.getMin() + ", max: " + 
             strMinMax.getMax());
}
```
The `MinMax<T extends Comparable<T>>` class demonstrates bounded type  
parameters that ensure the type supports comparison operations. By requiring  
`T extends Comparable<T>`, we can call `compareTo` on values of type `T`.  
This enables tracking minimum and maximum values for any comparable type like  
integers, strings, or custom classes that implement `Comparable`. The bound  
provides compile-time guarantees that necessary methods are available.  


## Wildcard with lower bound

This example demonstrates using wildcards with lower bounds for write  
scenarios.  

```java
void main() {

  List<Integer> integers = new ArrayList<>();
  addNumbers(integers);
  IO.println("Integers: " + integers);

  List<Number> numbers = new ArrayList<>();
  addNumbers(numbers);
  IO.println("Numbers: " + numbers);

  List<Object> objects = new ArrayList<>();
  addNumbers(objects);
  IO.println("Objects: " + objects);
}

void addNumbers(List<? super Integer> list) {
  list.add(1);
  list.add(2);
  list.add(3);
}
```
The lower bounded wildcard `? super Integer` allows the method to accept  
lists of `Integer` or any of its superclasses (`Number`, `Object`). This is  
contravariance - the opposite of `? extends`. Lower bounds are used when you  
want to add elements to a collection. The method can write `Integer` values  
to the list because any supertype of `Integer` can hold `Integer` values.  
This is useful for consumer-style operations.  


## Generic constructor

This example shows using generic constructors with type inference.  

```java
class Container<T> {

  private T value;

  <U extends T> Container(U value) {
    this.value = value;
  }

  public T getValue() {
    return value;
  }
}

void main() {

  var container1 = new Container<Number>(42);
  IO.println("Value: " + container1.getValue());

  var container2 = new Container<Number>(3.14);
  IO.println("Value: " + container2.getValue());

  var container3 = new Container<Object>("text");
  IO.println("Value: " + container3.getValue());
}
```
Generic constructors can have their own type parameters separate from the  
class type parameters. The constructor `<U extends T> Container(U value)`  
allows passing any subtype of `T` to initialize the container. This provides  
flexibility at construction time while maintaining type safety. The `U`  
parameter is inferred from the argument type, so we can pass an `Integer` to  
a `Container<Number>` because `Integer extends Number`.  


## Type inference with diamond operator

This example demonstrates type inference using the diamond operator in modern  
Java.  

```java
class Triple<A, B, C> {

  private A first;
  private B second;
  private C third;

  public Triple(A first, B second, C third) {
    this.first = first;
    this.second = second;
    this.third = third;
  }

  @Override
  public String toString() {
    return "(" + first + ", " + second + ", " + third + ")";
  }
}

void main() {

  var t1 = new Triple<>("Name", 25, true);
  IO.println(t1);

  var t2 = new Triple<>(1.5, "test", List.of(1, 2, 3));
  IO.println(t2);

  Triple<Integer, Integer, Integer> t3 = new Triple<>(1, 2, 3);
  IO.println(t3);
}
```
The diamond operator `<>` allows the compiler to infer generic types from the  
context. In `new Triple<>("Name", 25, true)`, the compiler infers the types  
as `String`, `Integer`, and `Boolean` from the constructor arguments. This  
reduces verbosity while maintaining type safety. When using `var`, the entire  
type is inferred. When declaring with an explicit type, only the constructor  
type parameters are inferred from the right-hand side.  


## Generic method with type witness

This example shows explicit type specification when type inference fails or  
needs clarification.  

```java
void main() {

  var list1 = Utils.<String>createList("apple", "banana", "cherry");
  IO.println(list1);

  var list2 = Utils.<Integer>createList(1, 2, 3, 4, 5);
  IO.println(list2);

  var list3 = Utils.<Number>createList(1, 2.5, 3L, 4.0f);
  IO.println(list3);
}

class Utils {

  @SafeVarargs
  static <T> List<T> createList(T... elements) {
    return new ArrayList<>(List.of(elements));
  }
}
```
Type witnesses are explicit type arguments provided before method names when  
calling generic methods. They're used when the compiler cannot infer the type  
or when you want to be explicit. The syntax `Utils.<String>createList()`  
specifies that `T` should be `String`. In the third example,  
`Utils.<Number>createList()` explicitly sets the common supertype for mixed  
numeric values. This is useful when dealing with complex type hierarchies.  


## Nested generic types

This example demonstrates working with nested generic types like lists of  
lists.  

```java
void main() {

  List<List<Integer>> matrix = new ArrayList<>();
  matrix.add(List.of(1, 2, 3));
  matrix.add(List.of(4, 5, 6));
  matrix.add(List.of(7, 8, 9));

  printMatrix(matrix);

  IO.println("Flattened: " + flatten(matrix));

  var stringMatrix = List.of(
      List.of("a", "b"),
      List.of("c", "d", "e")
  );
  IO.println("Flattened strings: " + flatten(stringMatrix));
}

<T> void printMatrix(List<List<T>> matrix) {
  for (var row : matrix) {
    IO.println(row);
  }
}

<T> List<T> flatten(List<List<T>> nested) {
  var result = new ArrayList<T>();
  for (var list : nested) {
    result.addAll(list);
  }
  return result;
}
```
Nested generics like `List<List<Integer>>` represent complex data structures  
such as matrices or tables. The type parameter can itself be a generic type.  
The `printMatrix` method accepts any two-dimensional list structure, and  
`flatten` converts nested lists into a single-level list. Working with nested  
generics requires careful attention to type parameters - `List<List<T>>`  
means a list of lists where each inner list contains elements of type `T`.  


## Generic with recursive type bound

This example shows the recursive type bound pattern commonly used with  
Comparable.  

```java
class Person implements Comparable<Person> {

  private String name;
  private int age;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  public String getName() {
    return name;
  }

  public int getAge() {
    return age;
  }

  @Override
  public int compareTo(Person other) {
    return Integer.compare(this.age, other.age);
  }

  @Override
  public String toString() {
    return name + " (" + age + ")";
  }
}

void main() {

  var people = List.of(
      new Person("Alice", 30),
      new Person("Bob", 25),
      new Person("Charlie", 35)
  );

  var youngest = min(people);
  IO.println("Youngest: " + youngest);
}

<T extends Comparable<T>> T min(List<T> list) {
  if (list.isEmpty()) {
    return null;
  }

  T minVal = list.get(0);
  for (T item : list) {
    if (item.compareTo(minVal) < 0) {
      minVal = item;
    }
  }
  return minVal;
}
```
The recursive type bound `<T extends Comparable<T>>` is a common pattern that  
ensures a type can compare instances of itself. The `Person` class implements  
`Comparable<Person>`, meaning it can compare to other `Person` objects. This  
self-referential bound is essential for generic comparison and sorting  
algorithms. The `min` method uses this bound to find the minimum element in a  
list of any comparable type.  


## Generic builder pattern

This example demonstrates using generics with the builder pattern for fluent  
APIs.  

```java
class Product {

  private String name;
  private double price;
  private String category;

  private Product() {}

  @Override
  public String toString() {
    return "Product{name=" + name + ", price=" + price + ", category=" + 
           category + "}";
  }

  static class Builder<T extends Builder<T>> {

    protected Product product = new Product();

    public T name(String name) {
      product.name = name;
      return self();
    }

    public T price(double price) {
      product.price = price;
      return self();
    }

    public T category(String category) {
      product.category = category;
      return self();
    }

    public Product build() {
      return product;
    }

    @SuppressWarnings("unchecked")
    protected T self() {
      return (T) this;
    }
  }
}

void main() {

  var product = new Product.Builder<>()
      .name("Laptop")
      .price(999.99)
      .category("Electronics")
      .build();

  IO.println(product);
}
```
The generic builder pattern uses a recursive type bound `<T extends Builder<T>>`  
to enable fluent method chaining. The `self()` method returns the correct  
type for subclass builders, allowing the builder pattern to work with  
inheritance. This pattern is more complex than basic builders but provides  
better extensibility. Each builder method returns `T` instead of `Builder`,  
ensuring subclass builders maintain their specific type through the chain.  


## Type token pattern

This example demonstrates the type token pattern for working with generic  
types at runtime.  

```java
class TypeReference<T> {

  private final Class<T> type;

  public TypeReference(Class<T> type) {
    this.type = type;
  }

  public Class<T> getType() {
    return type;
  }

  public T cast(Object obj) {
    return type.cast(obj);
  }

  public boolean isInstance(Object obj) {
    return type.isInstance(obj);
  }
}

void main() {

  var stringType = new TypeReference<>(String.class);
  Object obj1 = "Hello";
  
  if (stringType.isInstance(obj1)) {
    String str = stringType.cast(obj1);
    IO.println("Casted string: " + str);
  }

  var intType = new TypeReference<>(Integer.class);
  Object obj2 = 42;
  
  if (intType.isInstance(obj2)) {
    Integer num = intType.cast(obj2);
    IO.println("Casted integer: " + num);
  }
}
```
The type token pattern preserves generic type information at runtime by  
storing a `Class<T>` object. This is necessary because of type erasure -  
generic type parameters are not available at runtime. By passing a class  
literal to the constructor, we can perform runtime type checks and safe  
casting. This pattern is used in libraries like Jackson and Gson for generic  
type handling during serialization and deserialization.  


## Generic with enumeration

This example shows using generics with enum types to create type-safe  
registries.  

```java
enum Status {
  PENDING, ACTIVE, COMPLETED, CANCELLED
}

class Task<S extends Enum<S>> {

  private String name;
  private S status;

  public Task(String name, S initialStatus) {
    this.name = name;
    this.status = initialStatus;
  }

  public void setStatus(S status) {
    this.status = status;
  }

  public S getStatus() {
    return status;
  }

  @Override
  public String toString() {
    return name + " [" + status + "]";
  }
}

void main() {

  var task = new Task<>("Write documentation", Status.PENDING);
  IO.println(task);

  task.setStatus(Status.ACTIVE);
  IO.println(task);

  task.setStatus(Status.COMPLETED);
  IO.println(task);
}
```
Combining generics with enums allows creating flexible yet type-safe  
components. The bound `<S extends Enum<S>>` ensures the type parameter is an  
enum type. This pattern is useful when you want to parameterize classes with  
different enum types while ensuring compile-time type safety. The `Task`  
class can work with any enum type representing status, state, or category  
values.  


## Generic stream operations

This example demonstrates using generics with Stream API operations for  
flexible data processing.  

```java
void main() {

  var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
  
  var evenSquares = transform(numbers, 
      n -> n % 2 == 0, 
      n -> n * n);
  IO.println("Even squares: " + evenSquares);

  var words = List.of("apple", "banana", "cherry", "date", "elderberry");
  
  var longWords = transform(words,
      w -> w.length() > 5,
      String::toUpperCase);
  IO.println("Long words uppercase: " + longWords);
}

<T, R> List<R> transform(List<T> list, Predicate<T> filter, 
                         Function<T, R> mapper) {
  return list.stream()
      .filter(filter)
      .map(mapper)
      .collect(Collectors.toList());
}
```
This example combines generics with functional programming through the Stream  
API. The `transform` method is generic over both input type `T` and output  
type `R`, accepting a filter predicate and mapping function. This  
demonstrates how generics work seamlessly with functional interfaces and  
streams to create highly reusable data processing pipelines that maintain  
type safety throughout the transformation chain.  


## Generic exception handling

This example shows using generics with exception handling patterns for  
flexible error management.  

```java
class Result<T> {

  private final T value;
  private final Exception error;

  private Result(T value, Exception error) {
    this.value = value;
    this.error = error;
  }

  public static <T> Result<T> success(T value) {
    return new Result<>(value, null);
  }

  public static <T> Result<T> failure(Exception error) {
    return new Result<>(null, error);
  }

  public boolean isSuccess() {
    return error == null;
  }

  public T getValue() {
    return value;
  }

  public Exception getError() {
    return error;
  }
}

void main() {

  var result1 = divide(10, 2);
  if (result1.isSuccess()) {
    IO.println("Result: " + result1.getValue());
  } else {
    IO.println("Error: " + result1.getError().getMessage());
  }

  var result2 = divide(10, 0);
  if (result2.isSuccess()) {
    IO.println("Result: " + result2.getValue());
  } else {
    IO.println("Error: " + result2.getError().getMessage());
  }
}

Result<Double> divide(int a, int b) {
  try {
    return Result.success((double) a / b);
  } catch (Exception e) {
    return Result.failure(e);
  }
}
```
The `Result<T>` pattern uses generics to represent operations that may  
succeed with a value or fail with an exception. This is an alternative to  
throwing exceptions, making error handling more explicit. The generic type  
parameter `T` represents the success value type. This pattern is common in  
functional programming and helps avoid exceptions for expected failure cases,  
making error handling part of the normal control flow.  


## Generic with Optional

This example demonstrates combining generics with Optional for null-safe  
operations.  

```java
class Repository<T> {

  private Map<String, T> storage = new HashMap<>();

  public void save(String id, T item) {
    storage.put(id, item);
  }

  public Optional<T> findById(String id) {
    return Optional.ofNullable(storage.get(id));
  }

  public List<T> findAll() {
    return new ArrayList<>(storage.values());
  }
}

void main() {

  var userRepo = new Repository<String>();
  userRepo.save("1", "Alice");
  userRepo.save("2", "Bob");
  userRepo.save("3", "Charlie");

  userRepo.findById("2")
      .ifPresent(user -> IO.println("Found: " + user));

  userRepo.findById("99")
      .ifPresentOrElse(
          user -> IO.println("Found: " + user),
          () -> IO.println("User not found")
      );

  IO.println("All users: " + userRepo.findAll());
}
```
Combining generics with `Optional` creates robust, null-safe APIs. The  
`Repository<T>` class provides a generic storage mechanism where `findById`  
returns `Optional<T>` instead of potentially null values. This forces callers  
to explicitly handle the absence of values, preventing null pointer  
exceptions. The pattern works with any type `T`, making it a reusable  
component for different entity types.  


## Generic predicate composition

This example shows composing generic predicates for flexible filtering logic.  

```java
class PredicateBuilder<T> {

  private Predicate<T> predicate;

  public PredicateBuilder(Predicate<T> predicate) {
    this.predicate = predicate;
  }

  public PredicateBuilder<T> and(Predicate<T> other) {
    predicate = predicate.and(other);
    return this;
  }

  public PredicateBuilder<T> or(Predicate<T> other) {
    predicate = predicate.or(other);
    return this;
  }

  public PredicateBuilder<T> negate() {
    predicate = predicate.negate();
    return this;
  }

  public Predicate<T> build() {
    return predicate;
  }
}

void main() {

  var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12);

  var predicate = new PredicateBuilder<Integer>(n -> n > 5)
      .and(n -> n % 2 == 0)
      .build();

  var filtered = numbers.stream()
      .filter(predicate)
      .collect(Collectors.toList());

  IO.println("Filtered numbers: " + filtered);
}
```
The `PredicateBuilder<T>` demonstrates composing predicates using generics.  
It provides a fluent API for combining multiple conditions with `and`, `or`,  
and `negate` operations. The generic type parameter `T` ensures all predicates  
in the chain work with the same type. This pattern is useful for building  
complex filtering logic dynamically, especially in query builders and search  
functionality.  


## Generic comparator chaining

This example demonstrates creating and chaining generic comparators for  
complex sorting.  

```java
record Employee(String name, int age, double salary) {}

void main() {

  var employees = List.of(
      new Employee("Alice", 30, 50000),
      new Employee("Bob", 25, 55000),
      new Employee("Charlie", 30, 48000),
      new Employee("Diana", 25, 55000)
  );

  IO.println("Original:");
  employees.forEach(IO::println);

  var sorted = employees.stream()
      .sorted(
          Comparator.<Employee>comparingInt(Employee::age)
              .thenComparingDouble(Employee::salary)
              .thenComparing(Employee::name)
      )
      .collect(Collectors.toList());

  IO.println("\nSorted by age, then salary, then name:");
  sorted.forEach(IO::println);
}
```
Generic comparators can be chained to create sophisticated sorting logic. The  
`Comparator.<Employee>comparingInt()` uses a type witness to specify the type  
being compared. Chaining with `thenComparingDouble` and `thenComparing`  
creates a multi-level sort order. This demonstrates how generics in the  
`Comparator` interface enable type-safe, composable sorting strategies that  
work with any comparable attributes.  


## Generic factory method pattern

This example shows using generic factory methods to create instances based on  
type parameters.  

```java
interface Animal {
  void makeSound();
}

class Dog implements Animal {
  @Override
  public void makeSound() {
    IO.println("Woof!");
  }
}

class Cat implements Animal {
  @Override
  public void makeSound() {
    IO.println("Meow!");
  }
}

class AnimalFactory {

  public static <T extends Animal> T create(Class<T> type) {
    try {
      return type.getDeclaredConstructor().newInstance();
    } catch (Exception e) {
      throw new RuntimeException("Failed to create instance", e);
    }
  }
}

void main() {

  var dog = AnimalFactory.create(Dog.class);
  dog.makeSound();

  var cat = AnimalFactory.create(Cat.class);
  cat.makeSound();
}
```
Generic factory methods use `Class<T>` parameters to create instances of the  
specified type. The method `<T extends Animal> T create(Class<T> type)`  
ensures the returned instance matches the requested type. This pattern  
leverages reflection with generics to provide type-safe object creation. The  
bound `extends Animal` restricts creation to animal types, providing  
compile-time guarantees about what can be instantiated.  


## Generic cache implementation

This example demonstrates a simple generic cache with expiration logic.  

```java
class CacheEntry<V> {

  private V value;
  private long timestamp;

  public CacheEntry(V value) {
    this.value = value;
    this.timestamp = System.currentTimeMillis();
  }

  public V getValue() {
    return value;
  }

  public boolean isExpired(long ttlMillis) {
    return System.currentTimeMillis() - timestamp > ttlMillis;
  }
}

class Cache<K, V> {

  private Map<K, CacheEntry<V>> store = new HashMap<>();
  private long ttl;

  public Cache(long ttlMillis) {
    this.ttl = ttlMillis;
  }

  public void put(K key, V value) {
    store.put(key, new CacheEntry<>(value));
  }

  public Optional<V> get(K key) {
    var entry = store.get(key);
    if (entry != null && !entry.isExpired(ttl)) {
      return Optional.of(entry.getValue());
    }
    store.remove(key);
    return Optional.empty();
  }
}

void main() {

  var cache = new Cache<String, Integer>(5000);
  cache.put("age", 25);
  cache.put("count", 100);

  cache.get("age").ifPresent(v -> IO.println("Age: " + v));
  cache.get("count").ifPresent(v -> IO.println("Count: " + v));
}
```
A generic cache uses multiple type parameters: `K` for keys and `V` for  
values. The nested `CacheEntry<V>` wraps values with metadata like  
timestamps. This demonstrates how generics enable creating reusable data  
structures that work with any key-value types while maintaining type safety.  
The cache returns `Optional<V>` to handle missing or expired entries safely.  


## Generic visitor pattern

This example demonstrates the visitor pattern implemented with generics for  
type-safe element processing.  

```java
interface Visitor<T> {
  void visit(T element);
}

interface Visitable<T> {
  void accept(Visitor<T> visitor);
}

class Document implements Visitable<Document> {

  private String content;

  public Document(String content) {
    this.content = content;
  }

  public String getContent() {
    return content;
  }

  @Override
  public void accept(Visitor<Document> visitor) {
    visitor.visit(this);
  }
}

class WordCountVisitor implements Visitor<Document> {

  private int count = 0;

  @Override
  public void visit(Document doc) {
    count = doc.getContent().split("\\s+").length;
  }

  public int getCount() {
    return count;
  }
}

void main() {

  var doc = new Document("Java generics provide type safety and reusability");
  
  var wordCounter = new WordCountVisitor();
  doc.accept(wordCounter);
  
  IO.println("Word count: " + wordCounter.getCount());
}
```
The generic visitor pattern uses type parameters to ensure visitors and  
visitable elements match types correctly. The `Visitor<T>` interface defines  
the visiting operation for type `T`, and `Visitable<T>` accepts visitors of  
the same type. This pattern separates algorithms from the objects they  
operate on while maintaining type safety. The generic version is more  
flexible than traditional visitor patterns.  


## Generic with multiple wildcards

This example demonstrates using multiple wildcards in method signatures for  
maximum flexibility.  

```java
void main() {

  List<Integer> integers = List.of(1, 2, 3, 4, 5);
  List<Double> doubles = List.of(1.1, 2.2, 3.3);
  
  copy(integers, new ArrayList<Number>());
  copy(doubles, new ArrayList<Number>());
  
  List<String> strings = List.of("a", "b", "c");
  List<Object> objects = new ArrayList<>();
  copy(strings, objects);
  
  IO.println("Objects: " + objects);
}

<T> void copy(List<? extends T> source, List<? super T> dest) {
  for (T item : source) {
    dest.add(item);
  }
}
```
The `copy` method uses both upper and lower bounded wildcards. The source  
uses `? extends T` (covariance) allowing reading from any list of `T` or its  
subtypes. The destination uses `? super T` (contravariance) allowing writing  
to any list of `T` or its supertypes. This combination follows the PECS  
principle (Producer Extends, Consumer Super), enabling maximum flexibility  
for copy operations between compatible list types.  


## Generic method overloading

This example shows how generic methods can be overloaded with different type  
constraints.  

```java
class Processor {

  <T> void process(T item) {
    IO.println("Processing generic item: " + item);
  }

  <T extends Number> void process(T number) {
    IO.println("Processing number: " + number + ", double value: " + 
               number.doubleValue());
  }

  <T extends CharSequence> void process(T text) {
    IO.println("Processing text: " + text + ", length: " + text.length());
  }
}

void main() {

  var processor = new Processor();
  
  processor.process("Hello");
  processor.process(42);
  processor.process(3.14);
  processor.process(new StringBuilder("Builder"));
}
```
Generic methods can be overloaded with different bounds on type parameters.  
The compiler selects the most specific method based on the argument type. A  
method with `<T extends Number>` is more specific than one with unbounded  
`<T>` when passed a number. This allows providing specialized behavior for  
certain type categories while maintaining a general fallback. Overloading  
with generic bounds enables creating sophisticated, type-aware processing  
logic.  


## Generic collection wrapper

This example demonstrates creating a wrapper around collections with  
additional functionality.  

```java
class ObservableList<E> {

  private List<E> list = new ArrayList<>();
  private List<Consumer<E>> listeners = new ArrayList<>();

  public void addListener(Consumer<E> listener) {
    listeners.add(listener);
  }

  public void add(E element) {
    list.add(element);
    notifyListeners(element);
  }

  public E get(int index) {
    return list.get(index);
  }

  public int size() {
    return list.size();
  }

  private void notifyListeners(E element) {
    for (var listener : listeners) {
      listener.accept(element);
    }
  }
}

void main() {

  var observableList = new ObservableList<String>();
  
  observableList.addListener(item -> 
      IO.println("Added: " + item));
  
  observableList.add("apple");
  observableList.add("banana");
  observableList.add("cherry");
  
  IO.println("Total items: " + observableList.size());
}
```
The `ObservableList<E>` wraps a standard list and adds observation  
capabilities. It demonstrates how generics enable creating enhanced  
collection types that work with any element type. The observer pattern  
combined with generics provides type-safe event notifications. Each listener  
receives elements of type `E`, ensuring type consistency between the list  
contents and listener callbacks.  


## Generic state machine

This example shows implementing a simple generic state machine.  

```java
class StateMachine<S extends Enum<S>> {

  private S currentState;

  public StateMachine(S initialState) {
    this.currentState = initialState;
  }

  public S getState() {
    return currentState;
  }

  public void transition(S newState) {
    IO.println("Transitioning from " + currentState + " to " + newState);
    currentState = newState;
  }

  public boolean isInState(S state) {
    return currentState == state;
  }
}

enum OrderState {
  CREATED, CONFIRMED, SHIPPED, DELIVERED, CANCELLED
}

void main() {

  var orderStateMachine = new StateMachine<>(OrderState.CREATED);
  
  IO.println("Current state: " + orderStateMachine.getState());
  
  orderStateMachine.transition(OrderState.CONFIRMED);
  orderStateMachine.transition(OrderState.SHIPPED);
  orderStateMachine.transition(OrderState.DELIVERED);
  
  if (orderStateMachine.isInState(OrderState.DELIVERED)) {
    IO.println("Order has been delivered!");
  }
}
```
The generic state machine uses bounded type parameters `<S extends Enum<S>>`  
to work with any enum-based state representation. This provides type safety  
while allowing the state machine to be reused with different state  
enumerations. The generic approach ensures compile-time verification that  
only valid states from the specified enum can be used in transitions and  
checks. This pattern is useful for workflow engines and process management.  

