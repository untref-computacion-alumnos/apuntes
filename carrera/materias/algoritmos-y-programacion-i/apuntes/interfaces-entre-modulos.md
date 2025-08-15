# Interfaces entre módulos

En el desarrollo de software modular, los **módulos** no funcionan de manera aislada: deben **comunicarse** para cumplir los objetivos del sistema.

La forma en que esta comunicación se define y se gestiona se conoce como **interfaz entre módulos**.

Una **interfaz** es el conjunto de elementos (métodos, funciones, atributos accesibles, protocolos) que un módulo **expone** para que otros módulos puedan interactuar con él **sin conocer su implementación interna**.

---

## Conceptos clave

- **Módulo**: Unidad independiente de software con una funcionalidad bien definida.
- **Interfaz**: Contrato que especifica cómo un módulo puede ser utilizado.
- **Implementación**: Código interno que realiza las operaciones declaradas en la interfaz.
- **Encapsulamiento**: Ocultar detalles internos del módulo y mostrar solo la interfaz pública.

En otras palabras:

> La interfaz es **lo que otros pueden ver y usar**; la implementación es **cómo realmente funciona por dentro**.

---

## Importancia de las interfaces entre módulos

1. **Separación de responsabilidades**: Permiten que los desarrolladores trabajen en diferentes módulos de forma independiente.
2. **Independencia de implementación**: Un módulo puede cambiar internamente sin afectar a los demás, siempre que su interfaz no cambie.
3. **Reutilización**: Un módulo con una interfaz bien diseñada puede ser usado en otros proyectos.
4. **Claridad**: Documentan y organizan las formas de interacción en un sistema.

---

## Tipos de interfaces

### Interfaces públicas de clases (en Java)

- Definidas mediante métodos y atributos públicos de una clase.
- Permiten que otros módulos interactúen con la clase sin acceder a detalles internos.

**Ejemplo**:

```java
public class Calculator {
  public double add(double a, double b) {
    return a + b;
  }
}
```

### Interfaces formales (palabra clave `interface` en Java)

- Definen un **contrato** que otras clases deben cumplir.
- No contienen implementación (excepto métodos _default_ o _static_ en Java 8+).
- Usadas para garantizar consistencia en la comunicación entre módulos.

Ejemplo:

```java
public interface Operation {
  double execute(double a, double b);
}
```

### Interfaces de paquetes y librerías

- Se logran exponiendo solo clases y métodos necesarios a través de **modificadores de acceso** (`public`, `protected`, _default_, `private`).
- En Java 9+, se pueden exportar módulos explícitamente con `module-info.java`.

---

## Principios para diseñar interfaces efectivas

1. **Claridad**: La interfaz debe ser fácil de entender y usar.
2. **Simplicidad**: Exponer solo lo necesario, evitando métodos redundantes.
3. **Estabilidad**: Cambiar una interfaz pública afecta a todos los módulos que dependen de ella.
4. **Consistencia**: Mantener nombres y comportamientos coherentes.
5. **Documentación**: Explicar qué hace cada método, qué parámetros recibe y qué retorna.

---

## Ejemplo en Java: interacción de módulos con interfaces

Supongamos que tenemos un sistema con un módulo que procesa operaciones matemáticas y otro que las ejecuta.

```java
// Módulo 1: Definición de interfaz
public interface Operation {
  double execute(double a, double b);
}

// Módulo 2: Implementación de la interfaz
public class Add implements Operation {
  @Override
  public double execute(double a, double b) {
    return a + b;
  }
}

// Módulo 3: Implementación alternativa
public class Multiplication implements Operation {
  @Override
  public double execute(double a, double b) {
    return a * b;
  }
}

// Módulo principal que consume la interfaz
public class Calculator {
  public static void main(String[] args) {
    Operation op1 = new Add();
    Operation op2 = new Multiplication();

    System.out.println("Add: " + op1.execute(5, 3));
    System.out.println("Multiplication: " + op2.execute(5, 3));
  }
}
```

Ventajas en este diseño:

- La clase `Calculator` **no sabe** cómo están implementadas `Add` o `Multiplication`.
- Es fácil **agregar nuevas operaciones** sin modificar `Calculator`.

---

## Acoplamiento y cohesión en interfaces

- **Bajo acoplamiento**: La interfaz debe minimizar dependencias innecesarias.
- **Alta cohesión**: Cada interfaz debe enfocarse en un propósito concreto.

Ejemplo de mala práctica:

```java
public interface AllInOne {
  void add();
  void subtract();
  void connectBD();
  void exportCSV();
}
```

> La interfaz mezcla funciones sin relación, lo que viola la cohesión.

---

## Interfaces y modularidad en sistemas grandes

En aplicaciones complejas:

- Se definen **interfaces base** para los módulos principales.
- Se utilizan **paquetes** para organizar código y controlar acceso.
- Se documentan las interfaces para que otros equipos puedan implementarlas o consumirlas.

Ejemplo de organización:

```text
/src
  ├── app
  │     ├── Main.java
  │
  ├── operaciones
  │     ├── Operation.java
  │     ├── Add.java
  │     ├── Multiplication.java
```

---

## Buenas prácticas

- Diseñar interfaces pensando en **el usuario del módulo**, no en la implementación.
- Usar nombres claros y consistentes.
- Mantener las interfaces **lo más pequeñas posible** (Principio de Segregación de Interfaces - ISP).
- Documentar con JavaDoc para que sean fácilmente entendibles.
- Evitar exponer variables públicas; preferir métodos de acceso (_getters/setters_).

---

## Conclusión

Las **interfaces entre módulos** permiten que las distintas partes de un sistema interactúen de forma ordenada, clara y estable.

En Java, las interfaces pueden ser tanto **públicas en clases** como **interfaces formales** (`interface`).

Un buen diseño de interfaces:

- Favorece la modularidad.
- Facilita el mantenimiento.
- Incrementa la reutilización.
- Reduce el acoplamiento.

En resumen:

> Una buena interfaz es un **contrato claro** que define **qué se puede hacer**, sin decir **cómo se hace**.
