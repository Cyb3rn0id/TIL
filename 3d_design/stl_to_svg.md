## Convertire una sezione di un modello STL in SVG

Scaricare ed installare [OpenScad](https://openscad.org/)  
  
Dalla schermata iniziale cliccare sul tasto <kbd>NEW</kbd>  

Nella finestra dell'editor creare un semplice script:  
```
projection(cut=true)
translate([0,0,-2])
import("C:/path/modello.stl");
```

La prima riga dice ad openscad di 'fare una fetta' del modello STL visualizzato all'incrocio degli assi cartesiani, sul piano delimitato dall'asse X.  

La seconda riga dice ad OpenScad di traslare il modello lungo X,Y,Z dei valori riportati. Nell'esempio ho messo Z a -2 per fare in modo che il modello 'scenda' di 2mm verso il basso perchè desidero il taglio a quell'altezza. Da premettere che il modello nel file STL deve essere già orientato correttamente in quanto questo comando esegue solo la traslazione.  

La terza riga importa il modello STL in OpenScad. Scrivere il percorso completo per sicurezza ed utilizzare lo Slash (<kbd>Shift 7</kbd>) e non il backslash.  

Premere quindi il tasto `Preview` (o premere <kbd>F5</kbd>) e quindi il tasto `Render` (o premere <kbd>F6</kbd>).  

Esportare quindi con `File` > `Export` > `Export as SVG`