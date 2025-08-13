# Punteros y referencias

Los **punteros** y **referencias** son herramientas fundamentales para trabajar directamente con la memoria. Permiten acceder, modificar y gestionar datos a través de sus direcciones físicas, otorgando un control preciso sobre cómo se almacenan y manipulan.

---

## ¿Qué es un puntero?

Un **puntero** es una variable cuyo valor no es un dato en sí mismo, sino una **dirección de memoria** donde se encuentra almacenado ese dato.

- El contenido del puntero es una dirección.
- El operador `*` en _C_ y _C++_ (operador de desreferencia) permite acceder al valor almacenado en esa dirección.
- El operador `&` permite obtener la dirección de memoria de una variable.

Ejemplo básico en C:

```c
#include <stdio.h>

int main() {
  int x = 42;
  int *ptr = &x;  // ptr guarda la dirección de x.

  printf("Valor de x: %d\n", x);
  printf("Dirección de x: %p\n", (void*)&x);
  printf("Valor almacenado en ptr (dirección): %d\n", (void*)ptr);
  printf("Valor apuntado por ptr: %d\n", *ptr);

  return 0;
}
```

---

## ¿Qué es una referencia?

En _C++_ (y otros lenguajes), una **referencia** es un alias para una variable existente.

No almacena una dirección como un puntero, sino que actúa como un \*\* para el mismo valor.

- Una vez inicializada, no puede cambiar para referenciar otro objeto.
- El acceso a una referencia es transparente, como si fuera la variable original.
- En C, no existen referencias como tipo de dato, pero se simulan pasando punteros a funciones.

Ejemplo en C++:

```cpp
#include <iostream>

using namespace std;

int main() {
  int x = 42;
  int &ref = x;                           // ref es una referencia a x.

  cout << "x: " << x << endl;
  cout << "ref: " << ref << endl;

  ref = 100;                              // Modifica x.

  cout << "x modificado: " << x << endl;

  return 0;
}
```

---

## Diferencias clave entre punteros y referencias

| Característica             | Puntero           | Referencia          |
| -------------------------- | ----------------- | ------------------- |
| Puede ser nulo             | Sí                | No                  |
| Puede cambiar a qué apunta | Sí                | No                  |
| Sintaxis de acceso         | `*ptr`            | Directo             |
| Requiere inicialización    | No necesariamente | Sí obligatoriamente |

---

## Punteros y memoria

Los punteros permiten recorrer estructuras en memoria y manipular datos dinámicamente.

Por ejemplo, acceder a elementos de un arreglo usando [aritmética de punteros](https://www.ibm.com/docs/es/i/7.6.0?topic=pointers-pointer-arithmetic):

```c
#include <stdio.h>

int main() {
  int arr[] = {10, 20, 30, 40};
  int *p = arr; // arr es equivalente a &arr[0].

  for (int i = 0; i < 4; i++) {
    printf("Elemento %d: %d\n", i, *(p + i));
  }

  return 0;
}
```

---

## Punteros a punteros

Un **puntero a puntero** es una variable que almacena la dirección de otro puntero.

Ejemplo:

```c
#include <stdio.h>

int main() {
  int x = 5;
  int *p = &x;                // Puntero a entero.
  int **pp = &p;              // Puntero a puntero.

  printf("x: %d\n", x);
  printf("*p: %d\n", *p);
  printf("**pp: %d\n", **pp);

  return 0;
}
```

---

## Punteros y funciones

En C, los punteros permiten **pasar variables por referencia** a funciones, logrando que los cambios persistan fuera del alcance de la función.

```c
#include <stdio.h>

void duplicate(int *num) {
  *num = *num * 2;
}

int main() {
  int value = 10;

  duplicate(&value);

  printf("Value duplicated: %d\n", value);

  return 0;
}
```

---

## Punteros y memoria dinámica

La gestión manual de memoria se realiza con punteros y funciones como `malloc` y `free`.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  int *arr = malloc(5 * sizeof(int)); // Reserva memoria.

  if (!arr) {
    return 1;
  }

  for (int i = 0; i < 5; i++) {
    arr[i] = i + 1;
  }

  for (int i = 0; i < 5; i++) {
    printf("%d ", arr[i]);
  }

  free(arr);                          // Libera memoria.

  return 0;
}
```

---

## Riesgos y buenas prácticas

### Riesgos

- **Punteros colgantes**: Apuntar a memoria ya liberada.
- **Acceso inválido**: Usar direcciones no asignadas.
- **Fugas de memoria**: No liberar memoria dinámica.
- **Desbordamientos**: Acceder más allá de los límites asignados.

### Buenas prácticas

- Inicializar punteros en `NULL` si no apuntan a nada.
- Liberar memoria dinámica cuando ya no se use.
- Evitar aritmética de punteros innecesaria.
- Usar herramientas como `valgrind` para detectar problemas.

---

## Resumen

- Un **puntero** almacena direcciones de memoria y permite manipular datos de forma indirecta.
- Una **referencia** es un alias a una variable existente, sin necesidad de desreferencia explícita.
- En programación de bajo nivel, los punteros son esenciales para el manejo eficiente de memoria, estructuras dinámicas y comunicación entre funciones.

El uso correcto de los punteros y las referencias es clave para escribir código optimizado y seguro en lenguajes de bajo nivel.
