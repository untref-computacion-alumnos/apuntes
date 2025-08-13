# Introducción al lenguaje C

El lenguaje [**C**](<https://en.wikipedia.org/wiki/C_(programming_language)>) es uno de los más influyentes en la historia de la programación.

Diseñado en los años 70 por [**Dennis Ritchie**](https://en.wikipedia.org/wiki/Dennis_Ritchie) en los laboratorios Bell, C sirvió como base para sistemas operativos como [**UNIX**](https://en.wikipedia.org/wiki/Unix) e influyó en lenguajes como C++, C#, Java, Go, etc.

Se caracteriza por su **eficiencia, portabilidad y cercanía al hardware**, lo que lo convierte en una herramienta clave tanto para sistemas embebidos como para el desarrollo de software de alto rendimiento.

## Algunas características de C

- **Compilado**: El código fuente se traduce a código máquina antes de ser ejecutado.
- **Bajo nivel** (al menos más bajo nivel que _Java_): Permite interactuar más directamente con el hardware.
- **Tipo estructurado**: Soporta agrupación de datos en estructuras (`struct`).
- **Tipado estático**: El tipo de cada variable se define en tiempo de compilación.
- **Acceso a memoria de bajo nivel** mediante el uso de punteros.
- **Tipos de datos agregados (`struct`)** que permiten que datos relacionados (como un empleado, que tiene un id, un nombre y un salario) se combinen y se manipulen como un todo (en una única variable `empleado`).

---

## C/C++ IDEs

Existen múltiples entornos de desarrollo que facilitan escribir, compilar y depurar código en C/C++.

Algunos ejemplos:

- [JetBrains CLion](https://www.jetbrains.com/clion/)
- [Code::Blocks](https://www.codeblocks.org/)
- [Eclipse CDT (C/C++ Development Tooling)](https://projects-eclipse-org.translate.goog/projects/tools.cdt?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=tc)
- [Netbeans for C/C++ Development](https://netbeans.apache.org/front/main/index.html)
- [CodeLite IDE](https://codelite.org/)
- [Atom Code Editor](https://atom-editor.cc/)
- [Sublime Text Editor](https://www.sublimetext.com/)
- [Geany](https://www.geany.org/)
- [Visual Studio](https://visualstudio.microsoft.com/es/) / [Visual Studio Code](https://code.visualstudio.com/)
- [Vim](https://www.vim.org/) / [NeoVim](https://neovim.io/)

---

## Hello World

El programa más básico en C es el clásico **¡Hello, World!**, que demuestra la estructura mínima de un programa.

```c
#include <stdio.h>

int main() {
  printf("¡Hello, World!\n");

  return 0;
}
```

---

## Pasos en la compilación de C

Cuando se compila un programa en C, el proceso pasa por varias fases:

### Preprocessor

Procesa las directivas como `#include` y `#define`. Luego genera un archivo intermedio con todo el código listo para compilar.

### Compiler

Traduce el código C a **código ensamblador** específico de la arquitectura.

### Assembler

Convierte el código ensamblador en **código máquina** (archivos `.o` u `.obj`).

### Linker

Une todos los archivos objeto y bibliotecas necesarias para generar el ejecutable final.

---

## Palabras reservadas

Estas son las palabras reservadas del lenguaje que tienen un significado especial y no pueden usarse como nombres de variables, funciones o identifiadores:

- `auto` — Especifica almacenamiento automático (por defecto para variables locales).
- `break` — Sale inmediatamente de un bucle `for`, `while` o `switch`.
- `case` — Define una rama en una estructura `switch`.
- `char` — Declara una variable de tipo carácter.
- `const` — Indica que una variable no puede ser modificada después de inicializarse.
- `continue` — Salta a la siguiente iteración del bucle.
- `default` — Rama por defecto en un `switch` cuando no hay coincidencias.
- `do` — Usado en el bucle `do-while` que ejecuta primero y evalúa después.
- `double` — Declara una variable de punto flotante de doble precisión.
- `else` — Rama que se ejecuta si la condición de un `if` es falsa.
- `enum` — Declara un conjunto de constantes enteras con nombre.
- `extern` — Declara una variable o función definida en otro archivo.
- `float` — Declara una variable de punto flotante simple precisión.
- `for` — Inicia un bucle con contador.
- `goto` — Salta a una etiqueta específica (no recomendado por legibilidad).
- `if` — Evalúa una condición y ejecuta un bloque si es verdadera.
- `int` — Declara una variable de tipo entero.
- `long` — Declara un entero de mayor tamaño que `int`.
- `register` — Sugiere almacenar la variable en un registro de CPU (poco usado hoy).
- `return` — Sale de una función y opcionalmente devuelve un valor.
- `short` — Declara un entero de menor tamaño que `int`.
- `signed` — Especifica que un tipo numérico puede tener valores negativos y positivos.
- `sizeof` — Devuelve el tamaño en bytes de una variable o tipo.
- `static` — Mantiene el valor de una variable local entre llamadas o limita visibilidad en variables globales.
- `struct` — Declara una estructura para agrupar datos relacionados.
- `switch` — Permite múltiples caminos de ejecución basados en el valor de una variable.
- `typedef` — Crea un alias para un tipo de dato.
- `union` — Agrupa variables que comparten la misma zona de memoria.
- `unsigned` — Especifica que un tipo numérico solo puede contener valores positivos.
- `void` — Indica que una función no devuelve valor o que un puntero no tiene tipo.
- `volatile` — Indica que el valor de la variable puede cambiar fuera del control del programa (por hardware o interrupciones).
- `while` — Bucle que se repite mientras una condición sea verdadera.

---

## Tipos de datos

| type           | storage size | value range                                  | presition         |
| -------------- | ------------ | -------------------------------------------- | ----------------- |
| char           | 1 byte       | -128 to 127 or 0 to 255                      | -                 |
| unsigned char  | 1 byte       | 0 to 255                                     | -                 |
| signed char    | 1 byte       | -128 to 127                                  | -                 |
| int            | 2 or 4 bytes | -32768 to 32767 or -2147483648 to 2147483647 | -                 |
| unsigned int   | 2 or 4 bytes | 0 to 65535 or 0 to 4294967295                | -                 |
| short          | 2 bytes      | -32768 to 32767                              | -                 |
| unsigned short | 2 bytes      | 0 to 65535                                   | -                 |
| long           | 4 bytes      | -2147483648 to 2147483647                    | -                 |
| unsigned long  | 4 bytes      | 0 to 4294967295                              | -                 |
| float          | 4 bytes      | 1.2E-38 to 3.4E+38                           | 6 decimal places  |
| double         | 8 bytes      | 2.3E-308 to 1.7E+308                         | 15 decimal places |
| long double    | 10 bytes     | 3.4E-4932 to 1.1E+4932                       | 19 decimal places |

---

## Formatos del `printf`

- `%c`: Carácter.
- `%d`: Número decimal.
- `%i`: Número entero.
- `%e`: Número de coma flotante exponencial.
- `%f`: Número de coma flotante.
- `%o`: Número octadecimal.
- `%s`: Cadena de caracteres.
- `%u`: Número decimal unsigned.
- `%x`: Número hexadecimal.

---

## Caracteres especiales del `printf`

- `\n`: Nueva línea, o salto de línea.
- `\r`: Retorno de carro.
- `\t`: Tab.
- `\v`: Tab vertical.
- `\a`: Alerta sonora.
- `\b`: Retroceso.
- `\f`: Form feed.
- `\\`: Barra invertida.

---

## Entrada y salida

```c
#include <stdio.h>

int main() {
  char name[100];

  printf("Enter your name: ");
  scanf("%s", name);

  printf("Your name is: %s", name);

  return 0;
}
```

> **Nota**: `scanf("%s", ...)` detiene la lectura al primer espacio.
> Para leer una línea completa con espacios se recomienda usar `fgets()`.
