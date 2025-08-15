# Referencias

En la programación orientada a objetos, especialmente en Java, una **referencia** es una variable que **almacena la dirección en memoria** de un objeto, y no el objeto en sí.

Cuando se trabaja con objetos en Java, las variables no contienen directamente los datos del objeto, sino una referencia que apunta a su ubicación en el **heap** (memoria dinámica).

---

## Concepto básico

En Java:

- **Tipos primitivos** (`int`, `double`, `boolean`, etc.): La variable almacena directamente el valor.
- **Tipos objeto** (cualquier clase): La variable almacena **una referencia** a la ubicación del objeto en memoria.

> Esto significa que **dos variables pueden apuntar al mismo objeto** y, por lo tanto, modificarlo de forma compartida.

---

## Características de las referencias en Java

1. **No contienen el objeto, sino su dirección en memoria**.
2. **No se puede acceder directamente a la dirección de memoria** en Java (es manejada por la JVM).
3. Cuando se pasa un objeto como parámetro a un método, **se pasa la copia de la referencia**, no el objeto completo.
4. Una referencia puede:
   - Apuntar a un objeto.
   - Ser `null` (no apuntar a ningún objeto).
5. Si no hay ninguna referencia apuntando a un objeto, este queda disponible para el **Garballe Collector**.

---

## Declaración y uso de referencias

### Creación de un objeto y asignación de referencia

```java
Person p1 = new Person("Ana", 25);
```

- `p1` es una referencia que apunta al objeto `Person` creado en el heap.
- `"Ana"` y `25` son argumentos pasados al constructor.
- `new Person(...)` crea el objeto en memoria y retorna su referencia.

---

## Referencias múltiples

Es posible que varias referencias apunten al mismo objeto.

```java
Person p1 = new person("Luis", 30);
Person p2 = p1;                   // 'p2' apunta al mismo objeto que 'p1'.

p2.setName("Carlos");

System.out.println(p1.getName()); // Salida: Carlos
```

> En este ejemplo:
>
> - `p1` y `p2` **NO son dos objetos diferentes**, son dos referencias que apuntan al mismo objeto en memoria.
> - Cambiar el estado del objeto usando `p2` también afecta lo que vemos desde `p1`.

---

## Comparación de referencias

En Java existen dos formas de comparar objetos:

- **Por referencia (`==`)**: Compara si dos referencias apuntan al mismo objeto.
- **Por contenido (`.equals()`)**: Compara si el contenido del objeto es igual (si la clase lo define).

**Ejemplo**:

```java
Person p1 = new Person("Ana", 25);
Person p2 = p1;
Person p3 = new Person("Ana", 25);

System.out.println(p1 == p2);       // Salida: true (misma referencia).
System.out.println(p1 == p3);       // Salida: false (objetos distintos).
System.out.println(p1.equals(p3));  // Dependerá del 'equals()' en la clase 'Person'.
```

---

## Paso de referencias como parámetros

En Java, cuando pasamos un objeto a un método:

- Se pasa **la copia de la referencia**.
- El método puede modificar el objeto apuntado.
- No puede cambiar la referencia original fuera del método.

**Ejemplo**:

```java
public void changeName(Person person) {
  person.setName("New name");
}

public static void main(String[] args) {
  Person p = new Person("Luis", 30);
  changeName(p);
  System.out.println(p.getName());  // Salida: New name
}
```

> Acá el método `changeName()` modifica el **mismo objeto** al que apunta la referencia `p`.

---

## Referencia `null`

Una referencia puede estar **vacía** (`null`), lo que significa que no apunta a ningún objeto.

**Ejemplo**:

```java
Person p = null;

if (p == null) {
  System.out.println("The reference does not point to any object");
}
```

> Nota: Si se intenta acceder a métodos o atributos de una referencia `null`, se produce la excepción `NullPointerException`.

---

## Referencias y Garbage Collector

En Java, la gestión de memoria la realiza la **JVM**:

- Cuando un objeto no tiene **ninguna referencia** que lo apunte, se vuelve inaccesible.
- El **Garbage Collector (GC)** lo elimina de la memoria automáticamente.

**Ejemplo**:

```java
Person p1 = new Person("Ana", 25);
Person p2 = p1;

p1 = null;  // 'p2' todavía apunta al objeto, por lo tanto "sigue vivo".

p2 = null;  // Ahora el objeto ya no tiene referencias, por lo que el Garbage Collector lo elimina.
```

---

## Ejemplo completo

```java
class Person {
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
}

public class Example {
  public static void main(String[] args) {
    Person a = new Person("Juan", 20);  // Referencia a objeto.
    Person b = a;                       // Ambas referencias apuntan al mismo objeto.

    b.setName("Pedro");

    System.out.println(a.getName());    // Salida: Pedro

    a = null;                           // 'b' todavía apunta al objeto.
    System.out.println(b.getName());    // Salida: Pedro

    b = null;                           // Objeto ahora sin referencias, por lo que el Garbage Collector lo elimina.
  }
}
```

---

## Resumen gráfico

```text
Referencias → apuntan a objetos en memoria (heap)
+------------------------------------+
| Person p1                          |
|  └──> Objeto en heap {name, age}   |
+------------------------------------+

Tipos:
- Apuntando a objeto: Person p = new Person();
- Apuntando a null: Person p = null;
- Varias referencias al mismo objeto.
```

---

## Buenas prácticas con referencias

- Inicializar siempre las referencias antes de usarlas.
- Comprobar si una referencia es `null` antes de acceder a ella.
- Evitar mantener referencias innecesarias para permitir que el Garbage Collector libere memoria.
- Usar `equals()` en lugar de `==` cuando se compare el contenido de objetos.
- Ser consciente de que pasar objetos a métodos permite modificar su estado.

---

## Conclusión

Las **referencias** en Java son esenciales para trabajar con objetos, ya que permiten manipular estructuras complejas sin copiar toda su información.

Comprender cómo funcionan ayuda a evitar errores comunes como `NullPointerException` y facilita el manejo eficiente de la memoria.
