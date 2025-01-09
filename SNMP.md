###### tags: `xarxes` 

# SNMP

## Arquitectura

![imatge](https://hackmd.io/_uploads/Bksoru_VT.png)


Simple Network Management Protocol. És un protocol de capa d'aplicació. Consta de tres elements:

* L'administrador (NMS - Network Management System), que és el que obté informació dels clients.
* MIB (Management Information Base), que és la base de dades que enmagatzema la informació que obté l'administrador sobre els dispositius de xarxa. Resideix en cada agent. Cada agent té el seu propi MIB amb la informació local.
* Els agents, que són els que envien informació local cap al seu respectiu MIB.

>SNMP (Protocolo simple de administración de red) se desarrolló para permitir que los administradores puedan administrar los nodos, como los servidores, las estaciones de trabajo, los routers, los switches y los dispositivos de seguridad, en una red IP. Permite que los administradores de red administren el rendimiento de la red, detecten y resuelvan problemas de red, y planifiquen el crecimiento de la red.

## Tipus d'operacions
* *get*: Mitjançant un missatge de tipus *get*, l'administrador demana informació local a un agent.
* *set*: L'administrador modifica informació d'un dispositiu agent.
* *trap*: Els agents reenvien informació directament (sense un missatge *get* previ)

Es fa servir el port UDP 162 per aquest enviament d'informació. 

**Taula d'operacions de l'administrador i l'agent:**

| Operació | Descripció | 
| -------- | -------- | 
| *get-request*     | recupera el valor d'una variable concreta.     | 
| *get-next-request*     | recupera el següent valor dintre d'una taula. Aquí l'administrador no necessita conèixer el nom de la variable.     | 
| *get-bulk-request*     | recupera blocs de dades. Ens estalviem de fer diverses peticions *get*     | 
| *get-response*     | respon a una sol·licitud *get-request*, *get-next-request* o *get-bulk-request*     | 
| *set-request*     | enmagatzema el valor d'una variable específica i s'envia el nou valor a l'administrador     | 

## Traps
Els traps són missatges que envien els agents a l'administrador sense missatge *get* previ, automatitzats en base a una configuració prèvia des de l'administrador i que s'activen quan es compleix un event o una condició a la xarxa. Exemples:

* Autenticació incorrecta d'usuaris
* Els reinicis
* l'estat de l'enllaç (actiu o inactiu), 
* El seguiment d'adreces MAC
* El tancament d'una connexió TCP

Un dels aventatges és que no saturen el tràfic de xarxa amb missatges get i post de sondeig.

![](https://hackmd.io/_uploads/B1UaFkTza.png)

## Versions

> Existen varias versiones de SNMP, incluidas las siguientes:

    SNMPv1: el protocolo simple de administración de red, 
    un estándar de Internet completo, se define en RFC 1157.
    L'autenticació és mitjançant una cadena de comunitat.
    
    SNMPv2c: se define en las RFC 1901 a 1908; 
    utiliza el marco administrativo basado en cadenas de
    comunidad. Aquí podem definir més d'una cadena  
    i cadascuna pot tenir els seus permisos. S'afegeix
    la possibilitat d'obtenir blocs d'informació amb 
    una única petició *get* (get-bulk-request)
    
    SNMPv3: protocolo interoperable basado en estándares 
    definido originalmente en las RFC 2273 a 2275; 
    proporciona acceso seguro mediante la autenticación 
    y el cifrado de paquetes a través de la red.

![](https://hackmd.io/_uploads/HkGOcJ6Ma.png)

## Cadenes de comunitat
Per a que SNMP funcioni, l'administrador (NMS) ha de tenir accés als MIB. Per controlar aquest accés, SNMPv1 i SNMPv2c creen cadenes de comunitat (passwords de text no xifrat). Tipus de cadenes:

* Només lectura (ro)
* Lectura i escriptura (rw)

## Objectes de la base de dades MIB
Base de dades jeràrquica. Per cada variable (dada de la base de dades) es genera un OID.

## Passes per a configurar un SNMP
1. Configurem les cadenes de comunitat i els nivell d'accés.
```
snmp-server community <string_nom_cadena> ro|rw
```
2. Registrem la ubicació del dispositiu administrat i informació de contacte.
```
snmp-server location <string>
snmp-server contact <string>
```
3. Restringim l'accés a una cadena de comunitat a uns determinats  administradors amb una acl. Un cop definida la ACL, la podem cridar amb la comanda:
```
snmp-server community <string_nom_cadena> nom_o_num_acl
```
> Aquesta comanda es pot fer directament en el pas 1.

4. Especifiquem el destinatari dels *traps*
```
snmp-server host id-host [version {1 | 2c | 3 [auth | noauth | priv]}] 
    community-string 
```
> Per defecte no hi ha cap administrador *trap*

5. Habilitem *traps* en els agents
```
snmp-server enable traps tipus-de-notificació
```
> Si no s'especifiquen els tipus de *traps* s'habiliten totes. Per veure tots els tipus de notificacions:

```
snmp-server enable traps ?
```

Exemple:
```
R1(config)# snmp-server community batonaug ro SNMP_ACL
R1(config)# snmp-server location NOC_SNMP_MANAGER
R1(config)# snmp-server contact Wayne World
R1(config)# snmp-server host 192.168.1.3 version 2c batonaug
R1(config)# snmp-server enable traps
R1(config)# ip access-list standard SNMP_ACL
R1(config-std-nacl)# permit 192.168.1.3
```

## Enllaços
> https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/snmp/configuration/xe-16/snmp-xe-16-book/nm-snmp-cfg-snmp-support.html

> https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3560/software/release/12-2_20_se/configuration/guide/3560scg/swsnmp.pdf

> https://www.cisco.com/c/en/us/td/docs/optical/15000r/dwdm/configuration/guide/b_snmp.html

> https://ccnadesdecero.es/snmp-funcionamiento-configuracion/