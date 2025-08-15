# Diseño por Contrato (Design by Contract, DbC)

El **Diseño por Contrato** es una metodología de desarrollo de software que establece acuerdos formales entre las partes de un sistema (módulos, clases, métodos) mediante **contratos** que especifican:

- **Qué condiciones deben cumplirse antes de ejecutar una operación** (precondiciones).
- **Qué se garantiza una vez finalizada la operación** (postcondiciones).
- **Qué se mantiene verdadero siempre en el ciclo de vida del objeto** (invariantes).

La idea fue introducida por **Bertrand Meyer** en el lenguaje **Eiffel**, pero sus principios pueden aplicarse en cualquier lenguaje, incluido **Java**.

---

## Concepto básico

En DbC, cada método o clase se considera una **entidad contratante**.

El contrato define las **obligaciones** y **beneficios**:

- **Obligaciones**: Condiciones que debe cumplir el cliente (quien invoca el método).
- **Beneficios**: Garantías que provee el proveedor (quien implementa el método).

**Analogía**: Igual que en un contrato legal:

- Si ambas partes cumplen con lo estipulado, el resultado es correcto.
- Si una parte no cumple su obligación, se rompe el contrato.

---

## Elementos clave del Diseño por Contrato

### Precondiciones

Condiciones que deben cumplirse **antes** de que se ejecute un método.

- **Responsabilidad del cliente**: El código que llama al método debe garantizar que estas condiciones son verdaderas.
- Si no se cumplen, el método **no tiene obligación** de funcionar correctamente.

**Ejemplo en Java**:

```java
public class Calculator {
  public double divide(double numerator, double denominator) {
    if (denominator == 0) {
      throw new IllegalArgumentException("The denominator cannot be zero");
    }
    return numerator / denominator;
  }
}
```

- **Precondición**: `denominator != 0`

---

### Postcondiciones

Condiciones que deben cumplirse **después** de que el método haya terminado.

- **Responsabilidad del proveedor**: Si las precondiciones se cumplieron, el método debe garantizar que las postcondiciones también lo hagan.

**Ejemplo en Java**:

```java
public class Bank {
  private double balance;

  public Bank(double balance) {
    this.balance = balance;
  }

  public void deposit(double amount) {
    double balancePrevious = balance;
    balance += amount;

    assert balance == saldoAnterior + amount : "Postcondition failed: balance is not correct";
  }
}
```

- **Postcondición**: el saldo final = saldo anterior + monto.

---

### nvariantes

Condiciones que **siempre** deben cumplirse durante la vida del objeto.

- Deben ser verdaderas **antes y después** de cualquier método público.
- Garantizan que el objeto siempre está en un **estado válido**.

**Ejemplo en Java**:

```java
public class Account {
  private double balance;

  public Account(double balance) {
    if (balance < 0) {
      throw new IllegalArgumentException("Negative opening balance");
    }
    this.balance = balance;
  }

  public void retirar(double amount) {
    if (amount > balance) {
      throw new IllegalArgumentException("Insufficient balance");
    }
    balance -= amount;
    assert balance >= 0 : "Failed invariant: negative balance";
  }
}
```

- **Invariante**: `balance >= 0`

---

## Beneficios del Diseño por Contrato

1. **Mayor claridad**: Las responsabilidades de cada parte están explícitas.
2. **Menos errores**: Se detectan incumplimientos rápidamente.
3. **Facilidad de mantenimiento**: Cambios más seguros al estar documentadas las condiciones.
4. **Documentación viva**: El contrato actúa como parte de la especificación del software.
5. **Pruebas más efectivas**: Los contratos ayudan a definir casos de prueba claros.

---

## Cómo aplicar DbC en Java

Java no tiene soporte nativo para DbC como Eiffel, pero se puede implementar mediante:

- **Excepciones**: Para manejar violaciones de precondiciones y postcondiciones.
- **Aserciones (`assert`)**: Para verificar invariantes y postcondiciones durante la ejecución.
- **Documentación Javadoc**: Para declarar explícitamente las precondiciones y postcondiciones.
- **Bibliotecas externas**: Como _Java Modeling Language (JML)_ o _OVal_.

---

### Ejemplo integral en Java con precondiciones, postcondiciones e invariantes

```java
/**
 * Clase que representa una cuenta bancaria simple.
 */
public class BankAccount {
  private double balance;

  /**
   * Constructor con saldo inicial.
   *
   * @param balance Debe ser mayor a 0.
   *
   * @throws IllegalArgumentException Si {@code balance} es menor o igual a 0.
   */
  public BankAccount(double balance) {
    if (balance < 0) {
      throw new IllegalArgumentException("Negative opening balance");
    }
    this.balance = balance;
    verifyInvariant();
  }

  /**
   * Deposita un monto positivo en la cuenta.
   *
   * @param amount El monto (positivo) a depositar.
   *
   * @throws IllegalArgumentException Si {@code amount} es menor o igual a 0.
   */
  public void deposite(double amount) {
    if (amount <= 0) {
      throw new IllegalArgumentException("Invalid amount");
    }
    double balancePrevious = balance;
    balance += amount;
    assert balance == balancePrevious + amount : "Postcondition failed";
    verifyInvariant();
  }

  /**
   * Retira un monto de la cuenta.
   *
   * @param amount El monto a retirar (mayor a 0 y menor o igual que el saldo actual).
   *
   * @throws IllegalArgumentException Si {@code amount} es menor o igual que 0, o si es mayor al saldo actual.
   */
  public void withdraw(double amount) {
    if (amount <= 0) {
      throw new IllegalArgumentException("Invalid amount");
    }
    if (amount > balance) {
      throw new IllegalArgumentException("Insufficient balance");
    }
    double balancePrevious = balance;
    balance -= amount;
    assert balance == balancePrevious - amount : "Postcondition failed";
    verifyInvariant();
  }

  private void verifyInvariant() {
    assert balance >= 0 : "Failed invariant: negative balance";
  }

  public double getBalance() {
    return balance;
  }
}
```

---

## Buenas prácticas al usar DbC

1. **Especificar siempre las precondiciones y postcondiciones** en la documentación.
2. **No depender solo de comentarios**: Verificar las condiciones en tiempo de ejecución.
3. **Mantener las invariantes simples y claras**.
4. **Usar aserciones para condiciones que no deberían fallar** en producción.
5. **Evitar sobrevalidar** en métodos internos si ya hay garantías externas.
6. **Tratar los contratos como parte del diseño, no solo de la implementación**.

---

## Limitaciones del Diseño por Contrato

- **Rendimiento**: Las verificaciones pueden agregar sobrecarga en tiempo de ejecución.
- **Lenguajes sin soporte nativo** requieren más código adicional.
- **No reemplaza las pruebas**: Los contratos complementan, pero no sustituyen el testing.
- **Posible duplicación**: Precondiciones y postcondiciones pueden solaparse con validaciones de negocio.

---

## Conclusión

El **Diseño por Contrato** ayuda a crear sistemas más confiables y fáciles de mantener.

En Java, aunque no haya soporte nativo, se puede implementar combinando **validaciones, aserciones y documentación** para garantizar que:

- **Precondiciones**: El cliente cumple los requisitos para invocar.
- **Postcondiciones**: El proveedor cumple lo prometido si las precondiciones se cumplieron.
- **Invariantes**: El estado del objeto siempre es válido.

Adoptar esta metodología fomenta un **diseño más claro, robusto y predecible**, clave en el desarrollo de software de calidad.
