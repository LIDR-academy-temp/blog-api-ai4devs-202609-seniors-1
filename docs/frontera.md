<!-- blog-api: dueño del contenido del blog. -->

# Frontera

## Qué dijo el agente en el paso 4

Dijo haber cargado el `CLAUDE.md` global (con las instrucciones de Braintec y RTK que son ajenas a este ejercicio pero están en mi local), 
el de la carpeta `blog/` (REGLA-PADRE) y el de blog-api (cabecera en cada archivo nuevo), pero ninguno de blog-ai; listó las skills de Braintec y de Claude Code junto con `marcador-blog-api` y `marcador-blog-ai`; y llamó al campo `fragmentos_coincidentes` para seguir la convención `fragmentos_indexados` que ya usa el servicio.

## Qué encontraste en cada archivo de marcadores y qué indica sobre dónde se ejecuta cada guardarraíl

El registro de blog-api apuntó todas las escrituras de la sesión, también las de archivos de blog-ai, mientras que el de blog-ai ni siquiera existe, lo que indica que cada guardarraíl se ejecuta según el repositorio desde el que se lanza la sesión y no según el repositorio del archivo que se toca.
