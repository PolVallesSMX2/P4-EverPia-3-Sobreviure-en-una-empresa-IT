# T09: Servidor fitxers Linux. NFS (tasca individual)
## Fase 1: Configuració del entorn
Haurem de tenir dues VM un **Client** i un **Servidor**, hauran de tenir dos adaptadors de xarxa. Un en xarxa nat i l'altre en host-only.

Actualitzarem les dues màquines
```bash
sudo apt update -y && sudo apt upgrade -y
```
Seguidament instal·larem el servei NFS
```bash
sudo apt install nfs-kernel-server
```
![Capt](img/0.png)

Comprobarem que les dues màquines es veuen entre si amb un ping.
```bash
ping IP_CLIENT
```
![Capt](img/1.png)

![Capt](img/2.png)

```bash
ping IP_SERVIDOR
```
## Fase 2: Preparació del Servidor
Crearem dos grups **devs** i **admins**.
```bash
sudo groupadd devs
```
```bash
sudo groupadd admins
```
![Capt](img/3.png)

Crearem dos usuaris
- dev01 membre de devs
- admin01 membre de admins

