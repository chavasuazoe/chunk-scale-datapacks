# Contribuir a Chunk Scale

Gracias por contribuir.

## Flujo recomendado

1. Crea un fork del repositorio.
2. Crea una rama descriptiva, por ejemplo `fix/load-message`.
3. Mantén los cambios pequeños y enfocados.
4. Valida todos los archivos JSON.
5. Prueba el datapack en la versión exacta declarada en `pack.mcmeta`.
6. Comprueba `/reload`, entrada a chunks positivos y negativos, cambio de dimensión y funcionamiento en multijugador.
7. Abre un pull request con pasos de prueba y resultados.

## Convenciones

- Namespace principal: `chunk_scale`.
- Objetivos de scoreboard: prefijo `cs_`.
- Funciones públicas documentadas en `README.md`.
- Comentarios y documentación en español; nombres técnicos y rutas en inglés cuando corresponda.
- No amplíes `min_format` o `max_format` sin probar la versión añadida.

## Lista mínima de pruebas

- El datapack aparece en `/datapack list enabled`.
- `/reload` no genera errores.
- El primer jugador fija el origen.
- Los chunks cardinales vecinos usan escalas distintas.
- Las coordenadas negativas producen el chunk correcto.
- El Ender Dragon queda excluido.
- Los shulkers nunca superan 3.00×.
- `set_origin` obliga a recalcular las entidades cargadas.
- `reset_scales` restaura entidades cargadas.
