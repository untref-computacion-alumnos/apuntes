# Arreglos

## Definición

Un **arreglo** (o _array_) es una **estructura de datos lineal y estática** que permite almacenar múltiples valores del mismo tipo en una colección ordenada.

Cada valor dentro del arreglo se denomina **elemento**, y cada elemento puede ser accedido de manera directa mediante un **índice** numérico.

Ejemplo conceptual:

- Un arreglo de enteros con 5 elementos: `[10, 20, 30, 40, 50]`
- Accesos por índice:
  - `A[0] = 10`
  - `A[1] = 20`
  - `A[4] = 50`

---

## Características principales

- **Homogeneidad**: Todos los elementos son del mismo tipo (`int`, `char`, `float`, objetos, etc.).
- **Estática**: El tamaño del arreglo debe definirse al momento de su creación y no puede modificarse (en la mayoría de los lenguajes).
- **Acceso aleatorio**: Permite acceder directamente a cualquier elemento usando su índice en tiempo constante `O(1)`.
- **Memoria contigua**: Los elementos se almacenan de forma secuencial en memoria.

---

## Tipos de arreglos

### Arreglos unidimensionales

Son listas lineales de elementos, el caso más común.

Ejemplo en **Java**:

```java
int[] numbers = {10, 20, 30, 40, 50};
System.out.println(numbers[2]); // Salida: 30
```

Ejemplo en **Python** (listas, aunque dinámicas en realidad):

```python
numeros = [10, 20, 30, 40, 50]
print(numeros[2])  # imprime 30
```

---

### Arreglos bidimensionales

Se representan como **tablas** o **matrices** con filas y columnas.

Ejemplo en **Java**:

```java
int[][] matriz = {
  {1, 2, 3},
  {4, 5, 6},
  {7, 8, 9}
};
System.out.println(matriz[1][2]); // Salida: 6
```

Visualización:

```text
1 2 3
4 5 6
7 8 9
```

---

### Arreglos multidimensionales

Extienden la idea a tres o más dimensiones. Son útiles en aplicaciones como gráficos, procesamiento de imágenes o simulaciones.

Ejemplo en **Java**:

```java
int[][][] cube = new int[2][3][4];  // A¿rreglo de 3 dimensiones
```

---

### Arreglos dinámicos (o listas redimensionables)

En algunos lenguajes (por ejemplo, Python, Java con `ArrayList`, C++ con `vector`) se permite que el tamaño de los arreglos se ajuste dinámicamente en tiempo de ejecución.

Ejemplo en **Python**:

```python
lista = [1, 2, 3]
lista.append(4)    # [1, 2, 3, 4]
```

---

## Operaciones básicas con arreglos

### Acceso

```java
int[] array = {10, 20, 30, 40, 50};
int x = array[3]; // Acceso al cuarto elemento
```

### Recorrido

```java
int[] array = {10, 20, 30, 40, 50};

for (int i = 0; i < array.length; i++) {
  System.out.println(array[i]);
}
```

### Inserción (en arreglos estáticos no es directa, requiere desplazar elementos)

```java
int[] array = {10, 20, 30, 0, 0};
int n = 3;  // Cantidad de elementos reales
int pos = 1, value = 15;

// Desplazar
for (int i = n; i > pos; i--) {
  array[i] = array[i-1];
}
array[pos] = value;
n++;
```

### Eliminación

```java
int pos = 2;  // Eliminar en la posición 2
for (int i = pos; i < n - 1; i++) {
  array[i] = array[i + 1];
}
n--;
```

### Búsqueda

- **Lineal**: Recorre todos los elementos.
- **Binaria**: Requiere un arreglo ordenado, divide el espacio de búsqueda.

---

## Ventajas y desventajas

### Ventajas

- Acceso rápido a los elementos mediante índices.
- Representación compacta en memoria.
- Facilidad de implementación.

### Desventajas

- Tamaño fijo (en la mayoría de lenguajes).
- Costosa la inserción o eliminación (requiere mover elementos).
- No puede almacenar tipos heterogéneos (excepto en lenguajes dinámicos).

---

## Aplicaciones de los arreglos

- Implementación de otras estructuras de datos: pilas, colas, listas.
- Representación de matrices matemáticas.
- Procesamiento de imágenes y señales.
- Ordenamiento y búsqueda de datos.
- Simulaciones físicas y gráficas en múltiples dimensiones.

---

## Representación en memoria

Dado un arreglo `A` de tipo `int` y tamaño `n`, almacenado en dirección base `dir_base`:

```text
Dirección de A[i] = dir_base + (i * tamaño_elemento)
```

Ejemplo:

- `A[0]` → `dir_base`
- `A[1]` → `dir_base + 4` (si cada entero ocupa 4 bytes)
- `A[2]` → `dir_base + 8`

Esto permite el acceso directo en tiempo constante.

---

## Conclusión

Los **arreglos** son una de las estructuras de datos más importantes y fundamentales en programación.

Aunque presentan limitaciones como su tamaño fijo y dificultad en inserciones/eliminaciones, su eficiencia en **acceso aleatorio** y simplicidad los convierte en la base de estructuras más complejas y en un recurso esencial en problemas de cómputo, matemáticas y ciencias aplicadas.
