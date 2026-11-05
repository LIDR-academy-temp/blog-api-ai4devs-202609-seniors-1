# blog-api

## Regla de proceso: REGLA-FRONTERA

Toda función o método nuevo creado en `app/services/` de blog-api o `app/servicios/` de
blog-ai debe llevar inmediatamente encima el comentario `REGLA-FRONTERA: validada`.

Sintaxis según el lenguaje, en la línea justo anterior a la definición:

- TypeScript (blog-api, `app/services/`):

  ```ts
  // REGLA-FRONTERA: validada
  async indexado(slug: string) {
  ```

- Python (blog-ai, `app/servicios/`):

  ```python
  # REGLA-FRONTERA: validada
  def contar_fragmentos(slug: str) -> int:
  ```

Alcance:

- La regla se aplica también cuando, trabajando desde blog-api, se modifiquen archivos del
  repositorio hermano `../blog-ai`.
- Solo afecta a funciones y métodos **nuevos** en esas dos carpetas. No hace falta añadir el
  comentario a funciones existentes que no se crean en el cambio.
- Antes de dar un cambio por terminado, revisa el diff de ambos repositorios y comprueba que
  cada función o método nuevo en esas carpetas tiene el comentario en la línea inmediatamente
  anterior.
