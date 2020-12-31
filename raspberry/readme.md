### Problemi con il video HDMI (non visualizzato, monitor che dice mode non supportato)

Questo problema sembra essere dovuto a cavi HDMI che non convogliano bene le informazioni _EDID_ dal monitor/tv verso il Raspberry Pi o comunque a problemi di comunicazione tra i due dispositivi.  

- Togliere la microSD dal Raspberry e aprirla con un PC (anche con windows: La partizione di boot è formattata FAT32 per cui Windows la legge)
- Aprire con un editor di testo (Notepad++) il file config.txt (da Notepad++ assicurarsi di selezionare Modifica > Converti carattere di fine linea > UNIX)
- Togliere la nota (#) dalla riga _hdmi_safe=1_  
- Salvare e chiudere. Metti la microSD nella raspberry.  
- Dovrebbe partire con una risoluzione di default di 720x480.  
- Da Start > Preferenze > Configurazione Raspberry Pi andare in _Schermo_ e provare a cambiare risoluzione.  
- Quando viene dato ok e chiesto di riavviare, __non__ riavviare.  
- Spegnere il Raspberry pi.  
- Togliere la scheda, rileggere il file config.txt da un pc e rimettere la nota ad hdmi_safe=1
- Sotto scrivere:  _hdmi_ignore_edid=0xa5000080_ (questo farà in modo che il Raspberry ignori le informazioni inviate dal monitor via hdmi)
- Salvare e rimettere la scheda nel Raspberry.
Se non funziona, ripetere la procedura impostando altre risoluzioni. 

### Abilitare SSH all'avvio senza monitor, mouse e tastiera

Creare un file di testo vuoto e chiamalo SSH, senza estensione.  
Copiarlo nella root della scheda SD. L'impostazione è permanente.

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

### Impostare IP statico col Wi-Fi

Controllare lo stato del servizio dhcpcd:

    sudo service dhcpcd status
    
Dovrebbero uscire dei messaggi in cui dice che il servizio è attivo, se così non fosse, attivarlo e fare in modo che si attivi in automatico all'avvio:

    sudo service dhcpcd start
    sudo systemctl enable dhcpcd
    
Ora aprire il file _dhcpcd.conf_

    sudo nano /etc/dhcpcd.conf
    
Aggiungere alla fine del file:

    interface wlan0
    static ip_address=192.168.1.13/24
    static routers=192.168.1.1
    static domain_name_servers=192.168.1.1 8.8.8.8 8.8.4.4
    noipv6
    
Cambiare gli indirizzi ip (nell'esempio il 13 è quello che voglio assegnare e 1 -static_routers- è quello del router, lasciare lo /24 alla fine dell'indirizzo IP).  
Gli altri due indirizzi IP sono dei server DNS di Google. Le versioni precedenti di Raspbian accettavano _SSID (nome della rete WiFi)_ al posto di _interface wlan0_ e _inform 192.168.1.13_ al posto di _static ip_address=192.168.1.13/24_ provando ad utilizzare queste vecchie sintassi si nota che il simbolo del WiFi sul raspberry scorre di continuo (per dire: collegamento in corso) anzichè rimanere fisso, andando a controllare il servizio DHCPCD come illustrato prima viene scritto in rosso _unknown option: SSID_ e utilizzando un'app come FING su Android, viene rilevato che l'indirizzo IP è assegnato ma il Raspberry è comunque invisibile alla rete (non è possibile collegarsi ad internet, non si può usare SSH, VNC ecc). Cambiando solo _SSID_ con _interface wlan0_, il servizio DHCPCD non mostra errori ma si ha lo stesso comportamento: Raspberry invisibile alla rete. La sintassi da utilizzare, che a me ha funzionato su Raspberry Pi4 con l'ultima versione (dicembre 2020) di Raspberry Pi OS, è quella illustrata sopra.

### Eliminare il messaggio all'avvio dell'SSH che rompe sulla password di default

    sudo apt purge libpam-chksshpwd
    
Questo elimina un programmino che fa il check della password all'avvio

### Eseguire uno script python all'avvio

Bisogna modificare il file /etc/rc.local inserendo una chiamata ad uno script sh il quale a sua volta richiama l'interprete python con il nome dello script da avviare.  
Creare un file nella cartella desiderata (esempio, chiamo il file _startup.sh_):

    sudo nano startup.sh

Scrivere nel file:

    #!/bin/sh
    sudo python3 nomedelprogrammapython.py

Chiudere e salvare. Fornire i permessi di esecuzione al file sh:

    sudo chmod 777 startup.sh

Aprire il file rc.local:

    sudo nano /etc/rc.local
    
Alla fine del file (dopo l'istruzione _fi_), aggiungere il nome del file sh completo di percorso e seguito da start:

    //home/pi/startup.sh start
    
Chiudere e salvare. Al prossimo riavvio il file python sarà eseguito in automatico

### Test Raspberry Camera

    raspistill -v -o test.jpg
