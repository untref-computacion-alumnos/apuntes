# Apuntes de Ingeniería en Computación - UNTREF

# <<<<<<< HEAD

Se pide leer este `README.md` antes de clonar este repositorio para entender claramente su funcionamiento.

## Instalación y configuración del entorno

Si querés desarrollar, compilar o modificar los apuntes centralizados de las materias, tenés que seguir estos pasos.

> [!TIP]
> Para esta guía se asume que Python está instalado
>
> Se recomienda crear un entorno virtual de Python para trabajar con el proyecto.

1. Clonar el repositorio (se recomienda uso de [clave SSH](https://github.com/settings/keys)).

   ```sh
   git clone git@github.com:untref-computacion-alumnos/apuntes.git
   ```

2. Instalar las dependencias del proyecto:

   ```sh
   pip install -r requirements.txt
   ```

   - Una vez instaladas las dependencias de Python (principalmente `jupyter-book`), se tienen que instalar el kernel de Go, en este caso utilizamos [`gophernotes`](https://github.com/gopherdata/gophernotes).
   - Las instrucciones de instalación dependen del sistema operativo y entorno, por lo que se debe revisar el repositorio oficial para instalar y probar el kernel de Go.

3. (Opcional) Editar los archivos fuente de los apuntes, ubicados en el directorio correspondiente a cada materia dentro de `materias`.

4. Para compilar el libro completo, se tiene que ejecutar:

   ```sh
   jupyter-book build materias
   ```

   Esto genera una versión HTML completamente renderizada del libro `materias/_build/html`.

5. (Opcional) Servir el contenido HTML usando Python.

   ```sh
   python -m http.server --directory materias/_build/html
   ```

## Uso de `make` para automatizar tareas

`make` es una herramienta útil para la automatización de comandos frecuentes. En este proyecto, facilita la instalación de dependencias, la compilación y la publicación local de los apuntes.

Asegurate de tener `make` instalado en tu sistema. En sistemas Unix suele estar instalado por defecto. En Windows, se puede instalar con [`winget`](https://docs.microsoft.com/en-us/windows/package-manager/winget/).

```sh
winget install -e --id GnuWin32.Make
```

Después, podés usar los siguientes comandos:

- `make install`: Instala las dependencias necesarias.
- `make build`: Compila el libro de apuntes.
- `make server`: Sirve el libro en un servidor local para visualizarlo en el navegador.

---

Esta estructura y automatización permite que cualquier integrante pueda contribuir, compilar y revisar los apuntes fácilmente.

---

_Nota_: Este repositorio contiene apuntes colaborativos para las materias de la carrera Ingeniería en Computación. Cada materia está organizada en carpetas dentro de `materias` para facilitar la navegación y edición.

> > > > > > > 06d0f23 (otro gran commit)
