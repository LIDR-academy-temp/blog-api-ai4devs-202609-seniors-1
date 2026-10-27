# Registro de Prompts - Ejercicio Blog Polirepo

## Prompt 1: Configuración de guardarraíles (Paso 2)
- **Herramienta:** Claude Code CLI
- **Modelo:** Claude 3.5 Sonnet
- **Prompt enviado:**
Necesito que configures tres piezas en este repositorio (blog-api) y en el repositorio hermano (../blog-ai) sin cambiar nada más del código existente:

1. Un archivo CLAUDE.md en la raíz de cada repositorio con una sola regla propia:
   - En blog-api: "este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique"
   - En ../blog-ai: "los nombres de los campos del contrato público deben escribirse en español, nunca en inglés"

2. Un hook de tipo PostToolUse para las herramientas Write y Edit que se ejecute al escribir o editar un archivo. Debe añadir una línea al archivo MARCADORES-<nombre-del-repo>.txt en la raíz de su propio repositorio con la fecha, la herramienta utilizada y la ruta absoluta del archivo modificado. Usar rutas absolutas.

3. Una skill sencilla llamada marcador-<nombre-del-repo> en cada repositorio cuya descripción indique a qué repositorio pertenece.


## Prompt 2:
- **Herramienta:** Claude Code CLI
- **Modelo:** Claude 3.5 Sonnet
- **Prompt enviado:**
Añade a la clase ResultadoBusqueda en el archivo ../blog-ai/app/esquemas.py un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica solo ese archivo y utiliza la herramienta de edición de archivos (Edit), nunca un script de shell.

Al terminar, responde por separado a estas tres preguntas:
1. ¿Qué archivos CLAUDE.md se cargaron al iniciar la sesión? Cita la regla de cada uno.
2. ¿Qué skills tienes disponibles?
3. ¿Qué nombre le has dado al campo añadido y por qué?

