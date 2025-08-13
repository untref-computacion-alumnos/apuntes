# Errores comunes con punteros en C

En C, los punteros son una herramienta poderosa que permite **acceder y manipular memoria directamente**, pero también son una fuente frecuente de errores si no se usan correctamente.

A continuación se presentan ejemplos de errores comunes y su corrección.

---

## Declaración de múltiples punteros en la misma línea

### Error

```c
int main() {
  int* p1, p2;
  int n = 30;
  p1 = &n;
  p2 = &n; // Error: 'p2' no es un puntero, es un entero.
  return 0
}
```

### Corrección

```c
int main() {
  int *p1, *p1;
  typedef int* Pint;
  Pint p1, p2;
  return 0
}
```

> Recordar: El operador `*` sólo se aplica a la variable que declara el puntero

---

## Uso de punteros no inicializados

### Error

```c
int main() {
  int* p1;
  int n = *p1; // Error: 'p1' apunta a memoria desconocida
  printf("%d", n);
  return 0
}
```

### Corrección

```c
int main() {
  int* p1;
  int m = 10;
  p1 = &m;
  int n = *p1;
  printf("%d", n);
  return 0
}
```

---

## Asignar un puntero a una variable no inicializada

### Error

```c
int main() {
  int* p1;
  int m;
  p1 = &m;
  int n = *p1; // Error: 'm' no tiene un valor definido.
  printf("%d", n);
  return 0
}
```

### Corrección

```c
int main() {
  int* p1;
  int m = 0;
  p1 = &m;
  int n = *p1;
  printf("%d", n);
  return 0
}
```

---

## Asignar valores directamente a un puntero

### Error

```c
int main() {
  int* p1;
  int m = 100;
  p1 = m; // Error: 'p1' debe apuntar a una dirección, no a un valor.
  return 0;
}
```

### Corrección

```c
int main() {
  int* p1;
  int m = 100;
  p1 = &m;
  return 0;
}
```

---

## Sintaxis incorrecta para incrementar el valor apuntado

### Error

```c
int main() {
  int* p1;
  int m = 100;
  p1 = &m;
  *p1++; // Error: Incrementa el puntero, no el valor.
  printf("%d\n", *p1);
  printf("%d\n", m);
  return 0;
}
```

### Corrección

```c
int main() {
  int* p1;
  int m = 100;
  p1 = &m;
  (*p1)++;
  printf("%d\n", *p1);
  printf("%d\n", m);
  return 0;
}
```

> Los paréntesis aseguran que se incremente el **valor apuntado**, no la dirección.

---

## Intentar liberar memoria del stack

### Error

```c
int main() {
  int* p1;
  int m = 100;
  p1 = &m;
  free(p1); // Error: No se puede usar 'free()' sobre memoria del stack.
  return 0;
}
```

---

## Usar un puntero después de liberarlo

### Error

```c
int main() {
  int* p1;
  p1 = malloc(sizeof(int));
  *p1 = 99;
  free(p1);
  *p1 = 100; // Error: Acceso a memoria ya liberada.
  printf("%d", *p1);
  return 0;
}
```

### Corrección

```c
int main() {
  int* p1;
  p1 = malloc(sizeof(int));
  *p1 = 99;
  free(p1);
  p1 = NULL;
  p1 = malloc(sizeof(int));
  *p1 = 100;
  printf("%d", *p1);
  return 0;
}
```

---

## Doble `free()`

### Error

```c
int main() {
  int* p1;
  p1 = malloc(sizeof(int));
  *p1 = 100;
  free(p1);
  free(p1); // Error: Doble liberación.
  return 0;
}
```

### Corrección

```c
int main() {
  int* p1;
  p1 = malloc(sizeof(int));
  *p1 = 100;
  free(p1);
  p1 = NULL;
  free(p1);
  return 0;
}
```

---

## No usar `sizeof()` correcto en `malloc`

### Error

```c
int main() {
  int* p1;
  p1 = malloc(2); // Error: 2 bytes insuficientes para un int.
  int a = 32800;
  *p1 = a;
  printf("%d", *p1);
  return 0;
}
```

### Corrección

```c
int main() {
  int* p1;
  p1 = malloc(sizeof(int));
  int a = 32800;
  *p1 = a;
  printf("%d", *p1);
  return 0;
}
```

---

## Usar `sizeof()` sobre un puntero para conocer el tamaño de un array

### Error

```c
int main() {
  const char arr[] = "hola";
  const char *p = arr;
  printf("array: %lu\n", sizeof(arr));
  printf("pointer: %lu\n", sizeof(*p));
  return 0;
}
```

> Para conocer el tamaño de un array, usar `sizeof(array) / sizeof(array[0])`.
> `sizeof(pointer)` devuelve el tamaño del puntero, no del array apuntado.

---

## Crear basura con punteros y memoria dinámica

### Error

```c
int main() {
  int *p = malloc(sizeof(int));
  *p = 5;
  p = malloc(sizeof(int)); // Error: Se pierde referencia al bloque anterior (memory leak).
  return 0;
}
```

### Corrección

```c
int main() {
  int *p = malloc(sizeof(int));
  *p = 5;
  free(p);
  p = malloc(sizeof(int));
  return 0;
}
```

---

## Buenas prácticas al utilizar punteros

- Inicializar siempre punteros antes de usarlos.
- Evitar acceder a variables no inicializadas.
- Usar `sizeof()` correctamente al reservar memoria dinámica.
- Liberar memoria con `free()` y establecer el puntero a `NULL`.
- Evitar doble `free()` o acceder a memoria ya liberada.
- Usar `typedef` para simplificar la declaración de punteros si es necesario.
