# T02: DPR: còpies de seguretat. Cas pràctic

**Introducció al cas**

A la tasca anterior heu dissenyat una política de còpies de seguretat pel nostre nou client "Muntatges i Serveis Tècnics SL". Ara toca passar a l’acció i portar a la pràctica l’estudi anterior. El client demana que s’elaborin unes guies tècniques amb proves de concepte per tal que el seu personal estigui qualificat per implantar el pla de còpies de seguretat.

**Part 1: Còpia seguretat dels equips clients Windows**

Encara que en principi el DPR no contemplaria fer còpia dels arxius locals dels equips clients, se’ns demana fer una excepció amb l’equip Windows del director de l’empresa. En aquest equip es guarda informació important que no es vol tenir accessible al servidor de fitxers de l’empresa. Per aquest motiu és necessari definir una política de còpies de seguretat seguint l’esquema 3-2-1, es farà una còpia de seguretat a un disc secundari que té el propi equip i una segona còpia al cloud, en aquest cas, Google Drive usant l’eina **Duplicati.**


Com a prova de concepte per crear la guia, creareu una màquina virtual Windows 11 amb dos discos, en un instal·leu el sistema operatiu i un de secundari de 10 GB que servirà per emmagatzemar les còpies de seguretat. Per simular la part de Google Drive, useu un compte que no sigui el d’escola (podeu crear un compte específic per l’activitat).

Es desitja fer còpies de seguretat del perfil de l’usuari cada hora al disc secundari i a les 18:00 a Google Drive.
Documenteu el procediment de instal·lació de Duplicati, la configuració dels plans de còpies i observeu el funcionament. Per això, afegiu arxius a les carpetes de l’usuari, especialment a Documents.

Esborreu el contingut de Documents i procediu a fer una restauració des del disc secundari.

Comproveu com podeu fer una restauració des de la còpia que teniu emmagatzemada al cloud.

**Part 2: Còpia seguretat servidor Linux**

Per fer les còpies del servidor Linux la solució proposada pel vostre responsable és Duplicity que permet fer còpies tant contra un mitjà local o un servidor remot. Combinat amb el programador de tasques (cron) es poden implementar les polítiques de còpia que es desitgin.

Has de crear una guia tècnica per explicar com es pot usar aquesta eina per fer còpies d’un servidor Linux.

Per fer aquesta guia i com a prova de concepte, usaràs una màquina virtual amb un Ubuntu Server instal·lat i li afegiràs un segon disc de 10 GB que simularà una unitat auxiliar.

1. Inicialitza i formata en format xfs. Com simula una unitat externa, es muntarà manualment a /media/backup (primer cal crear la carpeta).
2. Instal·la duplicity.
3. Crea un parell d’usuaris més al sistema de manera que tinguin carpeta personal. Crea 4 arxius de 10 MB a la carpeta home del teu usuari.
4. Fes un còpia de seguretat de la carpeta /home.
5. Esborra els arxius i fes un restore per comprovar com es recuperen els arxius.
6. Afegeix un nou arxiu de 4 MB i fes una nova còpia. Observa com ara ha fet una còpia  incremental.

Desmunta la unitat de backup.

Ara passaràs a automatitzar el procés de les còpies utilitzant uns scripts bàsics i el programador de tasques (cron). Un aspecte molt important a nivell de seguretat, és que la unitat de backup ha d’estar per defecte, desmuntada. De manera que el primer pas sempre serà muntar la unitat i el darrer desmuntar-la, un cop s’ha fet la còpia.

7. Crea un script anomenat fullbackup.sh que realitzi la còpia completa de la carpeta /home i l’emmagatzemi al volum muntat. Usa la variable d’entorn PASSPHRASE (per donar valor a una variable d’entorn cal afegir a l’script una línia amb export PASSPHRASE=contrasenya) per no haver d’escriure la passphrase en el moment de l’execució. Recorda de donar permisos d’execució a l’script.
8. Programa al cron com a root  l’execució de l’script els diumenges a les 23:00.
9. Crea un segon script anomenat incrementalbackup.sh que realitzi còpies incrementals de la mateixa carpeta que abans. Heu de fixar el valor de la variable PASSPHRASE igual que al punt 5 i donar permisos d’execució a l’script.
10. Programa al cron l’execució d’aquest script com a root de dilluns a dissabte a les 23:00.

Materials i links de suport
●        Duplicati: https://duplicati.com/  
●        WayToIT. Creando archivos con fsutil [blog]. Març 2015. Disponible a:  
 https://waytoit.wordpress.com/2015/03/15/creando-archivos-con-fsutil/  
●        WayToIT. Creando archivos de prueba en Linux [blog]. Març 2015. Disponible a:  
 https://waytoit.wordpress.com/2015/03/21/creando-archivos-de-prueba-en-linux/  
●        Duplicity man page:  
  http://manpages.ubuntu.com/manpages/trusty/man1/duplicity.1.html  
Programant tasques amb cron:  
                      https://geekytheory.com/programar-tareas-en-linux-usando-crontab  



👉 Pots veure la solució [aquí](solucio.md)  
📍 Pots anar a la pàgina de projecte [aquí](../../README.md)
