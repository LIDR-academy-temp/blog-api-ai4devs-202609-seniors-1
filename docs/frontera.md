# Fronteras de contexto entre repositorios

Al iniciar Claude Code desde `blog-api` con `--add-dir ../blog-ai`, se cargaron las instrucciones `CLAUDE.md` del directorio padre y del repositorio principal, mientras que las de `blog-ai` se descubrieron al inspeccionar sus archivos; las skills de ambos repositorios aparecieron disponibles.

Al modificar `blog-ai/app/esquemas.py`, se ejecutó el hook `PostToolUse` configurado en `blog-api`, generando `blog-ai/MARCADORES-blog-api.txt` con el contenido `HOOK-API`, pero no se observó la ejecución del hook de `blog-ai`.
