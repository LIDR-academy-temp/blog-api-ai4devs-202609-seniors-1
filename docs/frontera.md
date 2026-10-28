Claude informó que reconoció y aplicó ~/blog/CLAUDE.md y blog-ai/CLAUDE.md, identificó la skill marcador-blog-ai junto con las skills generales y de anthropic-skills, y declaró que no había propuesto un campo para ResultadoBusqueda ni abierto los archivos relacionados.

El registro MARCADORES-blog-api.txt muestra que el hook de blog-api registró operaciones Write y Edit, incluidas modificaciones en archivos de blog-ai, mientras que MARCADORES-blog-ai.txt registra la creación de su archivo de prueba, lo que evidencia que cada hook se ejecuta según la configuración del proyecto activo y que el hook de blog-api también puede registrar ediciones realizadas fuera de su repositorio.

## Precisiones

1. MARCADORES-blog-ai.txt no contiene solo la creación del archivo de prueba: también registra, en la misma sesión, el guardado de `.claude/prompts/prueba-hook-posttooluse.md` (17:51:51) y la creación de este documento (17:57:23) en `blog-ai/docs/frontera.md`. Esa ruta ya no existe: el documento se trasladó después a `blog-api/docs/frontera.md` con `mv`, y ese traslado no quedó registrado porque los hooks solo se disparan con Write y Edit.
2. `blog-ai/contrato/openapi.json` aparecía modificado en git al comenzar la sesión de blog-ai, pero no figura en ninguno de los dos registros. Pudo modificarse con un comando de shell, en otra sesión o antes de que existieran los hooks; los registros no permiten saber cuál.
