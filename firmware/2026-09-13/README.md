# Firmware 2026-09-13

Cuatro capas (Base / Lower / Raise / Config), sin macros y sin RGB.
Ver `docs/keymap.html` para el layout completo.

| | |
|---|---|
| Commit | `0968192` |
| Run | [34801216637](https://github.com/Isaakavo/zmk-config/actions/runs/34801216637) |
| Board | `nice_nano//zmk` |
| Shield | `corne` + `nice_view_adapter` + `nice_view_gem` |
| ZMK | `main` |

| Archivo | sha256 (12) | Bloques |
|---|---|---|
| `corne_left-2026-09-13.uf2` | `108391b91004` | 1394 |
| `corne_right-2026-09-13.uf2` | `6304791b10b8` | 1235 |
| `settings_reset-2026-09-13.uf2` | `0dd6be82134d` | 206 |

Verificado en hardware: ambas mitades arrancan y el teclado escribe.

## Como flashear

1. Conecta una mitad por USB y haz **doble toque al boton de reset**. Aparece
   un volumen llamado `NICENANO`.
2. Copia el `.uf2` de esa mitad. Se reinicia solo al terminar.
3. Repite con la otra mitad.

El izquierdo va al izquierdo. Los dos archivos no son intercambiables.

## Identificar que mitad esta conectada

Cada placa mantiene su numero de serie USB entre el firmware y el bootloader,
asi que es la forma fiable de distinguirlas:

| Mitad | SerialNumber |
|---|---|
| Izquierda | `91F3CCF6FA80E2DF` |
| Derecha | `25F8BCC4E4B3EA78` |

    for d in /sys/bus/usb/devices/*/; do
      cat "$d/product" "$d/serial" 2>/dev/null | paste -sd' '
    done | grep -i nano

## settings_reset

Borra los bonds de Bluetooth guardados. Hace falta cuando el host ve el
teclado pero no completa el emparejamiento, o tras un salto grande de version
de ZMK: las llaves escritas por el stack anterior no sobreviven al cambio.
Flashear en ambas mitades, volver a flashear el firmware normal encima, y
borrar tambien la entrada del lado del host con `bluetoothctl remove <MAC>`.

## Si una mitad no enumera

Sintoma: `device not accepting address, error -71`, o intentos repetidos de
`new full-speed USB device` que nunca llegan a `Product:`.

Antes de sospechar del firmware, **prueba otro puerto USB fisico**. Comprueba
en `journalctl -k` que la ruta del puerto cambia de verdad (`usb 1-5` ->
`usb 1-6`); si sigue apareciendo la misma, no cambiaste de puerto. Eso fue
exactamente lo que pasó aqui, y costo un buen rato de diagnostico equivocado.
