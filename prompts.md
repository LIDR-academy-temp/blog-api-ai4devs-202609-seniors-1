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
Guarda cada prompt que te pida, así como el resultado de su ejecución, incluyendo este, en el archivo `prompts.md`. Fíjate en el ejemplo para saber la estructura
```

**Qué salió:** leí `prompts.md`, borré el ejemplo y registré este prompt con la estructura indicada (modelo, herramienta, prompt tal cual, qué salió). Funcionó a la primera.

## Prompt 2

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
crea lo siguiente y nada más que lo que se pide. Sin cambiar nada más. Tanto en este proyecto como en `blog-ai` (`~/projects/blog/blog-ai`):
* Un CLAUDE.md en la raíz con una sola regla propia del repositorio. En blog-api: este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique. En blog-ai: los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. Las reglas son distintas para poder reconocer después cuál se aplicó.
* Un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Pide que use rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio.
* Una skill sencilla llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece.
```

**Qué salió:** en cada repo: `CLAUDE.md` con una regla, `.claude/settings.json` + `.claude/hooks/marcador.sh` (PostToolUse Write|Edit, rutas absolutas) y `.claude/skills/marcador-<repo>/SKILL.md`. Probé el hook a mano en blog-api y escribió la línea esperada (borré el archivo de prueba).

## Prompt 3

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Guarda cada prompt que te pida, así como el resultado de su ejecución, incluyendo este, en el archivo prompts.md. Fíjate en el ejemplo para saber la estructura y añade los prompts al final
```

**Qué salió:** `prompts.md` ya tenía los prompts 1 y 2 con la estructura indicada, así que no rehice nada y añadí este al final como `Prompt 3`.

## Prompt 4

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Debes modificar únicamente ese archivo usando la herramienta de edición de archivos. Nunca un script
```

**Qué salió:** añadí `fragmentos_coincidentes: int = Field(default=1, ge=1)` a `ResultadoBusqueda` con la herramienta de edición, sin tocar nada más. Quedan pendientes el código que construye los resultados y regenerar `contrato/openapi.json`. Este prompt no se registró en su momento por la restricción de modificar solo ese archivo; se añade ahora.

## Prompt 5

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno.
```

**Qué salió:** listé los dos `CLAUDE.md` cargados (el de la carpeta padre y el de `blog-api`) citando su regla.

## Prompt 6

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Qué skills tiene disponibles.
```

**Qué salió:** listé las skills disponibles en la sesión, agrupadas por tipo, empezando por la del repositorio (`marcador-blog-api`).

## Prompt 7

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Qué nombre has dado al campo y por qué
```

**Qué salió:** expliqué que el campo se llama `fragmentos_coincidentes` y las razones del nombre y del valor por defecto.
