ᗧ···ᗣ···ᗣ Pac-Man en MIPS Assembly
  Este proyecto es una implementación funcional del clásico juego Pac-Man, desarrollado completamente en lenguaje ensamblador MIPS utilizando el simulador MARS. El juego cuenta con gráficos renderizados en tiempo real, inteligencia artificial básica para enemigos, sistema de colisiones, efectos de sonido y conversión de sistemas numéricos.
RequisitosSimulador 
 - MARS MIPS (Versión 4.5 recomendada).
 - Java Runtime Environment (JRE) para ejecutar MARS.
⚙️ Configuración e Instalación (¡IMPORTANTE!)Para que el juego funcione correctamente, las herramientas de MARS deben configurarse con los siguientes parámetros exactos:
 - Abrir MARS y cargar el archivo .asm.
 - Ir al menú Tools y abrir Bitmap Display.Configurar el Bitmap Display así: Unit Width: 32, Unit Height: 32, Display Width: 512, Display Height: 512, Base Address for Display: 0x10010000 (static data)
 - Ir al menú Tools y abrir Keyboard and Display MMIO Simulator.
 - Darle al botón "Connect to MIPS" en ambas herramientas.
 - Ensamblar (F3) y Ejecutar (F5).
 - Nota: Para mover al personaje, debes hacer clic dentro del cuadro de texto blanco de la ventana Keyboard and Display MMIO Simulator antes de presionar las teclas.
🎮 Cómo Jugar
  El objetivo es recoger todas las monedas (amarillas) y llegar a la meta (verde) sin ser atrapado por los fantasmas (rojos).
  Controles
    - Tecla Acción "W" Mover Arriba
    - "S" Mover Abajo
    - "A" Mover Izquierda
    - "D" Mover Derecha
🧠 Arquitectura Técnica
  Este proyecto implementa varias técnicas avanzadas de manejo de memoria y control de flujo en ensamblador:
    1. Gestión de Memoria en CapasPara evitar conflictos gráficos (bugs visuales), la memoria se segmentó en tres zonas seguras:Video (VRAM): Inicio de .data (0x10010000).Datos/Textos: Protegidos por un Buffer Shield de 4096 bytes para evitar sobrescritura por el display.Lógica del Mapa: Alojada en el Heap (0x10040000) para separar completamente la lógica de la representación visual.
    2. Entrada/Salida (MMIO)Se utiliza Polling sobre la dirección 0xffff0000 para leer el teclado. Se implementó una lectura mediante lw (Load Word) para asegurar la limpieza del bit de control y evitar el congelamiento del simulador.
    3. Conversión de BasesAl finalizar el juego, el sistema convierte y muestra la puntuación en cuatro bases numéricas distintas (requisito académico):Decimal (Base 10)Hexadecimal (Base 16)Octal (Base 8 - Algoritmo recursivo personalizado)Binario (Base 2)
