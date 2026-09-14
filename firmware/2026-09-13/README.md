# Firmware 2026-09-13

Cuatro capas (Base / Lower / Raise / Config), sin macros, con RGB underglow
apagado al arrancar. Ver `docs/keymap.html` para el layout completo.

| | |
|---|---|
| Commit | `9b39220` |
| Run | [34799885452](https://github.com/Isaakavo/zmk-config/actions/runs/34799885452) |
| Board | `nice_nano//zmk` |
| Shield | `corne` + `nice_view_adapter` + `nice_view_gem` |
| ZMK | `main` |

| Archivo | sha256 (12) | Bloques |
|---|---|---|
| `corne_left-2026-09-13.uf2` | `4d0ca2267fcd` | 1405 |
| `corne_right-2026-09-13.uf2` | `4a3bb808bc1f` | 1246 |

## Cómo flashear

1. Conecta una mitad por USB y haz **doble toque al botón de reset**. Aparece
   un volumen llamado `NICENANO`.
2. Copia el `.uf2` de esa mitad. Se reinicia solo al terminar.
3. Repite con la otra mitad.

El izquierdo va al izquierdo. Los dos archivos no son intercambiables.

Flashea **las dos mitades**: este firmware cambia el keymap en ambas.
