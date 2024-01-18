Este repositorio forma parte del curso IoT de Samsung Innovation Campus
El objetivo es el control de un motor de corriente contínua por wifi

## Profesores:
      Francisco Alejandro Alaffita Hernández
      Beatris Adriana Escobedo Trujillo

Está organizado de la siguiente manera:

# Curso:
      Esta carpeta contiene los documentos para hacer las conexiones y cada una de las lecciones para 
      lograr hacer el circuito y los programas para controlar el motor de corriente contínua.
      
      0. Justificación
      1. Conectando la Raspberry pi 4 al módulo L298N y motor de Corriente directa
      2. Medir velocidad desde el encoder del motor
      3. Control del Motor via MQTT
      4. Conectando una pantalla Oled a Raspberry Pi
      5. Calibración de la ecuación diferencial

# Imagenes:
      Contiene todas las imagenes y los circuitos usadas en los documentos que se encuentran en la 
      carpeta Curso en formato png y de fritzing en el caso de los circuitos.

# Python:
      Contiene los programas en python de manera desglosada, es decir, dependiendo en que etapa te 
      encuentres del curso es el archivo necesario, te vas a encontrar con una subcarpeta, la cual 
      contiene los programas parciales para ir acompletando el proyecto final, es decir, 
      
      >si vas a conectar el motor entonces necesitas el archivo: solo_motor_raspberry.py
      >si vas a conectar el encoder y el motor necesitas el archivo: velocidad_RPM.py y read_RPM.py
      >si vas a controlar el motor desde mqtt necesitas el archivo: velocidad_voltaje_mqtt.py
      >si vas a conectar sólo la pantalla necesitas el archivo: pantalla_oled.py

# Forma de Uso.

      Este proyecto lo puedes disfrutar de dos maneras:
      1. Por medio de la terminal con ayuda de MQTT.
            a. Recuerda que el archivo read_RPM.py y autocalibración_y_control.py deben estar en una carpeta
            b. En la raspberry activa el daemon >>sudo pigpiod
            c. Compila en la raspberry: autocalibracion_y_control.py
            d. Para controlar la velocidad del motor tienes que enviar desde mqtt y alguna terminal el porcentaje
               del voltaje (de 0 a 100%)
            e. Para que se calibre el motor tienes que enviar desde mqtt '-2'
            f. Si requieres cerrar el programa lo puedes hacer desde mqtt enviando '-1'
      
      2. Por medio de node-red
            a. Hacer los pasos anteriores (del a.-c.) y después echar a andar node-red y el programa que se encuentra 
               en la carpeta node-red/menu_total.json
            b. Tenemos un menú a la izquierda en el cual puedes escoger como controlar el motor, además de poder 
               elegir si calibras o no la velocidad simulada.
                  b.1. Si escojes controlar por porcentaje, estas controlando el porcentaje de 0 a 100% de 12 volts, es decir,
                       si pones 25% entonces estás suministrando 3 volts al motor
                  b.2 Si escoges controlar por voltaje, estás controlando directamente cuantos volts suministras al motor,
            c. Si escojes calibración, se suministrará el máximo voltaje sobre el motor por 2 segundos y se calibrará.
 
 ![This is an image](https://raw.githubusercontent.com/AlexAlaffita/Simulacion-y-control-de-un-motor-cc/main/Imagenes/node_red_dashboard.png)


# Circuito
      Raspberry     L298N       |    Motor                    L298N    Raspberry      |     Pantalla   Raspberry
          23  -------In2        |    Vcc M(rojo)      ------- Out A+       -          |       Vcc  ----- 3v3-GPIO1
          24  -------In1        |    Gnd M(negro)     ------- Out B-       -          |       Gnd  ----- Gnd
          25  -------en         |    Vcc E(verde)     -------   -       3v3-GPIO1     |       SCL  ----- SCL
          GND -------GND        |    Gnd E(azul)      -------   -       Gnd           |       SDA  ----- SDA
                                |    Señal A(café)    -------   -       GPIO5         |
                                |    señal B(amarillo)-------   -       GPIO6         |

Vcc M y Gnd M son del motor y  Vcc E y Gnd E son del encoder, Señal A y Señal B son los dos sensores del encoder.
![This is an image](https://raw.githubusercontent.com/AlexAlaffita/Simulacion-y-control-de-un-motor-cc/main/Imagenes/circuito_motor_encoder_L298N_pantalla_bb.png)


# Preparación de la Raspberry
      Se deben instalar varias bibliotecas y paquetes en la raspberry, personalmente creo que instalar todo desde Thonny IDE 
      de la Raspberry es muy sencillo:
      1. L298N
      2. PIGPIO
      3. MQTT
      4. PAHO-MQTT
      5. REMOTE-I2C 
      6. ADAFRUIT-SSD1306
      7. LUMA 
      8. LUMA.CORE
      9. LUMA.OLED
      10. CANVAS  
      11. ADAFRUIT-CIRCUITPYTHON-DISPLAYIO-SH1106
      12. NUMPY
      13. SKLEARN
     
      Además de otras comprobaciones, es mejor si lo buscas en la parte del curso correspondiente, pero si lo que buscas es 
      copiar y pegar,
      
      Para la pantalla:
      sudo apt install -y python3-dev
      sudo apt install -y python-imaging python-smbus i2c-tools
      sudo apt install -y python3-pil
      sudo apt install -y python3-pip
      sudo apt install -y python3-setuptools
      sudo apt install -y python3-rpi.gpio
      
      Para las bibliotecas de mate:
      pip3 install opencv-python
      sudo apt-get install libcblas-dev
      sudo apt-get install libhdf5-dev
      sudo apt-get install libhdf5-serial-dev
      sudo apt-get install libatlas-base-dev
      sudo apt-get install libjasper-dev
      sudo apt-get install libqtgui4 
      sudo apt-get install libqt4-test
  


