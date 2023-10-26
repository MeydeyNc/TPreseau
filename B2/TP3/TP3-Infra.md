# TP3 INFRA : Prmeiers pas GNS, Cisco et VLAN.


### I. Dumb Switch. 


Nous avons définis les IPs de nos VPCs à l'aide de la console intégrée à GNS : 
````
PC1> ip 10.3.1.1
Checking for duplicate address...
PC1 : 10.3.1.1 255.255.255.0
````

````
PC2> ip 10.3.1.2
Checking for duplicate address...
PC2 : 10.3.1.2 255.255.255.0
````

Nous pouvons ping PC2 depuis PC1 : 
````
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=0.212 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=0.361 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=0.438 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=0.430 ms
````
La Cam table : 
````
IOU1#show mac address
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0050.7966.6800    DYNAMIC     Et0/1
   1    0050.7966.6801    DYNAMIC     Et0/2
Total Mac Addresses for this criterion: 2
````

### II. VLANs

Tout le monde peut se ping : 
````
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=0.315 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=0.616 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=0.308 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=0.317 ms
^C
PC1> ping 10.3.1.3

84 bytes from 10.3.1.3 icmp_seq=1 ttl=64 time=0.225 ms
84 bytes from 10.3.1.3 icmp_seq=2 ttl=64 time=0.403 ms
84 bytes from 10.3.1.3 icmp_seq=3 ttl=64 time=0.391 ms
84 bytes from 10.3.1.3 icmp_seq=4 ttl=64 time=0.355 ms
````

Nous venons de créer nos VLANs : 
````
IOU1#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/0, Et0/1, Et0/2, Et0/3
                                                Et1/0, Et1/1, Et1/2, Et1/3
                                                Et2/0, Et2/1, Et2/2, Et2/3
                                                Et3/0, Et3/1, Et3/2, Et3/3
10   Lan1                             active
20   Lan2                             active
[...]
````

Voici les commandes effectuées : 
````
IOU1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
IOU1(config)#vlan 10
IOU1(config-vlan)#name Lan1
IOU1(config-vlan)#exit
IOU1(config)#vlan 20
IOU1(config-vlan)#name Lan2
IOU1(config-vlan)#exit
IOU1(config)#exit
````

On configure les VLANs : 
````
IOU1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
IOU1(config)#interface Ethernet0/1
IOU1(config-if)#switchport mode access
IOU1(config-if)#switchport access vlan 10
IOU1(config-if)#exit
IOU1(config)#interface Ethernet0/2
IOU1(config-if)#switchport mode access
IOU1(config-if)#switchport access vlan 10
IOU1(config-if)#exit
IOU1(config)#interface Ethernet0/3
IOU1(config-if)#switchport mode access
IOU1(config-if)#switchport access vlan 20
IOU1(config-if)#exit
IOU1(config)#exit
````

On vérifie : 
````
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=0.218 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=0.422 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=0.658 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=0.400 ms
^C
PC1> ping 10.3.1.3

^Chost (10.3.1.3) not reachable
````

Les VLANs sont effectifs.

### III. Ptite VM DHCP.

