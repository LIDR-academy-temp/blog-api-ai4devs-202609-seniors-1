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

---

## Prompt 1

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
resumir que hace el proyecto
```

**Qué salió:** resumen del proyecto y del ejercicio a partir del README, las rutas y el contrato.

## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea en el repositorio de blog-api (/home/hpadmin/dev/ai4devs/blog/blog-api) los siguientes archivos:

1. Un CLAUDE.md en la raíz con una sola regla: este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique. 

2. Un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Usá rutas absolutas. Registrá los cambios en archivos situados fuera de tu repositorio.

3. Una skill llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece.

y en el repositorio de blog-ai (/home/hpadmin/dev/ai4devs/blog/blog-ai) los siguientes archivos:
1. CLAUDE.md en la raiz, con una regla que sea que los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. 

2. Un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Usá rutas absolutas. Registrá los cambios en archivos situados fuera de tu repositorio.

3. Una skill llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece.

Guardá cada prompt en el archivo prompts.md en la raiz de este proyecto
```

**Qué salió:** creó CLAUDE.md, .claude/settings.json con el hook, el script .claude/hooks/marcador.py y la skill en los dos repositorios.

## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
No uses el modo de aceptación automática. No edites mediante scripts de shell. El hook de esta práctica solo registra las herramientas Write y Edit.
```

**Qué salió:** confirmó que editaría solo con Write y Edit, sin scripts de shell, y pidiendo confirmación en vez de aceptar cambios automáticamente.

## Prompt 4

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
guardá todos los prompts en el archivo raiz prompts.md, añadiendo al final para mantener el orden
```

**Qué salió:** añadió los prompts 3 y 4 al final de prompts.md con la herramienta Edit.

## Prompt 5

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Añadí a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modificá solo ese archivo y utilizar la herramienta de edición de archivos, nunca un script.
```

**Qué salió:** añadió `fragmentos_coincidentes: int = Field(default=1, ge=1)` con Edit. Avisó de que `indice.py` todavía no lo calcula y de que hay que regenerar `contrato/openapi.json`.

## Prompt 6

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Por ahora, no hagas nada. No es el objetivo del ejercicio. Responde por separado cada una de las siguientes preguntas:

1.    Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de uno cada?

2.    Qué skills tiene disponibles?

3.    Qué nombre ha dado al campo y por qué?
```

**Qué salió:** dijo que se cargaron el CLAUDE.md de la carpeta padre y el de blog-api, pero no el de blog-ai (lo leyó con Read). Listó las skills y explicó el nombre `fragmentos_coincidentes`.

## Prompt 7

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crear el archivo docs/frontera.md que contenga lo siguiente:

1. Qué dijo el agente en el paso 4: qué archivos CLAUDE.md dijo haber cargado (a), qué skills disponibles tenía (b) y qué nombre dio al campo (c).
a. Archivos CLAUDE.md cargados al iniciar la sesión
Se cargaron dos:
- /home/hpadmin/dev/ai4devs/blog/CLAUDE.md: está en la carpeta que contiene los repositorios, fuera de todos ellos. Claude Code lo cargó porque al arrancar lee los CLAUDE.md de las carpetas superiores. Su regla:
▎ toda respuesta que des aquí termina con esta línea, sola y literal: REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
- /home/hpadmin/dev/ai4devs/blog/blog-api/CLAUDE.md: el del repositorio donde arrancó la sesión. Su regla:
▎ Este repositorio es el dueño del contenido del blog. Todo archivo nuevo debe empezar con un comentario que lo indique
El de blog-ai (/home/hpadmin/dev/ai4devs/blog/blog-ai/CLAUDE.md) no se cargó al inicio, aunque blog-ai estaba agregado como carpeta de trabajo adicional. Lo abrí yo con Read antes de modificar esquemas.py. Su regla:
▎ Los nombres de los campos del contrato público […] se escriben en español, nunca en inglés

b. Skills disponibles
- Del ejercicio: marcador-blog-api y marcador-blog-ai. Cada una muestra el archivo MARCADORES-<repo>.txt de su repositorio.
- De Claude Code: update-config, keybindings-help, code-review, simplify, fewer-permission-prompts, loop, schedule, claude-api, claude-in-chrome, run, plugin-authoring, init, security-review y dataviz.
- De Anthropic (anthropic-skills:): built-in-browser, chrome-browser, computer-use, deep-research, docs, docx, import-memory, morning, pdf, pptx, setup-writing-style, skill-creator y xlsx.

c. Nombre del campo y por qué
Lo llamó fragmentos_coincidentes, por tres razones:
- Español: el CLAUDE.md de blog-ai pide que los campos del contrato público estén en español, y ResultadoBusqueda forma parte de ese contrato. Por eso no usé, por ejemplo, match_count.
- Las palabras del pedido: pediste «cuántos fragmentos del artículo han coincidido».
- El estilo del archivo: sigue el formato que ya usan otros campos, como fragmentos_indexados y motivos_omision. Además, «fragmento» es el término que usan el esquema y la tabla fragmentos de la base de datos.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.


2. Qué encontraste en cada archivo de marcadores (a) y qué indica sobre dónde se ejecuta cada guardarraíl (b).
a. 
En MARCADORES-blog-api.txt:
2026-10-28T07:55:31-03:00    Edit    /home/hpadmin/dev/ai4devs/blog/blog-api/prompts.md
2026-10-28T07:58:15-03:00    Edit    /home/hpadmin/dev/ai4devs/blog/blog-ai/app/esquemas.py

En MARCADORES-blog-ai.txt
-- No creó el archivo --

b. Está bien que MARCADORES-blog-ai.txt esté vacío porque el que está ejecutando es blog-api. Las Skills no se disparan en blog-ai, que son las que escriben el archivo. El funcionamiento es el esperado 
```

**Qué salió:** creó `docs/frontera.md` en blog-api con Write, empezando con el comentario de propiedad que pide el CLAUDE.md de blog-api, y añadió los prompts 5 a 7 aquí.
