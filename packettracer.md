# Apunts Packet tracer

## Instal·lació de Packet tracer a Ubuntu 24.04

A l'instal·lar el packet `.deb` de *netacad*:

```bash
$ sudo dpkg -i Baixades/CiscoPacketTracer822_amd64_signed.deb
```

Et dona el següent error de dependències:

```bash
 packettracer depèn de libgl1-mesa-glx; tot i així:
  El paquet libgl1-mesa-glx no està instal·lat.
 packettracer depèn de libxcb-xinerama0-dev; tot i així:
  El paquet libxcb-xinerama0-dev no està instal·lat.
```

Si els paquets que falten estan als repositoris d'Ubuntu, les dependències es poden resoldre amb la comanda `apt install -f`, però el tema és que un d'ells no hi és:

```bash
$ sudo apt install -f
S'està llegint la llista de paquets… Fet
S'està construint l'arbre de dependències… Fet
S'està llegint la informació de l'estat… Fet  
S'estan corregint les dependències… Fet
Se SUPRIMIRAN els paquets següents:
  packettracer
0 actualitzats, 0 nous a instal·lar, 1 a suprimir i 226 no actualitzats.
1 no instal·lats o suprimits completament.
Després d'aquesta operació s'utilitzaran 0 B d'espai en disc addicional.
Voleu continuar? [S/n] 
(S'està llegint la base de dades… hi ha 221331 fitxers i directoris instal·lats 
actualment.)
S'està desinstal·lant packettracer (8.2.2)…
gtk-update-icon-cache: No theme index file.
S'estan processant els activadors per a shared-mime-info (2.4-4)…
```

Intentem executar el Packet tracer perquè suposem que ja és instal·lat i ...

```bash
joan@super-ThinkBook-14-G4-IAP:~$ packettracer
packettracer: no s'ha trobat l'ordre
```

Què ha passat?

```
joan@super-ThinkBook-14-G4-IAP:~$ dpkg -l | grep ackett
rc  packettracer                                   8.2.2                                    amd64        Cisco PacketTracer 8.2.2 installation package
```

Que com que les dependències no s'han resolt, el paquet s'ha desinstal·lat. I és que el paquet `libgl1-mesa-glx` ja no es fa servir. La solució temporal que jo he adoptat és baixar el paquet del [lloc de paquets de Ubuntu](https://packages.ubuntu.com/jammy-updates/amd64/libgl1-mesa-glx/download) per Ubuntu 23.0.4 i instal·lar-lo:

```bash
$ sudo dpkg -i Baixades/libgl1-mesa-glx_23.0.4-0ubuntu1~22.04.1_amd64.deb
```

Després, he intentat resoldre l'altre dependència:

```bash
$ sudo apt search libxcb-xinerama0-dev
S'està ordenant… Fet
Cerca a tot el text… Fet
libxcb-xinerama0-dev/noble 1.15-1ubuntu2 amd64
  X C Binding, xinerama extension, development files
```
Perfecte. Aquest paquet sí hi és als repositoris:

```bash
$ sudo apt install libxcb-xinerama0-dev
S'està llegint la llista de paquets… Fet 
S'està construint l'arbre de dependències… Fet
S'està llegint la informació de l'estat… Fet  
Pot ser que vulgueu executar «apt --fix-broken install» per a corregir-ho.
Els següents paquets tenen dependències sense satisfer:
 libxcb-xinerama0-dev : Depèn: libxcb1-dev però no s'instal·larà
E: Dependències no satisfetes. Proveu amb «apt --fix-broken install» sense paquets (o especifiqueu una solució).
```

També té dependències, però aquestes les puc resoldre fàcilment seguint el suggeriment:

```bash
$ sudo apt --fix-broken install
```

Ara ja puc instal·lar packet tracer:

```
$ sudo dpkg -i Baixades/CiscoPacketTracer822_amd64_signed.deb 
(S'està llegint la base de dades… hi ha 221604 fitxers i directoris instal·lats actualment.)
S'està preparant per a desempaquetar …/CiscoPacketTracer822_amd64_signed.deb…
S'està desempaquetant packettracer (8.2.2) sobre (8.2.2)…
gtk-update-icon-cache: No theme index file.
S'està configurant packettracer (8.2.2)…
gtk-update-icon-cache: No theme index file.
S'estan processant els activadors per a shared-mime-info (2.4-4)…
```
