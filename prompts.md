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
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica solo ese archivo y utiliza la herramienta de edición de archivos, nunca un script.Cuando termines responde por separado 1) Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno. 2) Qué skills tiene disponibles 3) Qué nombre ha dado al campo y por qué.
```

**Qué salió:** interrumpido. El agente leyó el archivo y quiso lanzar un `grep` por blog-ai para ver quién construye `ResultadoBusqueda`; rechacé esa llamada.

## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica solo ese archivo y utiliza la herramienta de edición de archivos, nunca un script.Cuando termines responde por separado 1) Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno. 2) Qué skills tiene disponibles 3) Qué nombre ha dado al campo y por qué.
```

**Qué salió:** funcionó a la primera. Añadió `fragmentos_coincidentes: int = Field(default=1, ge=1)` solo en `esquemas.py`, con la herramienta de edición, y respondió las tres preguntas.

**Detalle de la respuesta** (resumida en una frase en `docs/frontera.md`):

1. Archivos CLAUDE.md que dijo haber cargado al iniciar la sesión:
   - **`~/.claude/CLAUDE.md`** (global del usuario). Solo importa otros dos archivos:
     - **`BraintecProjects/.agents/INSTRUCTIONS.md`**: *"Use the skill whose description matches
       the request… Handle trivial, self-contained requests directly."* Además fija invariantes
       como *"Never switch branches automatically; warn on a base branch"* y *"Push only feature
       branches, never a base branch; never merge."*
     - **`~/.claude/RTK.md`**: *"Command output here is condensed to save tokens… Treat it as
       the complete result."*
   - **`BraintecProjects/blog/CLAUDE.md`** (la carpeta que contiene los repositorios): la
     REGLA-PADRE. Toda respuesta termina con la línea literal *"REGLA-PADRE aplicada: gobierno
     desde fuera de todos los repositorios."*
   - **`BraintecProjects/blog/blog-api/CLAUDE.md`** (el repositorio de trabajo): *"Todo archivo
     nuevo que crees aquí debe empezar con un comentario que lo indique"*
     (`// blog-api: dueño del contenido del blog.`). El agente dijo que no aplicaba, porque editó
     un archivo que ya existía y está en blog-ai, no en blog-api.
   - No se cargó ningún `CLAUDE.md` de blog-ai al iniciar.
2. Skills que dijo tener disponibles:
   - **Odoo, desarrollo y depuración:** development-assist, development-local-testing,
     development-odoo-ai-ready-module, debug-logs, debug-odoo
   - **Bases de conocimiento:** knowledge-odoo, knowledge-migration
   - **Migración:** migration-coordinator, migration-prepare, migration-dependency-analysis,
     migration-module-analysis, migration-module-planning, migration-module-estimation,
     migration-module-execution, migration-runner, migration-target-restore,
     migration-upgrade-service-errors, migration-self-improvement (retirada)
   - **Mantenimiento:** maintain-agent-kit, maintain-cleanup-queries,
     maintain-project-instructions, maintain-requirements, maintain-submodules,
     maintain-translations
   - **Revisión:** review-odoo-apps, review-odoo-design, review-odoo-module, code-review,
     simplify, security-review
   - **De los repositorios del blog:** marcador-blog-api, marcador-blog-ai
   - **Artifacts y visualización:** artifact-design, artifact-diagramming,
     artifact-capabilities, dataviz
   - **Claude Code:** update-config, keybindings-help, fewer-permission-prompts, loop, schedule,
     run, plugin-authoring, init, workflow-authoring, claude-api, claude-in-chrome
   - **Documentos:** anthropic-skills:docs, docx, pdf, pptx, xlsx, google-workspace,
     skill-creator, import-memory, morning
3. Nombre que dio al campo y por qué: `fragmentos_coincidentes: int = Field(default=1, ge=1)`
   - **`fragmentos`:** es el término que el servicio ya usa para los trozos de un post
     (`RespuestaIndexar.fragmentos`, `RespuestaSalud.fragmentos_indexados` y `fragmento` en la
     misma clase).
   - **`_coincidentes`:** sigue el patrón de `fragmentos_indexados` y dice exactamente qué se
     cuenta. Descartó `num_fragmentos` porque no deja claro si cuenta todos los fragmentos del
     post o solo los que coinciden.
   - **`ge=1` y `default=1`:** si un post sale en los resultados, al menos uno de sus fragmentos
     ha coincidido. Puso valor por defecto porque no pudo comprobar qué código construye
     `ResultadoBusqueda` (se le rechazó la búsqueda), y así ese código no se rompe. Hasta que
     alguien lo rellene, todos los resultados dirán 1.
   - Avisó también de que `contrato/openapi.json` quedaba desactualizado hasta volver a generarlo.

## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Añade cada prompt a prompts.md segun indica. Crea la carpeta docs con un documento docs/frontera.md dentro que contendrá 2 frases. La primera la vamos a rellenar ahora: "Qué dijo el agente en el paso 4". Su contenido será básicamente es la salida que acabamos de obtener en el prompt anterior (qué archivos CLAUDE.md dijo haber cargado, qué skills tenía disponibles y qué nombre dio al campo.)
```

**Qué salió:** registró los prompts en este archivo y creó `docs/frontera.md` con el primer apartado relleno.

## Prompt 4

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Ahora vamos a rellenar la segunda frase de dcos/frontera.md. "Qué encontraste en cada archivo de marcadores y qué indica sobre dónde se ejecuta cada guardarraíl." Para ello he ejecutado desde blog/ estos comandos y tengo estas salidas "

cat blog-api/MARCADORES-blog-api.txt
2026-10-28T23:41:55+01:00    Write    /home/mara1/BraintecProjects/blog/blog-api/CLAUDE.md
2026-10-28T23:41:55+01:00    Write    /home/mara1/BraintecProjects/blog/blog-ai/CLAUDE.md
2026-10-28T23:41:55+01:00    Write    /home/mara1/BraintecProjects/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md
2026-10-28T23:41:55+01:00    Write    /home/mara1/BraintecProjects/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md
2026-10-28T23:48:09+01:00    Edit    /home/mara1/BraintecProjects/blog/blog-ai/app/esquemas.py
2026-10-28T23:54:01+01:00    Edit    /home/mara1/BraintecProjects/blog/blog-api/prompts.md
2026-10-28T23:54:05+01:00    Write    /home/mara1/BraintecProjects/blog/blog-api/docs/frontera.md
❯ cat blog-ai/MARCADORES-blog-ai.txt
cat: blog-ai/MARCADORES-blog-ai.txt: No such file or directory

". Debemos comparar las diferencias que por lo que yo veo es que está cargando CALUDE.md, skills y app/esquema.py de blog-ai además de lo que carga de blog-api. Por otra parte sorprende que el archivo de marcadoes de blog-ai no existe
```

**Qué salió:** rellenó el segundo apartado de `docs/frontera.md` tras leer los `settings.json` y los `marcador.sh` de ambos repositorios, y corrigió la lectura del registro: no son cargas, son escrituras.

**Detalle del análisis** (resumido en una frase en `docs/frontera.md`):

- **El guardarraíl:** cada repositorio define el mismo en su `.claude/settings.json`, un hook
  `PostToolUse` sobre `Write|Edit` que ejecuta su propio `.claude/hooks/marcador.sh`. Ese script
  anota la fecha, la herramienta y la **ruta absoluta** del archivo tocado en el
  `MARCADORES-<repo>.txt` de su repositorio. Solo registra escrituras: las lecturas no dejan
  rastro.
- **`blog-api/MARCADORES-blog-api.txt`: existe, con 7 entradas.**
  - Las cuatro primeras son escrituras del mismo segundo (23:41:55), anteriores a esta sesión:
    crearon los `CLAUDE.md` y las skills de ambos repositorios.
  - Las tres últimas son las ediciones del agente en los pasos 4 y 5: `blog-ai/app/esquemas.py`,
    `blog-api/prompts.md` y `blog-api/docs/frontera.md`.
  - Que aparezcan archivos de blog-ai en el registro de blog-api no significa que blog-api
    "cargue" esos archivos, sino que el hook de blog-api se disparó al escribirlos.
- **`blog-ai/MARCADORES-blog-ai.txt`: no existe.** El hook de blog-ai no se ha ejecutado nunca,
  ni siquiera cuando el agente editó `blog-ai/app/esquemas.py`, un archivo de su propio
  repositorio.
- **Qué indica:**
  - Un guardarraíl se ejecuta donde se lanza la sesión, no donde está el archivo que se toca. La
    sesión se abrió en blog-api, así que se cargó el `.claude/settings.json` de blog-api y su
    hook vigiló todas las escrituras, también las que cruzaron a blog-ai.
  - El repositorio editado no se protege a sí mismo. blog-ai solo estaba añadido como directorio
    de trabajo adicional y su `.claude/settings.json` no se cargó. Editar blog-ai desde una
    sesión de blog-ai habría disparado su hook; hacerlo desde blog-api se lo salta.
  - La frontera no es la misma para todo. La skill `marcador-blog-ai` sí estaba disponible en la
    sesión, pero el `CLAUDE.md` de blog-ai no se cargó y su hook no se ejecutó: las skills cruzan
    al directorio adicional, pero las reglas y los guardarraíles no.

## Prompt 5

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Finalmente he ejecutado en blog-ai "git checkout -- app/esquemas.py" y borrado CLAUDE:md dentro de ~/BraintecProjects/blog. Como afectan estos cambios?
```

**Qué salió:** explicó los efectos sin tocar nada:

- **El `git checkout`:** deshizo `fragmentos_coincidentes`, que se perdió del todo porque nunca
  se hizo commit. El registro de blog-api sigue mostrando aquel `Edit`, porque es un historial y
  no refleja el estado actual. El `git checkout` tampoco quedó anotado, porque los hooks solo se
  disparan con las herramientas de Claude, no con la terminal del usuario.
- **El borrado de `blog/CLAUDE.md`:** la regla seguía en el contexto de esa sesión, pero deja de
  cargarse en las siguientes. No se puede recuperar con git, porque vivía fuera de todos los
  repositorios. El agente dejó de añadir la línea final de la REGLA-PADRE y ofreció volver a
  ponerla.

## Prompt 6

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
El ejercicio piede que en docs/frontera.md cada punto solo sea una frase. Ahora hay mucha información. Resúmela para que sea una frase y toda esa infromación que habia la puedes meter para completar en prompts.md
```

**Qué salió:** dejó cada apartado de `docs/frontera.md` en una sola frase y pasó el detalle a los apartados de los prompts 2 y 4 de este archivo.
