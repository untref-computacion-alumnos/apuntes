# Axiomas

Los **axiomas** son **enunciados o proposiciones aceptados como verdaderos sin necesidad de demostración**.

En el contexto de la programación y el diseño de software, los axiomas sirven como **principios fundamentales** sobre los que se construyen especificaciones, contratos y modelos formales.

---

## Definición general

Un **axioma** es:

- Una afirmación **básica y evidente** que se toma como verdadera.
- Punto de partida para deducir otras verdades (teoremas).
- **No se demuestra**, se **acepta** como base lógica.
- Se utiliza como **fundamento** para construir teorías o sistemas.

---

## Axiomas en programación

En ingeniería de software, los axiomas se aplican para:

1. **Definir el comportamiento esperado** de tipos abstractos de datos (TAD).
2. **Formalizar contratos** entre módulos, clases u objetos.
3. **Establecer reglas inmutables** sobre las que se apoya el sistema.
4. **Verificar propiedades** de programas de forma matemática.

Ejemplo: En un TAD `Stack` (stack), un axioma podría ser:

> Si apilamos un elemento `x` y luego desapilamos, el resultado es el mismo estado inicial.

Formalmente:

```java
pop(push(stack, x)) = stack
```

---

## Importancia de los axiomas en software

- **Claridad**: Establecen de manera explícita las reglas fundamentales.
- **Corrección**: Permiten verificar que las implementaciones respetan las propiedades.
- **Mantenibilidad**: Facilitan entender cómo debe comportarse un módulo sin revisar todo su código.
- **Estandarización**: Ayudan a que diferentes implementaciones de un mismo TAD sean equivalentes.

---

## Ejemplo en Java: TAD Stack con axiomas

### Definición de axiomas para `Stack`

Para una pila de elementos, se pueden establecer los siguientes axiomas:

1. **Pila vacía**:

   ```java
   isEmpty(emptyStack) = true
   ```

2. **Apilar y desapilar**:

   ```java
   pop(push(p, x)) = p
   ```

3. **Ver el tope después de apilar**:

   ```java
   top(push(p, x)) = x
   ```

4. **No está vacía después de apilar**:

   ```java
   isEmpty(push(p, x)) = false
   ```

---

### Implementación en Java

```java
import java.util.ArrayList;
import java.util.List;

public class Stack<T> {
  private List<T> elements = new ArrayList<>();

  public boolean isEmpty() {
    return elements.isEmpty();
  }

  public void push(T element) {
    elements.add(element);
  }

  public T pop() {
    if (isEmpty()) {
      throw new IllegalStateException("Cannot unstack from an empty stack");
    }
    return elements.remove(elements.size() - 1);
  }

  public T top() {
    if (isEmpty()) {
      throw new IllegalStateException("The stack is empty");
    }
    return elements.get(elements.size() - 1);
  }

  // Verificación de axiomas
  public static <T> void verifyAxioms() {
    Stack<T> stack = new Stack<>();

    // Axioma 1
    assert stack.isEmpty() : "Axiom 1 violated: empty stack must be isEmpty() == true";

    // Axioma 2 y 3
    stack.push((T) "A");
    assert stack.top().equals("A") : "Axiom 3 violated: incorrect summit";
    stack.pop();
    assert stack.isEmpty() : "Axiom 2 violated: popping after stacking must leave the stack empty";
  }
}
```

---

## Diferencia entre axiomas, precondiciones, postcondiciones e invariantes

| Concepto          | Momento de verificación                | Naturaleza                          |
| ----------------- | -------------------------------------- | ----------------------------------- |
| **Axioma**        | Siempre válido por definición          | Regla fundamental del TAD o sistema |
| **Precondición**  | Antes de ejecutar un método            | Condición necesaria de entrada      |
| **Postcondición** | Después de ejecutar un método          | Condición garantizada de salida     |
| **Invariante**    | Antes y después de cualquier operación | Estado interno consistente          |

---

## Axiomas y Diseño por Contrato

En el **Diseño por Contrato (DbC)**, los axiomas forman parte de las **especificaciones formales**:

- Describen **propiedades esenciales** que cualquier implementación debe respetar.
- Son independientes del lenguaje de programación.
- Ayudan a garantizar **interoperabilidad** entre diferentes implementaciones.

---

## Ejemplo de axiomas en otro tad: Lista

Axiomas posibles para una lista:

1. `length(emptyList) = 0`
2. `length(add(list, x)) = length(list) + 1`
3. `obtener(add(list, x), length(list)) = x`

Esto permite:

- Implementar listas de forma eficiente.
- Comprobar su validez sin ver su código interno.

---

## Ventajas de usar axiomas en programación

- **Formalizan el comportamiento esperado** sin depender de una implementación específica.
- **Facilitan el testing automático** de propiedades esenciales.
- **Previenen errores de diseño** al tener reglas claras.
- **Mejoran la comunicación** entre programadores.

---

## Conclusión

Los **axiomas** son principios fundamentales que definen el comportamiento esencial de un sistema, un módulo o un tipo de dato.

En Java, aunque no existe un mecanismo explícito para declararlos, se pueden representar mediante **métodos de verificación** y **aserciones** que comprueben las propiedades definidas.

Definir axiomas antes de implementar un TAD o clase es clave para lograr **coherencia, robustez y mantenibilidad** en el software.
