# Tipos Abstractos de Datos (TAD)

## Definición

Un **Tipo Abstracto de Dato (TAD)** es un modelo o concepto matemático que define **qué operaciones** se pueden realizar sobre un conjunto de datos y **qué significado tienen** esas operaciones, **sin especificar cómo se implementan internamente**.

En otras palabras, un TAD describe la **lógica** y **comportamiento** de un tipo de dato, ocultando los detalles de su implementación. Esto permite que el programador utilice un TAD sin preocuparse por la estructura interna que lo soporta.

---

## Principios fundamentales

### Encapsulamiento

- Los detalles internos de almacenamiento y manejo de datos están ocultos.
- Solo se accede a los datos a través de operaciones definidas.

### Independencia de implementación

- Un mismo TAD puede tener múltiples implementaciones distintas.
- Cambiar la implementación no afecta a quienes usan el TAD, siempre que la interfaz se mantenga.

### Interfaaz bien definida

- Se especifican las operaciones que se pueden realizar (nombre, parámetros, resultado esperado).
- No se exponen detalles innecesarios.

---

## Diferencias entre tipo de dato y TAD

| Característica       | Tipo de Dato (primitivo)   | Tipo de Dato Abstracto                          |
| -------------------- | -------------------------- | ----------------------------------------------- |
| Nivel de abstracción | Bajo (cercano al hardware) | Alto (conceptual)                               |
| Ejemplos             | `int`, `float`, `bool`     | Lista, Cola, Pila                               |
| Implementación       | Fija en el lenguaje        | Definida por el programador o biblioteca        |
| Flexibilidad         | Limitada                   | Alta                                            |
| Uso                  | Valores simples            | Estructuras complejas con operaciones definidas |

---

## Ejemplos de TAD y operaciones asociadas

### Pila (Stack)

- **Modelo**: LIFO (Last In, First Out)
- **Operaciones básicas**:
  - `apilar(elemento)` o `push(element)`: Inserta un elemento.
  - `desapilar()` o `pop()`: Elimina el último elemento, puede retornarlo.
  - `cima()` o `top()`: Retorna el último elemento sin eliminarlo.
  - `vacía()` o `isEmpty()`: Indica si la pila está vacía.

### Cola (Queue)

- **Modelo**: FIFO (First In, First Out)
- **Operaciones básicas**:
  - `encolar(elemento)` o `enqueue(element)`: Inserta un elemento al final.
  - `desencolar()` o `dequeue()`: Elimina el primer elemento, puede retornarlo.
  - `frente()` o `front()`: Retorna el primer elemento sin eliminarlo.
  - `vacía()` o `isEmpty()`: Indica si la cola está vacía.

### Lista (List)

- **Modelo**: Colección ordenada de elementos.
- **Operaciones básicas**:
  - `insertar(posición, elemento)` o `insert(position, element)`: Inserta un elemento en la posición específica.
  - `eliminar(posición)` o `remove(position)`: Elimina el elemento en esa posición. También se puede implementar por búsqueda del elemento.
  - `obtener(posición)` o `find(position)`: Retorna el elemento de esa posición. También se puede buscar al elemento.
  - `tamaño()` o `size()`: Retorna la cantidad de elementos.

### Conjunto (Set)

- **Modelo**: Colección no ordenada sin elementos repetidos.
- **Operaciones básicas**:
  - `insertar(posición)` o `insert(position)`: Agrega un elemento.
  - `eliminar(elemento)` o `remove(element)`: Elimina un elemento.
  - `contiene(elemento)` o `contains(element)`: Verifica si está presente.
  - `union`, `intersección`, `diferencia`, etc.: Operaciones entre conjuntos

### Diccionario (Dictioary) / Mapa (Map)

- **Modelo**:
- **Operaciones básicas**:
  - `insertar(clave, valor)` o `put(key, value)`: Inserta un valor con la clave dada.
  - `eliminar(clave)` o `remove(key)`: Elimina el par clave valor.
  - `obtener(clave)` o `get(key)`: Obtiene el valor de la clave dada.
  - `contiene(key)` o `exist(key)`: Verifica si existe la clave.

## Implementaciones posibles

Aunque el concepto de TAD es independiente de su implementación, en la práctica se utilizan estructuras concretas para materializarlo:

| TDA         | Implementaciones comunes                        |
| ----------- | ----------------------------------------------- |
| Pila        | Arreglo dinámico, lista enlazada                |
| Cola        | Arreglo circular, lista enlazada                |
| Lista       | Lista enlazada simple o doble, arreglo dinámico |
| Conjunto    | Tabla hash, árbol balanceado                    |
| Diccionario | Tabla hash, árbol binario de búsqueda           |

---

## Ventajas de usar TADs

- **Modularidad**: Cada TAD se implementa y prueba por separado.
- **Reutilización**: Se puede usar en múltiples programas.
- **Mantenibilidad**: Los cambios en la implementación no afectan al código que lo utiliza.
- **Claridad**: El código se entiende mejor gracias a interfaces bien definidas.
- **Abstracción**: Se centra en lo que hace, no en cómo lo hace.

---

## Ejemplo: Implementación de Stack en Java

```java
/**
 * Implementación de Stack en Java utilizando internamente una lista enlazada.
 */
public class Stack<T> {
  private java.util.LinkedList<T> elements = new java.util.LinkedList<>();

  public void push(T element) {
    elements.addFirst(element);
  }

  public T pop() {
    if (isEmpty()) {
      throw new IllegalStateException("Empty stack");
    }
    return elements.removeFirst();
  }

  public T top() {
    if (isEmpty()) {
      throw new IllegalStateException("Empty stack");
    }
    return elements.getFirst();
  }

  public boolean isEmpty() {
    return elements.isEmpty();
  }

  public int size() {
    return elements.size();WW
  }
}
```

---

## Conclusión

Los **Tipos Abstractos de Datos** son una herramienta fundamental para desarrollar software modular, escalable y fácil de mantener.

Separan el **qué** (operaciones disponibles) del **cómo** (implementación), permitiendo reutilizar y mejorar componentes sin afectar al resto del sistema.

Conocer y manejar TADs como **pilas**, **colas**, **listas**, **conjuntos** y **diccionarios**
