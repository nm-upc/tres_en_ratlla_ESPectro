# Tres en Raya — ESPectro (ESP32-S3)

Implementación del clásico Tres en Raya para la consola portátil ESPectro (ESP32-S3).

Parte del proyecto ESPectro — :contentReference[oaicite:0]{index=0}

---

## Descripción

Este proyecto implementa el juego clásico **Tres en Raya (Tic-Tac-Toe)** para la consola portátil ESPectro basada en **ESP32-S3**.

El jugador utiliza el joystick para desplazarse por el tablero y coloca su ficha mediante los botones de la consola. El sistema detecta automáticamente victorias, empates y mantiene estadísticas de partidas utilizando la memoria NVS integrada.

Además, aprovecha todas las funcionalidades de la plataforma ESPectro:

- Pantalla TFT ILI9488.
- Sonido mediante I2S.
- Gestión de récords y estadísticas.
- Dashboard web integrado.
- Actualización OTA mediante Game Loader.
- WiFi funcionando en segundo plano con FreeRTOS.

---

## Características

- Tablero clásico de 3x3.
- Control mediante joystick.
- Detección automática de:
  - Victoria.
  - Derrota.
  - Empate.
- Sistema de estadísticas persistentes.
- Dashboard web accesible desde cualquier navegador.
- Actualización OTA mediante archivos `.bin`.
- Compatibilidad total con la infraestructura ESPectro.

---

## Hardware utilizado

### Microcontrolador

- ESP32-S3

### Pantalla

- TFT ILI9488
- Resolución 320x480 px

### Controles

| Elemento | GPIO |
|-----------|--------|
| Joystick X | 5 |
| Joystick Y | 4 |
| Pulsador Joystick | 42 |
| Botón A | 40 |
| Botón B | 41 |

### Audio

Interfaz I2S:

| Señal | GPIO |
|---------|---------|
| BCLK | 8 |
| LRCLK | 16 |
| DIN | 18 |

---

## Estructura del proyecto

```text
src/
 └── main.cpp

include/

lib/

platformio.ini
```

---

## Funcionalidades ESPectro integradas

### Splash Screen

Al iniciar el sistema aparece la pantalla de bienvenida ESPectro acompañada de una secuencia sonora generada por I2S.

---

### Menú principal

El menú principal permite:

- Iniciar una partida.
- Acceder al Game Loader.
- Consultar el récord almacenado.
- Ver el estado del WiFi.

---

### Dashboard Web

El sistema crea automáticamente un punto de acceso WiFi:

```text
SSID: ESPectro
Password: gameloader
```

Dashboard:

```text
http://192.168.4.1
```

Desde el navegador se puede:

- Consultar estadísticas.
- Ver récords.
- Visualizar historial de partidas.
- Subir nuevas versiones del juego.

---

### Actualización OTA

La consola permite instalar nuevas versiones del juego directamente desde el navegador.

Proceso:

1. Compilar el proyecto.
2. Obtener el archivo `.bin`.
3. Conectarse al WiFi de ESPectro.
4. Abrir:

```text
http://192.168.4.1
```

5. Seleccionar el archivo.
6. Pulsar **Pujar joc**.
7. La consola reiniciará automáticamente.

---

## Sistema de estadísticas

Las estadísticas se almacenan mediante NVS.

Información guardada:

- Récord máximo.
- Historial de partidas.
- Número total de partidas.
- Último resultado.

Ejemplo:

```json
{
  "tres_en_raya": {
    "best": 15,
    "history": [15,12,9,7,4]
  }
}
```

---

## Sistema de audio

Se utilizan tonos generados mediante I2S para:

- Inicio del juego.
- Victoria.
- Empate.
- Movimiento del cursor.
- Fin de partida.

Funciones principales:

```cpp
playTone(freq, duration, volume);
playSilence(duration);
```

---

## FreeRTOS

El proyecto utiliza tareas independientes:

### wifiTask

Gestiona:

- Dashboard web.
- Actualizaciones OTA.
- Endpoints MCP.

Ejecutándose en:

```text
Core 0
Prioridad 1
```

---

## MCP Endpoints

El dashboard incorpora una pequeña interfaz MCP.

### Herramientas disponibles

#### get_records

Obtiene récords e historial.

```http
GET /mcp/tools/call?tool=get_records
```

---

#### get_status

Obtiene información del estado actual.

```http
GET /mcp/tools/call?tool=get_status
```

---

#### get_system_info

Obtiene información del hardware.

```http
GET /mcp/tools/call?tool=get_system_info
```

---

## Compilación

### PlatformIO

Compilar:

```bash
pio run
```

Subir por USB:

```bash
pio run --target upload
```

Generar firmware:

```bash
pio run
```

El archivo generado aparecerá normalmente en:

```text
.pio/build/<entorno>/firmware.bin
```

---

## Controles

| Acción | Control |
|----------|----------|
| Mover cursor | Joystick |
| Confirmar casilla | Botón A |
| Volver al menú | Botón B |

---

## Flujo del juego

```text
Inicio
   ↓
Splash Screen
   ↓
Menú Principal
   ↓
Nueva Partida
   ↓
Jugador mueve cursor
   ↓
Coloca ficha
   ↓
¿Victoria?
 ├─ Sí → Fin
 └─ No
      ↓
 ¿Empate?
 ├─ Sí → Fin
 └─ No
      ↓
 Siguiente turno
```

---

## Tecnologías utilizadas

- Arduino Framework
- ESP32-S3
- PlatformIO
- FreeRTOS
- LovyanGFX
- WiFi
- WebServer
- OTA Update
- NVS Flash Storage
- I2S Audio

---

## Autores

Desarrollado para la plataforma ESPectro.

Autores de la plataforma:

- :contentReference[oaicite:1]{index=1}
- :contentReference[oaicite:2]{index=2}

UPC · 2026

---

## Licencia

Proyecto educativo desarrollado para la plataforma ESPectro.
Puede utilizarse libremente con fines académicos y de aprendizaje.
