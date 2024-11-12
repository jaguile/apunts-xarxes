###### tags: `xarxes` 

# Testeig, verificació, certificació de cablejat

## Mapa de cablejat

Un mapa de cablejat és un test per veure que cadascun dels fils d’un cable termina correctament en cadascun dels extrems. 

Què et permet també veure en un mapa de cablejat:

* Parells oberts
* Curtcircuits
* Parells creuats
* Parells dividits
* En el cas de cables blindats, la integritat del blindatge.

### Parell obert (open)
Un dels fils no arriba a l'altre extrem.

### Curtcircuit (short)
Un dels fils contacta amb un altre sense l’aillament.

![](https://i.imgur.com/pgGsj7i.png)

### Parell invertit (reversed)

S’inverteix l’ordre en un mateix parell.

![](https://i.imgur.com/wPNvYTr.png)

### Parells creuats (crossed)

Quan els dos fils en un parell acaben en un altre parell i s’inverteixen amb els fils d’aquell parell. Per exemple, una terminació amb ordre A i l’altre amb l’ordre B.

![](https://i.imgur.com/2iYVxoB.png)

### Parell dividit (Split pair)

Quan un parell, arribant al final (en ambdues terminacions) inverteix un dels seus fils amb un altre fil d’un parell diferent. El que provoca això és que la senyal que viatja per cadascun d’aquells fils no és la mateixa que la que viatja pel fil del seu respectiu parell, provocant el que s’anomena Crosstalk (diafonia).

En aquest exemple, el pin 6 (verd, del parell 3) s’ha invertit en els dos extrems amb el pin 4 (blau, del parell 1).

![](https://i.imgur.com/cjSwlKt.png)

## Factors físics que afecten a la transmissió en un cable UTP

[Apunts comprovació i verificació d'un cable] (https://planificacionadministracionredes.readthedocs.io/es/latest/Tema04/Teoria.html#pruebas-de-rendimiento-de-los-enlaces)

| Paràmetre            | Descripció                                                                                                | Unitat de mesura | Objectiu del valor |
|----------------------|-----------------------------------------------------------------------------------------------------------|------------------|---------------------|
| **NEXT** (Near-End Crosstalk) | Diferència entre senyal emesa i la interferència sobre l'altre parell.          | dB               | **Alt** (major és millor) |
| **FEXT** (Far-End Crosstalk)  | Igual que NEXT però a l'extrem oposat del cable.                                  | dB               | **Alt** (major és millor) |
| **ACR-N** (Attenuation to Crosstalk Ratio - Near End) | Relació entre l'atenuació i el NEXT, indicant la qualitat del senyal rebut.     | dB               | **Alt** (major és millor) |
| **ACR-F** (Attenuation to Crosstalk Ratio - Far End)  | Similar a l'ACR-N però mesurat a l'extrem oposat del cable.                        | dB               | **Alt** (major és millor) |
| **RL** (Pèrdua de retorn)        | Mesura la diferència entre la senyal emesa i la que es reflecteix cap a l'emissor degut a imperfeccions del cable.    | dB               | **Alt** (major és millor) |
| **PSNEXT** (Power Sum Near-End Crosstalk) | Mesura el NEXT en cada parell tenint en compte la suma de les interferències dels altres. | dB               | **Alt** (major és millor) |
| **PSELFEXT** (Power Sum Equal-Level Far-End Crosstalk) | Mesura el FEXT tenint en compte totes les interferències dels altres parells.    | dB               | **Alt** (major és millor) |
| **Atenuació (o pèrdua d'inserció)**         | Reducció del senyal a mesura que viatja pel cable.                                                       | dB               | **Baix** (menor és millor) |
| **Longitud**         | Mesura de la longitud total del cable per assegurar que no supera el màxim permès.                        | metres (m)       | **Segons les normes** (menor que 100 m) |
| **Retard de propagació (o temps propi)** | Retard total en el temps que triga el senyal a arribar d'un extrem a l'altre.                            | nanosegons (ns) | **Baix** (menor és millor) |
| **Delay Skew (Diferència de retard)**       | Diferència de retard entre el parell que més retard de propagació té i el que menys (afecta la sincronització de la transmissió de dades)             | nanosegons (ns) | **Baix** (menor és millor) |
| **PSACR-N** (Power Sum ACR-N) | Relació entre l'atenuació i la suma del NEXT de tots els parells al mateix extrem.               | dB               | **Alt** (major és millor) |
| **PSACR-F** (Power Sum ACR-F) | Relació entre l'atenuació i la suma del FEXT de tots els parells a l'extrem oposat.             | dB               | **Alt** (major és millor) |

### Altres paràmetres

#### NVP

El NVP (Nominal Velocity of Propagation) és un paràmetre que indica la velocitat a la qual el senyal elèctric es desplaça pel cable en comparació amb la velocitat de la llum en el buit. S'expressa com un percentatge de la velocitat de la llum.

Per exemple, si un cable UTP té un NVP del 70%, això significa que el senyal es propaga pel cable a una velocitat del 70% de la velocitat de la llum.
Importància del NVP

El NVP és fonamental en les certificacions de cables perquè:

    Permet a la certificadora calcular amb precisió la longitud del cable i el retard de propagació del senyal. La longitud s'obté mesurant el temps que triga el senyal a viatjar pel cable i tornar, i el NVP permet convertir aquest temps en una mesura de longitud.
    Un NVP incorrecte pot provocar errors en la mesura de la longitud, que és especialment problemàtic quan es certifica el cablejat segons els estàndards que limiten la longitud màxima (com els 100 m per a cables Ethernet en instal·lacions convencionals).

Cada tipus de cable té un NVP nominal específic, que depèn de la seva construcció, materials, i l'aïllament dels conductors.