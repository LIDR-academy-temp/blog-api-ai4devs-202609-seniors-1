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
Me solicitan el siguiente ejercicio sobre un par de repos, como harías los distintos prompts:

---

2. Prepara tres piezas en cada repositorio: `blog-api` y `blog-ai`. Con la sesión del agente iniciada en `blog-api`, pídele que cree lo siguiente en ambos repositorios, sin cambiar nada más:

* Un `CLAUDE.md` en la raíz con una sola regla propia del repositorio. En `blog-api`: este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique. En `blog-ai`: los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. Las reglas son distintas para poder reconocer después cuál se aplicó.
* Un hook que se ejecute al escribir o editar un archivo, mediante `PostToolUse` para las herramientas `Write` y `Edit`. Debe añadir una línea a `MARCADORES-<nombre-del-repo>.txt`, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Pide que use rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio.
* Una skill sencilla llamada `marcador-<nombre-del-repo>`, cuya descripción indique a qué repositorio pertenece.

```

**Qué salió:** 
```
Mi planteamiento es un único prompt con las tres piezas, porque la sesión está en blog-api y el agente debe tocar los dos repos. Las cuatro cosas que importan son estas:

- Alcance cerrado: pide "sin cambiar nada más".
- Rutas absolutas: las pides en el comando del hook y en el archivo de marcadores.
- Reglas distintas en cada CLAUDE.md.
- Verificación al final.

Prompt (para pegar en la sesión de blog-api)

Necesito preparar tres piezas en dos repositorios:
- blog-api: /home/mtomas/ai4devs/blog/blog-api (el actual)
- blog-ai:  /home/mtomas/ai4devs/blog/blog-ai

Crea SOLO los archivos que describo, en ambos repos. No modifiques, formatees
ni borres nada más, y no hagas commits.

1. CLAUDE.md en la raíz de cada repo, con una única regla:
   - blog-api: "Este repositorio es el dueño del contenido. Todo archivo nuevo
     debe empezar con un comentario que lo indique."
   - blog-ai: "Los nombres de los campos del contrato público deben escribirse
     en español, nunca en inglés."
   Sin ninguna otra línea de contenido.

2. Un hook PostToolUse con matcher "Write|Edit" en .claude/settings.json de
   cada repo (si el archivo ya existe, fusiona sin tocar lo demás). Debe
   añadir una línea a MARCADORES-<nombre-del-repo>.txt en la raíz de SU
   repositorio, con: fecha (ISO 8601), herramienta usada (tool_name) y ruta
   del archivo modificado (tool_input.file_path).
   - Usa rutas absolutas tanto para el script/comando del hook como para el
     archivo de marcadores (no $CLAUDE_PROJECT_DIR relativo ni rutas
     relativas): el hook debe poder registrar cambios en archivos situados
     fuera de su repositorio.
   - Pon la lógica en un script (.claude/hooks/marcador.sh) que lea el JSON
     de stdin con jq y haga append (>>) al archivo.
   - Resultado esperado de cada línea:
     2026-10-28T10:15:00+01:00 | Write | /ruta/absoluta/archivo.py

3. Una skill sencilla en .claude/skills/marcador-<nombre-del-repo>/SKILL.md
   (marcador-blog-api y marcador-blog-ai), con frontmatter name y description.
   La description debe indicar explícitamente a qué repositorio pertenece
   (p. ej. "Skill del repositorio blog-api: ..."). El cuerpo: unas pocas
   líneas, por ejemplo que añada una nota de marcador manual al
   MARCADORES-<repo>.txt.

Al terminar, lista los archivos creados en cada repo, comprueba con
`git status` que no hay nada más cambiado y prueba cada script del hook
con un JSON de ejemplo por stdin (borrando después las líneas de prueba de
los MARCADORES).

Notas

- Rutas: comprueba que la de blog-ai es la real antes de enviarlo.
- Qué hook se activa: desde blog-api, el hook que dispara es el de blog-api, incluso cua. Por eso se piden rutas absolutas. Esas ediciones aparecerán en MARCADORES-blog-api.txt
  con la ruta de blog-ai.
- Hooks nuevos: los settings.json creados a mitad de sesión pueden requerir reiniciar o uen.
- CLAUDE.md de blog-ai: solo se aplica al abrir una sesión en blog-ai. Para reconocer qué regla se aplicó, abre una sesión en cada repo y pide que cree un archivo o un campo del contrato.
- Si prefieres tres prompts separados (uno por pieza), el contenido es el mismo troceadoicada, así que puedes revisar su salida antes de seguir.

✻ Crunched for 19s · done 6:20 PM
```

---

## Prompt 2

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
 Sí, pásame los tres prompts separados
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Prompt 1: CLAUDE.md (en ambos repos)

Crea un CLAUDE.md en la raíz de cada uno de estos repositorios:
- blog-api: /home/mtomas/ai4devs/blog/blog-api
- blog-ai:  /home/mtomas/ai4devs/blog/blog-ai

Cada uno con UNA sola regla, y distinta:
- blog-api: "Este repositorio es el dueño del contenido. Todo archivo nuevo
  debe empezar con un comentario que lo indique."
- blog-ai: "Los nombres de los campos del contrato público deben escribirse
  en español, nunca en inglés."

No añadas ninguna otra línea de contenido, no modifiques ningún otro archivo
y no hagas commits. Al terminar, muestra el contenido de ambos archivos y
el `git status` de cada repo.

Prompt 2: Hook PostToolUse (en ambos repos)

Crea un hook PostToolUse con matcher "Write|Edit" en cada repositorio:
- blog-api: /home/mtomas/ai4devs/blog/blog-api
- blog-ai:  /home/mtomas/ai4devs/blog/blog-ai

Archivos a crear en cada repo (sin tocar nada más ni hacer commits):
- .claude/hooks/marcador.sh: lee el JSON de stdin con jq y añade (>>) una
  línea a MARCADORES-<nombre-del-repo>.txt en la raíz de SU repositorio, con
  este formato: fecha ISO 8601 | tool_name | tool_input.file_path
  Ejemplo: 2026-10-28T10:15:00+01:00 | Write | /ruta/absoluta/archivo.py
- .claude/settings.json: registra el hook. Si el archivo ya existe, fusiona
  sin alterar el resto.

Usa rutas absolutas en todo: en el comando del hook en settings.json y en el
destino del archivo de marcadores dentro del script. El hook tiene que poder
registrar cambios en archivos situados fuera de su repositorio, así que no
uses rutas relativas.

Marca el script como ejecutable. Al terminar, pruébalo pasándole por stdin un
JSON de ejemplo (con un file_path fuera del repo), muestra la línea generada
y borra después las líneas de prueba de MARCADORES-*.txt. Confirma con
`git status` que solo existen los archivos descritos.

Prompt 3: Skills (en ambos repos)

Crea una skill sencilla en cada repositorio:
- blog-api: /home/mtomas/ai4devs/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md
- blog-ai:  /home/mtomas/ai4devs/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md

Cada SKILL.md lleva frontmatter con `name` (igual que la carpeta) y
`description`. La description debe indicar explícitamente a qué repositorio
pertenece, por ejemplo: "Skill del repositorio blog-api: añade un marcador
manual a MARCADORES-blog-api.txt".

El cuerpo, de pocas líneas: instruye añadir una línea con fecha y un texto
dado por el usuario a MARCADORES-<nombre-del-repo>.txt de su propio repo
(ruta absoluta).

No modifiques ningún otro archivo ni hagas commits. Al terminar, muestra
ambos SKILL.md y el `git status` de cada repo.

Orden y comprobaciones

- Orden: 1, 2 y 3. El hook (2) puede registrar las ediciones de los otros pasos, así que el prompt 3 ya dejará marcas en MARCADORES-blog-api.txt, lo que sirve como prueba real.
- Ficheros de prueba: si no quieres esas marcas, pide en el prompt 2 que borre las líneas de prueba, como ya indica.
- Recarga: tras el prompt 2, abre /hooks o reinicia la sesión para que el hook se cargue.

✻ Cogitated for 10s · done 6:24 PM
```


---

## Prompt 3

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Crea un CLAUDE.md en la raíz de cada uno de estos repositorios:
- blog-api: /home/mtomas/ai4devs/blog/blog-api
- blog-ai:  /home/mtomas/ai4devs/blog/blog-ai

Cada uno con UNA sola regla, y distinta:
- blog-api: "Este repositorio es el dueño del contenido. Todo archivo nuevo
  debe empezar con un comentario que lo indique."
- blog-ai: "Los nombres de los campos del contrato público deben escribirse
  en español, nunca en inglés."

No añadas ninguna otra línea de contenido, no modifiques ningún otro archivo
y no hagas commits. Al terminar, muestra el contenido de ambos archivos y
el `git status` de cada repo.

```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
  Listed 1 directory

Ambos repos existen y ninguno tiene CLAUDE.md todavía.

● Write(CLAUDE.md)
Wrote 1 line to CLAUDE.md
Este repositorio es el dueño del contenido. Todo archivo nuevo debe empezar con un comentario que lo indique.

● Write(~/ai4devs/blog/blog-ai/CLAUDE.md)
Wrote 1 line to ~/ai4devs/blog/blog-ai/CLAUDE.md
Los nombres de los campos del contrato público deben escribirse en español, nunca en inglés.
Allowed by auto mode classifier

  Ran 1 shell command

Creé el CLAUDE.md en la raíz de blog-api y de blog-ai, cada uno con su única regla, y no hice commits.

- blog-api/CLAUDE.md: "Este repositorio es el dueño del contenido. Todo archivo nuevo debe empezar con un comentario que lo indique."
- blog-ai/CLAUDE.md: "Los nombres de los campos del contrato público deben escribirse en español, nunca en inglés."

El git status de blog-ai solo muestra ?? CLAUDE.md. El de blog-api muestra ?? CLAUDE.md y además  M prompts.md. No he tocado prompts.md: el estado inicial de la sesión estaba limpio, así que ese cambio debe de ser tuyo, hecho después de arrancar. Compruébalo antes de hacer commit.

✻ Crunched for 16s · done 6:25 PM
```


---

## Prompt 4

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
 Iba a pasar el prompt 2 pero he visto que solo indicabas de crearlo en el blog-api, ¿por qué? Te he dicho en los dos repositorios.
```

**Qué salió:** (Había copiado mal el prompt, no entiendo como, y había perdido la línea del blog-ai, por raro que parezca Claude tenía razón 😅)
```
Creo que el prompt 2 sí incluía los dos repositorios. Empieza así:

▎ Crea un hook PostToolUse con matcher "Write|Edit" en cada repositorio:
▎ - blog-api: /home/mtomas/ai4devs/blog/blog-api
▎ - blog-ai: /home/mtomas/ai4devs/blog/blog-ai

Y sigue con "Archivos a crear en cada repo". Quizá lo viste en otra versión, o te llevó a confusión que las rutas de los archivos van como <nombre-del-repo> y no escritas por separado. Si eso hizo dudar al agente, mejor dejarlo explícito. Esta es la versión sin ambigüedad:

Crea un hook PostToolUse (matcher "Write|Edit") en AMBOS repositorios.
Son dos instalaciones independientes, una por repo; no basta con hacer una.

Para blog-api (/home/mtomas/ai4devs/blog/blog-api), crea:
- /home/mtomas/ai4devs/blog/blog-api/.claude/hooks/marcador.sh
- /home/mtomas/ai4devs/blog/blog-api/.claude/settings.json
  Destino de las líneas: /home/mtomas/ai4devs/blog/blog-api/MARCADORES-blog-api.txt

Para blog-ai (/home/mtomas/ai4devs/blog/blog-ai), crea:
- /home/mtomas/ai4devs/blog/blog-ai/.claude/hooks/marcador.sh
- /home/mtomas/ai4devs/blog/blog-ai/.claude/settings.json
  Destino de las líneas: /home/mtomas/ai4devs/blog/blog-ai/MARCADORES-blog-ai.txt

Cada marcador.sh lee el JSON de stdin con jq y añade (>>) una línea al
archivo de marcadores de SU repo, con formato:
fecha ISO 8601 | tool_name | tool_input.file_path
Ejemplo: 2026-10-28T10:15:00+01:00 | Write | /ruta/absoluta/archivo.py

Usa rutas absolutas en todo: en el comando del hook en settings.json y en el
destino dentro del script. El hook debe poder registrar cambios en archivos
fuera de su repositorio. Si un settings.json ya existe, fusiona sin alterar
el resto. Marca los scripts como ejecutables.

No modifiques nada más ni hagas commits. Al terminar, prueba CADA script con
un JSON de ejemplo por stdin (con un file_path fuera del repo), muestra la
línea generada y borra las líneas de prueba. Confirma con `git status` en
los dos repos que solo existen los archivos descritos.

Aquí se nombran los cuatro archivos y los dos destinos, y se pide probar cada script, de modo que el agente no pueda dar por hecho solo blog-api.

✻ Cooked for 10s · done 6:31 PM
```


---

## Prompt 5

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Vale, ejecuta ese prompt 2 en los dos repos
```

**Qué salió:** (me ha solicitado permiso para ejecutar un script).
```
jq no está instalado, así que los scripts usarán python3 para leer el JSON de stdin (el efecto es el mismo).

● Write(.claude/hooks/marcador.sh)
Wrote 10 lines to .claude/hooks/marcador.sh
#!/usr/bin/env bash
# Registra en MARCADORES-blog-api.txt cada Write/Edit: fecha | herramienta | ruta
DESTINO="/home/mtomas/ai4devs/blog/blog-api/MARCADORES-blog-api.txt"
python3 -I -c '
import sys, json, datetime
d = json.load(sys.stdin)
ruta = d.get("tool_input", {}).get("file_path", "")
fecha = datetime.datetime.now().astimezone().isoformat(timespec="seconds")
print(f"{fecha} | {d.get(\"tool_name\", \"\")} | {ruta}")
' >> "$DESTINO"
Allowed by auto mode classifier

● Write(~/ai4devs/blog/blog-ai/.claude/hooks/marcador.sh)
Wrote 10 lines to ~/ai4devs/blog/blog-ai/.claude/hooks/marcador.sh
#!/usr/bin/env bash
# Registra en MARCADORES-blog-ai.txt cada Write/Edit: fecha | herramienta | ruta
DESTINO="/home/mtomas/ai4devs/blog/blog-ai/MARCADORES-blog-ai.txt"
python3 -I -c '
import sys, json, datetime
d = json.load(sys.stdin)
ruta = d.get("tool_input", {}).get("file_path", "")
fecha = datetime.datetime.now().astimezone().isoformat(timespec="seconds")
print(f"{fecha} | {d.get(\"tool_name\", \"\")} | {ruta}")
' >> "$DESTINO"
Allowed by auto mode classifier

● Write(.claude/settings.json)
Wrote 15 lines to .claude/settings.json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "/home/mtomas/ai4devs/blog/blog-api/.claude/hooks/marcador.sh"
          }
… +5 lines
Allowed by auto mode classifier

● Write(~/ai4devs/blog/blog-ai/.claude/settings.json)
Wrote 15 lines to ~/ai4devs/blog/blog-ai/.claude/settings.json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "/home/mtomas/ai4devs/blog/blog-ai/.claude/hooks/marcador.sh"
          }
… +5 lines
Allowed by auto mode classifier

  Ran 1 shell command

La prueba falló: las comillas escapadas dentro del f-string son un error de sintaxis. Lo corrijo en ambos scripts.

  Ran 1 shell command

El hook PostToolUse (Write|Edit) está instalado en blog-api y en blog-ai, y probé los dos scripts por separado.

Archivos creados en cada repo (<repo> es blog-api o blog-ai):
- .claude/hooks/marcador.sh, ejecutable.
- .claude/settings.json, con el hook registrado.

Rutas absolutas: el comando del hook y el destino del marcador (/home/mtomas/ai4devs/blog/<repo>/MARCADORES-<repo>.txt) usan rutas absolutas.

Prueba: pasé a cada script un JSON de ejemplo con un file_path fuera del repo (/tmp/fuera/ejemplo.txt). Cada uno escribió su línea en su propio archivo de marcadores:
2026-10-28T18:45:30+01:00 | Write | /tmp/fuera/ejemplo.txt.
Después borré los dos MARCADORES-*.txt de prueba.

Dos cosas que debes saber:
- jq: no está instalado, así que los scripts leen el JSON con python3 -I en lugar de jq. El resultado es el mismo.
- Primer intento: falló por un error de sintaxis (comillas dentro de un f-string). Lo corregí y repetí la prueba con ambos scripts.

Estado de git:
- blog-api: .claude/ y CLAUDE.md sin seguir, más  M prompts.md. Ese cambio no es mío (ya lo vi antes).
- blog-ai: .claude/ y CLAUDE.md sin seguir.

El hook solo se activa si recargas la configuración, con /hooks o reiniciando la sesión. Aún no he comprobado que se dispare con una escritura real.

✻ Brewed for 50s · done 6:45 PM
```


---

## Prompt 6

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Ahora el prompt 3, las skills
```

**Qué salió:**
```

● Write(.claude/skills/marcador-blog-api/SKILL.md)
Wrote 10 lines to .claude/skills/marcador-blog-api/SKILL.md
---
name: marcador-blog-api
description: Skill del repositorio blog-api (/home/mtomas/ai4devs/blog/blog-api): añade un marcador manual con fecha y texto a MARCADORES-blog-api.txt.
---

Añade una línea al final de `/home/mtomas/ai4devs/blog/blog-api/MARCADORES-blog-api.txt` con el formato:

`<fecha ISO 8601> | marcador | <texto indicado por el usuario>`

Usa la ruta absoluta indicada. No modifiques ningún otro archivo.
Allowed by auto mode classifier

● Write(~/ai4devs/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md)
Wrote 10 lines to ~/ai4devs/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md
---
name: marcador-blog-ai
description: Skill del repositorio blog-ai (/home/mtomas/ai4devs/blog/blog-ai): añade un marcador manual con fecha y texto a MARCADORES-blog-ai.txt.
---

Añade una línea al final de `/home/mtomas/ai4devs/blog/blog-ai/MARCADORES-blog-ai.txt` con el formato:

`<fecha ISO 8601> | marcador | <texto indicado por el usuario>`

Usa la ruta absoluta indicada. No modifiques ningún otro archivo.
Allowed by auto mode classifier

  Read 1 file, ran 2 shell commands

Creé las dos skills, marcador-blog-api y marcador-blog-ai, cada una en .claude/skills/<nombre>/SKILL.md de su repo. No hice commits.

- Frontmatter: name es igual que la carpeta. La description empieza con "Skill del repositorio blog-api" o "Skill del repositorio blog-ai", con la ruta del repo.
- Cuerpo: pide añadir a MARCADORES-<repo>.txt, con ruta absoluta, una línea fecha ISO 8601 | marcador | <texto del usuario>. No toca nada más.

El hook de blog-api ya se dispara con escrituras reales. Al crear las skills, MARCADORES-blog-api.txt registró las dos escrituras, y la segunda es un archivo de blog-ai, fuera de su repo:

2026-10-28T18:48:53+01:00 | Write | /home/mtomas/ai4devs/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md
2026-10-28T18:48:53+01:00 | Write | /home/mtomas/ai4devs/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md

Por eso MARCADORES-blog-api.txt aparece ahora como archivo sin seguir en git status. blog-ai no tiene su MARCADORES-blog-ai.txt porque su hook solo se activa en sesiones abiertas en ese repo.

El resto del git status es el esperado: .claude/ (hook, settings y skill) y CLAUDE.md en cada repo. En blog-api sigue además el  M prompts.md, que no es mío.

✻ Cogitated for 17s · done 6:49 PM
```


---

## Prompt 7

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Puedes montarme un prompt para ejecutar el siguiente ejercicio:
  4. Un encargo en el repositorio añadido y tres preguntas. Pídele que añada a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Indica que debe modificar solo ese archivo y utilizar la herramienta de edición de archivos, nunca un script.

  Al terminar, pídele que responda por separado:

  Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno.

  Qué skills tiene disponibles.

  Qué nombre ha dado al campo y por qué.
```

**Qué salió:** (opcional, una línea) funcionó a la primera / tuve que insistir / me inventó una ruta que no existe.
```
Aquí tienes el prompt, listo para pegarlo en la sesión:

Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda.

Condiciones:
- Modifica solo ese archivo (../blog-ai/app/esquemas.py). No toques ningún otro.
- Usa la herramienta de edición de archivos (Edit). No uses nunca un script, ni sed, ni python, ni redirecciones de shell para escribir.

Al terminar, responde por separado a estas tres preguntas:

1. Qué archivos CLAUDE.md se cargaron al iniciar la sesión. Cita la regla de cada uno.
2. Qué skills tienes disponibles.
3. Qué nombre has dado al campo y por qué.

Dos observaciones para la ejecución:

- Directorio adicional: ../blog-ai ya está como directorio adicional de esta sesión. Debería poder editarlo sin arrancar otra sesión.
- Qué comprobar en las respuestas:
  - La pregunta 1 debería citar el CLAUDE.md de la carpeta padre, con su regla de la línea final, y el de blog-api, con su regla del comentario inicial en archivos nuevos.
  - La pregunta 2 debería listar marcador-blog-api y marcador-blog-ai, entre otras.
  - Si el repo blog-ai tiene su propio CLAUDE.md, mira si aparece. Puede que no se cargue hasta que se lea un archivo de ese repo.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

✻ Brewed for 17s · done 6:54 PM
```


---

## Prompt 8

**Modelo:** Sonnet 5.5 Medium
**Herramienta:** Claude Code

```
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda.

Condiciones:
- Modifica solo ese archivo (../blog-ai/app/esquemas.py). No toques ningún otro.
- Usa la herramienta de edición de archivos (Edit). No uses nunca un script, ni sed, ni python, ni redirecciones de shell para escribir.

Al terminar, responde por separado a estas tres preguntas:

1. Qué archivos CLAUDE.md se cargaron al iniciar la sesión. Cita la regla de cada uno.
2. Qué skills tienes disponibles.
3. Qué nombre has dado al campo y por qué.
```

**Qué salió:** (Me ha solicitado permiso para editar el fichero de esquemas.py)
```
  Read 1 file

● Update(~/ai4devs/blog/blog-ai/app/esquemas.py)
Added 3 lines
    # Similitud coseno en [0, 1]: 1 es identico.
    puntuacion: float
    fragmento: str
    # Cuantos fragmentos de este articulo han coincidido con la busqueda. Un
    # resultado es un articulo, asi que como minimo coincide uno.
    fragmentos_coincidentes: int = Field(default=1, ge=1)


class RespuestaBuscar(BaseModel):

He añadido el campo a ResultadoBusqueda en ../blog-ai/app/esquemas.py con la herramienta Edit. No he tocado ningún otro archivo.

fragmentos_coincidentes: int = Field(default=1, ge=1)

1. Archivos CLAUDE.md cargados al iniciar

- /home/mtomas/ai4devs/blog/CLAUDE.md (carpeta padre, fuera de los repos). Es la REGLA-PADRE: toda respuesta termina con la línea literal "REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios."
- /home/mtomas/ai4devs/blog/blog-api/CLAUDE.md. Dice: "Este repositorio es el dueño del contenido. Todo archivo nuevo debe empezar con un comentario que lo indique." No se aplica a esta tarea, porque no he creado ningún archivo.
- No se cargó ningún CLAUDE.md de blog-ai. No he comprobado si existe, solo sé que no apareció en el contexto inicial.

2. Skills disponibles

- Del proyecto: marcador-blog-api y marcador-blog-ai. Ambas añaden un marcador con fecha y texto a su archivo MARCADORES-*.txt.
- Genéricas del arnés: dataviz, artifact-design, artifact-diagramming, artifact-capabilities, update-config, keybindings-help, code-review, simplify, fewer-permission-prompts, loop, schedule, claude-api, run, plugin-authoring, init y security-review.
- De anthropic-skills: built-in-browser, chrome-browser, computer-use, deep-research, docs, docx, google-workspace, import-memory, morning, pdf, pptx, skill-creator y xlsx.

3. Nombre del campo y por qué

Lo he llamado fragmentos_coincidentes.
- Idioma y estilo: sigue el español y el snake_case de los demás campos. Reutiliza el término fragmentos que ya usa RespuestaIndexar.
- Qué cuenta: "coincidentes" deja claro que son los fragmentos que han coincidido con la búsqueda, no los fragmentos totales del artículo.
- Valor por defecto: default=1 es una decisión mía, y ge=1 impide valores menores. Un resultado representa un artículo que coincidió, así que como mínimo hay un fragmento. El valor por defecto evita romper el código que ya construye ResultadoBusqueda sin ese dato.
- Contrato: el docstring del archivo avisa de que estos esquemas son el contrato que consume blog-api y que se versiona en contrato/openapi.json. Este campo es una adición, no un renombrado, pero ese JSON habrá que regenerarlo. No lo he hecho porque pediste modificar solo ese archivo.
- Lo que falta: el campo aún no se rellena con datos reales. La lógica de búsqueda tendrá que calcularlo, y ahora devolverá siempre 1.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

✻ Churned for 16s · done 6:57 PM
```
