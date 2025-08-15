# Acoplamiento y Cohesión

En el diseño de software, **acoplamiento** y **cohesión** son dos conceptos clave que ayudan a medir la calidad de la estructura y organización del código.

- **Cohesión**: Mide **qué tan relacionadas están las responsabilidades de un módulo o clase**.
- **Acoplamiento**: Mide **qué tanto depende un módulo o clase de otros para funcionar**.

El objetivo en el desarrollo es:

- **Alta cohesión**
- **Bajo acoplamiento**

---

## Cohesión

La **cohesión** describe el **grado de relación y enfoque** que tienen las funciones y datos dentro de un módulo.

- **Alta cohesión**: Todas las funciones de un módulo están estrechamente relacionadas con su responsabilidad principal.
- **Baja cohesión**: Un módulo realiza múltiples tareas no relacionadas.

### Beneficios de la alta cohesión

- Código más claro y entendible.
- Mayor facilidad de mantenimiento.
- Posibilidad de reutilización más sencilla.

---

### Tipos de cohesión (de más débil a más fuerte)

1. **Cohesión coincidental**

   - No hay relación clara entre las tareas.
   - Ejemplo: Un método que procesa datos, imprime reportes y envía emails.

2. **Cohesión lógica**

   - Tareas agrupadas porque son del mismo tipo, aunque no dependan unas de otras.

3. **Cohesión temporal**

   - Funciones que se ejecutan juntas en el mismo momento (por ejemplo, inicialización).

4. **Cohesión procedimental**

   - Tareas que siguen una secuencia de pasos.

5. **Cohesión comunicacional**

   - Funciones que trabajan sobre los mismos datos.

6. **Cohesión secuencial**

   - La salida de una función es la entrada de la siguiente.

7. **Cohesión funcional**

   - Todas las funciones trabajan para lograr un único objetivo claro.
   - Es la cohesión más deseada.

---

### Ejemplo de cohesión en Java

**Baja cohesión:**

```java
public class Utilities {
  public void processData() { ... }
  public void generateInvoice() { ... }
  public void sendMail() { ... }
}
```

- La clase mezcla responsabilidades sin relación directa.

**Alta cohesión:**

```java
public class ProcessData {
  public void processData() { ... }
  public void cleanData() { ... }
}
```

- La clase se enfoca en una sola responsabilidad: procesar datos.

---

## Acoplamiento

El **acoplamiento** describe el **grado de dependencia** entre módulos o clases.

- **Bajo acoplamiento**: Un módulo interactúa con otros solo a través de interfaces claras y mínimas.
- **Alto acoplamiento**: Un módulo depende mucho de la implementación interna de otros.

---

### Tipos de acoplamiento (de más fuerte a más débil)

1. **Acoplamiento de contenido** (más fuerte)

   - Un módulo accede directamente al código interno de otro.

2. **Acoplamiento común**

   - Módulos comparten variables globales.

3. **Acoplamiento externo**

   - Dependencia de interfaces externas mal definidas.

4. **Acoplamiento de control**

   - Un módulo controla el flujo interno de otro.

5. **Acoplamiento de sello** (_Stamp coupling_)

   - Pasar estructuras de datos completas cuando solo se necesita una parte.

6. **Acoplamiento de datos**

   - Pasar solo los datos necesarios entre módulos (lo ideal).

7. **Acoplamiento de mensaje** (más débil)

   - Comunicación mediante intercambio de mensajes (por ejemplo, en programación orientada a objetos).

---

### Ejemplo de acoplamiento en Java

**Alto acoplamiento:**

```java
public class Client {
  public void process() {
    Service s = new Service();
    s.attribute = "data"; // Acceso directo a datos internos
  }
}

class Service {
  public String attribute;
}
```

- `Client` depende directamente de la estructura interna de `Service`.

**Bajo acoplamiento:**

```java
public class Client {
  public void process() {
    Service s = new Service();
    s.setDato("data");  // Uso de interfaz pública
  }
}

class Service {
  private String attribute;

  public void setData(String data) {
    this.attribute = data;
  }
}
```

- `Client` interactúa con `Service` solo a través de métodos públicos.

---

## Relación entre cohesión y acoplamiento

| Alta cohesión           | Bajo acoplamiento                           |
| ----------------------- | ------------------------------------------- |
| Recomendado             | Recomendado                                 |
| Fácil de mantener       | Fácil de modificar sin romper otros módulos |
| Código más reutilizable | Código más independiente                    |

| Baja cohesión     | Alto acoplamiento                           |
| ----------------- | ------------------------------------------- |
| Evitar            | Evitar                                      |
| Código confuso    | Difícil de modificar y mantener             |
| Difícil de probar | Cambios en un módulo afectan a muchos otros |

---

## Buenas prácticas para lograr alta cohesión y bajo acoplamiento

1. **Aplicar el Principio de Responsabilidad Única (SRP)**.
2. **Encapsular la implementación interna** y exponer solo lo necesario.
3. **Usar interfaces y abstracciones** para comunicarse entre módulos.
4. **Evitar dependencias circulares**.
5. **Aplicar inyección de dependencias** para desacoplar componentes.
6. **Organizar el código por dominios y responsabilidades claras**.

---

## Ejemplo combinado en Java

```java
// Alta cohesión y bajo acoplamiento
public interface Notifier {
  void sendMessage(String msg);
}

public class EmailNotifier implements Notifier {
  public void sendMessage(String msg) {
    System.out.println("Sending email: " + msg);
  }
}

public class Order {
  private Notifier notifier;

  public Order(Notifier notifier) {
    this.notifier = notifier;
  }

  public void confirm() {
    // Lógica de confirmación.
    notifier.sendMessage("Order confirmed");
  }
}

public class Main {
  public static void main(String[] args) {
    Notifier email = new EmailNotifier();
    Order order = new Order(email);
    order.confirm();
  }
}
```

- **Alta cohesión**: Cada clase tiene una responsabilidad clara.
- **Bajo acoplamiento**: `Order` depende de una interfaz (`Notifier`), no de una implementación específica.

---

## Conclusión

- **Cohesión**: Qué tan bien enfocadas están las responsabilidades dentro de un módulo.

  > Buscar **alta cohesión** para módulos más claros y reutilizables.

- **Acoplamiento**: Qué tan dependientes son los módulos entre sí.

  > Buscar **bajo acoplamiento** para sistemas más flexibles y fáciles de mantener.

En conjunto, alta cohesión y bajo acoplamiento son indicadores de un **buen diseño de software**, favoreciendo la **modularidad, mantenibilidad y escalabilidad** del sistema.
