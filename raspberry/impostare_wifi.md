### Impostare il WiFi all'avvio senza monitor, mouse e tastiera

Su un pc creare con Notepad++ un file dal nome `wpa_supplicant.conf`  
Su Notepad++ assicurarsi di selezionare <kbd>Modifica > Converti carattere di fine linea > UNIX</kbd>
Scrivere nel file:
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=it

network={
  ssid="nome rete"
  psk="password"
  key_mgmt=WPA-PSK
  }
```    
Salvarlo nella root della SD. L'impostazione è permanente.
Il contenuto di questo file viene trasferito nel file `_wpa_supplicant_` di sistema che si può editare con:
```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
Nella cartella `/files/` di questo repository è contenuto [un file wpa_supplicant.conf di esempio](/files/wpa_supplicant.conf)