# Work. Apunts Wifi
## Captures wireshark
[Wap Protocol Family](https://wiki.wireshark.org/SampleCaptures#wap-protocol-family)

[Wifi - Wireless LAN captures - 802.11](https://wiki.wireshark.org/SampleCaptures#wifi--wireless-lan-captures--80211)

## Wifi - conceptes generals

La tecnologia wifi és una tecnologia per a la connexió de dispositius sense fil. A nivell físic fa servir les ones electromagnètiques com a mitjà de transmissió i actua en la capa 1 del model TCP/IP a partir dels estàndars IEEE 802.11, els quals permeten la creació de xarxes WLAN fent ús de freqüències de ràdio.

**Conceptes associats a la Wifi**

* SSID - Service set identifier. És el nom que se li assigna a una xarxa wifi que s'anuncia als dispositius inalàmbrics que hi han al voltant.

* Estació - Dispositiu inalàmbric.

* Punt d'accés: Fa de pont entre la xarxa wireless i la cablejada i possibilita l'accés a la xarxa dels dispositus inalàmbrics.

## Paràmetres físics relacionats amb la tecnologia wifi

### Banda de freqüència

* Banda de freqüència - és el rang de freqüència en el que actuen les ones wifi en una mateixa xarxa. A major freqüència, major velocitat de dades però menor abast. A Wifi trobem les següents bandes:

    * 2.4 GHz
    * 5 GHz
    * 6 GHz

* Canal - Les xarxes wifi que actuen en una mateixa banda, han de compartir aquest rang de freqüència, per la qual cosa es divideix la banda en una sèrie de canals i xarxes wifi que actuen molt a prop han d'emetre en canals diferents per a evitar interferències. Canals a 2.4 GHz:

![Canals a 2.4 GHz](canals_24ghz.png)

[Wikipedia. Canals wifi](https://en.wikipedia.org/wiki/List_of_WLAN_channels)

### Estudi de cobertura
[Estudi de cobertura wifi - pàg 49](https://openaccess.uoc.edu/bitstream/10609/118426/7/inavidadTFM0620memoria.pdf)

Bàsicament, la cobertura wifi és l'àrea on arriba la senyal d'una xarxa wifi. Quins factors determinen la cobertura? Alguns poden ser la banda de freqüència en la que actua, el canal, els obstacles físics, i l'atenuació o la força de la senyal.

* Força de la senyal: mesurat en decibel·lis (dBM). A major senyal, millor rendiment.
* Obstacles físics: Els obstacles físics poden disminuir la força de la senyal (parets, sostres, terra, mobles, etc).
* Interferències, per exemple, amb altres xarxes wifi. En aquest punt és important l'el·lecció del canal.
* Col·locació dels punts d'accés: Llocs centrals, lliures d'obstacles (situar el PA en llocs elevats)

![Qualitat de la senyal depenent dels dBm](cobertura_wifi.jpeg)

#### Eines de mapes de calor

NetSpot, Ekahau HeatMapper, Wifi Analyzer (Android), Acrylic Wi-fi Home

## Estandars wifi
[Relació amb estandars 802.11](https://www.wi-fi.org/certification/programs)

1. 802.11a (1999)
2. 802.11b (1999) - 11 Mbps
3. 802.11g (2003) - 54 Mbps
4. 802.11h (2003) - Banda dels 5GHz
5. 802.11i (2004) - WPA2
6. 802.11n (2004) - 650 Mbps
7. 802.11ac (2014) - 1.3Gbps. 3 antenes. Possibilitat de MU-MIMO.
8. 802.11ax (2020) - Banda dels 5GHz. Possibilitat de MU-MIMO.

![Correspondència versió wifi IEEE](estandars_wifi.png)

### 802.11 Wifi MAC header vs 802.3 Ethernet MAC header

![Capçaleres wifi vs Ethernet](wifi_ethernet_headers.png)

## Tecnologies emergents: MU-MIMO, Beamforming

### MU-MIMO

*Multi-User, Multiple Input, Multiple Output*. És una tecnologia avançada en xarxes Wi-Fi que permet a un punt d'accés (AP) comunicar-se amb diversos dispositius de manera simultània, millorant la capacitat, eficiència i rendiment de la xarxa. 

Utilitza múltiples antenes per enviar i rebre diverses transmissions de dades alhora de dos o més dispositius.

**MIMO** permet l'enviament i recepció de dades simultànies, però del mateix dispositiu.

### Beamforming

Permet enfocar la senyal (tradicionalment omnidireccional a wifi) cap els dispositius destinataris i guanyar en abast i qualitat de la senyal.

## Arquitectura wifi

### Xarxa wifi en mode infraestructura 
Hi ha un punt d'accés wifi que actúa com a intermediari per la comunicació entre els dispositius de la xarxa.

### Xarxa wifi en mode ad-hoc
No hi ha cap punt d'accés que centralitza la comunicació. els dispositius es connecten directament.

### Repetidor wifi
Es connecta al punt d'accés principal. No té per què emetre la senyal a la mateixa banda que el punt d'accés principal.

### Sistemes de wifi de xarxa 
#### Wireless distribution system (WDS)
Hi han dos modes: 
1. Un punt d'accés central i la resta són repetidors.
2. Dues xarxes wifi unides per un punt d'accés que fa de pont.

#### En malla
Els diferents punts d'accés es connecten entre ells formant una xarxa en malla. Cada punt d'accés es connecta en cada moment amb el punt d'accés que li vingui millor (segons l'estat de la resta). 

**Desaventatge**: Configuració. cal configurar encaminament estàtic o dinàmic (OSPF) en els diferents PA per a poder-se connectar entre ells.

### PLC
a través de la xarxa elèctrica.

### Hotspot
Un hotspot és una ubicació física on es proporciona accés a Internet de manera inalàmbrica a través de Wi-Fi. 

### Xarxes convidades
Una xarxa convidada és una xarxa Wi-Fi separada i aïllada de la xarxa principal, creada perquè els visitants o usuaris externs es connectin a Internet sense accedir a recursos privats o sensibles de la xarxa principal. Així, és una mesura de seguretat per evitar que els dispositius dels convidats comprometin la xarxa interna.

## Seguretat
[Auditoria wifi amb hashcat i Kali Linux](https://youtu.be/paS0w6wQP_g?si=NYSnnvrSQErIo78z)
[Sistemes de seguretat wifi. Deiferències entre les diferents versions de WPA](https://latam.kaspersky.com/resource-center/definitions/wep-vs-wpa)

WPAx, Protocol EAPOL

### Atac de desautenticació
[How to crack wpa2 wifi password with Aircrack-ng](https://youtu.be/4rnrfbb1-Wg?si=O6rIr9yY4JBVEFSB)
[Manual d'aircrack-ng](https://www.aircrack-ng.org/doku.php?id=cracking_wpa)

1. Amb la nostra targeta wifi (iwconfig), escanegem les wifi que tenim en la nostra proximitat; 
2. Escollim la wifi i executem (airmon-ng, crec) per trobar equips connectats a la wifi; 
3. Apliquem atac de desautenticació, perquè el que volem és aconseguir desautenticar un dispositiu per poder capturar posteriorment paquets del handshake d'un nou intent d'autenticació. Aquest pas ens donarà la captura del handshake. La mirem des de wireshark per veure com són aquests paquets.

### Altres protocols de connexió i autenticació (WPS, EAP)

## Eines de diagnòstic
* Wireshark
* NetSpot

## Possibles pràctiques
1. Analitzar captures wifi amb wireshark
2. Analitzar captures wifi amb aircrack-ng
3. Estudi de la senyal wifi que ens pugui arribar generant un mapa de calor o alguna eina similar.
4. Estudi cobertura wifi amb packet tracer: Podem escalar el mapa físic d'una xarxa i estudiar la cobertura.
