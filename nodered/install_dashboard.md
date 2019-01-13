Installare NPM (Node.JS Package Manager):
```bash
$ sudo apt-get install npm
```
Installare la dashboard:
```bash
$ cd ~/.node-red
$ npm-install node-red-dashboard
```
Far eseguire nodered in automatico alla partenza del sistema:
```bash
$ sudo systemctl enable nodered.service
```
Accesso alla dashboard:
```
http://localhost:1880/ui
```
