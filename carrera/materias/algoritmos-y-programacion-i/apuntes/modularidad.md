# Modularidad

La **modularidad** es un principio fundamental en el desarrollo de software que consiste en **dividir un sistema en partes más pequeñas y manejables**, llamadas **módulos**, de forma que cada uno cumpla una función específica e independiente.

Un módulo es una unidad funcional del programa que **puede desarrollarse, probarse y mantenerse de manera separada**, pero que se integra con los demás para formar un sistema completo.

---

## Conceptos clave

- **Módulo**: Componente o unidad del software que encapsula una parte de la funcionalidad.
- **Encapsulamiento**: Ocultamiento de la implementación interna de un módulo, exponiendo solo lo necesario (interfaz pública).
- **Interfaz**: Conjunto de métodos, funciones o servicios que un módulo ofrece para interactuar con otros.
- **Independencia**: Un módulo idealmente tiene bajo acoplamiento con otros y alta cohesión interna.

---

## Características de la modularidad

1. **Descomposición funcional**: Dividir el problema en tareas más pequeñas.
2. **Cohesión**: Cada módulo debe cumplir un único propósito claro.
3. **Bajo acoplamiento**: Los módulos deben depender lo menos posible entre sí.
4. **Reutilización**: Un módulo bien diseñado puede usarse en otros proyectos.
5. **Encapsulamiento**: La implementación interna está oculta, solo se expone lo esencial.

---

## Ventajas de la modularidad

| Ventaja               | Explicación                                                                        |
| --------------------- | ---------------------------------------------------------------------------------- |
| **Mantenibilidad**    | Permite localizar y corregir errores en un módulo sin afectar el resto del sistema |
| **Reutilización**     | Módulos genéricos pueden usarse en otros programas                                 |
| **Trabajo en equipo** | Diferentes programadores pueden trabajar en módulos distintos en paralelo          |
| **Escalabilidad**     | Es más fácil agregar nuevas funcionalidades                                        |
| **Claridad**          | El código está más organizado y es más comprensible                                |

---

## Ejemplo de modularidad en Java

### Sin modularidad (código monolítico)

```java
public class Calculator {
  public static void main(String[] args) {
    double a = 5, b = 3;

    // Suma
    System.out.println("Add: " + (a + b));

    // Resta
    System.out.println("Subtraction: " + (a - b));

    // Multiplicación
    System.out.println("Multiplicatio: " + (a * b));

    // División
    if (b != 0) {
      System.out.println("Division: " + (a / b));
    } else {
      System.out.println("Error: Division by zero");
    }
  }
}
```

- Todo el código está en un solo lugar.
- Difícil de mantener y extender.

### Con modularidad

```java
class Operations {
  public double add(double x, double y) {
    return x + y;
  }

  public double subtract(double x, double y) {
    return x - y;
  }

  public double multiply(double x, double y) {
    return x * y;
  }

  public double divide(double x, double y) {
    if (y == 0) {
      throw new IllegalArgumentException("Division by zero");
    }
    return x / y;
  }
}

public class Calculator {
  public static void main(String[] args) {
    Operations op = new Operations();

    double a = 5, b = 3;

    System.out.println("Add: " + op.add(a, b));
    System.out.println("Subtraction: " + op.subtract(a, b));
    System.out.println("Multiplication: " + op.multiply(a, b));
    System.out.println("Division: " + op.divide(a, b));
  }
}
```

- Cada operación está encapsulada en un módulo (`Operations`).
- Más fácil de mantener, probar y extender.

---

## Principios relacionados

1. **Principio de responsabilidad única (SRP)**: Cada módulo debe tener **un solo motivo de cambio**.
2. **Bajo acoplamiento**: Los módulos deben depender lo menos posible unos de otros, y cuando lo hagan, debe ser a travpes de interfaces claras.
3. **Alta cohesión**: Los elementos dentro de un módulo deben estar fuertemente relacionados en función.
4. **Interfaces bien definidas**: Claridad en cómo se comunican los módulos.

---

## Modularidad y desarrollo a gran escala

En sistemas grandes:

- **Separación en paquetes** (`package` en Java) ayuda a organizar el código.
- Uso de **arquitecturas modulares** (por ejemplo, MVC, microservicios).
- Documentación clara de cada módulo.

Ejemplo de organización en Java:

```text
/src
  ├── calculator
  │     ├── Operations.java
  │     ├── Calculator.java
  │     └── utils
  │           └── Validations.java
```

---

## Beneficios a largo plazo

- **Facilidad para agregar nuevas funciones** sin romper código existente.
- **Pruebas unitarias más simples** gracias a la independencia de módulos.
- **Colaboración entre equipos** más ordenada.
- **Evolución tecnológica** (sustituir módulos por implementaciones más modernas sin reescribir todo el sistema).

---

## Conclusión

La **modularidad** es clave para construir software **escalable, mantenible y reutilizable**.

En Java y otros lenguajes orientados a objetos, se logra principalmente a través de **clases, interfaces y paquetes**, diseñados con **alta cohesión**.

Adoptar este enfoque desde el inicio del desarrollo evitando problemas futuros y facilita la evolución del sistema.
