# Invariantes de Representación

Las **invariantes de representación** son condiciones lógicas que deben cumplirse **siempre** para que el estado interno de un objeto sea válido.

Son una parte fundamental del **Diseño por Contrato** y se utilizan para garantizar la **consistencia de los datos** durante todo el ciclo de vida de un objeto.

---

## Definición

Una **invariante de representación** es una propiedad que:

- Describe el **estado válido** de un objeto.
- **Debe cumplirse**:
  1. Justo después de que el objeto es creado (constructor).
  2. Después de la ejecución de cualquier método público.
  3. Siempre que el objeto esté visible para el "mundo exterior".
- **No necesariamente se cumple** mientras un método privado está modificando el estado del objeto (pero debe restaurarse antes de terminar el método).

---

## Propósito

- **Asegurar la integridad de los datos**: Evita estados inválidos.
- **Reducir errores lógicos**: Detecta violaciones de estado rápidamente.
- **Documentar el comportamiento esperado**: Sirve como guía para otros desarrolladores.
- **Facilitar el mantenimiento**: Si se modifica el código, las invariantes ayudan a comprobar que el nuevo comportamiento es correcto.

---

## Ejemplo en lenguaje natural

En una **cuenta bancaria**, una invariante podría ser:

> "El saldo nunca puede ser negativo."

Esto significa que:

- Al crear la cuenta el saldo inicial debe ser ≥ 0.
- Después de depositar o retirar el saldo debe seguir siendo ≥ 0.
- Si en algún momento es < 0, se rompió la invariante.

---

## Ejemplo en Java

### Definiendo una invariante

```java
public class BankAccount {
  private double balance;

  public BankAccount(double balance) {
    if (balance < 0) {
      throw new IllegalArgumentException("Initial balance cannot be negative");
    }
    this.balance = balance;
    verifyInvariant();
  }

  public void deposit(double amount) {
    if (amount <= 0) {
      throw new IllegalArgumentException("Invalid amount");
    }
    balance += amount;
    verifyInvariant();
  }

  public void withdraw(double amount) {
    if (amount <= 0) {
      throw new IllegalArgumentException("Invalid amount");
    }
    if (amount > balance) {
      throw new IllegalArgumentException("Insufficient balance");
    }
    balance -= amount;
    verifyInvariant();
  }

  public double getBalance() {
    return balance;
  }

  // Método para comprobar la invariante
  private void verifyInvariant() {
    assert balance >= 0 : "Invariant violated: negative balance";
  }
}
```

**Invariante de representación**: `balance >= 0`

---

## Características de las invariantes

- **Visibilidad**: Las invariantes no necesariamente son visibles para el usuario final, pero sí para el desarrollador.
- **Permanencia**: Siempre deben cumplirse en los estados estables del objeto.
- **Especificidad**: Describen condiciones concretas (no vaguedades).
- **Testabilidad**: Pueden comprobarse mediante código (`assert`) o tests unitarios.

---

## Cuándo verificar las invariantes

1. **En el constructor** garantiza que el objeto comienza en un estado válido.
2. **En el final de cada método público** asegura que el objeto no se corrompe.
3. **En puntos críticos del código** después de operaciones complejas o cambios masivos de estado.

---

## Ejemplo avanzado con varias invariantes

```java
public class Rectangle {
  private int width;
  private int high;

  public Rectangle(int width, int high) {
    this.width = width;
    this.high = high;
    verifyInvariant();
  }

  public void redimensionar(int width, int high) {
    this.width = width;
    this.high = high;
    verifyInvariant();
  }

  public int getArea() {
    return width * high;
  }

  private void verifyInvariant() {
    assert width > 0 : "Invariant violated: width must be positive";
    assert high > 0 : "Invariant violated: high must be positive";
    assert getArea() > 0 : "Invariant violated: the area must be positive";
  }
}
```

**Invariantes de representación**:

1. `width > 0`.
2. `high > 0`.
3. `width * high > 0` (el área es positiva).

---

## Invariantes vs. Pre/Postcondiciones

| Característica  | Precondiciones              | Postcondiciones               | Invariantes                         |
| --------------- | --------------------------- | ----------------------------- | ----------------------------------- |
| **Momento**     | Antes de ejecutar un método | Después de ejecutar un método | Antes y después de cualquier método |
| **Responsable** | Cliente                     | Proveedor                     | Clase (internamente)                |
| **Objetivo**    | Validar entrada             | Validar salida                | Mantener consistencia interna       |

---

## Buenas prácticas

- **Definir invariantes claras y simples**.
- **Centralizar su comprobación** en un método privado (`verifyInvariant`).
- **Usar `assert`** para verificaciones en tiempo de desarrollo.
- **No exponer estado interno** que permita romper invariantes desde fuera.
- **Escribir tests automáticos** que intenten violar invariantes y confirmen que el sistema lo impide.

---

## Ventajas de las invariantes

- **Mayor robustez**: Detecta errores de lógica en etapas tempranas.
- **Mejor documentación**: Describe explícitamente lo que siempre debe cumplirse.
- **Mantenibilidad**: Si se cambian métodos internos, se puede verificar fácilmente que el estado sigue siendo válido.
- **Prevención de corrupción de datos**: Evita estados ilegales en la memoria.

---

## Conclusión

Las **invariantes de representación** son un pilar del diseño seguro y confiable de software orientado a objetos.

En Java, aunque no exista una sintaxis especial para ellas, se pueden implementar de forma sencilla mediante métodos privados y **aserciones**.

Definirlas y respetarlas es esencial para garantizar que los objetos **siempre permanezcan en un estado válido** durante todo su ciclo de vida.
