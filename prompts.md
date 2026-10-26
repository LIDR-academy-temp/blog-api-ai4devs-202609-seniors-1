# Prompts


#Prompts 

Modelo Sonnet 5.5 y esfuerzo medio

## Prompt 1

crea lo siguiente para estos dos repositorios C:\IA\MasterLIDR\blog\blog-api y C:\IA\MasterLIDR\blog\blog-ai , sin cambiar nada más.


Un CLAUDE.md en la raíz con una sola regla propia del repositorio. En blog-api: este repositorio es el dueño del contenido y todo archivo nuevo debe empezar con un comentario que lo indique. En blog-ai: los nombres de los campos del contrato público deben escribirse en español, nunca en inglés. Las reglas son distintas para poder reconocer después cuál se aplicó.

Un hook que se ejecute al escribir o editar un archivo, mediante PostToolUse para las herramientas Write y Edit. Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt, en la raíz de su propio repositorio, con la fecha, la herramienta utilizada y la ruta del archivo modificado. Pide que use rutas absolutas: el hook tendrá que registrar cambios en archivos situados fuera de su repositorio.

Una skill sencilla llamada marcador-<nombre-del-repo>, cuya descripción indique a qué repositorio pertenece.


## Prompt 2

Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. 
debes modificar solo ese archivo y utilizar la herramienta de edición de archivos, nunca un script.


## Prompt 3
Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno.

## Prompt 4
Qué skills tiene disponibles.

## Prompt 5
Qué nombre ha dado al campo y por qué.

