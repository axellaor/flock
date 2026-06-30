# Flock 🦉

Flock es un juego de agrupación diario en el navegador, inspirado en mecánicas tipo Connections, pero diseñado para los amantes de la ornitología.
El objetivo es agrupar 16 aves en 4 categorías ocultas de 4 elementos cada una, con un máximo de 4 errores permitidos por partida.

## ✨ Características Principales

* **Dos Modos de Juego:**
  * **📅 Modo Diario:** Un puzzle único cada día, generado de forma determinista a partir de la fecha (semilla numérica), por lo que es el mismo para todos los jugadores. Incluye contador de rachas, contador de días jugados y persistencia automática si cierras la pestaña a mitad de partida.
  * **🔁 Modo Práctica:** Genera puzzles aleatorios para jugar de forma ilimitada, sin afectar a las estadísticas del diario.
* **Generación por Ejes Temáticos:** Cada puzzle combina 4 categorías, una de cada eje (Taxonomía, Hábitat, Dieta y Comportamiento/Biogeografía), elegidas y mezcladas mediante un generador pseudoaleatorio con semilla para el modo diario.
* **Filtro de Exclusividad:** Antes de mostrar el puzzle, el sistema descarta cualquier ave que pertenezca a más de una de las 4 categorías elegidas en esa partida concreta, evitando ambigüedades entre, por ejemplo, taxonomía y hábitat.
* **Barra de Proximidad:** Al fallar un intento, una fila de píldoras muestra cuántas de las 4 aves seleccionadas pertenecen realmente a cada categoría aún sin resolver, con un resaltado especial cuando el acierto está a una sola carta (3 de 4).
* **Pista de Categorías:** Un modal "Ver categorías" muestra el nombre e icono de las categorías todavía no resueltas, sin revelar qué aves pertenecen a cada una.
* **Estadísticas Detalladas:** Modal con partidas jugadas, porcentaje de victorias, racha actual, racha máxima y un gráfico de barras con la distribución de partidas ganadas según el número de errores cometidos (0, 1, 2 o 3+).
* **Compartir Resultado:** Botón que genera un resumen tipo Wordle con emojis de colores representando el orden de tus aciertos y errores, copiable o compartible directamente desde el dispositivo.
* **Sistema de Sonido:** Efectos sutiles sintetizados con Web Audio API (sin archivos de audio externos) para seleccionar, deseleccionar, barajar, acertar, fallar, ver pista, ganar y perder.

## 🎮 Cómo Jugar

1. Selecciona 4 cartas de aves que creas que pertenecen a la misma categoría.
2. Pulsa **Confirmar** para comprobar tu selección.
3. Si aciertas las 4, la categoría se revela con su icono, nombre y las aves que la componen.
4. Si fallas, la barra de proximidad te indica cuántas de las 4 cartas elegidas pertenecían a cada categoría restante.
5. Tienes 4 vidas (corazones): cada error resta una. Si las agotas, se revelan automáticamente todas las categorías pendientes.
6. En el modo diario, una vez completada la partida (ganada o perdida), no podrás repetirla hasta el día siguiente; se mostrará una cuenta atrás hasta el próximo puzzle.

## 🛠️ Tecnologías y Arquitectura

Este proyecto está construido sin frameworks externos para mantenerlo ligero y rápido:

* **HTML5 / CSS3:** Interfaz 100% responsiva pensada para caber en una sola pantalla sin necesidad de scroll, con diseño en modo oscuro (Dark Mode).
* **Vanilla JavaScript:** Toda la lógica del juego, generación de puzzles, filtrado de exclusividad y cálculo de proximidad.
* **Generador Pseudoaleatorio con Semilla:** El modo diario usa una función `seededRng` basada en el número de día desde una fecha de referencia, garantizando que todos los jugadores reciban el mismo puzzle.
* **LocalStorage API:** Para la persistencia del progreso diario en curso, el resultado del día ya jugado y las estadísticas históricas (partidas, racha, distribución de errores).
* **Web Audio API:** Síntesis de tonos en tiempo real mediante osciladores, sin dependencias de archivos de audio.

---

## 🔄 Cambios respecto a la versión anterior

Comparando con la implementación previa de Flock, este `index.html` introduce los siguientes cambios:

* **`recordDailyResult` ahora recibe `errors` además de `win`**, y actualiza un objeto `dist` (distribución de errores: 0, 1, 2, 3+) en las estadísticas guardadas, usado para alimentar el nuevo gráfico de barras del modal de estadísticas.
* **Nuevo modal de estadísticas (`openStats` / `stats-modal`)**: muestra partidas jugadas, porcentaje de victorias, racha actual, racha máxima y un gráfico de barras animado con la distribución histórica de errores en partidas ganadas.
* **Sistema de compartir resultado (`buildShareText` / `shareResult`)**: genera un texto tipo Wordle con emojis de colores (`🟧🟩🟦🟨`) representando, intento a intento, a qué categoría pertenecía cada carta seleccionada. Usa `navigator.share` si está disponible, o copia al portapapeles como alternativa.
* **Nueva variable `guessColors`**: registra, por cada intento, los colores de categoría de las 4 cartas seleccionadas. Se guarda junto al progreso diario (`saveDailyProgress`) y al resultado final (`saveDailyResult`) para poder reconstruir el resumen compartible aunque se recargue la página.
* **La barra de proximidad (`showProximity`, clase `.prox-hot`) ha vuelto a estar activa** tras fallar un intento, mostrando cuántas aves de la selección pertenecían a cada categoría restante.
* **Pequeño ajuste en `loadStats`**: si el objeto guardado en `localStorage` no tiene el campo `dist` (usuarios con estadísticas previas a este cambio), se inicializa automáticamente para evitar errores.
