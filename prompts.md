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

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Estamos en el repositorio blog-api. Este repositorio está ubicado bajo la carpeta blog/, que contiene otros dos repositorios: blog-ai y blog-web.

Realiza la siguiente acción únicamente para los repositorios blog-api y blog-ai:

1. Crea un archivo CLAUDE.md en la raíz con una sola regla propia del repositorio.

En blog-api escribe: 
# Reglas de blog-api

## REGLA-HIJA blog-api

Este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique:

REGLA-HIJA de blog-api aplicada.

En blog-ai escribe:
# Reglas de blog-ai

## REGLA-HIJA blog-ai

Los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. 
```

**Qué salió:** en modo manual on, pudo crear el archivo `blog-ai/CLAUDE.md` sin problemas. ME solicitó permisos para poder crear `blog-api/CLAUDE.md` y lo creó mediante PowerShell.

## Prompt 2

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Ahora crea una segunda acción, y de nuevo únicamente para los repositorios blog-api y blog-ai:

2. Crea un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debes añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz del propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Donde <nombre-del-repo> sería: blog-api o blog-ai en cada caso. Usa rutas absolutas, para poder así registrar cambios en archivos situados fuera del repositorio.
```

**Qué salió:** volvió a preguntar permisos y creó el hook en blog-api y en blog-ai, y lo probó con una entrada simulada. Cada línea debería tener el siguiente formato:
`2026-10-26T18:08:08.609Z Write C:\fuera\prueba.txt`

## Prompt 3

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Finalmente, crea una última acción, únicamente para los repositorios blog-api y blog-ai:

3. Crea una skill llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece. Igual que antes, <nombre-del-repo> sería: blog-api o blog-ai en cada caso.
```

**Qué salió:** tras solicitar permiso, creó los skills `marcador-blog-api` y `marcador-blog-ai` en cada repositorio, vinculándlo a su respectivo hook. Cada skill lee el fichero `MARCADORES-<repo>.txt`, lo resume y distingue los archivos de dentro del repo de los de fuera.

## Prompt 4

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica únicamente ese archivo, nada más. Utilizar la herramienta de edición de archivos, nunca un script.
```

**Qué salió:** añadió a la clase `ResultadoBusqueda` el campo `fragmentos_coincidentes: int = Field(default=1, ge=1)` en `blog-ai/app/esquemas.py`, con la herramienta de edición y sin tocar ningón otro archivo. Al final de la respuesta se mostró el mensaje:
`REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.`

Se generó el archivo `MARCADORES-blog-api.txt`, con contenido:
`2026-10-26T18:43:21.836Z Edit Z:\PROJECTS\s7\blog\blog-ai\app\esquemas.py`

Pero no se generó el archivo `MARCADORES-blog-ai.txt`.

## Prompt 5

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Ahora responde qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno.
```

**Qué salió:** Al iniciar la sesión se cargaron dos archivos CLAUDE.md:

1. `Z:\home\jardotnet\PROJECTS\s7\blog\CLAUDE.md`, la carpeta que contiene los repositorios. Su regla es la REGLA-PADRE: este archivo no vive dentro de ningún repositorio, así que toda respuesta que dé en este espacio de trabajo debe terminar con la línea literal «REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.»
2. `Z:\home\jardotnet\PROJECTS\s7\blog\blog-api\CLAUDE.md`, el repositorio `blog-api`. Su regla es la REGLA-HIJA blog-api: el repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que diga «REGLA-HIJA de blog-api aplicada.»

No se cargó ningún `CLAUDE.md` de `blog-ai`. Ese directorio lo añadí después con `/add-dir` y no apareció ninguno de sus archivos de instrucciones en el contexto. Por eso la REGLA-HIJA no se aplicó a mi edición anterior: era un archivo existente de `blog-ai`, no un archivo nuevo de `blog-api`.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

## Prompt 6

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Qué skills tienes disponibles?
```

**Qué salió:** Estas son las skills que tengo disponibles, agrupadas por tipo.

**Del proyecto**

- `marcador-blog-api`: Ver, resumir o comprobar los marcadores de archivos escritos o editados en blog-api (`MARCADORES-blog-api.txt`).
- `marcador-blog-ai`: Lo mismo para blog-ai (`MARCADORES-blog-ai.txt`).
- `guided-refactor`: Refactorizar con inventario de solo lectura, plan breve y aprobación antes de editar.

**Código y revisión**

- `code-review`: Revisa el diff o una PR.
- `simplify`: Limpia y simplifica el código cambiado.
- `security-review`: Revisión de seguridad de los cambios de la rama.
- `run`: Lanza la app para comprobar que un cambio funciona.
- `init`: Crea un `CLAUDE.md`.
- `claude-api`: Referencia de la API de Claude y del SDK de Anthropic.

**Configuración y automatización**

- `update-config`: Edita `settings.json` (hooks, permisos, variables de entorno).
- `keybindings-help`: Atajos de teclado.
- `fewer-permission-prompts`: Reduce las peticiones de permiso con una lista de permitidos.
- `loop`: Ejecuta una tarea de forma recurrente.
- `schedule`: Agentes para tareas programadas.
- `plugin-authoring`: Crea mods o hooks.
- `workflow-authoring`: Guía para escribir scripts de `Workflow`.

**Artifacts y visualización**

- `artifact-design`: Diseño de páginas.
- `artifact-diagramming`: Diagramas publicables.
- `artifact-capabilities`: Capacidades de ejecución de un artifact.
- `dataviz`: Gráficos y dashboards.

**Plugins de Cowork**

- `cowork-plugin-management:cowork-plugin-customizer`
- `cowork-plugin-management:create-cowork-plugin`

**Navegador y escritorio**

- `claude-in-chrome`
- `anthropic-skills:chrome-browser`
- `anthropic-skills:built-in-browser`
- `anthropic-skills:computer-use`

**Documentos y archivos**

- `anthropic-skills:docs`
- `anthropic-skills:docx`
- `anthropic-skills:pptx`
- `anthropic-skills:xlsx`
- `anthropic-skills:pdf`
- `anthropic-skills:google-workspace`

**Otras**

- `anthropic-skills:deep-research`
- `anthropic-skills:import-memory`
- `anthropic-skills:morning`
- `anthropic-skills:skill-creator`

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

## Prompt 7

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Qué nombre has dado al campo y por qué?
```

**Qué salió:** El campo se llama `fragmentos_coincidentes`. Lo elegí por estas razones:

- Idioma y estilo del archivo: los nombres de `esquemas.py` están en español, sin acentos y en `snake_case` (`puntuacion`, `fragmento`, `motivos_omision`, `fragmentos_indexados`). El nuevo sigue esa misma convención.
- Plural frente a `fragmento`: `ResultadoBusqueda` ya tiene `fragmento: str`, el texto del fragmento mostrado. Con el plural queda claro que el nuevo campo es un contador, no otro texto.
- «Coincidentes»: describe justo lo que pediste, cuántos fragmentos del artículo coincidieron con la búsqueda. Evité nombres como `fragmentos` a secas, que se confundiría con `RespuestaIndexar.fragmentos` (cuántos se generaron al indexar), o `total_fragmentos`, que sugeriría todos los del artículo y no solo los que coincidieron.

Sobre el valor por defecto: en `esquemas.py` usé `default=1` y `ge=1`, lo que es una decisión mía, no algo que pidieras.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

## Prompt 8

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Crea el archivo docs/frontera.md, con tútulo #Ejercicio Blog Polirepo y un subtítulo ##Parte B
```

**Qué salió:** creó el archivo, con el siguiente comentario inicial:
`<!-- REGLA-HIJA de blog-api aplicada. -->`
