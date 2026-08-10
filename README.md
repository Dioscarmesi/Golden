# Atlas de prueba — VipCard / VipCardManager

Imágenes numeradas para verificar que cada cartel recorta la celda correcta.
Cada celda lleva su **índice 0-based** (el que recibe `ApplyAtlas`), la letra del
atlas (A/B), la plataforma y su columna/fila.

## Grillas

| Tipo | Grilla | Celdas | PC | Quest |
|---|---|---|---|---|
| Usuarios | 16 × 8 | 128 | 2048×1024 (celda 128×128) | 1024×512 (celda 64×64) |
| Anuncios | 4 × 2 | 8 | 2048×1024 (celda 512×512) | 1024×512 (celda 256×256) |

Hay dos atlas de cada tipo, **A** y **B**, con la rueda de color girada 180° entre
ellos para poder distinguirlos de un vistazo y probar el multi-atlas.

## Archivos

| Archivo | Contenido |
|---|---|
| `users_A_pc.png` | Usuarios, atlas A, PC |
| `users_A_quest.png` | Usuarios, atlas A, Quest |
| `users_B_pc.png` | Usuarios, atlas B, PC |
| `users_B_quest.png` | Usuarios, atlas B, Quest |
| `ads_A_pc.png` | Anuncios, atlas A, PC |
| `ads_A_quest.png` | Anuncios, atlas A, Quest |
| `ads_B_pc.png` | Anuncios, atlas B, PC |
| `ads_B_quest.png` | Anuncios, atlas B, Quest |

## URLs directas (para los VRCUrl)

```
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/users_A_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/users_B_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/users_A_quest.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/users_B_quest.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/ads_A_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/ads_B_pc.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/ads_A_quest.png
https://raw.githubusercontent.com/Dioscarmesi/worldtool-test-atlases/main/ads_B_quest.png
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

Con dos atlas encadenados, las celdas siguen contando de corrido: el atlas A cubre
los índices globales 0–127 y el B los 128–255. Si un cartel muestra un número del
atlas equivocado, el problema está en el reparto del pool, no en el recorte.

## Cómo leerlas

- **Número correcto, atlas correcto** → el recorte está bien.
- **Número corrido en horizontal** → las columnas configuradas no coinciden con las reales.
- **Número corrido en vertical** → filas mal, o el eje V invertido.
- **Imagen estirada o partida entre dos celdas** → la grilla del cartel no es la del atlas.

Generadas con [jimp](https://github.com/jimp-dev/jimp). Contenido sintético, sin datos de nadie.
