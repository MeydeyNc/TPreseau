# TP-3 

## I. ARP

### I.1 

Utilisation du SSH afin d'optimiser le markdown. 
```` 
ssh mmederic@10.3.1.12

[mmederic@localhost ~]$ ip n s
10.3.1.15 dev enp0s8 lladdr 0a:00:27:00:00:0a DELAY
10.3.1.11 dev enp0s8 lladdr 08:00:27:bd:cc:a4 STALE

[mmederic@localhost ~]$ ping 10.3.1.11
PING 10.3.1.11 (10.3.1.11) 56(84) bytes of data.
64 bytes from 10.3.1.11: icmp_seq=1 ttl=64 time=0.687 ms
64 bytes from 10.3.1.11: icmp_seq=2 ttl=64 time=1.33 ms
64 bytes from 10.3.1.11: icmp_seq=3 ttl=64 time=3.48 ms
64 bytes from 10.3.1.11: icmp_seq=4 ttl=64 time=1.34 ms
64 bytes from 10.3.1.11: icmp_seq=5 ttl=64 time=1.30 ms
^C
--- 10.3.1.11 ping statistics ---

[mmederic@localhost ~]$ ip n s
10.3.1.15 dev enp0s8 lladdr 0a:00:27:00:00:0a REACHABLE
10.3.1.11 dev enp0s8 lladdr 08:00:27:bd:cc:a4 REACHABLE
````
Ici nous avons la table arp avant et après un ping. 

Nous savons que l'adresse MAC se compose de 6 bytes en Hexadecimal. Nous pouvons donc facilement retrouver les adresses MAC dans la table ARP. Ensuite il nous suffit de la confirmer avec un ``ip a`` sur l'autre machine. 
Ce qui nous donne : 
````
[mmederic@localhost ~]$ ip n s
10.3.1.12 dev enp0s8 lladdr 08:00:27:3c:ee:26 REACHABLE
10.3.1.15 dev enp0s8 lladdr 0a:00:27:00:00:0c REACHABLE
````
Sur la machine dite "Michel" en 10.3.1.11 
Puis : 
````
[mmederic@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:3c:ee:26 brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.12/24 brd 10.3.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe3c:ee26/64 scope link
       valid_lft forever preferred_lft forever
````
Sur la machine dite "Germain" en 10.3.1.12
Ici ce qui nous intéresse c'est l'adresse MAC : ``08:00:27:3c:ee:26`` que nous retrouvons bien au-dessus dans la table ARP, accompagnée de l'IP de Michel. 

### I.2

On vide la table ARP : 
````
[mmederic@localhost ~]$ sudo ip n flush all
[sudo] password for mmederic:
[mmederic@localhost ~]$ ip n s
10.3.1.15 dev enp0s8 lladdr 0a:00:27:00:00:0c DELAY
````
On voit bien la table vide, sans l'IP de notre cher Germain.

Voici ce que ça donne quand on lance un tcpdump : 
````
09:48:25.033224 IP 10.3.1.15.50650 > localhost.localdomain.ssh: Flags [.], ack 38192, win 8212, length 0
09:48:25.096077 IP localhost.localdomain.ssh > 10.3.1.15.50650: Flags [P.], seq 38192:38460, ack 1, win 501, length 268
````
Voici ce qu'on voit lorsqu'on fait un ARP : 
````
09:48:25.137036 IP 10.3.1.15.50650 > localhost.localdomain.ssh: Flags [.], ack 38460, win 8211, length 0
09:48:25.162887 ARP, Request who-has localhost.localdomain tell 10.3.1.11, length 46
09:48:25.162906 ARP, Reply localhost.localdomain is-at 08:00:27:3c:ee:26 (oui Unknown), length 28
09:48:25.163256 IP 10.3.1.11 > localhost.localdomain: ICMP echo request, id 2, seq 1, length 64
09:48:25.163298 IP localhost.localdomain > 10.3.1.11: ICMP echo reply, id 2, seq 1, length 64
````
Une trace d'un ping : 
````
09:48:26.150093 IP 10.3.1.15.50650 > localhost.localdomain.ssh: Flags [.], ack 42784, win 8212, length 0
09:48:26.192254 IP 10.3.1.11 > localhost.localdomain: ICMP echo request, id 2, seq 2, length 64
09:48:26.192290 IP localhost.localdomain > 10.3.1.11: ICMP echo reply, id 2, seq 2, length 64
````
Puis voir joint dans le même dossier, le tp2_arp.pcapng.

## II. Routage. 

### II.1. 

Nous venons d'activer le routage sur notre VM : Routeur : 
````
[mmederic@localhost ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8 enp0s9
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
[mmederic@localhost ~]$
````
Nous pouvons voir le masquerade activé, les deux interfaces bien connectées, bien en "public".

On vérifie que la route est créée : 
````
[mmederic@localhost ~]$ ip r s
10.3.1.0/24 dev enp0s8 proto kernel scope link src 10.3.1.11 metric 100
10.3.2.0/24 via 10.3.1.254 dev enp0s8 proto static metric 100
````
Nous tentons un ping pour vérifier que tout se passe bien : 
````
[mmederic@localhost ~]$ ping 10.3.2.12
PING 10.3.2.12 (10.3.2.12) 56(84) bytes of data.
64 bytes from 10.3.2.12: icmp_seq=1 ttl=63 time=0.763 ms
64 bytes from 10.3.2.12: icmp_seq=2 ttl=63 time=0.881 ms
64 bytes from 10.3.2.12: icmp_seq=3 ttl=63 time=0.938 ms
64 bytes from 10.3.2.12: icmp_seq=4 ttl=63 time=1.04 ms
64 bytes from 10.3.2.12: icmp_seq=5 ttl=63 time=1.81 ms
^C
--- 10.3.2.12 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4352ms
rtt min/avg/max/mdev = 0.763/1.085/1.810/0.372 ms
````

### II.2

Nous avons vidés les tables des 3 VMs. 
Puis nous avons ping de Michel à Germain. 
Une fois le ping effectué, voici ce que nous avons pu observer : 
Chez Michel (10.3.1.11) : 
````
[mmederic@localhost ~]$ ip n s
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:0c REACHABLE
10.3.1.254 dev enp0s8 lladdr 08:00:27:9b:41:5a REACHABLE
````
Chez Germain (10.3.2.12) : 
````
[mmederic@localhost ~]$ ip n s
10.3.2.1 dev enp0s8 lladdr 0a:00:27:00:00:3a DELAY
10.3.2.254 dev enp0s8 lladdr 08:00:27:cd:6c:70 REACHABLE
````
Chez le routeur : 
````
[mmederic@localhost ~]$ ip n s
10.3.2.12 dev enp0s9 lladdr 08:00:27:3c:ee:26 STALE
10.3.1.11 dev enp0s8 lladdr 08:00:27:95:56:51 REACHABLE
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:0c DELAY
````
Ce que je comprends ici, c'est que la 10.3.1.11 (Michel) qui a ping vers la 10.3.2.12 (Germain) est bien évidemment passée par le routeur (10.3.1.254). 
Cependant on nous dit que la connexion du routeur à Germain est "corrompue" ou du moins "périmée". 
Peut-être que c'est le cas car ce n'est pas la dernière IP utilisée afin d'effectuer le pong ? Mais la 10.3.1.11 ? De ce que je comprends les adresses dans la table ARP ont une péremption. Surtout si la route est statique. Et cette arrivée à péremption dépend de notre OS. 


Capture depuis Michel(John) :

| Ordre | Type Tram   | IP Source | MAC Source                         | IP Destination | MAC Destination                 |
| ----- | ----------- | --------- | ---------------------------------- | -------------- | ------------------------------- |
| 1     | Requête ARP | x         | Router       ``08:00:27:9b:41:5a`` | x              | Michel    ``08:00:27:95:56:51`` |
| 2     | Réponse ARP | x         | Michel(john) ``08:00:27:95:56:51`` | x              | Router    ``08:00:27:9b:41:5a`` |
| 3     | Requête ARP | x         | Michel(john) ``08:00:27:95:56:51`` | x              | Router    ``08:00:27:9b:41:5a`` |
| 4     | Réponse ARP | x         | Router       ``08:00:27:cd:6c:70`` | x              | Michel    ``08:00:27:95:56:51`` |
| 5     | Ping        | 10.3.1.11 | Michel(john) ``08:00:27:95:56:51`` | 10.3.2.12      | Router    ``08:00:27:9b:41:5a`` |
| 6     | Ping        | 10.3.2.12 | Router       ``08:00:27:9b:41:5a`` | 10.3.1.11      | Michel    ``08:00:27:95:56:51`` |
| 7     | Ping        | 10.3.1.11 | Michel(john) ``08:00:27:95:56:51`` | 10.3.2.12      | Router    ``08:00:27:9b:41:5a`` |
| 8     | Ping        | 10.3.2.12 | Router       ``08:00:27:9b:41:5a`` | 10.3.1.11      | Michel    ``08:00:27:95:56:51`` |

Capture depuis Germain(Marcel) :

| Ordre | Type Tram   | IP Source | MAC Source                           | IP Destination | MAC Destination                 |
| ----- | ----------- | --------- | ------------------------------------ | -------------- | ------------------------------- |
| 1     | Requête ARP | x         | Germain(marcel)``08:00:27:3c:ee:26`` | x              | Broadcast ``ff:ff:ff:ff:ff:ff`` |
| 2     | Réponse ARP | x         | Routeur        ``08:00:27:cd:6c:70`` | x              | Germain   ``08:00:27:3c:ee:26`` |
| 3     | Ping        | 10.3.1.12 | Germain(marcel)``08:00:27:3c:ee:26`` | 10.3.2.11      | Routeur   ``08:00:27:cd:6c:70`` |
| 4     | Ping        | 10.3.2.11 | Router         ``08:00:27:cd:6c:70`` | 10.3.1.12      | Germain   ``08:00:27:3c:ee:26`` |
| 5     | Requête ARP | x         | Router         ``08:00:27:cd:6c:70`` | x              | Germain   ``08:00:27:3c:ee:26`` |
| 6     | Réponse ARP | x         | Germain(marcel)``08:00:27:3c:ee:26`` | x              | Routeur   ``08:00:27:cd:6c:70`` |
| 7     | Ping        | 10.3.1.12 | Germain(marcel)``08:00:27:3c:ee:26`` | 10.3.2.11      | Routeur   ``08:00:27:cd:6c:70`` |
| 8     | Ping        | 10.3.2.12 | Router         ``08:00:27:cd:6c:70`` | 10.3.1.11      | Germain   ``08:00:27:3c:ee:26`` |

### II.3

Ne venons de configurer une adresse par défaut à nos VMs. 
Voici ce que ça donne : 
````
[mmederic@localhost ~]$ sudo ip route add default via 10.3.2.254 dev enp0s8
[sudo] password for mmederic:
[mmederic@localhost ~]$ ip r s
default via 10.3.2.254 dev enp0s8
10.3.1.0/24 via 10.3.2.254 dev enp0s8 proto static metric 100
10.3.2.0/24 dev enp0s8 proto kernel scope link src 10.3.2.12 metric 100
````

Nous allons maintenant configurer un DNS pour nos VMs : 
````
[mmederic@localhost ~]$ sudo nano /etc/resolv.conf
[mmederic@localhost ~]$ curl gitlab.com
[mmederic@localhost ~]$ dig gitlab.com

; <<>> DiG 9.16.23-RH <<>> gitlab.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 26070
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;gitlab.com.                    IN      A

;; ANSWER SECTION:
gitlab.com.             53      IN      A       172.65.251.78

;; Query time: 24 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Fri Oct 28 13:27:27 CEST 2022
;; MSG SIZE  rcvd: 55

[mmederic@localhost ~]$ sudo cat /etc/resolv.conf
# Generated by NetworkManager
search home
nameserver 1.1.1.1
````
Nous pouvons ping : 
````
[mmederic@localhost ~]$ [mmederic@localhost ~]$ ping google.com
PING google.com (142.250.178.142) 56(84) bytes of data.
64 bytes from par21s22-in-f14.1e100.net (142.250.178.142): icmp_seq=1 ttl=113 time=17.9 ms
64 bytes from par21s22-in-f14.1e100.net (142.250.178.142): icmp_seq=2 ttl=113 time=19.6 ms
64 bytes from par21s22-in-f14.1e100.net (142.250.178.142): icmp_seq=3 ttl=113 time=18.2 ms
64 bytes from par21s22-in-f14.1e100.net (142.250.178.142): icmp_seq=4 ttl=113 time=18.7 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3235ms
rtt min/avg/max/mdev = 17.946/18.619/19.640/0.643 ms
````

Voici ce que nous capturons dans notre analyse du ping vers 8.8.8.8 : 

| Ordre | Type Tram   | IP Source | MAC Source                           | IP Destination | MAC Destination                    |
| ----- | ----------- | --------- | ------------------------------------ | -------------- | ---------------------------------- |
| 1     | Ping        | 10.3.1.11 | Michel(john) ``08:00:27:95:56:51``   | 8.8.8.8        | DNS Google   ``08:00:27:9b:41:5a`` |
| 2     | Pong        | 8.8.8.8   | DNS Google   ``08:00:27:9b:41:5a``   | 10.3.1.11      | Michel(john) ``08:00:27:95:56:51`` |

## III. DHCP. 

### III.1.

Nous allons donc configurer un DHCP sur Michel (John) : 
Premièrement nous installons la possibilité de créer un serveur dhcp sur la VM. 
Nous téléchargeons donc ce dont nous avons besoin : ```` sudo dnf install dhcp-server -y ````

Puis direction la création d'un fichier primordial pour notre serveur dhcp : 
```` sudo nano /etc/dhcp/dhcpd.conf ````

Voici ce que nous pouvons y trouver : 
```` 
// DHCP Server Configuration file.
// see /usr/share/doc/dhcp-server/dhcpd.conf.example
// see dhcpd.conf(5) man page


default-lease-time 900;
max-lease-time 10800;

ddns-update-style none;

authoritative;

subnet 10.3.1.0 netmask 255.255.255.0 {
range 10.3.1.5 10.3.1.200;
option routers 10.3.1.1;
option subnet-mask 255.255.255.0;
option domain-name-servers 10.3.1.1;

}
````
Puis nous lancons notre nouveau dhcp : 
```` sudo systemctl enable --now dhcpd ````

Passons désormais à "Bob". 
Un petit ````ip a ```` pour mieux se situer : 
```` [mmederic@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8e:a5:d2 brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.5/24 brd 10.3.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 807sec preferred_lft 807sec
    inet6 fe80::a00:27ff:fe8e:a5d2/64 scope link
       valid_lft forever preferred_lft forever````
Le dhcp à l'air de fonctionner ! 
Nous avons une adresse ip pour bob qui vient d'être créé dans le même réseau que Michel(John).

Petite update : 
```` 
[mmederic@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8e:a5:d2 brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.20/24 brd 10.3.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 799sec preferred_lft 799sec
    inet6 fe80::a00:27ff:fe8e:a5d2/64 scope link
       valid_lft forever preferred_lft forever
````
 Nous venons de ré-actuliser le fichier coeur du serveur DHCP : 
 ```` 
default-lease-time 900;
max-lease-time 10800;

authoritative;

subnet 10.3.1.0 netmask 255.255.255.0 {
        range 10.3.1.20 10.3.1.200;
        option routers 10.3.1.254;
        option subnet-mask 255.255.255.0;
        option domain-name-servers 1.1.1.1, 8.8.8.8;

}
```` 
Pourquoi ? Car si une adresse IP statique se trouve dans la range de notre dhcp, cela peut (je suppose) créer des problèmes.
Nous avons donc modifié la "fourchette" d'adresses IP disponibles à la distribution par le DHCP.
Nous avons aussi ajouter des serveurs DNS potables et surtout utilisables. 

Nous allons maintenant passer à la suite du TP : 
Nous avons notre adresse IP que nous allons libérer pour en acquérir une autre grâce à notre dhcp. 
 
 Pour se faire : 

Afin de lâcher l'adresse actuelle : 

```` sudo dhclient -v -r enp0s8
Removed stale PID file
Internet Systems Consortium DHCP Client 4.4.2b1
Copyright 2004-2019 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp0s8/08:00:27:8e:a5:d2
Sending on   LPF/enp0s8/08:00:27:8e:a5:d2
Sending on   Socket/fallback
DHCPRELEASE of 10.3.1.21 on enp0s8 to 10.3.1.11 port 67 (xid=0x32183e00)````


Pour demande une nouvelle adresse IP : 

```` sudo dhclient -v enp0s8
Internet Systems Consortium DHCP Client 4.4.2b1
Copyright 2004-2019 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp0s8/08:00:27:8e:a5:d2
Sending on   LPF/enp0s8/08:00:27:8e:a5:d2
Sending on   Socket/fallback
DHCPDISCOVER on enp0s8 to 255.255.255.255 port 67 interval 4 (xid=0x71a09545)
DHCPOFFER of 10.3.1.21 from 10.3.1.11
DHCPREQUEST for 10.3.1.21 on enp0s8 to 255.255.255.255 port 67 (xid=0x71a09545)
DHCPACK of 10.3.1.21 from 10.3.1.11 (xid=0x71a09545)
bound to 10.3.1.21 -- renewal in 415 seconds.````

Et voilà : 
```` [mmederic@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8e:a5:d2 brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.20/24 brd 10.3.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 620sec preferred_lft 620sec
    inet 10.3.1.21/24 brd 10.3.1.255 scope global secondary dynamic enp0s8
       valid_lft 945sec preferred_lft 945sec
    inet6 fe80::a00:27ff:fe8e:a5d2/64 scope link
       valid_lft forever preferred_lft forever````
       
Bob peut ping sa passerelle : 
```` [mmederic@localhost ~]$ ping 10.3.1.254
PING 10.3.1.254 (10.3.1.254) 56(84) bytes of data.
64 bytes from 10.3.1.254: icmp_seq=1 ttl=64 time=0.460 ms
64 bytes from 10.3.1.254: icmp_seq=2 ttl=64 time=0.654 ms
64 bytes from 10.3.1.254: icmp_seq=3 ttl=64 time=0.560 ms
64 bytes from 10.3.1.254: icmp_seq=4 ttl=64 time=0.566 ms
^C
--- 10.3.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3122ms
rtt min/avg/max/mdev = 0.460/0.560/0.654/0.068 ms````

Bob a bien une adresse par défaut : 
````[mmederic@localhost ~]$ ip r s
default via 10.3.1.254 dev enp0s8 proto dhcp src 10.3.1.20 metric 100
10.3.1.0/24 dev enp0s8 proto kernel scope link src 10.3.1.20 metric 100````

La route fonctionne : 
````[mmederic@localhost ~]$ ping youtube.com
PING youtube.com (142.250.179.78) 56(84) bytes of data.
64 bytes from par21s19-in-f14.1e100.net (142.250.179.78): icmp_seq=1 ttl=114 time=20.1 ms
64 bytes from par21s19-in-f14.1e100.net (142.250.179.78): icmp_seq=2 ttl=114 time=20.2 ms
64 bytes from par21s19-in-f14.1e100.net (142.250.179.78): icmp_seq=3 ttl=114 time=16.0 ms
64 bytes from par21s19-in-f14.1e100.net (142.250.179.78): icmp_seq=4 ttl=114 time=18.8 ms
^C
--- youtube.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2997ms
rtt min/avg/max/mdev = 15.993/18.764/20.240/1.699 ms````

La commande ````dig```` fonctionne : 
````
[mmederic@localhost ~]$ dig youtube.com

; <<>> DiG 9.16.23-RH <<>> youtube.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 4150
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;youtube.com.                   IN      A

;; ANSWER SECTION:
youtube.com.            60      IN      A       216.58.209.238

;; Query time: 33 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Fri Nov 04 17:48:13 CET 2022
;; MSG SIZE  rcvd: 56
``

### III.2. 

