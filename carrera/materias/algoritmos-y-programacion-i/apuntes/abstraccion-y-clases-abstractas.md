# Abstracción y Clases Abstractas en Java

## Introducción a la Abstracción

La **abstracción** es un principio fundamental de la **Programación Orientada a Objetos (POO)**.

Consiste en **ocultar los detalles de implementación** de un objeto y mostrar únicamente lo que es relevante para su uso.

En otras palabras:

- Permite **enfocarse en el "qué hace" un objeto** y no en "cómo lo hace".
- Facilita la **simplicidad**, la **reutilización** y la **modularidad** del código.

Ejemplo de abstracción en la vida real:

Un **teléfono móvil**: el usuario sabe que puede llamar, enviar mensajes y sacar fotos, pero no necesita conocer los circuitos internos ni la lógica que hace posible esas funciones.

---

## Abstracción en Java

En Java, la abstracción se logra de dos formas principales:

1. **Interfaces**
2. **Clases abstractas**

---

## Clases Abstractas

### Definición

Una **clase abstracta** es una clase que:

- Puede contener **métodos abstractos** (sin implementación).
- Puede contener **métodos concretos** (con implementación).
- **No se puede instanciar directamente** (no se puede crear un objeto a partir de ella).
- Se utiliza como **base para otras clases** que la heredan.

Se declara con la palabra clave `abstract`:

```java
abstract class Animal {
  // Método abstracto (sin implementación)
  abstract void makeSound();

  // Método concreto (con implementación)
  void sleep() {
    System.out.println("Zzz...");
  }
}
```

---

### Métodos Abstractos

- Se declaran sin cuerpo.
- Fuerzan a las subclases a proporcionar su propia implementación.

Ejemplo:

```java
abstract class Vehicle {
  abstract void mover();
}

class Car extends Vehicle {
  @Override
  void mover() {
    System.out.println("The car moves on 4 wheels.");
  }
}

class Bicycle extends Vehicle {
  @Override
  void mover() {
    System.out.println("The bicycle moves forward by pedaling.");
  }
}
```

---

### ¿Características principales

- Una clase abstracta puede tener:

  - **Variables de instancia**.
  - **Constructores**.
  - **Métodos abstractos**.
  - **Métodos concretos**.

- Puede heredar de otra clase (abstracta o no).
- Puede implementar interfaces.
- Las subclases concretas **deben implementar todos los métodos abstractos**, salvo que ellas mismas sean abstractas.

---

## Diferencias entre Clase Abstracta e Interfaz

| Aspecto           | Clase Abstracta                                                       | Interfaz                                                                     |
| ----------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Instanciación** | No se puede instanciar                                                | No se puede instanciar                                                       |
| **Métodos**       | Puede tener abstractos y concretos                                    | Antes de Java 8: solo abstractos. Desde Java 8: también `default` y `static` |
| **Constructores** | Sí puede tener                                                        | No puede tener                                                               |
| **Herencia**      | Una clase solo puede heredar de una clase abstracta (herencia simple) | Una clase puede implementar múltiples interfaces                             |
| **Variables**     | Puede tener atributos con modificadores de acceso                     | Solo constantes (`public static final`)                                      |

---

## Ejemplo Completo

```java
// Clase abstracta
abstract class Figure {
  String color;

  Figure(String color) {
    this.color = color;
  }

  // Método abstracto
  abstract double area();

  // Método concreto
  void showColor() {
    System.out.println("Color: " + color);
  }
}

// Subclase concreta
class Circle extends Figure {
  double radio;

  Circle(String color, double radio) {
    super(color);
    this.radio = radio;
  }

  @Override
  double area() {
    return Math.PI * radio * radio;
  }
}

// Otra subclase concreta
class Rectangle extends Figure {
  double base, height;

  Rectangle(String color, double base, double height) {
    super(color);
    this.base = base;
    this.height = height;
  }

  @Override
  double area() {
    return base * height;
  }
}

// Programa principal
public class Main {
  public static void main(String[] args) {
    Figure f1 = new Circle("Red", 5);
    Figure f2 = new Rectangle("Blue", 4, 6);

    f1.showColor();
    System.out.println("Area: " + f1.area());

    f2.showColor();
    System.out.println("Area: " + f2.area());
  }
}
```

**Salida**:

```text
Color: Red
Área: 78.53981633974483
Color: Blue
Área: 24.0
```

---

## Ventajas de la Abstracción con Clases Abstractas

1. **Reutilización de código**: Los métodos concretos se heredan sin necesidad de reescribirlos.
2. **Flexibilidad**: Se pueden definir métodos genéricos y dejar que las subclases decidan cómo implementarlos.
3. **Mantenimiento más sencillo**: Facilita agregar nuevas clases sin modificar el código existente.
4. **Organización del diseño**: Representa de manera clara conceptos jerárquicos.

---

## Resumen

- La **abstracción** permite enfocarse en _qué hace_ un objeto, ocultando el _cómo lo hace_.
- En Java, la abstracción se implementa con **interfaces** y **clases abstractas**.
- Una **clase abstracta**:

  - Puede tener métodos abstractos y concretos.
  - No se puede instanciar directamente.
  - Sirve como plantilla para otras clases.

- Favorece el diseño limpio, modular y extensible de programas orientados a objetos.
