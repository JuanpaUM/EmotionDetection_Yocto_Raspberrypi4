# EmotionDetection_Yocto_Raspberrypi4

## Esta imagen se realiza para una rasperrypi4, utilizando la versión dunfell de Poky

### A continuacion se muestran los pasos a seguir para la configuracion de la imagen:

1. Se utilizan los siguientes layers:
    - meta-openembedded
    - meta-raspberrypi
    - meta-tensorflow-lite
    
   Se deben clonar de la siguiente manera dentro de la carpeta poky:
   
        git clone https://git.openembedded.org/meta-openembedded -b dunfell

        git clone https://github.com/agherzan/meta-raspberrypi -b dunfell

        git clone https://github.com/NobuoTsukamoto/meta-tensorflow-lite -b dunfell
        
2. A esta carpeta se le debe agregar la carpeta **"meta-proyecto"**

### La carpeta poky debe quedar similar a la siguiente imagen:

![pokyTree](https://user-images.githubusercontent.com/79667174/221376419-7269a50a-c3d8-4b88-8a33-e3d42f919c31.png)
