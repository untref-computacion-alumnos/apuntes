# Composición y Descomposición

La **composición** y la **descomposición** son procesos clave en el análisis y desarrollo de soluciones.

Permiten estructurar un problema o sistema, ya sea **uniendo elementos** para formar algo más complejo (composición) o **dividiéndolo** en partes más simples (descomposición).

Estos conceptos son aplicables tanto en programación como en otras áreas de la ingeniería y la resolución de problemas.

---

## Definiciones

### Composición

La **composición** consiste en integrar varias partes, componentes o funciones para formar un todo más complejo que cumpla un objetivo específico.

En programación, la composición implica **combinar módulos, funciones o clases** para crear programas más grandes y funcionales.

**Ejemplo**:

- Combinar funciones de entrada, procesamiento y salida para formar un sistema de gestión de notas.
- En matemáticas: Componer funciones $f(g(x))$.

---

### Descomposición

La **descomposición** es el proceso inverso: consiste en **dividir un problema o sistema complejo en partes más pequeñas y manejables**.

En programación, la descomposición se utiliza para:

- Gestión de clientes.
- Gestión de productos.
- Procesamiento de pagos.
- Generación de reportes.

---

## Importancia en la resolución de problemas

La **descomposición** ayuda a **entender** y **planificar** la solución, mientras que la **composición** permite **integrar** las partes para obtener un resultado final coherente.

- **Descomposición**:

  - Reduce la complejidad.
  - Facilita la detección de errores.
  - Favorece la asignación de tareas en equipos.

- **Composición**:

  - Permite reutilizar soluciones.
  - Integra componentes probados para formar sistemas robustos.
  - Acelera el desarrollo al reutilizar módulos existentes.

---

## Estrategias

### Estrategia de descomposición

- **Dividir por funciones**: Separar en base a tareas (por ejemplo, entrada, procesamiento, salida).
- **Dividir por datos**: Separar en base a la estructura de los datos que se procesan.
- **Dividir por niveles de abstracción**: Primero resolver de forma general y luego entrar en detalles (refinamientos sucesivos).

### Estrategia de composición

- **Integración ascendente (Bottom-Up)**:

  - Primero se desarrollan las partes más básicas.
  - Después se integran en niveles superiores.

- **Integración descendente (Top-Down)**:

  - Primero se diseña el sistema general.
  - Después se desarrollan e integran los componentes.

---

## Ejemplo

**Problema**: Diseñar un programa que calcule el promedio de notas de un grupo y determine si aprobaron.

### Descomposición

1. **Entrada de datos**: Leer las notas.
2. **Procesamiento**: Calcular el promedio.
3. **Decisión**: Determinar si el promedio es mayor o igual a 6.
4. **Salida**: Mostrar promedio y estado.

### Composición

1. Crear una función `leerNotas()`.
2. Crear una función `calcularPromedio(lista)`.
3. Crear una función `determinarEstado(promedio)`.
4. Integrar todo en un solo.

```text
INICIO FUNCIÓN leerNotas()
  RETORNAR [7, 8, 5, 9]
FIN FUNCIÓN

INICIO FUNCIÓN calcularPromedio(notas)
  RETORNAR suma(notas) / largo(notas)
FIN FUNCIÓN

INICIO FUNCIÓN determinarEstado(promedio)
  SI promedio ES MAYOR O IGUAL QUE 4
    RETORNAR "Aprobado"
  SI NO
    RETORNAR "Desaprobado"
  FIN SI
FIN FUNCIÓN

INICIO FUNCIÓN main()
  notas <- leerNotas()
  promedio <- calcularPromedio(notas)
  estado <- determinarEstado(promedio)
  ESCRIBIR(promedio)
  ESCRIBIR(estado)
FIN FUNCIÓN
```

---

## Ventajas de usar composición y descomposición

- **Organización**: Facilita trabajar de forma estructurada.
- **Mantenimiento**: Cambios en una parte no afectan al resto si está bien modularizado.
- **Reutilización**: Los componentes pueden usarse en otros proyectos.
- **Trabajo colaborativo**: Permite asignar partes específicas a diferentes miembros del equipo.
- **Pruebas más simples**: Se pueden validar módulos por separado antes de integrarlos.

---

## Relación con otros conceptos

- **Refinamiento sucesivo**: La descomposición puede aplicarse de forma iterativa hasta llegar a un nivel detallado.
- **Modularidad**: La composición usa módulos creados en la descomposición.
- **Abstracción**: Permite ocultar detalles de implementación y centrarse en la funcionalidad.

---

## Conclusión

La **descomposición** permite entender y planificar mejor los problemas complejos dividiéndolos en partes simples.

La **composición** permite integrar esas partes para formar soluciones completas y funcionales.

Usar los dos procesos de forma complementaria sirve para desarrollar soluciones eficientes, mantenibles y escalables.
