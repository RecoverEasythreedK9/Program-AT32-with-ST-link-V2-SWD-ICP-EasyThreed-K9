# Artery-AT32-SWD-ICP
Programar cualquier Artery AT32 por SWD ICP con un clon ST-LINK V2 de 2€
Artery permite usar J-link como programador pero J-link permite usar programadores convertidos de ST-link a J-link solo para chips ST
compra un un ST-Link V2 clónico en aliexpress
https://es.aliexpress.com/item/1005006160511992.html
![1](https://github.com/user-attachments/assets/f7d54c89-b454-42b6-abc4-2390120edbe0)
compra un juego de cables dupont en aliexpress
https://es.aliexpress.com/item/1005007072081464.html
![2](https://github.com/user-attachments/assets/25897f60-32f9-41ae-aa0e-29a8c96b26f3)
descarga los drivers
https://www.st.com/en/development-tools/stsw-link009.html
conéctalo para que sea detectado e instala los drivers
actualízalo si quieres a la última versión de firmware
https://www.st.com/en/development-tools/stsw-link007.html
descarga e instala "J-Link Software and Documentation pack" (contiene los drivers, selecciona legacy drivers en la instalación)
https://www.segger.com/downloads/jlink/
instala "Supports Segger tools to identify AT32 MCU" desde la web de Artery para tu chip en cuestión
por ejemplo para un AT32F403A ve a https://www.arterychip.com/en/product/AT32F403A.jsp y descarga 4_Segger_Win https://www.arterychip.com/file/download/2330
extrae el contenido y ejecuta como administrador el instalador
de la misma web de Artery descarga el ICP Programmer In-Circuit-Programming tool supporting AT32 MCU
https://www.arterychip.com/file/download/2275
descarga el convertidor de st-link v2 a "j-link st-link v2" modificado para v2 clones
https://mega.nz/file/E1A0AKYA#Z76TdbhYfYocrwyGPuR_jVtRUkSVtxo7I2T6c3Wx7t0
(incluye también el convertidor para v2 genuinos como aquí https://www.segger.com/products/debug-probes/j-link/models/other-j-links/st-link-on-board/)
abre el STLinkReflash_for_clones.exe con un editor hex como winhex y busca el siguiente texto y sustituye la palabra STLink por otra de 6 letras:
J-Link STLink V2 compiled Aug 12 2019 10:28:03
por
J-Link HACKED V2 compiled Aug 12 2019 10:28:03
esto hace que el soft de jlink detecte un programador diferente a jlink stlink y avise que es un clon pero permite programar
este mismo stlinkreflash permite volverlo a convertir a stlink v2 con la opción 3
conecta el stlink y ejecuta en nuevo STLinkReflash_for_clones.exe eligiendo la opción 1
abre el Artery ICP Programmer y elige J-LINK como programador, conecta el stlink modificado por SWD
1swdio 2vcc3,3v 3swclk 4no-conectado 5rst 6gnd (en mi placa el pin 4 está puenteado con el 6 a masa)
ya puedes leer (guardar una copia de respaldo), borrar y programar el chip, saldrá un mensaje de j-link clónico pero permitirá programar
para leer toda la memoria flash del chip, indica la capacidad en "read size 0x" con un número hexadecimal, por ejemplo 256kb son 40000
