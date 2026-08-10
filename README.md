# Atlas de prueba — VipCard / VipCardManager

Imágenes numeradas para verificar que cada cartel recorta la celda correcta.
Cada celda lleva su **índice 0-based** (el que recibe `ApplyAtlas`), la letra del
atlas (A/B), la plataforma y su columna/fila.

## Formato

Todo entra en **2048 × 2048**, que es el máximo que acepta `VRCImageDownloader`
([docs](https://creators.vrchat.com/worlds/udon/image-loading/)). Celdas verticales 1:2,
como el quad del póster (0,61 × 1,09).

| Tipo | Grilla | Por imagen | PC | Quest |
|---|---|---|---|---|
| **Usuarios** | 8 × 4 | **32** (0–31) | 2048×2048 — celda **256 × 512** | 1024×1024 — celda 128 × 256 |
| **Anuncios** | 4 × 2 | **8** (0–7) | 2048×2048 — celda **512 × 1024** | 1024×1024 — celda 256 × 512 |

Coincide con los defaults de la Tool: `card_cols 8 / card_rows 4`, `ads_cols 4 / ads_rows 2`.

## Archivos

`users_A_pc.png` · `users_A_quest.png` · `users_B_pc.png` · `users_B_quest.png`
`ads_A_pc.png` · `ads_A_quest.png` · `ads_B_pc.png` · `ads_B_quest.png`

Los atlas **A** y **B** tienen la rueda de color girada 180° entre sí, para
distinguirlos de un vistazo y poder probar el multi-atlas. Entre los dos hay
64 usuarios y 16 anuncios.

## URLs directas (para los VRCUrl)

```
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/users_A_pc.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/users_B_pc.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/users_A_quest.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/users_B_quest.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/ads_A_pc.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/ads_B_pc.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/ads_A_quest.png
https://raw.githubusercontent.com/Dioscarmesi/Golden/main/ads_B_quest.png
```

## Configuración en el VipCardManager

```
columns    = 8      rows    = 4       (atlas de usuarios)
adsColumns = 4      adsRows = 2       (atlas de anuncios)

atlasUrls      = [ users_A_pc,    users_B_pc    ]
atlasUrlsQuest = [ users_A_quest, users_B_quest ]
adsUrls        = [ ads_A_pc,      ads_B_pc      ]
adsUrlsQuest   = [ ads_A_quest,   ads_B_quest   ]
```

Ojo: se baja **una imagen cada 5 segundos**, así que con cuatro atlas la carga
completa tarda unos 20 s desde que entrás al mundo.

## Ojo con la numeración

El número dibujado es **0-based**, igual que el índice interno del código.
En la Tool, en cambio, la celda del usuario es **1-based** y `RebuildPool()` le
resta 1. Es decir: un usuario con **card cell 1** aparece en la celda rotulada **0**.

Con dos atlas encadenados las celdas cuentan de corrido: A cubre los índices
globales 0–31 y B los 32–63. Si un cartel muestra un número del atlas equivocado,
el problema está en el reparto del pool, no en el recorte.

## Cómo leerlas

- **Número correcto, atlas correcto** → el recorte está bien.
- **Número corrido en horizontal** → las columnas configuradas no coinciden con las reales.
- **Número corrido en vertical** → filas mal, o el eje V invertido.
- **Media franja blanca cruzando el cartel** → la grilla del cartel no es la del atlas.

Generadas con [jimp](https://github.com/jimp-dev/jimp). Contenido sintético, sin datos de nadie.
