### Eseguire uno script python all'avvio

Bisogna modificare il file _/etc/rc.local_ inserendo una chiamata ad uno script _sh_ il quale a sua volta richiama l'interprete python con il nome dello script da avviare.  

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