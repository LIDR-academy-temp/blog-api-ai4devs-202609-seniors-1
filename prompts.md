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

**Modelo:** Opus 5.5 Max
**Herramienta:** Claude Code

```
Create these 3 files for for both this project and  `blog-ai`; you can find `blog-ai` project in the same level as `blog-api`.

Create a CLAUDE.md file 
The CLAUDE.md file will be located at the project's root folder and contain a single rule, which is unique to each repo

* blog-api: Este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique
* blog-ai: Los nombres de los campos del contrato público deben escribirse en español, nunca en inglés


Create a hook that will execute whenever a file is written or modified, via `PostToolUse` for `Write` and `Edit` tools. It must add a line to `MARCADORES-<repo-name>.txt`, at the root of its own repo, with date, used tool and absolute path to modified file.

Create simple skill called `marcador-<repo-name>` which description indicates to what repository it belongs to.
```

**Qué salió:** Funcionó sin bloqueos: CLAUDE.md con su regla, hook PostToolUse para Write|Edit (script con jq que anota fecha, herramienta y ruta absoluta en MARCADORES-<repo>.txt) y skill marcador-<repo> en blog-api y blog-ai; el hook se probó con payloads de prueba sobre una copia y el de blog-api además se disparó en vivo en esta sesión al editar prompts.md, y los archivos nuevos de blog-api no llevan el comentario de propiedad porque la regla aún no regía en esta sesión y el prompt no lo pedía.

## Prompt 2

**Modelo:** Opus 5.5 Max
**Herramienta:** Claude Code

```
Add a field to the `ResultadoBusqueda` class, located in `../blog-ai/app/esquemas.py`, to indicate how many article fragments matched the search.
You should modify ONLY that file and use the file edition tool, never a script
```

**Qué salió:** Funcionó dentro del límite pedido: Claude añadió fragmentos_coincidentes (int | None = None) a ResultadoBusqueda editando solo esquemas.py con Edit; lo nombró en español por la regla de blog-ai, que no se cargó al iniciar la sesión y que encontró leyendo ese repo a mano; lo dejó opcional porque indice.buscar, que no se podía tocar, no lo rellena; el contrato versionado quedó desactualizado (--verificar falla); el hook de blog-ai no se disparó y la edición la anotó el de blog-api; y este Qué salió quedó pendiente un turno para respetar «solo ese archivo».

## Prompt 3

**Modelo:** Opus 5.5 Max
**Herramienta:** Claude Code

```
answer individually:

* which `CLAUDE.md` files were loaded upon session init? Quote each one's rule
* What skills are available?
* What name did you assign to the new field and why?
```

**Qué salió:** Respondió las tres preguntas: al iniciar se cargaron el CLAUDE.md global de Rodrigo, el de la carpeta padre (REGLA-PADRE) y el de blog-api, pero no el de blog-ai; entre las skills sí está marcador-blog-ai (además de marcador-blog-api, prompt-recorder y las integradas), así que del otro repo cruzaron las skills pero no su CLAUDE.md ni su hook; y explicó el nombre fragmentos_coincidentes por la regla de español de blog-ai y el patrón de fragmentos_indexados. Además rellenó el Qué salió pendiente del Prompt 2.

## Prompt 4

**Modelo:** Opus 5.5 Max
**Herramienta:** Claude Code

```
I created a file name `frontera.md`; you can find it here: /Users/Rodrigo/Documents/blog/blog-api/docs/frontera.md
for first question, answer with a summary of the 3 points of your last answer
for the second question, answer this: "en este punto de la práctica, veo 5 entradas en `/blog-api/MARCADORES-blog-api.txt`; 4 son ediciones del archivo prompts.md y la quinta la edición de `esquemas.py`; no existe el archivo `/blog-ai/MARCADORES-blog-ai.txt`"

at this point, stop the prompt recorder skill
this is the last bit before opening the PR for the module 7 exercise, so feel free to tune it as needed, but lets keep it human-sounding
```

**Qué salió:** Claude rellenó las dos respuestas de docs/frontera.md: la primera resume el paso 4 y la segunda se basa en el texto dado, corrigiendo «la quinta» (la entrada de esquemas.py es la tercera de cinco) y añadiendo lo que indica: los guardarraíles corren en el repo donde arranca la sesión, así que blog-ai queda sin vigilancia; además puso al principio el comentario de propiedad que pide la regla de blog-api para archivos nuevos y paró el prompt-recorder renombrando su archivo label en .git, porque el script no trae orden para detenerlo.
