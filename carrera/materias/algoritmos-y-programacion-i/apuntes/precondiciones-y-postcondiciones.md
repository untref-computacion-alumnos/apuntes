# Precondiciones y Postcondiciones

En el desarrollo de software, las **precondiciones** y **postcondiciones** son conceptos fundamentales para garantizar que los métodos, funciones o procedimientos se ejecuten correctamente y produzcan resultados esperados.

Forman parte de la metodología de **Diseño por Contrato** (Design by Contract), que define acuerdos formales entre el código que llama (cliente) y el código que se ejecuta (proveedor).

---

## Concepto general

### Precondición

Es una **condición lógica** que debe cumplirse **antes** de ejecutar un método o función para que su comportamiento sea correcto.

- Es una **obligación del cliente**: Quien invoca el método debe asegurarse de cumplirla.
- Si la precondición no se cumple, el método no garantiza su funcionamiento correcto.
- Se utilizan para:
  - Validar parámetros de entrada.
  - Garantizar que el estado del objeto es válido antes de la ejecución.

**Ejemplo en lenguaje natural**:

> "Solo puedo retirar dinero si el saldo es suficiente".

---

### Postcondición

Es una **condición lógica** que debe cumplirse **después** de la ejecución de un método o función, siempre que las precondiciones hayan sido satisfechas.

- Es una **obligación del proveedor**: si las precondiciones se cumplieron, el método debe garantizar que la postcondición se cumple.
- Se utilizan para:
  - Garantizar que el resultado final sea el esperado.
  - Verificar que los efectos colaterales sean correctos.

**Ejemplo en lenguaje natural**:

> "Después de retirar dinero, el saldo será el saldo anterior menos el monto retirado".

---

## Relación entre precondiciones y postcondiciones

| Aspecto                   | Precondición                                       | Postcondición                                       |
| ------------------------- | -------------------------------------------------- | --------------------------------------------------- |
| **Momento de evaluación** | Antes de ejecutar el método                        | Después de ejecutar el método                       |
| **Responsable**           | Cliente (quien llama al método)                    | Proveedor (quien implementa el método)              |
| **Propósito**             | Verificar que se cumplen las condiciones iniciales | Garantizar el estado o resultado final correcto     |
| **Consecuencia si falla** | El método no está obligado a funcionar bien        | Es un error de implementación o lógica en el método |

---

## Ejemplos en Java

### Ejemplo con precondición

```java
public class Calculator {
  /**
   * Divide dos números.
   *
   * @throws IllegalArgumentException Si {@code denominator} es 0.
   */
  public double divide(double numerator, double denominator) {
    if (denominator == 0) { // Precondición: el denominador no puede ser cero.
      throw new IllegalArgumentException("The denominator cannot be zero.");
    }
    return numerator / denominator;
  }
}
```

- **Precondición**: `denominator != 0`.
- Si el cliente no respeta esta condición, el método lanza una excepción.

---

### Ejemplo con postcondición

```java
public class Account {
  private double balance;

  public Account(double balance) {
    if (balance < 0) {
      throw new IllegalArgumentException("Negative opening balance");
    }
    this.balance = balance;
  }

  /**
   * Deposita un monto positivo en la cuenta.
   */
  public void deposit(double amount) {
    double balancePrevious = balance;
    balance += amount;
    assert balance == balancePrevious + amount : "Postcondition failed: balance is not correct";  // Postcondición: el saldo final será el saldo anterior + monto.
  }

  public double getbalance() {
    return balance;
  }
}
```

- **Postcondición**: `saldo_final == balancePrevious + amount`.
- Si la postcondición falla, significa que el método no está funcionando según lo esperado.

---

### Ejemplo integral con ambas

```java
public class BankAccount {
  private double balance;

  public BankAccount(double balance) {
    if (balance < 0) {
      throw new IllegalArgumentException("Negative opening balance");
    }
    this.balance = balance;
  }

  /**
   * Retira dinero de la cuenta.
   */
  public void retirar(double amount) {
    // Precondiciones
    if (amount <= 0) {
      throw new IllegalArgumentException("Invalid amount");
    }
    if (amount > balance) {
      throw new IllegalArgumentException("Insufficient balance");
    }

    double balancePrevious = balance;
    balance -= amount;

    // Postcondición
    assert balance == balancePrevious - amount : "Postcondition failed";
  }
}
```

---

## Implementación en Java

En Java, las precondiciones y postcondiciones se pueden implementar usando:

1. **Validaciones con excepciones o errores**:

   - `IllegalArgumentException` para parámetros inválidos.
   - `IllegalStateException` si el estado del objeto es incorrecto.
   - `Error` para cuando se requiere que el programa termine la ejecución de forma abrupta.

2. **Aserciones (`assert`)**:

   - Útiles para validar postcondiciones e invariantes.
   - Se activan con el flag `-ea` al ejecutar (`java -ea Programa`).

3. **Documentación Javadoc**:

   - Especificar explícitamente las condiciones usando `@pre` y `@post` (por convención, no es estándar del lenguaje).

4. **Bibliotecas externas**:

   - _Java Modeling Language (JML)_ permite declarar pre/post/invariantes en comentarios y verificarlos automáticamente.

---

## Buenas prácticas

- **Especificar siempre** las precondiciones y postcondiciones, incluso en métodos privados si son relevantes.
- **No duplicar validaciones innecesarias** si el contrato ya lo garantiza.
- **Usar nombres de variables descriptivos** para que las condiciones sean legibles.
- **Documentar con ejemplos** para que otros desarrolladores entiendan rápidamente las reglas.
- **No abusar de las precondiciones**, demasiadas restricciones pueden hacer que el método sea difícil de reutilizar.
- **Asegurarse de cumplir las postcondiciones siempre**, incluso si hay excepciones intermedias.

---

## Ventajas de su uso

- Mejora la **claridad** y la **comunicación** entre desarrolladores.
- Reduce errores al detectar condiciones incorrectas antes de que el método ejecute lógica compleja.
- Facilita el **testing** al definir de forma precisa los escenarios de entrada y salida válidos.
- Ayuda en la **mantenibilidad** del software: cualquier cambio debe seguir cumpliendo las mismas condiciones.

---

## Conclusión

Las **precondiciones** y **postcondiciones** son herramientas clave para construir software más **robusto**, **claro** y **fácil de mantener**.

En Java, aunque no haya soporte nativo específico, se pueden implementar de forma efectiva con **excepciones, aserciones y documentación**.

Respetar estos contratos asegura que los métodos funcionen dentro de un marco previsible y controlado, reduciendo errores y mejorando la calidad global del sistema.
