# Organización de la memoria

En programación, la **organización de la memoria** describe cómo un sistema computacional distribuye y administra la memoria para almacenar **datos, instrucciones y estructuras internas** durante la ejecución de un programa.

En Java, la memoria está organizada en **áreas bien definidas** que gestionan:

- Variables y objetos.
- Información de ejecución.
- Recursos temporales y permanentes.

Comprender esta organización sirve para:

- Optimizar el uso de recursos.
- Evitar errores como fugas de memoria (_memory leak_).
- Mejorar el rendimiento del software.

---

## Tipos principales de memoria en un programa Java

Java gestiona la memoria automáticamente mediante la **JVM ([Java Virtual Machine](http://en.wikipedia.org/wiki/Java_virtual_machine))**, que divide la memoria en distintas zonas:

- **Stack (Pila de ejecución)**.
- **Heap (Montículo de objetos)**.
- **Method Area (o Metaspace en versiones modernas)**.
- **PC Registers** y **Native Method Stack** (zonas internas de la JVM).

---

## Stack

### Características

- Almacena variables **locales** y **referencias** a objetos.
- Crece y disminuye automáticamente con las llamadas y retornos de métodos.
- Cada hilo (_thread_) tiene su propia pila independiente.
- Muy rápida pero limitada en tamaño.

### Ejemplo en Java

```java
public class Example {
  public static void main(String[] args) {
    int x = 5;                // Variable local en stack.
    int y = addition(x, 10);  // Llamada a método crea un nuevo frame en stack.
  }

  public static int addition(int a, int b) {
    int result = a + b;       // Variable local en stack.
    return result;            // El frame se elimina al retornar.
  }
}
```

Cuando `addition()` termina, su **frame** en el stack se libera y las variables locales dejan de existir.

## Heap

### Características

- Zona donde se almacenan **objetos** y **arrays** en tiempo de ejecución.
- Compartida por todos los hilos.
- Administrada por el [**Garbage Collector**](https://www.ibm.com/mx-es/topics/garbage-collection-java).
- Más lenta que la pila, pero mucho más grande.

### Ejemplo en Java

```java
public class Example {
  public static void main(String[] args) {
    Person p1 = new Person("Ana");  // Objeto en heap.
    Person p2 = new Person("Luis"); // Otro objeto en heap.
  }
}

public class Person {
  private String name;

  public Person(String name) {
    this.name = name;
  }
}
```

> Las referencias `p1` y `p2` están en el stack, pero los objetos `Person` están en el heap.

---

## Method Area / Metaspace

### Características

- Almacenan **información sobre clases**, métodos y constantes.
- Contiene datos como:
  - Código de métodos compilados.
  - Nombres de clases.
  - Constantes literales (`final`).
- En Java 8 y posteriores se reemplazó `PermGen` por `Metaspace`, que usa memoria nativa.

### Ejemplo conceptual

Cuando se carga una clase:

```java
class Example {
  static final double PI = 3.14159;
}
```

> La constante `PI` y la estructura interna de `Example` se almacenan en la **Method Area**.

---

## PC Registers y Native Method Stack

### PC Registers

- Cada hilo tiene un contador de programa (Program Counter).
- Guarda la dirección de la instrucción que se está ejecutando.

### Native Method Stack

- Soporta ejecución de métodos nativos (no escritos en Java, por ejemplo, en C/C++).
- Se gestiona fuera del heap y stack de Java.

---

## Ciclo de vida de los datos

1. **Declaración**: Se reserva espacio en stack o heap.
2. **Asignación**: Se inicializa con un valor.
3. **Uso**: Se accede/modifica según sea necesario.
4. **Liberación**:
   - Variables locales: Al salir del bloque (stack).
   - Objetos: Liberados por el Garballe Collector (heap).

---

## Garbage Collector (GC)

### Función

- Libera automáticamente la memoria de objetos **sin referencias activas**.
- Evita fugas de memoria.
- Se ejecuta de forma automática, pero se puede sugerir con:

  ```java
  System.gc();
  ```

  > Nota: `System.gc()` no garantiza ejecución inmediata.

### Ejemplo

```java
public class Example {
  public static void main(String[] args) {
    Person p = new Person("Juan");
    p = null;     // El objeto queda sin referencia.
    System.gc();  // Se sugiere ejecución del GC.
  }
}
```

---

## Comparación de Stack y Heap

| **Características** | **Stack**                      | **Heap**                       |
| ------------------- | ------------------------------ | ------------------------------ |
| Contenido           | Variables locales, referencias | Objetos y arrays               |
| Acceso              | Muy rápido                     | Más lento                      |
| Tamaño              | Limitado                       | Mucho mayor                    |
| Gestión             | Automática (marcos de pila)    | Garbage Collector              |
| Tiempo de vida      | Hasta que termina el bloque    | Hasta que no hayan referencias |

---

## Buenas prácticas de uso de memoria

- Evitar la creación innecesaria de objetos.
- Usar **variables locales** siempre que sea posible.
- Liberar referencias cuando un objeto ya no se use.
- Preferir **tipos primitivos** (`int`, `double`) cuando no sea necesaria la complejidad de objetos.
- Usar **estructuras de datos adecuadas** para evitar desperdicio de memoria.

---

## Resumen visual de la organización de la memoria en Java

```text
┌──────────────────────────────────────────────┐
│                JVM Memory                    │
├──────────────────────────────────────────────┤
│  Method Area / Metaspace                     │
│    - Información de clases                   │
│    - Constantes                              │
│    - Métodos                                 │
├──────────────────────────────────────────────┤
│  Heap                                        │
│    - Objetos                                 │
│    - Arrays                                  │
├──────────────────────────────────────────────┤
│  Stack (por hilo)                            │
│    - Variables locales                       │
│    - Referencias a objetos                   │
├──────────────────────────────────────────────┤
│  PC Registers                                │
│  Native Method Stack                         │
└──────────────────────────────────────────────┘
```

---

## Conclusión

La **organización de la memoria** en Java permite:

- Una separación clara entre datos temporales (stack) y permanentes (heap).
- Gestión automática de recursos mediante el Garballe Collector.
- Aislamiento entre hilos gracias a pilas independientes.

Se debe entender **qué parte del programa se almacena en cada zona** para escribir código más eficiente, evitar errores y optimizar el uso de recursos.
