# Subrutinas

## Definición General

Una **subrutina** es un **bloque de código independiente y reutilizable** que realiza una tarea específica dentro de un programa.

También se las conoce como **procedimientos, funciones o métodos**, dependiendo del lenguaje de programación y del contexto.

La idea central es **evitar la repetición de código**, mejorar la **modularidad**, la **legibilidad** y facilitar el **mantenimiento** de los programas.

---

## Características Principales

- **Nombre identificador**: Cada subrutina debe tener un nombre único para poder ser invocada.
- **Entrada (parámetros)**: Pueden recibir datos externos que se utilizan dentro de la subrutina.
- **Salida (retorno de valores)**: Pueden devolver un resultado o no, según el tipo de subrutina.
- **Reutilización**: Una vez definida, puede ser invocada múltiples veces en diferentes partes del programa.
- **Encapsulamiento**: Permiten separar la lógica en bloques más comprensibles y fáciles de depurar.

---

## Tipos de Subrutinas

### Procedimientos

- Ejecutan un conjunto de instrucciones.
- No devuelven un valor explícito.
- Ejemplo en **Pascal**:

  ```pascal
  procedure Saludar(nombre: string);
  begin
    writeln('Hola ', nombre);
  end;
  ```

### Funciones

- Ejecutan instrucciones y **devuelven un valor**.
- Ejemplo en **Python**:

  ```python
  def sumar(a, b):
    return a + b
  resultado = sumar(5, 3)  # resultado = 8
  ```

### Métodos

- Son **subrutinas asociadas a objetos** en programación orientada a objetos (POO).
- Acceden a los atributos y comportamientos de la clase.
- Ejemplo en **Java**:

  ```java
  class Calculadora {
    int sumar(int a, int b) {
      return a + b;
    }
  }
  ```

---

## Ventajas del Uso de Subrutinas

1. **Reutilización**: Evita repetir el mismo código en varias partes del programa.
2. **Legibilidad**: El código se organiza en bloques con nombres significativos.
3. **Mantenimiento**: Cambios o correcciones se hacen en una sola parte.
4. **Colaboración**: Facilita el trabajo en equipo dividiendo las responsabilidades.
5. **Abstracción**: Permite pensar en el “qué hace” la subrutina y no en el “cómo lo hace”.

---

## Parámetros en Subrutinas

### Parámetros por valor

- Se pasa una **copia** del valor.
- Cambios dentro de la subrutina **no afectan** a la variable original.
- Ejemplo en **C**:

  ```c
  void duplicar(int x) {
    x = x * 2;
  }
  ```

### Parámetros por referencia

- Se pasa la **dirección de memoria** (referencia).
- Cambios dentro de la subrutina **afectan** a la variable original.
- Ejemplo en **C++**:

  ```cpp
  void duplicar(int &x) {
    x = x * 2;
  }
  ```

### Parámetros con valores por defecto

- Se pueden establecer valores predeterminados.
- Ejemplo en **Python**:

  ```python
  def saludar(nombre = "Invitado"):
    print("Hola", nombre)

  saludar()       # Hola Invitado
  saludar("Ana")  # Hola Ana
  ```

---

## Ámbito de Variables en Subrutinas

- **Variables locales**: Declaradas dentro de la subrutina; existen solo mientras se ejecuta.
- **Variables globales**: Declaradas fuera de cualquier subrutina; accesibles desde todo el programa.
- **Ámbito léxico**: El alcance de las variables depende del lugar donde fueron definidas en el código.

Ejemplo en **JavaScript**:

```javascript
let global = "Soy global";

function ejemplo() {
  let local = "Soy local";
  console.log(global); // Accede
  console.log(local); // Accede
}

console.log(global); // Accede
console.log(local); // Error: no definida
```

---

## Buenas Prácticas

1. Usar **nombres significativos** que describan lo que hace la subrutina.
2. Mantenerlas **cortas y específicas** (una sola responsabilidad).
3. Evitar **efectos secundarios** inesperados.
4. Documentar los **parámetros** y el **valor de retorno**.
5. Reutilizar subrutinas en lugar de copiar código.
6. No abusar de variables globales.

---

## Conclusión

Las **subrutinas** son un pilar fundamental de la programación estructurada y de la programación en general.

Su uso correcto **mejora la claridad, eficiencia y mantenibilidad** de los programas, además de servir como base para conceptos más avanzados como la **programación orientada a objetos**, la **recursividad** y el **diseño modular**.
