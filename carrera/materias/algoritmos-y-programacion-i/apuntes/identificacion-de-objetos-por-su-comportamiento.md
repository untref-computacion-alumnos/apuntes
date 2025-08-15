# Identificación de objetos por su comportamiento

En la **programación orientada a objetos (POO)**, la **identificación de objetos por su comportamiento** consiste en reconocer y definir objetos no solo por las características que tienen (**atributos**), sino principalmente por **lo que hacen** (**métodos**).

Esto se basa en la idea de que los objetos son **entidades activas**, que interactúan entre sí **enviándose mensajes** y realizando acciones específicas.

---

## Concepto

- Un objeto se puede describir por **dos aspectos principales**:

  1. **Estado**: Información que almacena (atributos).
  2. **Comportamiento**: Conjunto de acciones que puede realizar (métodos).

- La **identificación por comportamiento** se enfoca en **qué hace** un objeto, más que en **qué tiene**.

**Ejemplo**:

Un objeto de tipo `Printer` podría tener atributos como `brand`, `model`, `color`, pero lo que realmente le define en un sistema son acciones como:

- `printDocument()`
- `cancelPrint()`
- `getState()`

---

## Importancia de la identificación por comportamiento

- **Modelado más realista**: Representa la forma en que interactúan las entidades en el mundo real.
- **Enfoque funcional**: Evita crear objetos innecesarios que solo almacenan datos, y promueve objetos que **hacen cosas**.
- **Flexibilidad y extensibilidad**: Permite que un mismo tipo de objeto se distinga por las acciones que implementa (por ejemplo, interfaces y polimorfismo en Java).
- **Abstracción más clara**: El comportamiento describe la finalidad del objeto en el sistema.

---

## Pasos para identificar objetos por su comportamiento

1. **Analizar el problema**: Leer la descripción y detectar **verbos** y **acciones**.
2. **Relacionar acciones con entidades**: Vincular cada acción con un posible objeto.
3. **Agrupar acciones similares**: Un mismo objeto debe tener comportamientos relacionados.
4. **Definir métodos**: Cada acción se traduce en un método en la clase correspondiente.
5. **Eliminar redundancias**: Evitar métodos duplicados o innecesarios.

---

## Ejemplo de análisis

**Enunciado del problema**: Un sistema de gestión de biblioteca tiene que permitir que un usuario solicite un libro, lo devuelva y consulte su historial.

- Verbos detectados:

  - _Solicitar_: Acción de un usuario.
  - _Devolver_: Acción de un usuario.
  - _Consultar_: Acción de un usuario.

- Objeto identificado:
  - `User`: Métodos `requestBook()`, `returnBook()`, `checkHistory()`.

---

## Ejemplo en Java

```java
public class User {
  private String name;

  public User(String name) {
    this.name = name;
  }

  public void requestBook(Book book) {
    System.out.println(name + " has requested the book " + book.getTitle());
  }

  public void returnBook(Book book) {
    System.out.println(name + " has returned the book " + book.getTitle());
  }

  public void checkHistory() {
    System.out.println("Showing history of " + name);
  }
}

public class Book {
  private String title;

  public Book(String title) {
    this.title = title;
  }

  public String getTitle() {
    return title;
  }
}

// Uso
User u1 = new User("Ana");
Book b1 = new Book("1984");

u1.requestBook(b1);
u1.returnBook(b1);
u1.checkHistory();
```

En este ejemplo:

- El **objeto `User`** se define más por **lo que hace** (comportamiento) que por los datos que tiene.
- Los métodos son la clave para entender su papel dentro del sistema.

---

## Relación con interfaces y polimorfismo

En Java, el comportamiento de un objeto puede **describirse y garantizarse** a través de **interfaces**.

**Ejemplo**:

```java
public interface Printable {
  void print();
}

public class Bill implements Printable {
  @Override
  public void print() {
    System.out.println("Printing bill...");
  }
}

public class Report implements Printable {
  @Override
  public void print() {
    System.out.println("Printing report...");
  }
}

// Uso polimórfico
Printable doc1 = new Bill();
Printable doc2 = new Report();

doc1.print();
doc2.print();
```

- Tanto `Bill` como `Report` son **objetos distintos**, pero se identifican por el **mismo comportamiento** (`print()`).

---

## Ventajas de identificar objetos por comportamiento

1. **Mayor cohesión**: Los objetos agrupan comportamientos relacionados.
2. **Facilidad para el mantenimiento**: Al tener responsabilidades claras, es más fácil modificar o ampliar el sistema.
3. **Reutilización de código**: El comportamiento puede compartirse entre diferentes clases.
4. **Soporte para polimorfismo**: Objetos distintos pueden responder a la misma acción de diferentes maneras.
5. **Desacoplamiento**: El sistema se enfoca en **qué se hace** más que en **cómo se hace**.

---

## Buenas prácticas

- Definir métodos con **nombres claros y descriptivos** (usar verbos).
- Mantener **coherencia** entre el nombre del objeto y sus métodos.
- Evitar comportamientos que no correspondan a la responsabilidad principal del objeto.
- Usar **interfaces** para describir comportamientos comunes entre objetos diferentes.
- Aplicar **principio de responsabilidad única (SRP)**.

---

## Ejemplo integrador: Sistema de pagos

**Objetivo**: Identificar objetos según lo que hacen en el proceso de pago.

### Verbos clave

- Procesar pago.
- Validar tarjeta.
- Generar recibo.

### Objetos identificados

- `ProcesadorDePago`.
- `ValidadorDeTarjeta`.
- `GeneradorDeRecibo`.

### Implementación en Java

```java
public class ProcesadorPago {
  public void procesar() {
    System.out.println("Procesando pago...");
  }
}

public class ValidadorTarjeta {
  public void validar() {
    System.out.println("Validando tarjeta...");
  }
}

public class GeneradorRecibo {
  public void generar() {
    System.out.println("Generando recibo...");
  }
}

// Uso
ValidadorTarjeta validador = new ValidadorTarjeta();
ProcesadorPago procesador = new ProcesadorPago();
GeneradorRecibo generador = new GeneradorRecibo();

validador.validar();
procesador.procesar();
generador.generar();
```

Acá cada objeto está definido **por su comportamiento principal** en el flujo del sistema.

---

## Conclusión

- La **identificación de objetos por su comportamiento** es un enfoque que prioriza las **acciones** de los objetos sobre sus atributos.
- Permite construir sistemas más **claros, flexibles y reutilizables**.
- En Java, este enfoque se refuerza mediante **métodos, interfaces y polimorfismo**.
- Comprender y aplicar esta técnica ayuda a diseñar **arquitecturas limpias** y con **alta cohesión**.
