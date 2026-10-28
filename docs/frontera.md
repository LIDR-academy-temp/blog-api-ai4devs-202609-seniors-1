# La frontera entre repositorios — lo observado

> Práctica del M7 sobre `blog-api` y `blog-ai`, con la sesión iniciada desde `blog-api` y
> `../blog-ai` añadido con `--add-dir`. En **manual mode**, no en aceptación automática.

## Las dos frases

**1 · Qué dijo el agente en el paso 4.** Dijo haber cargado **dos** `CLAUDE.md` —el de
`C:\Proyectos\blog\` con la REGLA-PADRE y el de `blog-api` con la REGLA-API— y añadió por su cuenta
que **un tercero, el de `blog-ai`, «no se cargó al iniciar»** y que lo leyó durante la tarea;
declaró **siete skills de proyecto, entre ellas `marcador-blog-api` y `marcador-blog-ai` a la vez**,
señalando que *«se cargaron skills de ambos repositorios, no solo del directorio de trabajo
primario»*; y llamó al campo **`fragmentos_coincidentes`**, en español y `snake_case`, porque **la
REGLA-AI de `blog-ai` lo prescribe literalmente** como ejemplo de buen nombre.

**2 · Qué había en cada archivo de marcadores.** `MARCADORES-blog-api.txt` tiene **una sola línea**
—`2026-10-28T16:57:13.027Z | Edit | C:\Proyectos\blog\blog-ai\app\esquemas.py`— y
`MARCADORES-blog-ai.txt` **no existe**: no está vacío, es que nunca se creó. Es decir, **el hook que
se ejecutó fue el del repositorio desde el que arranqué la sesión, y registró una edición hecha en
el otro repositorio**, mientras que el hook del repositorio añadido **no llegó a dispararse ni una
vez** aunque el archivo editado fuera suyo: **un guardarraíl protege desde donde arrancas, no donde
editas**.

---

## El detalle que no esperaba: las tres piezas no se comportan igual

Monté lo mismo en los dos repositorios —instrucciones, hook y skill— y al añadir `blog-ai` con
`--add-dir` **no se cargó lo mismo de cada una**:

| Pieza de `blog-ai` | ¿Se cargó al iniciar? | Cómo lo sé |
|---|:-:|---|
| `CLAUDE.md` (REGLA-AI) | ❌ **No** | El propio agente lo dijo, y la REGLA-AI **sí acabó influyendo**: leyó el archivo **durante** la tarea y nombró el campo según ella |
| **Hook** `PostToolUse` | ❌ **No** | `MARCADORES-blog-ai.txt` **no existe** |
| **Skill** `marcador-blog-ai` | ✅ **Sí** | Aparece en la lista de skills disponibles, junto a la de `blog-api` |

> **No es que «del directorio añadido no se cargue nada».** Las skills sí viajan; las instrucciones
> y los hooks, no. **Saber que puede leer el otro repositorio no dice nada sobre qué le obliga
> allí.**

## Por qué el resultado correcto no demuestra que hubiera garantía

El campo salió **bien nombrado y en español**, que es justo lo que pedía la REGLA-AI. Pero esa regla
**no estaba cargada**: el agente la cumplió porque **fue a leer el archivo por su cuenta** mientras
trabajaba.

**Si no hubiera ido a leerlo, nada lo habría impedido.** El acierto vino de una lectura oportuna,
no de un guardarraíl — y eso no se ve mirando el resultado, solo comparando lo que dijo tener
cargado con lo que los registros dicen que se ejecutó.

## Comprobación previa, para no confundir «no saltó» con «está roto»

Antes de la sesión real disparé **los dos hooks a mano**, con un evento `Edit` falso por stdin.
**Los dos escribieron su línea.** Después borré ambos archivos para que la prueba empezara en cero.

Por eso el `MARCADORES-blog-ai.txt` inexistente **significa que el hook no se cargó**, y no que
estuviera mal escrito.

## Hasta dónde llegué

**Los tres servicios no se levantaron.** En esta máquina no están instalados **Docker, Ollama ni
Python 3.13** —el de Windows Store da «Acceso denegado»—, así que `make setup` de `blog-ai` no se
pudo ejecutar. **La práctica no los necesita**: los cinco pasos de la parte A son sistema de
archivos y comportamiento del agente. Lo anoto porque el enunciado pide decir dónde me quedé.

## Estado al terminar

Revertido `blog-ai/app/esquemas.py` y borrado `blog/CLAUDE.md`, como pide el paso 5. El `CLAUDE.md`,
el hook y la skill de cada repositorio **se quedan donde están**: son el montaje de la práctica.
