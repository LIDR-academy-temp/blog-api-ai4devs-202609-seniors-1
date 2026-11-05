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

---

## Prompt 1

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Responde únicamente: CONEXIÓN BEDROCK OK. No modifiques ningún archivo ni ejecutes comandos.
```

**Qué salió:** Respondió solo «CONEXIÓN BEDROCK OK», sin ejecutar herramientas.

## Prompt 2

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Inspecciona la configuración de Claude Code en este repositorio (blog-api).

Identifica:
1. Los archivos CLAUDE.md y su ubicación.
2. Las reglas disponibles en .claude/rules/.
3. Las skills disponibles en .claude/skills/.
4. Los hooks configurados y los eventos que los activan.

Para cada elemento, explica brevemente su propósito y alcance.

Esta es una inspección de solo lectura. No modifiques archivos, no instales dependencias ni ejecutes comandos que alteren el repositorio.
```

**Qué salió:** Inspección de solo lectura: informó de que blog-api no tenía ninguna configuración de Claude Code (ni CLAUDE.md, ni rules, ni skills, ni hooks).

## Prompt 3

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Lee el README.md y el archivo prompts.md de este repositorio (blog-api).

Identifica:
1. Qué instrucciones existen para realizar el Ejercicio 7.
2. Qué entregables se solicitan.
3. Qué formato debe utilizarse para registrar los prompts.
4. Si hay referencias a otros documentos con instrucciones del ejercicio.

No modifiques ningún archivo ni ejecutes operaciones de escritura.

Si las instrucciones del Ejercicio 7 no aparecen en estos archivos, indícalo explícitamente. No inventes requisitos.
```

**Qué salió:** Resumió las instrucciones del README (lección «Ejercicio Blog Polirepo» del Módulo 7, rama `s7/start`) y avisó de que el nombre «Ejercicio 7» no aparece literalmente.

## Prompt 4

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Lee el archivo contracts/LEEME.md de blog-api y revisa las referencias al contrato entre blog-api y blog-ai.

Explícame:
1. Cómo se comunican ambos servicios.
2. Qué endpoints o contratos existen actualmente.
3. Qué restricciones debemos respetar al introducir un endpoint nuevo.
4. Qué cambio mínimo recomendarías para probar una regla de proceso en TypeScript y Python.

No modifiques ningún archivo ni ejecutes operaciones de escritura. No implementes todavía la propuesta.
```

**Qué salió:** Explicó que los servicios se comunican por HTTP/JSON a través de `app/services/blog_ai_service.ts` y detectó que la validación estricta del contrato estaba desactivada en el `.env` local. No modificó archivos.

## Prompt 5

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Estamos realizando el Ejercicio Blog Polirepo.

Propongo esta única regla de proceso:

"Toda función nueva de lógica de negocio debe incluir inmediatamente encima el comentario REGLA-FRONTERA: validada, tanto en TypeScript como en Python".

Diseña una estrategia mínima para:
1. Hacer cumplir la regla trabajando desde blog-api.
2. Aplicarla en un cambio pequeño que involucre blog-api y blog-ai.
3. Repetir la prueba iniciando una sesión nueva desde blog-ai.
4. Identificar exactamente cuándo y por qué la regla deja de aplicarse.
5. Señalar qué mecanismo concreto garantiza su cumplimiento en ambos repositorios.

Compara brevemente CLAUDE.md, rules, skills y hooks, y recomienda el mecanismo más adecuado para este ejercicio.

Por ahora, no crees ni modifiques archivos. No implementes código. Solo presenta el plan.
```

**Qué salió:** Propuso acotar la regla a `app/services/` y `app/servicios/` y recomendó un hook `PostToolUse` por repositorio como mecanismo de garantía, empezando con una primera ronda solo con CLAUDE.md.

## Prompt 6

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Vamos a ejecutar la Fase A del Ejercicio Blog Polirepo.

Crea únicamente el archivo CLAUDE.md en la raíz de blog-api.

Incluye esta regla de proceso:

"Toda función o método nuevo creado en app/services/ de blog-api o app/servicios/ de blog-ai debe llevar inmediatamente encima el comentario REGLA-FRONTERA: validada".

Utiliza la sintaxis de comentario apropiada para cada lenguaje:
- TypeScript: // REGLA-FRONTERA: validada
- Python: # REGLA-FRONTERA: validada

Indica expresamente que la regla debe aplicarse también cuando, trabajando desde blog-api, se modifiquen archivos del repositorio hermano ../blog-ai.

No crees hooks, skills ni scripts todavía.
No modifiques archivos de aplicación.
No hagas commits ni push.

Al finalizar, muestra el contenido completo de CLAUDE.md y los archivos modificados.
```

**Qué salió:** Creó únicamente `CLAUDE.md` en la raíz de blog-api con la regla REGLA-FRONTERA.

## Prompt 7

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Sin modificar archivos ni ejecutar comandos, responde:

1. ¿Qué instrucciones de proyecto tienes cargadas desde CLAUDE.md?
2. ¿Cuál es la regla REGLA-FRONTERA?
3. ¿En qué repositorios y carpetas debe aplicarse?
4. ¿Qué comentario exacto debe aparecer antes de cada función o método nuevo en TypeScript y Python?

Responde únicamente con las instrucciones que realmente tienes disponibles. No supongas ni inventes configuraciones.
```

**Qué salió:** Sesión nueva desde blog-api: confirmó que tenía cargado `blog-api/CLAUDE.md` y describió la regla, su alcance y los comentarios exactos.

## Prompt 8

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Realiza la primera prueba del Ejercicio Blog Polirepo.

Implementa un cambio mínimo que involucre ambos repositorios:

1. En blog-ai, crea un endpoint GET /indexado/{slug} que consulte si existe contenido indexado para un slug, reutilizando la lógica disponible.
2. En blog-api, crea un endpoint GET /posts/:slug/indexado que consuma el endpoint de blog-ai mediante BlogAiService.
3. Respeta los contratos existentes y las convenciones de cada proyecto.
4. Aplica las instrucciones de proyecto que tienes cargadas, también cuando modifiques el repositorio hermano blog-ai.
5. Añade únicamente las pruebas mínimas necesarias y ejecútalas cuando sea posible.

No crees nuevos archivos CLAUDE.md, reglas, skills ni hooks.
No modifiques prompts.md ni docs/frontera.md todavía.
No hagas commits ni push.

Al terminar, muestra los archivos modificados, los resultados de las pruebas y el diff de las funciones o métodos nuevos en ambos repositorios.
```

**Qué salió:** Creó `GET /indexado/{slug}` en blog-ai y `GET /posts/:slug/indexado` en blog-api; las funciones nuevas de `app/services/` y `app/servicios/` llevaban el comentario REGLA-FRONTERA. Las pruebas nuevas pasaron; `npm test` en blog-api mantuvo 1 fallo que ya existía antes del cambio.

## Prompt 9

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Antes de comenzar la Fase B del Ejercicio Blog Polirepo, revisa el estado Git de blog-api y ../blog-ai.

Indica:
1. Qué archivos fueron modificados o creados en cada repositorio.
2. Cuáles contienen funciones o métodos nuevos con REGLA-FRONTERA: validada.
3. Si hay cambios sin guardar o archivos sin seguimiento.
4. Cómo podríamos realizar una segunda prueba equivalente desde blog-ai sin borrar ni sobrescribir el trabajo de la Fase A.

No modifiques archivos, no restaures cambios, no hagas commits ni push. Solo informa.
```

**Qué salió:** Informó del estado Git de ambos repositorios (6 archivos modificados y `CLAUDE.md` sin seguimiento en blog-api; 4 modificados y 2 sin seguimiento en blog-ai) sin modificar nada.

## Prompt 10

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-ai

```
Estamos realizando la Fase B del Ejercicio Blog Polirepo.

Sin leer archivos de otros repositorios, sin modificar archivos y sin ejecutar comandos, responde:

1. ¿Qué archivos CLAUDE.md o instrucciones de proyecto tienes cargados automáticamente en esta sesión?
2. ¿Tienes cargada alguna regla de proceso llamada REGLA-FRONTERA?
3. ¿Existe alguna instrucción cargada que te obligue a añadir un comentario específico antes de crear funciones nuevas?
4. ¿De qué repositorio procede cada instrucción que tienes disponible?

Distingue entre instrucciones cargadas automáticamente y cualquier información que puedas conocer por otros medios.

No busques ni leas el archivo ../blog-api/CLAUDE.md. No supongas reglas que no estén presentes en tu contexto.
```

**Qué salió:** Sesión nueva desde blog-ai: respondió que no tenía cargado ningún CLAUDE.md ni la regla REGLA-FRONTERA.

## Prompt 11

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-ai

```
En este repositorio blog-ai, añade una función nueva llamada contar_fragmentos_por_slug(slug: str) -> int en app/servicios/indice.py.

La función debe reutilizar la conexión y la tabla de fragmentos existentes para devolver el número de fragmentos asociados al slug. No modifiques las funciones existentes salvo que sea imprescindible.

Respeta las convenciones de código que tengas cargadas automáticamente en esta sesión.

No consultes archivos del repositorio hermano ../blog-api.
No crees archivos CLAUDE.md, reglas, skills ni hooks.
No modifiques otros repositorios.
No hagas commits ni push.

Al terminar, muestra el diff de app/servicios/indice.py y explica qué pruebas ejecutaste.
```

**Qué salió:** Añadió `contar_fragmentos_por_slug()` en `app/servicios/indice.py` **sin** el comentario `# REGLA-FRONTERA: validada`. `py_compile` y los 2 tests existentes pasaron (ninguno usa la función nueva); prueba de humo con mock correcta; no se probó contra PostgreSQL.

## Prompt 12

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-ai

```
Hemos terminado la Fase B del Ejercicio Blog Polirepo.

Resume brevemente la evidencia observada en esta sesión:
1. Qué instrucciones de proyecto estaban cargadas al iniciar desde blog-ai.
2. Qué función nueva se creó y en qué archivo.
3. Si aparece inmediatamente encima el comentario REGLA-FRONTERA: validada.
4. Qué pruebas se ejecutaron y sus resultados.

No modifiques ningún archivo, no corrijas la función, no hagas commits ni push. Conserva el incumplimiento como evidencia del experimento.
```

**Qué salió:** Resumió la evidencia: sin instrucciones de proyecto cargadas y función nueva sin el comentario obligatorio. No modificó archivos.

## Prompt 13

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Crea el archivo docs/frontera.md en este repositorio blog-api, creando la carpeta docs si no existe.

El archivo debe contener exactamente estas dos frases, sin títulos, listas ni explicaciones adicionales:

Hice que la regla REGLA-FRONTERA se cumpliera mediante el archivo CLAUDE.md de blog-api, que Claude Code cargó al iniciar desde ese repositorio y aplicó a las funciones nuevas de TypeScript y Python, incluso al modificar el repositorio hermano blog-ai.

La regla dejó de aplicarse al iniciar una sesión nueva desde blog-ai, porque no se cargó el CLAUDE.md de blog-api; lo comprobé cuando Claude creó la función contar_fragmentos_por_slug() en app/servicios/indice.py sin el comentario obligatorio REGLA-FRONTERA: validada inmediatamente encima.

No modifiques ningún otro archivo.
No corrijas la función de blog-ai, porque necesitamos conservar la evidencia del incumplimiento.
No hagas commits ni push.

Al terminar, muestra el contenido completo de docs/frontera.md y el estado Git del archivo.
```

**Qué salió:** Creó `docs/frontera.md` con las dos frases indicadas, tras comprobar que la función de blog-ai existía sin el comentario.

## Prompt 14

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Necesito completar prompts.md para el Ejercicio Blog Polirepo.

Antes de modificar archivos, investiga si puedes recuperar los mensajes originales enviados por el usuario a Claude Code durante las sesiones de este ejercicio, tanto desde blog-api como desde blog-ai.

Comprueba si el historial local de Claude Code conserva:
- El texto literal de cada prompt.
- El orden cronológico.
- El modelo utilizado.
- La información de la sesión y el repositorio de origen.

Distingue claramente los prompts originales recuperables de cualquier texto que tendrías que reconstruir.

No muestres ni leas valores de tokens, claves, credenciales o variables de autenticación.
No modifiques archivos.
No escribas todavía prompts.md.
No hagas commits ni push.

Indica qué información puede recuperarse de manera fiable y cómo podríamos utilizarla para completar prompts.md.
```

**Qué salió:** Confirmó que el historial local conserva el texto literal, el orden, el modelo y la sesión/repositorio de los 14 prompts hasta ese momento. No modificó archivos.

## Prompt 15

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Completa el archivo prompts.md de blog-api utilizando los mensajes originales del historial local de Claude Code que acabas de identificar.

Requisitos:

1. Recupera el texto literal de los prompts de las cuatro sesiones del Ejercicio Blog Polirepo, respetando su orden cronológico, saltos de línea y contenido original.
2. Incluye también este prompt actual como último registro.
3. Usa un apartado ## Prompt N para cada mensaje.
4. En cada apartado incluye:
   - **Modelo:** Claude Opus 5.5 (Amazon Bedrock), según los metadatos recuperados.
   - **Herramienta:** Claude Code.
   - **Repositorio:** blog-api o blog-ai, según corresponda.
   - El texto original completo del prompt dentro de un bloque de código.
   - **Qué salió:** una descripción breve y factual del resultado, cuando pueda verificarse.
5. Elimina el ejemplo de la plantilla original.
6. No inventes textos, resultados ni niveles de esfuerzo que no estén registrados.
7. No incluyas credenciales, tokens ni valores de variables de autenticación.

Modifica únicamente prompts.md. No alteres docs/frontera.md, CLAUDE.md ni el código de ninguno de los repositorios.

No hagas commits ni push.

Al terminar, informa cuántos prompts registraste, de qué sesiones proceden y muestra el estado Git de prompts.md, sin reproducir nuevamente todos los prompts en pantalla.
```

**Qué salió:** Generó este archivo `prompts.md` a partir del historial local de Claude Code.

## Prompt 16

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
──
```

**Qué salió:** Mensaje sin contenido: solo contiene el separador `──`, registrado tal cual en el historial. Claude respondió que había llegado vacío y resumió el estado de las tareas.

## Prompt 17

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Realiza una validación final de blog-api antes de preparar el commit del Ejercicio Blog Polirepo.

Ejecuta node ace test y reporta:
1. Número de pruebas exitosas y fallidas.
2. Nombre y causa de cada prueba fallida.
3. Si el fallo está relacionado con los cambios del ejercicio o ya existía anteriormente, indicando la evidencia disponible.
4. Si las pruebas nuevas del endpoint GET /posts/:slug/indexado pasan correctamente.

No modifiques ningún archivo.
No corrijas errores todavía.
No hagas commits ni push.
No modifiques la evidencia conservada en blog-ai.
```

**Qué salió:** Ejecutó `node ace test`: 22 pruebas OK y 1 fallo (setup de «Regla 6 — GET /posts no devuelve ningun correo», `contrato_verificar.js` rechazado con «Invalid URL»). Según el historial de la sesión `4482141f`, el fallo ya existía antes de los cambios del ejercicio (20 OK y 1 fallo con los cambios apartados con `git stash`). Las 2 pruebas nuevas del indexado pasaron. No modificó archivos.

## Prompt 18

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Prepara una revisión final de los archivos para el pull request del Ejercicio Blog Polirepo.

Estamos en blog-api, rama frontera-dm.

Revisa únicamente, sin modificar archivos:

1. El estado Git completo de blog-api.
2. El estado Git completo de ../blog-ai.
3. Qué archivos de blog-api son necesarios para demostrar la regla, la integración entre repositorios y los entregables.
4. Qué archivos modificados pertenecen únicamente a la experimentación de la Fase B.
5. Si docs/frontera.md contiene exactamente dos frases.
6. Si prompts.md incluye los prompts originales recuperados, incluido el prompt más reciente de validación de pruebas, o si falta registrar alguno.

Propón exactamente qué archivos incluirías en el commit de blog-api y señala cualquier dependencia que pudiera quedar fuera del pull request.

No modifiques archivos, no hagas git add, commits, push ni operaciones de restauración.
```

**Qué salió:** Revisó el estado Git de ambos repositorios, confirmó que `docs/frontera.md` tiene dos frases, detectó que faltaban prompts en `prompts.md` y propuso los 9 archivos del commit de blog-api, señalando la dependencia de los cambios sin commitear de blog-ai. No modificó archivos.

## Prompt 19

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Actualiza únicamente prompts.md de blog-api usando el historial local original de Claude Code.

Conserva los 15 prompts ya registrados y agrega, en orden cronológico, todos los mensajes de usuario posteriores que falten, incluido este prompt actual.

Requisitos:
- Recupera el texto literal, sin reconstruirlo ni modificarlo.
- Conserva los saltos de línea originales.
- Mantén el formato ## Prompt N, Modelo, Herramienta, Repositorio, bloque de código y Qué salió.
- Si existe un mensaje vacío registrado, consérvalo e identifícalo como tal, sin inventar contenido.
- No incluyas credenciales ni tokens.
- Comprueba que el número de entradas coincida con los mensajes originales recuperados.

No modifiques ningún otro archivo.
No hagas git add, commit ni push.

Al finalizar, informa cuántos prompts contiene prompts.md y cuál es el último registrado.
```

**Qué salió:** Actualizó este archivo `prompts.md`, añadiendo los prompts 16 a 19 desde el historial local de Claude Code.

## Prompt 20

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Vamos a preparar la conservación de los cambios del Ejercicio Blog Polirepo en el repositorio hermano blog-ai.

Antes de hacer cualquier modificación, comprueba:
1. La rama actual y el estado Git de ../blog-ai.
2. Si existe ya una rama llamada frontera-dm en ese repositorio.
3. Si podemos crear esa rama desde el estado actual sin perder los cambios sin commit.
4. Qué archivos quedarían pendientes de incluir en un futuro commit.

No crees todavía la rama.
No modifiques archivos.
No hagas git add, commit, push ni operaciones de restauración.
No alteres la evidencia de la Fase B.

Informa únicamente del resultado y de los riesgos que debamos considerar.
```

**Qué salió:** Comprobó, sin modificar nada, que blog-ai estaba en `s7/start` al día con el remoto, que no existía ninguna rama `frontera-dm` en local ni en el remoto y que la rama podía crearse sin perder los 6 cambios sin commit; enumeró los riesgos.

## Prompt 21

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Crea únicamente la rama local frontera-dm en el repositorio hermano ../blog-ai, partiendo de su rama actual s7/start.

Utiliza git switch -c frontera-dm dentro de ../blog-ai.

Después comprueba:
1. Que la rama activa de blog-ai es frontera-dm.
2. Que los seis archivos modificados o nuevos siguen presentes.
3. Que la función contar_fragmentos_por_slug() conserva la ausencia del comentario REGLA-FRONTERA: validada.
4. Que blog-api permanece en su propia rama frontera-dm.

No modifiques el contenido de ningún archivo.
No hagas git add, commits ni push.
No ejecutes operaciones de restauración ni limpieza.
```

**Qué salió:** Creó la rama local `frontera-dm` en blog-ai con `git switch -c frontera-dm` desde `18a3a99`; los 6 archivos se mantuvieron idénticos (md5) y `contar_fragmentos_por_slug()` siguió sin el comentario. blog-api siguió en su rama `frontera-dm`.

## Prompt 22

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Prepara y crea un commit local en el repositorio hermano ../blog-ai, actualmente en la rama frontera-dm.

Incluye únicamente estos seis archivos:

- app/esquemas.py
- app/main.py
- app/servicios/indice.py
- contrato/openapi.json
- tests/__init__.py
- tests/test_indexado.py

Antes de hacer el commit:
1. Comprueba que los seis archivos existen.
2. Verifica que app/servicios/indice.py conserva la función contar_fragmentos_por_slug() sin el comentario REGLA-FRONTERA: validada.
3. Comprueba que no hay credenciales ni archivos de entorno entre los seis archivos.
4. Añade únicamente esos seis archivos al staging area.

Crea el commit con el mensaje:

frontera: integración blog-ai y evidencia de la fase B

Después muestra:
- El hash corto del commit.
- La rama activa.
- Los archivos incluidos.
- El resultado de git status --short.

No modifiques el contenido de ningún archivo.
No ejecutes formateadores.
No hagas push.
No alteres blog-api ni blog-web.
```

**Qué salió:** Creó en blog-ai el commit local `b27c4e7` en `frontera-dm` con los 6 archivos indicados (+128 líneas), tras comprobar la evidencia de la Fase B y que no había credenciales; añadió la línea `Co-Authored-By` de Claude al mensaje. Árbol limpio y sin push.

## Prompt 23

**Modelo:** Claude Opus 5.5 (Amazon Bedrock)
**Herramienta:** Claude Code
**Repositorio:** blog-api

```
Vamos a preparar el commit final del Ejercicio Blog Polirepo en blog-api, rama frontera-dm.

Primero, actualiza únicamente prompts.md recuperando del historial local de Claude Code todos los prompts originales que todavía no estén registrados, incluido este mensaje. Conserva su texto literal, orden cronológico y saltos de línea. No inventes contenido ni incluyas credenciales.

Después, revisa estos nueve archivos:

1. CLAUDE.md
2. docs/frontera.md
3. prompts.md
4. app/controllers/busqueda_controller.ts
5. app/services/blog_ai_service.ts
6. contracts/blog-ai.openapi.json
7. start/routes.ts
8. tests/functional/reglas_del_dominio.spec.ts
9. tests/unit/contrato.spec.ts

Comprueba que:
- docs/frontera.md contiene exactamente dos frases.
- CLAUDE.md conserva la regla REGLA-FRONTERA.
- prompts.md contiene todos los prompts recuperables hasta este mensaje.
- No se incluyen credenciales ni archivos de entorno.
- Los nueve archivos corresponden al ejercicio.

Añade al staging area únicamente esos nueve archivos.

No crees todavía el commit.
No hagas push.
No modifiques blog-ai ni blog-web.
No ejecutes formateadores ni corrijas el código.

Al finalizar, muestra el número de prompts registrados, los nueve archivos preparados y el resultado de git diff --cached --stat.
```

**Qué salió:** Actualizó este archivo `prompts.md` con los prompts 20 a 23 y añadió al staging de blog-api los nueve archivos del ejercicio, sin crear el commit.
