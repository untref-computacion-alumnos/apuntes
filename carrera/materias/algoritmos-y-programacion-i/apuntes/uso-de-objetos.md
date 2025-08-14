# Uso de objetos

Los **objetos** son la base de la programación orientada a objetos (POO).

El **uso de objetos** implica cómo crearlos, interactuar con ellos, modificar su estado y utilizar sus métodos para lograr el comportamiento deseado en un programa.

---

## Creación de objetos

Para usar un objeto primero se tiene que **instanciar** a partir de una clase.

```java
// Definición de una clase
public class Person {
  String name;
  int age;

  public Person() {
    super();
  }

  void greet() {
    System.out.println("Hello, I am " + name);
  }
}

// Creación de objeto
Person p1 = new Person();  // Instancia de 'p1'
Person p2 = new Person(); // Instancia de 'p2'
```

- Cada objeto creado es **independiente**.
- Pueden tener valores distintos para sus atributos.

---

## Acceso a atributos y métodos

### Atributos

Se accede mediante la referencia al objeto:

```java
p1.name = "Ana";
p1.age = 25;

p2.name = "Luis";
p2.age = 30;
```

### Métodos

Se invocan usando la referencia del objeto

```java
p1.greet(); // Hello, I am Ana
p2.greet(); // Hello, I am Luis
```

---

## Encapsulamiento y acceso controlado

Para un uso seguro de objetos se deben **ocultar los atributos** (`private`) y exponer **métodos públicos** (_getters_ y _setters_).

```java
public class Person {
  private String name;
  private int age;

  public Person() {
    super();
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getAge() {
    return age;
  }

  public void setAge(int age) {
    if (age >= 0) {
      this.age = age;
    }
  }
}

// Uso
Person p = new Person();
p.setName("Ana");
p.setAge(25);
System.out.println(p.getName());  // Ana
```

> Esto permite **controlar cambios y validar datos**, evitando errores.

---

## Constructores y uso eficiente de objetos

Los constructores permiten **inicializar objetos** al momento de crearlos:

```java
public class Person {
  private String name;
  private int age;

  public Person() {
    this.name = name;
    this.age = age;
  }

  public void greet() {
    System.out.println("Hello, I am " + name + " and I am " + age + " years old");
  }
}

// Uso
Person p = new Person("Ana", 25);
p.greet();  // Hello, I am Ana and I am 25 years old
```

---

## Interacción entre objetos

Los objetos pueden **interactuar entre sí**:

```java
public class Car {
  private String model;
  private int speed;

  public Car(String model) {
    this.model = model;
    this.speed = 0;
  }

  public void accelerate(int increase) {
    speed += increase;
    System.out.println(model + " accelerated to " + speed + " km/h");
  }
}

public class Driver {
  private String name;

  public Driver(String name) {
    this.name = name;
  }

  public void drive(Car car) {
    System.out.println(name + " is driving the car");
    car.accelerate(50);
  }
}

// Uso
Car car1 = new Car("Toyota");
Driver driver1 = new Driver("Luis");
c.drive(car1);
// Salida:
// Luis is driving the car
// Toyota accelerated to 50 km/h
```

> Ejemplo de **interacción entre objetos**, donde un objeto llama métodos del otro.

---

## Objetos como parámetros y retornos de métodos

Se pueden **pasar objetos** como argumentos o devolverlos desde métodos:

```java
public class Calculator {
  public int add(int a, int b) {
    return a + b;
  }

  public Person createPerson(String name, int age) {
    return new Person(name, age);
  }
}

// Uso
Calculator calc = new Calculator();
Person p = calc.createPerson("Ana", 25);
System.out.println(p.getName()); // Ana
```

> Permite **modularizar la lógica y reutilizar objetos**.

---

## Colecciones de objetos

Para manejar múltiples objetos se utilizan **estructuras de datos** como arreglos, listas y mapas:

```java
import java.util.ArrayList;

ArrayList<Person> persons = new ArrayList<>();
persons.Add(new Person("Ana", 25));
persons.Add(new Person("Luis", 30));

for (Person p : persons) {
  p.greet();
}
```

> Facilita el **almacenamiento, acceso y procesamiento** de objetos de forma organizada.

---

## Buenas prácticas en el uso de objetos

1. **Encapsular atributos** y usar métodos públicos para acceder a ellos.
2. **Evitar objetos innecesarios** para no desperdiciar memoria.
3. **Usar constructores** para inicialización consistente.
4. **Modularizar comportamiento** en métodos claros y concisos.
5. **Evitar exponer referencias internas** directamente.
6. **Reutilizar objetos** cuando sea posible.
7. **Seguir el principio de responsabilidad única**: Un objeto debe tener un propósito _claro_.

---

## Ejemplo: Biblioteca de objetos

```java
public class Book {
  private String title;
  private String author;

  public Book(String title, String author) {
    this.title = title;
    this.author = author;
  }

  public void showInfo() {
    System.out.println(title + " - " + author);
  }
}

public class Library {
  private ArrayList<Book> books = new ArrayList<>();

  public void addBook(Book book) {
    books.add(book);
  }

  public void showBooks() {
    for (Book b : books) {
      l.showInfo();
    }
  }
}

// Uso
Library lb = new Library();
lb.addBook(new Book("Cien Años de Soledad", "Gabriel García Márquez"));
lb.addBook(new Book("1984", "George Orwell"));
lb.showBooks();
```

- Cada libro es un **objeto independiente**.
- La biblioteca **gestiona los objetos** sin conocer detalles internos de cada libro.

---

## Conclusión

El **uso de objetos** consiste en **crear, inicializar, manipular y organizar entidades** que combinan estado y comportamiento.

Permite:

- Modularidad y reutilización de código.
- Interacción entre entidades.
- Gestión eficiente de datos complejos.

En Java, dominar el uso de objetos es clave para construir aplicaciones **claras, mantenibles y escalables**, siguiendo principios de programación orientada a objetos.
