# Algoritmos de Ordenamiento

## Conceptos

### Ordenamiento

El **ordenamiento** es el proceso de **reorganizar un conjunto de elementos** según un criterio definido, llamado **clave** (_key_), de manera que cumpla un **orden lineal** o secuencial.

El ordenamiento es fundamental en informática, ya que facilita **búsquedas rápidas, análisis de datos y optimización de algoritmos posteriores**.

---

### Orden Lineal

Un **orden lineal** es una relación binaria `<=` que cumple las siguientes propiedades:

- **Reflexiva**: Todo elemento se relaciona consigo mismo (`a <= a`).
- **Transitiva**: Si `a <= b` y `b <= c`, entonces `a <= c`.
- **Antisimétrica**: Si `a <= b` y `b <= a`, entonces `a = b`.
- **Total**: Cualquier par de elementos es comparable:

  ```text
  a <= b XOR b <= a
  ```

---

### Clave (Key)

- La **clave** es la parte del elemento que determina su posición relativa en el ordenamiento.
- Un mismo elemento puede tener múltiples atributos, pero la **clave** define el criterio de comparación.

> Ejemplo: Un registro de estudiante `{nombre, promedio, edad}` puede ordenarse por promedio (`key = promedio`) o por edad (`key = edad`).

---

### Definición formal

Dado los elementos **$e_1$, $e_2$, ..., $e_n$** con los valores claves **$k_1$, $k_2$, ..., $k_n$** respectivamente, debe resultar el mismo grupo de elementos en orden **$e_{i1}$, $e_{i2}$, ..., $e_{in}$** tal que **$k_{i1}$ <= $k_{i2}$ <= ... <= $k_{in}$**.

---

### Características

- No todos los elementos necesitan tener claves distintas.
- Los elementos con la misma clave no necesariamente deben mantener su orden original (estable o inestable).
- El ordenamiento puede ser **ascendente** (`<=`) o **descendente** (`>=`).

---

## Clasificación de Algoritmos de Ordenamiento

### Internos

- Se realizan completamente en **memoria principal (RAM)**.
- Aprovechan el **acceso aleatorio** para mover datos rápidamente.
- Ideales para conjuntos de datos que **caben en memoria**.

### Externos

- Se realizan parcialmente o completamente en **memoria secundaria** (disco).
- Necesarios cuando los datos son **demasiado grandes para la memoria RAM**.
- Emplean técnicas de **ordenamiento por bloques y fusión**.

---

### Algoritmos Simples

- **BubbleSort**
- **InsertionSort**
- **SelectionSort**

### Algoritmos Avanzados

- **QuickSort**
- **HeapSort**
- **MergeSort**
- **RadixSort**
- **BucketSort**

---

## Operación básica: Intercambio de elementos

Muchos algoritmos de ordenamiento requieren **intercambiar** elementos:

```text
FUNCIÓN intercambiar(arreglo, posición1, posición2):
  auxiliar <- arreglo[posición1]
  arreglo[posición1] <- arreglo[posición2]
  arreglo[posición2] <- auxiliar
FIN FUNCIÓN
```

```java
public static void swap(int[] arr, int pos1, int pos2) {
  int aux = arr[pos1];
  arr[pos1] = arr[pos2];
  arr[pos2] = aux;
}
```

---

## Algoritmos de Ordenamiento Simples

### SelectionSort

#### Idea básica

1. Buscar el **menor elemento** del arreglo.
2. Colocarlo en la **primera posición**.
3. Repetir el proceso con el subarreglo restante hasta ordenar todo.

#### Pseudocódigo

```text
FUNCIÓN selectionSort(arreglo):
  PARA i EN 0 .. |arreglo| - 1:
    posición_menor <- i
    PARA j EN i + 1 .. |arreglo| - 1:
      SI arreglo[j] < arreglo[posición_menor] ENTONCES
        posición_menor <- j
      FIN SI
    FIN PARA
    intercambiar(arreglo, i, posición_menor)
  FIN PARA
FIN FUNCIÓN
```

#### Código en Java

```java
public static void selectionSort(int[] arr) {
  for (int i = 0; i < arr.length - 1; i++) {
    int minIndex = i;
    for (int j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    swap(arr, i, minIndex);
  }
}
```

---

### BubbleSort

#### Idea básica

- Comparar **pares de elementos adyacentes** y mover los mayores hacia el final, como burbujas que suben.
- Repetir hasta que no haya más intercambios.

#### Pseudocódigo

```text
FUNCIÓN bubbleSort(arreglo):
  huboIntercambios <- true
  MIENTRAS huboIntercambios:
    huboIntercambios <- false
    PARA i EN 1 .. |arreglo| - 1:
      SI arreglo[i] < arreglo[i - 1] ENTONCES
        intercambiar(arreglo, i, i - 1)
        huboIntercambios <- true
      FIN SI
    FIN PARA
  FIN MIENTRAS
FIN FUNCIÓN
```

#### Código en Java

```java
public static void bubbleSort(int[] arr) {
  boolean swapped;
  int n = arr.length;
  do {
    swapped = false;
    for (int i = 1; i < n; i++) {
      if (arr[i] < arr[i - 1]) {
        swap(arr, i, i - 1);
        swapped = true;
      }
    }
  } while (swapped);
}
```

---

### InsertionSort

#### Idea básica

- Tomar cada elemento y **colocarlo en la posición correcta** dentro del subarreglo previamente ordenado.
- Muy eficiente para **arreglos pequeños o casi ordenados**.

#### Pseudocódigo

```text
FUNCIÓN insertionSort(arreglo):
  PARA i EN 1 .. |arreglo| - 1:
    elemento <- arreglo[i]
    j <- i - 1
    MIENTRAS j >= 0 Y arreglo[j] > elemento:
      arreglo[j+1] <- arreglo[j]
      j <- j - 1
    FIN MIENTRAS
    arreglo[j + 1] <- elemento
  FIN PARA
FIN FUNCIÓN
```

#### Código en Java

```java
public static void insertionSort(int[] arr) {
  for (int i = 1; i < arr.length; i++) {
    int key = arr[i];
    int j = i - 1;
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key;
  }
}
```

---

## Consideraciones adicionales

- La **elección del algoritmo** depende del **tamaño de los datos** y la **frecuencia de ordenamiento**.
- Para **grandes volúmenes** de datos, se prefieren algoritmos avanzados como **QuickSort**, **MergeSort** o **HeapSort**.
- Los algoritmos simples son útiles para **enseñanza, depuración y arreglos pequeños**.
- La **estabilidad** es importante si los elementos tienen **múltiples claves** y se desea preservar el orden original de claves iguales.

---

## Conclusión

Los **algoritmos de ordenamiento simples** proporcionan una **base conceptual** para entender cómo organizar datos.

Conocer sus **pseudocódigos, implementaciones y complejidades** permite:

- Elegir el algoritmo más adecuado según el contexto.
- Optimizar rendimiento y memoria.
- Comprender los algoritmos avanzados que combinan o mejoran estas técnicas.
