# EmotionDetection_Yocto_Raspberrypi4

## Esta imagen se realiza para una rasperrypi4, utilizando la versión dunfell de Poky

### A continuación se muestran los pasos a seguir para la configuración de la imagen:

1. Inicialmente se debe clonar poky utilizando:

       git clone https://github.com/yoctoproject/poky -b dunfell

2. Luego entrar al entorno de construcción con el siguiente comando desde la terminal de la carpeta poky:

       source oe-init-build-env

3. Se utilizan los siguientes layers:
    - meta-openembedded
    - meta-raspberrypi
    - meta-tensorflow-lite
    
   Se deben clonar de la siguiente manera dentro de la carpeta poky:
   
        git clone https://git.openembedded.org/meta-openembedded -b dunfell

        git clone https://github.com/agherzan/meta-raspberrypi -b dunfell

        git clone https://github.com/NobuoTsukamoto/meta-tensorflow-lite -b dunfell
        
4. A esta carpeta se le debe agregar la carpeta sumunistrada, **"meta-proyecto"**

### La carpeta poky debe quedar similar a la siguiente imagen:

![pokyTree](https://user-images.githubusercontent.com/79667174/221376419-7269a50a-c3d8-4b88-8a33-e3d42f919c31.png)

5. Se deben configurar los archivos:
    - local.conf
    - bblayers.conf
   
   Estos se encuantran en:
   
       $ ~poky/build/conf
   
   Se modifican utilizando los archivos suministrados en la carpeta **"conf"**

6. Se ingresar al entorno de construcción y luego crear una imagen Sato usando el comando:
 
        bitbake core-image-sato
  
7. Completando el proceso se procede a encontrar la imagen que utiliza la raspberrypi4 en su SD, que esta en la dirección:
    
        $ ~/poky/build/tmp/deploy/images 

   Aqui se encuantra un archivo similar a:
   
        core-image-sato-raspberrypi4-64-20230225183838.rootfs.rpi-sdimg
   
8. Esta imagen final se debe realizar un "Flash SD card", utilizando herramientas como "Disk Image Writer" ó "balenaEtcher".

9. Realizado este proceso, se debe conectar la raspberrypi, con la respectiva SD, el cable HDMI hacia una pantalla asi como un teclado.

10. Cuando haya iniciado se debe ir al siguiente directorio:

        $ cd // 
        $ cd usr/bin/PROYECTO 
        
- y Ejecutar el siguiente comando:

        python3 DETECTOR.py

#### Hasta aqui la aplicaion esta corriedo de manera local, para hacerlo de manera remota se deben seguir los siguientes pasos:

11. Conectar la rasperrypi y la PC a la misma red.

12. Revisar la ip de la raspberypi con el siguiente comando:

        ifconfig eth0
        
13. Una vez que se sabe la ip se debe habilitar la comunicación **ssh** en la PC y verificar que este activo mediante los siguientes comandos:

        sudo systemctl enable --now ssh
        systemctl status ssh
        
12. Una vez habilitado se procede a realizar la comuniacion con la rasperrypi mediante el siguiente comando:

        ssh root@<dirección_ip_raspberry> -X
    
    La Flag -X es para habilitar las ventanas X11

Ya una vez que se logra establecer comunicación se puede retomar desde el paso 10 y asi correr el programa remotamente.

##       Archivos adicionales

### Carpeta Training

Posee los archivos para realizar el entrenamiento que utiliza el programa principal **DETECTOR.py** para realizar la detección de emociones, el programa **train_emotion_detection.py** realiza este entreno suministrando un archivo con formato de datos jerárquicos, y se necesita un archivo de formato FlatBuffer ya que es el que utiliza Tensor Flow lite para su detección, el archivo **convert_h5_to_tflite.py** se encarga de esta conversión.

Dentro de la carpeta **Data** se encuentra el set de imágenes utilizado para realizar el entrenamiento con 5 categorias.

### Carpeta Graph

El archivo principal **DETECTOR.py** suministra dos archivos de texto, uno con las estadísticas en porcentajes y el otro con el total de las emociones detectadas.

El programa **Graph.py** se encarga de realizar un gráfico que muestra la distrubucción de las emociones detectadas.

Este archivo no se utiliza en la imagen de la raspberrypi, por que el proyecto esta pensado para conectarse remotamente a la misma, entonces lo ideal es que cuando se tienen las estadisticas utilizando Secure Copy Protocol (SCP) que es el protocolo utilizado por SSH para la transferencia de archivos, la PC se encargue de realizar este gráfico.

El programa recibe argumentos entonces se debe correr con un comando similar a:

    python3 Graph.py Total_23_50_38__26_10_2022.txt Total_23_50_38__26_10_2022.png



