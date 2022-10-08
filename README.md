<h1 style="text-align: center;"><span style="font-size: 14px; font-weight: 400;">Badusb_Wifi_SD_ExecOnStartUp</span></h1>
<p>El hardware utilizado:</p>
<p><a href="https://es.aliexpress.com/item/32839392329.html?spm=a2g0o.order_list.0.0.1875194dMcteUe&amp;gatewayAdapt=glo2esp">https://es.aliexpress.com/item/32839392329.html?spm=a2g0o.order_list.0.0.1875194dMcteUe&amp;gatewayAdapt=glo2esp</a></p>
<p><img src="/images/Frontal.png" alt="" width="350" height="300" /></p>
<p>Funcionalidades:</p>
<ol>
<li>Ejecutar comandos desde Wifi</li>
<li>Ejecutar codigo almacenado en la SD desde un comando Wifi</li>
<li>Ejecutar el archivo "script.txt" almacenado en la SD, al conectar la usb</li>
<li>Disponer de un servidor FTP, para poder subir cualquier archivo</li>
</ol>
<p>&nbsp;</p>
<p>Es recomendable hacer todo este proceso desde una maquina linux pero tambien se puede hacer desde windows</p>
<p>Instalacion:</p>
<ol>
<li>Descarga el proyecto: <a href="https://github.com/Marcejr117/DM-3212_wifi_SD_ExecOnStart/archive/refs/heads/main.zip">https://github.com/Marcejr117/DM-3212_wifi_SD_ExecOnStart/archive/refs/heads/main.zip</a></li>
<li>Abre el archivo "esp8266Programmer/esp8266Programmer.ino", modifica las preferencias de arduino y agrega esta linea: <a href="https://raw.githubusercontent.com/SpacehuhnTech/arduino/main/package_spacehuhn_index.json">https://raw.githubusercontent.com/SpacehuhnTech/arduino/main/package_spacehuhn_index.json<br /></a><img src="/images/arduino1.png" alt="" width="300" height="350" /></li>
<li>Conectamos la tarjeta al pc y configuramos el arduino de la siguiente forma:&nbsp;<img src="/images/arduino2" alt="" width="" height="" /></li>
<li>Subimos el sketch y nos preparamos para flashearla <img src="/images/arduino3" alt="" width="350" height="300" /></li>
<li>Desconectamos la tarjeta y puentemos los pines, para poner el esp8266 en modo lectura, en mi caso los dos pines destinados para este fin, se me rompieron, pero estos otros dos pines hacen la misma accion.&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <img src="/images/mifrontal.png" alt="" width="350" height="350" /></li>
<li>&nbsp;</li>
</ol>
<p>&nbsp;</p>
