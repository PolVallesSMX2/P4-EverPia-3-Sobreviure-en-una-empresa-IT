# a) FASE 1 POL
## QUE COPIAREM?
- Bases de dades perquè són dades crítiques i usades diariament.
- Documents de Projectes que contenen plànols i especificacions tècniques importants.
- Carpetes Documents del Usuaris ja que també poden contenir informació de treball important.
Com a tal no cal fer una copia completa de tots els arxius personals del Usuaris (equips clients), ja que guardarem possiblement molta informació innecessària com arxius temporals o personals. Com aquesta empresa els Usuaris guarden la informació important dins de les Carpetes “Documents” simplement caldrà copiar aquestes.
## CADA QUAN I DE QUINA MANERA?
- Bases de dades: Còpies incrementals cada 4 hores per complir amb l’RPO de 4 hores, i una còpia completa setmanal.
- Documents de Projectes i Carpetes Personals: còpia diferencial diària i còpia completa setmanal.
- Equips clients (carpetes Documents): còpia incremental o sincronització diària.
## QUIN MITJA USAR I ON GUARDAR LES DADES
- Mitjà local: NAS (Network Attached Storage) per fer còpies ràpides i accessibles localment.
- Mitjà extern: còpia al núvol (Cloud) com Azure, Google Cloud o servei local, per garantir còpia fora de lloc.
- Discs externs per a copies mensuals/setmanals com SSD, HDD, Cintes magnètiques…
Regla 3-2-1:
3 còpies, 2 tipus de mitjans diferents (NAS + cloud), i 1 còpia fora de lloc (cloud).

# b) FASE 1 XAVI
## Dades a Copiar (Priorització)
- Bases de Dades (Comptabilitat i Clients, 20 GB): dades crítiques, d’ús diari.
- Documents de Projectes (300 GB): importants per a l’activitat, amb creixement moderat i RPO de 24 h.
- Carpetes Personals (100 GB): necessàries per a la feina diària, però menys crítiques que la BD.
- Equips Clients (Windows 10/11): no cal fer còpia completa de tots els PC, ja que la majoria treballen amb fitxers al servidor. Només caldria contemplar còpia dels Documents locals.
##Periodicitat i Tipus de Còpia
- Bases de Dades (Comptabilitat/Clients):
  - Incremental cada 4 h (per complir RPO ≤ 4 h).
  - Completa diària.
- Documents de projectes:
  - Incremental diària.
  - Completa setmanal.
- Carpetes personals:
  - Incremental diària.
  - Completa setmanal.
- Històric
  - Retenció mínima d’1 mes → còpies setmanals/mensuals arxivades.
## Mitjans i Ubicació (Regla 3-2-1)
- Mitjans que recomanaria: 
  - NAS local per a còpies ràpides i restauració immediata.
  - Cloud per a còpia externa.
  - Discos externs per a còpies setmanals/mensuals arxivades.
- Regla 3-2-1:
  - 3 còpies de les dades (original + 2 còpies).
  - 2 tipus de mitjà diferents (NAS + Cloud).
  - 1 còpia fora de l’empresa (al núvol o en un centre extern).

> Important: La còpia més recent ha d’estar en local (NAS) per a restauració ràpida, amb rèplica al Cloud per protegir contra desastres físics.

# c) FASE 1 BLAI
## QUE COPIAREM?
Les dades més importants del servidor són aquelles les quals l’empresa no podria funcionar o seria molt difícil recuperar-les. Per exemple, són importants les bases de dades com els registres de clients o factures, els fitxers compartits com documents i projectes, la configuració del servidor com els comptes d’usuari i permisos, les màquines virtuals si n’hi ha, i els logs importants que ajuden a recuperar informació si passa alguna cosa.
No cal fer còpia de tots els 10 ordinadors dels usuaris si totes les seves dades ja estan guardades al servidor. Només convé fer còpia dels ordinadors que tinguin fitxers importants que no s’envien al servidor o configuracions difícils de repetir.

## CADA QUAN I DE QUINA MANERA?
Per assegurar que no es perdi informació important, és bo fer còpies de seguretat de manera regular. Una manera fàcil de fer-ho és així:
Cada dia laborable (de dilluns a divendres): fer una còpia incremental, que només guarda els canvis que s’han fet des de l’última còpia. Això és ràpid i no ocupa gaire espai.

Un dia a la setmana per exemple dissabte: fer una còpia diferencial, que guarda tots els canvis des de l’última còpia completa. Això serveix com a punt de seguretat més gran abans de la següent còpia completa.

Una vegada al mes: fer una còpia completa, que copia totes les dades crítiques del servidor. Així, si passa algun desastre, es podrà recuperar tot de cop.

## QUIN MITJA USAR I ON GUARDAR LES DADES
Per fer còpies de seguretat, es poden utilitzar diferents tipus de mitjans segons el que sigui més còmode i segur: discs durs externs, que són ràpids i fàcils d’utilitzar; un NAS un disc dur connectat a la xarxa, que permet tenir totes les còpies centralitzades i accessibles; Cloud, que és com un disc dur a Internet i serveix per tenir una còpia fora de l’empresa; i, si cal, cintes, que van bé per guardar moltes dades durant molt de temps.
Seguint la regla 3-2-1, sempre s’hauria de tenir almenys tres còpies de les dades: l’original al servidor, una còpia en un mitjà diferent com el NAS o un disc extern, i almenys una còpia fora del lloc, per exemple al Cloud. Això assegura que, si passa alguna cosa dolenta com un accident, robatori o fallada del servidor, les dades sempre es poden recuperar.


# d) FASE 1 PAU
Informe de còpies de seguretat
## QUE COPIAREM?
Les dades més crítiques del servidor inclouen els documents de projectes, la base de dades de Comptabilitat i Clients i les carpetes personals dels usuaris. No és necessari fer còpia de tots els 10 equips clients, només de les carpetes on els tècnics guarden fitxers importants temporalment.

## CADA QUAN I DE QUINA MANERA?
Pel tipus de còpia, es fara una còpia diària incremental per a les dades de Comptabilitat i Clients, còpia setmanal completa de tot el servidor, còpia diària diferencial de la documentació i les carpetes personals, i còpia mensual completa de totes les dades per complir amb la retenció mínima d’un mes.

## MITJANS I UBICACIÓ
El mitjà de còpia escollit és un NAS per a còpies ràpides i centralitzades, amb la còpia més recent guardada a l’oficina. A més, es manté una còpia addicional al Cloud per garantir recuperació fora del lloc en cas d’incident greu.
