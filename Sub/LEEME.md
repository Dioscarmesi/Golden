# Sub/ — comunidades Partner de Golden

Una carpeta numerada por comunidad (`001`, `002`…). La API (`/p/{código}`) elige la carpeta por el código; los códigos NO están aquí (repo público), sino en `Api/config/partner-codigos.json` de APIRender.

| Archivo | Qué es | Lo usa hoy |
|---|---|---|
| `hoja.json` | usuarios (`id` = nombre EXACTO de VRChat), `rank`, `banner`, `card`; `cards` true/false; `anuncios` 0–4 | ✅ |
| `info.json` | nombre de la comunidad y notas (no se descarga) | — |
| `banners.png` | atlas 4×4 de coronas (1024², celdas de 256) | ✅ |
| `coronas/N.png` | **corona N suelta, 1024×1024 con margen** (dibujo al 55 %). Mismo número que `banner` en la hoja | ⏳ preparado para el cambio |
| `vip.png` | atlas 8×4 de cards (2048²); solo si `cards: true` | según la hoja |
| `ad1..ad4.png` | anuncios del club (1024×512); solo los que diga `anuncios` | según la hoja |

Alta de una comunidad: carpeta nueva + `hoja.json` + `banners.png` + `coronas/` + línea en `partner-codigos.json`.
