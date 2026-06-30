#Flock 🦉
Flock es un juego diario de lógica y agrupación en el navegador, inspirado en mecánicas tipo Connections, pero diseñado específicamente para los amantes de la ornitología. El objetivo es encontrar los vínculos biológicos y agrupar 16 aves en 4 categorías temáticas distintas sin quedarte sin intentos.

##✨ Características Principales
* **Dos Modos de Juego:** Disfruta del "Modo Diario" con un puzzle único sincronizado globalmente (incluye contador de rachas y guardado automático), o juega partidas ilimitadas generadas aleatoriamente en el "Modo Práctica".
* **Generación Inteligente sin Ambigüedades:** El algoritmo del juego asegura que, en cada partida, las aves asignadas a una categoría no encajen accidentalmente en ninguna de las otras tres, garantizando un puzzle justo.
* **Sistema de Pistas y Proximidad:** Si te equivocas pero has seleccionado 3 de las 4 aves correctas de un grupo, el juego te avisará de que estás muy cerca. También puedes revelar los nombres de las categorías si te quedas atascado.
* **Audio Procedimental:** Efectos de sonido (selección, error, victoria) sintetizados íntegramente en tiempo real utilizando la Web Audio API del navegador.
* **Estadísticas y Compartir:** Seguimiento local de tu porcentaje de victorias, rachas actuales e históricas, y un generador de resultados con emojis de colores para compartir fácilmente en redes sociales.

##🎮 Cómo Jugar
Observa la cuadrícula con los nombres de las 16 aves.
Selecciona 4 aves que creas que comparten una característica taxonómica, de hábitat, dieta o comportamiento (por ejemplo, "Aves pelágicas de alta mar" o "Familia Corvidae").
Pulsa "Confirmar" para comprobar si tu agrupación es correcta.
Tienes un máximo de 4 vidas (corazones) para resolver y descubrir los 4 grupos del día.

##🛠️ Tecnologías y Arquitectura
Este proyecto está construido de forma nativa sin frameworks externos para una carga ultrarrápida:
* **HTML5 / CSS3:** Interfaz 100% responsiva con un diseño inmersivo en tonos tierra, utilizando variables CSS y animaciones fluidas (pop, shake).
* **Vanilla JavaScript:** Toda la lógica del juego, validaciones, sistema de barajado y un generador de números pseudoaleatorios (RNG) con semilla para asegurar que el puzzle diario sea idéntico para todos.
* **Web Audio API:** Creación de osciladores y nodos de ganancia para la experiencia sonora sin depender de archivos MP3/WAV.
* **LocalStorage API:** Persistencia de datos en el navegador para mantener el estado de la partida diaria a medias y el histórico de estadísticas del jugador.
