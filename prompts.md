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
Crea un fichero Claude.md en los directorios blog-api y blog-ai. Con solo un regla que para cada directorio es la siguente:





En blog-api: este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique. 



En blog-ai: los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. Las reglas son distintas para poder reconocer después cuál se aplicó.

Guarda este prompt en prompts.md
```

## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea en cada uno de estos directorios blog-api y blog-ai:

Un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Pide que use rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio.

Guarda este prompt en prompts.md
```

## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea en cada uno de estos directorios blog-api y blog-ai:

Una skill sencilla llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece.

Guarda este prompt en prompts.md
```

## Prompt 4

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Añada a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Solo se debe modificar ese archivo y utilizar la herramienta de edición de archivos, nunca un script.

Guarda este prompt en prompts.md
```

## Prompt 5

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno. Guarda este prompt en prompts.md
```

## Prompt 6

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Qué skills tienes disponibles. Guarda este prompt en prompts.md
```

## Prompt 7

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Qué nombre has dado al campo y por qué. Guarda este prompt en prompts.md
```
