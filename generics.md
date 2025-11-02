# Generics


## 

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

## 

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


## 

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



## 

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



## 

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



## 

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

## 

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


