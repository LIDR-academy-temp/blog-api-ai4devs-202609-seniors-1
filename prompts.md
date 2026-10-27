# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

## Cómo rellenarlo

- Un apartado `## Prompt N` por cada prompt.
- **Pega el prompt tal cual lo lanzaste**, dentro del bloque de código, aunque ocupe diez líneas
  y aunque tenga faltas. No lo reescribas para que quede bien: el que arreglaste mentalmente
  después no es el que lanzaste.
- Incluye también los que **no funcionaron**. Suelen ser los más útiles de leer.
- `Modelo` y `Herramienta` en todos. Si cambiaste de una a otra a mitad, se nota aquí.

Borra el ejemplo de abajo cuando escribas el primero.

---

## Prompt 1

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea un CLAUDE.md en este proyecto que indique que "este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique"
```

**Qué salió:** Lo hizo e indico que por su cuenta habia añadido ejemplos del comentario para diferentes lenguajes. Tambien que habia visto ahora el CLAUDE.md del directorio padre

## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea un CLAUDE.md en el proyecto y carpeta ../blog-ai que indique que "los nombres de los campos del contrato público deben escribirse en español, nunca en inglés
```

**Qué salió:** Indica que el contrato actual ya incumple la regla: post_id y slug (en el esquema Fuente) son nombres en inglés. Tambien que el archivo no lleva el comentario de propiedad de blog-api, porque esa regla es solo para los archivos de ese repositorio. E indica "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios"

## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
En este proyecto, crea un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-blog-api.txt, en la raíz del repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Usa rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio

```

**Qué salió:** Indica que creo el hook escribiendo en .claude/settings.json y en .claude/hooks/registrar-marcador.sh, que hizo una prueba y borro el fichero para que empiece vacio, y añadio "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios"

## Prompt 4

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
En el proyecto y carpeta ../blog-ai, crea un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-blog-ai.txt, en la raíz del repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Usa rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio

```

**Qué salió:** Indica que creo el hook escribiendo en .claude/settings.json y en .claude/hooks/registrar-marcador.sh, que hizo una prueba y borro el fichero para que empiece vacio, y añadio "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios". Indica ademas que el hook de blog-ai no funciona desde esta sesión porque la sesion arranco blog-api

## Prompt 5

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
En este proyecto, crea una skill sencilla llamada marcador-blog-api que simplemente indique en que proyecto se está ejecutando

```

**Qué salió:** Indico que creo la skill, y "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.". Tambien que por la regla de blog-api/CLAUDE.md, el archivo lleva el comentario de propiedad

## Prompt 6

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
En el proyecto y carpeta ../blog-ai, crea una skill sencilla llamada marcador-blog-ai que simplemente indique en que proyecto se está ejecutando y adicionalmente indique la fecha

```

**Qué salió:** Indico que creo la skill, y "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.". Tambien que no lleva el comentario de propiedad, porque esa regla es solo de blog-api


## Prompt 7

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica unicamente ese archivo y utiliza la herramienta de edición de archivos, nunca un script

```

**Qué salió:** Indica que lo realizo, y adicionalmente "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios."

## Prompt 8

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Indicame qué archivos CLAUDE.md se cargaron al iniciar la sesión, y cita la regla de cada uno

```

**Qué salió:** Indica la respuesta copiada a docs/frontera.md


## Prompt 9

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Que skills tienes disponibles

```

**Qué salió:** Indica la respuesta copiada a docs/frontera.md

## Prompt 10

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Que nombre diste al campo que te pedi añadir a la clase ResultadoBusqueda y por que

```

**Qué salió:** Indica la respuesta copiada a docs/frontera.md




