# Work. Apunts Wifi
## Captures wireshark
[Wap Protocol Family] (https://wiki.wireshark.org/SampleCaptures#wap-protocol-family)
[Wifi - Wireless LAN captures - 802.11] (https://wiki.wireshark.org/SampleCaptures#wifi--wireless-lan-captures--80211)

## Wifi - conceptes generals
* SSID
* Estació
* Punt d'accés: Fa de pont entre la xarxa wireless i la cablejada
* Sistema de disitribució: Possibilita la mobilitat entre APs.
* Conjunt de serveis Bàsic (BSS) - Grup d'estacions que s'intercomuniquen entre elles. Es defineixen dos tipus:
    1. Independents: comunicació directa entre elles
    2. Infraestructura: Per mitjà d'un punt d'accés concret

* Conjunt de servei Estés (ESS) - És la unió de diversos BSS
* Canal


## Paràmetres físics - capa 1 (OSI)
### Bandes de freqüència: 2.4GHz, 5GHz i 6GHz
#### Canals wifi i interferències
### dB. Atenuació i obstacles físics
### Estudi de cobertura
[Estudi de cobertura wifi - pàg 49] (https://openaccess.uoc.edu/bitstream/10609/118426/7/inavidadTFM0620memoria.pdf)

A S-08 tenim els nivells de senyal depenent dels rangs de dBm

 Càlcul de la ubicació òptima dels punts d'accés.


## Estandars wifi a la capa 2 (OSI)

### WiFi 4, 5, 6, 6E i 7
[Relació amb estandars 802.11] (https://www.wi-fi.org/certification/programs)
[Relació 2] (https://www.wi-fi.org/discover-wi-fi)
### Normatives IEEE 802.11
#### Evolució
802.11a(1999) > 802.11b(1999) > 802.11g(2003) > 802.11h(2003) > 802.11i(2004) > 802.11n(2004) > 802.11ac(2014) > 802.11ax(2020)

b: 11Mbps; g: reuneix a i b i és compatible amb b, tot i que amb equips b és molt més lenta. 54Mbps en tota la cel·la si tenim dispositius b; h: obrim la banda dels 5GHz; i: WPA2; n: 650Mbps; ac: 1.3Gbps. Fa ús de 3 antenes; ax: 6GHz

#### 802.11 Wifi MAC header vs 802.3 Ethernet MAC header
> S-08 Novembre 27 2022
* 802.11n - Actualment és la que més representa l'estandar WIFI
    * Treballa amb els dos aspectres de freqüància (2.4GHz i 5GHz)
    * Velocitats de dades de fins 600 mbps

### Tecnologies emergents: MU-MIMO, Beamforming, OFDMA

## Configuració d'un punt d'accés. Modes
Val qualsevol punt d'accés per configurar-lo en els diferents modes?

### Configuració Bàsica
* SSID
* Contrasenya 
* Canal

### Xarxes convidades
### Hotspot
### Infraestructura wifi centralitzada
Apunts: si tenim diversos AP a la xarxa per oferir una millor cobertura, han d'actuar a diferents canals (AP adjacents, a 5 canals de diferència); Si AP com a repetidor > ha d'anar en el mateix canal; AP en mode Bridge: per a unir dues xarxes LAN separades que no es poden unir per cable.

## Seguretat
[Auditoria wifi amb hashcat i Kali Linux] (https://youtu.be/paS0w6wQP_g?si=NYSnnvrSQErIo78z)
[Sistemes de seguretat wifi. Deiferències entre les diferents versions de WPA] (https://latam.kaspersky.com/resource-center/definitions/wep-vs-wpa)

WPAx, Protocol EAPOL

### Atac de desautenticació
[How to crack wpa2 wifi password with Aircrack-ng] (https://youtu.be/4rnrfbb1-Wg?si=O6rIr9yY4JBVEFSB)
[Manual d'aircrack-ng] (https://www.aircrack-ng.org/doku.php?id=cracking_wpa)

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
3. Estudi de la senyal wifi que ens pugui arribar.
4. Estudi cobertura wifi amb packet tracer: Podem escalar el mapa físic d'una xarxa i estudiar la cobertura.
