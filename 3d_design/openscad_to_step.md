## Convertire un file SCAD in STEP

> Istruzioni prese [da questo link](https://forum.lulzbot.com/t/tip-converting-openscad-files-easily-to-step-with-freecad/228), tradotte e aggiornate.

Installare [FreeCad](https://www.freecadweb.org/).

Cliccare sul Menù <kbd>Visualizza</kbd>><kbd>Ambiente</kbd>><kbd>OpenScad</kbd>.

Cliccare su <kbd>Modifica</kbd>><kbd>Preferenze</kbd>

Andare alla voce `OpenScad`.

Nel campo `Eseguibile OpenSCAD` inserire il percorso verso oenscad.exe (ad esempio `C:/Program Files/OpenSCAD/openscad.exe`)

In `Importazione OpenSCAD` selezionare `Utilizza ViewProvider in visulizzazione struttura` e `Usa feature Multimatrice`.

L'impostazione `Numero massimo di facce per poligoni (fn)` è di default 16: questo vuol dire che i poligoni con un numero di facce superiori a 16 verranno renderizzati come cilindri.

Premere <kbd>OK</kbd>.

Adesso dal menù <kbd>File</kbd> è possibile aprire i files in formato `.scad`

Dall'elenco degli oggetti (`Vista combinata - Modello - Etichette & attributi`) selezionare l'oggetto principale (gli oggetti hanno l'icona formata da due cerchi sovrapposti di sbieco) e quindi andare in <kbd>File</kbd>><kbd>Esporta</kbd> e in `Salva con nome` scegliere `STEP with colors (*.step *.stp)`