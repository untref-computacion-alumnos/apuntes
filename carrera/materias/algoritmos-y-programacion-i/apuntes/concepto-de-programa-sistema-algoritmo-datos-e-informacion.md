# Concepto de programa, sistema, algoritmo, datos e información

Comprender estos conceptos es esencial para entender cómo se resuelven problemas mediante herramientas informáticas y cómo se procesa la información de manera sistemática.

---

## Programa

### Definición

Un **programa** es un conjunto finito y ordenado de instrucciones que una computadora puede interpretar y ejecutar para realizar una tarea específica.

Estas instrucciones están escritas en un **lenguaje de programación**, el cual debe seguir reglas precisas de sintaxis y semántica para que el computador pueda comprenderlo.

### Características

- Es **finito**: Contiene un número limitado de instrucciones.
- Es **preciso**: Las instrucciones deben estar claramente definidas.
- Es **ejecutable**: Se puede llevar a cabo en una computadora u otro dispositivo programable.
- Produce **resultados** a partir de **datos de entrada**.
- Puede ser interactivo (responde a acciones del usuario) o autónomo.

### Ejemplo

En pseudocódigo, un programa que calcule el área de un triángulo:

```md
Inicio
Leer base
Leer altura
area ← (base \* altura) / 2
Mostrar area
Fin
```

---

## Sistema

### Definición

Un **sistema** es un conjunto de elementos interrelacionados que interactúan entre sí para lograr un objetivo común.

En el ámbito informático, un **sistema informático** está formado por **hardware**, **software** y, en muchos casos, **usuarios** que trabajan de manera coordinada para procesar datos y generar información útil.

### Características

- Tiene un **objetivo definido**.
- Está formado por **componentes** que interactúan.
- Existe un **flujo de información** o materiales entre sus partes.
- Posee **límites** que lo separan de su entorno.
- Requiere **retroalimentación** (feedback) para mejorar o corregir su funcionamiento.

### Ejemplos de sistemas informáticos

- Sistema operativo.
- Sistema de gestión de bases de datos.
- Sistema de control de tráfico aéreo.

---

## Algoritmo

### Definición

Un **algoritmo** es un conjunto finito, ordenado y no ambiguo de pasos que permite resolver un problema o realizar una tarea.

Es independiente del lenguaje de programación y puede expresarse de múltiples maneras (lenguaje natural, diagramas de flujo, pseudocódigo, etc.).

### Propiedades

- **Finito**: Debe terminar después de un número limitado de pasos.
- **Preciso**: Cada paso debe ser claro y sin ambigüedades.
- **Definido**: Para una misma entrada, siempre produce la misma salida.
- **Eficiente**: Resuelve el problema usando la menor cantidad de recursos posible.

### Ejemplo

Algoritmo para determinar si un número es par o impar:

```text
Inicio
  Leer numero
  Si numero mod 2 = 0 Entonces
    Mostrar "Es par"
  Si No
    Mostrar "Es impar"
Fin
```

---

## Datos

### Definición

Los **datos** son representaciones simbólicas (números, letras, imágenes, sonidos, etc.) de hechos, conceptos o instrucciones.

Por sí solos carecen de significado hasta que son procesados o interpretados.

### Tipos de datos

- **Numéricos**: Enteros, decimales.
- **Alfanuméricos**: Combinaciones de letras y números.
- **Lógicos**: Valores de verdad (verdadero/falso).
- **Multimedia**: Imágenes, videos, audio.

### Ejemplo

- `25`
- `"Juan Pérez"`
- `3.14`

---

## Información

### Definición

La **información** es el resultado del procesamiento, organización e interpretación de los datos, de manera que adquieran significado y puedan ser útiles para la toma de decisiones.

### Características

- Es **significativa**: los datos adquieren contexto.
- Es **relevante** para el usuario.
- Puede ser **almacenada** y **transmitida**.
- Su **calidad** depende de su exactitud, actualidad y pertinencia.

### Ejemplo

- **Dato**: `35`
- **Información**: `35°C es la temperatura actual de la ciudad.`

---

## Relación entre los conceptos

| Concepto        | Pregunta que responde                                                  | Estado inicial o final                          |
| --------------- | ---------------------------------------------------------------------- | ----------------------------------------------- |
| **Datos**       | ¿Qué valores tenemos?                                                  | Materia prima                                   |
| **Información** | ¿Qué significan esos valores?                                          | Resultado del procesamiento                     |
| **Algoritmo**   | ¿Cómo resolver el problema?                                            | Plan o procedimiento                            |
| **Programa**    | ¿Cómo implementar el algoritmo en un computador?                       | Traducción del plan a instrucciones ejecutables |
| **Sistema**     | ¿Dónde se ejecuta el programa y cómo interactúa con otros componentes? | Entorno y estructura                            |

En resumen:

- **Los datos** se procesan mediante un **algoritmo**.
- El **algoritmo** se implementa en un **programa**.
- El **programa** se ejecuta dentro de un **sistema**.
- El resultado es **información** útil.

---

## Ejemplo integrador

**Problema**: Calcular el promedio de notas de un estudiante y determinar si aprueba.

- **Datos**: `7, 8, 6, 9`.
- **Algoritmo**:

  - Sumar todas las notas.
  - Dividir por la cantidad de notas.
  - Si el promedio es mayor o igual a 6, indicar "Aprobado", si no "Reprobado".

- **Programa** (pseudocódigo):

  ```text
  Inicio
    Leer nota1, nota2, nota3, nota4
    promedio ← (nota1 + nota2 + nota3 + nota4) / 4
    Si promedio >= 6 Entonces
      Mostrar "Aprobado"
    Si No
      Mostrar "Reprobado"
  Fin
  ```

- **Sistema**: PC con sistema operativo y un compilador/intérprete que permita ejecutar el programa.
-
- **Información**: "Promedio: 7.5 - Aprobado".
