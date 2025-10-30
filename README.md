# Rastreador-de-Estrellas-con-Arduino
Este es un proyecto escolar basado en Arduino UNO, un módulo GPS NEO-6M y una pantalla TFT ILI9341 simulado en Wokwi.
https://wokwi.com/projects/446194251655536641

Su propósito principal es simular un dispositivo que muestra la ubicación de las estrellas más brillantes en el cielo nocturno, en tiempo real, basándose en la ubicación geográfica (latitud y longitud) y la hora del observador.

Resuelve el problema de "saber dónde mirar" para encontrar una estrella específica. Utiliza cálculos astronómicos para convertir las coordenadas celestes fijas de una estrella (Ascensión Recta y Declinación) en coordenadas locales (Altitud y Azimut), que indican qué tan alto sobre el horizonte y en qué dirección cardinal se encuentra la estrella.

Este es un proyecto de simulación académica para el laboratorio de "Controladores y Microcontroladores Programables" de la Facultad de Ingeniería Mecánica y Eléctrica (FIME) de la UANL.
El alcance del sistema está limitado al entorno de simulación Wokwi. No utiliza un módulo GPS real que se conecte a satélites, en su lugar, utiliza un "chip personalizado" (gps-neo6m.chip.c) que genera datos de ubicación y hora simulados. La salida es una visualización gráfica en una pantalla TFT, que muestra un mapa estelar simplificado con los puntos cardinales (N, S, E, W), los datos de coordenadas actuales y la posición de las estrellas con sus nombres.


<img width="795" height="510" alt="image" src="https://github.com/user-attachments/assets/5e316c3a-fbb8-42b3-8602-2bc1bad8d35f" />

# Requisitos
- Arduino UNO o Nano
- GPS NEO-6M
- Pantalla TFT ILI9341
- Librerías: Adafruit_GFX, Adafruit_ILI9341, TinyGPSPlus

# ¿Cómo funciona internamente?
Arquitectura general:
1. El módulo GPS envía datos NMEA vía puerto serial al Arduino.
2. Arduino, usando la librería TinyGPS++, decodifica los datos (latitud, longitud, hora).
3. A partir de ellos calcula posiciones estelares (Altitud/Azimut) mediante fórmulas astronómicas.
4. La pantalla ILI9341, controlada por Adafruit_GFX, dibuja en tiempo real las estrellas y la animación del cielo.

Estructura de carpetas:

En el entorno de Wokwi, el proyecto no usa una estructura de carpetas tradicional, sino un conjunto de archivos que definen el sistema:


  ├── sketch.ino

  ├── diagram.json 
  
  ├── gps-neo6m.chip.c
  
  ├── gps-neo6m.chip.json  
  
  ├── libraries.txt  
  
  ├── wokwi-project.txt  

<img width="795" height="586" alt="image" src="https://github.com/user-attachments/assets/a97c1eb3-4064-4fc8-82cc-635ebb55c2ca" />

Tecnologías usadas:

Hardware (Simulado):
- Arduino Uno (Microcontrolador)
- Módulo GPS NEO-6M (Sensor de entrada)
- Pantalla TFT ILI9341 (Salida visual)

Software y Librerías:
- Lenguaje Arduino (C++)
- Lenguaje C (Para el chip personalizado)
- Adafruit_GFX y Adafruit_ILI9341: Para el control de la pantalla TFT.
- TinyGPSPlus: Para la decodificación de datos NMEA del GPS.
- SoftwareSerial: Para crear un puerto serie por software y comunicarse con el GPS.

Plataforma:
- Wokwi: Simulador en línea de sistemas embebidos.


Comunicación entre módulos:
- GPS → Arduino: Comunicación serie (TX/RX).
- Arduino → TFT: Comunicación SPI.
- Procesamiento interno: Cálculos matemáticos y animación gráfica.


# ¿Cómo se usa?
Instalación:
Este proyecto es una simulación basada en web (Wokwi), por lo que no requiere instalación de software local, configuración de hardware físico ni compilación manual, sin embargo, si se llegara a necesitar este proyecto puede tener la siguiente instalación:
1. Instalar el IDE de Arduino.
2. Instalar las librerías desde el gestor:
    Adafruit_GFX
    Adafruit_ILI9341
    TinyGPSPlus

3. Cargar el código `sketch.ino` en tu Arduino.
4. Conectar el GPS y la pantalla según el pinout del sketch.
5. Verifica que el GPS obtenga señal.


Ejecutar la Simulación (Servidor Local):
Para ejecutar el proyecto:
1. Abre el proyecto en un navegador web usando el enlace:
https://wokwi.com/projects/446194251655536641

2. Espera a que cargue el editor de Wokwi.
3. Presiona el botón verde de "Play" (Iniciar simulación) en la parte superior del editor.
4. La simulación comenzará:
  - El código sketch.ino se compilará y se cargará en el Arduino Uno virtual.
  - El chip GPS personalizado (gps-neo6m.chip.c) comenzará a ejecutarse y a enviar datos NMEA (puedes verlo en el monitor serial si lo configuras).
  - La pantalla TFT (ILI9341) se encenderá y, después de unos segundos, mostrará las coordenadas LAT/LON y el mapa estelar actualizándose.


¿Cómo Contribuir?
Siendo un proyecto de Wokwi, la contribución es sencilla:
1. Abre el enlace del proyecto.
2. Modifica los archivos según sea necesario (por ejemplo, puedes agregar más estrellas al arreglo stars[ ] en sketch.ino, o cambiar las coordenadas iniciales en gps-neo6m.chip.c).
3. Prueba tus cambios ejecutando la simulación.
4. Haz clic en el botón "Guardar" (Save) para guardar una nueva versión del proyecto (esto creará un "fork" o una copia bajo tu propia cuenta de Wokwi).
5. Comparte el nuevo enlace con los mantenedores del proyecto.


Uso:
El sistema dibuja un cielo dinámico con estrellas reales, mostrando latitud, longitud y orientación en la pantalla.

En la pantalla aparecerán:
1. Coordenadas LAT/LON.
2. Fondo estrellado dinámico.
3. Estrellas visibles con nombre y color.


# FAQ (Dudas Frecuentes)
# P: ¿Por qué la pantalla está en negro o no muestra nada?
R: Asegúrate de haber presionado el botón "Play" en Wokwi. La simulación puede tardar unos segundos en inicializar la pantalla y recibir los primeros datos del GPS.
# P: ¿Por qué las estrellas no se mueven?
R: Las estrellas sí se mueven, pero muy lentamente, al igual que en la vida real. La simulación actualiza las posiciones cada 500ms (delay(500)) 53, pero el cambio solo es notable si dejas la simulación corriendo por varios minutos o si modificas la hora (utcHour) 54 o la lógica de tiempo en el sketch.ino.
# P: ¿Puedo usar esto con un GPS real?
R: Sí, El código en sketch.ino está listo para usarse. Solo necesitarías conectar un módulo GPS NEO-6M real a los pines 5V, GND, y conectar el pin TX del GPS al pin D4 del Arduino. El código gps.encode(gpsSerial.read()) 55 leerá los datos del hardware real exactamente igual que lee los datos simulados.
