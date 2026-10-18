# Sub/ — comunidades Partner de Golden

Una carpeta numerada por comunidad (`001`, `002`…). La API (`/p/{código}`) elige la carpeta por el código; los códigos NO están aquí (repo público), sino en `Api/config/partner-codigos.json` de APIRender.

| Archivo | Qué es | Lo usa hoy |
|---|---|---|
| `hoja.json` | usuarios (`id` = nombre EXACTO de VRChat), `rank`, `banner`, `card`; `cards`: `"golden"` (solo Golden) · `"juntas"` (Golden + club) · `"club"` (solo club) — ver tabla abajo; `anuncios` 0–4; `coronas` N (0–16) = usa `coronas/1..N.png` sueltas en vez de `banners.png` (solo baja las que lleve alguien) | ✅ |
| `info.json` | nombre de la comunidad y notas (no se descarga) | — |
| `banners.png` | atlas 4×4 de coronas (1024², celdas de 256) | ✅ |
| `coronas/N.png` | **corona N suelta, 1024×1024 con margen** (dibujo al 55 %), PC. Mismo número que `banner` en la hoja. Máx. 16 | ⏳ mundo listo, falta API |
| `coronas_quest/N.png` | la misma corona a 512×512 para Quest | ⏳ mundo listo, falta API |
| `cards_pc.png` / `cards_quest.png` | atlas 8×4 de cards: PC 2048², Quest 1024² (como `users_A_pc/quest` de Golden). `card` de la hoja = celda | ⏳ preparado (aún hace falta cambio en mundo y API) |
| `vip.png` | nombre antiguo del atlas de cards (2048², solo PC). Lo que la API sirve hoy si `cards: true` | Sub/001 |
| `ad1..ad4.png` | anuncios del club (1024×512); solo los que diga `anuncios` | según la hoja |

Alta de una comunidad: carpeta nueva + `hoja.json` + `banners.png` + `coronas/` (+ `cards_pc/quest.png` si trae cards) + línea en `partner-codigos.json`.

## Modos de cards (`"cards"` en la hoja)

| Valor | Mundo nuevo | Mundo publicado (anterior) |
|---|---|---|
| `"golden"` o sin campo | solo las de Golden | solo las de Golden |
| `"juntas"` | Golden + club (cada card del club sale seguro) | solo las de Golden (no entiende el texto) |
| `"club"` | solo las del club (libera las de Golden) | solo las de Golden (no entiende el texto) |
| `true` (formato viejo) | = `"club"` | solo las del club |
| `false` (formato viejo) | = `"golden"` | solo las de Golden |

**Ojo:** hasta que el mundo y la API usen `cards_pc/quest.png`, una comunidad SIN `vip.png` debe tener `"cards": false`.
