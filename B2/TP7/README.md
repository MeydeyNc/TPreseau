# 3-tier architecture et redondance. 

Voici les confs : 

- R1 : 
````
Current configuration : 1786 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
[...]
!
ip name-server 1.1.1.1
!
interface FastEthernet0/0
ip address dhcp
ip nat outside
ip virtual-reassembly
duplex auto
speed auto
!
interface FastEthernet1/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0.10
 encapsulation dot1Q 10
 ip address 10.7.10.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 10 ip 10.7.10.254
 standby 10 priority 150
 standby 10 preempt
!
!
interface FastEthernet1/0.30
 encapsulation dot1Q 30
 ip address 10.7.30.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 30 ip 10.7.30.254
!
ip dns server
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
no cdp log mismatch duplex
!        
````

- R2 :
````
hostname R2
!
[...]
!
ip name-server 1.1.1.1
!
!
interface FastEthernet0/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0.10
 encapsulation dot1Q 10
 ip address 10.7.10.253 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 10 ip 10.7.10.254
!
interface FastEthernet1/0.20
 encapsulation dot1Q 20
 ip address 10.7.20.253 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 20 ip 10.7.20.254
!
interface FastEthernet1/0.30
 encapsulation dot1Q 30
 ip address 10.7.30.253 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 30 ip 10.7.30.254
 standby 30 priority 150
 standby 30 preempt
!
ip dns server
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
!
````

- sur sw1 : 
````
Current configuration : 2103 bytes
!
! Last configuration change at 14:40:45 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw1
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

 - sur sw2 : 
````
Building configuration...

Current configuration : 2103 bytes
!
! Last configuration change at 10:41:25 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw2
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

- sur sw3 :
````
Current configuration : 2020 bytes
!
! Last configuration change at 10:33:49 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw3
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

- sur sw4:
````
Current configuration : 1926 bytes
!
! Last configuration change at 10:35:03 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw4
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

- sur sw5 :
````
Current configuration : 1725 bytes
!
! Last configuration change at 14:49:02 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw5
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

- sur sw6:
````
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw6
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

- sur sw7:
````
Current configuration : 1674 bytes
!
! Last configuration change at 10:10:29 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw7
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!
````

On peut ping ynov depuis PC4 : 
````
PC4> ping ynov.com
ynov.com resolved to 104.26.11.233
````


## Bonus : 

### A. ACL : 

Grâce à ce ping depuis le lan 20 : 
````
PC2> sh ip

NAME        : PC2[1]
IP/MASK     : 10.7.20.12/24
GATEWAY     : 10.7.20.254
DNS         : 1.1.1.1
MAC         : 00:50:79:66:68:01
LPORT       : 20050
RHOST:PORT  : 127.0.0.1:20051
MTU         : 1500

PC2> ping 10.7.30.67

84 bytes from 10.7.30.67 icmp_seq=1 ttl=63 time=18.839 ms
84 bytes from 10.7.30.67 icmp_seq=2 ttl=63 time=15.298 ms
84 bytes from 10.7.30.67 icmp_seq=3 ttl=63 time=19.557 ms
84 bytes from 10.7.30.67 icmp_seq=4 ttl=63 time=18.384 ms
^C
PC2> ping 10.7.30.11

*10.7.20.253 icmp_seq=1 ttl=255 time=5.516 ms (ICMP type:3, code:13, Communication administratively prohibited)
*10.7.20.253 icmp_seq=2 ttl=255 time=8.639 ms (ICMP type:3, code:13, Communication administratively prohibited)
*10.7.20.252 icmp_seq=3 ttl=255 time=10.163 ms (ICMP type:3, code:13, Communication administratively prohibited)
*10.7.20.253 icmp_seq=4 ttl=255 time=2.356 ms (ICMP type:3, code:13, Communication administratively prohibited)
````

le ping du 30.67 est permis mais pas sur le reste du réseau ! 

Voici ma ACL : 
````
R1#sh access-list 100
Extended IP access list 100
    10 permit icmp 10.7.10.0 0.0.0.255 host 10.7.30.67
    20 permit icmp host 10.7.30.67 10.7.10.0 0.0.0.255
    30 permit icmp 10.7.20.0 0.0.0.255 host 10.7.30.67
    40 permit icmp host 10.7.30.67 10.7.20.0 0.0.0.255
    50 permit icmp 10.7.10.0 0.0.0.255 host 10.7.10.254
    60 permit icmp 10.7.20.0 0.0.0.255 host 10.7.20.254
    70 permit icmp 10.7.20.0 0.0.0.255 10.7.20.0 0.0.0.255
    80 permit icmp 10.7.30.0 0.0.0.255 host 10.7.30.254
    90 permit icmp 10.7.30.0 0.0.0.255 10.7.30.0 0.0.0.255
````
### B. Spanning-tree

BPDU & Porfast mis en place : 
````
sw6#show spanning-tree interface e 0/1 detail
 Port 2 (Ethernet0/1) of VLAN0020 is designated forwarding
   Port path cost 100, Port priority 128, Port Identifier 128.2.
   Designated root has priority 32788, address aabb.cc00.0100
   Designated bridge has priority 32788, address aabb.cc00.0600
   Designated port id is 128.2, designated path cost 200
   Timers: message age 0, forward delay 0, hold 0
   Number of transitions to forwarding state: 1
   The port is in the portfast edge trunk mode
   Link type is point-to-point by default
   BPDU: sent 19278, received 0
````


### C. Observe and destroy then observe.

On vérifie la santé du lien LACP : 
````
sw1#show etherchannel detail
                Channel-group listing:
                ----------------------

Group: 1
----------
Group state = L2
Ports: 2   Maxports = 4
Port-channels: 1 Max Port-channels = 1
Protocol:    -
Minimum Links: 0


                Ports in the group:
                -------------------
Port: Et1/0
------------

Port state    = Up Mstr In-Bndl
Channel group = 1           Mode = On              Gcchange = -
Port-channel  = Po1         GC   =   -             Pseudo port-channel = Po1
Port index    = 0           Load = 0x00            Protocol =    -

Age of the port in the current state: 0d:07h:18m:22s
````

On check le lien HSRP : 
````
R1#sho standby br
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Fa1/0.10    10   150 P Active  local           unknown         10.7.10.254
Fa1/0.20    20   150 P Active  local           unknown         10.7.20.254
Fa1/0.30    30   100   Active  local           unknown         10.7.30.254
````

On vérifie l'état du STP : 
 - ici sur sw1 qui est root :
````
sw1#sh spanning-tree vlan 10-30

VLAN0010
  Spanning tree enabled protocol ieee
  Root ID    Priority    32778
             Address     aabb.cc00.0100
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32778  (priority 32768 sys-id-ext 10)
             Address     aabb.cc00.0100
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Desg FWD 100       128.1    P2p
Et2/0               Desg FWD 100       128.9    P2p
Et2/1               Desg FWD 100       128.10   P2p
Po1                 Desg FWD 56        128.65   P2p
````

 - sur sw3 :
````
sw3#sh spanning-tree vlan 10-30

VLAN0010
  Spanning tree enabled protocol ieee
  Root ID    Priority    32778
             Address     aabb.cc00.0100
             Cost        100
             Port        5 (Ethernet1/0)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32778  (priority 32768 sys-id-ext 10)
             Address     aabb.cc00.0300
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et1/0               Root FWD 100       128.5    P2p
Et1/1               Altn BLK 100       128.6    P2p
Et3/1               Desg FWD 100       128.14   P2p
Et3/2               Desg FWD 100       128.15   P2p
Et3/3               Desg FWD 100       128.16   P2p
````

Nous venons de couper le R1, voici ce que nous pouvons observer : 
````
R2#
*Mar  1 13:00:28.764: %HSRP-5-STATECHANGE: FastEthernet1/0.20 Grp 20 state Active -> Speak
R2#
*Mar  1 13:00:37.000: %HSRP-5-STATECHANGE: FastEthernet1/0.10 Grp 10 state Speak -> Standby
R2#
*Mar  1 13:00:38.760: %HSRP-5-STATECHANGE: FastEthernet1/0.20 Grp 20 state Speak -> Standby
R2#
*Mar  1 13:01:11.756: %HSRP-5-STATECHANGE: FastEthernet1/0.20 Grp 20 state Standby -> Active
R2#
*Mar  1 13:01:13.020: %HSRP-5-STATECHANGE: FastEthernet1/0.10 Grp 10 state Standby -> Active
````

Le R2 prend le relais.

Voici les [trames](tp7_stp_change.pcap) que nous avons pu voir s'échanger lors du shutdown de sw1, lien entre sw2 et sw4. 

### D. DHCP Helper

On vient de setup notre dhcp, voici la conf : 
````
[mmederic@localhost ~]$ sudo cat /etc/dhcp/dhcpd.conf
#
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page


option domain-name "tp7-domain.org";

option domain-name-servers 1.1.1.1;

default-lease-time 600;
max-lease-time 7200;

authoritative;

subnet 10.7.10.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.7.10.100 10.7.10.200;
        option routers 10.7.10.254;
}

subnet 10.7.20.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.7.20.100 10.7.20.200;
        option routers 10.7.20.254;
}

subnet 10.7.30.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.7.30.100 10.7.30.200;
        option routers 10.7.30.254;
}
````

Le service tourne bien : 
````
[mmederic@localhost ~]$ sudo systemctl status dhcpd | grep Active
     Active: active (running) since Tue 2023-12-12 10:03:56 CET; 5min ago
````

On utilise la commande pour activer le dhcp helper : 
````
R1(config)#interface fa 1/0
R1(config-if)#ip helper-address
R1(config-if)#ip helper-address 10.7.30.250
````

On change les ip grâce au dhcp : 
 - PC 5 : 
 ````
 PC5> sh ip

NAME        : PC5[1]
IP/MASK     : 10.7.30.11/24
GATEWAY     : 10.7.30.254
DNS         : 1.1.1.1
MAC         : 00:50:79:66:68:02
LPORT       : 20052
RHOST:PORT  : 127.0.0.1:20053
MTU         : 1500

PC5> ip dhcp -r
DDORA IP 10.7.30.100/24 GW 10.7.30.254
 ````
Malheuresement je n'y arrive pas pour la suite. 

J'ai vus qu'on pouvait paramétrer un DHCP pool pour permettre le changement des ips dans les différents Vlans. Mais je n'y arrive pas. 