# Funciones, `struct` y `typedef`

En C, los **funciones**, **estructuras (`struct`)** y **tipos alias (`typedef`)** son herramientas fundamentales para organizar y reutilizar código, permitiendo escribir programas más claros y mantenibles.

---

## Funciones

Una función es un bloque de código que realiza una tarea específica y puede devolver un valor.

```c
#include <stdio.h>

// Definición de la función.
int addition(int a, int b) {
  return a + b;
}

int main() {
  int resultado = addition(1, 2);

  printf("Resultado: %d\n", resultado);

  return 0;
}
```

### Declaración antes de usar

En C, la función **debe estar declarada o definida** antes de usarla en otra función:

```c
#include <stdio.h>

// Declaración (prototipo) de la función.
int addition(int a, int b);

int main() {
  int resultado = addition(1, 2);

  printf("Resultado: %d\n", resultado);

  return 0;
}

// Definición de la función.
int addition(int a, int b) {
  return a + b;
}
```

### Uso de archivos de headers

Se pueden separar las funciones en archivos de cabecera (`.h`) y código (`.c`):

```c
// file: functions.h
int addition(int a, int b) {
  return a + b;
}
```

```c
// file: main.c
#include <stdio.h>
#include "functions.h"

int main() {
  int resultado = addition(1, 2);

  printf("Resultado: %d\n", resultado);

  return 0;
}
```

- `#include <stdio.h>`: busca la librería preinstalada del compilador.
- `#include "functions.h"`: busca en el directorio del proyecto. También se puede indicar otra ruta:

  ```c
  #include "ruta/al/directorio/functions.h"
  ```

---

## `struct`

Un `struct` permite agrupar **variables de distintos tipos** en una sola unidad.

```c
struct Persona {
  int edad;
  float altura;
  char nombre[100];
};

int main() {
  struct Persona p1;

  p1.edad = 25;
  p1.altura = 1.75;

  strcpy(p1.nombre, "Juan");
}
```

- Se accede a los campos con el operador `.`.
- Se pueden definir variables globales de tipo `struct`:

  ```c
  struct Persona personaGlobal;

  int main() {
    personaGlobal.edad = 30;
  }
  ```

- Si no se necesita instanciar más variables, se puede omitir el nombre del `struct`.

---

## `typedef`

`typedef` permite crear **alias para tipos existentes**, facilitando la legibilidad y portabilidad del código:

```c
typedef int entero;

int main() {
  entero x = 10;

  printf("%d\n", x);
}
```

### Definir booleanos con `typedef` y `enum`

```c
typedef enum { false, true } bool;

int main() {
  bool bandera = true;

  printf("%d\n", bandera); // imprime 1
}
```

- La primera posición del `enum` corresponde a 0, la siguiente a 1, y así sucesivamente.
- Alternativa explícita:

  ```c
  enum { false = 0, true = 1 };
  ```

---

## `typedef` + `struct`

Se puede combinar `typedef` con `struct` para **definir estructuras con un nombre simple**, evitando tener que escribir `struct` cada vez:

```c
typedef struct Persona {
  int edad;
  float altura;
  char nombre[100];
} Persona;

int main() {
  Persona p1;

  p1.edad = 25;

  strcpy(p1.nombre, "Ana");
}
```

- Ahora se puede declarar variables directamente como `Persona` en lugar de `struct Persona`.
- Mejora la legibilidad y facilita la reutilización de estructuras complejas.

---

## Buenas prácticas

- Siempre usar **prototipos de función** en headers si la función se define después de `main` o en otro archivo.
- Inicializar las estructuras antes de usarlas.
- Evitar usar `strcpy` sin verificar tamaños para prevenir desbordes de buffer (usar `strncpy` en su lugar).
- Nombrar los `typedef` con nombres claros y descriptivos.

---

## Resumen gráfico

```md
Funciones -> Bloques de código reutilizables
struct -> Agrupa variables relacionadas
typedef -> Alias de tipos para mejorar legibilidad
typedef+struct -> Alias para estructuras complejas
```
