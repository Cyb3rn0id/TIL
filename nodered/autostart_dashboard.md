## Come far partire in automatico la dashboard di Node-Red all'avvio di Raspberry Pi OS  
Sistema testato su Raspberry Pi OS (debian 13 / trixie) ma con qualche problema

Recarsi nella cartella autostart:  
```bash
$ cd /etc/xdg/autostart
```  
creare un file con estensione .desktop  
```bash
$ sudo nano chromium.desktop
```  
Incollare al suo interno il seguente contenuto:  
```bash
[Desktop Entry]
Type=Application
Exec=/usr/lib/chromium/chromium --noerrdialogs --disable-session-crashed-bubble --disable-infobars --start-fullscreen http://127.0.0.1:1880/dashboard
Hidden=false
X-GNOME-Autostart-enabled=true
Name=ChromiumKioskAutostart
Comment=Start Chromium when GUI starts
```  
Salvare il file con <kbd>CTRL</kbd> <kbd>O</kbd>  
Uscire da Nano con <kbd>CTRL</kbd> <kbd>X</kbd>  
  
## Problemi riscontrati
1. nonostante la presenza del flag _--disable-session-crashed-bubble_ che serve a non far comparire il messaggio 'Chromium non si è chiuso correttamente ecc ecc', questo messaggio spesso compare lo stesso  
2. spesso e volentieri chromium parte si a pieno schermo ma copre solo metà monitor: la cosa è anomala in quanto chromium risulta essere proprio a pieno schermo (infatti compare il messaggio 'tenere premuto ESC' per uscire da schermo intero)  
  
## Note  
Esplorando da GUI la cartella _/etc/xdg/autostart_ i files ivi contenuti non compaiono come _nome.desktop_ ma con il nome indicato al campo _Name_ presente nel file
