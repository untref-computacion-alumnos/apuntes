# Atributos, parámetros y argumentos

Es fundamental comprender la diferencia entre **atributos**, **parámetros** y **argumentos**, ya que representan conceptos reacionados con el manejo y transmisión de datos dentro de un programa, pero cumplen funciones distintas.

---

## Atributos

### Definición

Un **atributo** (también llamado _campo_ o _variable de instancia_) es una **variable asociada a un objeto o clase** que almacena información sobre su estado.

En Java:

- Si pertenece a un objeto, **variable de instancia**.
- Si pertenece a la clase y es común a todos los objetos, **variable de clase** (`static`).

### Características

- Se declaran dentro de la clase, pero fuera de cualquier método o constructor.
- Pueden tener modificadores de acceso (`private`, `protected`, `public`).
- Pueden ser **primitivos** (`int`, `double`, etc.) o **referencias** a objetos.
- Su valor puede cambiar durante la vida del objeto.

### Ejemplo

```java
public class Person {
  private String name;                  // Atributo (variable de instancia).
  private int age;                      // Atributo (variable de instancia).

  public static int personsAmount = 0;  // Atributo de clase (estático).

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
    personsAmout++;
  }
}
```

Acá:

- `name` y `age` son atributos propios de cada objeto.
- `personsAmount` es un atributo compartido por toda la clase.

---

## Parámetros

### Definición

Un **parámetro** es una **variable declarada en la definición de un método o constructor**, que recibe un valor cuando dicho método o constructor es invocado.

### Características

- Se usan para **recibir datos** desde fuera del método.
- Se definen **entre paréntesis** en la declaración del método.
- Pueden ser de **tipo primitivo** o **tipo objeto**.
- Pueden ser:
  - **Por valor** (tipos primitivos en Java).
  - **Por referencia** (objetos en Java; lo que se pasa es la referencia, no una copia del objeto).

### Ejemplo

```java
public void greet(String greeting) {
  System.out.println(greeting + ", " + name);
}
```

Acá:

- `greeting` es un **parámetro** del método `greet`.

---

## Argumentos

### Definición

Un **argumento** es el **valor concreto** que se pasa a un parámetro cuando se llama a un método o constructor.

### Características

- Es el dato real que se envía.
- Puede ser una **variable**, **literal** o **resultado de una expresión**.
- Debe coincidir en tipo (o ser compatible) con el parámetro correspondiente..

### Ejemplo

```java
Person p = new Person("Juan", 30);
p.greet("Hello");
```

Acá:

- `"Juan"` y `30` son **argumentos** del constructor `Person`.
- `"Hello"` es un **argumento** del método `greet`.

---

## Diferencias entre atributos, parámetros y argumentos

| **Característica** | **Atributo**                             | **Parámetro**                              | **Argumento**                           |
| ------------------ | ---------------------------------------- | ------------------------------------------ | --------------------------------------- |
| Dónde se define    | Dentro de la clase, fuera de los métodos | En la declaración del método o constructor | Al invocar el método o constructor      |
| Quién lo asigna    | El propio objeto o la clase              | El código que llama al método              | El programador o el flujo del programa  |
| Ámbito             | Vida del objeto o clase                  | Vida durante la ejecución del método       | Depende de la expresión o valor enviado |
| Ejemplo            | `private String name;`                   | `String saludo`                            | `"Hola"`                                |

---

## Ejemplo integrador en Java

```java
public class Car {
  private String brand; // Atributo.
  private int speed;    // Atributo.

  // Constructor con parámetros.
  public Car(String brand, int speed) {
    // Se usa 'this' para diferenciar atributo de parámetro.
    this.brand = brand;
    this.speed = speed;
  }

  // Método con parámetro.
  public void accelerate(int increase) {
    this.speed += increase;
  }

  // Método sin parámetros.
  public void showData() {
    System.out.println("Brand: " + brand + ", Speed: " + speed + " km/h");
  }

  public static void main(String[] args) {
    Car myCar = new Car("Toyota", 0); // Argumentos enviados al constructor.
    myCar.accelerate(50);             // Argumento enviado al método.
    myCar.showData();                 // Sin argumentos.
  }
}
```

En este ejemplo:

- **Atributos**: `brand`, `speed`.
- **Parámetros**: `brand`, `speed` (constructor), `increase` (método `accelerate`).
- **Argumentos**: `"Toyota"`, `0`, `50` (valores enviados en llamadas).

---

## Paso de parámetros en Java

En Java, **todo se pasa por valor**:

- En tipos primitivos se pasa una copia del valor.
- En objetos se pasa una copia de la referencia (por lo que los métodos pueden modificar el contenido del objeto, pero no cambiar la referencia original).

Ejemplo:

```java
public void changeName(Person p) {
  p.setName("New name");              // Cambia el atributo del objeto.
}

public void changeReference(Person p) {
  p = new Person("Another name", 25); // Cambia referencia local, no afecta afuera.
}
```

---

## Buenas prácticas

- Usar **nombres claros y descriptivos** para atributos y parámetros.
- No abusar de atributos estáticos, salvo para valores constantes.
- Limitar el alcance de los atributos (preferir `private` + getters/setters).
- Mantener los parámetros mínimos necesarios para un método.
- Evitar el uso excesivo de parámetros (si son muchos, considerar agrupar en una clase).

---

## Resumen gráfico

```text
Clase: Person
------------------------------------------
Atributos:
- name : String
- age : int

Método: greet(parámetro: String greeting)
------------------------------------------
Llamada:
person.greet(argumento: "Hello")
```

- **Atributo**: Variable propia del objeto (estado).
- **Parámetro**: Variable definida en el método para recibir un valor.
- **Argumento**: Valor real pasado al invocar el método.
