Hice que la regla REGLA-FRONTERA se cumpliera mediante el archivo CLAUDE.md de blog-api, que Claude Code cargó al iniciar desde ese repositorio y aplicó a las funciones nuevas de TypeScript y Python, incluso al modificar el repositorio hermano blog-ai.

La regla dejó de aplicarse al iniciar una sesión nueva desde blog-ai, porque no se cargó el CLAUDE.md de blog-api; lo comprobé cuando Claude creó la función contar_fragmentos_por_slug() en app/servicios/indice.py sin el comentario obligatorio REGLA-FRONTERA: validada inmediatamente encima.
