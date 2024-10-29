###### tags: `xarxes`

# Protocols de capa 3

## IPV4
### Com s’estructura una capçalera ipv4
El tamany d’una capçalera ipv4 pot variar entre *32\*5=160 bits=20 bytes* o octets i *32\*15=480 bits=60 bytes* o octets.

Els camps de la capçalera ipv4 van en blocs (o registres) de 32 bits i el mínim són **5 blocs (i el màxim, 15 blocs)**. La resta de blocs fins a 15 que es poden afegir són camps opcionals i el camp *padding*.

![](https://hackmd.io/_uploads/HJi6YRVzp.png)

#### version
sempre és 4, que és la versió ip. **Té un tamany de 4 bits.**. Aquest camp es manté a ipv6.

#### IHL (Internet header length)
Com que la capçalera ipv4 pot variar en tamany, la mateixa té un camp que indica quin tamany que té en quant a blocs o paraules de 32 bits. És el camp IHL (Internet Header Length). **Té un tamany de 4 bits.** Desapareix a ipv6.

#### Type of service
Permet indicar el tipus de servei que es vol des del dispositiu que emet el paquet i, per tant, quina prioritat/retard/rendiment/confiabilitat ha de tenir. 

El camp conté (d’esquerra a dreta) un camp de preferència (3-bit); tres indicadors, D[elay bit], T[hroughput bit] i R[eliability bit]; i 2 bits no utilitzats. El camp de precedència és una prioritat, de 0 (normal) a 7 (paquet de control de la xarxa). Els tres bits indicadors permeten al host especificar el que li interessa més del grup {retardo, rendimiento, confiabilidad}. **Té un tamany de 8 bits.**. Es renombra com a *Traffic class* a ipv6.

Si un dels tres bit que hi han entre el 4 i el sisè té per valor 1:

* **Delay bit**. Interessa que el paquet tingui el mínim retràs.
* **Throughput bit**. Interessa que sempre que es pugui se li doni més ample de banda.
* **Reliability bit**. Interessa la confiabilitat, que arribi bé el paquet, abans que la rapidesa.

#### Total Length
Tamany total del datagrama ip (capçalera i dades). **Té un tamany de 16 bits.** A ipv6 es renombra a *payload length*, tot i que a ipv6 es refereix únicament al tamany de les dades, no inclou la capçalera ipv6.

#### Identification
És l’identificador del datagrama al qual pertany aquest datagrama (un datagrama pot fragmentar-se en més datagrames en el seu viatge per les xarxes). **Té un tamany de 16 bits.** Desapareix a ipv6.

#### Flags
**Són tres bits** que indiquen opcions sobre la fragmentació del datagrama. El primer bit no es fa servir; el segon bit a 1 indica que el datagrama no es pot fragmentar; el tercer bit indica si el paquet és l’últim fragment d’una sèrie de paquets fragmentats. Desapareix a ipv6.

#### Fragmentation offset
Cada xarxa d'àrea local té un MTU (Maximum Transmission Units), que indica la mida màxima que pot tenir un paquet que passa per aquell xarxa. Per tant, si el datagrama en qüestió supera aquest MTU, s’ha de fragmentar. El camp Fragmentation offset indica en quina posició del datagrama original estava l’inici de les dades del datagrama actual. **Té un tamany de 16 bits.** Desapareix a ipv6.

#### Time to live
https://packetpushers.net/ip-time-to-live-and-hop-limit-basics/ 
Indica el nombre màxim de salts que pot efectuar un datagrama a nivell de capa d’internet. O sigui, el nombre màxim de routers pels quals ha de passar. Cada vegada que el datagrama passa per un router, aquest valor disminueix en 1. Si arriba un datagrama a un router amb un TTL a 1 o a 0, aquest és descartat i destruit. A ipv6 es renombra a *Hop Limit length*.

#### Protocol 
8 bits. indica quin protocol de capa superior ha generat el paquet.

#### Suma de verificació d’encapçalament (header checksum)
16 bits de control perquè no hi hagi errors a l’encapçalament per a ajudar a garantir la seva integritat.

#### Adreça d’origen (source address) (32 bits)
especifica l’adreça ip de la màquina que ha generat el paquet.

#### Adreça de destinació (destination address) (32 bits)
especifica l’adreça ip de la màquina a la qual es volen enviar les dades.

#### Opcions (options and padding) (longitud variable)
Permet que Ip suporti varies opcions, com la seguretat

#### Farciment (longitud variable)
Afegeix zeros perquè l’encapçalament sigui múltiple de 32 bits.

## IPV6

### Com s’estructura una capçalera ipv6

| ipv4 header | ipv6 header | 
| -------- | -------- | 
|![](https://hackmd.io/_uploads/HkYpGlSza.png)     | ![](https://hackmd.io/_uploads/rylgXlBGT.png)|

Aquesta capçalera no varia en quant a tamany. Sempre és igual. Per tant, ja no cal que contingui el camp *IHL* que sí feia falta a *ipv4*.

#### Camp version
sempre és 6, que és la versió ip.

> Version: A 4-bit field, the same as in IPv4. It contains the number 6 instead of the number 4 for IPv4.

#### Traffic class
És equivalent al camp *ipv4* *Type of Service*.

> An 8-bit field similar to the type of service (ToS) field in IPv4. It tags the packet with a traffic class that it uses in differentiated services (DiffServ). These functionalities are the same for IPv6 and IPv4.

#### Flow Label
Nou camp a *ipv6*. Per etiquetar paquets:

> A completely new 20-bit field. It tags a flow for the IP packets. It can be used for multilayer switching techniques and faster packet-switching performance.

#### Payload Length
> Similar to the Total Length field of IPv4.

#### Next Header
> The value of this field determines the type of information that follows the basic IPv6 header. It can be a transport-layer packet, such as TCP or UDP, or it can be an extension header. The next header field is similar to the Protocol field of IPv4.

#### Hop Limit
>This field specifies the maximum number of hops that an IP packet can traverse. Each hop or router decreases this field by one (similar to the Time to Live [TTL] field in IPv4). Because there is no checksum in the IPv6 header, the router can decrease the field without recomputing the checksum. On IPv4 routers the recomputation costs processing time.

#### Source Address and Destination Address
> Source address: This field has 16 octets or 128 bits. It identifies the source of the packet.
Destination Address: This field has 16 octets or 128 bits. It identifies the destination of the packet.

#### Canvis respecte capçalera ipv4

* Fragmentation fields moved out of base header
* IP options moved out of base header
* Header Checksum eliminated
* Header Length field eliminated
* Revised
    * Time to Live → Hop Limit
    * Protocol → Next Header
    * Precedence and TOS → Traffic Class
    * Addresses increased 32 bits → 128 bits
* Extended
    * Flow Label field added

> The IPv6 header has 40 octets in contrast to the 20 octets in IPv4. IPv6 has a smaller number of fields, and the header is 64-bit aligned to enable fast processing by current processors. Address fields are four times larger than in IPv4.

### Característiques de ipv6
* Espai més llarg d'adreçament
* Agregació de prefixes
* Autoconfiguració
* No necessitat de NAT
* Capçalera més simple
* No hi han adreces *broadcast*
* No checksums
* IPSec nadiu per a ipv6
* Tipus d'adreces 
    * *unicast, multicast, anycast*
    * *Unicast*: *Global, Link local, Site local*

### Representació d'adreces ipv6. Regles de simplificació

### Unicast
#### Parts d'una adreça de host (Unicast)
Una ipv6 té dues parts:
* prefix de xarxa (64-bit): representa la xarxa a la que el dispositiu està connectat.
* Identificador local (64-bit): Identifica el host a la xarxa local. En el cas d'*Ethernet*, l'adreça de host deriva de l'adreça MAC.

![](https://hackmd.io/_uploads/Sy5QJWSMp.png)

#### Unicast. Autoconfiguració
Encara que existeix DHCPv6, no és necessari. És suficient amb que l'encaminador de la xarxa anuncïi el seu prefix (64-bit).

El sufix de xarxa es genera a partir de la MAC, com hem vist abans, però el 7è i el 8è bit canvien als següents valors:

**Universal/Local (U/L):** el bit situado junto al bit de orden inferior en el primer byte se utiliza para indicar si la dirección se administra universal o localmente. 
* Si el bit U/L té el valor 0, vol dir que és una adreça Local Scope.
* Si el bit U/L té el valor 1, vol dir que és global.

El bit U/L bit se designa mediante u en la figura de abajo.

**Individual/Group (I/G) (Individual/Grupo):** el bit de orden inferior del primer byte se utiliza para indicar si se trata de un dirección individual (de unidifusión) o de grupo (de multidifusión). 
* Cuando está establecido en el valor 0, la dirección es de unidifusión.
* Cuando está establecido en el valor 1, la dirección es de multidifusión. 

El bit I/G se designa mediante g en la figura de abajo.

![](https://hackmd.io/_uploads/H16l4bHMp.gif)

Exemple de modificació de la MAC en una adreça global unicast:

![](https://hackmd.io/_uploads/SJGQU-BG6.png)

#### Unicast Global
Són les que fa servir una màquina per connectar-se a internet (Sense necessitat de NAT). En binari, comencen per `001` o en hexadecimal, per `2` o `3`.

El prefix de xarxa s'obté de l'encaminador de la seva xarxa.

#### Unicast Link Local
Són privades però només fan les funcions de descubriment del vehí. En binari comencen per `1111 1110 10` o en hexadecimal per `FE8`

#### Unicast site local
Són com les privades a ipv4. En binari comencen per `1111 1110 11` o en hexadecimal per `FEC`.

### Multicast
Comencen amb `FF`. Representen grup de màquines. Poden servir per:
* Protocol de descubriment de vehí (substitueix ARP)
* Per demanar prefix de xarxa a un grup d'encaminadors.

## Protocols d'encaminament

### OSPF