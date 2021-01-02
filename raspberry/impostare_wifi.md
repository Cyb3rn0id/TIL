### Impostare il WiFi all'avvio senza monitor, mouse e tastiera

Su un pc creare con Notepad++ un file dal nome _wpa_supplicant.conf_  
Su Notepad++ assicurarsi di selezionare Modifica > Converti carattere di fine linea > UNIX
Scrivere nel file:

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=it

    network={
      ssid="nome rete"
      psk="password"
      key_mgmt=WPA-PSK
    }
    
Salvarlo nella root della SD. L'impostazione è permanente.
Il contenuto di questo file viene trasferito nel file _wpa_supplicant_ che si può editare con:

    sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

Nella cartella _/files/_ è contenuto un file [wpa_supplicant.conf di esempio](/files/wpa_supplicant.conf)