# TP4 : Buffet à volonté

## I. Quelques ping

Admin1 => Admin2
```
admin1> ping 10.5.10.12
84 bytes from 10.5.10.12 icmp_seq=1 ttl=64 time=33.019 ms
84 bytes from 10.5.10.12 icmp_seq=2 ttl=64 time=1.524 ms
84 bytes from 10.5.10.12 icmp_seq=3 ttl=64 time=1.721 ms
84 bytes from 10.5.10.12 icmp_seq=4 ttl=64 time=3.683 ms
84 bytes from 10.5.10.12 icmp_seq=5 ttl=64 time=1.112 ms
```
Guest3 => Guest1
```
guest3> ping 10.5.20.11
host (10.5.20.11) not reachable
```
Admin2 => Guest2
```
admin2> ping 10.5.20.12
No gateway found
```

## II. Donf et machine virtuelle
* [Conf GNS3](tp4DNS.gns3)
* Impossible de mettre la Vm dns