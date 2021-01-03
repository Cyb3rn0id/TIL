### Raspberry Pi che non si collega al WiFi

Questo problema l'ho avuto spesso con il Raspberry Pi4 mentre non l'ho mai avuto con il 3, nè con il 2 munito di dongle WiFi compatibile. 
La procedura guidata mostra il messaggio "Unable to connect to the network". Il problema può presentarsi sempre anche con il _wpa_supplicant.conf_ correttamente configurato.

Il motivo del mancato collegamento è un mistero. La prima cosa da fare, piuttosto scontata, è quella di controllare la corretta digitazione della password.  
Successivamente, su internet sono documentate condizioni particolari causate dall'utilizzo di particolari cavi HDMI con una certa risoluzione.
Esempi:

- [Dal forum ufficiale di Raspberry Pi](https://www.raspberrypi.org/forums/viewtopic.php?t=254640)
- [Dal Hackaday](https://hackaday.com/2019/11/28/raspberry-pi-4-hdmi-is-jamming-its-own-wifi/)

Per cui il primo consiglio è:

- Provate ad abbassare la risoluzione (lo potete fare dal _raspi-config_).
- Se ne avete la possibilità, provate a cambiare cavetto HDMI

Se tutto questo non funziona, provate queste altre soluzioni:

**Abilitate l'hotspot sul cellulare** - provate a collegarvi all'hotspot generato dal cellulare: a questo il Raspberry PI si collega? Se si, spegnete l'hotspot e vedete se ora si collega alla rete WiFi configurata. Per me la soluzione è stata proprio questa, dopo essermi collegato una volta all'hotspot del cellulare, poi Raspberry si è sempre collegato a qualsiasi altra rete. Questa cosa davvero per me non ha alcun senso.

**Riavviate il router o l'access point** - sembra assurdo anche questo, ma lo spegni/riaccendi molto spesso risolve tutti i problemi. Se invece siete costretti a ripetere questa cosa ogni volta che spegnete e riaccendete il Raspberry... allora il problema è sicuramente da ricercare in altro.

**Cambiate il canale di trasmissione** - in genere i router o gli access point hanno impostato il canale in automatico, provate a mettere un canale fisso.

**Cambiate la modalità WiFi** - in genere i router o gli access point hanno abilitata la modalità WiFi b/g/n o automatica: provate a cambiarla mettendo, se c'è la possibiltà, la modalità "solo N".

Su internet alcuni danno il consiglio di non utilizzare il carattere _underscore_ nel nome della rete WiFi perchè qualcuno è riuscito a collegarsi dopo aver compiuto questa operazione. 
In realtà anche io ho l'underscore nel SSID della mia rete, ma comunque non riuscivo a collegarmi nemmeno dopo averlo tolto. In aggiunta ho messo l'underscore anche nel nome dell'hotspot del cellulare e invece qui si collegava sempre, pertanto la questione dell'underscore per me non ha funzionato.
