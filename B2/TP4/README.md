# Router-On-A-Stick

On commence par adresser toutes les ips statiques : 
 - PC1 :
````
PC1> ip 10.1.10.1 255.255.255.0
Checking for duplicate address...
PC1 : 10.1.10.1 255.255.255.0

PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.10.1/24
GATEWAY     : 255.255.255.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20009
RHOST:PORT  : 127.0.0.1:20010
MTU         : 1500
````
 - PC2 :
 ````
PC2> ip 10.1.10.2
Checking for duplicate address...
PC2 : 10.1.10.2 255.255.255.0

PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.10.2/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 20011
RHOST:PORT  : 127.0.0.1:20012
MTU         : 1500
 ````
 - adm1 :
````
adm1> ip 10.1.20.1
Checking for duplicate address...
adm1 : 10.1.20.1 255.255.255.0

adm1> show ip

NAME        : adm1[1]
IP/MASK     : 10.1.20.1/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:02
LPORT       : 20007
RHOST:PORT  : 127.0.0.1:20008
MTU         : 1500
```` 

On setup nos VLANs : 
````
IOU1#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- 
10   clients                          active
20   admins                           active
30   servers                          active
[...]
````

Tout s'est bien passé dans l'attribution des VLANs : 
````
IOU1#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- 
10   clients                          active    Et0/1, Et0/2
20   admins                           active    Et1/1
30   servers                          active    Et2/1
[...]
````

Nous venons d'ajouter les différents VLANs sur le switch : 
````
IOU1#show interface trunk

Port        Mode             Encapsulation  Status        Native vlan
Et0/0       on               802.1q         trunking      1

Port        Vlans allowed on trunk
Et0/0       1-4094

Port        Vlans allowed and active in management domain
Et0/0       1,10,20,30

Port        Vlans in spanning tree forwarding state and not pruned
Et0/0       1,10,20,30
````

Nous configurons nos adresses IP sur les interfaces du router : 
````
R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  up                    up
FastEthernet0/0.10         10.1.10.254     YES manual up                    up
FastEthernet0/0.20         10.1.20.254     YES manual up                    up
FastEthernet0/0.30         10.1.30.254     YES manual up                    up
FastEthernet0/1            unassigned      YES unset  administratively down down
FastEthernet1/0            unassigned      YES unset  administratively down down
FastEthernet2/0            unassigned      YES unset  administratively down down
````

On test les différents ping : 
- pc1 :
````
PC1> ping 10.1.10.254

10.1.10.254 icmp_seq=1 timeout
84 bytes from 10.1.10.254 icmp_seq=2 ttl=255 time=10.543 ms
84 bytes from 10.1.10.254 icmp_seq=3 ttl=255 time=8.813 ms
84 bytes from 10.1.10.254 icmp_seq=4 ttl=255 time=3.644 ms
84 bytes from 10.1.10.254 icmp_seq=5 ttl=255 time=1.190 ms
````

- pc2 :
````
PC2> ping 10.1.10.254

84 bytes from 10.1.10.254 icmp_seq=1 ttl=255 time=3.283 ms
84 bytes from 10.1.10.254 icmp_seq=2 ttl=255 time=9.464 ms
84 bytes from 10.1.10.254 icmp_seq=3 ttl=255 time=9.710 ms
84 bytes from 10.1.10.254 icmp_seq=4 ttl=255 time=11.880 ms
````

- adm1 :
````
adm1> ping 10.1.20.254

84 bytes from 10.1.20.254 icmp_seq=1 ttl=255 time=7.249 ms
84 bytes from 10.1.20.254 icmp_seq=2 ttl=255 time=3.261 ms
84 bytes from 10.1.20.254 icmp_seq=3 ttl=255 time=1.299 ms
84 bytes from 10.1.20.254 icmp_seq=4 ttl=255 time=9.283 ms
````

- web1:
````
[mmederic@web1 ~]$ ping 10.1.30.254
PING 10.1.30.254 (10.1.30.254) 56(84) bytes of data.
64 bytes from 10.1.30.254: icmp_seq=1 ttl=255 time=27.8 ms
64 bytes from 10.1.30.254: icmp_seq=2 ttl=255 time=5.54 ms
64 bytes from 10.1.30.254: icmp_seq=3 ttl=255 time=8.51 ms
64 bytes from 10.1.30.254: icmp_seq=4 ttl=255 time=2.07 ms
````

Les différents réseaux peuvent se ping : 
- vlan 10 :
````
pc1> ping 10.1.30.1

84 bytes from 10.1.30.1 icmp_seq=1 ttl=63 time=19.722 ms
84 bytes from 10.1.30.1 icmp_seq=2 ttl=63 time=20.929 ms
84 bytes from 10.1.30.1 icmp_seq=3 ttl=63 time=16.752 ms
````

- vlan 20 :
````
adm1> ping 10.1.30.1

84 bytes from 10.1.30.1 icmp_seq=1 ttl=63 time=12.882 ms
84 bytes from 10.1.30.1 icmp_seq=2 ttl=63 time=16.578 ms
84 bytes from 10.1.30.1 icmp_seq=3 ttl=63 time=11.573 ms
84 bytes from 10.1.30.1 icmp_seq=4 ttl=63 time=18.740 ms
````

- vlan 30 :
````
[mmederic@web1 ~]$ ping 10.1.10.2
PING 10.1.10.2 (10.1.10.2) 56(84) bytes of data.
64 bytes from 10.1.10.2: icmp_seq=1 ttl=63 time=17.4 ms
64 bytes from 10.1.10.2: icmp_seq=2 ttl=63 time=14.2 ms
64 bytes from 10.1.10.2: icmp_seq=3 ttl=63 time=14.8 ms
64 bytes from 10.1.10.2: icmp_seq=4 ttl=63 time=17.4 ms
````

# II. NAT.

On vient d'intégrer un cloud dans la topo, et configurer le router pour récup une ip en dynamique : 
````
R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES NVRAM  up                    up
FastEthernet0/0.10         10.1.10.254     YES NVRAM  up                    up
FastEthernet0/0.20         10.1.20.254     YES NVRAM  up                    up
FastEthernet0/0.30         10.1.30.254     YES NVRAM  up                    up
FastEthernet0/1            unassigned      YES DHCP   up                    up
````

Configuration du Cloud ayant échoué sur windows, on a direct pris un NAT pour avoir l'accès internet. On se rappel de la capture avec pleins de TCP mais surtout HTTP chelous. 

On peut maintenant ping : 
````
R1#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 20/22/28 ms
````
Alors , comme nous avons vus ensemble : Mon pc est ensorcelé visiblement. 

J'ai internet : 
- la VM
````
[mmederic@web1 ~]$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=2 ttl=54 time=30.0 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=54 time=29.5 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=54 time=24.9 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=54 time=28.2 ms
````

- pc1 :
````
pc1> ping  toto.com
toto.com resolved to 52.199.8.8

toto.com icmp_seq=1 timeout
````
Mais on en peut pas ping depuis les vpcs. 

# III. Add a building. 

Les runnings config : 
- sw1 : 
````
sw1#sho running-config
Building configuration...

Current configuration : 1604 bytes
!
! Last configuration change at 20:59:13 UTC Mon Nov 6 2023
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
- sw2 : 
````
sw3#sho running-config
Building configuration...

Current configuration : 1635 bytes
!
! Last configuration change at 05:45:57 UTC Tue Nov 7 2023
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

- sw3 : 
````
sw3#sho running-config
Building configuration...

Current configuration : 1635 bytes
!
! Last configuration change at 05:45:57 UTC Tue Nov 7 2023
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

- R1 : 
````
R1#show running-config
Building configuration...

Current configuration : 1599 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
boot-start-marker
boot-end-marker
!
!
no aaa new-model
memory-size iomem 5
no ip icmp rate-limit unreachable
ip cef
!
no ip domain lookup
!
multilink bundle-name authenticated
!
archive
 log config
  hidekeys
!
ip tcp synwait-time 5
!
interface FastEthernet0/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 speed 100
 full-duplex
!
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.1.10.254 255.255.255.0
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.1.20.254 255.255.255.0
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet0/0.30
 encapsulation dot1Q 30
 ip address 10.1.30.254 255.255.255.0
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet0/1
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0
 ip address dhcp
 shutdown
 duplex auto
 speed auto
!
interface FastEthernet2/0
 no ip address
 shutdown
 duplex auto
 speed auto
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
ip nat inside source list 1 interface FastEthernet0/1 overload
!
access-list 1 permit any
no cdp log mismatch duplex
!
control-plane
!
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line vty 0 4
 login
!
!
end
````

*j'ai volontairement réduit les "!" pour que ça prenne moins de place.*


Nous venons de mettre en place notre beau serveur dhcp : 
````
sudo cat /etc/dhcp/dhcpd.conf
[sudo] password for mmederic:
#
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
#
option domain-name "GNS-server-is-back";

option domain-name-servers 1.1.1.1;

default-lease-time 600;

max-lease-time 7200;

authoritative;

subnet 10.1.10.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.1.10.3 10.1.10.10;
        option routers 10.1.10.254;

}
````

On fait les vérifs : 
- PC3 :
````
PC3> ip dhcp -r
DDORA IP 10.1.10.3/24 GW 10.1.10.254

PC3> ping 1.1.1.1

1.1.1.1 icmp_seq=1 timeout
1.1.1.1 icmp_seq=2 timeout
^C
PC3> ping google.com
google.com resolved to 142.250.178.142

google.com icmp_seq=1 timeout
^C
PC3> ping 10.1.30.1

84 bytes from 10.1.30.1 icmp_seq=1 ttl=63 time=23.030 ms
84 bytes from 10.1.30.1 icmp_seq=2 ttl=63 time=13.298 ms
84 bytes from 10.1.30.1 icmp_seq=3 ttl=63 time=19.880 ms
^C
PC3> ping ynov.com
ynov.com resolved to 104.26.11.233
````

- PC4 :
````
PC4> ip dhcp -r
DDORA IP 10.1.10.4/24 GW 10.1.10.254

PC4> ping 10.1.30.1

84 bytes from 10.1.30.1 icmp_seq=1 ttl=63 time=21.439 ms
84 bytes from 10.1.30.1 icmp_seq=2 ttl=63 time=16.054 ms
84 bytes from 10.1.30.1 icmp_seq=3 ttl=63 time=12.233 ms
84 bytes from 10.1.30.1 icmp_seq=4 ttl=63 time=15.785 ms
^C
PC4> ping 1.1.1.1

1.1.1.1 icmp_seq=1 timeout
^C
PC4> ping ynov.com
ynov.com resolved to 172.67.74.226
````

- PC5 :
````
PC5> ip dhcp -r
DDORA IP 10.1.10.5/24 GW 10.1.10.254

PC5> ping google.com
google.com resolved to 142.250.75.238

^C
PC5> ping 10.1.30.1

84 bytes from 10.1.30.1 icmp_seq=1 ttl=63 time=33.649 ms
84 bytes from 10.1.30.1 icmp_seq=2 ttl=63 time=18.222 ms
84 bytes from 10.1.30.1 icmp_seq=3 ttl=63 time=14.876 ms
84 bytes from 10.1.30.1 icmp_seq=4 ttl=63 time=17.869 ms
^C
PC5> ping ynov.com
ynov.com resolved to 172.67.74.226
````

C'était bieng. Merci. 