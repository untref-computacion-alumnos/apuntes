# Globalidad y Localidad

En programación, **globalidad** y **localidad** se refieren al **ámbito** (o _scope_) en el que una variable, función o recurso es accesible dentro de un programa.

Comprender estos conceptos es clave para:

- Organizar el código.
- Evitar conflictos de nombres.
- Controlar el uso de memoria.
- Mejorar la legibilidad y mantenimiento del software.

---

## Ámbito o _scope_

El **ámbito** define la parte del programa donde un identificador (variable, constante, función, etc.) es reconocido y puede ser usado.

En Java, el ámbito se determina principalmente por:

- **El lugar donde se declara** el elemento.
- **Las llaves `{ ... }`** que delimitan bloques de código.

---

## Globalidad

### Definición

Se refiere a los elementos que están **disponibles en todo el programa** o en un amplio conjunto de clases y métodos.

En Java, no existen **variables verdaderamente globales** (como en otros lenguajes), pero se puede simular la globalidad mediante:

- **Variables estáticas** (`static`) en una clase.
- **Constantes estáticas** (`static final`).
- **Campos públicos** accesibles desde otras clases.

### Características

- Son accesibles desde cualquier parte del código que tenga visibilidad de la clase.
- Se mantienen en memoria durante toda la ejecución del programa.
- Tiene que usarse con cuidado para evitar dependencias excesivas.

### Ejemplo en Java

```java
public class Config {
  public static String appName = "My Application";  // Variable global.
}

public class Main {
  public static void main(String[] args) {
    System.out.println("Name: " + Config.appName);
  }
}
```

En este ejemplo:

- `appName` es accesible desde cualquier parte del programa usando `Config.appName`.

---

## Localidad

### Definición

Se refiere a los elementos que **solo existen y son accesibles dentro de un bloque específico** del código.

En Java, las variables **locales**:

- Se declaran dentro de métodos, constructores o bloques.
- Se crean cuando se entra en el bloque.
- Se destruyen cuando se sale del bloque.

### Características

- Solo se pueden usar dentro del bloque donde fueron definidas.
- No consumen memoria una vez que termina el bloque.
- Ayudan a evitar interferencias con otras partes del código.

### Ejemplo en Java

```java
public class Example {
  public static void main(String[] args) {
    int count = 0;                          // Variable local al método 'main'.
    for (int i = 0; i < 5; i++) {           // 'i' es local al bucle.
      count += i;
    }

    System.out.println("Count: " + count);  // Acá no se puede usar 'i' porque solo existe dentro del bloque del bucle 'for'.
  }
}
```

---

## Comparación entre globalidad y localidad

| **Características** | **Globalidad**                                 | **Localidad**                              |
| ------------------- | ---------------------------------------------- | ------------------------------------------ |
| Ámbito              | Todo el programa o clase                       | Solo el bloque o método donde se declara   |
| Duración en memoria | Toda la ejecución                              | Solo durante la ejecución del bloque       |
| Accesibilidad       | Desde cualquier parte con visibilidad          | Únicamente dentro del bloque               |
| Ejemplo en Java     | Campo `static` público                         | Variable en un método                      |
| Riesgo              | Acoplamiento excesivo, dificultad para depurar | Requiere paso de datos entre métodos       |
| Ventaja             | Facilidad de acceso                            | Mayor encapsulamiento y control de memoria |

---

## Buenas prácticas

- **Preferir la localidad** siempre que sea posible, reduciendo errores y mejorando la modularidad.
- Evitar variables globales para **almacenar estados cambiantes** que puedan ser modificados desde múltiples lugares.
- Usar constantes globales (`static final`) solo para valores fijos (por ejemplo, `PI`, configuraciones, etc.).
- Cuando se requiera compartir información, **pasarla como parámetros** en lugar de usar globales.
- Nombrar claramente las variables globales para evitar confusión.

---

## Ejemplo integrador

```java
public class AppConfig {
  public static final String VERSION = "1.0.0"; // Constante global.
  public static int globalCount = 0;            // Variable global (evitar en lo posible).
}

public class Program {
  public static void main(String[] args) {
    int a = 0;  // Variable local

    for (int i = 1; i <= 3; i++) {
      a += i;
      AppConfig.globalCount++;
    }

    System.out.println("Local addition: " + a);
    System.out.println("Global counting: " + AppConfig.globalCount);
    System.out.println("Version: " + AppConfig.VERSION);
  }
}
```

En este caso:

- `VERSION` es un dato global constante.
- `globalCount` es global y cambia en todo el programa.
- `a` es local al método `main`.

---

## Conclusión

La **globalidad** y la **localidad** son conceptos fundamentales en la organización del código:

- **Globalidad**: Fácil acceso, pero puede generar alto acoplamiento.
- **Localidad**: Mayor seguridad, menor riesgo de interferencia.

Un buen diseño equilibra ambas, usando **globalidad para constantes y configuraciones**, y **localidad para lógica y datos específicos de cada bloque**.
