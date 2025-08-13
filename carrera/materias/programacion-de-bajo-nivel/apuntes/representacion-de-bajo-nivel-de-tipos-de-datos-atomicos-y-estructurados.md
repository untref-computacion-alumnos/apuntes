# Representación de bajo nivel de tipos de datos atómicos y estructurados

Comprender cómo se representan los datos en memoria es esencial para escribir código eficiente y seguro.

Los **tipos de datos** se dividen generalmente en:

- **Atómicos**: Aquellis que representan un único valor indivisible (enteros, caracteres, numéricos de coma flotante, booleanos, etc).
- **Estructurados**: Aquellos que agrupan varios valores, que pueden ser del mismo tipo o de tipos distintos (arreglos, estructuras, uniones, etc).

La forma en que se representan **físicamente** en memoria depende del tamaño en _bytes_, la arquitectura del procesador, el orden de almacenamiento (endianess) y las reglas de alineación.

---

## Representación de tipos atómicos

### Enteros (`int`, `short`, `long`, etc)

- Se almacenan como secuencias de bits que representan valores numéricos.
- Los números con signo suelen utilizar [**complemento a dos**](https://en.wikipedia.org/wiki/Two%27s_complement) para representar positivos y negativos.
- El tamaño varía según la arquitectura (32 bits, 64 bits, etc.).

Ejemplo en C:

```c
#include <stdio.h>
#include <stdint.h>

int main() {
  int32_t a = -42;

  printf("Valor: %d\n", a);
  printf("Tamaño en bytes: %zu\n", sizeof(a));

  return 0;
}
```

### Caracteres (`char`)

- Ocupan normalmente **1 byte** (_8 bits_).
- Representan un código numérico (ASCII, UTF-8, etc.).
- En C, un `char` también puede interpretarse como un número entero pequeño.

---

### Números en coma flotante (`float`, `double`)

- Se representan según el estándar [**IEE 754**](https://en.wikipedia.org/wiki/IEEE_754).
  - **Signo**: 1 bit.
  - **Exponente**: Campo que determina la escala.
  - **Mantisa**: Representa la parte significativa.
- Los valores son aproximados debido a la limitación en la cantidad de bits.

Ejemplo de tamaño:

| Tipo        | Tamaño típico                         |
| ----------- | ------------------------------------- |
| float       | 4 bytes                               |
| double      | 8 bytes                               |
| long double | 8, 12 o 16 bytes según implementación |

---

### Booleanos (`bool`)

- Normalmente ocupan **1 byte** en _C/C++_ (aunque solo usan 1 bit para representar `true` o `false`).
- En bajo nivel, suelen representarse como `0` (falso) o `1` (verdadero).

---

## Representación de tipos estructurados

### Arreglos

- Secuencia contigua de elementos del mismo tipo.
- Cada elemento ocupa un tamaño fijo.
- La dirección del primer elemento (`&arr[0]`) es también la dirección del arreglo.

Ejemplo:

```c
int arr[4] = {10, 20, 30, 40};
```

En memoria (4 bytes por entero, little-endian):

| Dirección | Contenido (hex) |
| --------- | --------------- |
| 0x1000    | 0A 00 00 00     |
| 0x1004    | 14 00 00 00     |
| 0x1008    | 1E 00 00 00     |
| 0x100C    | 28 00 00 00     |

---

### Estructuras (`struct`)

- Agrupan variables de distintos tipos.
- Pueden tener **relleno (padding)** para cumplir requisitos de alineación.
- El orden de los campos y el alineamiento afectan el tamaño total.

Ejemplo:

```c
#include <stdio.h>

struct Example {
  char  c;  // 1 byte
  int   x;  // 4 bytes (pero alineado)
};

int main() {
  printf("Tamaño de struct: %zu\n", sizeof(struct Example));

  return 0;
}
```

En una arquitectura de 32 bits, podría ocupar **8 bytes** debido al padding entre `char` e `int`.

---

### Uniones (`union`)

- Todos los campos comparten la misma dirección de inicio.
- El tamaño total es el del miembro más grande.
- Útiles para interpretar el mismo bloque de memoria de distintas formas.

Ejemplo:

```c
#include <stdio.h>

union Data {
  int   integer;
  float real;
  char  bytes[4];
};

int main() {
  union Data d;

  d.integer = 0x41424344;

  printf("Bytes: %c %c %c %c\n", d.bytes[0], d.bytes[1], d.bytes[2], d.bytes[3]);

  return 0;
}
```

---

## Endianess

El **endianess** determina el orden en que se almacenan los bytes en memoria:

- **Little-endian**: El byte menos significativo se guarda primero.
- **Big-endian**: El byte más significativo se guarda primero.

Ejemplo con `0x12345678` (4 bytes):

| Dirección | Little-endian | Big-endian |
| --------- | ------------- | ---------- |
| 0x1000    | 78            | 12         |
| 0x1001    | 56            | 34         |
| 0x1002    | 34            | 56         |
| 0x1003    | 12            | 78         |

---

## Alineación de datos

- El procesador accede más rápido a datos alineados en direcciones múltiplos de su tamaño.
- Por ejemplo, un entero de 4 bytes suele almacenarse en una dirección múltiplo de 4.
- El compilador puede insertar **padding** para mantener la alineación.

---

## Resumen

- Los **tipos atómicos** ocupan tamaños fijos y se representan directamente como secuencias de bits interpretadas según su tipo.
- Los **tipos estructurados** ocupan bloques de memoria más complejos, con posibles ajustes de alineación y relleno.
- Comprender la representación fija permite:
  - Optimizar el uso de memoria.
  - Evitar errores al trabajar con punteros.
  - Interpretar correctamente datos binarios en bajo nivel.
