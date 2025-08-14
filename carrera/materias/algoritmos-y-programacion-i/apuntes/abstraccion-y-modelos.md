# Abstracción y Modelos

La **abstracción** y los **modelos** son herramientas conceptuales fundamentales para comprender, representar y resolver problemas.

Permiten manejar la complejidad al enfocarse en lo esencial y representar la realidad de forma simplificada para su análisis y manipulación.

---

## Abstracción

### Definición

La **abstracción** es el proceso de identificar y destacar las características esenciales de un objeto o sistema, ignorando los detalles irrelevantes para el contexto actual.

Es una forma de simplificar un problema sin perder la información necesaria para su resolución.

**Ejemplo**:

Si se quiere programar un sistema para gestionar autos, interesa su marca, modelo y matrícula; pero no se necesita modelar el color del tornillo que sujeta el espejo retrovisor.

---

### Propósito

- Reducir la complejidad.
- Permitir centrarse en lo relevante.
- Facilitar la comunicación y el razonamiento.
- Servir como base para el diseño y la implementación de soluciones.

---

### Tipos de abstracción

#### Abstracción de datos

Se centra en **qué datos** se manejan y sus propiedades, sin importar cómo se almacenan o procesan internamente.

**Ejemplo**: En una base de datos, una tabla `Clientes` con campos `nombre`, `dni`, `email` es una abstracción que oculta cómo se guardan físicamente esos datos en el disco.

#### Abstracción procedimental

Se enfoca en **qué hace** una operación, sin especificar los detalles internos de su implementación.

**Ejemplo**: Una función `calcularPromedio(notas)` que podemos usar sin saber cómo está implementada internamente.

#### Abstracción de control

Se refiere a ocultar los detalles del flujo de control, proporcionando estructuras más sencillas para coordinar acciones.

**Ejemplo**: Un bucle `for` oculta el mecanismo de incremento y comparación que lo hace funcionar.

---

### Abstracción en programación

En programación, la abstracción puede aplicarse en distintos niveles:

- **Lenguaje**: Construcciones de alto nivel (funciones, clases, módulos).
- **Diseño**: Diagramas y pseudocódigo que representan la lógica.
- **Arquitectura**: Capas de un sistema (presentación, negocio, datos) donde cada capa oculta detalles a las demás.

---

## Modelos

### Definición

Un **modelo** es una representación simplificada de la realidad que captura los elementos y relaciones relevantes para un propósito específico.

**Ejemplo**:

- Un **mapa** es un modelo geográfico que representa ubicaciones y distancias sin mostrar cada detalle del terreno.
- Un **diagrama de clases** en UML es un modelo de la estructura de un sistema de software.

---

### Características

- **Simplificación**: No incluye todos los detalles del mundo real.
- **Especificidad**: Se crea con un objetivo determinado.
- **Representatividad**: Refleja las propiedades esenciales del sistema.
- **Interpretabilidad**: Debe ser comprensible para sus usuarios.

---

### Tipos de modelos

#### Modelos físicos

Representaciones tangibles o materiales del objeto real.

**Ejemplo**: Una maqueta de un puente.

#### Modelos conceptuales

Representaciones abstractas que describen ideas, procesos o relaciones.

**Ejemplo**: Un diagrama de flujo para mostrar el recorrido de datos en un sistema.

#### Modelos matemáticos

Representaciones basadas en ecuaciones y expresiones formales.

**Ejemplo**: Una fórmula para calcular la depreciación de un activo.

#### Modelos computacionales

Modelos implementados mediante programas informáticos.

**Ejemplo**: Un simulador del clima.

---

## Relación entre abstracción y modelos

- La **abstracción** es el proceso mental mediante el cual se seleccionan las características relevantes.
- El **modelo** es el resultado concreto de aplicar la abstracción.
- Un modelo **es una representación**, mientras que la abstracción es **la técnica para construir esa representación**.

**Esquema:**

```text
Realidad → (Abstracción) → Modelo
```

---

## Ejemplos

### Ejemplo 1: Sistema de ventas

1. **Abstracción**: Identificar que lo relevante son clientes, productos y ventas, ignorando detalles como el color de las paredes del local.
2. **Modelo**: Diagrama entidad-relación con entidades `Cliente`, `Producto` y `Venta`, y las relaciones entre ellas.

### Ejemplo 2: Tránsito vehicular

1. **Abstracción**: Considerar vehículos, semáforos y calles; ignorar la marca de cada vehículo.
2. **Modelo**: Simulación por computadora que representa el flujo de autos y peatones.

---

## Ventajas de usar abstracciones y modelos

- Permiten manejar sistemas complejos.
- Mejoran la comunicación entre personas y equipos.
- Facilitan el diseño y mantenimiento de soluciones.
- Ayudan a predecir el comportamiento del sistema.
- Posibilitan la reutilización de ideas y estructuras.

---

## Conclusión

La abstracción y los modelos son esenciales para simplificar la realidad y representar los aspectos clave de un sistema o problema.  
Aplicar abstracción ayuda a concentrarse en lo importante, y un buen modelo permite comunicar, analizar y simular el comportamiento del sistema antes de su implementación.

En programación y desarrollo de sistemas:

- **Abstracción**: Pensar y decidir qué detalles son importantes.
- **Modelo**: Materializar esa decisión en una representación formal y utilizable.
