### VNC che mostra messaggio "cannot currently show the desktop"

Questo messaggio viene mostrato da un client VNC (su un pc o sul cellulare) quando ci colleghiamo al Raspberry PI su cui è abilitato il server VNC. Le cause di questo messaggio sono molteplici. Personalmente ho risolto cambiando la risoluzione:

- Con un client SSH colleghiamoci al Raspberry Pi (personalmente utilizzo [PuTTY](https://www.putty.org/))
- Facciamo partire il `raspi-config`:  
```
sudo raspi-config  
```

- Selezionare la voce <kbd>2 Display Options</kbd>
- Selezionare la voce <kbd>D1 Resolution</kbd>
- Selezionare la massima risoluzione possibile (es.: <kbd>DMT Mode 82 1920x1080 60Hz 16:9</kbd>)
- Compare il messaggio <kbd>The resolution is set to DMT Mode 82<kbd> (se è stato scelto, chiaramente, DMT Mode 82). Premere invio
- Selezionare <kbd>Finish</kbd> in basso a destra per uscire dal `raspi-config`
- Vi viene chiesto di riavviare. Riavviate
 
Se questo non dovesse funzionare, in rete sono documentate altre soluzioni, tra cui:
 
1 - Installare `lxsession`:
```    
sudo apt-get install lxsession
```

2 - Re-Installare `lxsession` e la libreria `libgtk`:
```
sudo apt-get install --reinstall libgtk2.0-0
sudo apt-get install --reinstall lxsession
```

3 - Anche se è scontato, verificare che Raspberry parta con la GUI anzichè a riga di comando. Questo si fa sempre da `raspi-config`: <kbd>System Options > Boot / Auto Login > Desktop Autologin</kbd>

4 - Liberare spazio nella partizione di `root`. E' possibile verificare lo spazio con il comando:
```
df -h
```
Compare l'elenco delle partizioni con la percentuale di spazio utilizzata, se `dev/root/` è piena, cercare di liberare spazio oppure passare ad una microSD più capiente

5 - Altre soluzioni sono riportate, per lo stesso argomento, nel [forum di Raspberry Pi](https://www.raspberrypi.org/forums/viewtopic.php?t=216737)