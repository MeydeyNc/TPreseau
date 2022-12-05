# TP-5 Reseau et Infra. 

## I. 3. 

On définit les ip statiques demandées via la commande ci-dessous : 

````
PC2> ip 10.5.1.2/24 
Checking for duplicate address...
PC2 : 10.5.1.2 255.255.255.0
````
Commande effectuée pour PC1 et PC2 : 

````
PC1> ip 10.5.1.1/24 
Checking for duplicate address...
PC1 : 10.5.1.1 255.255.255.0
````

On ping pour voir que tout va bien : 

````
PC2> ping 10.5.1.1

84 bytes from 10.5.1.1 icmp_seq=1 ttl=64 time=0.322 ms
84 bytes from 10.5.1.1 icmp_seq=2 ttl=64 time=0.366 ms
84 bytes from 10.5.1.1 icmp_seq=3 ttl=64 time=0.391 ms
^C
````
Notre ping fonctionne. 

## II. 3. 

On va modifier les ips pour avoir celles qui sont demandées. 
On ré-utilise la commande précédente : 

````
PC3> ip 10.5.10.3/24 
Checking for duplicate address...
PC3 : 10.5.10.3 255.255.255.0
````

On vérifie que tout le monde peut se ping : 

````
PC3> ping 10.5.10.2

84 bytes from 10.5.10.2 icmp_seq=1 ttl=64 time=0.247 ms
84 bytes from 10.5.10.2 icmp_seq=2 ttl=64 time=0.417 ms
84 bytes from 10.5.10.2 icmp_seq=3 ttl=64 time=0.359 ms
84 bytes from 10.5.10.2 icmp_seq=4 ttl=64 time=0.417 ms
^C
PC3> ping 10.5.10.1

84 bytes from 10.5.10.1 icmp_seq=1 ttl=64 time=0.317 ms
84 bytes from 10.5.10.1 icmp_seq=2 ttl=64 time=0.449 ms
84 bytes from 10.5.10.1 icmp_seq=3 ttl=64 time=0.396 ms
84 bytes from 10.5.10.1 icmp_seq=4 ttl=64 time=0.554 ms
^C
````

Nous configurons notre switch afin d'y intégrer 2 vlans distincts. 
Le vlan 10 : 
````
sw1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
sw1(config)#
sw1(config)#interface Ethernet0/1
sw1(config-if)#
sw1(config-if)#switchport mode access
sw1(config-if)#
sw1(config-if)#switchport access vlan 10
sw1(config-if)#
sw1(config-if)#
sw1(config-if)#
sw1(config-if)#exit
````
 - Nous avons aussi intégrer dans le vlan 10, le port Ethernet 0/0 avec la même commande. 

le vlan 20 : 
````
sw1(config)#interface Ethernet0/2
sw1(config-if)#
sw1(config-if)#switchport mode access
sw1(config-if)#
sw1(config-if)#switchport access vlan 20
sw1(config-if)#
sw1(config-if)#exit
sw1(config)#
sw1(config)#exit
````
Nous vérifions que tout le monde est au bon endroit : 

````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   admins                           active    Et0/0, Et0/1
20   guests                           active    Et0/2
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
````

On essaie de ping PC2 avec PC1 : 
````
PC1> ping 10.5.10.2

84 bytes from 10.5.10.2 icmp_seq=1 ttl=64 time=0.222 ms
84 bytes from 10.5.10.2 icmp_seq=2 ttl=64 time=0.534 ms
84 bytes from 10.5.10.2 icmp_seq=3 ttl=64 time=0.367 ms
^C
````
ça fonctionne. 

On ressaie avec PC1 sur PC3 : 
````
PC1> ping 10.5.10.3

^Chost (10.5.10.3) not reachable
````
ça ne fonctionne pas, nous venons bien de définir 2 différents vlan. 

## III. 3.

Nous venons de définir les IPs pour nos pcs, comme vus précédemment. Ainsi que d'importer notre VM dans le réseau. 

Nous pouvons voir actuellement l'état de nos vlans : 

````
sw1#show vlan br

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et1/1, Et1/2, Et1/3, Et2/0
                                                Et2/1, Et2/2, Et2/3, Et3/0
                                                Et3/1, Et3/2, Et3/3
10   admins                           active    Et0/0, Et0/1
20   guests                           active    Et0/2
30   servers                          active    Et0/3
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
````

Nous venons de configurer le trunk pour notre routeur : 

````
sw1#show interface trunk

Port        Mode             Encapsulation  Status        Native vlan
Et1/0       on               802.1q         trunking      1

Port        Vlans allowed on trunk
Et1/0       1-4094

Port        Vlans allowed and active in management domain
Et1/0       1,10,20,30

Port        Vlans in spanning tree forwarding state and not pruned
Et1/0       1,10,20,30
sw1#
````

Nous configurons donc notre routeur pour la suite : 
````
R1(config)#interface fastEthernet 0/0.30
R1(config-subif)#encapsulation dot1Q 30
R1(config-subif)#ip addr 10.5.30.254 255.255.255.0
R1(config-subif)#exit
````
Nous l'effectuons évidemment sur nos 3 vlans (10,20,30). 
Voici ce que nous avons à la suite de nos ajustements : 

````
R1#show ip interface br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  administratively down down
FastEthernet0/0.10         10.5.10.254     YES manual administratively down down
FastEthernet0/0.20         10.5.20.254     YES manual administratively down down
FastEthernet0/0.30         10.5.30.254     YES manual administratively down down
FastEthernet0/1            unassigned      YES unset  administratively down down
FastEthernet1/0            unassigned      YES unset  administratively down down
FastEthernet2/0            unassigned      YES unset  administratively down down
````

Il nous faut ensuite mettre en fonction l'interface 0/0 : 

````
R1(config)#interface fastEthernet 0/0
R1(config-if)#no shut
````

Nous vérifions que tout est en marche : 

````
R1#show ip interface br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  up                    up
FastEthernet0/0.10         10.5.10.254     YES manual up                    up
FastEthernet0/0.20         10.5.20.254     YES manual up                    up
FastEthernet0/0.30         10.5.30.254     YES manual up                    up
FastEthernet0/1            unassigned      YES unset  administratively down down
FastEthernet1/0            unassigned      YES unset  administratively down down
FastEthernet2/0            unassigned      YES unset  administratively down down
````
L'interface est lancée, nous allons voir si la connexion est effective. 
Nous pouvons ping depuis un même réseau: 

````
pc1> ping 10.5.10.254

84 bytes from 10.5.10.254 icmp_seq=1 ttl=255 time=3.766 ms
84 bytes from 10.5.10.254 icmp_seq=2 ttl=255 time=11.044 ms
84 bytes from 10.5.10.254 icmp_seq=3 ttl=255 time=2.788 ms
84 bytes from 10.5.10.254 icmp_seq=4 ttl=255 time=7.348 ms
84 bytes from 10.5.10.254 icmp_seq=5 ttl=255 time=5.719 ms
^C
````

Nous allons ajouter des routes par défaut : 

````
pc1> ip 10.5.10.1/10.5.10.254
Checking for duplicate address...
pc1 : 10.5.10.1 255.255.255.0 gateway 10.5.10.254
````

Nous avons configurer la route par défaut sur notre vm : 

````
sudo ip route add default via 10.5.30.254 dev enp0s3

````

Nous pouvons ping la vm depuis pc1 : 

````
pc1> ping 10.5.30.1

84 bytes from 10.5.30.1 icmp_seq=1 ttl=63 time=16.556 ms
84 bytes from 10.5.30.1 icmp_seq=2 ttl=63 time=13.050 ms
84 bytes from 10.5.30.1 icmp_seq=3 ttl=63 time=16.741 ms
84 bytes from 10.5.30.1 icmp_seq=4 ttl=63 time=17.856 ms
^C
````

Nous pouvons ping depuis adm1 : 

````
adm1> ping 10.5.10.1

84 bytes from 10.5.10.1 icmp_seq=1 ttl=63 time=30.143 ms
84 bytes from 10.5.10.1 icmp_seq=2 ttl=63 time=12.284 ms
84 bytes from 10.5.10.1 icmp_seq=3 ttl=63 time=13.242 ms
^C
````
````
adm1> ping 10.5.30.1

84 bytes from 10.5.30.1 icmp_seq=1 ttl=63 time=14.119 ms
84 bytes from 10.5.30.1 icmp_seq=2 ttl=63 time=21.890 ms
84 bytes from 10.5.30.1 icmp_seq=3 ttl=63 time=12.027 ms
84 bytes from 10.5.30.1 icmp_seq=4 ttl=63 time=14.286 ms
^C
````


## IV. 3. 

Nous pouvons ping 1.1.1.1 depuis notre routeur : 

````
R1#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 28/32/44 ms
````

Nous allons maintenant paramétrer notre NAT. 

Nous paramètrons notre interface interne : 
````
R1(config)#interface fastEthernet 0/0
R1(config-if)#ip nat inside

*Mar  1 00:10:38.455: %LINEPROTO-5-UPDOWN: Line protocol on Interface NVI0, changed state to up
R1(config-if)#
````

Notre interface externe : 
````
R1(config)#interface fastEthernet 0/1
R1(config-if)#ip nat outside
R1(config-if)#
R1(config-if)#exit
````

On check notre interface ip : 
````
R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES NVRAM  up                    up
FastEthernet0/0.10         10.5.10.254     YES NVRAM  up                    up
FastEthernet0/0.20         10.5.20.254     YES NVRAM  up                    up
FastEthernet0/0.30         10.5.30.254     YES NVRAM  up                    up
FastEthernet0/1            192.168.122.78  YES DHCP   up                    up
FastEthernet1/0            unassigned      YES NVRAM  administratively down down
FastEthernet2/0            unassigned      YES NVRAM  administratively down down
NVI0                       10.5.10.254     YES unset  up                    up
````

A partir d'ici malheureusement je n'ai pas réussi à établir la connexion internet pour les VPCs et la VM. 
Avant la répartition de connexion nat inside/outside je pouvais ping internet depuis le routeur, puis plus rien. 


