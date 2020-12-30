# Installare altre piattaforme in Arduino IDE

La maggior parte delle piattaforme va installata in due passaggi:

- Aggiungere l'URL di un file JSON in File/Impostazioni/URL aggiuntive per il gestore Schede
- Installare la scheda, eseguendone la ricerca, da Strumenti/Scheda/Gestore schede

## Piattaforme installabili dal gestore schede

Le URL dei file JSON possono essere più di una purchè separate da virgola:

#### ESP8266
http://arduino.esp8266.com/stable/package_esp8266com_index.json

#### ESP32
https://raw.githubusercontent.com/jantje/arduino-esp32/master/package/package_Espressif_esp32_index.json

In realtà per ESP32 l'URL giusto dovrebbe essere questo:

https://dl.espressif.com/dl/package_esp32_index.json

E, anche se digitando questo url nel Browser si vede chiaramente che il file esiste, in Arduino IDE mi da errore, mentre il primo URL consente di installare senza problemi

#### ChipKIT32
https://github.com/chipKIT32/chipKIT-core/raw/master/package_chipkit_index.json

#### Infineon XMC
https://github.com/Infineon/Assets/releases/download/current/package_infineon_index.json

Per gli XMC è necessario installare anche il Segger J-Link, presente a questo indirizzo: https://www.segger.com/downloads/jlink

Ulteriori informazioni qui: https://github.com/Infineon/XMC-for-Arduino

#### STM32

https://raw.githubusercontent.com/stm32duino/BoardManagerFiles/master/STM32/package_stm_index.json

#### Tutto insieme

Questi sono tutti i files json di sopra, separati da virgola:

http://arduino.esp8266.com/stable/package_esp8266com_index.json,https://raw.githubusercontent.com/jantje/arduino-esp32/master/package/package_Espressif_esp32_index.json,https://github.com/Infineon/Assets/releases/download/current/package_infineon_index.json,https://github.com/chipKIT32/chipKIT-core/raw/master/package_chipkit_index.json,https://raw.githubusercontent.com/stm32duino/BoardManagerFiles/master/STM32/package_stm_index.json


## Piattaforme da installare in altro modo

#### Teensy

Per installare il supporto per Teensy c'è il Teensyduino installer:

https://www.pjrc.com/teensy/td_download.html

Al momento della stesura di questo documento c'è la versione 1.45, che, dopo averla installata, mi ha causato un problema in Arduino IDE (l'ide si visualizza male e all'avvio vengono segnalati una serie di errori nella finestra terminale), ho installato la 1.46 Beta 9 che non mi fa questo problema ed è reperibile qui:

https://forum.pjrc.com/threads/54711-Teensy-4-0-First-Beta-Test?p=193715&viewfull=1#post193715

