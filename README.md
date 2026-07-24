# Chunk Scale

Datapack para **Minecraft: Java Edition** que asigna una escala determinista a cada chunk y cambia automáticamente el tamaño de jugadores y entidades vivas cuando cruzan sus límites.

> **Compatibilidad de esta versión:** Minecraft Java **26.3 Snapshot 4**, formato de datapack **111.0**. El archivo actual declara `min_format` y `max_format` como `[111, 0]`, por lo que no debe anunciarse como compatible con otras versiones sin actualizarlo y probarlo.

## Características

- Escala jugadores, mobs y otras entidades vivas.
- Cambia el tamaño únicamente cuando una entidad entra en otro chunk.
- Fija automáticamente como origen el chunk del primer jugador que entra al mundo.
- Usa un patrón determinista de cinco escalas.
- Evita que dos chunks vecinos en dirección norte, sur, este u oeste tengan la misma escala.
- Funciona en vanilla; no necesita Fabric, Forge, NeoForge ni mods del cliente.
- Es apto para un jugador y servidores Java. En servidores, solo se instala en el mundo del servidor.

## Escalas

| Tipo | Multiplicador |
|---|---:|
| Normal | 1.00× |
| Pequeña | 0.40× |
| Mediana | 0.75× |
| Grande | 1.50× |
| Enorme | 3.00× |

La escala enorme se limita a 3.00× por la restricción técnica de los shulkers. El Ender Dragon queda excluido porque no admite el atributo de escala.

## Algoritmo

El índice de escala se calcula como:

```text
índice = ((chunkX - origenX) + 2 × (chunkZ - origenZ)) mod 5
```

El origen genera el índice `0` y usa escala normal. Al desplazarse un chunk en cualquier dirección cardinal, el índice cambia en `±1` o `±2`, evitando repeticiones entre vecinos ortogonales.

## Requisitos

- Minecraft: Java Edition.
- Versión exacta recomendada: **26.3 Snapshot 4**.
- Datapack format: **111.0**.
- Sin dependencias externas.
- Para ejecutar manualmente las funciones administrativas se requieren permisos para comandos.

## Instalación

1. Descarga el archivo de la sección **Releases**, no el ZIP automático de “Source code” de GitHub.
2. Cierra el mundo.
3. Copia el ZIP en:

   ```text
   .minecraft/saves/TU_MUNDO/datapacks/
   ```

4. Abre el mundo con Minecraft Java 26.3 Snapshot 4.
5. Si el mundo ya estaba abierto, ejecuta:

   ```mcfunction
   /reload
   ```

6. Comprueba que esté activo:

   ```mcfunction
   /datapack list enabled
   ```

> El ZIP de una release debe contener `pack.mcmeta` y la carpeta `data/` directamente en la raíz. El ZIP automático del código fuente de GitHub añade una carpeta exterior y no debe publicarse como descarga instalable directa.

## Comandos

### Cambiar el origen

Ejecuta el comando desde el chunk que deseas convertir en origen de escala normal:

```mcfunction
/function chunk_scale:set_origin
```

### Restablecer temporalmente las escalas

```mcfunction
/function chunk_scale:reset_scales
```

Esto restaura las entidades cargadas, pero el datapack vuelve a aplicar la escala correspondiente en el siguiente tick.

## Personalización

Edita estos archivos para modificar los multiplicadores:

```text
data/chunk_scale/function/scale/normal.mcfunction
data/chunk_scale/function/scale/tiny.mcfunction
data/chunk_scale/function/scale/medium.mcfunction
data/chunk_scale/function/scale/large.mcfunction
data/chunk_scale/function/scale/huge.mcfunction
```

Después de editar, ejecuta `/reload`.

## Entidades afectadas

Se incluyen:

- Jugadores.
- Mobs y otras entidades que exponen el dato `Health`.
- Mannequins y entidades vivas equivalentes, cuando sean compatibles con el atributo.

No se incluyen:

- Ender Dragon.
- Objetos tirados.
- Flechas y otros proyectiles.
- Barcos.
- Minecarts.
- Entidades que no exponen `Health`.

## Rendimiento

El datapack examina cada tick a todos los jugadores y entidades vivas cargadas. Para cada entidad obtiene sus coordenadas X/Z y solo recalcula la escala cuando cambia de chunk. En servidores con granjas de mobs o muchas entidades cargadas puede aumentar el coste por tick.

## Limitaciones conocidas

- Una entidad que crece dentro de un espacio estrecho puede quedar atrapada o sufrir asfixia.
- El patrón depende de las coordenadas de chunk y de un único origen global.
- El mensaje mostrado durante `/reload` puede indicar que el primer jugador fijará el origen incluso cuando ya existe un origen guardado.
- `reset_scales` solo afecta entidades cargadas. Antes de retirar el datapack conviene cargar las zonas importantes y ejecutar esa función.
- Las snapshots pueden cambiar formatos y comandos sin mantener compatibilidad.

## Desinstalación

1. Carga las zonas donde existan entidades importantes.
2. Ejecuta:

   ```mcfunction
   /function chunk_scale:reset_scales
   ```

3. Cierra el mundo.
4. Retira el ZIP de `datapacks/`.
5. Abre el mundo y ejecuta `/reload` si es necesario.

La versión actual no incluye una función de desinstalación que elimine objetivos de scoreboard y storage. Consulta `docs/AUDIT.md` para las mejoras recomendadas.

## Estructura

```text
.
├── data/
│   ├── chunk_scale/function/
│   └── minecraft/tags/function/
├── pack.mcmeta
├── README.md
├── README_ES.txt
├── CHANGELOG.md
├── CONTRIBUTING.md
└── docs/
```

## Versionado

Versión pública inicial sugerida:

```text
v0.1.0-mc26.3-snapshot4
```

Título de release sugerido:

```text
Chunk Scale v0.1.0 — Minecraft 26.3 Snapshot 4
```

## Licencia

No publiques una licencia hasta confirmar que posees los derechos del código. Si eres el autor y deseas permitir uso, modificación y redistribución, puedes completar `LICENSE-MIT.template`, renombrarlo a `LICENSE` y sustituir el marcador de autor.

## Aviso de marca

Este es un proyecto comunitario no oficial. Minecraft es una marca de Mojang Studios/Microsoft. El proyecto no está aprobado ni asociado oficialmente con Mojang Studios o Microsoft.
