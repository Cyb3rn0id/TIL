### VNC che mostra messaggio "cannot currently show the desktop"

Questo messaggio viene mostrato da un client VNC (su un pc o sul cellulare) quando ci colleghiamo al Raspberry PI su cui è abilitato il server VNC. Le cause di questo messaggio sono molteplici. Personalmente ho risolto cambiando la risoluzione:

- Con un client SSH colleghiamoci al Raspberry Pi (personalmente utilizzo PuTTY)
- Facciamo partire il _raspi-config_:

    sudo raspi-config
    
 - Selezionare la voce _2 Display Options_
 - Selezionare la voce _D1 Resolution_
 - Selezionare la massima risoluzione possibile (es.: _DMT Mode 82 1920x1080 60Hz 16:9_)
 - Compare il messaggio _The resolution is set to DMT Mode 82_ (se è stato scelto, chiaramente, DMT Mode 82). Premere invio
 - Selezionare _Finish_ in basso a destra per uscire dal Raspi-Config
 - Vi viene chiesto di riavviare. Riavviate
 
Se questo non dovesse funzionare, in rete sono documentate altre soluzioni, tra cui:
 
1 - Installare _lxsession_:
    
    sudo apt-get install lxsession
     
2 - Re-Installare _lxsession_ e la libreria _libgtk_:
   
    sudo apt-get install --reinstall libgtk2.0-0
    sudo apt-get install --reinstall lxsession
    
3 - Anche se è scontato, verificare che Raspberry parta con la GUI anzichè a riga di comando (questo si fa sempre da _raspi-config_: _System Options_ > _Boot / Auto Login_ > _Desktop Autologin_)

4 - Liberare spazio nella partizione di _root_. E' possibile verificare lo spazio con il comando:

    df -h

Compare l'elenco delle partizioni con la percentuale di spazio utilizzata, se _/dev/root/_ è piena, cercare di liberare spazio oppure passare ad una microSD più capiente

5 - Altre soluzioni sono riportate, per lo stesso argomento, nel [forum di Raspberry Pi](https://www.raspberrypi.org/forums/viewtopic.php?t=216737)
