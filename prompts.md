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

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Crea el archivo CLAUDE.md en el proyecto blog-ai(../blog-ai) usando el comando init, y al final agrega una sección "REGLAS DE PROCESO" con solo la siguiente regla: Este repositorio es dueño del contenido y todo archivo nuevo que se cree y ubique unicamente en este repositorio debe empezar con un comentario que lo indique.
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Ya creé /home/claos/development/blog/blog-api/CLAUDE.md con el prefijo obligatorio. Tiene los comandos habituales, la arquitectura en capas, la frontera con blog-ai y, al final, la sección REGLAS DE PROCESO con solo la regla que pediste. No ejecuté nada: no corrí los tests ni los comandos del archivo.
```

## Prompt 2

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Crea el archivo CLAUDE.md en el proyecto (../blog-ai) usando el comando init ubicandote en esa carpeta primero, y al final agrega una sección "REGLAS DE PROCESO" con solo la siguiente regla: Los nombres de los campos del contrato público únicamente de este proyecto deben escribirse en español, nunca en inglés.

```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Creé /home/claos/development/blog/blog-ai/CLAUDE.md con el prefijo obligatorio. Incluye los comandos, la arquitectura, el contrato con blog-api y las trampas del dominio. Al final está la sección REGLAS DE PROCESO con solo la regla que pediste. No ejecuté make ni levanté el servicio, solo leí el código y los archivos de configuración.

- Carpeta de trabajo: el shell vuelve a blog-api después de cada comando, porque blog-ai queda fuera del directorio de trabajo de esta sesión. Por eso no pude "ubicarme" de forma persistente en blog-ai. Hice cd dentro de cada comando y escribí el archivo con ruta absoluta.
- Archivos sin commitear: blog-ai no tiene commiteados ni este CLAUDE.md ni el de blog-api; los dos son archivos nuevos sin seguimiento en git.
- Tests y linter: blog-ai no tiene tests ni linter configurados. Lo dejé escrito así en el archivo.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```

## Prompt 3

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Crea un hook PostToolUse que aplique para ambos proyectos (../blog-api y ../blog-ai) al utilizar las herramientas Write y Edit. El hook debe añadir una línea al archivo "MARCADORES-<nombre-del-repo>.txt", que se encontrará en la raiz de cada repositorio según corresponda. La línea debe contener la fecha, la herramienta utilizada y la ruta del archivo tocado. Usa rutas absolutas; determina que es lo mejor si queremos un gobierno único desde ../, un hook en cada repositorio, un hook en un solo repositorio, o un hook en la raiz (si es factible).

```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
El hook PostToolUse (Write|Edit) está creado y probado con entradas simuladas. En esta sesión todavía no se ha disparado de verdad, porque Claude Code carga los hooks al arrancar. Hay que reiniciar la sesión (o abrir /hooks) para que los lea. Los archivos de prueba que generé los borré; los MARCADORES-*.txt se crearán con la primera escritura real.

Qué hay

┌───────────────────────────────────────────────────────────────────┬─────────────────────────────────────────────────┐
│                              Archivo                              │                    Para qué                     │
├───────────────────────────────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ /home/claos/development/blog/.claude/hooks/marcador.sh            │ La lógica, en un único sitio y fuera de los dos │
│                                                                   │  repos.                                         │
├───────────────────────────────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ /home/claos/development/blog/blog-api/.claude/settings.local.json │ Registra el hook y apunta al script por ruta    │
│                                                                   │ absoluta.                                       │
├───────────────────────────────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ /home/claos/development/blog/blog-ai/.claude/settings.local.json  │ Igual que el anterior.                          │
└───────────────────────────────────────────────────────────────────┴─────────────────────────────────────────────────┘

Cada línea tiene este formato, con fecha ISO y ruta absoluta:

2026-10-28T18:54:57-05:00 | Edit | /home/claos/development/blog/blog-ai/app/main.py

Se escribe en el MARCADORES-<repo>.txt del repo que contiene el archivo tocado, no del repo desde el que arrancó la sesión. Si trabajas en blog-api y editas algo de blog-ai, la línea va al marcador de blog-ai. Las rutas fuera de los dos repos y el propio MARCADORES-*.txt se ignoran.

Qué probé

- Un Write en blog-api y un Edit en blog-ai con entradas simuladas escribieron en el marcador correcto.
- Un Edit sobre blog-ai lanzado desde blog-api fue al marcador de blog-ai.
- Una ruta en /tmp, el propio marcador y una entrada que no era JSON salieron en silencio, sin tocar nada.

Por qué esta opción

- Un hook en ../: no es factible. Según la documentación, Claude Code lee .claude/settings.json del directorio de trabajo de la sesión y no sube por las carpetas padre. Esto lo confirmó un subagente leyendo la documentación, y no lo comprobé arrancando una sesión.
- ~/.claude/settings.json: sí daría un gobierno único, y cubriría también sesiones abiertas en ../. Lo descarté porque ese archivo pesa unos 42 KB y tiene hooks de otras herramientas, y porque dispararía en todos tus proyectos.
- Hook en un solo repo: deja el otro sin cubrir.
- Lo que hice: un script único y un registro mínimo en cada repo. Si cambias el formato, lo cambias en un solo sitio.

Límites

- Sesiones abiertas en ../: no cargan estos hooks. Hay que arrancar desde blog-api o blog-ai.
- Ruta fija: el script y los dos settings.local.json apuntan a /home/claos/development/blog. En otra máquina o con otra carpeta no funcionan sin cambiar esa ruta.
- Fuera de git: settings.local.json queda ignorado por tu ~/.config/git/ignore, así que no entra en ningún commit.
- MARCADORES-*.txt sin ignorar: aparecerán como archivos sin seguimiento en cada repo. No toqué ningún .gitignore. Dime si quieres ignorarlos o commitearlos.
- jq: el script lo necesita, y está instalado en tu equipo.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```

## Prompt 4

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Crea una skill en cada repositorio (../blog-api y ../blog-ai) llamada marcador-<nombre-del-repo> cuya descripción indique a que repositorio pertenece.
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Creé una skill en cada repositorio. No las probé: los repos no listan skills nuevas hasta reiniciar la sesión o recargarlas.

┌─────────────┬─────────────────────────────────────────────────────────────────────────────────┬───────────────────┐
│ Repositorio │                                     Archivo                                     │      Nombre       │
├─────────────┼─────────────────────────────────────────────────────────────────────────────────┼───────────────────┤
│ blog-api    │ /home/claos/development/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md │ marcador-blog-api │
├─────────────┼─────────────────────────────────────────────────────────────────────────────────┼───────────────────┤
│ blog-ai     │ /home/claos/development/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md   │ marcador-blog-ai  │
└─────────────┴─────────────────────────────────────────────────────────────────────────────────┴───────────────────┘

Cada descripción empieza con "Pertenece al repositorio blog-api" o "Pertenece al repositorio blog-ai", seguido de qué es ese repo y cuándo usarla.

No indicaste qué debía hacer la skill, así que la ligué al hook anterior. Lee el MARCADORES-<repo>.txt de su propio repositorio y responde sobre qué archivos se tocaron, cuándo y con qué herramienta. Si el archivo no existe, lo dice. Es lo único que inferí; si querías otra función, dímelo y la cambio.

- Regla de blog-api: SKILL.md exige que el frontmatter vaya en la primera línea, así que no pude poner el comentario de propiedad al principio. Lo puse justo después del frontmatter: <!-- Este repositorio (blog-api) es dueño del contenido de este archivo. -->. Es la lectura más cercana posible de tu regla.
- Regla de blog-ai: la de los campos en español trata del contrato público, no de estas skills, así que no aplicó.
- Git: las skills no están ignoradas, así que aparecerán como archivos nuevos sin seguimiento en cada repo. A diferencia de settings.local.json, tendrías que commitearlas.
- Marcadores: las skills hablan de MARCADORES-<repo>.txt, que solo se crea con el hook activo. En un clon ajeno no existirá.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```

## Prompt 5

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Añade a la clase ResultadoBusqueda en ../blog-ai/app/esquemas.py un campo que indique cuántos fragmentos del artículo han coincidido con la bùsqueda. Toca únicamente ese archivo, usa solo las herramientas Write y Edit, nunca un script.
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
He añadido el campo fragmentos_coincidentes: int = Field(default=1, ge=1) a ResultadoBusqueda en ../blog-ai/app/esquemas.py. Solo he tocado ese archivo y solo con Read y Edit. No he ejecutado nada, así que no he comprobado que el cambio funcione.

- Valor por defecto: el campo tiene default=1 porque un resultado solo existe si coincidió al menos un fragmento. Así el código que construye ResultadoBusqueda sin el campo sigue funcionando.
- Quién lo rellena: el servicio de búsqueda todavía no calcula el número real. Hasta que lo haga, siempre devolverá 1.
- Contrato: el campo nuevo cambia el OpenAPI de blog-ai, y blog-api valida contra una copia fijada en contracts/blog-ai.openapi.json. Para adoptarlo hay que copiar a mano ../blog-ai/contrato/openapi.json sobre esa copia y ejecutar node ace contrato:verificar. Yo no lo he hecho porque pediste tocar un solo archivo.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```

## Prompt 6

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Qué archivos CLAUDE.md se cargaron al iniciar esta sesión? Cita la regla que encontraste en cada uno.
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Se cargaron dos archivos CLAUDE.md:

1. /home/claos/development/blog/CLAUDE.md (la carpeta que contiene los repositorios, no está dentro de ninguno)

Su sección ## REGLA-PADRE dice:

▎ Por eso, toda respuesta que des aquí termina con esta línea, sola y literal:
▎ REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

2. /home/claos/development/blog/blog-api/CLAUDE.md (el repositorio blog-api)

Su sección ## REGLAS DE PROCESO dice:

▎ Este repositorio es dueño del contenido y todo archivo nuevo que se cree y ubique unicamente en este repositorio debe empezar con un comentario que lo indique.

El resto de este archivo es guía técnica: comandos, arquitectura en capas, reglas de negocio y la frontera con blog-ai. No lo cuento como regla de proceso.

En la tarea anterior no creé ningún archivo nuevo, solo edité esquemas.py. Por eso la regla de blog-api no se aplicó. Además, ese archivo está en blog-ai, no en blog-api.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```

## Prompt 7

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Qué skills relacionados a estos repositorios tienes cargados?
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Hay dos skills relacionadas con estos repositorios, una por repositorio:

- marcador-blog-api: pertenece a blog-api. Consulta y resume MARCADORES-blog-api.txt, el registro de archivos tocados con Write y Edit en ese repositorio. Sirve cuando preguntan qué se ha modificado en blog-api o piden revisar los marcadores.
- marcador-blog-ai: pertenece a blog-ai. Hace lo mismo con MARCADORES-blog-ai.txt.

No hay ninguna para blog-web. Tampoco he invocado ninguna de las dos en esta sesión: solo conozco su descripción. En la tarea anterior edité ../blog-ai/app/esquemas.py, y esa edición debería figurar en MARCADORES-blog-ai.txt. No he comprobado si está registrada.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```
## Prompt 8

**Modelo:** Sonet High
**Herramienta:** Claude Code

```
Qué nombre le diste al campo en la clase ResultadoBusqueda y por qué?
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
El campo se llama fragmentos_coincidentes, con tipo int. Lo elegí por tres razones:

- Convención del archivo: los campos están en español y en snake_case (post_id, motivos_omision, puntuacion). Además, RespuestaIndexar ya usa fragmentos para contar fragmentos.
- Tu enunciado: pediste cuántos fragmentos "han coincidido" con la búsqueda, así que coincidentes recoge ese verbo.
- Distinguirlo de fragmento: esa clase ya tiene fragmento: str, que es el texto del fragmento mostrado. El plural y el sufijo dejan claro que el nuevo es un recuento y no otro texto.

Le puse default=1 y ge=1 porque un resultado solo existe si coincidió al menos un fragmento. El valor por defecto también evita romper el código que construye ResultadoBusqueda sin el campo. El nombre fue una decisión mía, no algo que pidieras, así que si prefieres otro, como coincidencias o num_fragmentos, se cambia con una sola edición.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```


