# Frontera entre repositorios

1. Claude Code indicó que había cargado los archivos CLAUDE.md de la carpeta padre blog/ y del repositorio blog-api, pero no el de blog-ai; también confirmó que tenía disponibles las skills marcador-blog-api y marcador-blog-ai, además de otras skills globales y de plugins, y explicó que eligió el nombre fragmentos_coincidentes por las convenciones del código y no por una regla cargada de blog-ai.

2. Al revisar los marcadores, comprobé que MARCADORES-blog-api.txt contenía cuatro registros, incluido un Edit sobre blog-ai/app/esquemas.py, mientras que MARCADORES-blog-ai.txt no existía, lo que demuestra que el hook del repositorio desde el que inicié Claude Code registró la modificación externa, pero no se observó la ejecución del hook propio del repositorio añadido.
