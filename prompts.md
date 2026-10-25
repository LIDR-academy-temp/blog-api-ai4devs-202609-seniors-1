# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

---

## Prompt 1

**Modelo:** Opus 5.5 medium
**Herramienta:** Claude Code

```
Antes de modificar ningún archivo, inspecciona el contexto de esta sesión.

  1. Indica cuál es tu directorio de trabajo principal.
  2. Indica qué directorios adicionales tienes disponibles.
  3. Identifica qué archivos CLAUDE.md se han cargado como instrucciones de la sesión y cuáles has encontrado únicamente al inspeccionar archivos.
  4. Indica qué skills tienes disponibles y distingue las que están registradas en la sesión de las que solo puedes encontrar leyendo el sistema de archivos.
  5. No modifiques ningún archivo.

  No supongas que tener acceso a un directorio implica haber cargado sus instrucciones. Si no puedes comprobar algo, indícalo explícitamente.
```

**Qué salió:** Mostro que Claude reconoce las skills de ambos repositorios, pero declara haber cargado las instrucciones CLAUDE.md únicamente del repositorio principal y su directorio padre.

---

## Prompt 2

**Modelo:** Opus 5.5 medium
**Herramienta:** Claude Code

```
Realiza un cambio experimental mínimo en ../blog-ai/app/esquemas.py.

Localiza el modelo ResultadoBusqueda y añade un campo opcional llamado marcador_experimento de tipo str, con valor predeterminado None.

No modifiques ningún otro archivo de código.

Antes de editar, indica qué instrucciones y skills consideras aplicables, distinguiendo entre las que estaban cargadas inicialmente y las que hayas descubierto después.

Realiza el cambio utilizando la herramienta Edit.

Después, explica:
1. Qué archivo modificaste.
2. Qué campo añadiste.
3. Qué instrucciones CLAUDE.md aplicaste.
4. Qué skills utilizaste realmente.
5. Qué hooks puedes confirmar que se ejecutaron, distinguiendo evidencia directa de suposiciones.

No modifiques ni borres los archivos MARCADORES-*.txt.
```

**Qué salió:** Claude aplico la REGLA-PADRE, por decision propia utilizo la REGLA-AI y descarto la REGLA-API ya que no aplicaba por el cambio que se iba a hacer. Ademas dijo que ejecuto el hook de blog-api no el de blog-ai. 


