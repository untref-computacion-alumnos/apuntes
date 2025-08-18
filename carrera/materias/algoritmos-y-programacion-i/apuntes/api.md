# La API de Java

## Introducción

La **API de Java (Application Programming Interface)** es el conjunto de **clases, interfaces y paquetes predefinidos** que provee el propio lenguaje Java para facilitar el desarrollo de aplicaciones.

En lugar de tener que programar todo desde cero, los desarrolladores pueden **reutilizar código confiable** que ya fue probado, optimizado y documentado por _Oracle_ y la comunidad.

La API forma parte del **JDK (Java Development Kit)** y se encuentra organizada en **paquetes (packages)**.

---

## ¿Qué contiene la API de Java?

La API está formada por miles de clases e interfaces que permiten:

- **Entrada/Salida (I/O)**: Lectura y escritura de archivos, flujos de datos, sockets.
- **Colecciones**: Estructuras de datos como listas, mapas, conjuntos, colas.
- **Redes**: Soporte para programación cliente/servidor.
- **Bases de datos (JDBC)**: Conexión y consultas en SQL.
- **Interfaz gráfica (GUI)**: Construcción de interfaces gráficas con _Swing_, _AWT_ y _JavaFX_.
- **Concurrencia**: Manejo de hilos, sincronización y paralelismo.
- **Utilidades**: Fechas, calendarios, matemáticas, expresiones regulares, etc.
- **Seguridad y criptografía**: Cifrado, firmas digitales, manejo de permisos.

---

## Organización en paquetes

Las clases de la API de Java están organizadas en **paquetes**.

Algunos de los más usados son:

- `java.lang`: Clases básicas (String, Math, Object, Integer, etc.).
- `java.util`: Estructuras de datos, colecciones, utilidades.
- `java.io`: Entrada y salida de datos.
- `java.nio`: Entrada/salida no bloqueante.
- `java.net`: Programación de redes.
- `java.sql`: Acceso a bases de datos mediante JDBC.
- `java.time`: Manejo moderno de fechas y horas.
- `javax.swing`: Interfaces gráficas con Swing.
- `javafx.*`: Desarrollo moderno de interfaces gráficas.
- `java.security`: Seguridad y criptografía.

---

## Ejemplo básico de uso de la API

```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    // Uso de la clase ArrayList de java.util
    ArrayList<String> list = new ArrayList<>();

    list.add("Java");
    list.add("Python");
    list.add("Go");

    System.out.println("Languages: " + list);

    // Uso de la clase Math de java.lang
    double raiz = Math.sqrt(16);
    System.out.println("Square root of 16: " + raiz);
  }
}
```

**Salida:**

```md
Languages: [Java, Python, Go]
Square root of 16: 4.0
```

---

## API vs Librerías Externas

- **API de Java**: Forma parte del JDK, se instala automáticamente con Java y se encuentra siempre disponible.

- **Librerías externas (frameworks, dependencias)**: Son desarrolladas por terceros (por ejemplo, Hibernate, Spring, Apache Commons) y deben agregarse manualmente al proyecto mediante un gestor de dependencias como _Maven_ o _Gradle_.

---

## Documentación oficial

La API de Java está completamente documentada en formato **JavaDoc**, que describe:

- Paquetes
- Clases
- Interfaces
- Métodos y atributos
- Ejemplos de uso

Enlace oficial: [Java SE API Documentation](https://docs.oracle.com/en/java/javase/)

---

## Ventajas de la API de Java

- Reutilización de código probado y confiable.
- Ahorro de tiempo en el desarrollo.
- Portabilidad entre sistemas operativos.
- Documentación extensa y detallada.
- Estándar mantenido por Oracle y la comunidad.

---

## Ejemplos destacados de uso

### Manejo de cadenas (`java.lang.String`)

```java
public class Main {
  public static void main(String[] args){
    String text = "¡Hello, World!";
    System.out.println(text.toUpperCase());   // Salida: ¡Hello, World
    System.out.println(text.substring(1, 6)); // Hola
  }
}
```

### Manejo de fechas (`java.time`)

```java
import java.time.LocalDate;

public class Main {
  public static void main(String[] args) {
    LocalDate today = LocalDate.now();
    System.out.println("Actual date: " + today);
  }
}
```

### Lectura de archivos (`java.io`)

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class Main {
  public static void main(String[] args) {
    try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
      String line;
      while ((line = br.readLine()) != null) {
        System.out.println(line);
      }
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

---

## Conclusión

La **API de Java** es el **corazón del desarrollo en este lenguaje**, ya que ofrece todas las herramientas necesarias para crear aplicaciones robustas, seguras y multiplataforma.

Conocer sus paquetes y clases más importantes es esencial para todo programador Java.
