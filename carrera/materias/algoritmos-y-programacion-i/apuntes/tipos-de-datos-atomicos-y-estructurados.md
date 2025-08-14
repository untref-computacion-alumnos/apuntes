# Tipos de Datos Atómicos y Estructurados

En programación y ciencias de la computación, un **tipo de dato** define el conjunto de valores que una variable puede tomar y las operaciones que se pueden realizar sobre esos valores.

Los tipos de datos se clasifican principalmente en **atómicos** y **estructurados**.

---

## Tipos de Datos Atómicos

### Definición

Un **tipo de dato atómico** (o primitivo) es aquel que **no se puede descomponer** en elementos más simples desde el punto de vista del lenguaje de programación.

Son los bloques básicos con los que se construyen estructuras más complejas.

### Características

- **Indivisibles** para el lenguaje.
- Representan valores simples.
- Generalmente están predefinidos por el lenguaje.
- Sirven como base para crear tipos más complejos.

### Ejemplos comunes

Dependiendo del lenguaje, los nombres y tamaños pueden variar, pero los más habituales son:

| Tipo                                | Descripción                                                              | Ejemplo         |
| ----------------------------------- | ------------------------------------------------------------------------ | --------------- |
| Entero (`int`)                      | Números enteros positivos o negativos                                    | `42`, `-7`      |
| Real / Flotante (`float`, `double`) | Números con decimales                                                    | `3.14`, `-0.5`  |
| Carácter (`char`)                   | Un único símbolo alfanumérico                                            | `'A'`, `'9'`    |
| Booleano (`bool`)                   | Valores lógicos                                                          | `True`, `False` |
| Cadena de texto (`string`)          | Secuencia de caracteres (en algunos lenguajes se considera estructurado) | `"Hola"`        |

> **Nota:** Algunos lenguajes tratan las cadenas como estructuras de caracteres, mientras que otros las consideran atómicas.

---

## Tipos de Datos Estructurados

### Definición

Un **tipo de dato estructurado** es aquel que **agrupa varios valores**, que pueden ser del mismo tipo o de tipos diferentes.

Se construyen a partir de tipos atómicos u otros tipos estructurados.

### Características

- Están compuestos por **subelementos**.
- Pueden almacenar múltiples valores.
- Facilitan la organización y manipulación de grandes volúmenes de datos.
- Pueden ser **homogéneos** (mismo tipo de dato) o **heterogéneos** (distintos tipos).

### Ejemplos comunes

| Tipo estructurado      | Descripción                                                      | Ejemplo en pseudocódigo                        |
| ---------------------- | ---------------------------------------------------------------- | ---------------------------------------------- |
| **Arreglo / Vector**   | Conjunto de elementos del mismo tipo, de tamaño fijo o dinámico  | `notas[5] = {7,8,6,9,5}`                       |
| **Matriz**             | Arreglo bidimensional o multidimensional                         | `matriz[3][3]`                                 |
| **Registro / Struct**  | Colección de campos de distintos tipos, identificados por nombre | `Alumno: {nombre: "Ana", edad: 20, nota: 8.5}` |
| **Lista**              | Colección ordenada de elementos, normalmente de tamaño dinámico  | `["rojo", "verde", "azul"]`                    |
| **Cola**               | Estructura FIFO (First In, First Out)                            | `[1,2,3]` → sale 1 primero                     |
| **Pila**               | Estructura LIFO (Last In, First Out)                             | `[1,2,3]` → sale 3 primero                     |
| **Diccionario / Mapa** | Colección de pares clave-valor                                   | `{ "id": 1, "nombre": "Juan" }`                |

---

## Comparación entre datos atómicos y estructurados

| Característica   | Atómicos                  | Estructurados                         |
| ---------------- | ------------------------- | ------------------------------------- |
| Complejidad      | Simples                   | Compuestos                            |
| División interna | No tienen                 | Sí tienen                             |
| Ejemplos         | Enteros, booleanos        | Arreglos, registros                   |
| Uso principal    | Almacenar valores básicos | Organizar múltiples valores           |
| Creación         | Generalmente predefinidos | Se construyen a partir de otros tipos |

---

## Ejemplo

**Problema**: Almacenar y mostrar información de un alumno.

### Usando tipos atómicos

```java
String nombre = "Ana"   // string
int edad = 20           // int
double notaFinal = 8.5  // double
```

### Usando un tipo estructurado

```java
int[] notasAlumno = {4, 7, 8, 5}
```

En este caso, el **array** (tipo estructurado) agrupa en una sola variable los datos atómicos de las notas de alumnos.

---

## Importancia en programación

- Permiten elegir la **representación más adecuada** para la información.
- Facilitan la **organización de datos**.
- Mejoran la **eficiencia** del programa al usar tipos apropiados.
- Hacen posible implementar estructuras complejas como **árboles, grafos y bases de datos**.

---

## Conclusión

Los **tipos de datos atómicos** son la base para el manejo de información en cualquier lenguaje de programación, mientras que los **estructurados** permiten organizar y manipular grandes conjuntos de datos de forma eficiente.

El dominio de ambos es esencial para diseñar programas robustos, escalables y fáciles de mantener.
