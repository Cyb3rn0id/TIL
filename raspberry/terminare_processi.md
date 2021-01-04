### Processi e come terminarli

**Elenco dei processi attivi**
```
ls -A | more
```
vengono elencati tutti i processi attivi con il proprio _PID_

**Recuperare il PID di un determinato processo**

Bisogna conoscere il nome del processo, ad esempio: `_python3_`:
```
pgrep python3
```
oppure:
```
pidof python3
```
`pgrep` ritorna il PID del processo principale, `pidof` ritorna il PID del programma principale e dei processi associati

**Terminare un processo conoscendone il nome**
```
sudo pkill python3
```
**Terminare un processo conoscendone il PID**
```
sudo kill 540
```
**Terminare un processo con tutti i processi figli**

In questo caso è necessario conoscere il nome del processo:
```
sudo killall python3
```




