# Paradigmas de programación

Un **paradigma de programación** es un estilo o enfoque que define la manera en que un programador organiza, estructura y desarrolla un programa.

Cada paradigma establece **principios, conceptos y técnicas** que orientan la solución de problemas mediante el uso de un lenguaje de programación.

---

## Definición

Un paradigma de programación es un **modelo conceptual** que determina cómo se representan los datos y cómo se estructuran las operaciones para resolver problemas.

Se relaciona estrechamente con:

- **La forma de pensar** del programador.
- **Las herramientas** y características que ofrece el lenguaje de programación.
- **El tipo de problemas** que se busca resolver.

---

## Tipos principales de paradigmas

Existen múltiples clasificaciones, pero los paradigmas más estudiados son:

### Paradigma imperativo

- **Idea central**: Describir un conjunto de instrucciones que modifican el estado del programa.
- **Enfoque**: "Cómo" se hace la tarea, paso a paso.
- **Características**:
  - Uso de variables y estructuras de control (bucles, condicionales).
  - Énfasis en la secuencia de instrucciones.
- **Ejemplos de lenguajes**: C, Pascal, Fortran.
- **Ventajas**:
  - Fácil de entender para quienes piensan de forma secuencial.
  - Buena eficiencia en tiempo de ejecución.
- **Desventajas**:
  - Menor abstracción.
  - Mayor riesgo de errores por cambios en el estado del programa.

**Ejemplo en pseudocódigo (calcular suma de 1 a N)**:

```text
suma ← 0
Para i desde 1 hasta N hacer
  suma ← suma + i
Fin Para
Mostrar suma
```

---

### Paradigma declarativo

- **Idea central**: Especificar _qué_ se quiere obtener, sin detallar _cómo_ lograrlo.
- **Enfoque**: Describir el problema, no el procedimiento.
- **Características**:
  - El control de ejecución lo gestiona el intérprete o compilador.
  - Orientado a la descripción de relaciones y propiedades.
- **Ejemplos de lenguajes**: SQL, Prolog, HTML (en parte).
- **Ventajas**:
  - Menor código para tareas específicas.
  - Mayor claridad en ciertos tipos de problemas.
- **Desventajas**:
  - Menor control sobre el rendimiento.
  - Puede ser menos intuitivo para problemas secuenciales.

**Ejemplo en SQL (sumar valores de una columna)**:

```sql
SELECT SUM(valor) FROM tabla;
```

---

### Paradigma orientado a objetos (POO)

- **Idea central**: Modelar el problema en términos de **objetos** que combinan datos (**atributos**) y operaciones (**métodos**).
- **Enfoque**: Pensar en entidades del mundo real y sus interacciones.
- **Características**:
  - Abstracción, encapsulamiento, herencia y polimorfismo.
  - Los objetos interactúan enviándose mensajes.
- **Ejemplos de lenguajes**: Java, C++, Python, Ruby.
- **Ventajas**:
  - Modularidad y reutilización de código.
  - Facilita el mantenimiento y la ampliación del software.
- **Desventajas**:
  - Puede requerir más tiempo de diseño inicial.
  - Complejidad innecesaria en programas pequeños.

**Ejemplo en pseudocódigo**:

```text
Clase Persona
  Atributos: nombre, edad

  Método saludar():
    Mostrar "Hola, soy " + nombre
  Fin Método
Fin Clase

p ← nueva Persona("Juan", 30)

p.saludar()
```

---

### Paradigma funcional

- **Idea central**: Construir programas usando funciones puras (sin efectos secundarios).
- **Enfoque**: La computación se entiende como la evaluación de funciones matemáticas.
- **Características**:
  - Evita modificar el estado y las variables.
  - Uso intensivo de recursividad y funciones de orden superior.
- **Ejemplos de lenguajes**: Haskell, Lisp, Erlang; soportado también en Python y JavaScript.
- **Ventajas**:
  - Programas más fáciles de razonar y depurar.
  - Menor riesgo de errores por cambios de estado.
- **Desventajas**:
  - Curva de aprendizaje más pronunciada.
  - Menos eficiente en ciertos contextos.

**Ejemplo en Haskell (suma de 1 a N)**:

```haskell
sumatoria n = sum [1..n]
```

---

### Paradigma lógico

- **Idea central**: Basarse en reglas lógicas y deducción para llegar a conclusiones.
- **Enfoque**: Definir hechos y reglas; el motor lógico deduce respuestas.
- **Características**:
  - Usa lógica de predicados.
  - No se programa el algoritmo paso a paso.
- **Ejemplos de lenguajes**: Prolog.
- **Ventajas**:
  - Expresivo para problemas de razonamiento y búsqueda.
- **Desventajas**:
  - Menor eficiencia en cálculos numéricos.
  - Requiere pensar en términos de lógica formal.

**Ejemplo en Prolog**:

```prolog
padre(juan, maria).
padre(juan, pedro).
hijo(X, Y) :- padre(Y, X).
```

---

## Lenguajes multiparadigma

Muchos lenguajes actuales combinan características de varios paradigmas, permitiendo elegir el enfoque más adecuado para cada problema.

**Ejemplos**:

- **Python**: Soporta imperativo, orientado a objetos y funcional.
- **JavaScript**: Soporta imperativo, funcional y orientado a objetos.
- **Scala**: Combina orientado a objetos y funcional.

---

## Comparativa de paradigmas

| Paradigma           | Cómo se enfoca el problema | Ejemplo de lenguajes | Ventaja principal                | Desventaja principal               |
| ------------------- | -------------------------- | -------------------- | -------------------------------- | ---------------------------------- |
| Imperativo          | Secuencia de instrucciones | C, Pascal, Fortran   | Control detallado del flujo      | Mayor riesgo de errores por estado |
| Declarativo         | Descripción del resultado  | SQL, Prolog          | Código más conciso               | Menor control de ejecución         |
| Orientado a objetos | Modelado de entidades      | Java, C++, Python    | Modularidad y reutilización      | Complejidad en proyectos pequeños  |
| Funcional           | Evaluación de funciones    | Haskell, Lisp        | Facilidad de razonamiento        | Curva de aprendizaje alta          |
| Lógico              | Razonamiento por reglas    | Prolog               | Expresivo para problemas lógicos | Bajo rendimiento numérico          |

---

## Resumen visual

```md
Paradigma
├── Imperativo: paso a paso, controla el estado.
├── Declarativo: especifica el resultado, no el procedimiento.
├── Orientado a objetos: entidades con atributos y métodos.
├── Funcional: funciones puras, sin efectos secundarios.
└── Lógico: deducción y reglas lógicas.
```

---

## Conclusión

La elección del paradigma depende de:

- El **tipo de problema** a resolver.
- El **entorno de desarrollo**.
- La **experiencia** del programador.
- Las **características** del lenguaje disponible.

En la práctica, la mayoría de proyectos combinan varios paradigmas para aprovechar sus ventajas y compensar sus limitaciones.
