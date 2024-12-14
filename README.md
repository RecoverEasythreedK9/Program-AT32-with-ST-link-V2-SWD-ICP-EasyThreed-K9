# Program AT32 with ST-Link V2 / Programar AT32 con ST-Link V2


Programar cualquier Artery AT32 por SWD ICP con un clon ST-LINK V2 de 2€

Cuando en la placa hay chips serial-to-usb como CH340 o FT232 para comunicar con el microcontrolador pero no hay botones ni jumpers de BOOT0 ni BOOT1 que permita programar por usb ISP

Artery ICP Programmer permite usar J-link como programador, y el soft de J-link permite usar programadores convertidos de ST-link a "J-link St-link" pero solo para chips ST
![BEFORE](https://github.com/user-attachments/assets/1eb0e96b-b286-4723-8061-7da3fce0836e)
![ver](https://github.com/user-attachments/assets/49835699-0b6c-46c8-acdb-9f38e8f22725)


compra un un ST-Link V2 clónico en aliexpress como este (incluye 4 cables dupont)

https://es.aliexpress.com/item/1005006160511992.html

![1](https://github.com/user-attachments/assets/f7d54c89-b454-42b6-abc4-2390120edbe0)

consigue 5 cables dupont o compra un juego de cables en aliexpress como estos

https://es.aliexpress.com/item/1005007072081464.html

![2](https://github.com/user-attachments/assets/25897f60-32f9-41ae-aa0e-29a8c96b26f3)

descarga los drivers para el st-link v2

https://www.st.com/en/development-tools/stsw-link009.html

conéctalo para que sea detectado e instala los drivers

descarga e instala "J-Link Software and Documentation pack" (contiene los drivers, selecciona legacy drivers en la instalación)

https://www.segger.com/downloads/jlink/

instala "Supports Segger tools to identify AT32 MCU" desde la web de Artery para tu chip en cuestión

por ejemplo para un AT32F403A ve a https://www.arterychip.com/en/product/AT32F403A.jsp y descarga "4_Segger_Win" https://www.arterychip.com/file/download/2330

extrae el contenido y ejecuta como administrador el instalador

de la misma web de Artery descarga el "ICP Programmer In-Circuit-Programming tool supporting AT32 MCU"

https://www.arterychip.com/file/download/2275

descarga el convertidor de st-link v2 a "j-link st-link v2" modificado para clones

https://mega.nz/file/E1A0AKYA#Z76TdbhYfYocrwyGPuR_jVtRUkSVtxo7I2T6c3Wx7t0

(incluye también el convertidor para st-link genuinos como aparece aquí https://www.segger.com/products/debug-probes/j-link/models/other-j-links/st-link-on-board/)

fuentes:

https://gist.github.com/jamesy0ung/919ef51fea4631e9dfe0bd26dc85c8f0

https://github.com/Zelmoghazy/st-link-v2-clone

abre el "STLinkReflash_for_clones.exe" con un hex editor como winhex y busca el siguiente texto y sustituye la palabra "STLink" por otra de 6 letras: (como XXXXXX...)

J-Link STLink V2 compiled Aug 12 2019 10:28:03

por

J-Link XXXXXX V2 compiled Aug 12 2019 10:28:03

esto hace que el soft de jlink detecte un programador diferente a "jlink stlink" y avise que es un clon pero permite programar con él

guarda el exe

conecta el stlink y ejecuta el STLinkReflash_for_clones.exe recién modificado eligiendo la opción 1

(este mismo stlinkreflash recién modificado o el descargado de mega tal cual, permiten volverlo a convertir si se desea a stlink v2 con la opción 3)

abre el Artery ICP Programmer y elige J-LINK como programador, conecta el stlink modificado al SWD de 6 pines (solo se conectan 5):

1swdio 2vcc3,3v 3swclk 4no-conectado 5rst 6gnd (en mi placa, el pin 4 está puenteado con el 6 a masa)

ya puedes leer (guardar una copia de respaldo), borrar y programar el chip, saldrá un mensaje de j-link clónico pero permitirá programar

![AFTER](https://github.com/user-attachments/assets/7b60e600-a85a-45dd-9360-dd6bb1f58437)

para leer toda la memoria flash del chip, indica su capacidad en Bytes en "read size 0x" pero con un valor hexadecimal, por ejemplo 262144 Bytes (256x1024, 1KB=1024 Bytes, 256KB) en decimal son 40000 en hexadecimal, busca una calculadora online

![OK](https://github.com/user-attachments/assets/546f0b7d-5082-47b3-971b-a686a07ea482)

ahora puedes restaurar la impresora 3d Easythreed K9 al estado de fábrica:

https://github.com/RecoverEasythreedK9/Dump-stock-Flash-Eeprom-Easythreed-K9-AT32
