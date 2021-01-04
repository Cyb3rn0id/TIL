### Test Raspberry Camera

Il seguente script avvia la telecamera e cattura l'immagine salvandola in `/home/pi/test.jpg`, torna utile per testare il funzionamento della telecamera:
```
raspistill -v -o test.jpg
```

Nel caso in cui venga generato un errore verificare le seguenti cose:

- che il connettore _Sunny_ (quello quadrato a pressione che dal CCD si collega al PCB della telecamera) sia correttamente agganciato: premerlo bene verso il basso
- che il flat sia correttamente innestato lato telecamera nonchè orientato bene (ha i contatti solo da un lato)
- che il flat sia correttamente innestato lato Raspberry nonchè orientato bene (ha i contatti solo da un lato)
- che il flat non sia danneggiato