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

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Analiza este repositorio sin modificar ningún archivo.

Explícame brevemente su estructura y localiza:

1. Archivos de instrucciones para agentes como CLAUDE.md o AGENTS.md.
2. Hooks o comprobaciones automáticas que se ejecuten al editar archivos o integrar cambios.
3. Skills, comandos o atajos del equipo.

Indica las rutas exactas. Si algo no existe, dilo explícitamente.

Comprueba también que puedes ejecutar comandos de solo lectura.
```

**Qué salió:** Al analizar el repositorio **blog-api**, Claude Code identificó que es una API desarrollada con AdonisJS y TypeScript, organizada en controladores, modelos, servicios, validadores y tests. Comprobó que no existen archivos de instrucciones para agentes como CLAUDE.md o AGENTS.md, ni hooks automáticos configurados. Encontró comprobaciones manuales mediante scripts de package.json y comandos del Makefile, como `make check`, `make test` y `make contrato`. Tampoco existen skills ni comandos propios de Claude Code dentro del repositorio, aunque hay algunas disponibles a través de plugins del usuario. Finalmente, confirmó que podía ejecutar comandos de solo lectura sin modificar ningún archivo.

---

## Prompt 2 - Sobre blog-ai

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Analiza este repositorio sin modificar ningún archivo.

Explícame brevemente su estructura y localiza:

1. Archivos de instrucciones para agentes como CLAUDE.md o AGENTS.md.
2. Hooks o comprobaciones automáticas que se ejecuten al editar archivos o integrar cambios.
3. Skills, comandos o atajos del equipo.

Indica las rutas exactas. Si algo no existe, dilo explícitamente.

Comprueba también que puedes ejecutar comandos de solo lectura.
```

**Qué salió:** Claude Code analizó el repositorio blog-ai y comprobó que es un backend desarrollado en Python con FastAPI, encargado de las funcionalidades de inteligencia artificial del blog. Confirmó que se encuentra en la rama s7/start y que no existen archivos de instrucciones para agentes como CLAUDE.md o AGENTS.md. Tampoco encontró hooks automáticos, configuraciones de CI ni skills propias del repositorio. Únicamente identificó comandos manuales definidos en el Makefile, como make check, make setup y make up. Las skills disponibles en la sesión proceden de plugins del usuario, no del proyecto. Finalmente, verificó que podía ejecutar comandos de solo lectura sin modificar ningún archivo.

---


## Prompt 3

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Necesito observar el alcance de los guardarraíles de Claude Code entre dos repositorios independientes: blog-api (directorio actual) y blog-ai (../blog-ai).

Configura los siguientes tres elementos en CADA repositorio:

**1. CLAUDE.md**

  - En blog-api, crea un CLAUDE.md en la raíz con una sola regla: "Este repositorio es el dueño del contenido y todo archivo nuevo debe comenzar con un
  comentario que lo indique".
  - En blog-ai, crea un CLAUDE.md en la raíz con una sola regla: "Los nombres de los campos del contrato público deben escribirse en español, nunca en
  inglés".

  No copies las reglas entre repositorios.

**2. Hook PostToolUse**

  Configura un hook PostToolUse en cada repositorio para las herramientas Write y Edit.

  Cada hook debe añadir una línea a su propio archivo de marcadores:
  - blog-api/MARCADORES-blog-api.txt
  - blog-ai/MARCADORES-blog-ai.txt

  Cada línea debe registrar la fecha y hora, el nombre de la herramienta utilizada y la ruta absoluta del archivo modificado.

  Utiliza rutas absolutas tanto para localizar los archivos de marcadores como para registrar los archivos modificados, incluso cuando estos estén fuera del
  repositorio al que pertenece el hook.

  Usa la configuración de hooks propia de Claude Code y los scripts auxiliares que sean estrictamente necesarios.

**3. Skill**

  Crea una skill de proyecto en cada repositorio:

  - blog-api: marcador-blog-api
  - blog-ai: marcador-blog-ai

  Utiliza la estructura .claude/skills/<nombre>/SKILL.md y añade una descripción que identifique claramente el repositorio al que pertenece cada skill.
  Rellena la skill siguiendo el standard de SKILLs con el frontmatter y el contenido del skill.

  **Restricciones importantes**

  - No modifiques blog-web.
  - No cambies código de aplicación, contratos ni tests.
  - No configures hooks o skills globales del usuario.
  - No hagas commits ni pushes.
  - No intentes corregir posibles problemas de alcance entre repositorios; necesitamos observarlos más adelante.
  - Si necesitas permiso para modificar ../blog-ai, solicítalo.

  Al terminar, enumera todos los archivos creados o modificados y explica brevemente cómo has configurado cada elemento.
```

**Qué salió:** Claude Code creó correctamente los tres elementos solicitados en ambos repositorios: un CLAUDE.md con una regla específica, un hook PostToolUse para registrar las operaciones Write y Edit, y una skill identificativa. Al revisar los resultados, comprobé que el hook de blog-api había registrado tres escrituras, incluidas modificaciones de archivos pertenecientes a blog-ai. Sin embargo, el archivo MARCADORES-blog-ai.txt todavía no existía, por lo que no había evidencia de ejecución del hook de blog-ai. Claude también aplicó la REGLA-PADRE, terminando su respuesta con la frase literal configurada fuera de los repositorios. No se modificó blog-web ni se realizaron commits.

---

## Prompt 4

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Quiero realizar un analisis sobre el alcance de los guardarraíles entre repositorios.

Estoy trabajando desde blog-api, con blog-ai añadido mediante --add-dir.

Modifica únicamente el archivo:

../blog-ai/app/esquemas.py

Localiza la clase ResultadoBusqueda y añade un campo que indique cuántos fragmentos de un artículo han coincidido con la búsqueda.

Condiciones:

1. Modifica exclusivamente ../blog-ai/app/esquemas.py.
2. Utiliza la herramienta Edit para realizar el cambio.
3. No utilices Bash, scripts de Python, sed ni ningún otro método para modificar archivos.
4. No modifiques hooks, skills, configuraciones ni archivos CLAUDE.md.
5. No hagas commits ni pushes.
6. Respeta las instrucciones que tengas cargadas en esta sesión.
7. No intentes solucionar posibles problemas de alcance de los guardarraíles.

Al terminar, indícame el nombre exacto del campo añadido, su tipo y por qué elegiste ese nombre.

El objetivo es observar qué reglas se aplican al editar un archivo de un repositorio añadido.
```

**Qué salió:** Claude Code modificó correctamente la clase ResultadoBusqueda del archivo blog-ai/app/esquemas.py utilizando la herramienta Edit. Añadió el campo fragmentos_coincidentes de tipo int, con valor por defecto 1 y un mínimo de 1, siguiendo la nomenclatura en español del esquema. También comprobé que el hook de blog-api registró esta modificación, aunque el archivo editado pertenecía a blog-ai. En cambio, no encontré el archivo de marcadores propio de blog-ai. Claude terminó su respuesta aplicando la REGLA-PADRE y no realizó commits ni pushes.

---

## Prompt 5

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
¿Qué archivos CLAUDE.md se cargaron al iniciar esta sesión de Claude Code?

Indica la ruta de cada archivo y cita la regla que contiene.

Distingue entre los archivos cuyas instrucciones se cargaron realmente en la sesión y los archivos que simplemente puedes consultar porque tienes acceso a sus directorios.

No modifiques ningún archivo.
```

**Qué salió:** Claude Code indicó que al iniciar la sesión se cargaron dos archivos de instrucciones: el CLAUDE.md de la carpeta padre blog/, que contiene la REGLA-PADRE, y el CLAUDE.md de blog-api, que establece que el repositorio es dueño del contenido y que los archivos nuevos deben comenzar con un comentario identificativo. Sin embargo, explicó que el CLAUDE.md de blog-ai no se cargó automáticamente, aunque tenía acceso a ese repositorio mediante --add-dir. También confirmó que la REGLA-PADRE estaba activa al finalizar su respuesta con la frase configurada. Esto muestra que tener acceso a otro repositorio no implica necesariamente cargar sus instrucciones automáticamente.

---

## Prompt 6

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
¿Qué skills tienes disponibles en esta sesión de Claude Code?

Enumera sus nombres e indica de dónde procede cada una, diferenciando entre:

1. Skills propias de blog-api.
2. Skills propias de blog-ai, añadido mediante --add-dir.
3. Skills globales o procedentes de plugins del usuario.

Distingue entre las skills realmente disponibles para utilizar en esta sesión y los archivos SKILL.md que simplemente podrías consultar.

No modifiques ningún archivo.
```

**Qué salió:** Claude Code indicó que tenía disponibles las dos skills creadas durante la práctica: marcador-blog-api, perteneciente al repositorio principal, y marcador-blog-ai, perteneciente al repositorio añadido mediante --add-dir. También enumeró otras skills globales, integradas y procedentes de plugins como Postman, mattpocock-skills y anthropic-skills. Confirmó que ambas skills propias aparecían en su listado de herramientas disponibles, aunque no había leído sus archivos SKILL.md. Esto muestra una diferencia interesante: según Claude, la skill de blog-ai estaba disponible, mientras que su archivo CLAUDE.md no se había cargado automáticamente al iniciar la sesión.

---

## Prompt 7

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
¿Qué nombre exacto has elegido para el nuevo campo de la clase ResultadoBusqueda en ../blog-ai/app/esquemas.py y por qué?

Explícame si elegiste ese nombre porque estabas siguiendo alguna instrucción CLAUDE.md cargada en esta sesión o simplemente por tu propio criterio y las convenciones existentes en el código.

Ten en cuenta la diferencia entre una regla realmente cargada y un archivo que podrías consultar, pero cuyas instrucciones no se cargaron automáticamente.

No modifiques ningún archivo.
```

**Qué salió:** Claude Code confirmó que había añadido el campo fragmentos_coincidentes, de tipo int y con Field(default=1, ge=1). Explicó que eligió ese nombre por criterio propio, siguiendo las convenciones existentes en el archivo, donde los campos utilizan nombres en español y snake_case. También indicó que ninguna instrucción CLAUDE.md había determinado el nombre, ya que la regla de blog-ai no se había cargado automáticamente en la sesión. Aunque el campo cumplía la regla de utilizar nombres en español, esto ocurrió sin que Claude declarase haber aplicado dicha instrucción. Finalmente, volvió a cumplir la REGLA-PADRE y no modificó ningún otro archivo.
