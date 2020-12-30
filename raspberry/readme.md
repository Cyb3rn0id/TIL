### Problemi con il video HDMI (non visualizzato, monitor che dice mode non supportato)
Togliere la microSD dal raspberry e aprirla con un PC (anche con windows).  
La partizione di boot è formattata FAT32 per cui Windows la legge.  
Aprire con un editor di testo (notepad++) il file config.txt  
Da Notepad++ assicurarsi di mettere modifica>converti carattere di fine linea>unix
togliere la nota (#) da hdmi_safe=1  
salvare e chiudere. Mettere nella raspberry.  
Dovrebbe partire con una risoluzione di default di 720x480.  
Da Start>Preferenze>Configurazione Raspberry Pi andare in "schermo" e provare a cambiare risoluzione.  
Quando viene dato ok e chiesto di riavviare, non riavviare.  Spegnere il raspberry pi.  
Togliere la scheda, rileggere il file config.txt e rimettere la nota ad hdmi_safe=1
Sotto scrivere:  hdmi_ignore_edid=0xa5000080   
questo farà in modo che il raspberry ignori le informazioni inviate dal monitor via hdmi.
Se non funziona, ripetere la procedura impostando altre risoluzioni. 

### Abilitare SSH all'avvio
Creare un file di testo vuoto e chiamarlo SSH, senza estensione. Copiarlo nella root della scheda SD.
L'impostazione è permanente.

### Impostare il WiFi all'avvio
Creare un file wpa_supplicant.conf e scriverci dentro:

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=it

    network={
      ssid="nome rete"
      psk="password"
    }
    
Salvarlo nella root della SD. L'impostazione è permanente.

### Impostare IP statico col Wi-Fi

    sudo nano /etc/dhcpcd.conf
    
Aggiungere alla fine del file:

    SSID nomedellarete
    inform 192.168.1.13
    static routers=192.168.1.1
    static domain_name_servers=8.8.8.8 8.8.4.4
    noipv6
    
Cambia gli indirizzi ip (nell'esempio il 13 è quello che voglio assegnare e 1 -static_routers- è quello del router).  
Gli altri due indirizzi IP sono di google. Mi è capitato col raspberry pi4 che alcuni indirizzi IP, anche se validi e il raspberry si collegava alla rete, il raspberry rimane comunque "invisibile" alla rete per cui i servizi come internet, SSH e VNC non funzionano. La cosa migliore è fargli assegnare l'IP in automatico e poi usare lo stesso IP assegnato come fisso.

### Eliminare il messaggio all'avvio dell'SSH che rompe sulla password di default

    sudo apt purge libpam-chksshpwd
    
Questo elimina un programmino che fa il check della password all'avvio

