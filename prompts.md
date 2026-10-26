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

**Modelo:** Sonnet High
**Herramienta:** Claude Code

```
Necesito preparar la configuración del agente en dos repositorios hermanos: el actual (/home/javier/workspace/ai4devs/ejercicios/blog/blog-api) y blog-ai (/home/javier/workspace/ai4devs/ejercicios/blog/blog-ai). Crea lo mismo en ambos, y no cambies ninguna otra cosa ni hagas commit.

1. Un CLAUDE.md en la raíz de cada repositorio, con una sola regla propia de ese repositorio:
   - blog-api: "Este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique."
   - blog-ai: "Los nombres de los campos del contrato público deben escribirse en español, nunca en inglés."

2. Un hook en .claude/settings.json de cada repositorio, de tipo PostToolUse para las herramientas Write y Edit. Cada vez que se ejecute debe añadir una línea al archivo MARCADORES-<nombre-del-repo>.txt (MARCADORES-blog-api.txt y MARCADORES-blog-ai.txt), en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Usa rutas absolutas, tanto para el archivo de marcadores como para la ruta que se registra: el hook tendrá que anotar cambios en archivos que están fuera de su    repositorio. El hook recibe los datos de la herramienta por la entrada estándar en JSON (puedes usar jq, que está instalado). Valida solo que el JSON de settings.json es correcto; no ejecutes el hook ni crees a mano ningún archivo MARCADORES, porque no quiero que contengan líneas de prueba.

3. Una skill sencilla en .claude/skills/ de cada repositorio, llamada marcador-<nombre-del-repo> (marcador-blog-api y marcador-blog-ai), con un SKILL.md cuya descripción indique a qué repositorio pertenece.

Cuando termines, dime en una lista qué archivos has creado, con su ruta completa.
```

**Qué salió:** 
Creé los seis archivos y validé que los dos settings.json son JSON correcto. No hice commit ni toqué nada más.

blog-api
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-api/CLAUDE.md
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-api/.claude/settings.json
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md

blog-ai
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-ai/CLAUDE.md
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-ai/.claude/settings.json
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md

Cada hook añade una línea con el formato fecha | herramienta | ruta absoluta. Usa jq y escribe en el MARCADORES-<repo>.txt de su propio repositorio, con la ruta absoluta.

- Hook activado sin querer: el hook de blog-api se activó solo mientras yo escribía los demás archivos, porque Claude Code recarga los ajustes en caliente. Generó MARCADORES-blog-api.txt con tres líneas, una de ellas sobre un archivo de blog-ai. Eran líneas de mi propia configuración, así que borré ese archivo con rm. Ahora ningún MARCADORES-*.txt existe y git status solo muestra .claude/ y CLAUDE.md como nuevos. El hook sigue activo, así que el archivo aparecerá en cuanto se use Write o Edit en esta sesión.
- Comentario inicial: la regla de blog-api exige que todo archivo nuevo empiece con un comentario que indique que el repositorio es el dueño del contenido. No lo añadí a estos archivos porque pediste textos concretos, y un comentario en settings.json lo invalidaría.
- .gitignore: no añadí los MARCADORES-*.txt a ningún .gitignore, porque pediste no cambiar nada más. Aparecerán como archivos sin seguimiento.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

---

## Prompt 2

**Modelo:** Sonnet High
**Herramienta:** Claude Code

```
En el repositorio /home/javier/workspace/ai4devs/ejercicios/blog/blog-ai, en el archivo app/esquemas.py, añade a la clase ResultadoBusqueda un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda.

Modifica solo ese archivo y usa la herramienta de edición de archivos; no uses un script ni comandos de shell para escribir.
```

**Qué salió:** 
Añadí a ResultadoBusqueda el campo fragmentos_coincidentes: int = Field(default=1, ge=1) en app/esquemas.py, con un comentario breve. No ejecuté nada para comprobarlo.

- Valor por defecto: puse 1. Si un post sale en los resultados, al menos un fragmento coincidió. Así el código que construye ResultadoBusqueda sigue funcionando sin cambios, ya que solo toqué este archivo.
- Cálculo real pendiente: hasta que el código de búsqueda cuente los fragmentos por post y pase el número, el campo valdrá siempre 1.
- Contrato: el campo cambia el esquema de /openapi.json. Hay que regenerar contrato/openapi.json, que es la versión guardada en el repositorio y la que consume blog-api. Es un cambio compatible, porque solo añade un campo a la respuesta.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

---

## Prompt 3

**Modelo:** Sonnet High
**Herramienta:** Claude Code

```
Respóndeme por separado a estas tres preguntas:
1. Qué archivos CLAUDE.md se cargaron al iniciar esta sesión, citando la regla de cada uno.
2. Qué skills tienes disponibles.
3. Qué nombre has dado al campo y por qué.

```

**Qué salió:** 
1. Archivos CLAUDE.md cargados al iniciar

Se cargaron dos:

- /home/javier/workspace/ai4devs/ejercicios/blog/CLAUDE.md, de la carpeta que contiene los repositorios. Su regla es la REGLA-PADRE: "toda respuesta que des aquí termina con esta línea, sola y literal: REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios."
- /home/javier/workspace/ai4devs/ejercicios/blog/blog-api/CLAUDE.md, del repositorio de trabajo. Su regla es: "Este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique."

No se cargó ningún CLAUDE.md de blog-ai. Ese directorio está como directorio adicional, y no consta que tenga uno. La segunda regla pertenece a blog-api y no aplicaba a mi edición: modifiqué un archivo existente de blog-ai, no creé ninguno.

2. Skills disponibles

- Producto y discovery:
  - arbol-oportunidad-solucion
  - crear-historias-de-usuario
  - division-de-historias-usuario
  - mapa-de-historias-usuario
  - mapa-viaje-cliente
  - crear-lean-canvas
  - crear-spec-sdd
  - cuando-usar-ia-metodo-ed2a
  - validar-idea-antes-de-construir
  - priorizar-funcionalidades
  - planificacion-roadmap
  - facilitar-inception-agil
  - crear-y-revisar-okrs
- Organización y equipos: diseno-organizacional-agil, management-3-0-y-equipos-agiles.
- Específicas de los repositorios: marcador-blog-api y marcador-blog-ai, que explican los marcadores de cambios que registra el hook de cada repositorio.
- Plugin product-management: brainstorm, product-brainstorming, competitive-brief, metrics-review, roadmap-update, sprint-planning, stakeholder-update, synthesize-research y write-spec.
- Plugin cowork-plugin-management: cowork-plugin-customizer y create-cowork-plugin.
- Artifacts y visualización: artifact-design, artifact-diagramming, artifact-capabilities y dataviz.
- Herramientas de Claude Code:
  - update-config
  - keybindings-help
  - code-review
  - simplify
  - fewer-permission-prompts
  - loop
  - schedule
  - claude-api
  - claude-in-chrome
  - run
  - plugin-authoring
  - init
  - security-review
- anthropic-skills: built-in-browser, chrome-browser, computer-use, deep-research, docs, docx, google-workspace, import-memory, morning, pdf, pptx, skill-creator y xlsx.

3. Nombre del campo y por qué

Lo llamé fragmentos_coincidentes. Lo elegí por estas razones:

- Convención del archivo: los campos van en español y en snake_case (puntuacion, fragmento, motivos_omision).
- Sin ambigüedad: fragmentos solo, o total_fragmentos, se confundiría con RespuestaIndexar.fragmentos y RespuestaSalud.fragmentos_indexados, que cuentan fragmentos indexados. Este campo cuenta los que coincidieron con la búsqueda.
- Contrato: ResultadoBusqueda es el contrato que consume blog-api, así que el nombre debía describir el significado sin necesitar el comentario. Lo definí como int con ge=1 y valor por defecto 1.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

