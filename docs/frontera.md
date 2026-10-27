# LOCALIZACION PREVIA

## EN BLOG_AI
El archivo de instrucciones del agente, si existe. Suele llamarse CLAUDE.md o AGENTS.md y estar en la raíz
- No hay

Las comprobaciones automáticas que se ejecutan al editar archivos o integrar cambios, si las hay.
- No hay

Los atajos del equipo, si los hay
- Sí los hay, en el Makefile

## EN BLOG_API
El archivo de instrucciones del agente, si existe. Suele llamarse CLAUDE.md o AGENTS.md y estar en la raíz
- No hay

Las comprobaciones automáticas que se ejecutan al editar archivos o integrar cambios, si las hay.
- No hay

Los atajos del equipo, si los hay
- Sí los hay, en Makefile y en package.json

# PARTE B: LAS DOS FRASES

## Qué dijo el agente en el paso 4: qué archivos CLAUDE.md dijo haber cargado, qué skills tenía disponibles y qué nombre dio al campo

Al iniciar la sesión se cargaron dos archivos CLAUDE.md:
1. /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/CLAUDE.md (la carpeta que contiene los repositorios)
Este archivo no vive dentro de ningún repositorio: está en la carpeta que los contiene.
Por eso, toda respuesta que des aquí termina con esta línea, sola y literal:
REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
2. /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/blog-api/CLAUDE.md (el directorio de trabajo principal)
Este repositorio es el dueño del contenido.
Todo archivo nuevo que crees aquí debe empezar con un comentario que lo indique, usando la sintaxis de comentario de su lenguaje.
También da ejemplos para TypeScript, Markdown y YAML. Si el formato no admite comentarios, como JSON, pide avisar en lugar de forzarlo.
Lo que no se cargó: blog-ai se añadió como directorio de trabajo adicional, y no se cargó ningún CLAUDE.md suyo

Las skills del proyecto: 
- marcador-blog-api: indica en qué proyecto se está ejecutando.
- marcador-blog-ai: indica en qué proyecto se está ejecutando y la fecha.
Las dos dicen activarse con la misma pregunta («¿en qué proyecto o repositorio estás?»). Si me la haces, puede que no esté claro cuál usar.


Lo llamé fragmentos_coincidentes:
fragmentos_coincidentes: int = Field(default=1, ge=1)
Lo elegí por tres motivos:
1. Sigue el estilo del archivo. esquemas.py usa nombres en español, en snake_case y sin tildes, como motivos_omision, posts_indexados o fragmentos_indexados.
2. Usa el término que ya existe. El servicio ya llama «fragmentos» a los trozos en que divide un artículo (fragmento, fragmentos en RespuestaIndexar, fragmentos_indexados). Repetirlo deja claro que se cuentan esas mismas unidades.
3. Dice qué se cuenta. «Coincidentes» indica que no son todos los fragmentos del artículo, sino los que han coincidido con la búsqueda, que es lo que pediste. El plural deja claro que es una cantidad, y no se confunde con fragmento, que es el texto que se devuelve.
Como el archivo avisa de que sus nombres forman parte del contrato con blog-api, elegí uno que no hubiera que cambiar más adelante. Renombrarlo después rompería el contrato.

## Qué encontraste en cada archivo de marcadores y qué indica sobre dónde se ejecuta cada guardarraíl.

En MARCADORES-blog-api.txt encontre:
2026-10-27T19:55:20+01:00       Write   /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/blog-ai/.claude/hooks/registrar-marcador.sh
2026-10-27T19:55:20+01:00       Write   /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/blog-ai/.claude/settings.json
2026-10-27T20:00:41+01:00       Write   /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md
2026-10-27T20:01:51+01:00       Write   /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md
2026-10-27T20:04:35+01:00       Edit    /home/sergio/AI4Devs/Modulo7-Ejercicio/blog/blog-ai/app/esquemas.py

Sin embargo MARCADORES-blog-ai.txt no existe 

Esto indica que el el agente ejecuto el hook del proyecto en el que se inicio la sesion (blog-api) y nunca el de el otro (blog-ai), tampoco cuando se inicio la sesion en blog-api con blog-ai añadido. En el paso 4 al agente no hizo ninguna mención a los hooks configurados, entiendo que porque solo habiamos preguntado por archivos CLAUDE.md y skills


