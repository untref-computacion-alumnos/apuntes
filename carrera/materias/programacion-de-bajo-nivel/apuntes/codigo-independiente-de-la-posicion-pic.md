# Código Independiente de la Posición (PIC)

EL [PIC (Position Independent Code)](https://en-m-wikipedia-org.translate.goog/wiki/Position-independent_code?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=tc) es un tipo de código máquina diseñado para ejecutarse correctamente **sin importar en qué dirección de memoria se cargue**.

Este concepto es fundamental en sistemas operativos modernos, especialmente para implementar **bibliotecas compartidas (shared libraries)** y para mejorar la **seguridad** de la memoria.

---

## ¿Por qué es importante el PIC?

En un programa normal, el compilador genera instrucciones que hacen referencia a **direcciones absolutas** en memoria. Esto significa que el código **asume** que será cargado en una ubicación específica.

Sin embargo, en muchos escenarios esto no es posible o seguro:

- **Bibliotecas compartidas**: Deben poder cargarse en distintas direcciones en diferentes procesos.
- [**ASLR (Address Space Layout Randomization)**](https://en.wikipedia.org/wiki/Address_space_layout_randomization): Una técnica de seguridad que cambia aleatoriamente las direcciones de carga para prevenir ataques.
- **Carga dinámica de módulos**: Plugins o controladores que se insertan en tiempo de ejecución.

El PIC permite que un mismo binario funcione **correctamente** incluso si se carga en ubicaciones de memoria distintas.

---

## ¿Cómo funciona el PIC?

El PIC se basa en el uso de **direcciones relativas** en lugar de direcciones absolutas.

En lugar de referirse a una variable o función usando su ubicación exacta en memoria, el codigo usa **offsets** calculados en tiempo de ejecución.

Ejemplo conceptual:

- **Código normal**: Carga valor desde la dirección `0x00402010`.
- **Código PIC**: Carga valor desde [Registro Base + Desplazamiento].

El **registro base** apunta a la posición actual del código o a una tabla especial (GOT o PLT) que almacena direcciones reales.

---

## GOT y PLT

En sistemas **Unix/Linux** usando [ELF (Executable and Linkable Format)](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format), el PIC se implementa con ayuda de:

- [**GOT (Global Offset Table)**](https://en.wikipedia.org/wiki/Global_Offset_Table): Contiene las direcciones reales de variables y datos globales.
- [**PLT (Proceduce Linkage Table)**](https://docs.oracle.com/cd/E26505_01/html/E26506/chapter6-1235.html): Contiene las direcciones de funciones externas, resolviéndolas solo la primera vez que se llaman.

Esto permite que el código nunca necesite saber de antemano la dirección absoluta de algo; simplemente accede a través de la tabla.

---

## Ejemplo en C

Compilando un programa como PIC:

```sh
gcc -fPIC -c example.c -o example.o
```

Código:

```c
#include <stdio.h>

int global = 42;

void show() {
  printf("Global: %d\n", global);
}

int main() {
  show();

  return 0;
}
```

Al compilar con `-fPIC`, el compilador genera acceso a `global` a través de la **GOT**, evitando direcciones absolutas.

---

## PIC y bibliotecas compartidas

Las **bibliotecas compartidas** (`.so` en Linux, `.dll` en Windows) se benefician del PIC porque:

- Pueden ser cargadas en **cualquier** dirección libre del espacio de memoria del proceso.
- El mismo código de biblioteca puede ser usado por múltiples procesos **sin necesidad de recompilar**.

En Linux, la mayoría de las bibliotecas del sistema están compiladas con `-fPIC`.

---

## PIC y seguridad

El PIC es clave para implementar **ASLR**:

- ASLR mueve aleatoriamente las secciones de código y datos de un programa cada vez que se ejecuta.
- Esto dificulta que un atacante pueda predecir la ubicación de instrucciones vulnerables.
- Sin PIC, el código no podría moverse fácilmente.

---

## Ventajas y desventajas

### Ventajas

- **Flexibilidad**: Código puede cargarse en cualquier dirección.
- **Compatibilidad**: Facilita el uso de bibliotecas compartidas.
- **Seguridad**: Permite ASLR y dificulta ciertos exploits.
- **Eficiencia en memoria**: Múltiples procesos pueden compartir la misma copia del código.

### Desventajas

- **Pequeña pérdida de rendimiento**: Debido al uso de tablas intermedias (GOT/PLT) para resolver direcciones.
- **Tamaño de código mayor**: Se añaden estructuras de datos para manejar las referencias.

---

## Resumen

El **Código Independiente de la Posición (PIC)** es una técnica de compilación que permite que un programa o biblioteca se ejecute correctamente sin importar en qué lugar de la memoria se cargue.

Su uso es fundamental para:

- Bibliotecas compartidas.
- Carga dinámica de módulos.
- Implementar medidas de seguridad como ASLR.

Aunque tiene costo de rendimiento, tiene beneficios en flexibilidad, reutilización y seguridad lo hacen indispensable en sistemas modernos.
