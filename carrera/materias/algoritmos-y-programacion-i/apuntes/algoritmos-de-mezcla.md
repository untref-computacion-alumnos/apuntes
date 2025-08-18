# Algoritmos de Mezcla

La **mezcla** (merge) es el proceso de **fusionar dos o más secuencias ya ordenadas** en una **nueva secuencia** que **preserva** ese orden. Es una operación central en estructuras y algoritmos (por ejemplo, en _Merge Sort_, en índices de bases de datos, en procesamiento de streams y en ordenamiento externo).

---

## Conceptos y utilidad

### Definición (intuición)

Dadas dos colecciones **A** y **B** _ya ordenadas_ (por la misma clave y en el mismo sentido), producir una tercera colección **C** que contenga **todos** sus elementos en **orden ascendente** (o descendente).

### ¿Por qué es útil?

- **Evita reordenar desde cero**: Si A y B ya están ordenados, podemos combinar en tiempo lineal **O(|A| + |B|)**.
- **Estabilidad**: Si se desea, la mezcla puede ser **estable** (al encontrar claves iguales, los elementos de A mantienen su orden relativo respecto de los de B).
- **Escalable**: Base del **ordenamiento externo** (con discos) y de la **mezcla k-vías** (k listas/archivos).

---

## Propiedades y requisitos

- Las listas de entrada se asumen **ordenadas** por la **misma clave** y **en el mismo sentido**.
- La mezcla resulta **lineal** en el tamaño total.
- Puede ser **estable** o no, según la regla de desempate para claves iguales.
- **Memoria**: Típicamente se usa un **arreglo destino** (o lista) para escribir el resultado; hay variantes _in-place_.

---

## Mezcla lineal clásica (manteniendo orden ascendente)

### Idea básica

Mantener dos índices (**i** en A, **j** en B). En cada paso:

- Comparar `A[i]` con `B[j]`.
- Copiar a C el **menor** (o el que deba ir primero).
- Avanzar el índice del arreglo del que se copió.
- Al terminar uno, **copiar el resto** del otro.

### Pseudocódigo (estable)

```text
FUNCIÓN mezcla(A, B):
  C <- nuevo arreglo de tamaño |A| + |B|
  i <- 0
  j <- 0
  k <- 0
  MIENTRAS i < |A| Y j < |B|:
    SI A[i] <= B[j] ENTONCES:
      C[k] <- A[i]
      i <- i + 1
    SI NO:
      C[k] <- B[j]
      j <- j + 1
    FIN SI
    k <- k + 1
  FIN MIENTRAS
  MIENTRAS i < |A|:
    C[k] <- A[i]
    i <- i + 1
    k <- k + 1
  FIN MIENTRAS
  MIENTRAS j < |B|:
    C[k] <- B[j]
    j <- j + 1
    k <- k + 1
  FIN MIENTRAS
  RETORNAR C
FIN FUNCIÓN
```

### Java (enteros)

```java
public static int[] mergeAsc(int[] A, int[] B) {
  int n = A.length, m = B.length;
  int[] C = new int[n + m];
  int i = 0, j = 0, k = 0;
  while (i < n && j < m) {
    if (A[i] <= B[j]) {
      C[k++] = A[i++];
    } else {
      C[k++] = B[j++];
    }
  }
  while (i < n) {
    C[k++] = A[i++];
  }
  while (j < m) {
    C[k++] = B[j++];
  }
  return C;
}
```

### Java (genérico + `Comparator<T>`)

```java
public static <T> List<T> mergeAsc(List<T> A, List<T> B, Comparator<? super T> cmp) {
  ArrayList<T> C = new ArrayList<>(A.size() + B.size());
  int i = 0, j = 0;
  while (i < A.size() && j < B.size()) {
    if (cmp.compare(A.get(i), B.get(j)) <= 0) {
      C.add(A.get(i++));
    } else {
      C.add(B.get(j++));
    }
  }
  while (i < A.size()) C.add(A.get(i++));
  while (j < B.size()) C.add(B.get(j++));
  return C;
}
```

### Invariante (correctitud, bosquejo)

Al inicio de cada iteración, `C[0..k-1]` contiene los k menores elementos de `A∪B` en orden ascendente, y `A[i]` y `B[j]` son los **siguientes candidatos** más pequeños de sus listas. La comparación elige el siguiente en orden y aumenta el puntero correspondiente. Terminar una lista implica que la otra contiene los **mayores restantes**, por lo que basta **copiar**.

---

## Mezcla lineal v2 (A concatenado con B invertido)

### Idea

Evitar dos bucles finales usando **una sola pasada** sobre una **estructura intermedia**:

1. Crear `C = A ⧺ reverse(B)`.
2. Dos punteros: `i` al inicio (A), `j` al final (inicio lógico de B original).
3. Extraer siempre el **menor** entre `C[i]` y `C[j]` y avanzar/retroceder el puntero correspondiente.
4. Escribir en `D` (resultado) hasta completarlo.

> Observación clave: al tomar `C[j]` desde el extremo derecho de `C`, se consumen los elementos de **B en su orden original**.

### Pseudocódigo (con estabilidad hacia A)

```text
FUNCIÓN mezcla(arregloA, arregloB):
  arregloC <- nuevo arreglo de tamaño |arregloA| + |arregloB|
  arregloD <- nuevo arreglo de tamaño |arregloA| + |arregloB|
  arregloC <- *arregloA
  arregloC <- *arregloB⁻¹
  i <- 0
  k <- 0
  j <- |arregloC| - 1
  MIENTRAS k < |arregloD|:
    SI arregloC[i] < arregloC[j] ENTONCES:
      arregloD[k] <- arregloC[i]
      i++
    SI NO:
      arregloD[k] <- arregloC[j]
      j--
    FIN SI
    k++
  FIN MIENTRAS
  RETORNAR arregloD
FIN FUNCIÓN
```

### Java (enteros)

```java
public static int[] mergeAscV2(int[] A, int[] B) {
  int n = A.length, m = B.length, N = n + m;
  int[] C = new int[N];
  System.arraycopy(A, 0, C, 0, n);
  for (int q = 0; q < m; q++) {
    C[n + q] = B[m - 1 - q];
  }
  int[] D = new int[N];
  int i = 0, j = N - 1, k = 0;
  while (k < N) {
    if (C[i] <= C[j]) {
      D[k++] = C[i++];
    } else {
      D[k++] = C[j--];
    }
  }
  return D;
}
```

#### Comentarios

- **Estabilidad**: Con `<=` se prioriza A; los elementos de B se consumen por el puntero derecho en **orden original**, preservando su estabilidad interna.
- **Ventaja**: Un único lazo para la mezcla final, sin “colas” separadas.

---

## Casos borde y validación

- A vacío, B no vacío → C = B.
- B vacío, A no vacío → C = A.
- A y B del mismo tamaño o muy desbalanceados.
- Elementos **repetidos** → verificar **estabilidad** (¿A antes que B?).
- Tipos con **comparador**: asegurar que el `Comparator` sea **consistente** (reflexivo, antisimétrico, transitivo).

---

## Errores comunes

- **Off-by-one**: Índices fuera de rango (j < m vs j <= m − 1).
- Olvidar **copiar el remanente** de A o de B (en la versión clásica).
- Comparación equivocada (usar `<` cuando se quiere estabilidad→usar `<=`).
- No usar **misma clave/sentido** de orden en A y B.
- En v2, **olvidar invertir B** o confundir el puntero derecho.
