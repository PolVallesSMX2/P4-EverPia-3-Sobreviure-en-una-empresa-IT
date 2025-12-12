# T02: DPR: còpies de seguretat. Cas pràctic
## PART 1: Windows 11 + Duplicati

Haurem de configurar una maquina virtual Windows afegint un disc dur (virtual) de 10 GB per a les còpies.

![capt](img/1.png)

També crearem un nou compte de google drive per tenir espai d’emmagatzematge cloud.

![capt](img/2.png)

Seguidament accedim a la web
[duplicati.com/download](duplicati.com/download)
I descarguem duplicati per a Windows.

![capt](img/3.png)

Un cop instal·lat l’obrim i sens obrira la web/app, en cas que no obri accedim des de l’url:
 
127.0.0.1:8200/ngclient/

![capt](img/4.png)

Un cop accedit per primer cop ens demanara introduïr una contrasenya, un cop desada ja estarem dins l’interfície.

![capt](img/5.png)

Ara crearem un nou backup des d’aquesta eina.

![capt](img/6.png)

Seguirem els passos demanats i introduirem nom, descripció, xifratge, contrasenya…

![capt](img/7.png)

Seleccionem la destinació del nostre sistema (File System)

![capt](img/8.png)

Seguidament haurem de seleccionar la ruta del nostre disc on guardarem les copies. En cas que no aparegui el nostre disc, haurem de inicialitzar el disc com vam aprendre al primer curs.

![capt](img/9.png)

Haurem de seleccionar quines dades o d’on s’hauran de extreure les dades.

![capt](img/10.png)

Farem click a seguent i escollirem quan s’executa la còpia.

![capt](img/11.png)

Seguidament haurem d’afegir l’opció passphrase per introduir una contrasenya. També haurem d’afegir l’opcio “snapshot-policy”

![capt](img/12.png) ![capt](img/13.png)

Ara podrem observar com ja tenim aquest backup creat correctament, l’executarem per provar el correcta funcionament.

![capt](img/14.png)

Un cop el procés ha finalitzat si obrim l’explorador d’arxius podem observar com s’han guardat les dades de forma xifrades.

![capt](img/15.png)

Ara veurem com fer backups a google drive.

Crearem un nou backup, però aquest cop seleccionarem el destí Google Drive.

![capt](img/16.png)

Un cop avancem, haurem de vincular duplicati amb google drive, per fer-ho farem clic sobre l’enllaç AuthID.

![capt](img/17.png)

I iniciarem la sessió amb el nostre compte de Google (nou).

![capt](img/18.png)

També haurem de indicar la ruta de la carpeta on volem guardar les dades, per fer-ho introduirem la url en el camp Ruta de la carpeta.

![capt](img/19.png) ![capt](img/20.png)

Seleccionem les mateixes dades d’origen.

![capt](img/21.png)

Definim quan s’executarà, diariament a les 18:00

![capt](img/22.png)

Afegirem l'opció passphrase com a l’anterior amb una contrasenya i snapshot-policy.

Executem el backup de Drive per realitzar un test.

![capt](img/23.png)

Al finalitzar podrem confirmar el correcta funcionament revisant la carpeta de google drive.

![capt](img/24.png)

Ara farem algunes proves de les còpies i restauració, crearem un arxiu dins la ruta del usuari.

Crearem un arxiu dins el nostre directori personal amb la comanda:

```bash
fsutil file createnew C:\Users\[USUARI]\Documents\test1.txt 10485760
```

![capt](img/25.png)

Seguidament farem una còpia des de duplicati, borrarem aquest arxiu i restaurarem desde l’eina.

![capt](img/26.png) ![capt](img/27.png)  

![capt](img/28.png)

Si tot ha funcionat, podem observar com el document ha tornat al seu lloc. També podem revisar de la mateixa forma el funcionament del backup amb Google Drive. Aquest s'ha de crear de la mateixa manera que l'anterior però seleccionant el mètode Google Drive.

Executem una còpia a google drive, eliminem el fitxer manualment, i restaurem.

![capt](img/29.png) ![capt](img/30.png)

Seleccionem la carpeta Documents i continuem.

![capt](img/31.png)

Si tot ha funcionat, podem observar com el document ha tornat al seu lloc.

## Part 2: Còpia seguretat servidor Linux

De la mateixa manera que la VM de Windows haurem de tenir dos disc durs, el per defecte i un segon on guardarem les còpies. 

![capt](img/32.png)

Un cop dins la màquina verifiquem que estigui detectant aquest.
```bash
lsblk
```

![capt](img/33.png)

Creem una partició sobre el nou disc amb la comanda:
```bash
sudo fdisk /dev/sdb
```

![capt](img/34.png)

Un cop ens aparegui el “menu” indicarem les instruccions:
n → Per crear una nova partició
p → indiquem que es primària
Enter
Enter
Enter
W → Guardar i sortir

![capt](img/35.png) ![capt](img/36.png)

Formategem el disc en format XFS, pero primer de tot haurem d’instal·lar el servei XFS 
```bash
sudo apt install xfsprogs
```
![capt](img/37.png)

```bash
sudo mkfs.xfs /dev/sdb1
```
![capt](img/38.png)

Seguidament crearem una carpeta i muntarem el disc a aquesta.
```bash
sudo mkdir -p /media/backup
sudo mount /dev/sdb1 /media/backup
```
![capt](img/39.png)

Podem comprovar si està muntat correctament amb la comanda.
```bash
df -h | grep backup
```
![capt](img/40.png)

Ara instal·larem duplicity, l’eina per automatitzar les còpies.
```bash
sudo apt install duplicity -y
duplicity –version
```
![capt](img/41.png)

Crearem dos usuaris, asegurant-nos que tenen directoris personals.
```bash
sudo adduser usuari1
sudo adduser usuari2
```
![capt](img/42.png)

Ara crearem 4 fitxers de 10 MB dins el directori que hem creat anteriorment.
for i in 1 2 3 4; do sudo dd if=/dev/zero of=fitxer$i bs=1M count=10; done

![capt](img/43.png)

Comprovem amb `ls -lh`

![capt](img/44.png)

Crearem la copia amb duplicity, ens demana un passphrase (contrasenya) la qual la xifrarà.
```bash
sudo duplicity /home file:///media/backup/home-backup
```

![capt](img/45.png)

Al finalitzar, podem observar que hi ha al directori destí.

![capt](img/46.png)

Seguidament esborrarem els arxius de prova creats anteriorment per veure si els pot restaurar correctament.
```bash
sudo rm fitxer1 fitxer2 fitxer3 fitxer4
ls
```

![capt](img/47.png)

Ara restaurarem els arxius amb duplicity
```bash
sudo duplicity restore file:///media/backup/home-backup /home/restored
ls /home/restored/usuari
```

![capt](img/48.png)

Com podem observar ens ha restaurat els fitxers.

Ara afegirem un fitxer nou i veurem com la nova còpia és incremental.​
```bash
sudo dd if=/dev/zero of=fitxer_nou bs=1M count=4
ls -lh
```

![capt](img/49.png)

Executarem la mateixa comanda d’abans per crear la còpia.
```bash
sudo duplicity /home file:///media/backup/home-backup
```

![capt](img/50.png)

Podem veure l’informació del backup
```bash
sudo duplicity collection-status file:///media/backup/home-backup
```

![capt](img/51.png)

Ara desmontem l’unitat
```bash
sudo umount /media/backup
```
I comprovem 
```bash
df -h | grep backup
```

![capt](img/52.png)

Ara automatitzarem tots aquest procesos amb un script.
```bash
sudo nano /root/fullbackup.sh
```

```bash
#!/bin/bash

mount /dev/sdb1 /media/backup

export PASSPHRASE="la_teva_contrasenya"

duplicity full /home file:///media/backup/home-backup

unset PASSPHRASE

umount /media/backup
```

![capt](img/53.png)

Ara donem permisos d’execució a aquest script.
```bash
sudo chmod +x /root/fullbackup.sh
```
I el provem manualment
```bash
sudo /root/fullbackup.sh
```

![capt](img/54.png)

Si no dóna errors, està bé.​

Ara programarem l'execució amb cron.
```bash
sudo crontab -e
```
I afegim aquesta línea al final:
```bash
0 23 * * 0 /root/fullbackup.sh
```

![capt](img/55.png)

Guardem els canvis amb 
```bash
sudo crontab -l
```

![capt](img/56.png)

Ara crearem un altre script que farà el mateix però fent una còpia incremental
```bash
sudo nano /root/incrementalbackup.sh
```

![capt](img/57.png)

Desem i sortim

Donem permisos d’execució a l’script
```bash
sudo chmod +x /root/incrementalbackup.sh
```
El provem manualment
```bash
sudo /root/incrementalbackup.sh
```

![capt](img/58.png)

Ara afegim aquest script al cron també, tornem com a root a crontab
```bash
sudo crontab -e
```
A sota de la línia anterior, afegim:
```bash
0 23 * * 1-6 /root/incrementalbackup.sh
```

![capt](img/59.png)

Desem els canvis
```bash
sudo crontab -l
```

![capt](img/60.png)
