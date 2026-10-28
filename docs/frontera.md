<!-- Este archivo pertenece a blog-api, el repositorio dueño del contenido. -->

1. Qué dijo el agente en el paso 4: qué archivos CLAUDE.md dijo haber cargado, qué skills tenía disponibles y qué nombre dio al campo.

   - **CLAUDE.md:** dijo haber cargado tres al iniciar la sesión: el global (`~/.claude/CLAUDE.md`, mi guía de estilo personal), el de la carpeta padre (`blog/CLAUDE.md`, el de la REGLA-PADRE) y el de `blog-api`. El de `blog-ai` no se cargó; el agente solo lo vio porque fue a leerlo por su cuenta antes de editar `esquemas.py`.
   - **Skills:** `marcador-blog-api`, `marcador-blog-ai`, mi `prompt-recorder` y las que trae Claude Code de serie (navegador, documentos, `code-review`, etc.). Curiosamente, la skill de `blog-ai` sí estaba disponible, aunque su CLAUDE.md y su hook no.
   - **Nombre del campo:** `fragmentos_coincidentes`. Lo puso en español por la regla de `blog-ai` (los campos del contrato público van en español), aunque yo se lo había pedido en inglés, y siguiendo el patrón de `fragmentos_indexados`.

2. Qué encontraste en cada archivo de marcadores y qué indica sobre dónde se ejecuta cada guardarraíl.

   Al acabar el paso 4 veo cinco entradas en `blog-api/MARCADORES-blog-api.txt`: cuatro son ediciones de `prompts.md` y la otra es la de `esquemas.py`, que es un archivo de `blog-ai`. `blog-ai/MARCADORES-blog-ai.txt` ni siquiera existe.

   Eso indica que los guardarraíles se ejecutan en el repositorio donde arranca la sesión, no en el del archivo que se toca. El hook de `blog-api` anota cada Write o Edit de la sesión, aunque el archivo sea de `blog-ai`, y el de `blog-ai` no llega a cargarse; con su CLAUDE.md pasa lo mismo. Trabajando desde `blog-api`, la frontera con `blog-ai` queda sin vigilancia.
