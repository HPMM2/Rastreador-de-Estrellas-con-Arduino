# Rastreador-de-Estrellas-con-Arduino
Este es un proyecto escolar basado en Arduino UNO, un módulo GPS NEO-6M y una pantalla TFT ILI9341 simulado en Wokwi.
https://wokwi.com/projects/446194251655536641

El sistema muestra en tiempo real la posición de las estrellas visibles desde tu ubicación actual obtenida mediante GPS.
Utiliza coordenadas astronómicas (ascensión recta y declinación) para convertirlas a coordenadas locales (altitud y azimut), ofreciendo una representación dinámica del cielo nocturno en tu pantalla. 

El propósito del proyecto es visualizar datos GPS de forma clara y atractiva, demostrando la conexión entre sensores, módulos y pantallas mediante comunicación serial y SPI.
Contexto: Este proyecto fue hecho por estudiantes para estudiantes, aficionados o campistas que deseen identificar estrellas visibles.
Alcance: visualización de estrellas brillantes en hemisferio norte y sur, con posibilidad de ampliación del catálogo estelar.

<img width="795" height="510" alt="image" src="https://github.com/user-attachments/assets/5e316c3a-fbb8-42b3-8602-2bc1bad8d35f" />

# Requisitos


# ¿Cómo funciona internamente?
Arquitectura general:
1. El módulo GPS envía datos NMEA vía puerto serial al Arduino.
2. Arduino, usando la librería TinyGPS++, decodifica los datos (latitud, longitud, hora).
3. A partir de ellos calcula posiciones estelares (Altitud/Azimut) mediante fórmulas astronómicas.
4. La pantalla ILI9341, controlada por Adafruit_GFX, dibuja en tiempo real las estrellas y la animación del cielo.

Estructura de carpetas:

/src

  ├── sketch.ino

  ├── diagram.json 
  
  ├── gps-neo6m.chip.c
  
  ├── gps-neo6m.chip.json  
  
  ├── libraries.txt  
  
  ├── wokwi-project.txt  

<img width="795" height="586" alt="image" src="https://github.com/user-attachments/assets/a97c1eb3-4064-4fc8-82cc-635ebb55c2ca" />

Tecnologías usadas:
- Lenguaje C (Arduino)
- Librerías: Adafruit_GFX.h, Adafruit_ILI9341.h, TinyGPSPlus.h
- Hardware: Arduino UNO, GPS NEO-6M, pantalla TFT ILI9341

Comunicación entre módulos:
- GPS → Arduino: Comunicación serie (TX/RX).
- Arduino → TFT: Comunicación SPI.
- Procesamiento interno: Cálculos matemáticos y animación gráfica.


# ¿Cómo se usa?
Instalación:
1. Instalar el IDE de Arduino.
2. Instalar las librerías desde el gestor:
    Adafruit_GFX
    Adafruit_ILI9341
    TinyGPSPlus

3. Cargar el código en tu Arduino.
4. Conectar el GPS y la pantalla según el pinout del sketch.
5. Abrir el monitor serie para verificar que el GPS obtiene señal.


Ejecución:
Encender el sistema y esperar la señal del GPS.


En la pantalla aparecerán:
1. Coordenadas LAT/LON.
2. Fondo estrellado dinámico.
3. Estrellas visibles con nombre y color.



