# ¿Cómo colaborar?

Para colaborar con el proyecto, ya sea redactando apuntes, subiendo exámenes o archivos, se pide la utilización de pull requests.

En el repositorio, a la derecha del nombre del mismo aparecen opciones, donde se debe buscar la opción `Fork` -> `Create a new fork`. Esto crea una copia del repositorio principal. Se marca la opción `Create fork` y se creará una del repositorio en tu cuenta de GitHub.

Se realizan los cambios pertinentes en el repositorio (se recomienda hacer [cambios pequeños](https://dev.to/oculus42/make-small-commits-22cd)).

Se agrega el o los archivos cambiados.

```sh
# Agregar un archivo en particular. Recomendable para commits pequeños.
git add archivo_cambiado.extensión

# Agregar todos los archivos editados.
git add .
```

- Se crea un commit con un mensaje claro del cambio.

```sh
git commit -m "cambio X en X lugar"
```

- Se sube el cambio al repositorio copiado.

```sh
git push
```

Nuevamente en el repositorio copiado, debería aparecer la opción `Contribute`, en la cual se abrirá la opción `Open pull request`.

Dentro de la página se agrega un título y también se puede agregar una descripción, se pide ser lo más explícito de los cambios hechos para poder aceptar el _pull request_. Luego se selecciona la opción `Create pull request`.
