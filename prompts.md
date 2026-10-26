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

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```
Crea en blog-api un claude-md con una sola regla de instruccion: este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique
```

**Qué salió:** Creé blog-api/CLAUDE.md con una sola regla: este repositorio es el dueño del contenido, y todo archivo nuevo debe empezar con un comentario que lo diga, escrito con la sintaxis de comentarios de su lenguaje. Incluí un ejemplo en TypeScript: // blog-api es el dueño del contenido.

## Prompt 2

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```
En el proyecto de blog-ai creame en CLAUDE.md una sola regla: os nombres de los campos del contrato público deben escribirse en español, nunca en inglés.
```

**Qué salió:** Creé blog-ai/CLAUDE.md (antes no existía) con una sola regla: los nombres de los campos del contrato público se escriben en español, nunca en inglés.

No he revisado si la carpeta contrato/ ya cumple la regla, y el archivo está sin commit.


## Prompt 3

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```

Dentro de blog-api creame un hook que se ejecute al escribir o editar un archivi: mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Con las rutas absolutas
```

**Qué salió:** He creado el hook en blog-api y probé el script a mano: escribe bien la línea. En esta sesión todavía no se ha disparado. La carpeta .claude/ no existía cuando empezó la sesión, así que Claude Code no ha cargado la configuración nueva. Abre /hooks una vez (o reinicia la sesión) para que la cargue.


## Prompt 4

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```

Dentro de blog-api creame un hook que se ejecute al escribir o editar un archivi: mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Con las rutas absolutas
```

**Qué salió:** He creado el hook en blog-api y probé el script a mano: escribe bien la línea. En esta sesión todavía no se ha disparado. La carpeta .claude/ no existía cuando empezó la sesión, así que Claude Code no ha cargado la configuración nueva. Abre /hooks una vez (o reinicia la sesión) para que la cargue.

## Prompt 5

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```
lo mismo para blog-ai
```

**Qué salió:** He creado el mismo hook en blog-ai. Lo probé a mano y escribe bien la línea en MARCADORES-blog-ai.txt:

## Prompt 5

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```
Creame una skill sencuilla para cara repositorio blog-api y blog-ai con el nombre marcadore-<nombre_del_repo> cuya descripcion indique a que repositorio pertenece
```

**Qué salió:** REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

## Prompt 6

**Modelo:** Opus 1M xHigh
**Herramienta:** Claude Code

```

Añademe a la clas ResultadoBusqueda en ../blog-ai/app/esquema.py un campo que indique cuantros fragmentos del
  articulo han coindidio con la busqueda. Solo tienes que modificar ese archivo y utilizar la herramiento de edicion
  de archivos, nunca un script. Cuando termines tienes que responderme: 1. Que archivos claude.md se cargaron al
  iniciar la sesion citando la regla de cada uno. 2- Que skills tienes disponibles. 3- Que nombre ha dado al campo y
  porque
```

**Qué salió:** Añadí el campo a ResultadoBusqueda con la herramienta Edit, sin scripts. Solo cambié ese archivo y no ejecuté nada para probarlo.





