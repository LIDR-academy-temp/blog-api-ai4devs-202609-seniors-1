# Prompts


## Prompt 1

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
No realizes commits ni PR de forma automática.
Limitate a las instrucciones que te indico, sin asumir nada de lo que se indique en los archivos readme de los proyectos

```

**Qué salió:** 
Confirma que no tratará readme como instrucciones.
Añade REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.

## Prompt 2

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
En este proyecto (blog-api) crea un archivo de instrucciones CLAUDE.md con las siguientes reglas: "este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique."
```

**Qué salió:** 
Crea archivo. Añade las dos reglas. Añade ejemplos de comentarios. 
Añade mensaje de regla.padre.

## Prompt 3

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
En el proyecto blog-ai, crea un archivo de instrucciones CLAUDE.md con las siguientes reglas: los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. Las reglas son distintas para poder reconocer después cuál se aplicó.
```

**Qué salió:** 
Genera archivo con la regla. Pero indica que no añade comentario por estar fuera de blog-api y allí no debe aplicar esa regla.
Si añade REGLA-PADRE

## Prompt 4

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
Crea en los repositorios blog-api y blog-ai (sin incluir blog-web ) un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. 
que use rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio.

```

**Qué salió:** 
Genera hook y script marcador.py en cada repositorio.
El script de blog-api incluye el comentario # Contenido propiedad del repositorio blog-api.
El script generado en blog-ai no lo incluye.

Genera mensaje REGLA-PADRE.

Cambia a idioma inglés.


## Prompt 5

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
Crea en los repositorios blog-api y blog-ai (sin incluir blog-web ) una skill sencilla llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece.
```

**Qué salió:** 
Genera skills en cada repositorio.
El script de blog-api incluye el comentario # Contenido propiedad del repositorio blog-api.
El script generado en blog-ai no lo incluye.

Genera mensaje REGLA-PADRE.

## Prompt 6

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
Añade en la clase ResultadoBusqueda (de ../blog-ai/app/esquemas.py)  un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda.

modifica solamente este archivo. Y modificalo mediante la herramienta de edición de archivos (nunca mediante script)

```

**Qué salió:** 
Genera campo en la clase.
No añade comentario en la cabecera del fichero.
Registra edición en archivo marcadores del proyecto api.


## Prompt 7

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno.

```

**Qué salió:** 
blog/CLAUDE.md con el mensaje de REGLA-PADRE
blog-api/CLAUDE.md con la regla del comentario.

indica que no cargó el claude de blog-ai porque está añadido como directorio de trabajo adicinal.

Indica que no aplico la regla de blog-api porque el archivo ya existía, y está en blog-api (fuera el ámbito de la regla).


## Prompt 8

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
Qué skills tiene disponibles?
```

**Qué salió:** 
Indica que tiene las skills de ambos proyectos (marcador-blog-api y marcador-blog-ai)

Lista conjunto de skills adicionales generales (desarrollo claide, automatización, artifacts y documentos)


## Prompt 9

**Modelo:** Opus 5.5 Medium
**Herramienta:** Claude Code

```
¿Que nombre le has dado al campo, y por que?

```

**Qué salió:** 
Lo ha nombrado fragmentos_coincidentes.

Indica 3 motivos. 

Indica que el español lo ha seleccionado porque los campos del archivo ya estaban en español y snack_case. **No lo ha llamado  así por las instrucciones de ese repositorio.**

