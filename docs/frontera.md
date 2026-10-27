<!-- REGLA-HIJA de blog-api aplicada. -->

# Ejercicio Blog Polirepo

## Parte B

### Qué dijo el agente en el paso 4

- Cargó el `CLAUDE.md` de la carpeta raíz `blog\CLAUDE.md`, así como el del directorio con que se inició la sesion `blog-api\CLAUDE.md`.

- Cargó los dos skills del proyecto generados: `marcador-blog-api` y `marcador-blog-ai`.

- Llamó al campo con el nombre `fragmentos_coincidentes`, en español, sin acentos, en plural, y en `snake_case`.

### Qué encontraste en cada archivo de marcadores y qué indica sobre dónde se ejecuta cada guardarraíl

Solo encontré un único archivo `MARCADORES-blog-api.txt`, con el siguiente contenido, tras haber generado también este mismo fichero desde el prompt:

>2026-10-26T18:43:21.836Z Edit Z:\home\jardotnet\PROJECTS\s7\blog\blog-ai\app\esquemas.py
>
>2026-10-26T19:25:52.734Z Write Z:\home\jardotnet\PROJECTS\s7\blog\blog-api\docs\frontera.md

No generó el archivo `MARCADORES-blog-ai.txt`, ya que inicié la sesión en `blog-api`, y solo se ejecutó su hook. Posteriormente, añadí `blog-ai` con `/add-dir`, y eso me dió acceso a sus archivos pero no cargó su configuración, ni su hook, ni tampoco su `CLAUDE.md`.

Por tanto, el hook de `blog-ai` nunca se ejecutó, por lo que el archivo `MARCADORES-blog-ai.txt` no se llegó a crear.
