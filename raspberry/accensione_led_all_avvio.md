## Come far accendere un LED all'avvio del Raspberry Pi  
Sistema testato su Raspberry Pi OS (debian 13 / trixie)

Recarsi nella cartella firmware:  
```bash
$ cd /boot/firmware
```  
editare il file config.txt
```bash
$ sudo nano config.txt
```  
Aggiungere una riga del tipo:  
```bash
# Set GPIO26 come uscita (op) a livello alto (dh) 
gpio=26=op,dh
```  
Salvare il file con <kbd>CTRL</kbd> <kbd>O</kbd>  
Uscire da Nano con <kbd>CTRL</kbd> <kbd>X</kbd>  

Maggiori informazioni qui: [Forum Raspberry Pi](https://forums.raspberrypi.com/viewtopic.php?f=117&t=208748)
