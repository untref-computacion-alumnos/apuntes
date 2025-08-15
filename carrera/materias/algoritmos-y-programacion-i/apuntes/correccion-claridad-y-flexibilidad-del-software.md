# Corrección, claridad y flexibilidad del software

En el desarrollo de software, tres cualidades determinan la calidad y utilidad de un programa:

1. **Corrección**: El software hace lo que se supone que tiene que hacer.
2. **Claridad**: El software es comprensible y fácil de mantener.
3. **Flexibilidad**: El software puede adaptarse a cambios y nuevas necesidades sin grandes dificultades.

Estas propiedades son esenciales para garantizar que un sistema sea **funcional, mantenible y escalable**.

---

## Corrección

### Definición

La **corrección** de un software es la propiedad que asegura que el programa:

- Cumple con las especificaciones y requisitos establecidos.
- Produce resultados correctos para todas las entradas válidas.
- Maneja adecuadamente las entradas no válidas.

En términos simples: **un programa correcto hace lo que debe, siempre**.

### Cómo lograr la corrección

- **Análisis de requisitos precisos**: Entender el problema y definir claramente lo que debe hacer el software.
- **Diseño detallado**: Estructurar la solución antes de implementarla.
- **Validación y verificación**:
  - **Verificación**: Comprobar que el software se implementó según el diseño.
  - **Validación**: Comprobar que el software satisface las necesidades reales del usuario.
- **Pruebas exhaustivas**:
  - Casos normales.
  - Casos límite.
  - Casos de error.

### Ejemplo en Java

```java
public int divide(int numerator, int denominator) {
  if (denominator == 0) {
    throw new IllegalArgumentException("The denominator cannot be zero");
  }
  return numerator / denominator;
}
```

> Aca se asegura la **corrección** manejando el caso de división por cero.

---

## Claridad

### Definición

La **claridad** es la capacidad del software para ser leído, entendido y mantenido fácilmente por otros desarrolladores (o por uno mismo en el futuro).

Un software claro:

- Usa nombres descriptivos para variables, métodos y clases.
- Tiene una estructura lógica y coherente.
- Incluye comentarios útiles (no redundantes).
- Evita la complejidad innecesaria.

### Importancia

- Reduce el tiempo necesario para entender el código.
- Facilita la detección y corrección de errores.
- Permite la colaboración entre equipos.

### Buenas prácticas para la claridad

- Seguir **convenciones de estilo** (como las guías de Java).
- Usar **indentación consistente**.
- Evitar funciones demasiado largas aplicando el principio de responsabilidad única.
- Documentar el **por qué**, no solo el **qué**.

### Ejemplo: código poco claro vs claro

**Código poco claro**:

```java
public int x(int y, int z) {
  int w = y;
  for (int i = 0; i < z; i++) {
    w = w + i;
  }
  return w;
}
```

**Código claro**:

```java
/**
 * Returns the first argument incremented by {@code b} times.
 *
 * @param a The number to be increased.
 * @param b The amount of increases.
 *
 * @return The variable {@code a} incremented {@code b} times.
 *
 * @throws IllegalArgumentException If {@code b} is negative.
 */
public int increment(int a, int b) {
  if (b <= 0) {
    throw new IllegalArgumentException("The second number must be positive to increment");
  }
  return a + b;
}
```

- Nombres descriptivos.
- Documentación clara.
- Estructura más legible.
- Manejo de posibles problemas.

---

## Flexibilidad

### Definición

La **flexibilidad** es la capacidad del software para adaptarse a nuevos requisitos o cambios sin necesidad de rehacerlo por completo.

Un software flexible:

- Tiene un diseño modular.
- Permite agregar o modificar funcionalidades con cambios mínimos en el código existente.
- Minimiza la dependencia entre componentes.

### Importancia

- Los requisitos cambian con el tiempo.
- Reduce el costo y esfuerzo de mantenimiento.
- Facilita la escalabilidad.

### Estrategias para aumentar la flexibilidad

- **Programar para interfaces**, no para implementaciones.
- Usar **patrones de diseño** (por ejemplo, Strategy, Observer, Factory).
- Aplicar el principio **Open/Closed** (abierto para extensión, cerrado para modificación).
- Evitar el **acoplamiento fuerte**.

### Ejemplo en Java (flexible con interfaces)

```java
interface Sending {
  void send(String msg);
}

class SendingMail implements Sending {
  public void send(String msg) {
    System.out.println("Sending mail: " + msg);
  }
}

class SendingSMS implements Sending {
  public void send(String msg) {
    System.out.println("Sending SMS: " + msg);
  }
}

class Notifier {
  private Sending method;

  public Notifier(Sending method) {
    this.method = method;
  }

  public void notify(String msg) {
    method.send(msg);
  }
}

// Uso
Notifier not = new Notifier(new SendingMail());
not.notify("¡Hello, World!");

not = new Notifier(new SendingSMS());
not.notify("¡Hello, World!");
```

> Acá cambiar la forma de envío no requiere modificar `Notifier`, solo cambiar la implementación de `Sending`.

---

## Relación entre corrección, claridad y flexibilidad

Estas tres propiedades no son independientes:

- Un código **correcto pero poco claro** será difícil de mantener.
- Un código **claro pero incorrecto** no cumple su propósito.
- Un código **correcto y claro pero rígido** será costoso de modificar.

El objetivo es **balancear las tres** para lograr software de alta calidad.

---

## Buenas prácticas generales

- **Diseñar antes de programar**: Reduce errores y mejora la calidad.
- **Usar nombres significativos**: Facilita la comprensión.
- **Escribir pruebas automatizadas**: Asegura la corrección.
- **Aplicar principios [SOLID](https://en.wikipedia.org/wiki/SOLID)**: Mejora la flexibilidad.
- **Refactorizar periódicamente**: Mejora la claridad y la mantenibilidad.

---

## Conclusión

- **Corrección**: Garantiza que el software haga lo que debe.
- **Claridad**: Facilita su comprensión y mantenimiento.
- **Flexibilidad**: Permite que el software evolucione.

El equilibrio de estas tres cualidades permite desarrollar software robusto, mantenible y adaptable en el tiempo.
