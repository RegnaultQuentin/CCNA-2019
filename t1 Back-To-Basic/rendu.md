# Bact to basic

## I. Gather informations

* Récupérer une liste des cartes réseau avec leur nom, leur IP et leur adresse MAC
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:26:34:c5 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86064sec preferred_lft 86064sec
    inet6 fe80::ed40:af4e:b1e5:101a/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:f4:f7:80 brd ff:ff:ff:ff:ff:ff
    inet 192.168.188.3/24 brd 192.168.188.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fef4:f780/64 scope link
       valid_lft forever preferred_lft forever
```
* Déterminer si les cartes réseaux ont récupéré une IP en DHCP ou non
    Carte enp0s3
```
DHCP4.OPTION[3]:                        expiry = 1569572886
DHCP4.OPTION[4]:                        ip_address = 10.0.2.15
```
    La carte enp0s8 n'a pas d'Ip en DHCP.

* Afficher la table de routage de la machine et sa table ARP

Table de routage
```
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
192.168.188.0/24 dev enp0s8 proto kernel scope link src 192.168.188.3 metric 101
```

Table ARP
```
10.0.2.2 dev enp0s3 lladdr 52:54:00:12:35:02 STALE
Cette route est celle de la carte enp0s3, elle est utilisée pour une connexion externe, la passerelle de cette route est à l'IP 10.0.2.2.

192.168.188.1 dev enp0s8 lladdr 0a:00:27:00:00:36 REACHABLE
Cette route est celle de la carte enp0s8, elle est utilisée pour une connexion local, la passerelle de cette route est à l'IP 192.168.188.1.
```
* Récupérer la liste des ports en écoute (listening) sur la machine (TCP et UDP)
```
; <<>> DiG 9.11.4-P2-RedHat-9.11.4-17.P2.el8_0.1 <<>> www.reddit.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62101
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 13, ADDITIONAL: 27

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;www.reddit.com.                        IN      A

;; ANSWER SECTION:
www.reddit.com.         42      IN      CNAME   reddit.map.fastly.net.
reddit.map.fastly.net.  29      IN      A       151.101.1.140
reddit.map.fastly.net.  29      IN      A       151.101.193.140
reddit.map.fastly.net.  29      IN      A       151.101.65.140
reddit.map.fastly.net.  29      IN      A       151.101.129.140

;; AUTHORITY SECTION:
net.                    168707  IN      NS      g.gtld-servers.net.
net.                    168707  IN      NS      c.gtld-servers.net.
net.                    168707  IN      NS      h.gtld-servers.net.
net.                    168707  IN      NS      a.gtld-servers.net.
net.                    168707  IN      NS      l.gtld-servers.net.
net.                    168707  IN      NS      k.gtld-servers.net.
net.                    168707  IN      NS      m.gtld-servers.net.
net.                    168707  IN      NS      f.gtld-servers.net.
net.                    168707  IN      NS      i.gtld-servers.net.
net.                    168707  IN      NS      d.gtld-servers.net.
net.                    168707  IN      NS      e.gtld-servers.net.
net.                    168707  IN      NS      j.gtld-servers.net.
net.                    168707  IN      NS      b.gtld-servers.net.

;; ADDITIONAL SECTION:
a.gtld-servers.net.     168695  IN      A       192.5.6.30
a.gtld-servers.net.     168695  IN      AAAA    2001:503:a83e::2:30
m.gtld-servers.net.     168695  IN      A       192.55.83.30
m.gtld-servers.net.     168695  IN      AAAA    2001:501:b1f9::30
j.gtld-servers.net.     168695  IN      A       192.48.79.30
j.gtld-servers.net.     168695  IN      AAAA    2001:502:7094::30
k.gtld-servers.net.     168695  IN      A       192.52.178.30
k.gtld-servers.net.     168695  IN      AAAA    2001:503:d2d::30
f.gtld-servers.net.     168695  IN      A       192.35.51.30
f.gtld-servers.net.     168695  IN      AAAA    2001:503:d414::30
c.gtld-servers.net.     168695  IN      A       192.26.92.30
c.gtld-servers.net.     168695  IN      AAAA    2001:503:83eb::30
g.gtld-servers.net.     168695  IN      A       192.42.93.30
g.gtld-servers.net.     168695  IN      AAAA    2001:503:eea3::30
l.gtld-servers.net.     168695  IN      A       192.41.162.30
l.gtld-servers.net.     168695  IN      AAAA    2001:500:d937::30
b.gtld-servers.net.     168695  IN      A       192.33.14.30
b.gtld-servers.net.     168695  IN      AAAA    2001:503:231d::2:30
i.gtld-servers.net.     168695  IN      A       192.43.172.30
i.gtld-servers.net.     168695  IN      AAAA    2001:503:39c1::30
h.gtld-servers.net.     168695  IN      A       192.54.112.30
h.gtld-servers.net.     168695  IN      AAAA    2001:502:8cc::30
e.gtld-servers.net.     168695  IN      A       192.12.94.30
e.gtld-servers.net.     168695  IN      AAAA    2001:502:1ca1::30
d.gtld-servers.net.     168695  IN      A       192.31.80.30
d.gtld-servers.net.     168695  IN      AAAA    2001:500:856e::30

;; Query time: 58 msec
;; SERVER: 10.33.10.20#53(10.33.10.20)
;; WHEN: Thu Sep 26 05:34:16 EDT 2019
;; MSG SIZE  rcvd: 935
```
* Afficher l'état actuel du firewall



### Récupération des données système

## II. Edit configuration

### 1. Configuration cartes réseau

### 2. Serveur SSH

