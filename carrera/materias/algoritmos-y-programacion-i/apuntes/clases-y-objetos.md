# Clases y objetos

En la **programación orientada a objetos (POO)**, los conceptos de **clase** y **objeto** son fundamentales.

Este tema explica cómo se definen, cómo se crean, cómo interactúan y cómo se usan en la práctica con ejemplos en Java.

---

## Definición de clase

Una **clase** es un **molde o plantilla** que define un tipo de objeto.

Especifica:

- **Atributos**: Propiedades o estado del objeto.
- **Métodos**: Comportamientos o acciones que puede realizar el objeto.

**Ejemplo en Java**:

```java
public class Person {
  String name;    // Atributo
  int age;        // Atributo

  void greet() {  // Método
    System.out.println("Hello, I am " + name);
  }
}
```

> La clase define **qué es una persona**, pero todavía no hay persons concretas creadas.

---

## Definición de objeto

Un **objeto** es una **instancia de una clase**, es decir, un ejemplar concreto con valores propios en sus atributos.

```java
Person p1 = new Person(); // p1 es un objeto
p1.name = "Ana";
p1.age = 25;
p1.greet();               // Salida: Hello, I am Ana
```

- Cada objeto tiene un **estado independiente**.
- Los métodos operan sobre el estado de cada objeto.

---

## Relación entre clase y objeto

| Concepto       | Descripción                                             |
| -------------- | ------------------------------------------------------- |
| Clase          | Molde o plantilla que define atributos y métodos.       |
| Objeto         | Instancia concreta de la clase con valores específicos. |
| Estado         | Valores actuales de los atributos de un objeto.         |
| Comportamiento | Métodos que definen las acciones del objeto.            |

**Analogía**: Clase = Plano de un edificio; Objeto = Edificio construido siguiendo ese plano.

---

## Componentes de una clase

### Atributos

- Variables que representan el estado del objeto.
- Pueden ser **primitivos** o referencias a otros objetos.
- Se debe usar **encapsulamiento** (`private`) para protegerlos.

```java
private String name;
private int age;
```

### Métodos

- Definen el comportamiento del objeto.
- Pueden modificar atributos o interactuar con otros objetos.
- Se declaran con un tipo de retorno o `void` (no retorna nada).

```java
public void birthday() {
  age++;
}

public int getAge() {
  return age;
}
```

### Constructores

- Métodos especiales que inicializan objetos.
- Pueden ser **sobrecargados** para distintas formas de inicialización.

```java
public Person(String name, int age) {
  this.name = name;
  this.age = age;
}
```

---

## Creación y uso de objetos

1. **Declaración**: `Person p` crea una referencia.
2. **Instanciación**: `new Person()` crea un objeto en memoria.
3. **Asignación**: `p = new Person()` referencia que apunta al objeto.

```java
Person p1 = new Person("Ana", 25);
Person p2 = new Person("Luis", 30);
```

- `p1` y `p2` son objetos independientes.
- Cada uno mantiene su **propio estado**.

---

## Encpsulamiento y getters/setters

Permite proteger los atributos y controlar el acceso a ellos.

```java
public class Person {
  private String name;
  private int age;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
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
```

- Mejora la **seguridad y mantenibilidad** del código.
- Facilita la **validación de datos** al modificar atributos.

---

## Objetos como parámetros y retorno de métodos

Los objetos pueden ser **pasados como argumentos** o **retornados** desde métodos:

```java
public class Calculator {
  public Person createPerson(String name, int age) {
    return new Person(name, age);
  }
}

// Uso
Calculator calc = new Calculator();
Person p = calc.createPerson("Ana", 25);
System.out.println(p.getName()); // Ana
```

- Permite **modularidad** y **reutilización** de código.

---

## Interacción entre objetos

Los objetos pueden **colaborar** entre sí para resolver problemas:

```java
public class Car {
  private String model;
  private int speed;

  public void accelerate(int increase) {
    speed += increase;
  }
}

public class Driver {
  public void drive(Car car) {
    car.accelerate(50);
  }
}

// Uso
Car myCar = new Car();
Driver c = new Driver();
c.drive(myCar);
```

- Ejemplo de **relación de asociación** entre objetos.
- Un objeto puede **invocar métodos de otro** para lograr comportamiento conjunto.

---

## Colección de objetos

Se pueden almacenar múltiples objetos usando **arreglos, listas o mapas**:

```java
ArrayList<Person> persons = new ArrayList<>();
persons.add(new Person("Ana", 25));
persons.add(new Person("Luis", 30));

for (Person p : persons) {
  System.out.println(p.getName());
}
```

- Facilita la **gestión y manipulación de conjuntos de objetos**.
- Permite aplicar **algoritmos** sobre grupos de objetos.

---

## Buenas prácticas

1. **Encapsular atributos**.
2. **Responsabilidad única** por clase.
3. **Modularidad y reutilización**: Cada clase tiene un propósito claro.
4. **Nombres claros** para clases, métodos y atributos.
5. **Constructores bien definidos** para inicialización consistente.
6. Evitar **exposición directa de referencias internas**.
7. **Documentar métodos** y clases para facilitar mantenimiento.

---

## Ejemplo: Sistema de biblioteca

```java
public class Book {
  private String title;
  private String author;

  public Book(String title, String author) {
    this.title = title;
    this.author = author;
  }

  public void showInformation() {
    System.out.println(title + " - " + author);
  }
}

public class Library {
  private ArrayList<Book> books = new ArrayList<>();

  public void addBook(Book book) {
    books.add(book);
  }

  public void showBooks() {
    for (Book book : books) {
      book.showInformation();
    }
  }
}

// Uso
Library bib = new Library();
bib.addBook(new Book("Cien Años de Soledad", "Gabriel García Márquez"));
bib.addBook(new Book("1984", "George Orwell"));
bib.showBooks();
```

- Cada **libro** es un objeto.
- La **biblioteca** gestiona la colección de objetos.
- Se demuestra **modularidad, encapsulamiento e interacción entre objetos**.

---

## Conclusión

- Una **clase** define un tipo de objeto, y un **objeto** es su instancia concreta.
- Los objetos permiten **representar entidades del mundo real**, encapsular datos y comportamientos, y organizar la lógica del programa de manera modular.
- Comprender **clases y objetos** es esencial para diseñar sistemas **robustos, mantenibles y escalables** en Java y en cualquier otro lenguaje orientado a objetos.
