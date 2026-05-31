````md
# ❌⭕ Tres en Ratlla

Joc de **Tres en Ratlla** per a la consola portàtil ESPectro (ESP32-S3).

Parte del proyecto ESPectro — [base_espectro](https://github.com/bf-upc/base_espectro)

---

## Descripción

Implementación del clásico **Tres en Ratlla** para la consola portátil ESPectro (ESP32-S3).

Enfréntate a una inteligencia artificial que utiliza el algoritmo **Minimax**, capaz de calcular siempre la mejor jugada posible. Mueve el cursor por el tablero utilizando el joystick y coloca tus fichas para intentar conseguir tres en línea antes que la máquina.

---

## Controles

| Control | Acción |
|----------|----------|
| Joystick eje X | Mover cursor izquierda/derecha |
| Joystick eje Y | Mover cursor arriba/abajo |
| Botón A | Colocar ficha |
| Botón B | Acceder al Game Loader |

---

## Puntuación

- +1 punto por cada partida ganada
- +1 punto por cada empate
- Las derrotas no suman puntos
- El récord se guarda automáticamente en la memoria flash (NVS)
- El historial de las últimas 20 partidas es visible en el dashboard

---

## Dashboard

Con la consola encendida, conéctate a la red WiFi **ESPectro** (contraseña: **gameloader**) y abre **http://192.168.4.1** para ver las estadísticas en tiempo real.

### Estadísticas disponibles

- Récord histórico
- Número total de partidas
- Puntuación media
- Resultado de las últimas partidas
- Gráfico con el historial reciente

---

## Inteligencia Artificial

La máquina utiliza el algoritmo **Minimax**, que evalúa todas las jugadas posibles para seleccionar siempre el movimiento óptimo. Esto garantiza que la IA nunca cometa errores estratégicos.

---

## Compilar y flashear

```bash
git clone https://github.com/bf-upc/tres_en_ratlla_espectro

cd tres_en_ratlla_espectro

pio run --target upload
````

---

## Requisitos

* PlatformIO
* Librería `lovyan03/LovyanGFX @ ^1.1.12`

---

## Game Loader

El binario compilado se encuentra en:

```text
.pio/build/rymcu-esp32-s3-devkitc-1/firmware.bin
```

y puede subirse vía **Game Loader** sin necesidad de cables.

---

## Proyecto base

Este juego forma parte del proyecto **ESPectro** y está desarrollado sobre la plantilla oficial:

https://github.com/bf-upc/base_espectro

```
```
