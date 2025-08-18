# Pseudocódigo

El **pseudocódigo** es una forma de **describir algoritmos** usando un lenguaje informal, cercano al natural (en este caso, español), con estructuras y convenciones que lo hacen **preciso**, **legible** y **independiente** de cualquier lenguaje de programación. Es ideal para **pensar** soluciones, **comunicar** ideas y **documentar** antes (o además) de codificar.

---

## ¿Para qué sirve?

- **Diseño de algoritmos**: Pensar la solución sin tener en cuenta la sintaxis de un lenguaje.
- **Comunicación**: Equipos mixtos (docentes, estudiantes, devs) leen y entienden el mismo proceso.
- **Documentación**: Describe la intención y la lógica, no los detalles técnicos.
- **Puente al código**: Facilita traducir a Java, Python, Go, C, etc.

---

## Características deseables

- **Claridad**: Fácil de leer en voz alta.
- **Abstracción**: Ignora detalles no esenciales (tipos de bajo nivel, gestión de memoria, etc.).
- **Determinismo**: Cuando haga falta, cada paso debe dejar claro qué ocurre.
- **Estandarización interna**: Equipo/curso acuerda **convenciones** y las respeta.

---

## Convenciones de estilo (recomendadas)

- **Palabras clave en MAYÚSCULAS**: `INICIO`, `FIN`, `SI`, `MIENTRAS`, `PARA`, `SUBPROCESO`, etc.
- **Sangría** para bloques anidados (2–4 espacios).
- **Comentarios** con `//` (línea) o `/* ... */` (bloque).
- **Nombres en español y descriptivos**:
  - Variables: `suma`, `indice`, `maximo`, `contadorAciertos`
  - Funciones: `esPrimo(n)`, `buscarMaximo(lista)`
- **Índices de arreglos**: Por coherencia, este apunte usa **base 0** (`0..n-1`). Si se usa base 1, **declararlo** al inicio.
- **Operadores comunes**: `+ - * / %` (módulo), `^` (potencia cuando se indique), `== != < <= > >=`, `Y`, `O`, `NO`.

---

## Elementos del pseudocódigo

### Estructura general

```text
FUNCIÓN nombre_de_la_función:
    // Código
FIN FUNCIÓN
```

### Variables y tipos (nivel conceptual)

- **Numéricos**: `entero`, `real`
- **Lógicos**: `booleano` (`VERDADERO`, `FALSO`)
- **Texto**: `cadena`
- **Estructuras**: `arreglo`, `matriz`, `registro` (tupla/campos)
- **Colecciones**: `conjunto`, `lista`, `cola`, `pila` (si el curso lo admite)

> En pseudocódigo suelen omitirse declaraciones estrictas; si se usan, colocalas al inicio por claridad.

### Entrada/Salida

```text
LEER variable
ESCRIBIR expresion
```

Ejemplo:

```text
ESCRIBIR "Ingrese cantidad:"
LEER cantidad
```

### Asignación

```text
variable <- expresion
```

Ejemplo:

```text
promedio <- suma / cantidad
```

### Selección (condicionales)

```text
SI condicion ENTONCES:
    // bloque A
SI NO:
    // bloque B
FIN SI

// Múltiples ramas
SEGUN sea valor
    CASO v1:
        // ...
    CASO v2:
        // ...
    DE_OTRO_MODO:
        // ...
FIN SEGUN
```

### Repetición (bucles)

```text
MIENTRAS condicion HACER:
    // ...
FIN MIENTRAS

REPETIR:
    // ...
HASTA QUE condicion  // se detiene cuando la condición es VERDADERA

PARA i <- inicio HASTA fin HACER:        // paso +1 por defecto
    // ...
FIN PARA

PARA i <- inicio HASTA fin CON PASO p HACER:
    // ...
FIN PARA
```

**Control del flujo dentro del bucle** (si tu convención lo admite):

```text
CONTINUAR   // salta a la siguiente iteración
SALIR       // rompe el bucle actual
```

### Subprocesos y funciones

```text
SUBPROCESO mostrarTitulo(titulo: cadena)
    ESCRIBIR "==== ", titulo, " ===="
FIN SUBPROCESO

FUNCION esPar(n: entero) : booleano
    RETORNAR (n % 2 == 0)
FIN FUNCION
```

- **Parámetros**: por valor (copias) o por referencia (permite modificar). Si necesitas distinguir:

```text
SUBPROCESO intercambiar(REF a: entero, REF b: entero)
    temp <- a
    a <- b
    b <- temp
FIN_SUBPROCESO
```

### Ámbito

- Variables **locales** a un subproceso/función.
- Variables **globales** (evitarlas salvo necesidad didáctica).

### Estructuras de datos (conceptual)

**Arreglo** (1D):

```text
// arreglo de n enteros
DEFINIR notas[0..n-1] COMO entero
```

**Matriz** (2D):

```text
DEFINIR tablero[0..filas-1][0..cols-1] COMO entero
```

**Registro** (tupla):

```text
REGISTRO Alumno
    legajo: entero
    nombre: cadena
    promedio: real
FIN_REGISTRO

DEFINIR a COMO Alumno
a.legajo <- 123
a.nombre <- "Rosa"
a.promedio <- 8.7
```

**Pila/Cola** (interfaces):

```text
PILA P               // operaciones: APILAR(x), DESAPILAR(), CIMA(), ES_VACIA()
COLA Q               // operaciones: ENCOLAR(x), DESENCOLAR(), FRENTE(), ES_VACIA()
```

---

## Patrones y plantillas útiles

### Recorrer un arreglo

```text
PARA i <- 0 HASTA n - 1 HACER:
    // usar arreglo[i]
FIN PARA
```

### Acumulador y contador

```text
suma <- 0
contador <- 0
PARA i <- 0 HASTA n - 1 HACER:
    suma <- suma + arreglo[i]
    contador <- contador + 1
FIN PARA
promedio <- suma / contador
```

### Máximo/Mínimo

```text
maximo <- arreglo[0]
PARA i <- 1 HASTA n - 1 HACER:
    SI arreglo[i] > maximo ENTONCES:
        maximo <- arreglo[i]
    FIN SI
FIN PARA
```

### Búsqueda lineal (con posición)

```text
pos <- -1
PARA i <- 0 HASTA n - 1 HACER:
    SI arreglo[i] == buscado ENTONCES:
        pos <- i
        SALIR
    FIN SI
FIN PARA
```

### Recorrido de matriz

```text
PARA f <- 0 HASTA filas - 1 HACER:
    PARA c <- 0 HASTA cols - 1 HACER:
        // usar matriz[f][c]
    FIN PARA
FIN PARA
```

### Lectura hasta centinela

```text
LEER x
MIENTRAS x != CENTINELA HACER:
    // procesar x
    LEER x
FIN MIENTRAS
```

---

## Ejemplos completos

### Máximo común divisor (Euclides)

```text
FUNCION mcd(a: entero, b: entero) : entero
    // Pre: a ≥ 0, b ≥ 0, no ambos 0
    MIENTRAS b != 0 HACER:
        temp <- b
        b <- a % b
        a <- temp
    FIN MIENTRAS
    RETORNAR a
FIN FUNCION
```

**Invariante**: `mcd(a, b)` no cambia durante el bucle.
**Variante**: `b` disminuye (en valor absoluto) hasta 0.

---

### Búsqueda binaria (arreglo ordenado ascendente)

```text
FUNCION busquedaBinaria(A: arreglo de entero, n: entero, x: entero) : entero:
    // Pre: A[0..n - 1] está ordenado ascendente
    izq <- 0
    der <- n - 1
    MIENTRAS izq ≤ der HACER:
        medio <- (izq + der) DIV 2
        SI A[medio] == x ENTONCES:
            RETORNAR medio
        SINO SI A[medio] < x ENTONCES:
            izq <- medio + 1
        SINO:
            der <- medio - 1
        FIN SI
    FIN MIENTRAS
    RETORNAR -1     // no encontrado
FIN FUNCION
```

---

### Ordenamiento por inserción

```text
SUBPROCESO insercion(A: arreglo de entero, n: entero):
    PARA i <- 1 HASTA n - 1 HACER:
        clave <- A[i]
        j <- i - 1
        MIENTRAS j ≥ 0 Y A[j] > clave HACER:
            A[j + 1] <- A[j]
            j <- j - 1
        FIN_MIENTRAS
        A[j + 1] <- clave
    FIN PARA
FIN SUBPROCESO
```

## Correctitud y complejidad

### Especificación

- **Precondición**: Qué debe cumplirse **antes** (por ejemplo, “la lista está ordenada”).
- **Postcondición**: Qué garantiza **después** (por ejemplo, “retorna la posición o -1”).
- **Efectos colaterales**: Qué cambia (arreglos modificados, variables globales, etc.).

### Invariantes y variantes

- **Invariante de bucle**: Propiedad verdadera al **inicio de cada iteración**.
- **Variante**: Medida que **disminuye** y garantiza **terminación** (tamaño restante, índice decreciente, etc.).

---

## Validaciones y manejo de errores (a nivel algoritmo)

- **Chequear entradas**: `SI n ≤ 0 ENTONCES ESCRIBIR "Tamaño inválido"; RETORNAR`
- **Evitar división por cero**: Verificar denominadores.
- **Rangos**: Índices dentro de `0..n-1`.
- **Estados no válidos**: “cola vacía”, “pila vacía”, etc.

---

## Del pseudocódigo al código (mapeo rápido)

| Concepto   | Pseudocódigo            | Python               | Java                            |
| ---------- | ----------------------- | -------------------- | ------------------------------- |
| Asignación | `x <- 5`                | `x = 5`              | `int x = 5;`                    |
| Igualdad   | `a == b`                | `a == b`             | `a == b` (primitivos)           |
| Y/O/NO     | `Y` / `O` / `NO`        | `and` / `or` / `not` | `&&` / \`                       |
| Si/Sino    | `SI ... SINO ...`       | `if ... else:`       | `if (...) { ... } else { ... }` |
| Mientras   | `MIENTRAS ...`          | `while ...:`         | `while (...) { ... }`           |
| Para       | `PARA i <- 0 HASTA n-1` | `for i in range(n):` | `for (int i=0; i<n; i++)`       |
| Función    | `FUNCION f(...) : tipo` | `def f(...):`        | `static Tipo f(...) { ... }`    |
| Retornar   | `RETORNAR x`            | `return x`           | `return x;`                     |

> La traducción nunca es literal al 100%; respeta la **intención** y la **lógica**.

---

## Buenas prácticas

- **Nombrá** bien: `sumaPares`, `estaOrdenado`, `contadorErrores`.
- **Una tarea por función**: Subprocesos cortos y enfocados.
- **Evitá anidamiento profundo**: Extraé lógica a subprocesos.
- **Declará pre/postcondiciones** en comentarios.
- **Usá invariantes** en bucles complejos.
- **Sé consistente** con índices (base 0 o 1) y con comparaciones (`≤`, `<`).
- **Casos borde**: Listas vacías, un solo elemento, todos iguales, límites numéricos.

---

## Anti-patrones frecuentes

- **Pseudocódigo con sintaxis de un lenguaje específico** (pierde independencia).
- **Omitir condiciones clave** (“repetir hasta… ¿hasta qué?”).
- **Variables mágicas** sin explicar su propósito.
- **Efectos colaterales ocultos** (modificar estructuras sin documentarlo).
- **No considerar casos vacíos** (n = 0, lista vacía, etc.).

---

## Nota sobre dialectos de pseudocódigo

Existen variantes (académicas, de libros, herramientas como PSeInt). Lo importante es **acordar** y **ser consistente**: mismas palabras clave, misma base de índices, mismas reglas de estilo.

---

### Cierre

El pseudocódigo es un “lienzo lógico”: cuanto más claro y disciplinado se es al escribirlo, más fácil es **probar la correctitud**, **razonar sobre complejidad** y **traducirlo** a cualquier lenguaje.
