# Utilizzare il Monitor touchscreen Waveshare 7" 1024x600

Prova fatta su Raspberry Pi4 con RetroPie e tutti gli aggiornamenti di Ottobre 2023

Del monitor Waveshare 7" (risoluzione 1024x600, touch capacitivo) ne esistono due versioni:  

- la versione "QLED Quantum Dot" : ha i pulsanti per le regolazioni, due porte USB (una per il touch e una per l'alimentazione) e l'uscita audio su jack 3.5mm. Ha un adesivo posteriore con la scritta "7HP-CAPQLED" => [link](https://www.waveshare.com/7hp-capqled.htm)
- la versione "IPS Low Power" : questa ha soltanto una porta USB utilizzata sia per touch che per alimentazione (non ci sono i pulsanti, non c'è il jack). Questa versione ha il PCB marchiato come "rev 4.1" => [link](https://www.waveshare.com/7inch-hdmi-lcd-c.htm)

La prima versione non mi ha mai creato problemi, mentre la seconda qualche problema (risolvibilissimo) si. Ho testato questo metodo con entrambi i modelli di display.  Qui metto le istruzioni per farli funzionare correttamente in retropie, anche se dovrebbero andar bene anche per Raspberry Pi Os.  
  
Estrarre la SD e leggerla su un altro pc (oppure editare il config.txt con nano)  
Aprire il file <kbd>config.txt</kbd>    
Andare in fondo al file fino alla sezione `[rpi4]`: commentare (mettere #) davanti alle due righe:  

```
dtoverlay=vc4-fkms-v3d
max_framebuffers=2
```  

Le due righe in questione dovranno quindi apparire così:  

```
#dtoverlay=vc4-fkms-v3d
#max_framebuffers=2
```

Sotto aggiungere questa parte:  

```
max_usb_current=1  
hdmi_force_hotplug=1  
config_hdmi_boost=5  
hdmi_group=2  
hdmi_mode=87  
hdmi_drive=1  
hdmi_cvt=1024 600 60 6 0 0 0
```   

(grazie a [questo gist di pierrealexaline](https://gist.github.com/pierrealexaline/0aa6d38ccdcf6cb21fc4c22387a413be)).  

    Nota: per una versione di Raspberry Pi inferiore alla 4, tutto questo va fatto al di sopra della sezione `[rpi4]`
  
Spiegazione dei flag:  
- `max_usb_current=1` Serve ad abilitare la massima corrente erogabile sulle porte USB dato che il monitor verrà alimentato da li. Questo flag, in realtà, su Raspberry Pi4 non ha nessun effetto dato che su questo SBC già viene erogata la corrente massima su USB
- `hdmi_force_hotplug=1` Forza l'attivazione dell'uscita HDMI anche se non viene rilevato nessun monitor collegato
- `config_hdmi_boost=5` Qui è impostabile un valore da 0 (debole) a 11 (forte) che determina la potenza del segnale sul cavo HDMI, si aumenta questo valore in caso di cavi molto lunghi o presenza di interferenze a video
- `hdmi_group=2` Specifica il tipo di HDMI (1=CEA, 2=DMT). CEA (Consumer Electronics Association) è utilizzato per le TV e supporta le risoluzioni normalmente utilizzate dalle semplici televisioni, DMT (Display Monitor Timings) è utilizzato per i monitor, che supportano svariate risoluzioni che normalmente non si trovano sulle normali TV, viene usata questa modalità anche per risoluzioni non standard.
- `hdmi_mode=87` Questo valore assume un significato diverso a seconda del valore di `hdmi_group`. In particolare, per hdmi_group=2, un valore superiore ad 86 indica una modalità "personalizzata", ovvero con valori larghezza/altezza/refresh non tabellati (vedi in fondo "link utili").
- `hdmi_drive=1`  1=modalità DVI senza suono, 2=modalità HDMI (sul display tipo QLED potete mettere il valore 2 se volete estrarre l'audio da HDMI e sfruttare quini il jack incluso su quel modello di monitor - a me con hdmi_drive=2 succedono cose strane: il display comincia, un po' alla volta, a fare una vignettatura come incominciasse a "bruciarsi" nei 4 angoli)
- `hdmi_cvt=1024 600 60 6 0 0 0` CVT sta per Coordinated Video Timing (anche se a me piace pensare alla 'C' come 'custom'):
    - Il formato di questo flag è `hdmi_cvt=[width] [height] [framerate] [aspect] [margins] [interlace] [rb]` e solo i primi 3 valori sono obbligatori, mentre i restanti sono facoltativi. Abbiamo quindi impostato:
    -  width=1024
    -  height=600
    -  framerate=60Hz
    -  aspect=6 (aspect ratio, questo valore imposta 15:9), valori possibili:
        -  1=4:3
        -  2=14:9
        -  3=16:9
        -  4=5:4
        -  5=16:10
        -  6=15:9
        -  Nota: Nessuno di questi valori è identico alla risoluzione del monitor in questione, quindi mettiamo un valore che si avvicina, dovrebbe andare bene anche 3 (16:9)
    -  margins=0 (0=margini disabilitati, 1=margini abilitati. Questo flag sembra essere l'opposto dell'opzione di configurazione disable_overscan)
    -  interlace=0 (0=scansione progressiva, 1=interlacciato)
    -  rb=0 (reduced blanking, 0=disabilitato, 1=abilitato)

    Nota: volendo utilizzare entrambe le uscite HDMI sui raspberry da 4 in su, è possibile utilizzare monitor diversi e quindi specificare diverse impostazioni per per `hdmi_cvt` postponendo uno 0 per uscita HDMI0 o un 1 per uscita HDMI1, frapponendo il segno di due punti (`hdmi_cvt:0` e `hdmi_cvt:1`).

    Nota2: Se anche tutto questo non funziona, c'è un ulteriore flag di configurazione, `hdmi_timings`, ancora più complicato e spiegato bene nel tutorial di Adafruit linkato in basso

### Problema 'SDL Window' su Retropie
Se state utilizzando questa configurazione su retropie, dopo aver fatto tutto, al riavvio probabilmente retropie non partirà mostrando questo errore:  

`Error creating SDL window / Could not get SDL display`  

E si viene riportati al prompt dei comandi. Digitare `sudo raspi-config`  per avviare raspi-config.
Selezionare l'opzione <kbd>2 Display options</kbd> e quindi <kbd>D1-resolution</kbd>.  
Nella lista dovrebbero apparire un paio di voci che normalmente non c'erano prima della modifica al config. Selezionare <kbd>DMT mode 87 1024x600 60Hz 15:9</kbd>

    è praticamente l'impostazione che abbiamo messo in config.txt, credo che, in realtà, questo passaggio sia inutile

Tornare al menù principale e selezionare <kbd>6 Advanced Options</kbd> e quindi <kbd>A2 GL driver</kbd>.   
Qui io ho selezionato <kbd>G2 GL (fake KMS) ...</kbd> ho riavviato e ha funzionato tutto correttamente su entrambi i modelli di display.

### Link utili
- [Tutti i parametri impostabili in config.txt](https://elinux.org/RPi_Configuration)
- [tutorial Adafruit fatto molto bene](https://learn.adafruit.com/using-weird-displays-with-raspberry-pi/everything-else)
- [Tabella con gli HDMI mode](https://onlinelibrary.wiley.com/doi/pdf/10.1002/9781119415572.app3)
