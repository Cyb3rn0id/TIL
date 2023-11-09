# Monitor Waveshare 7" e retropie

Prova fatta su Raspberry Pi4 con RetroPie e tutti gli aggiornamenti di Ottobre 2023

Del monitor Waveshare 7" (risoluzione 1024x600, touch capacitivo) ne esistono due versioni:  

- la versione "QLED Quantum Dot" : ha i pulsanti per le regolazioni, due porte USB (una per il touch e una per l'alimentazione) e l'uscita audio su jack 3.5mm. Ha un adesivo posteriore con la scritta "7HP-CAPQLED" => [link](https://www.waveshare.com/7hp-capqled.htm)
- la versione "IPS Low Power" : questa ha soltanto una porta USB utilizzata sia per touch che per alimentazione (non ci sono i pulsanti, non c'è il jack). Questa versione ha il PCB marchiato come "rev 4.1" => [link](https://www.waveshare.com/7inch-hdmi-lcd-c.htm)

La prima versione non mi ha mai creato problemi, mentre la seconda qualche problema (risolvibilissimo) si. Ho testato questo metodo con entrambi i modelli di display.  Qui metto le istruzioni per farli funzionare correttamente in retropie, anche se dovrebbero andar bene anche per Raspberry Pi Os.  

  
Estrarre la SD e leggerla su un altro pc.  
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
config_hdmi_boost=7  
hdmi_group=2  
hdmi_mode=88  
hdmi_drive=1  
hdmi_cvt 1024 600 60 6 0 0 0
```   

(grazie a [questo gist di pierrealexaline](https://gist.github.com/pierrealexaline/0aa6d38ccdcf6cb21fc4c22387a413be)).  

Dopo aver fatto questo, al riavvio probabilmente retropie non parte e mostra questo errore:  

`Error creating SDL window / Could not get SDL display`  

Digitare `sudo raspi-config`  
Selezionare <kbd>2 Display options</kbd> e quindi <kbd>D1-resolution</kbd>.  
Nella lista dovrebbero apparire un paio di voci che normalmente non c'erano prima della modifica al config. Selezionare <kbd>DMT mode 88 1024x600 60Hz 15:9</kbd>

    è praticamente l'impostazione che abbiamo messo in config.txt, credo che questo passaggio sia comunque inutile   

Tornare al menù principale e selezionare <kbd>6 Advanced Options</kbd> e quindi <kbd>A2 GL driver</kbd>.   
Qui io ho selezionato <kbd>G2 GL (fake KMS) ...</kbd> ho riavviato e ha funzionato tutto correttamente su entrambi i modelli di display.
