# Algoritmos de Búsqueda

## Conceptos

### Búsqueda

La **búsqueda** es el proceso mediante el cual se **localiza o recupera uno o más elementos** de un conjunto de datos a partir de una **clave** específica.

Es una operación fundamental en informática, ya que muchos problemas dependen de **encontrar información rápidamente**.

---

### Características de la búsqueda

El resultado de una búsqueda puede ser:

- **Ningún elemento**: La clave no existe en el conjunto.
- **Un elemento**: La clave es única y se encuentra un único resultado.
- **Más de un elemento**: Varias entradas cumplen la condición de búsqueda (en colecciones no únicas).

---

### Clasificación general

Los algoritmos de búsqueda se pueden clasificar según:

- **Lugar de ejecución:**

  - Internos: Memoria principal (RAM).
  - Externos: Memoria secundaria (discos, bases de datos masivas).

- **Principio de operación:**
  - Basados en **comparaciones de claves** (Secuencial, Binaria).
  - Basados en **transformaciones de claves** (Hashing, tablas de dispersión).

---

## Algoritmos de Búsqueda Interna

### Búsqueda secuencial (lineal)

#### Consideraciones

- Método más simple de búsqueda.
- No requiere que los datos estén ordenados.
- También se conoce como **búsqueda lineal**.
- Tiempo de ejecución proporcional al tamaño del conjunto.

#### Idea básica

Recorrer los elementos **uno por uno** hasta encontrar el elemento buscado.

#### Pseudocódigo

```text
FUNCIÓN secuencial(arreglo, elemento):
  i <- 0
  posición <- -1
  MIENTRAS i < |arreglo| Y posición = -1:
    SI arreglo[i] = elemento ENTONCES:
      posición <- i
    FIN SI
    i <- i + 1
  FIN MIENTRAS
  RETORNAR posición
FIN FUNCIÓN
```

#### 2.1.4 Código en Java

```java
public static int busquedaSecuencial(int[] arr, int elem) {
  for (int i = 0; i < arr.length; i++) {
    if (arr[i] == elem) {
      return i;
    }
  }
  return -1;
}
```

---

### Búsqueda binaria

#### Consideraciones

- Requiere que el **arreglo esté ordenado** previamente.
- Basada en **división y conquista**, reduciendo el espacio de búsqueda a la mitad en cada iteración.
- Tiempo de ejecución mucho más eficiente que la búsqueda secuencial.

#### Idea básica

1. Comparar el **elemento del medio** con el elemento buscado.
2. Si es igual, se retorna la posición.
3. Si es menor, se descarta la mitad izquierda; si es mayor, se descarta la mitad derecha.
4. Repetir hasta encontrar el elemento o agotar el rango.

#### Pseudocódigo

```text
FUNCIÓN binaria(arreglo, elemento):
  izquierda <- 0
  derecha <- |arreglo| - 1
  posición <- -1
  MIENTRAS izquierda <= derecha Y posición = -1:
    medio <- (izquierda + derecha) / 2
    SI arreglo[medio] = elemento ENTONCES:
      posición <- medio
    FIN SI
    SI arreglo[medio] < elemento ENTONCES:
      izquierda <- medio + 1
    FIN SI
    SI arreglo[medio] > elemento ENTONCES:
      derecha <- medio - 1
    FIN SI
  FIN MIENTRAS
  RETORNAR posición
FIN FUNCIÓN
```

#### Código en Java

```java
public static int busquedaBinaria(int[] arr, int elem) {
  int left = 0;
  int right = arr.length - 1;
  while (left <= right) {
    int mid = left + (right - left) / 2;
    if (arr[mid] == elem) {
      return mid;
    }
    if (arr[mid] < elem) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return -1;
}
```

#### Observaciones

- Eficiente para **grandes conjuntos ordenados**.
- Puede implementarse de manera **iterativa** (como arriba) o **recursiva**.

---

## Algoritmos basados en transformaciones de claves

- Se utilizan para **búsquedas más rápidas**, especialmente en **bases de datos y grandes conjuntos de información**.
- Se basa en **Hashing**, donde la clave se transforma mediante una **función hash** que determina directamente la posición del elemento.
- Permite un acceso cercano a `O(1)` en promedio.
- Se aborda en estructuras como **HashMap, HashSet, tablas de dispersión**.

---

## Conclusión

- Elegir el algoritmo adecuado depende del **tipo de datos**, el **tamaño del conjunto** y la **frecuencia de búsquedas**.
- **Búsqueda secuencial**: Simple, flexible, eficiente para conjuntos pequeños.
- **Búsqueda binaria**: Requiere ordenamiento previo, muy eficiente en conjuntos grandes.
- **Hashing**: Excelente para acceso rápido, especialmente con claves únicas y estructuras de datos dinámicas.
