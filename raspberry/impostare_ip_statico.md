### Impostare IP statico col Wi-Fi

Controllare lo stato del servizio `dhcpcd`:
```
sudo service dhcpcd status
``` 
Dovrebbero uscire dei messaggi in cui dice che il servizio è attivo, se così non fosse, attivarlo e fare in modo che si attivi in automatico all'avvio:
```
sudo service dhcpcd start
sudo systemctl enable dhcpcd
```    
Ora aprire il file `dhcpcd.conf`
```
sudo nano /etc/dhcpcd.conf
```
Aggiungere alla fine del file:
```
interface wlan0
static ip_address=192.168.1.13/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8 8.8.4.4
noipv6
```    
Cambiare gli indirizzi ip: nell'esempio il `13` è quello che voglio assegnare e `1` (static_routers) è quello del router, lasciare lo `/24` alla fine dell'indirizzo IP.

Gli altri due indirizzi IP in `domain_name_server`, oltre a quello del router, sono dei server DNS di Google. Le versioni precedenti di Raspbian accettavano `SSID (nome della rete WiFi)` al posto di `interface wlan0` e `inform 192.168.1.13` al posto di `static ip_address=192.168.1.13/24`

Provando ad utilizzare queste vecchie sintassi si nota che il simbolo del WiFi sul raspberry scorre di continuo (per dire: _collegamento in corso_) anzichè rimanere fisso, andando a controllare il servizio DHCPCD come illustrato prima viene scritto in rosso `unknown option: SSID_` e utilizzando un'app come [FING](https://play.google.com/store/apps/details?id=com.overlook.android.fing&hl=it&gl=US) su Android, viene rilevato che l'indirizzo IP è assegnato ma il Raspberry è comunque invisibile alla rete (non è possibile collegarsi ad internet, non si può usare SSH, VNC ecc). 

Cambiando solo `SSID` con `interface wlan0`, il servizio DHCPCD non mostra errori ma si ha lo stesso comportamento: Raspberry invisibile alla rete. La sintassi da utilizzare, che a me ha funzionato su Raspberry Pi4 con l'ultima versione (dicembre 2020) di Raspberry Pi OS, è quella illustrata sopra.

Se il nostro dispositivo viene collegato successivamente ad un altro che "si è preso" quell'indirizzo IP, il Raspberry non si riuscirà a collegare: in questi casi dando `sudo service dhcpcd status` è possibile leggere degli errori in rosso nel report, ad esempio viene restituito:  
```
wlan0: hardware address xx:xx:xx:xx:xx:xx claims 192.168.1.13
wlan0: DAD detected 192.168.1.13
control_handle_data: Operation not permitted
```    
dove la serie di _xx_ è il MAC Address del dispositivo a cui è stato assegnato l'indirizzo IP (192.168.1.13 nell'esempio) che abbiamo impostato come statico nel file `dhcpcd.conf`. 
 
 A questo punto la cosa migliore da fare, in ogni caso, è quella di assegnare indirizzi IP statici direttamente dal router.

 ### Assegnare indirizzo IP statico nel router TIM agcombo

 Nel router della TIM, ad esempio, è possibile farlo dal menù<kbd>Il mio Media Access Gateway</kbd> > <kbd>DHCPv4</kbd> 
 qui bisogna cliccare <kbd>Mostra Controlli avanzati</kbd> e compare una sezione <kbd>Indirizzi IP Statici</kbd>, cliccando sul tasto <kbd>Aggiungere indirizzo statico</kbd> è possibile selezionare da un elenco il dispositivo nella colonna <kbd>Nomehost</kbd>: in questo caso il campo del MAC Address viene compilato in automatico, altrimenti se il nostro dispositivo non compare perchè non si è collegato, possiamo scrivere l'indirizzo MAC a mano.

 ![IP statico modem TIM](img/ip_fisso_modem_tim.png)