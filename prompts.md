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

**Modelo:** Opus 5.5 (claude-opus-5-5)
**Herramienta:** Claude Code v2.1.312

```
Estoy en el repo blog-api y quiero dejar preparados los guardarraíles de este repo y del hermano ../blog-ai. Haz solo esto, y nada más en ninguno de los dos:

1. Un CLAUDE.md en la raíz de cada repo con UNA sola regla, propia de ese repo:
   - blog-api: este repo es el dueño del contenido, y todo archivo nuevo que se cree aquí debe empezar con un comentario que lo indique.
   - blog-ai: los nombres de los campos del contrato público se escriben en español, nunca en inglés.
2. En cada repo, un hook de Claude Code que se ejecute con PostToolUse cuando se use Write o Edit, y que añada una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repo, con la fecha, la herramienta usada y la ruta del archivo modificado. Usa rutas absolutas: el hook tendrá que registrar archivos que estén fuera de su repo.
3. En cada repo, una skill sencilla llamada marcador-<nombre-del-repo> (marcador-blog-api, marcador-blog-ai) cuya descripción diga a qué repo pertenece.

No hagas commit, ni rama, ni PR, y no toques código de la aplicación. Si algo no está claro, pregúntamelo. Cuando termines, dime las rutas de cada archivo que has creado.
```

**Qué salió:** Funcionó a la primera, con una sola pregunta del agente: si el comentario de «dueño del contenido» debía ir también en los archivos que iba a crear; elegí la opción «Donde se pueda» (no hubo ningún otro mensaje mío). Creó en `blog-api` y en `blog-ai` un `CLAUDE.md` con su regla, un hook `PostToolUse` (`Write|Edit`, script `.claude/hooks/marcador.py` con ruta absoluta) y una skill `marcador-<repo>`. Cerró la respuesta con la línea de `REGLA-PADRE`. Al terminar, `MARCADORES-blog-api.txt` ya tenía 3 líneas (las escribió el hook, no el agente) y `blog-ai` no tenía archivo de marcadores. Además, el agente dijo que cada hook solo se ejecuta en una sesión abierta en su propio repo; eso es lo que dijo, no lo he comprobado.

## Prompt 2

**Modelo:** Opus 5.5 (claude-opus-5-5)
**Herramienta:** Claude Code v2.1.312 (sesión nueva con `claude --add-dir ../blog-ai`; **ojo: la sesión estuvo en modo auto**, no en manual como pide la lección; el agente sí usó la herramienta `Edit`)

```
En ../blog-ai/app/esquemas.py, añade a la clase ResultadoBusqueda un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica solo ese archivo y usa la herramienta de edición de archivos, nunca un script de shell. No hagas commit.

Cuando termines, respóndeme por separado a estas tres preguntas, sin mezclarlas:
1. Qué archivos CLAUDE.md se cargaron al iniciar esta sesión; cita la regla de cada uno.
2. Qué skills tienes disponibles.
3. Qué nombre le has dado al campo y por qué.
```

**Qué salió:** Editó `../blog-ai/app/esquemas.py` con la herramienta `Edit` y añadió `fragmentos_coincidentes: int = Field(default=1, ge=1)` a `ResultadoBusqueda`, sin tocar más archivos ni hacer commit. Dijo que se cargaron el `CLAUDE.md` de `blog/` y el de `blog-api`, y que no se cargó ninguno de `blog-ai`; citó las skills `marcador-blog-api` y `marcador-blog-ai` entre muchas otras; y justificó el nombre por seguir el vocabulario en español del archivo. Cerró con la línea de `REGLA-PADRE`. En los marcadores, `MARCADORES-blog-api.txt` ganó una línea (`Edit` sobre `esquemas.py`, un archivo de `blog-ai`) y `MARCADORES-blog-ai.txt` no existe.
