# Encapsulamiento

El **encapsulamiento** es uno de los **pilares fundamentales de la Programación Orientada a Objetos (POO)**.

Consiste en **ocultar** los detalles internos de un objeto y exponer únicamente la información y funcionalidades necesarias a través de una **interfaz pública**.

En otras palabras:

> El encapsulamiento protege los datos y asegura que solo puedan ser modificados de formas controladas.

---

## Concepto

- **Ocultamiento de información** (_Information Hiding_): Los atributos internos de un objeto no son accesibles directamente desde fuera.
- **Control de acceso**: Se define qué partes del código pueden ver y modificar el estado del objeto.
- **Interfaz pública**: Conjunto de métodos que permiten interactuar con el objeto de manera controlada.

---

## Objetivos del encapsulamiento

1. **Proteger el estado interno**: Evitar modificaciones directas que puedan dejar al objeto en un estado inconsistente.
2. **Facilitar el mantenimiento**: Se pueden cambiar detalles internos sin afectar el código que usa el objeto.
3. **Controlar la lógica de acceso**: Asegurar que cualquier cambio de estado pase por validaciones.
4. **Aumentar la modularidad**: Los objetos se tratan como "cajas negras" con comportamientos definidos.

---

## Encapsulamiento en Java

En Java, el encapsulamiento se logra mediante:

- **Modificadores de acceso** (`private`, `protected`, `public`, _default_).
- **Métodos de acceso** (_getters_ y _setters_) para manipular atributos privados.

Ejemplo básico:

```java
public class Person {
  // Atributos privados (no accesibles directamente desde fuera).
  private String name;
  private int age;

  // Constructor.
  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  // Getter.
  public String getName() {
    return name;
  }

  // Setter con validación.
  public void setAge(int age) {
    if (age > 0) {
      this.age = age;
    } else {
      System.out.println("Invalid age");
    }
  }
}
```

En este ejemplo:

- `name` y `age` están **encapsulados**.
- El acceso se realiza a través de `getName()` y `setAge()`.

---

## Modificadores de acceso en Java

| Modificador | Visibilidad                                  |
| ----------- | -------------------------------------------- |
| `public`    | Accesible desde cualquier clase              |
| `protected` | Accesible desde el mismo paquete y subclases |
| _(default)_ | Accesible solo dentro del mismo paquete      |
| `private`   | Accesible solo dentro de la misma clase      |

---

## Beneficios del encapsulamiento

- **Seguridad**: Evita el acceso no autorizado a datos críticos.
- **Flexibilidad**: Se puede cambiar la implementación interna sin romper el código que usa la clase.
- **Mantenimiento más sencillo**: Menor riesgo de introducir errores al modificar la clase.
- **Reutilización**: Facilita usar clases encapsuladas en otros proyectos.

---

## Ejemplo práctico de encapsulamiento con validación

```java
public class BankAccount {
  private double balance;

  public BankAccount(double balance) {
    if (balance >= 0) {
      this.balance = balance;
    } else {
      this.balance = 0;
    }
  }

  public double getBalance() {
    return balance;
  }

  public void deposit(double amount) {
    if (amount > 0) {
      balance += amount;
    } else {
      System.out.println("Monto inválido");
    }
  }

  public void withdraw(double amount) {
    if (amount > 0 && amount <= balance) {
      balance -= amount;
    } else {
      System.out.println("Invalid withdrawal");
    }
  }
}
```

En este caso:

- `balance` no puede ser modificado directamente.
- Todas las operaciones pasan por métodos con validación.

---

## Encapsulamiento y ocultamiento de información

Aunque a veces se usan como sinónimos, no son exactamente lo mismo:

- **Encapsulamiento**: Concepto más amplio, agrupa datos y métodos que operan sobre ellos.
- **Ocultamiento de información**: Parte del encapsulamiento, se centra en **esconder** detalles internos.

---

## Malas prácticas que rompen el encapsulamiento

- Hacer atributos `public` sin necesidad:

```java
public class Example {
  public int attribute;
}
```

- No validar datos en `setters`:

```java
person.setAge(-5); // Estado inválido permitido.
```

---

## Encapsulamiento y mantenimiento de software

Un sistema con buen encapsulamiento:

- Reduce el **acoplamiento** entre clases.
- Permite **reemplazar implementaciones** sin afectar a otros módulos.
- Favorece la **prueba unitaria** porque cada clase es independiente.

---

## Conclusión

El **encapsulamiento** es clave para crear software **robusto, seguro y mantenible**.

En Java, se logra principalmente con:

- Atributos privados.
- Métodos públicos de acceso controlado.
- Uso inteligente de modificadores de acceso.

> Un buen encapsulamiento convierte a las clases en **cajas negras**: sabes qué hacen, pero no necesitas saber cómo lo hacen internamente.
