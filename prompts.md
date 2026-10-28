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

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Necesito configurar reglas, hooks y skills para comprobar cómo se aplican las instrucciones dentro de cada repositorio y desde el directorio padre.

1. Repositorios y estructura

El directorio de trabajo es ~/blog y contiene estos repositorios:

blog-api

blog-ai

blog-web

Trabajaremos principalmente con blog-api y blog-ai. Antes de realizar cualquier cambio, revisa la estructura real de directorios y los archivos de configuración existentes, incluyendo CLAUDE.md, .claude/settings.json, hooks y skills.

No inventes archivos, rutas, configuraciones ni resultados. Si algo no existe o no puedes comprobarlo, indícalo explícitamente.

2. Regla del directorio padre

En ~/blog/CLAUDE.md debe existir una regla que indique que toda respuesta debe terminar con la siguiente línea literal:

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

Este archivo debe permanecer fuera de los repositorios Git individuales.

3. Regla específica de blog-api

Crea blog-api/CLAUDE.md con una regla que establezca que este repositorio es responsable del contenido y que todo archivo nuevo creado en él debe comenzar con un comentario que indique que pertenece a blog-api.

La regla debe ser clara y aplicable a los archivos nuevos. No modifiques archivos de aplicación que no sean necesarios para configurar esta regla.

4. Regla específica de blog-ai

Crea blog-ai/CLAUDE.md con una regla que establezca que los nombres de los campos de los contratos públicos deben estar en español y nunca en inglés.

La regla debe ser explícita y aplicable al código nuevo o modificado que defina contratos públicos.

5. Hooks para registrar modificaciones

Configura en cada repositorio un hook PostToolUse que se ejecute después del uso de las herramientas Write y Edit.

En blog-api, el hook debe registrar las modificaciones en:

blog-api/MARCADORES-blog-api.txt

En blog-ai, el hook debe registrar las modificaciones en:

blog-ai/MARCADORES-blog-ai.txt

Cada línea del registro debe incluir:

Fecha y hora.

Nombre de la herramienta utilizada.

Ruta del archivo modificado.

Utiliza scripts de hook independientes para cada repositorio y configura las rutas de acuerdo con la estructura real del proyecto. El mecanismo debe permitir registrar las modificaciones de archivos fuera del repositorio cuando el evento proporcione la información necesaria.

Los scripts deben escribir los registros mediante operaciones de shell, sin utilizar las herramientas Write o Edit para actualizar sus propios archivos de marcadores, a fin de evitar recursión.

No crees manualmente archivos de marcadores para simular una ejecución. Deben servir como evidencia de las ejecuciones reales del hook.

6. Skills específicas por repositorio

Crea las siguientes skills:

marcador-blog-api: su nombre y descripción deben indicar claramente que corresponde al repositorio blog-api.

marcador-blog-ai: su nombre y descripción deben indicar claramente que corresponde al repositorio blog-ai.

Revisa la estructura de skills admitida por la versión y configuración existentes de Claude Code. Colócalas donde corresponda y no afirmes que están disponibles para el agente sin comprobarlo.

7. Validación y restricciones

Antes de modificar archivos:

Inspecciona las configuraciones y reglas existentes.

Identifica los cambios necesarios.

Evita sobrescribir instrucciones que no estén relacionadas con esta actividad.

Informa qué archivos crearás o modificarás.

Después de los cambios:

Muestra qué archivos quedaron creados o modificados.

Explica cómo se configura cada hook y qué archivo de marcadores le corresponde.

Indica cómo comprobar que las skills están disponibles.

Distingue entre archivos existentes, configuraciones declaradas y comportamientos que se hayan probado realmente.

No declares que un hook funciona hasta haber comprobado su ejecución mediante una modificación real con Write o Edit.

Si no puedes verificar algo, indícalo y proporciona el siguiente paso para comprobarlo.

No realices cambios adicionales fuera del alcance descrito sin consultarme previamente.
```

## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea un archivo temportal de prueba dentro de blog-api, utilizando la herramienta Write
```

**Qué salió:** funcionó a la primera; creó `prueba-temporal.txt` con el comentario de pertenencia a blog-api.

## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Necesito probar el hook PostToolUse configurado en este repositorio.

Utiliza la herramienta Write para crear un archivo temporal llamado `PRUEBA-HOOK-TEMPORAL.md` en la raíz de `blog-api`.

El archivo debe contener una sola línea que diga: "Prueba temporal del hook de registro".

No modifiques ningún otro archivo, no ejecutes comandos para crear el archivo y no elimines el archivo temporal todavía. Después de crearlo, indícame qué herramienta utilizaste y qué archivo modificaste.
```

**Qué salió:** creó el archivo con Write; la "sola línea" chocaba con la regla de blog-api y metió el comentario de pertenencia en la misma línea.

## Prompt 4

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Necesito validar las reglas y skills configuradas para este ejercicio.

Indica qué archivos CLAUDE.md tienes cargados o reconoces como instrucciones aplicables en esta sesión. Para cada archivo, cita la regla concreta que estás aplicando. Distingue entre archivos que puedes verificar y archivos cuya carga efectiva no puedes confirmar.

Indica qué skills están disponibles en esta sesión y explica cuáles corresponden a blog-api y cuáles a blog-ai. No afirmes que una skill está disponible si no puedes comprobarlo.

Revisa ../blog-ai/app/esquemas.py y localiza la clase ResultadoBusqueda.

Propón el nombre en español de un campo que indique cuántos fragmentos de artículos coincidieron con la búsqueda y explica brevemente por qué ese nombre es adecuado.

Todavía no modifiques ningún archivo. No inventes información ni afirmes haber leído o cargado archivos que no hayas podido verificar.
```

**Qué salió:** Claude indicó que reconoció y aplicó ~/blog/CLAUDE.md y blog-ai/CLAUDE.md. Identificó marcador-blog-ai y otras skills disponibles, pero declaró que no había propuesto ningún campo para ResultadoBusqueda ni abierto app/esquemas.py en esa conversación.

## Prompt 5

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
Quiero probar el hook PostToolUse de este repositorio.

Utiliza la herramienta Write para crear en la raíz de este repositorio un archivo temporal llamado `PRUEBA-HOOK-BLOG-AI-20261027.md`, con una sola línea que diga: "Prueba temporal del hook propio de blog-ai".

No modifiques ningún otro archivo, no ejecutes comandos de shell para crear el archivo y no elimines el archivo temporal todavía. Al terminar, indica qué herramienta utilizaste y qué archivo creaste.
```

**Qué salió:** creó `PRUEBA-HOOK-BLOG-AI-20261027.md` con Write. El hook no mostró salida en la conversación, pero dejó la línea en `MARCADORES-blog-ai.txt` (17:50:42).

## Prompt 6

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
gUARDA EL PROMT
```

**Qué salió:** guardó el prompt 5 tal cual en `blog-ai/.claude/prompts/prueba-hook-posttooluse.md`; el prompt no decía dónde, así que eligió la ruta.

## Prompt 7

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
¿Qué archivos CLAUDE.md dijo haber cargado o reconocido?



¿Qué skills indicó que estaban disponibles?



¿Qué nombre propuso para el campo de ResultadoBusqueda y por qué?
```

**Qué salió:** Claude indicó que reconoció y aplicó ~/blog/CLAUDE.md y blog-ai/CLAUDE.md. Identificó marcador-blog-ai y otras skills disponibles, pero declaró que no había propuesto ningún campo para ResultadoBusqueda ni abierto app/esquemas.py en esa conversación.

## Prompt 8

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
puedes guardsar el siguiente texto en docs/frontera.md: Claude informó que reconoció y aplicó ~/blog/CLAUDE.md y blog-ai/CLAUDE.md, identificó la skill marcador-blog-ai junto con las skills generales y de anthropic-skills, y declaró que no había propuesto un campo para ResultadoBusqueda ni abierto los archivos relacionados.

El registro MARCADORES-blog-api.txt muestra que el hook de blog-api registró operaciones Write y Edit, incluidas modificaciones en archivos de blog-ai, mientras que MARCADORES-blog-ai.txt registra la creación de su archivo de prueba, lo que evidencia que cada hook se ejecuta según la configuración del proyecto activo y que el hook de blog-api también puede registrar ediciones realizadas fuera de su repositorio.
```

**Qué salió:** guardó el texto, pero en `blog-ai/docs/frontera.md`: la ruta relativa se resolvió contra el repositorio de la sesión, no contra blog-api.

## Prompt 9

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
sí, lee los registros y compruébalo
```

**Qué salió:** confirmó el texto con los dos registros y los scripts de hook, y añadió dos precisiones: el registro de blog-ai ya tenía más entradas que la de la prueba, y `contrato/openapi.json` estaba modificado sin aparecer en ningún registro.

## Prompt 10

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
el que creaste debe quedar aqui: blog-api/docs/frontera.md, valida si no es asi y ajusta lo necesario
```

**Qué salió:** movió el archivo a `blog-api/docs/frontera.md` con `mv` y borró `blog-ai/docs/`. Al ser un comando de shell, ningún hook registró el traslado.

## Prompt 11

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
añade las dos precisiones a frontera.md
```

**Qué salió:** no funcionó: se denegó la lectura de blog-api, fuera de los directorios de trabajo de la sesión. Propuso el texto para añadirlo a mano.

## Prompt 12

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
en blog-api/prompts.md, busca esto: Qué salió: distinguió CLAUDE.md cargados (padre, blog-api) del de blog-ai (leído en disco, carga no confirmada); propuso fragmentos_coincidentes, avisando de que falta definir el umbral de "coincidir". y reemplazalo por: Qué salió: Claude indicó que reconoció y aplicó ~/blog/CLAUDE.md y blog-ai/CLAUDE.md. Identificó marcador-blog-ai y otras skills disponibles, pero declaró que no había propuesto ningún campo para ResultadoBusqueda ni abierto app/esquemas.py en esa conversación.
```

**Qué salió:** no funcionó: se denegó la lectura de blog-api. Avisó de que el texto actual describe el resultado de la sesión de blog-api y el nuevo, el de la sesión de blog-ai.

## Prompt 13

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
Por favor identifica donde se ejecutaron estos dos promtp que llevan esta actividad: 

La modificación de ../blog-ai/app/esquemas.py.



La prueba del hook de blog-ai, que creó PRUEBA-HOOK-BLOG-AI-20261027.md.

 y agregalo al promps
```

**Qué salió:** lo identificó con los registros de marcadores; no pudo agregarlo porque se denegó la lectura de blog-api.

- La modificación de ../blog-ai/app/esquemas.py (17:41:27) se ejecutó en la sesión abierta en blog-api: solo la registró MARCADORES-blog-api.txt.
- La prueba del hook de blog-ai, que creó PRUEBA-HOOK-BLOG-AI-20261027.md (17:50:42), se ejecutó en la sesión abierta en blog-ai: solo la registró MARCADORES-blog-ai.txt.

## Prompt 14

**Modelo:** Opus 5.5
**Herramienta:** Claude Code (sesión abierta en blog-ai)

```
gusrda los prompts aqui: ~/blog/blog-api/prompts.md
```

**Qué salió:** con el acceso a blog-api ya permitido, añadió los prompts 5 a 14 a este archivo y las precisiones pendientes a `docs/frontera.md`.

## Pull request

https://github.com/LIDR-academy-temp/blog-api-ai4devs-202609-seniors-1/pull/9
