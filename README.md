# EmotionDetection_Yocto_Raspberrypi4

## Esta imagen se realiza para una rasperrypi4, utilizando la versión dunfell de Poky

### A continuacion se muestran los pasos a seguir para la configuracion de la imagen:

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
        
4. A esta carpeta se le debe agregar la carpeta **"meta-proyecto"**

### La carpeta poky debe quedar similar a la siguiente imagen:

![pokyTree](https://user-images.githubusercontent.com/79667174/221376419-7269a50a-c3d8-4b88-8a33-e3d42f919c31.png)

5. Se deben configurar los archivos:
    - local.conf
    - bblayers.conf
   
   Estos se encuantran en, se modifican utilizando los archivos suministrados en la carpeta *"conf"*:
   
   ~poky/build/conf
   
   
   
    
