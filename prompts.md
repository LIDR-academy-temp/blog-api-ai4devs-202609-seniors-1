# Prompts

**Modelo:** Claude Opus 5 · **Herramienta:** Claude Code (app de escritorio) para preparar el
entorno y el montaje, **y Claude Code en terminal (`claude --add-dir ../blog-ai`, manual mode)**
para el paso 4, que es el que había que observar.

---

## Prompt 1

```
vamos con el modulo 7
```

**Qué salió:** el agente fue **primero a la lección del ejercicio** —hábito que viene de haber
llegado tarde al del M2— y encontró dos cosas: **el plazo era ese mismo día** y **ninguno de los
tres prerequisitos estaba instalado** (Docker, Ollama, Python 3.13).

---

## Prompt 2 — la decisión que hizo que el ejercicio saliera hoy

```
sí, haz la práctica sin levantar los servicios
```

**Por qué:** leyendo el enunciado entero, **los cinco pasos de la parte A no necesitan los tres
servicios**: crear un `CLAUDE.md` en la carpeta padre, montar instrucciones, hook y skill en dos
repos, abrir sesión con `--add-dir`, editar un archivo y **leer los dos marcadores**. Docker, Ollama
y Python solo hacen falta para que el blog funcione, y el blog no interviene.

Y el enunciado lo admite: *«No necesitas dejarlo funcionando… Si te quedas a medias, indica dónde y
qué viste»*.

---

## Prompt 3 — el del paso 4, lanzado desde `blog-api`

> Terminal aparte: `cd C:\Proyectos\blog\blog-api` → `claude --add-dir ../blog-ai` → `/login` →
> `shift+tab` hasta **manual mode**.

```
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos
fragmentos del artículo han coincidido con la búsqueda. Modifica solo ese archivo y usa la
herramienta de edición de archivos, nunca un script de shell.

Al terminar, responde por separado y con estos tres encabezados:

1) CLAUDE.md CARGADOS: qué archivos CLAUDE.md se cargaron al iniciar esta sesión, citando la regla
   de cada uno.
2) SKILLS DISPONIBLES: qué skills tienes disponibles, con su nombre exacto.
3) NOMBRE DEL CAMPO: qué nombre le has dado al campo y por qué.
```

**Qué salió:** editó con la herramienta `Edit` —no con shell—, nombró el campo
`fragmentos_coincidentes` y contestó las tres. **Tardó 3 m 43 s.**

Y dio un aviso que nadie le pidió: el valor **todavía no se calcula** (`app/servicios/indice.py:118`
construye `ResultadoBusqueda` sin ese campo, por eso le puso `default=1`), y **habría que regenerar
`contrato/openapi.json`, que es el contrato versionado que consume `blog-api`**.

> 🔑 **Las dos cláusulas que sostienen el ejercicio:**
> - *«usa la herramienta de edición de archivos, nunca un script de shell»* — sin eso, **el hook no
>   se entera**, porque solo escucha `Write` y `Edit`.
> - *«responde por separado y con estos tres encabezados»* — fuerza respuestas comparables con los
>   registros, en vez de un párrafo.

---

## Dos que no fueron prompts y cambiaron el resultado

**El intento headless que falló.** Primero probé a lanzar el paso 4 sin terminal, con
`claude --add-dir ../blog-ai --allowedTools "Read,Edit,..." -p "<el prompt>"`. Respondió
**`Failed to authenticate: OAuth session expired`**. Fue lo que obligó a hacerlo en una terminal
real, con `/login` de por medio — **y resultó ser mejor, porque así se vio el modo en la barra de
estado**: la sesión arrancó en `auto mode on`, que el enunciado prohíbe.

**El disparo manual de los hooks, antes de la sesión real.** Les metí por stdin un evento `Edit`
falso a los dos. **Los dos escribieron su línea**; luego borré los dos archivos.

> 🎯 **Ese paso es el que da valor a la segunda frase.** Sin él, `MARCADORES-blog-ai.txt`
> inexistente admite dos lecturas —«no se cargó» o «está roto»— y **no habría forma de elegir**.
> Es, literal, el *«rompe algo a propósito y mira si salta»* del M5: **verde también es lo que sale
> cuando no mira nada**.

---

## Lo que delató el archivo esta vez

En el M5 el hallazgo fue que **dos de mis cinco palabras estaban mal**. En el M6, que **el entorno
costó diez veces más que la tarea**. Este:

> ### El prompt que más cambió el resultado fue decidir qué NO hacer.

*«Haz la práctica sin levantar los servicios»* no pide nada al agente: **recorta el alcance**. Y es
lo que convirtió un ejercicio bloqueado por tres instalaciones —una de ellas con reinicio y permisos
de administrador— **en algo entregable la misma mañana**, sin perder nada de lo que se observa.

**Leer el enunciado entero antes de instalar nada fue el trabajo.** Lo demás fueron tres prompts.
