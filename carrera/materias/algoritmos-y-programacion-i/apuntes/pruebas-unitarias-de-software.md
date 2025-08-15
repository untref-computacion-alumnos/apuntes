# Pruebas Unitarias de Software

Las **pruebas unitarias** son un método de verificación de software que consiste en comprobar, de forma aislada, el correcto funcionamiento de las **unidades más pequeñas** de un sistema (normalmente funciones o métodos).

El objetivo principal es **detectar errores lo antes posible**, asegurando que cada componente cumpla con su especificación.

---

## Concepto de prueba unitaria

### Definición

Una **prueba unitaria** es un caso de prueba diseñado para validar el comportamiento de una **unidad de código** de forma independiente.

En el contexto de programación orientada a objetos (como Java), una unidad suele ser un **método de una clase**.

---

## Objetivos

- **Verificar el funcionamiento correcto** de cada unidad de forma individual.
- **Detectar errores de manera temprana** antes de que se integren en componentes mayores.
- **Asegurar que las modificaciones o refactorizaciones no rompan el código existente** (_regresión_).
- **Documentar el comportamiento esperado** de una unidad de código.

---

## aracterísticas de las pruebas unitarias

- **Automatizables**: Se ejecutan mediante herramientas o frameworks.
- **Repetibles**: Pueden ejecutarse múltiples veces con los mismos resultados.
- **Independientes**: No dependen de otras pruebas.
- **Rápidas**: Deben ejecutarse en poco tiempo.
- **Deterministas**: Para una misma entrada, siempre producen la misma salida.

---

## Beneficios

- Reducción de costos en la corrección de errores.
- Mayor **confianza** en el código.
- Facilitan la **refactorización**.
- Funcionan como **documentación viva** del sistema.
- Ayudan a encontrar errores de diseño.

---

## Proceso de realización de pruebas unitarias

1. **Identificar la unidad a probar** (función, método, clase).
2. **Definir casos de prueba**:
   - Entradas válidas y esperadas.
   - Entradas inválidas y manejo de excepciones.
   - Casos límite o extremos (_edge cases_).
3. **Implementar el test** usando un framework de pruebas (por ejemplo, JUnit en Java).
4. **Ejecutar la prueba** y verificar los resultados.
5. **Corregir errores** si los resultados no son los esperados.
6. **Repetir el ciclo** ante cambios en el código.

---

## Tipos de pruebas unitarias

- **Positivas**: Confirman que el método funciona con entradas correctas.
- **Negativas**: Verifican el manejo adecuado de entradas incorrectas.
- **De rendimiento** (en unidades críticas): Miden tiempos de ejecución en casos específicos.
- **De regresión**: Aseguran que nuevas modificaciones no introduzcan errores antiguos.

---

## Herramientas comunes para pruebas unitarias

- **JUnit** (Java).
- **TestNG** (Java).
- **NUnit** (.NET).
- **PyTest** (Python).
- **Jest** (JavaScript).

---

## Pruebas unitarias en Java con JUnit

JUnit es el framework más usado en Java para pruebas unitarias.

### Estructura básica de un test en JUnit 5

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class CalculatorTest {
  @Test
  public void testAddition() {
    Calculator calc = new Calculator();
    int result = calc.addition(2, 3);
    assertEquals(5, result, "The sum must be 5");
  }
}
```

---

### Ejemplo completo con varios casos

```java
public class Calculator {
  public int add(int a, int b) {
    return a + b;
  }

  public int divide(int a, int b) {
    if (b == 0) {
      throw new IllegalArgumentException("Cannot be divided by zero");
    }
    return a / b;
  }
}
```

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class CalculatorTest {
  @Test
  public void testSumaPositiva() {
    Calculator calc = new Calculator();
    assertEquals(7, calc.add(3, 4));
  }

  @Test
  public void testSumaNegativa() {
    Calculator calc = new Calculator();
    assertEquals(-1, calc.add(-3, 2));
  }

  @Test
  public void testDivisionValida() {
    Calculator calc = new Calculator();
    assertEquals(2, calc.divide(10, 5));
  }

  @Test
  public void testDivisionPorCero() {
    Calculator calc = new Calculator();
    assertThrows(IllegalArgumentException.class, () -> { calc.divide(10, 0) });
  }
}
```

---

## Buenas prácticas en pruebas unitarias

- **Nombrar claramente** las pruebas (`testNombreDelCaso`).
- **Probar un solo escenario por test**.
- Usar **valores significativos** en las entradas.
- **Evitar dependencias externas** (BD, red, archivos).
- Mantener las pruebas **rápidas** y **deterministas**.
- Revisar que la cobertura (_coverage_) de código sea adecuada, pero sin obsesionarse con el 100%.
- Integrar las pruebas en un **pipeline de integración continua**.

---

## Cobertura de pruebas (_coverage_)

La **cobertura de código** mide qué porcentaje del código es ejecutado por las pruebas.

Tipos comunes:

- **Cobertura de líneas**: Líneas ejecutadas.
- **Cobertura de ramas**: Decisiones (`if`, `switch`) ejecutadas.
- **Cobertura de condiciones**: Combinaciones lógicas evaluadas.

Herramientas:

- **JaCoCo** (Java).
- **Cobertura**.
- **SonarQube** (para análisis de calidad y cobertura).

---

## Relación con TDD (_Test-Driven Development_)

- En **TDD**, las pruebas unitarias se escriben **antes** del código de producción.
- Ciclo TDD: **Red → Green → Refactor**:
  1. Escribir una prueba que falle.
  2. Escribir el código mínimo para pasar la prueba.
  3. Refactorizar el código manteniendo las pruebas verdes.

---

## Conclusión

Las pruebas unitarias son una herramienta fundamental para:

- Mejorar la calidad del software.
- Reducir errores en etapas posteriores.
- Facilitar cambios y mantenimiento.
- Generar confianza en el equipo de desarrollo.

Implementadas de forma sistemática, contribuyen a un desarrollo más ágil, seguro y eficiente.
