<!-- blog-api es el dueño del contenido del blog «Corriente». -->

# Frontera

## 1. Qué dijo el agente en el paso 4

Qué archivos CLAUDE.md dijo haber cargado (a), qué skills disponibles tenía (b) y qué nombre dio al campo (c).

### a. Archivos CLAUDE.md cargados al iniciar la sesión

Se cargaron dos:

- `/home/hpadmin/dev/ai4devs/blog/CLAUDE.md`: está en la carpeta que contiene los repositorios, fuera de todos ellos. Claude Code lo cargó porque al arrancar lee los CLAUDE.md de las carpetas superiores. Su regla:
  > toda respuesta que des aquí termina con esta línea, sola y literal: REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
- `/home/hpadmin/dev/ai4devs/blog/blog-api/CLAUDE.md`: el del repositorio donde arrancó la sesión. Su regla:
  > Este repositorio es el dueño del contenido del blog. Todo archivo nuevo debe empezar con un comentario que lo indique

El de blog-ai (`/home/hpadmin/dev/ai4devs/blog/blog-ai/CLAUDE.md`) no se cargó al inicio, aunque blog-ai estaba agregado como carpeta de trabajo adicional. Lo abrí yo con Read antes de modificar `esquemas.py`. Su regla:

> Los nombres de los campos del contrato público […] se escriben en español, nunca en inglés

### b. Skills disponibles

- Del ejercicio: `marcador-blog-api` y `marcador-blog-ai`. Cada una muestra el archivo `MARCADORES-<repo>.txt` de su repositorio.
- De Claude Code: `update-config`, `keybindings-help`, `code-review`, `simplify`, `fewer-permission-prompts`, `loop`, `schedule`, `claude-api`, `claude-in-chrome`, `run`, `plugin-authoring`, `init`, `security-review` y `dataviz`.
- De Anthropic (`anthropic-skills:`): `built-in-browser`, `chrome-browser`, `computer-use`, `deep-research`, `docs`, `docx`, `import-memory`, `morning`, `pdf`, `pptx`, `setup-writing-style`, `skill-creator` y `xlsx`.

### c. Nombre del campo y por qué

Lo llamó `fragmentos_coincidentes`, por tres razones:

- Español: el CLAUDE.md de blog-ai pide que los campos del contrato público estén en español, y `ResultadoBusqueda` forma parte de ese contrato. Por eso no usé, por ejemplo, `match_count`.
- Las palabras del pedido: pediste «cuántos fragmentos del artículo han coincidido».
- El estilo del archivo: sigue el formato que ya usan otros campos, como `fragmentos_indexados` y `motivos_omision`. Además, «fragmento» es el término que usan el esquema y la tabla `fragmentos` de la base de datos.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

## 2. Qué encontraste en cada archivo de marcadores (a) y qué indica sobre dónde se ejecuta cada guardarraíl (b)

### a. Contenido de los archivos de marcadores

En `MARCADORES-blog-api.txt`:

```
2026-10-28T07:55:31-03:00    Edit    /home/hpadmin/dev/ai4devs/blog/blog-api/prompts.md
2026-10-28T07:58:15-03:00    Edit    /home/hpadmin/dev/ai4devs/blog/blog-ai/app/esquemas.py
```

En `MARCADORES-blog-ai.txt`:

-- No creó el archivo --

### b. Dónde se ejecuta cada guardarraíl

Está bien que `MARCADORES-blog-ai.txt` esté vacío porque el que está ejecutando es blog-api. Las Skills no se disparan en blog-ai, que son las que escriben el archivo. El funcionamiento es el esperado
