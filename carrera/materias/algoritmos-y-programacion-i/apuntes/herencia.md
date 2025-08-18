# Herencia

## Introducción

La **herencia** es uno de los **pilares fundamentales de la Programación Orientada a Objetos (POO)** junto con la abstracción, el polimorfismo y el encapsulamiento.

Permite que una clase (**subclase** o **clase hija**) pueda **reutilizar y extender** los atributos y métodos de otra clase (**superclase** o **clase padre**).

La idea principal es modelar relaciones del tipo **"es un(a)"**.

Por ejemplo:

- Un **Perro** es un **Animal**.
- Un **Círculo** es una **FiguraGeometrica**.

Esto favorece la **reutilización de código**, la **organización jerárquica** y la **extensibilidad** de los programas.

---

## Conceptos Fundamentales

- **Superclase (o clase base)**: La clase que contiene los atributos y métodos comunes.
- **Subclase (o clase derivada)**: Clase que hereda de otra y puede añadir nuevas características o redefinir las heredadas.
- **Palabra clave `extends` (Java)**: Se utiliza para indicar que una clase hereda de otra.
- **Acceso a miembros heredados**:
  - Una subclase **hereda** todos los atributos y métodos **no privados** de la superclase.
  - Puede **agregar** atributos o métodos adicionales.
  - Puede **sobrescribir** métodos de la superclase.

---

## Ventajas de la Herencia

1. **Reutilización de código**: No es necesario volver a escribir atributos y métodos comunes.
2. **Extensibilidad**: Permite añadir funcionalidades a partir de clases ya existentes.
3. **Organización jerárquica**: Facilita la representación de relaciones reales en forma de árboles jerárquicos.
4. **Polimorfismo**: Permite tratar objetos de diferentes subclases como si fueran de la superclase.
5. **Mantenimiento más sencillo**: Cambios en la superclase impactan automáticamente en las subclases.

---

## Sintaxis de la Herencia en Java

### Ejemplo básico

```java
class Animal {
  String name;

  void eat() {
    System.out.println(name + " is eating.");
  }
}

class Dog extends Animal {
  void bark() {
    System.out.println(name + " is barking.");
  }
}

// Uso
public class Main {
  public static void main(String[] args) {
    Dog p = new Dog();
    p.name = "Firulais";
    p.eat();  // Método heredado
    p.bark(); // Método propio
  }
}
```

### Salida

```text
Firulais is eating.
Firulais is barking.
```

---

## El constructor y la palabra clave `super`

- En Java, los constructores **no se heredan**, pero la subclase puede llamar al constructor de la superclase con `super()`.
- `super` también se usa para acceder a métodos y atributos de la superclase.

```java
class Animal {
  String name;

  Animal(String name) {
    this.name = name;
  }

  void eat() {
    System.out.println(name + " is eating.");
  }
}

class Dog extends Animal {
  String race;

  Dog(String name, String race) {
    super(name);  // Llamada al constructor de Animal
    this.race = race;
  }

  void showInformation() {
    System.out.println("Nombre: " + name + ", Raza: " + race);
  }
}

public class Main {
  public static void main(String[] args) {
    Dog p = new Dog("Rocky", "Bulldog");
    p.eat();
    p.showInformation();
  }
}
```

---

## Sobreescritura de métodos (Override)

Una subclase puede **redefinir** un método de la superclase para adaptarlo a sus necesidades.

- Se usa la anotación `@Override` para mayor claridad.
- El método debe tener la **misma firma** (nombre, parámetros y tipo de retorno compatible).

```java
class Animal {
  void makeSound() {
    System.out.println("The animal makes a sound.");
  }
}

class Dog extends Animal {
  @Override
  void makeSound() {
    System.out.println("The dog barks.");
  }
}

public class Main {
  public static void main(String[] args) {
    Animal a = new Dog();
    a.makeSound();  // Ejecuta el método sobreescrito
  }
}
```

### Salida

```text
The dog barks.
```

---

## Tipos de Herencia

### Herencia simple

Una clase hereda de una sola superclase.

Java **solo permite herencia simple** entre clases (no múltiple).

```java
class A { ... }

class B extends A { ... }
```

### Herencia multinivel

Una clase hereda de otra, que a su vez hereda de otra.

```java
class A { ... }

class B extends A { ... }

class C extends B { ... }
```

### Herencia jerárquica

Varias clases heredan de la misma superclase.

```java
class Animal { ... }

class Dog extends Animal { ... }

class Gato extends Animal { ... }
```

### Herencia múltiple (prohibida en clases, pero posible con interfaces)

Java evita conflictos de ambigüedad no permitiendo herencia múltiple entre clases.

Para lograrla se usan **interfaces**.

---

## Herencia y Polimorfismo

La herencia habilita el **polimorfismo**, que permite que un objeto de una subclase sea tratado como uno de su superclase.

Esto es útil para trabajar con **colecciones de objetos heterogéneos**.

```java
class Animal {
  void makeSound() {
    System.out.println("Generic sound");
  }
}

class Dog extends Animal {
  @Override
  void makeSound() {
    System.out.println("Guau!");
  }
}

class Gato extends Animal {
  @Override
  void makeSound() {
    System.out.println("Miau!");
  }
}

public class Main {
  public static void main(String[] args) {
    Animal[] animals = { new Dog(), new Gato() };

    for (Animal a : animals) {
      a.makeSound();  // Comportamiento diferente según el tipo real
    }
  }
}
```

### Salida

```text
Guau!
Miau!
```

---

## Modificadores de Acceso y Herencia

- **public**: Accesible desde cualquier lugar.
- **protected**: Accesible en la misma clase, paquete y subclases.
- **(default)**: Accesible solo en el mismo paquete.
- **private**: **No se hereda** directamente.

Ejemplo:

```java
class Person {
  private String dni;     // No accesible en subclases
  protected String name;  // Sí accesible en subclases
  public int age;         // Accesible desde cualquier lugar
}
```

---

## Limitaciones y Buenas Prácticas

### Limitaciones

- Java no permite herencia múltiple de clases (sí de interfaces).
- Un exceso de herencia puede complicar la jerarquía y reducir la flexibilidad.

### Buenas prácticas

1. Usar herencia solo cuando haya una clara relación **"es un(a)"**.
2. Evitar jerarquías muy profundas.
3. Preferir **composición** antes que herencia si la relación es **"tiene un(a)"**.
4. Usar la anotación `@Override` para evitar errores de sobreescritura.
5. Diseñar superclases lo más genéricas posible.

---

## Conclusión

La herencia es una poderosa herramienta de la POO que permite crear jerarquías de clases, **reutilizar código** y habilitar el **polimorfismo**.

En Java, se implementa mediante la palabra clave `extends` y está limitada a la **herencia simple** entre clases, aunque permite herencia múltiple a través de interfaces.

Usada correctamente, la herencia mejora la organización, la reutilización y la extensibilidad de los programas.
