# Lógica

La **lógica** es la disciplina que estudia los principios del **razonamiento válido**, es decir, las reglas que permiten distinguir cuándo un argumento es correcto y cuándo no lo es. Es una herramienta fundamental en **matemática**, **filosofía**, **ciencias de la computación** y **programación**.

---

## Definición general

- **Lógica**: Rama de la filosofía y de las matemáticas que estudia las estructuras formales del pensamiento.
- Su objetivo es garantizar que, dadas ciertas **premisas**, se pueda obtener una **conclusión válida**.
- En programación, la lógica se utiliza para diseñar **algoritmos**, **estructuras de control**, **condiciones** y **operaciones booleanas**.

Ejemplo clásico:

> Premisa 1: Todos los humanos son mortales.  
> Premisa 2: Sócrates es humano.  
> Conclusión: Sócrates es mortal.

---

## Tipos de lógica

### Lógica proposicional

- Se basa en **proposiciones** (enunciados que pueden ser **verdaderos o falsos**, pero no ambos).
- Utiliza **conectivos lógicos** para formar proposiciones compuestas:
  - **¬** (negación, “no”)
  - **∧** (conjunción, “y”)
  - **∨** (disyunción, “o”)
  - **→** (implicación, “si... entonces”)
  - **↔** (bicondicional, “si y solo si”)

Ejemplo:

- p: "Está lloviendo"
- q: "Llevo paraguas"
- Proposición: _p → q_ = "Si está lloviendo, entonces llevo paraguas".

---

### Lógica de predicados (o lógica de primer orden)

- Extiende la lógica proposicional incorporando:
  - **Variables** (x, y, z)
  - **Cuantificadores**:
    - ∀ (para todo / universal)
    - ∃ (existe al menos uno / existencial)

Ejemplo:

- "Todos los estudiantes aprobaron el examen":

  - ∀x (Estudiante(x) → Aprobó(x))

- "Algún estudiante aprobó el examen":
  - ∃x (Estudiante(x) ∧ Aprobó(x))

---

### Lógica matemática

- Formaliza el razonamiento mediante símbolos y sistemas axiomáticos.
- Es la base de la **teoría de conjuntos**, **aritmética formal** y **demostraciones matemáticas**.

---

### Lógica computacional

- Rama aplicada a la informática:

  - **Lógica booleana**: Pperaciones sobre valores binarios (0 y 1).
  - **Álgebra de Boole**: Define cómo combinar variables lógicas.
  - Ejemplo en programación:

    ```java
    boolean a = true;
    boolean b = false;
    System.out.println(a && !b);  // true
    ```

---

## Tablas de verdad

Las **tablas de verdad** muestran el valor de una proposición compuesta en función de los valores de sus proposiciones simples.

### Ejemplo: Conjunción (p ∧ q)

| p   | q   | p ∧ q |
| --- | --- | ----- |
| V   | V   | V     |
| V   | F   | F     |
| F   | V   | F     |
| F   | F   | F     |

### Ejemplo: Implicación (p → q)

| p   | q   | p → q |
| --- | --- | ----- |
| V   | V   | V     |
| V   | F   | F     |
| F   | V   | V     |
| F   | F   | V     |

---

## Razonamiento lógico

### Deductivo

- Parte de premisas generales para llegar a conclusiones particulares.
- Ejemplo:
  - Todos los perros son mamíferos.
  - Fido es un perro.
  - ⇒ Fido es un mamífero.

### Inductivo

- Parte de casos particulares para llegar a conclusiones generales (probables).
- Ejemplo:
  - El sol salió hoy.
  - El sol salió ayer.
  - ⇒ El sol siempre sale cada día. (probable, no seguro).

### Abductivo

- Razonamiento basado en la mejor explicación posible.
- Ejemplo:
  - El césped está mojado.
  - ⇒ Posible explicación: Llovió.

---

## Aplicaciones en programación

- **Condicionales**:

  ```java
  if (edad >= 18 && ciudadano) {
    System.out.println("Puede votar");
  }
  ```

- **Ciclos** (condiciones lógicas para repetición).
- **Búsqueda y algoritmos** (por ejemplol, árboles de decisión).
- **Verificación de software** (demostrar corrección lógica).
- **Inteligencia Artificial** (lógica difusa, razonamiento automático).

---

## Principales leyes de la lógica

- **Identidad**: p ≡ p
- **No contradicción**: ¬(p ∧ ¬p)
- **Tercero excluido**: p ∨ ¬p
- **De Morgan**:

  - ¬(p ∧ q) ≡ (¬p ∨ ¬q)
  - ¬(p ∨ q) ≡ (¬p ∧ ¬q)

Ejemplo en código:

```java
boolean p = true;
boolean q = false;
System.out.println(!(p && q) == (!p || !q));  // Ley de De Morgan: true
```

---

## Ejemplo práctico: Validación de acceso

```java
public class Main {
  public static void main(String[] args) {
    String user = "admin";
    String key = "1234";

    if (user.equals("admin") && key.equals("1234")) {
      System.out.println("Access granted");
    } else {
      System.out.println("Access denied");
    }
  }
}
```

Acá se utiliza una **conjunción lógica (AND)** para validar simultáneamente dos condiciones.

---

## Importancia de la lógica

- Permite **razonar correctamente** y evitar contradicciones.
- Es la base de la **matemática moderna**.
- En computación, se traduce directamente en **circuitos electrónicos** (puertas lógicas).
- En programación, asegura que los algoritmos tengan **condiciones claras** y **ejecución predecible**.
- Es esencial para áreas como:
  - **Verificación formal de programas**.
  - **Bases de datos** (consultas SQL, lógica de predicados).
  - **Inteligencia artificial y sistemas expertos**.

---

## Conclusión

La lógica es una herramienta transversal que conecta la **filosofía**, la **matemática** y la **informática**.

Permite construir **argumentos válidos**, diseñar **algoritmos correctos**, y fundamentar gran parte del conocimiento científico y tecnológico.
