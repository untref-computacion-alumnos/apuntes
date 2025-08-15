# Estructuras de control de flujo

Las **estructuras de control de flujo** son mecanismos que permiten **alterar el orden** en que se ejecutan las instrucciones de un programa.

Gracias a estas, es posible tomar decisiones, repetir bloques de código o saltar a diferentes partes del programa según ciertas condiciones.

Las estructuras de control de flujo se clasifican en tres grandes grupos:

1. **Secuenciales**.
2. **Selectivas o condicionales**.
3. **Repetitivas o iterativas**.

---

## Estructuras de control secuenciales

### Concepto

La ejecución secuencial es el **flujo natural** de un programa: Las instrucciones se ejecutan una tras otra en el orden en que aparecen.

### Ejemplo en Java

```java
public class Secuential {
  public static void main(String[] args) {
    int a = 5;
    int b = 10;
    int addition = a + b;

    System.out.println("The addition is: " + addition);
    System.out.println("End of program");
  }
}
```

Acá las instrucciones se ejecutan de arriba hacia abajo, sin saltos ni repeticiones.

---

## Estructuras de control selectivas o condicionales

Permiten **tomar decisiones** y ejecutar distintos bloques de código dependiendo de si se cumple o no una condición.

### Tipos

#### `if`

Ejecuta un bloque de código sí y solo si la condición es verdadera.

```java
if (condición) {
  // Código a ejecutar si la condición es verdadera.
}
```

**Ejemplo**:

```java
int edad = 20;

if (edad >= 18) {
  System.out.println("Is of legal age");
}

// Salida: Is of legal age
```

#### `if-else`

Permite ejecutar un bloque sí y solo si la condición es verdadera, y otro bloque si es falsa.

```java
if (condición) {
  // Código a ejecutar si la condición es verdadera.
} else {
  // Código a ejecutar si la condición es falsa.
}
```

**Ejemplo**:

```java
int edad = 16;

if (edad >= 18) {
  System.out.println("Is of legal age");
} else {
  System.out.println("Is a minor");
}

// Salida: Is a minor
```

#### `if-else if-else`

Permite evaluar múltiples condiciones en forma de cascada.

```java
if (condición 1) {
  // Código a ejecutar si esta primera condición es verdadera.
} else if (condición 2) {
  // Código a ejecutar si esta segunda condición es verdadera.
} else {
  // Código a ejecutar si las condiciones anteriores son falsas.
}
```

**Ejemplo**:

```java
int grade = 7;

if (grade >= 9) {
  System.out.println("Excelent");
} else if (grade >= 4) {
  System.out.println("Approved");
} else {
  System.out.println("Disapproved")
}
```

#### `switch`

Selecciona una opción entre múltiples posibles valores.

```java
switch (variable) {
  case valor1:
    // Código a ejecutar.
    break;
  case valor2;
    // Código a ejecutar.
    break;
  default:
    // Código por defecto.
}
```

**Ejemplo**:

```java
int dia = 3;
switch (dia) {
  case 1:
    System.out.println("Monday");
    break;
  case 2:
    System.out.println("Tuesday");
    break;
  case 3:
    System.out.println("Wednesday");
    break;
  default:
    System.out.println("Another day");
}
```

---

## Estructuras de control repetitivas o iterativas (bucles)

Permiten **repetir** un bloque de instrucciones mientras se cumpla una condición o hasta que se cumpla.

### Tipos

#### `while`

Repite el bloque **mientras** (_while_ se traduce como _mientras_) la condición evaluada sea verdadera.

```java
while (condición) {
  // Código a ejecutar repetidamente mientras se cumpla la condición.
}
```

**Ejemplo**:

```java
int i = 1;
while (i <= 5) {
  System.out.println(i);
  i++;
}
```

#### `do-while`

Similar al bloque `while`, pero garantiza que el bloque se ejecute **por lo menos una vez**.

```java
do {
  // Código a ejecutar aunque sea una vez, y repetidamente mientras se cumpla la condición.
} while (condición);
```

**Ejemplo**:

```java
int i = 1;
do {
  System.out.println(i);
  i++;
} while (i <= 5);
```

#### `for`

Ideal cuando se conoce el número de repeticiones. _for_ se traduce como _por_, y se puede pensar como _por cada vez_.

Se puede utilizar para trabajar tanto sobre un índice como sobre un valor del índice dado.

```java
for (inicialización; condición; actualización) {
  // Código a repetir mientras la condición interna se cumpla.
}
```

**Ejemplo**:

```java
for (int i = 1; i <= 5; i++) {
  System.out.println(i);
}
```

#### `for-each`

Recorre colecciones o arreglos de forma simplificada.

_for each_ se puede traducir como _por cada_.

Se utiliza para los valores de los elementos, no sobre los índices.

```java
for (Tipo elemento : colección) {
  // Código a ejecutar.
}
```

**Ejemplo**:

```java
String[] names = {"Ana", "Luis", "María"};
for (String name : names) {
  System.out.println(name);
}
```

---

## Sentencias de control de bucles

- `break`: Interrumple la ejecución del bucle actual.
- `continue`: Salta a la siguiente iteración.
- `return`: Finaliza el método actual (puede salir de un bucle si se llama dentro de este).

**Ejemplo con `break` y `continue`**

```java
for (int i = 1; i <= 10; i++) {
  if (i == 5) {
    continue; // Salto el número 5.
  }
  if (i == 8) {
    break;    // Termino el bucle al llegar al número 8.
  }
  System.out.println(i);
}
```

---

## Buenas prácticas con estructuras de control

- Evitar condiciones excesivamente complejas; dividirlas en variables booleanas con nombres descriptivos.
- Usar `switch` cuando se evalúa con una sola variable contra muchos valores posibles.
- Evitar bucles infinitos (`while(true)`) salvo que estén bien controlados por una condición clara de salida.
- Usar `for-each` para recorrer colecciones cuando no es necesario el índice.
- Documentar casos especiales o límites dentro de condicionales.

---

## Diagrama de flujo general

```md
Inicio
↓
Instrucción 1
↓
[Condición?] -> No -> Instrucción siguiente
↓
Si
↓
Bloque de instrucciones
↓
Reevaluar condición / Siguiente instrucción
↓
Fin
```

---

## Conclusión

Las **estructuras de control de flujo** son esenciales para dar **lógica y flexibilidad** a un programa.

En Java, así como en la programación en general, el uso correcto de condicionales y bucles permite crear aplicaciones más eficientes, claras y fáciles de mantener.
