# T10: Servidor impressió Linux. CUPS (tasca individual)

En aquesta practica haurem de tenir dues VM, Ubuntu Server, Zorin Client, les dues amb una segona interfície Host-only. Per començar es dues màguines hauram d'estar actualitzades.
```bash
sudo apt update -y
sudo apt upgrade -y
```
Ara haurem de instal·lar els paquets necessàris per tenir una impressora virtual.

```bash
sudo apt install cups-pdf
```
![capt](img/1.png)

Per accedir a la configuració haurem d'iniciar sessió web des d'un client i accedir per el port 631, pero si ho fem donarà error de conexió, per solucionar-ho cal editar l'arxiu `/etc/cups/cupsd.conf`, però com sempre primer farem un còpia de seguretat de l'arxiu.
```bash
sudo cp /etc/cups/cupsd.conf /etc/cups/cupsd_copy.cong
sudo nano /etc/cups/cupsd.conf
```
![capt](img/2.png)

Ara reiniciem el servei i comprovem el seu correcta funcionament.
```bash
sudo systemctl restart cups
sudo systemctl status cups
```
![capt](img/3.png)

Ara si que podrem accedir i iniciar sessió des d'un client a la web.

https://IP:631

El següent pas sera afegir una impressora virtual, per fer-ho anem a la pestanya **Administració**

Si ens demana iniciar sessió introduïm les credencials del nostre usuari.

![capt](img/4.png)

Seguidament fem clic a **Add printer**

![capt](img/5.png)

Ens aparèixera un error de no tenir **permisos**, per solucionar-ho hem d'afegir el nostre usuari al grup **lpadmin**.

![capt](img/6.png)

```bash
sudo usermod -a -G lpadmin usuari
id usuari
```

![capt](img/7.png)

Ara ja podrem afegir una impressora, fem clic a **Add printer** i seleccionem la configuració de l'impressora.

Local Printers: CUPS-PDF (Virtual PDF Printer)

![capt](img/8.png)

Nombre: (El podem cambiar si desitjem)
Descripción: (La podem cambiar si desitjem)
Ubicación: Server
Compartición: Activada  <-- **IMPORTANT**

![capt](img/9.png)

Marca/Make: Generic
Model: Generic CUPS-PDF Printer (no options) (en)
Fem click a **Add printer**

![capt](img/10.png) ![capt](img/11.png)

Ara afegirem l'impressora recent creada al client, anirem a **Settings** --> **Printers** --> **Add printer**

Seleccionem i afegim la nostre impressora

![capt](img/12.png)

Ara enviem diversos treballs d'impressió des del client i observem com apareixen a la cua.

![capt](img/13.png)

També podem veure al servidors els documents PDF que s'han generat amb les peticions.
```bash
tree
```

![capt](img/14.png)

