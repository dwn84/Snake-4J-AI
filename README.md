# 🐍 Snake - 4 Jugadores

Un juego de culebritas (Snake) donde **4 culebras controladas por IA** compiten automáticamente sobre un tablero de 720 × 1280 píxeles. Cada culebra tiene su propio color, tono y comportamiento, y el objetivo es llegar primero al límite de puntos del nivel seleccionado.

**[▶️ Jugar ahora](https://tu-usuario.github.io/snake-4-jugadores/)**

---

## 🎮 Descripción

Cuatro culebras de colores (negra, roja, azul y verde) se mueven de forma autónoma por el tablero. Usan un algoritmo de **búsqueda en anchura (BFS)** para calcular el camino más corto hacia el píxel de comida más cercano, evitando paredes, otras culebras y sus propios cuerpos.

Cada vez que una culebra gira, se genera un **sonido único** mediante la Web Audio API. La partida es prácticamente infinita hasta que una culebra alcanza el límite de puntos del nivel elegido.

---

## ✨ Características

- 🤖 **4 culebras con IA propia**: se mueven, giran y compiten sin intervención del jugador.
- 🎨 **Colores identificativos**: negra, roja, azul y verde.
- 🎵 **Sonido único por giro**: cada culebra tiene dos notas asignadas (giro derecha / giro izquierda).
- 🍬 **Comida dinámica**: los píxeles fucsia crecen progresivamente.
- 🏆 **3 niveles** con límites de puntos distintos.
- 🔥 **Modo ganador explosivo**: al alcanzar el límite, la velocidad aumenta y la comida se duplica sin tope.
- 📐 **Tablero vertical**: 720 × 1280 píxeles con márgenes de 80 px arriba y abajo.
- 🎹 **Audio sintetizado**: sin archivos externos, todo generado con la Web Audio API.

---

## 🕹️ Cómo jugar

1. Abre el juego en tu navegador.
2. Selecciona un nivel: **CORTO**, **MEDIO** o **EXTENSO**.
3. Las culebras se mueven solas — solo observa y disfruta.
4. La primera culebra en alcanzar el límite de puntos gana.
5. Cuando la culebra ganadora choque contra algo, aparece el mensaje de victoria.
6. Tras 10 segundos, vuelve al menú para elegir un nuevo nivel.

> 💡 **Nota**: es un juego de *visualización* — no hay controles de teclado ni ratón durante la partida. Elige el nivel y observa la competición.

---

## 🏅 Niveles

| Nivel | Puntos para ganar | Color del botón |
| :--- | :---: | :--- |
| **CORTO** | 111 | Verde |
| **MEDIO** | 333 | Azul |
| **EXTENSO** | 999 | Rojo |

---

## 🎼 Mapa de sonidos

Cada giro reproduce una nota según la culebra y la dirección. La dirección se calcula con el producto cruz de los vectores:

| Culebra | Giro → DERECHA | Giro → IZQUIERDA | Color |
| :--- | :---: | :---: | :--- |
| **Negra** (grave) | Do3 · C3 | Sol3 · G3 | ⚫ |
| **Roja** (media-cálida) | Re4 · D4 | La4 · A4 | 🔴 |
| **Azul** (media-melódica) | Mi4 · E4 | Do5 · C5 | 🔵 |
| **Verde** (aguda-brillante) | Sol5 · G5 | La5 · A5 | 🟢 |

---

## 🍬 Mecánica de la comida

Los píxeles fucsia **parpadean** y crecen cuando son comidos. Su comportamiento cambia según la fase:

### Fase normal (antes de alcanzar el límite)
- Se **inicia con 128 píxeles** repartidos por el tablero.
- Cada píxel comido **desaparece** y aparecen **2 nuevos**.
- Efecto neto: **+1 píxel por cada comida** → el tablero se llena progresivamente.

### Fase ganador (al alcanzar el límite)
- Solo queda la culebra ganadora.
- La comida se **duplica** por cada punto capturado (sin límite real, más allá del tamaño del tablero).
- La **velocidad aumenta ×1.1** y el tamaño de la culebra **+1 píxel** por punto.

### Al chocar
- La culebra se recorta desde la cola hasta quedar en 1 píxel.
- Reaparece en la **misma posición donde chocó** (si es posible) tras 350 ms.

---

## 🛠️ Tecnologías

| Capa | Tecnología |
| :--- | :--- |
| Render 3D | [Three.js](https://threejs.org/) `v0.160.0` (cargado vía importmap desde CDN) |
| Render de segmentos | `InstancedMesh` para máximo rendimiento |
| Audio | Web Audio API (`OscillatorNode` + `GainNode`) |
| IA | BFS multi-fuente sobre rejilla de ocupación |
| Empaquetado | HTML único, sin dependencias externas más allá de Three.js |

---

## 📦 Instalación local

No requiere instalación ni servidor. Solo abre el archivo:

```bash
# Clona el repositorio
git clone https://github.com/tu-usuario/snake-4-jugadores.git
cd snake-4-jugadores

# Abre index.html en tu navegador
open index.html         # macOS
start index.html        # Windows
xdg-open index.html     # Linux
