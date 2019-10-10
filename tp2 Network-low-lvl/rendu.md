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
      ```
      IOU3#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    aabb.cc00.0200    DYNAMIC     Et0/2
   1    aabb.cc00.0400    DYNAMIC     Et0/1
   1    aabb.cc00.0420    DYNAMIC     Et0/2

      ```
    - comprendre/expliquer chaque ligne
    



* En lançant Wireshark sur les liens des switches, il y a des trames CDP qui circulent. Quoi qu'est-ce ?

### Mise en évidence du Spanning Tree Protocol

* Déterminer les informations STP
    - à l'aide des commandes dédiées au protocole

* Faire un schéma en représentant les informations STP
    - rôle des switches (qui est le root bridge)
    - rôle de chacun des ports



* Confirmer les informations STP
    - effectuer un ping d'une machine à une autre
    - vérifier que les trames passent bien par le chemin attendu (Wireshark)



* Ainsi, déterminer quel lien a été désactivé par STP

* Faire un schéma qui explique le trajet d'une requête ARP lorsque PC1 ping PC3, et de sa réponse
    - Représenter TOUTES les trames ARP (n'oubliez pas les broadcasts)



### Reconfigurer STP


* Changer la priorité d'un switch qui n'est pas le root bridge


* Vérifier les changements
    - avec des commandes sur les switches
    - capturer les échanges qui suivent une reconfiguration STP avec Wireshark


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

* Faire communiquer les PCs deux à deux
    - vérifier que PC2 ne peut joindre que PC3
    - vérifier que PC1 ne peut joindre personne alors qu'il est dans le même réseau (sad)

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

* Faire communiquer les PCs deux à deux
    - vérifier que PC1 ne peut joindre que PC3
    - vérifier que PC4 ne peut joindre que PC2

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