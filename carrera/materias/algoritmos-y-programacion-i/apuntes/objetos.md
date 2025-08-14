# Objetos

## Definición

En _programación orientada a objetos_, un **objeto** es una **entidad que combina estado y comportamiento**.

Esta compuesto por:

- **Atributos**: Representan el estado del objeto (datos almacenados).
- **Métodos**: Representan el comportamiento del objeto (acciones que puede realizar).

Los objetos son **instancias de clases**.

Una **clase** actúa como un molde o plantilla que defime _cómo_ serán los objetos creados a partir de ella.

---

## Relación entre clase y objeto

- **Clase**: Descripción abstracta (molde).
- **Objeto**: Instancia concreta de esa descripción.

**Ejemplo en Java**:

```java
// Clase: Define atributos y métodos.
public class Person {
  String name;  // Atributo: nombre de la persona.
  int age;       // Atributo: edad de la persona.

  // Constructor: Instancia la clase al momento de ser llamado.
  public Person() {
    super();
  }

  // Método: comportamiento del objeto (la persona).
  void greet() {
    System.out.println("Hello, I am " + name);
  }
}

public class Main {
  public static void main(String[] args) {
    Person p1 = new Person(); // 'p1' es un objeto, la instancia de la clase 'Person'.
    p1.name = "Ana";
    p1.age = 25;
    p1.greet(); // Salida: Hello, I am Ana

    Person p2 = new Person(); // 'p2' es un objeto, otra instancia de la clase 'Person'.
    p2.name = "Luis";
    p2.age = 30;
    p2.greet(); // Salida: Hello, I am Luis
  }
}
```

---

## Componentes de un objeto

### Atributos

- Variables que guardan el estado del objeto.
- Pueden ser de cualquier tipo de dato, ya sea primitivo o referencia.
- Su visibilidad se controla con **modificadores de acceso** (`private`, `public`, `protected`).

**Ejemplo**:

```java
// Los atributos tienen que ser privados.
private String name;
private int age;
```

### Métodos

- Definen el comportamiento del objeto.
- Pueden acceder y modificar los atributos.
- Pueden devolver valores o no (`void`, traducido literal como _vacio_).

**Ejemplo**:

```java
// 'public' indica que el método es público.
// 'void' indica que el método no retorna ningún dato.
public void birthday() {
  age++; // '++' incrementa el valor de la variable 'age' en 1.
}
```

---

## Creación y uso de objetos en Java

Para crear un objeto se utiliza la palabra reservada `new` seguida del constructor de la clase.

```java
// Tipo de variable - Nombre de la variable - Palabra reservada 'new' - Constructor de la clase
Person p = new Person();
```

**Paso a paso**:

1. **Declaración**: `Person p` crea una referencia a un objeto de tipo Person.
2. **Instanciación**: `new Person()` crea un objeto en memoria.
3. **Asignación**: `p = new Person()` la referencia `p` apunta al nuevo objeto.

---

## Constructores

Un **constructor** es un método especial que se ejecuta al crear un objeto.

Sirve para inicializar sus atributos.

**Ejemplo**:

```java
public class Person {
  private String name;
  private int age;

  // Constructor: Se le pasan los parámetros al momento de instanciarlo para cambiar los atributos sin exponerlos.
  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }
}

// Uso
Person p = new Person("Ana", 25);
```

---

## Encapsulamiento

El **encapsulamiento** consiste en ocultar los atributos internos y exponer solo lo necesario a través de métodos públicos denominados _getters_ y _setters_.

**Ejemplo**:

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
}
```

---

## Métodos especiales en objetos Java

### `toString()`

Devuelve una representación en texto del objeto.

```java
@Override
public String toString() {
  return "Person{name='" + name + "', age=" + age + "}";
}
```

### `equals()` y `hashCode()`

Permiten comparar objeto y usarlos en estructuras como `HashSet` o `HashMap`.

---

## Ciclo de vida de un objeto en Java

1. **Creación**: Usando `new`.
2. **Uso**: Mientras es referenciado por variables.
3. **Inalcanzable**: Cuando ninguna referencia apunta a él.
4. **Recolección de basura (Garballe Collection)**: Java libera automáticamente la memoria ocupada.

---

## Objetos y memoria en Java

En Java:

- **Atributos y métodos estáticos**: Almacenados en memoria **metaspace** (o área de clase).
- **Objetos**: Almacenados en **Heap**.
- **Variables de referencia**: Almacenadas en **Stack**.

---

## Ejemplo completo en Java

```java
public class Car {
  private String brand;
  private String model;
  private int speed;

  public Car(String brand, String model) {
    this.brand = brand;
    this.model = model;
    this.speed = 0;
  }

  public void accelerate(int increase) {
    speed += increase;
    System.out.println("Actual speed: " + speed + " km/h");
  }

  public void curb(int decrease) {
    speed -= decrease;
    if (speed < 0) {
      speed = 0;
    }
    System.out.println("Actual speed: " + speed + " km/h");
  }

  @Override
  public String toString() {
    return brand + " " + model + " (" + speed + " km/h)";
  }
}
```

---

## Beneficios de trabajar con objetos

- **Modularidad**: Se divide el programa en componentes independientes.
- **Reutilización**: Se pueden crear múltiples instancias de una misma clase.
- **Mantenibilidad**: Cambios en una clase afectan a todos sus objetos de manera controlada.
- **Abstracción**: El usuario de un objeto no necesita conocer su implementación interna.
- **Escalabilidad**: Facilita el crecimiento de aplicaciones complejas.

---

## Conclusión

Un **objeto** es la unidad básica de la programación orientada a objetos.

A través de atributos y objetos, encapsula datos y comportamientos, permitiendo construir programas más claros, organizados y fáciles de mantener.

Comprender cómo se crean, usan y destruyen los objetos es esencial para dominar el paradigma orientado a objetos.
