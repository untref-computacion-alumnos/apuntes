# Manejo de Excepciones

El **manejo de excepciones** es un mecanismo que permite **detectar, controlar y responder** a situaciones anómalas que pueden ocurrir durante la ejecución de un programa.

Su objetivo principal es **prevenir fallos** y **garantizar que el sistema pueda recuperarse o finalizar de forma controlada**.

---

## ¿Qué es una excepción?

Una **excepción** es un evento que interrumpe el flujo normal de ejecución de un programa debido a:

- Errores de entrada/salida.
- Datos inválidos.
- Fallos en operaciones aritméticas (por ejemplo, división por cero).
- Problemas de conexión a una base de datos o red.
- Otros comportamientos inesperados.

En Java, una excepción es un **objeto** que representa un error o condición inusual.

Cuando se lanza una excepción, el flujo normal del programa se detiene y se busca un bloque de código que pueda manejarla.

---

## Importancia del manejo de excepciones

- **Evita que el programa se detenga abruptamente**.
- **Mejora la robustez** del software.
- **Facilita la localización de errores**.
- **Permite manejar errores de forma centralizada**.
- **Aumenta la confiabilidad** ante situaciones imprevistas.

---

## Tipos de excepciones en Java

En Java, todas las excepciones heredan de la clase `Throwable` y se dividen en dos grandes grupos:

### Excepciones comprobadas (_checked exceptions_)

- Se verifican **en tiempo de compilación**.
- El compilador obliga a manejarlas con `try-catch` o declararlas con `throws`.
- Ejemplos: `IOException`, `SQLException`, `FileNotFoundException`.

### Excepciones no comprobadas (_unchecked exceptions_)

- Se verifican **en tiempo de ejecución**.
- Heredan de `RuntimeException`.
- No es obligatorio capturarlas ni declararlas.
- Ejemplos: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException`.

### Errores (_Errors_)

- Condiciones graves normalmente fuera del control del programador.
- Generalmente no se recuperan.
- Ejemplos: `OutOfMemoryError`, `StackOverflowError`.

---

## Flujo del manejo de excepciones

1. Ocurre una condición anómala.
2. Se crea un **objeto excepción**.
3. La excepción es **lanzada** (`throw`).
4. La JVM busca un bloque `catch` adecuado.
5. Si lo encuentra, ejecuta su código de manejo.
6. Si no lo encuentra, el programa termina y la JVM muestra un **stack trace**.

---

## Sintaxis en Java

### Estructura básica

```java
try {
  // Código que puede lanzar una excepción.
} catch (TipoDeExcepcion e) {
  // Código para manejar la excepción.
} finally {
  // Bloque opcional que siempre se ejecuta.
}
```

---

## Ejemplo simple

```java
public class DivisionExample {
  public static void main(String[] args) {
    try {
      int a = 10;
      int b = 0;
      int result = a / b; // Lanza ArithmeticException
      System.out.println("Result: " + result);
    } catch (ArithmeticException e) {
      System.out.println("Error: Division by zero not allowed.");
    } finally {
      System.out.println("End of calculation.");
    }
  }
}
```

**Salida**:

```md
Error: Division by zero not allowed.
End of calculation.
```

---

## Múltiples bloques `catch`

```java
try {
  String text = null;
  System.out.println(text.length());  // NullPointerException
} catch (NullPointerException e) {
  System.out.println("Error: Null object.");
} catch (Exception e) {
  System.out.println("Generic error: " + e.getMessage());
}
```

---

## Uso de `throws` y `throw`

- **`throw`**: Lanza una excepción específica en un punto concreto del código.
- **`throws`**: Declara que un método puede lanzar una o más excepciones.

**Ejemplo**:

```java
public class Example {
  public void readFile(String name) throws IOException {
    FileReader fr = new FileReader(name);
    // ...
  }
}
```

---

## Excepciones personalizadas

Se pueden crear clases propias que extiendan `Exception` o `RuntimeException`.

```java
public class InvalidAgeException extends Exception {
  public InvalidAgeException(String msg) {
    super(msg);
  }
}

public class RegisterUser {
  public void register(int age) throws InvalidAgeException {
    if (age < 18) {
      throw new InvalidAgeException("Age must be greater than or equal to 18.");
    }
    System.out.println("Registered user.");
  }
}
```

---

## Buenas prácticas

- **No atrapar excepciones genéricas** salvo que sea estrictamente necesario.
- **Especificar el tipo exacto** de excepción a manejar.
- **Proporcionar mensajes claros** en las excepciones.
- **No usar excepciones para control de flujo normal**.
- **Cerrar recursos** en bloques `finally` o usar _try-with-resources_.

---

## `try-with-resources`

Desde Java 7, se pueden manejar automáticamente recursos que implementan `AutoCloseable`.

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
  String line;
  while ((line = br.readLine()) != null) {
    System.out.println(line);
  }
} catch (IOException e) {
  System.out.println("Error reading file: " + e.getMessage());
}
```

---

## Ventajas del manejo de excepciones

- **Aísla el código de manejo de errores** del código normal.
- **Permite recuperación controlada**.
- **Mejora la claridad** y legibilidad.
- **Reduce fallos inesperados** en producción.

---

## Conclusión

El **manejo de excepciones** es un mecanismo esencial para escribir software robusto, confiable y mantenible.

En Java, el modelo de excepciones está fuertemente tipado y obliga a los desarrolladores a **anticipar y manejar** posibles errores, mejorando así la calidad del código y la experiencia del usuario.
