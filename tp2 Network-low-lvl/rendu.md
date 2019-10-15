# TP2 : Network low-level, Switching

## I. Simplest setup

### Plan d'adressage

<table>
  <tr>
    <td>Machine</td><td>net1</td>
  </tr>
  <tr>
    <td>Pc1</td><td>10.2.1.1/24</td>
  </tr>
  <tr>
  <td>Pc2</td><td>10.2.1.2/24</td>
  </tr>
</table>


### To Do

* Mettre en place la topologie ci-dessus

<img src="https://cdn.discordapp.com/attachments/582825013690892290/629265229192101888/unknown.png">

* Faire communiquer les deux PCs 
    - avec un ping qui fonctionne
        Pc1 vers Pc2
        ```
        PC-1> ping 10.2.1.2/24
        84 bytes from 10.2.1.2 icmp_seq=1 ttl=64 time=0.170 ms
        84 bytes from 10.2.1.2 icmp_seq=2 ttl=64 time=0.665 ms
        ```

        Pc2 vers Pc1
        ```
        PC-2> ping 10.2.1.1/24
        84 bytes from 10.2.1.1 icmp_seq=1 ttl=64 time=0.947 ms
        84 bytes from 10.2.1.1 icmp_seq=2 ttl=64 time=0.336 ms
        ```
        
        * déterminer le protocole utilisé par ping à l'aide de Wireshark

            Le protocole utilisé par le ping est le protocole ICMP "Internet Control Message Protocol

    - analyser les échanges ARP
        * utiliser Wireshark et mettre en évidence l'échange ARP entre les deux machines (ARP Request et ARP Reply)

            <img src="https://cdn.discordapp.com/attachments/582825013690892290/629270154685054978/unknown.png">

        * corréler avec les tables ARP des différentes machines

            Table ARP Pc1
            ```
            PC-1> show arp

            00:50:79:66:68:01  10.2.1.2 expires in 114 seconds
            ```

            Table ARP Pc2

            ```
            PC-2> show arp
            
            00:50:79:66:68:00  10.2.1.1 expires in 114 seconds
            ```



* Récapituler toutes les étapes (dans le compte-rendu, à l'écrit) quand PC1 exécute ping PC2 pour la première fois
    - échanges ARP
        * 10.2.1.1 envoie une request
        * 10.2.1.2 envoie une réponse 
    - échange ping




* Expliquer...
    - pourquoi le switch n'a pas besoin d'IP
      * Il sert de lien entre les machines
    - pourquoi les machines ont besoin d'une IP pour pouvoir se ping
      * Elles ont besoin d'une IP pour ce trouver dans le réseau 


## II. More switches

### Plan d'adressage

<table>
  <tr>
    <td>Machine</td><td>net1</td>
  </tr>
  <tr>
    <td>Pc1</td><td>10.2.2.1/24</td>
  </tr>
  <tr>
  <td>Pc2</td><td>10.2.2.2/24</td>
  </tr>
  <tr>
    <td>Pc3</td><td>10.2.2.3/24</td>
  </tr>
</table>

### ToDo

* Mettre en place la topologie ci-dessus

* Faire communiquer les trois PCs
    - avec des ping qui fonctionnent
        Pc1 ping Pc2&Pc3
        ```
        PC-1> ping 10.2.2.2/24
        84 bytes from 10.2.2.2 icmp_seq=1 ttl=64 time=2.351 ms
        84 bytes from 10.2.2.2 icmp_seq=2 ttl=64 time=0.574 ms
        84 bytes from 10.2.2.2 icmp_seq=3 ttl=64 time=0.389 ms
        84 bytes from 10.2.2.2 icmp_seq=4 ttl=64 time=0.381 ms
        84 bytes from 10.2.2.2 icmp_seq=5 ttl=64 time=1.465 ms

        PC-1> ping 10.2.2.3
        84 bytes from 10.2.2.3 icmp_seq=1 ttl=64 time=1.360 ms
        84 bytes from 10.2.2.3 icmp_seq=2 ttl=64 time=1.038 ms
        84 bytes from 10.2.2.3 icmp_seq=3 ttl=64 time=1.639 ms
        84 bytes from 10.2.2.3 icmp_seq=4 ttl=64 time=1.879 ms
        84 bytes from 10.2.2.3 icmp_seq=5 ttl=64 time=1.133 ms
        ```


        Pc2 ping Pc3&Pc1
        ```
        PC-2> ping 10.2.2.3
        84 bytes from 10.2.2.3 icmp_seq=1 ttl=64 time=0.965 ms
        84 bytes from 10.2.2.3 icmp_seq=2 ttl=64 time=0.860 ms
        84 bytes from 10.2.2.3 icmp_seq=3 ttl=64 time=0.853 ms
        84 bytes from 10.2.2.3 icmp_seq=4 ttl=64 time=1.158 ms
        84 bytes from 10.2.2.3 icmp_seq=5 ttl=64 time=1.408 ms

        PC-2> ping 10.2.2.1
        84 bytes from 10.2.2.1 icmp_seq=1 ttl=64 time=0.685 ms
        84 bytes from 10.2.2.1 icmp_seq=2 ttl=64 time=0.386 ms
        84 bytes from 10.2.2.1 icmp_seq=3 ttl=64 time=0.445 ms
        84 bytes from 10.2.2.1 icmp_seq=4 ttl=64 time=0.395 ms
        84 bytes from 10.2.2.1 icmp_seq=5 ttl=64 time=0.459 ms
        ```

        Pc3 ping Pc1&Pc2
        ```
        PC-3> ping 10.2.2.1
        84 bytes from 10.2.2.1 icmp_seq=1 ttl=64 time=1.950 ms
        84 bytes from 10.2.2.1 icmp_seq=2 ttl=64 time=1.954 ms
        84 bytes from 10.2.2.1 icmp_seq=3 ttl=64 time=0.916 ms
        84 bytes from 10.2.2.1 icmp_seq=4 ttl=64 time=0.928 ms
        84 bytes from 10.2.2.1 icmp_seq=5 ttl=64 time=0.984 ms

        PC-3> ping 10.2.2.2
        84 bytes from 10.2.2.2 icmp_seq=1 ttl=64 time=1.008 ms
        84 bytes from 10.2.2.2 icmp_seq=2 ttl=64 time=0.975 ms
        84 bytes from 10.2.2.2 icmp_seq=3 ttl=64 time=0.982 ms
        84 bytes from 10.2.2.2 icmp_seq=4 ttl=64 time=0.976 ms
        84 bytes from 10.2.2.2 icmp_seq=5 ttl=64 time=1.966 ms
        ```

* Analyser la table MAC d'un switch
    - show mac address-table
      
      <img src="https://cdn.discordapp.com/attachments/582825013690892290/631767082475716608/unknown.png">
      (Déso le copié/collé mettait en pls mes balises)
    - comprendre/expliquer chaque ligne
      * Type de lan
      * Adresse Mac
      * Type d'adresse (dynamique ou non)
      * Ports utilisé  
* En lançant Wireshark sur les liens des switches, il y a des trames CDP qui circulent. Quoi qu'est-ce ?
  - C'est un protocole cisco qui permet de trouver les péripheriques connecté directement.

### Mise en évidence du Spanning Tree Protocol

* Déterminer les informations STP
    - à l'aide des commandes dédiées au protocole

* Faire un schéma en représentant les informations STP
    - rôle des switches (qui est le root bridge)
    - rôle de chacun des ports

```
                        +-----+
                        | PC2 |
                        +--+--+
                           |
                           |
                       +---+---+ 
                   +---+  SW2  +----+
                   |   +-------+    |
                   |                |
                   |                |
+-----+        +---+---+        +---+---+        +-----+
| PC1 +--------+  SW1  +--------+  SW3  +--------+ PC3 |
+-----+        +-------+        +-------+        +-----+
```

* SW2 = Root bridge 
  - Tous les ports designated forward
* SW1
  - Et0/2 root vers SW2
  - Tous les autres designated forward

* SW3
  - Et0/0 Alternate vers SW1 (c'est un chemin alternatif)
  - Et0/2  root vers SW2
  - Tous les autres designated forward

* Confirmer les informations STP
    - effectuer un ping d'une machine à une autre
    - vérifier que les trames passent bien par le chemin attendu (Wireshark)

    Pc1 ping Pc3
    - SW1 vers SW2
    <img src ="https://cdn.discordapp.com/attachments/582825013690892290/631788772144447489/unknown.png">

    - SW2 vers SW3
    <img src="https://cdn.discordapp.com/attachments/582825013690892290/631789343446532096/unknown.png">

    - SW1 vers SW3  
    Aucune trames du ping passe par ici



* Ainsi, déterminer quel lien a été désactivé par STP
  - Le lien SW1 vers SW3 a été désactivé. 
* Faire un schéma qui explique le trajet d'une requête ARP lorsque PC1 ping PC3, et de sa réponse
    - Représenter TOUTES les trames ARP (n'oubliez pas les broadcasts)

    <img src ="https://media.discordapp.net/attachments/582825013690892290/633569141567258634/schemarequetearp.png?width=786&height=355">

    Dans cette exemple les flêches rouges sont les demandes de qui est l'ip 10.2.2.3, les bleues sont les réponses.


### Reconfigurer STP


* Changer la priorité d'un switch qui n'est pas le root bridge


* Vérifier les changements
    - avec des commandes sur les switches
    
```
IOU1#show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: VLAN0001
Extended system ID                      is enabled
Portfast Default                        is disabled
Portfast Edge BPDU Guard Default        is disabled
Portfast Edge BPDU Filter Default       is disabled
Loopguard Default                       is disabled
PVST Simulation Default                 is enabled but inactive in rapid-pvst mode
Bridge Assurance                        is enabled
EtherChannel misconfig guard            is enabled
Configured Pathcost method used is short
UplinkFast                              is disabled
BackboneFast                            is disabled

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
VLAN0001                     0         0        0         16         16
---------------------- -------- --------- -------- ---------- ----------
1 vlan                       0         0        0         16         16
```
    Le root bridge est désormais suur le SW1


  - capturer les échanges qui suivent une reconfiguration STP avec Wireshark
  
    * Pc3 ping Pc1 échanges entre le SW3 et SW1
    <img src ="https://cdn.discordapp.com/attachments/582825013690892290/633578737572642816/unknown.png">
    Aucun échanges hormis le broadcast ARP entre le SW3/SW2 et SW2/SW1


## III. Isolation

### 1. Simple

#### Plan d'adressage 


<table>
  <tr>
    <td>Machine</td><td>net1</td><td>Vlan</td>
  </tr>
  <tr>
    <td>Pc1</td><td>10.2.3.1/24</td><td>10</td>
  </tr>
  <tr>
  <td>Pc2</td><td>10.2.3.2/24</td><td>20</td>
  </tr>
  <tr>
    <td>Pc3</td><td>10.2.3.3/24</td><td>20</td>
  </tr>
</table>

#### ToDo


* Mettre en place la topologie ci-dessus
    - voir les commandes dédiées à la manipulation de VLANs
```
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   client-network                   active    Et0/0
20   client-network20                 active    Et0/1, Et0/2
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
```
* Faire communiquer les PCs deux à deux
    - vérifier que PC2 ne peut joindre que PC3

```
Ping Pc2 vers Pc3
  PC-2> ping 10.2.3.3/24
  84 bytes from 10.2.3.3 icmp_seq=1 ttl=64 time=0.675 ms
  84 bytes from 10.2.3.3 icmp_seq=2 ttl=64 time=0.756 ms
  84 bytes from 10.2.3.3 icmp_seq=3 ttl=64 time=0.829 ms
  84 bytes from 10.2.3.3 icmp_seq=4 ttl=64 time=1.557 ms
  84 bytes from 10.2.3.3 icmp_seq=5 ttl=64 time=0.909 ms
```

```
Ping Pc2 vers Pc1
  PC-2> ping 10.2.3.1/24
  host (10.2.3.1) not reachable
```
<br>
    - vérifier que PC1 ne peut joindre personne alors qu'il est dans le même réseau (sad)

```
PC-1> ping 10.2.3.2/24
host (10.2.3.2) not reachable

PC-1> ping 10.2.3.3/24
host (10.2.3.3) not reachable
```

### 2. Avec trunk

#### Plan d'adressage 

<table>
  <tr>
    <td>Machine</td><td>net1</td><td>net 2</td><td>VLAN</td>
  </tr>
  <tr>
    <td>Pc1</td><td>10.2.10.1/24</td><td>X</td><td>10</td>
  </tr>
  <tr>
  <td>Pc2</td><td>X</td><td>10.2.20.1/24</td><td>20</td>
  </tr>
  <tr>
    <td>Pc3</td><td>10.2.10.2/24</td><td>X</td><td>10</td>
  </tr>
  <tr>
    <td>Pc4</td><td>X</td><td>10.2.20.2/24</td><td>20</td>
  </tr>
</table>

#### ToDo


* Mettre en place la topologie ci-dessus
```
IOU1#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   client-network                   active    Et0/0
20   client-network20                 active    Et0/1
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
```
```
IOU2#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   client-network                   active    Et0/1
20   client-network20                 active    Et0/2
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
```

* Faire communiquer les PCs deux à deux
    - vérifier que PC1 ne peut joindre que PC3
```
Pc1 vers Pc3
PC-1> ping 10.2.10.2/24
84 bytes from 10.2.10.2 icmp_seq=1 ttl=64 time=0.867 ms
84 bytes from 10.2.10.2 icmp_seq=2 ttl=64 time=1.827 ms
84 bytes from 10.2.10.2 icmp_seq=3 ttl=64 time=0.881 ms
84 bytes from 10.2.10.2 icmp_seq=4 ttl=64 time=1.869 ms
84 bytes from 10.2.10.2 icmp_seq=5 ttl=64 time=1.140 ms
```
```
Pc1 vers Pc2
PC-1> ping 10.2.20.1/24
host (255.255.255.0) not reachable
```
```
Pc1 vers Pc4
PC-1> ping 10.2.20.2/24
host (255.255.255.0) not reachable
```
<br>
    - vérifier que PC4 ne peut joindre que PC2

```
Pc4 vers Pc2
PC-4> ping 10.2.20.1/24
84 bytes from 10.2.20.1 icmp_seq=1 ttl=64 time=0.315 ms
84 bytes from 10.2.20.1 icmp_seq=2 ttl=64 time=0.465 ms
84 bytes from 10.2.20.1 icmp_seq=3 ttl=64 time=0.352 ms
84 bytes from 10.2.20.1 icmp_seq=4 ttl=64 time=0.443 ms
84 bytes from 10.2.20.1 icmp_seq=5 ttl=64 time=0.389 ms
```
```
Pc4 vers Pc1
PC-4> ping 10.2.10.1/24
host (255.255.255.0) not reachable
```
```
Pc4 vers Pc3
PC-4> ping 10.2.10.2/24
host (255.255.255.0) not reachable
```

* Mettre en évidence l'utilisation des VLANs avec Wireshark

## IV. Need perfs

### Plan d'adressage

<table>
  <tr>
    <td>Machine</td><td>net1</td><td>net 2</td><td>VLAN</td>
  </tr>
  <tr>
    <td>Pc1</td><td>10.2.10.1/24</td><td>X</td><td>10</td>
  </tr>
  <tr>
  <td>Pc2</td><td>X</td><td>10.2.20.1/24</td><td>20</td>
  </tr>
  <tr>
    <td>Pc3</td><td>10.2.10.2/24</td><td>X</td><td>10</td>
  </tr>
  <tr>
    <td>Pc4</td><td>X</td><td>10.2.20.2/24</td><td>20</td>
  </tr>
</table>

### ToDo

* Mettre en place la topologie ci-dessus
    - configurer LACP entre SW1 et SW2
    - utiliser Wireshark pour mettre en évidence l'utilisation de trames LACP
    - vérifier avec un show ip interface po1 que la bande passante a bien été doublée