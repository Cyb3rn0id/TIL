### Problemi con il video HDMI (non visualizzato, monitor che dice mode non supportato)

Questo problema sembra essere dovuto a cavi HDMI che non convogliano bene le informazioni _EDID_ dal monitor/tv verso il Raspberry Pi o comunque a problemi di comunicazione tra i due dispositivi. E' un problema che potrebbe essere causato dal cavo.

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