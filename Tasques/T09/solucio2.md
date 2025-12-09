# Projecte04: Servidor NFS

## El Cas Client: DevOptimize Solutions

Per al client `DevOptimize Solutions` s'ha dissenyat i implementat un servidor de fitxers centralitzat basat en **NFS (Network File System)** per millorar el control de versions i l'eficiència. La solució s'ha demostrat utilitzant un Servidor (Ubuntu Server 24.04 LTS) i un Client (Zorin OS 18), atenent a la seva demanda inicial de treballar sense autenticació centralitzada.

---

## Fase 1: Preparació de l'entorn

Es defineixen les següents adreces IP per a la xarxa Host-Only:

| Equip | Rol | IP Host-Only |
| :--- | :--- | :--- |
| **Servidor** | Ubuntu Server 24.04 LTS | `10.0.2.6` |
| **Client** | Zorin OS 18 | `10.0.2.15` (Assumida) |

### 1. Actualització i Connectivitat

S'actualitzen ambdues màquines:

```bash
sudo apt update -y && sudo apt upgrade -y
```

Es comprova la connectivitat:

```bash
ping 10.0.2.15 # Des del servidor al client
```

[Capt](img/1.png)

```bash
ping 10.0.2.6 # Des del client al servidor
```
[Capt](img/2.png)

---

## Fase 2: Preparació del servidor

### 1. Creació de Grups i Usuaris (Servidor i Client)

**Al Servidor:** Creació de grups i usuaris.
```bash
sudo groupadd devs
```
```bash
sudo groupadd admins
```
[Capt](img/3.png)

Creació d'usuaris:
```bash
sudo useradd -m dev01 -G devs
sudo passwd dev01
sudo useradd -m admin01 -G admins
sudo passwd admin01
```
[Capt](img/4.png)
[Capt](img/5.png)

**Replicació d'UID/GID:** Es comproven els identificadors del Servidor i es repliquen al Client per assegurar la coherència dels permisos d'NFS.

Verificació al Client:
```bash
id dev01 && id admin01
```
[Capt](img/22.png)

### 2. Creació de Directoris i Permisos (Servidor)

Creació dels directoris base:
```bash
sudo mkdir -p /srv/nfs/dev_projectes
sudo mkdir -p /srv/nfs/admin_tools
```
[Capt](img/6.png)

Aplicació dels permisos clau (Propietari: **`root`**, Grup: control total (`770`)):
```bash
sudo chown root:devs /srv/nfs/dev_projectes/
sudo chmod 770 /srv/nfs/dev_projectes/

sudo chown root:admins /srv/nfs/admin_tools/
sudo chmod 770 /srv/nfs/admin_tools/
```
Comprovació dels permisos:
```bash
ls -la /srv/nfs/
```
[Capt](img/7.png)

### 3. Instal·lació d'NFS (Servidor i Client)

Al **Servidor**:
```bash
sudo apt install nfs-kernel-server -y
```
[Capt](img/8.png)
```bash
sudo systemctl enable --now nfs-server
```
[Capt](img/9.png)

Al **Client**:
```bash
sudo apt install nfs-common -y
```

---

## Fase 3: L'Exportació d'Administració (El Dilema del root\_squash)

El client requereix que l'usuari `root` del client pugui instal·lar eines al directori d'administració.

### Prova 1 (L'Error) i Justificació de la Correcció

Amb la configuració per defecte, l'exportació d'NFS aplica **`root_squash`**.

Quan el **`root_squash`** està actiu, el Servidor impedeix que l'usuari `root` del client tingui privilegis complets, *mapant* (squashing) el seu accés al compte sense privilegis **`nobody`**. Això impedeix que l'administrador remot pugui realitzar les seves tasques de `root`, cosa que obliga a deshabilitar aquesta seguretat per al cas d'ús.

### Prova 2 (La Solució: `no_root_squash`)

Per complir el requisit del client, deshabilitarem la mesura de seguretat.

**Al Servidor:** Editem `/etc/exports` afegint **`no_root_squash`**.
```bash
sudo nano /etc/exports
```
Contigut afegit:
```
/srv/nfs/admin_tools 10.0.2.0/24(rw,sync,no_root_squash)
```
[Captura de pantalla de l'entrada de `/etc/exports` per a `admin_tools` amb `no_root_squash` (similar a img/16.2.png)]

Apliquem els canvis:
```bash
sudo exportfs -a
```

**Al Client:** Muntem el recurs i provem de crear un fitxer com a `root`.
```bash
sudo umount /mnt/admin_tools 
sudo mkdir -p /mnt/admin_tools
sudo mount 10.0.2.6:/srv/nfs/admin_tools /mnt/admin_tools/
sudo touch /mnt/admin_tools/root_file_test_2
ls -l /mnt/admin_tools/
```

**Verificació:**

El propietari del fitxer serà **`root`**. Això confirma que l'opció **`no_root_squash`** funciona, permetent al `root` del client actuar com a `root` del servidor.

---

## Fase 4: L'Exportació de Desenvolupament (Permisos rw vs ro)

El directori de projectes s'exporta amb doble regla: `rw` per a la xarxa, `ro` per a l'IP de consultors (`10.0.2.100`).

### 1. Configuració d'Exportació (Servidor)

Afegim la doble regla a `/etc/exports`:
```bash
# /etc/exports al Servidor (10.0.2.6)
/srv/nfs/dev_projectes 10.0.2.0/24(rw,sync) 10.0.2.100(ro,sync)
```
[Captura de pantalla amb les dues línies d'exportació a `/etc/exports` (img/40.png)]
Recarreguem:
```bash
sudo exportfs -a
```

### 2. Prova d'Escriptura (IP `10.0.2.15` - Permís `rw`)

**Al Client:** Muntem el recurs:
```bash
sudo mkdir -p /mnt/dev_projectes
sudo mount 10.0.2.6:/srv/nfs/dev_projectes /mnt/dev_projectes
```
Com a usuari `dev01` (membre del grup `devs` amb permisos locals):
```bash
su - dev01
touch /mnt/dev_projectes/prova_dev_rw.txt
ls -l /mnt/dev_projectes/
```
[Captura de pantalla on `dev01` crea el fitxer exitosament (img/50.png)]

**Resultat:** **EXITÓS**. L'IP permet **`rw`** d'NFS i l'usuari té permisos locals (`770`).

### 3. Prova de Només Lectura (IP `10.0.2.100` - Permís `ro`)

**Al Client:** Desmuntem, canviem la IP a `10.0.2.100` i tornem a muntar.
Com a usuari `dev01`:
```bash
sudo umount /mnt/dev_projectes
# ...Canvi d'IP a 10.0.2.100...
sudo mount 10.0.2.6:/srv/nfs/dev_projectes /mnt/dev_projectes
su - dev01
touch /mnt/dev_projectes/prova_dev_ro.txt
```
**Resultat:** **Permís denegat**.
**Justificació:** La directiva **`ro`** aplicada per NFS a l'IP `10.0.2.100` preval sobre els permisos locals de l'usuari `dev01`.

### 4. Prova de Permisos de Grup (Tornem a `10.0.2.15` amb `rw`)

**Al Client:** Tornem a la IP `10.0.2.15`.
Com a usuari `admin01` (membre d'un altre grup):
```bash
exit # Sortim de dev01
su - admin01
touch /mnt/dev_projectes/prova_admin.txt
```
**Resultat:** **Permís denegat**.
**Justificació:** Tot i tenir permís **`rw`** d'NFS (nivell de xarxa), l'usuari `admin01` no pertany al grup `devs`. Com que els permisos locals del directori són **`770`**, **`admin01` no té accés a nivell del sistema de fitxers (chmod).**

---

## Fase 5: Muntatge Automàtic amb /etc/fstab

Configurem el muntatge automàtic al client.

**Al Client:**
```bash
sudo nano /etc/fstab
```
Afegim les línies:
```
# Servidor NFS       Punt de Muntatge   Tipus   Opcions                           fs_freq fs_passno
10.0.2.6:/srv/nfs/admin_tools /mnt/admin_tools nfs defaults,timeo=900,retrans=5 0 0
10.0.2.6:/srv/nfs/dev_projectes /mnt/dev_projectes nfs defaults,timeo=900,retrans=5 0 0
```
[Capt](img/21.png)

### 1. Prova sense Reinici
```bash
sudo mount -a
```
[Capt](img/19.png) (Mostra el muntatge a `/mnt/admin_tools`)

### 2. Prova amb Reinici

Es reinicia el Client i es verifica que els recursos s'han muntat correctament.
[Capt](img/20.png) (Mostra la verificació amb `ls` o GUI)

---

## Conclusió i Recomanacions

La prova de concepte ha confirmat que la solució NFSv3 pot satisfer els requisits de control d'accés del client. No obstant això, es presenten limitacions significatives en termes de seguretat i escalabilitat:

1.  **Implementació d'Autenticació Centralitzada (LDAP/FreeIPA):**
    La replicació manual d'UID/GID és un punt de fallada. Es recomana implementar **LDAP o FreeIPA**. Això garantiria que els usuaris tinguin l'**UID/GID idèntic en totes les màquines** automàticament, eliminant els problemes de permisos d'NFS.

2.  **Migració a NFSv4 amb Kerberos:**
    L'NFSv3 és insegur, ja que només confia en l'adreça IP i l'UID numèric. Es recomana migrar a **NFSv4 amb Kerberos**. Kerberos proporciona una **autenticació criptogràfica forta** (GSSAPI), verificant la identitat real de l'usuari i la integritat de les dades, fent innecessària l'opció de risc **`no_root_squash`**.

3.  **Adopció d'un Sistema de Control de Versions (GIT):**
    Per evitar errors de versions i pèrdua d'eficiència, **s'ha d'adoptar i fer obligatori l'ús de GIT** per al codi font. L'NFS s'ha de relegar a l'emmagatzematge d'actius compartits o dades de configuració, i no a l'edició directa de codi.
