# Sub/ — comunidades Partner de Golden

Una carpeta numerada por comunidad (`001`, `002`…). La API (`/p/{código}`) elige la carpeta por el código; los códigos NO están aquí (repo público), sino en `Api/config/partner-codigos.json` de APIRender.

| Archivo | Qué es | Lo usa hoy |
|---|---|---|
| `hoja.json` | usuarios (`id` = nombre EXACTO de VRChat), `rank`, `banner`, `card`; `cards` true/false; `anuncios` 0–4 | ✅ |
| `info.json` | nombre de la comunidad y notas (no se descarga) | — |
| `banners.png` | atlas 4×4 de coronas (1024², celdas de 256) | ✅ |
| `coronas/N.png` | **corona N suelta, 1024×1024 con margen** (dibujo al 55 %). Mismo número que `banner` en la hoja | ⏳ preparado para el cambio |
| `cards_pc.png` / `cards_quest.png` | atlas 8×4 de cards: PC 2048², Quest 1024² (como `users_A_pc/quest` de Golden). `card` de la hoja = celda | ⏳ preparado (aún hace falta cambio en mundo y API) |
| `vip.png` | nombre antiguo del atlas de cards (2048², solo PC). Lo que la API sirve hoy si `cards: true` | Sub/001 |
| `ad1..ad4.png` | anuncios del club (1024×512); solo los que diga `anuncios` | según la hoja |

Alta de una comunidad: carpeta nueva + `hoja.json` + `banners.png` + `coronas/` (+ `cards_pc/quest.png` si trae cards) + línea en `partner-codigos.json`.

**Ojo:** hasta que el mundo y la API usen `cards_pc/quest.png`, una comunidad SIN `vip.png` debe tener `"cards": false`.
