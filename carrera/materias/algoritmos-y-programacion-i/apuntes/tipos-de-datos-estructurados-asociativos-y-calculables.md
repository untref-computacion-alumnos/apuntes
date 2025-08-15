# Tipos de datos estructurados asociativos (objetos) y calculables (vectores)

En programación, los **tipos de datos estructurados** son aquellos que permiten almacenar y organizar **múltipes valores** bajo una misma estructura.

Dentro de esta categoría, se encuentran:

1. **Estructurados asociativos**: Datos organizados en forma de **clave-valor**, como los objetos en Java.
2. **Estructurados calculables**: Datos organizados en **posiciones secuenciales** y accesibles mediante índices numéricos, como los vectores o arreglos.

---

## Tipos de datos estructurados asociativos (Objetos)

### Concepto

Un **tipo de dato estructurado asociativo** almacena pares **clave-valor**.

Cada valor está asociado a una clave única, y se accede a la información **mediante la clave**, no mediante una posición numérica.

En Java, el ejemplo más común de estructura asociativa es el uso de **objetos** y **colecciones como `Map`**.

---

### Características principales

- Acceso a los elementos mediante **claves únicas**.
- Las claves pueden ser de distintos tipos (Strings, enteros, enums, etc.).
- Permiten representar entidades del mundo real con propiedades y comportamientos.
- Facilitan la **búsqueda rápida** de elementos.

---

### Ejemplo con objetos en Java

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

  public int getAge() {
    return age;
  }
}

// Uso
Person p1 = new Person("Ana", 30);
System.out.println("Name: " + p1.getName());
System.out.println("Age: " + p1.getAge());
```

Acá:

- `Person` es un **objeto** que agrupa datos (`name`, `age`) y métodos (`getName()`, `getAge()`).
- Internamente, estos datos se pueden ver como un **mapa clave-valor** (`name`: "Ana", `age`: 30).

---

### Ejemplo con `HashMap` en Java

```java
import java.util.HashMap;
import java.util.Map;

public class Example {
  public static void main(String[] args) {
    Map<String, String> capitals = new HashMap<>();

    capitals.put("Argentina", "Buenos Aires");
    capitals.put("Chile", "Santiago");
    capitals.put("Perú", "Lima");

    System.out.println("Capital de chile: " + capitals.get("Chile"));
  }
}
```

- `Map` es una estructura asociativa pura: Cada clave tiene un valor único.
- Acceso mediante la clave, no mediante posición.

---

## Tipos de datos estructurados calculables (Vectores)

### Concepto

Un **tipo de dato estructurado calculable** almacena elementos en posiciones ordenadas y numeradas (índices).

En Java, esto se representa con **arreglos (`arrays`)** o listas indexadas.

El acceso a un elemento se hace mediante un **índice numérico** que comienza en **0**.

---

### Características principales

- Acceso rápido a un elemento conociendo su índice.
- Los elementos están almacenados de forma **contigua** en memoria.
- Los índices permiten realizar **recorridos secuenciales** y **operaciones matemáticas** sobre los elementos.
- Son ideales para datos **homogéneos** (del mismo tipo).

---

### Ejemplo de vector en Java

```java
public class Example {
  public static void main(String[] args) {
    int[] numbers = {10, 20, 30, 40, 50};

    System.out.println("First element: " + numbers[0]);

    for (int i = 0; i < numbers.length; i++) {
      System.out.println("Element in position " + i + ": " + numbers[i]);
    }
  }
}
```

Acá:

- `numbers` es un **vector** de enteros.
- El acceso se hace mediante un **índice numérico** (`numbers[0]`, `numbers[1]`, etc.).

---

### Operaciones comunes en vectores

- Recorrido secuencual con bucles.
- Búsqueda de elementos por posición.
- Cálculo de sumas, promedios o máximos.
- Ordenamiento.

**Ejemplo**: Suma de elementos.

```java
int total = 0;

for (int num : numbers) {
  total += num;
}

System.out.println("Total addition: " + total);
```

---

## Comparación entre asociativos y calculables

| **Característica**     | **Asociativos (Objetos/Map)**       | **Calculables (Vectores)**              |
| ---------------------- | ----------------------------------- | --------------------------------------- |
| Acceso                 | Por clave                           | Por índice numérico                     |
| Organización           | No necesariamente ordenada          | Ordenada secuencialmente                |
| Uso típico             | Representar entidades y propiedades | Listas de datos numéricos u homogéneos  |
| Ejemplos en Java       | `HashMap`, `TreeMap`, objetos       | Arrays, `ArrayList`                     |
| Velocidad de búsqueda  | Muy rápido por clave                | Muy rápido por índice                   |
| Flexibilidad de tamaño | Depende de la implementación        | Fijo en arrays, dinámico en `ArrayList` |

---

## Ejemplo integrador

```java
import java.util.HashMap;
import java.util.Map;

public class Library {
  public static void main(String[] args) {
    // Estructura asociativa: Map
    Map<String, String> books = new HashMap<>();
    books.put("978-3-16-148410-0", "El Quijote");
    books.put("978-0-14-044913-6", "La Odisea");

    System.out.println("Book with ISBN ISBN 978-3-16-148410-0: " + books.get("978-3-16-148410-0"));

    // Estructura calculable: Vector
    String[] categories = {"Novel", "Poetry", "Essay"};

    System.out.println("First category: " + categories[0]);
  }
}
```

En este caso:

- **Asociativo**: `books` almacena datos en forma de **clave (ISBN)** - **valor (título)**.
- **Calculable**: `categories` es un vector que almacena datos ordenados por índice.

---

## Conclusión

- Los **tipos de datos estructurados asociativos** (como objetos y `Map`) permiten almacenar información en **pares clave-valor**, ideales para búsquedas rápidas y representación de entidades.
- Los **tipos de datos estructurados calculables** (vectores o arrays) permiten organizar datos de forma **secuencial**, ideales para cálculos y recorridos.
- Ambos son esenciales para modelar y resolver problemas en Java, y su elección depende del tipo de acceso y organización que se requiera.
