# Parte B

## 1. Qué dijo el agente en el paso 4: qué archivos CLAUDE.md dijo haber cargado, qué skills tenía disponibles y qué nombre dio al campo.

El agente indicó lo siguiente:
- Archivos CLAUDE.md cargados: 
  - /home/mtomas/ai4devs/blog/CLAUDE.md
  - /home/mtomas/ai4devs/blog/blog-api/CLAUDE.md

- Skills:
  - Del proyecto: marcador-blog-api y marcador-blog-ai. Ambas añaden un marcador con fecha y texto a su archivo MARCADORES-*.txt.
  - Genéricas del arnés: dataviz, artifact-design, artifact-diagramming, artifact-capabilities, update-config, keybindings-help, code-review, simplify, fewer-permission-prompts, loop, schedule, claude-api, run, plugin-authoring, init y security-review.
  - De anthropic-skills: built-in-browser, chrome-browser, computer-use, deep-research, docs, docx, google-workspace, import-memory, morning, pdf, pptx, skill-creator y xlsx.

- Nombre del campo: fragmentos_coincidentes


## 2. Qué encontraste en cada archivo de marcadores y qué indica sobre dónde se ejecuta cada guardarraíl.

- blog-api/MARCADORES-blog-api.txt

```
2026-10-28T18:48:53+01:00 | Write | /home/mtomas/ai4devs/blog/blog-api/.claude/skills/marcador-blog-api/SKILL.md
2026-10-28T18:48:53+01:00 | Write | /home/mtomas/ai4devs/blog/blog-ai/.claude/skills/marcador-blog-ai/SKILL.md
2026-10-28T18:57:24+01:00 | Edit | /home/mtomas/ai4devs/blog/blog-ai/app/esquemas.py
```

- blog-ai/MARCADORES-blog-ai.txt
(no se ha creado)

Los hooks de registro de la escritura o edición de ficheros, se ejecutan sólo en dónde se inició la sesión, en este caso blog-api, aunque se aplican tanto las modificaciones en su propio directorio, como en el directorio de blog-ai. De ahí que haya registrado las modificaciones sobre el directorio de blog-ai. El hook de blog-ai no se ejecutó porque ese repositorio solo estaba como directorio adicional, no como proyecto de la sesión.