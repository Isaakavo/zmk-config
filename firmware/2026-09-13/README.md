# Firmware 2026-09-13

Cuatro capas (Base / Lower / Raise / Config), sin macros, con RGB underglow
apagado al arrancar. Ver `docs/keymap.html` para el layout completo.

| | |
|---|---|
| Commit | `89e3448` |
| Run | [34800800468](https://github.com/Isaakavo/zmk-config/actions/runs/34800800468) |
| Board | `nice_nano//zmk` |
| Shield | `corne` + `nice_view_adapter` + `nice_view_gem` |
| ZMK | `main` |

| Archivo | sha256 (12) | Bloques |
|---|---|---|
| `corne_left-2026-09-13.uf2` | `328cf763dbd2` | 1404 |
| `corne_right-2026-09-13.uf2` | `a2951b8160ff` | 1246 |

Estos archivos reemplazan una build anterior del mismo dia, hecha desde
`30209d2`, que apagaba las dos pantallas: le faltaba
`CONFIG_ZMK_RGB_UNDERGLOW_EXT_POWER=n` y cada evento de inactividad o de
desconexion de USB cortaba el riel VCC del que cuelga el nice!view. Aquella
build se borro a proposito para que nadie la flashee por error.

## Como flashear

1. Conecta una mitad por USB y haz **doble toque al boton de reset**. Aparece
   un volumen llamado `NICENANO`.
2. Copia el `.uf2` de esa mitad. Se reinicia solo al terminar.
3. Repite con la otra mitad.

El izquierdo va al izquierdo. Los dos archivos no son intercambiables.

Flashea **las dos mitades**: este firmware cambia el keymap en ambas.
