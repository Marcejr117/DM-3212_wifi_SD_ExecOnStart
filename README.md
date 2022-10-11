<html>
    <head>
    </head>
    <body>
        <h1>Badusb_Wifi_SD_ExecOnStartUp</h1>
        <p>Este reporsitorio es una modificacion de: <a href="https://github.com/joelsernamoreno/badusb_sd_wifi">https://github.com/joelsernamoreno/badusb_sd_wifi</a></p>
        <p>El hardware utilizado: <a href="https://es.aliexpress.com/item/32839392329.html?spm=a2g0o.order_list.0.0.1875194dMcteUe&amp;gatewayAdapt=glo2esp">https://es.aliexpress.com/item/32839392329.html?spm=a2g0o.order_list.0.0.1875194dMcteUe&amp;gatewayAdapt=glo2esp</a></p>
        <p><img src="/images/Frontal.png" alt="" width="350" height="350" /></p>
        <p><img src="/images/trasera.png" alt="" width="350" height="150" /></p>
        <p>Funcionalidades:</p>
        <ol>
            <li>Ejecutar comandos desde el navegador (wifi)</li>
            <li>Ejecutar codigo almacenado en la SD desde un comando Wifi</li>
            <li>Ejecutar el archivo "script.txt" almacenado en la SD, al conectar la USB</li>
            <li>Disponer de un servidor FTP, para poder subir cualquier archivo</li>
            <li>Cambio en la distribicion de teclado: US,ESP...</li>
            <li>Interfaz grafica</li>
        </ol>
        <p>&nbsp;</p>
        <p>El proceso esta explicado tanto para linux como para windows</p>
        <p>Instalacion:</p>
        <ol>
            <ol>
                <li>Descarga el proyecto: <a href="https://github.com/Marcejr117/DM-3212_wifi_SD_ExecOnStart/archive/refs/heads/main.zip">https://github.com/Marcejr117/DM-3212_wifi_SD_ExecOnStart/archive/refs/heads/main.zip</a></li>
                <li>Abre el archivo "esp8266Programmer/esp8266Programmer.ino", modifica las preferencias de arduino y agrega esta linea: <a href="https://raw.githubusercontent.com/SpacehuhnTech/arduino/main/package_spacehuhn_index.json">http://arduino.esp8266.com/stable/package_esp8266com_index.json<br /></a><img src="/images/arduino1.png" alt="" width="550" height="500" /></li>
                <li>Conectamos la tarjeta al pc y configuramos el arduino de la siguiente forma:<br />&nbsp;<img src="images/arduino2.png" alt="" width="550" height="500" /></li>
                <li>Subimos el sketch a la tarjeta</li>
            </ol>
        </ol>
        <p><img src="images/arduino3.png" alt="" width="300" height="100" /></p>
        <ol>
            <li>Desconectamos la tarjeta y puentemos los pines, para poner el esp8266 en modo lectura, en mi caso los dos pines destinados para este fin, se me rompieron, pero estos otros dos pines hacen la misma accion.<br /><img src="/images/programmingmode.png" alt="" width="400" height="350" /></li>
            <li>Ahora debemos crear el archivo ".bin" o usar el que ya esta compilado "esp_code\esp_code.ino.generic.bin" en caso de querer compilarlo uno mismo debe de abrir el archivo "esp_code\esp_code.ino" y configurar arduino IDE de la siguiente forma:<br />- Descargamos la placa esp8266 la version 2.3.0:<br /><img src="images/arduino4.png" alt="" width="450" height="400" /><br />- seleccionamos la tarjeta "Generic 8266 asi como las siguientes configuraciones":<br /><img src="images/arduino6.png" alt="" width="450" height="400" /><br />- copiamos el servidor FTP "esp8266FTPServer-1.0" en la carpeta de librerias que en windows suele estar localizada en "C:\Users\Nombre_Usuario\Documents\Arduino\libraries", en linux: "/Home/Arduino/libraries"<br />- Finalmente lo exportamos a binario y ya tenemos el archivo listo para continuar con el siguiente paso:<br /><img src="images/arduino7.png" alt="" width="450" height="400" /></li>
            <li>conectamos de nuevo del modulo y dependiendo de si nos encontramos en linux o en windows este metodo cambia, yo recomiendo linux ya que la herramienta permite establezer un "flash_size" de 32Mb y en windows como maximo 16Mb:<br />- Para linux:<br />-- Abrimos un terminal y nos vamos a la carpeta del proyecto "esptool-master_linux" y ponemos el siguiente comando, revisa que la ruta del archivo ".bin" este especificada correctamente: <br />sudo python esptool.py --port=/dev/ttyACM0 --baud 115200 write_flash 0x00000 ../esp_code/esp_code.ino.generic.bin --flash_size 32m <br />-- Debemos tener en cuenta que debemos ejecutar el coamndo con python2, puede que necesitemos instalar algunos paquetes mas, en caso de no encontrarlo en google pueden comentarmelo<br />- Para Windows:<br />--debemos abrir la herramienta situada en "esptool-master_Windows" y configuramos de la siguiente forma:<br /><img src="images/arduino8.png" alt="" width="350" height="300" /><br /><img src="images/arduino9.png" alt="" width="350" height="300" /><br /><img src="images/arduino10.png" alt="" width="350" height="300" /></li>
            <li>Desconectamos la placa y quitamos le modo puente entre los dos pines, abrimos le scketch localizado en: "atmega32u4_code_SD_Start/atmega32u4_code_SD_Start.ino" y configuramos arduino con la placa leonardo, tambien debemos copiar la carpeta "Keyboard-1.0.4" en "C:\Program Files (x86)\Arduino\libraries" en caso de que exista una carpta llamada "Keyboard" la eliminan y copian esta "Keyboard-1.0.4"<br />En caso de que esten en linux debemos localizar la carpeta donde se guardan las librerias.</li>
            <li>Vamos a subir los archivos localizamos en "/HTML" a traves de ftp, para ello es preferible usar linux pero tambien se puede hacer con Filezilla client en windows, es importante usar el modo pasivo y que solo se realize una conexion a la vez, para este punto debemos tener la tarjeta conectada en el equipo y conectados a la red llamada "BadUSB_test" con la contrase&ntilde;a "badUSBWifi":<br />- Linux:<br />--Abrimos una terminal y nos dirijimos a la carpeta "HTML" y ponemos el siguiente comando "pftp -i 192.168.1.1" o tambien "ftp -p -i 192.168.1.1" <br />--Usuario "esp8266" y contrase&ntilde;a "esp8266" <br />-- Una vez conectado vamos a subir todo los archivos con el comando "put" como por ejemplo: "put virtualkeyboard.html" uno por uno <br />- Windows:<br />-- Debemos descargar Filezilla client y configurar un "sitio" para que la conexion sea pasiva, uso exclusivo de FTP y que solo admite una conexion a la vez<br /><img src="images/filezilla1.png" alt="" width="550" height="450" /><br /><img src="images/filezilla2.png" alt="" width="550" height="450" /><br />-- una vez le damos a conectar ya podemos subir los archivos<br /><img src="images/filezilla3.png" alt="" width="550" height="450" /></li>
            <li>finalmente desconectamos la placa y la volvemos a conectar, nos conectamos a la red "BadUSB_test" contrase&ntilde;a: "badUSBWifi", y accedemos desde la web a la direccion: "192.168.1.1" y tendremos una interfaz grafica desde la que podemos interactuar, cabe destacar que:<br />- Los comandos que mandes desde esta interfaz grafica, se interpretan con el layout ingles<br />- para utilizar la funcionalidad de SD debemos tenerla formateada en "FAT" aun he visto que tambien se podria en "FAT32", debemos crear una archivo llamado "script.txt" (podemos tener mas scripts dentro para poder ejecutarlos posteriormente con el comando "exec archivo.txt" desde la interfaz grafica)<br />- Los script de la SD estan configurados para que se ejecuten con el layout espa&ntilde;ol y los de la interfaz grafica se ejecutan con layout ingles, en caso de quere que los scripts de la SD se ejecuten con layout ingles debemos cambiar esta linea<br /><img src="images/arduino11.png" alt="" width="550" height="450" /><br />
            </li>
        </ol>
        <h3>Sintaxis</h3>
        <p>- print (example: print test)<br />- println (example: println test)<br />- press (example: press KEY_RETURN)<br />- rawpress (example: press KEY_RETURN)<br />- delay (example: delay 1000)<br />- release (example: release)<br />- runwin (example: runwin)<br />- rungnome (example: rungnome)<br />- runmac (example: runmac)<br />- execSD ((example: execSD test.txt, execSD helloworld.txt, execSD remote.txt, etc)</p>
        <h3>Links de apoyo</h3>
        <a href="https://www.arduino.cc/reference/en/language/functions/usb/keyboard/keyboardmodifiers/">Teclas especiales</a><br />
        <a href="https://www.arduino.cc/reference/en/language/functions/usb/keyboard/">https://www.arduino.cc/reference/en/language/functions/usb/keyboard/</a><br />
        <a href="https://github.com/joelsernamoreno/badusb_sd_wifi">https://github.com/joelsernamoreno/badusb_sd_wifi</a><br />
        <a href="https://github.com/Necr0tizing/ArduinoKeyboardLayouts">https://github.com/Necr0tizing/ArduinoKeyboardLayouts</a><br />
        <a href="https://github.com/TheMMcOfficial/CJMCU-3212-wifi_ducky">https://github.com/TheMMcOfficial/CJMCU-3212-wifi_ducky</a><br />
        <h4>Imagenes de apoyo</h4>
        <img src="images/1.jpg" /><br>
        <img src="images/2.png" /> <br>
        <img src="images/3.png" /> <br>
        <img src="images/4.png" /><br>
    </body>
</html>
