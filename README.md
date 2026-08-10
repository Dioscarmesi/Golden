# Atlas de prueba — VipCard / VipCardManager

Imágenes numeradas para verificar que cada cartel recorta la celda correcta.
Cada celda lleva su **índice 0-based** (el que recibe `ApplyAtlas`), la letra del
atlas (A/B), la plataforma y su columna/fila.

## ⚠️ Límite de VRChat: 2048 × 2048

`VRCImageDownloader` **rechaza con error** cualquier imagen mayor a 2048×2048, en
PC y en Quest por igual. Los buffers de entrada y salida topan además en 32 MB, y
solo se puede bajar una imagen cada 5 segundos.
Fuente: [Image Loading — VRChat Creation](https://creators.vrchat.com/worlds/udon/image-loading/).

Con grilla 16 × 8 eso ata el tamaño de celda:

| Celda | Atlas que exige | ¿Carga en VRChat? |
|---|---|---|
| **128 × 256** | **2048 × 2048** | **Sí** |
| 256 × 512 | 4096 × 4096 | No — error |
| 512 × 1024 | 8192 × 8192 | No — error |

## Los dos juegos

### `vrchat-2048/` — el que funciona

| Tipo | Grilla | Celdas | PC | Quest |
|---|---|---|---|---|
| Usuarios | 16 × 8 | 128 | 2048×2048 (celda 128 × 256) | 1024×1024 (celda 64 × 128) |
| Anuncios | 4 × 2 | 8 | 2048×1024 (celda 512 × 512) | 1024×512 (celda 256 × 256) |

### `as-requested/` — con las medidas pedidas

| Tipo | Grilla | Celdas | PC | Quest |
|---|---|---|---|---|
| Usuarios | 16 × 8 | 128 | 8192×8192 (celda 512 × 1024) | 4096×4096 (celda 256 × 512) |
| Anuncios | 4 × 2 | 8 | 2048×1024 (celda 512 × 512) | 1024×512 (celda 256 × 256) |

Los de usuarios de esta carpeta **no los va a cargar VRChat**. Sirven si el atlas
se importa a mano al proyecto como textura, o para reescalarlos a 2048 antes de subirlos.

La celda de usuario es vertical (1:2) en ambos juegos, para acompañar el quad del
póster, que va en 0,61 × 1,09.

## Archivos

En cada carpeta: `users_A_pc.png`, `users_A_quest.png`, `users_B_pc.png`,
`users_B_quest.png`, `ads_A_pc.png`, `ads_A_quest.png`, `ads_B_pc.png`, `ads_B_quest.png`.

Los atlas **A** y **B** tienen la rueda de color girada 180° entre sí, para
distinguirlos de un vistazo y poder probar el multi-atlas.

## URLs directas (para los VRCUrl)

```
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/users_A_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/users_B_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/users_A_quest.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/users_B_quest.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/ads_A_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/ads_B_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/ads_A_quest.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/vrchat-2048/ads_B_quest.png
```

## Configuración en el VipCardManager

```
columns    = 16     rows    = 8      (atlas de usuarios)
adsColumns = 4      adsRows = 2      (atlas de anuncios)

atlasUrls      = [ users_A_pc,    users_B_pc    ]
atlasUrlsQuest = [ users_A_quest, users_B_quest ]
adsUrls        = [ ads_A_pc,      ads_B_pc      ]
adsUrlsQuest   = [ ads_A_quest,   ads_B_quest   ]
```

## Ojo con la numeración

El número dibujado es **0-based**, igual que el índice interno del código.
En la Tool, en cambio, la celda del usuario es **1-based** y `RebuildPool()` le
resta 1. Es decir: un usuario con **card cell 1** aparece en la celda rotulada **0**.

Con dos atlas encadenados las celdas cuentan de corrido: A cubre los índices
globales 0–127 y B los 128–255. Si un cartel muestra un número del atlas
equivocado, el problema está en el reparto del pool, no en el recorte.

## Cómo leerlas

- **Número correcto, atlas correcto** → el recorte está bien.
- **Número corrido en horizontal** → las columnas configuradas no coinciden con las reales.
- **Número corrido en vertical** → filas mal, o el eje V invertido.
- **Media franja blanca cruzando el cartel** → la grilla del cartel no es la del atlas.

Generadas con [jimp](https://github.com/jimp-dev/jimp). Contenido sintético, sin datos de nadie.
