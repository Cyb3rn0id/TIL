### Eliminare il messaggio all'avvio dell'SSH (password di default)

L'impostazione guidata del Raspberry Pi che si trova nella versione 2 Dicembre 2020 di Raspberry Pi OS non salva la password se l'avete modificata, per cui se dalla procedura guidata modificate la password e poi riavviate, questo messaggio di warning si presenta lo stesso. Per modificare la password è necessario utilizzare `raspi-config`.

Ad ogni modo, anche se non è consigliato, si può eliminare il programmino eseguito all'avvio che controlla se è abilitato SSH e la password è rimasta quella di default:
```
sudo apt purge libpam-chksshpwd
```