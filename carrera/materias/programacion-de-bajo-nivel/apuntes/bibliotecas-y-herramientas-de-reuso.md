# Bibliotecas y herramientas de reuso

El **reuso de código** permite aprovechar componentes ya desarrollados para no tener que escribir todo desde cero.

En el contexto de lenguajes de bajo nivel como **C**, este reuso se logra principalmente a través de **bibliotecas (libraries)** y diversas **herramientas** que facilitan su creación, distribución y mantenimiento.

---

## ¿Qué es una biblioteca?

Una **biblioteca** es un conjunto de funciones, procedimientos y/o definiciones ya compiladas, listas para ser utilizadas por otros programas.

Permiten encapsular lógica común (por ejemplo, funciones matemáticas, manejo de cadenas, acceso a hardware) en un solo lugar.

### Tipos de bibliotecas

#### **Bibliotecas estáticas** (`.a` en Linux, `.lib` en Windows)

- Se enlazan en tiempo de compilación.
- El código de la biblioteca se **copia** dentro del ejecutable final.
- No dependen de archivos externos en tiempo de ejecución.
- Aumentan el tamaño del ejecutable y requieren recompilación para actualizaciones.

#### **Bibliotecas dinámicas o compartidas** (`.so` en Linux, `.dll` en Windows)

- Se cargan en tiempo de ejecución.
- El ejecutable contiene solo referencias a la biblioteca.
- Menor tamaño del binario y posibilidad de actualizar la biblioteca sin recompilar el programa.
- Dependencia externa (si falta la biblioteca, el programa no funciona).

---

## Proceso de creación y uso de biblioteca en C

### Crear el código fuente

```c
// file: math.c

int add(int a, int b) {
  return a + b;
}
```

### Compilar en código objeto

```sh
gcc -c math.c -o math.o
```

### Crear la biblioteca estática

```sh
ar rcs libmath.a math.o
```

### Usar la biblioteca en otro programa

```c
// file: main.c

#include <stdio.h>

int add(int a, int b);

int main() {
  printf("Result: %d\n", add(5, 3));

  return 0;
}
```

Compilación:

```c
gcc main.c -L. -lmath -o app
```

_(El flag `-L` indica buscar bibliotecas en el directorio actual, y `-lmath` enlaza con `libmath.a`)_

---

## Herramientas para manejo de bibliotecas y reuso

### En entornos Unix/Linux

- **`gcc`**: Compilador de C/C++ que permite generar y enlazar bibliotecas.
- **`ar`**: Creador y manipulador de bibliotecas estáticas.
- **`ld`**: Enlazador que combina objetos y bibliotecas.
- **`make`**: Herramienta de automatización para compilar y enlazar proyectos grandes.
- **`pkg-config`**: Facilita encontrar bibliotecas y sus rutas de inclusión.
- **`ldd`**: Lista las dependencias dinámicas de un binario.

### En entornos Windows

- **Visual Studio** _(No Visual Studio Code)_: Incluye herramientas para generar `.lib` y `.dll`.
- **MinGW**: Implementa GCC y utilidades GNU en Windows.
- **Dependency Walker**: Muestra qué DLL necesita un programa.

---

## Buenas prácticas para el reuso de bibliotecas

- **Documentar la API**: Describir claramente las funciones, los parámetros y valores de retorno.
- **Versionado**: Mantener versiones claras para evitar incompatibilidades.
- **Separar interfaz e implementación**: Archivos `.h` (headers) para las declaraciones y `.c` para las definiciones.
- **Usar compilación condicional**: Uso de `#ifdef`/`#ifndef` para mantener compatibilidad multiplataforma.
- **Compilar con -fPIC**: En bibliotecas compartidas asegura código independiente de la posición.

---

## Reuso más allá de bibliotecas

Además de bibliotecas, existen otras herramientas para formatear el reuso:

- **Plantillas de proyecto**: Estructuras predefinidas para comenzar nuevos desarrollos.
- **Repositorios de código**: GitHub, GitLab, Bitbucket.
- **Paquetes y gestores**:
  - `apt`, `yum` en Linux para bibliotecas del sistema.
  - `vcpkg`, `conan` para C/C++ multiplataforma.
- **Macros y cabeceras reutilizables**: Funciones inline y macros para código repetitivo.

---

## Ventajas del reuso en bibliotecas

- **Ahorro de tiempo**: No reinventar cosas ya hechas.
- **Menos errores**: Uso de código probado y estable.
- **Mantenibilidad**: Actualizar la biblioteca sin tocar el resto del programa.
- **Optimización**: Compiladores y librerías ya optimizadas para el hardware.

---

## Desafíos y riesgos

- **Compatibilidad**: Cambios en la API pueden romper programas existentes.
- **Dependencias**: Bibliotecas dinámicas faltantes causan errores de ejecución.
- **Licencias**: Es necesario respetar licencias (GPL, MIT, Apache, etc.).
- **Sobrecarga de abstracción**: Usar demasiadas bibliotecas puede agregar complejidad innecesaria.

---

## Resumen

Las **bibliotecas y herramientas de reuso** son pilares del desarrollo eficiente en bajo nivel.

Dominar su creación, gestión y uso no solo acelera el desarrollo, sino que mejora la calidad, mantenibilidad y escalabilidad de los proyectos.
