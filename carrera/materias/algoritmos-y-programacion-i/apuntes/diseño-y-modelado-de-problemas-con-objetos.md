# Diseño y modelado de problemas con objetos

El **diseño y modelado de problemas con objetos** es una técnica de análisis que permite representar problemas del mundo real mediante **objetos**, sus atributos y comportamientos.

Esto facilita la construcción de programas **claros, modulares y escalables**.

---

## Conceptos clave

### Objeto

- Representa una **entidad concreta o conceptual**.
- Tiene **atributos** (estado) y **métodos** (comportamiento).

### Clase

- Plantilla que define los atributos y métodos de los objetos.
- Permite crear **múltiples instancias**.

### Atributos

- Datos que describen las propiedades del objeto.

### Métodos

- Operaciones que definen la conducta del objeto.

### Relación entre objetos

- Los objetos pueden **colaborar, heredar, asociarse o componerse** para resolver problemas complejos.

---

## Pasos para modelar problemas con objetos

### Identificación de objetos

1. Analizar el problema.
2. Detectar entidades que representen conceptos o cosas del mundo real.
3. Definir qué atributos y comportamientos posee cada entidad.

**Ejemplo**: Sistema de biblioteca

- Objetos: `Book`, `User`, `Librarian`, `Lending`.
- Atributos: title, author, name, date.
- Métodos: lendBook, returnBook, showInformation.

### Definición de clases

- Crear clases que **representen los objetos identificados**.
- Especificar **atributos y métodos**.

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
```

### Determinación de relaciones

Existen distintos tipos de relaciones entre objetos:

1. **Asociación**: Un objeto conoce a otro.

   ```java
    public class Lending {
      private Book book;
      private User user;
    }
   ```

2. **Herencia**: Un objeto hereda atributos y métodos de otro.

   ```java
    public class Person { ... }

    // La palabra reservada 'extends' indica que X clase hereda de Y clase.
    public class Librarian extends Person { ... }
   ```

3. **Composición**: Un objeto está compuesto por otros objetos.

   ```java
   public class Library {
   private ArrayList<Book> books;
   }
   ```

### Definición de responsabilidades

- Cada objeto debe tener **una responsabilidad clara**.
- Aplicar el **principio de responsabilidad única** ([Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)).
- Facilita la **mantenibilidad** y la **reutilización**.

### Diseño de métodos

- Definir **operaciones que cada objeto puede realizar**.
- Separar lógica en **métodos claros y concisos**.
- Evitar métodos demasiado largos o con múltiples responsabilidades.

---

## Ejemplo: Sistema de biblioteca en Java

```java
// Clase del libro
public class Book {
  private String title;
  private String author;

  public Book(String title, String author) {
    this.title = title;
    this.author = author;
  }

  public String getTitle() {
    return title;
  }

  public void showInformation() {
    System.out.println(title + " - " + author);
  }
}

// Clase del usuario
public class User {
  private String name;

  public User(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }
}

// Clase del préstamo
import java.time.LocalDate;

public class Lending {
  private Book book;
  private User user;
  private LocalDate date;

  public Lending(Book book, User user) {
    this.book = book;
    this.user = user;
    this.date = LocalDate.now();
  }

  public void showLending() {
    System.out.println(user.getName() + " have the book " + book.getTitle() + " from " + date);
  }
}

// Clase de la biblioteca
import java.util.ArrayList;

public class Library {
  private ArrayList<Book> books = new ArrayList<>();

  public Library() {
    super();
  }

  public void addBook(Book book) {
    books.add(book);
  }

  public void showBooks() {
    for (Book b : books) {
      b.showInformation();
    }
  }
}
```

- Cada clase representa **una entidad del mundo real**.
- Las clases interactúan entre sí mediante **relaciones de asociación y composición**.

---

## Buenas prácticas de diseño con objetos

1. **Encapsulamiento**: Ocultar atributos internos y exponer solo lo necesario.
2. **Cohesión**: Mantener cada objeto enfocado en una sola responsabilidad.
3. **Bajo acoplamiento**: Minimizar dependencias entre objetos.
4. **Reutilización**: Diseñar clases que puedan usarse en distintos contextos.
5. **Legibilidad**: Nombres claros para clases, atributos y métodos.
6. **Uso de UML**: Diagramas de clases y objetos ayudan a visualizar el diseño antes de programar.

---

## Ventajas del modelado con objetos

- **Claridad conceptual**: El diseño refleja entidades del mundo real.
- **Mantenibilidad**: Cambios en una clase no afectan al resto si está bien encapsulada.
- **Reutilización**: Objetos bien diseñados pueden usarse en múltiples sistemas.
- **Escalabilidad**: Permite ampliar el sistema añadiendo nuevas clases u objetos.
- **Facilita pruebas**: Se pueden probar los objetos de forma independiente.

---

## Conclusión

El **diseño y modelado de problemas con objetos** permite transformar problemas complejos en soluciones estructuradas y comprensibles.

Al identificar objetos, definir clases, relaciones y responsabilidades, se obtiene un **modelo coherente** que guía la implementación en Java u otros lenguajes con orientación a objetos.

El resultado es un software **modular, escalable y fácil de mantener**, reflejando de manera clara la realidad que se busca representar.
