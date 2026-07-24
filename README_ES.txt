CHUNK SCALE — Minecraft Java 26.3 Snapshot 4
============================================

QUÉ HACE
--------
Cada entidad viva cambia de tamaño al entrar en otro chunk.
El primer jugador que entra al mundo fija automáticamente el chunk de origen,
y ese chunk usa escala normal.

Escalas:
- NORMAL:  1.00x
- PEQUEÑA: 0.40x
- MEDIANA: 0.75x
- GRANDE:  1.50x
- ENORME:  3.00x

El patrón se repite cada cinco valores, pero chunks vecinos en dirección norte,
sur, este u oeste nunca tienen la misma escala.

INSTALACIÓN
-----------
1. Cierra el mundo.
2. Copia el archivo ZIP dentro de:
   .minecraft/saves/TU_MUNDO/datapacks/
3. Abre el mundo en Minecraft Java 26.3 Snapshot 4.
4. Ejecuta /reload si el mundo ya estaba abierto.
5. Comprueba con /datapack list enabled

COMANDOS
--------
/function chunk_scale:set_origin
  Convierte el chunk donde estás en el nuevo origen de escala normal.

/function chunk_scale:reset_scales
  Restaura momentáneamente las entidades cargadas a su escala predeterminada.
  El datapack volverá a aplicar las escalas en el siguiente tick.

PERSONALIZACIÓN
---------------
Edita estos archivos para cambiar los tamaños:
- data/chunk_scale/function/scale/normal.mcfunction
- data/chunk_scale/function/scale/tiny.mcfunction
- data/chunk_scale/function/scale/medium.mcfunction
- data/chunk_scale/function/scale/large.mcfunction
- data/chunk_scale/function/scale/huge.mcfunction

NOTAS
-----
- Solo escala entidades vivas: jugadores, mobs, armor stands/mannequins si
  exponen Health, etc. No escala objetos, flechas, barcos ni minecarts.
- El Ender Dragon queda excluido porque Minecraft no permite escalarlo.
- La escala enorme es 3.0x para respetar el límite técnico de los shulkers.
- Al crecer dentro de espacios estrechos, una entidad puede quedar atrapada o
  recibir daño por asfixia. Es comportamiento normal del juego.
- En servidores con muchísimas entidades cargadas, el chequeo cada tick puede
  tener coste de rendimiento. Se usa cada tick para que el cambio sea inmediato.
