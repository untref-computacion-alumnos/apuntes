# Polimorfismo

## Definición

El **polimorfismo** es un principio fundamental de la **programación orientada a objetos (POO)** que significa _"muchas formas"_.

Se refiere a la capacidad que tienen los objetos de diferentes clases de responder a un mismo mensaje (método) de distintas maneras.

En otras palabras, el polimorfismo permite que un mismo método pueda tener **diferentes implementaciones** dependiendo del objeto que lo invoque.

---

## Importancia

- Promueve la **flexibilidad** y **reutilización de código**.
- Facilita la **extensibilidad**, ya que se pueden añadir nuevas clases sin modificar el código existente.
- Permite **programar para una interfaz** y no para una implementación concreta.
- Hace posible escribir código más **genérico** y **mantenible**.

---

## Tipos de Polimorfismo

En Java (y en otros lenguajes orientados a objetos), existen dos tipos principales:

### Polimorfismo en tiempo de compilación (Sobrecarga)

- Se da cuando **métodos con el mismo nombre** tienen **parámetros distintos** (tipo o número).
- Se resuelve en el momento de la **compilación**.
- Ejemplo típico: sobrecarga de constructores o de métodos matemáticos.

### Polimorfismo en tiempo de ejecución (Sobrescritura)

- Se da cuando una **subclase redefine un método** ya definido en la clase padre.
- Se resuelve en el momento de la **ejecución**, dependiendo del tipo real del objeto.
- Ejemplo típico: métodos que se comportan distinto según la clase concreta del objeto.

---

## Ejemplo de Polimorfismo en Java

### Polimorfismo en tiempo de compilación (sobrecarga)

```java
class Calculator {
  // Método para sumar enteros
  int add(int a, int b) {
    return a + b;
  }

  // Método para sumar decimales (sobrecarga)
  double add(double a, double b) {
    return a + b;
  }

  // Método para sumar tres números (sobrecarga)
  int add(int a, int b, int c) {
    return a + b + c;
  }
}

public class Main {
  public static void main(String[] args) {
    Calculator calc = new Calculator();
    System.out.println(calc.add(5, 10));    // usa add(int, int)
    System.out.println(calc.add(2.5, 3.7)); // usa add(double, double)
    System.out.println(calc.add(1, 2, 3));  // usa add(int, int, int)
  }
}
```

---

### Polimorfismo en tiempo de ejecución (sobrescritura)

```java
class Animal {
  void sound() {
    System.out.println("The animal makes a sound");
  }
}

class Dog extends Animal {
  @Override
  void sound() {
    System.out.println("The dog barks");
  }
}

class Cat extends Animal {
  @Override
  void sound() {
    System.out.println("The cat meows");
  }
}

public class Main {
  public static void main(String[] args) {
    Animal a1 = new Dog();  // objeto Dog visto como Animal
    Animal a2 = new Cat();  // objeto Cat visto como Animal

    a1.sound(); // imprime "The dog barks"
    a2.sound(); // imprime "The cat meows"
  }
}
```

En este ejemplo:

- El método `sound()` está definido en la superclase `Animal`.
- Cada subclase (`Dog` y `Cat`) sobrescribe ese método con su propia implementación.
- Aunque el tipo de las variables (`a1`, `a2`) es `Animal`, la ejecución depende del tipo real del objeto (Dog o Cat). Esto es **polimorfismo dinámico**.

---

## Polimorfismo con Interfaces

En Java, el polimorfismo también se logra usando **interfaces**:

```java
interface Figure {
  double area();
}

class Circle implements Figure {
  double radio;

  Circle(double radio) {
    this.radio = radio;
  }

  public double area() {
    return Math.PI * radio * radio;
  }
}

class Rectangle implements Figure {
  double width, high;

  Rectangle(double width, double high) {
    this.width = width;
    this.high = high;
  }

  public double area() {
    return width * high;
  }
}

public class Main {
  public static void main(String[] args) {
    Figure f1 = new Circle(5);
    Figure f2 = new Rectangle(4, 6);

    System.out.println("Area of the circle: " + f1.area());
    System.out.println("Area of the rectangle: " + f2.area());
  }
}
```

Acá:

- `Figure` define un contrato (`area()`).
- `Circle` y `Rectangle` lo implementan con sus propias fórmulas.
- Gracias al polimorfismo, podemos trabajar con el tipo `Figure` sin importar la clase concreta.

---

## Beneficios del Polimorfismo

- **Código genérico**: Permite trabajar con superclases o interfaces en lugar de clases específicas.
- **Extensibilidad**: Se pueden añadir nuevas clases sin modificar el código existente.
- **Mantenibilidad**: Se reduce la duplicación de código.
- **Flexibilidad**: Permite reemplazar comportamientos en tiempo de ejecución.

---

## Resumen

- El polimorfismo permite que **un mismo método tenga diferentes implementaciones** según el objeto.
- Existen dos tipos principales:

  - **Sobrecarga (tiempo de compilación)**
  - **Sobrescritura (tiempo de ejecución)**

- También se logra mediante **interfaces**.
- Es un pilar fundamental junto con **encapsulamiento** y **herencia** en la POO.
