# Environnement Virtuel. 

![Yes Corruption.](/B2/TP2/images/Lolcat_in_folder.jpg)

### Compte-rendu : 

- Carte réseau node1.lan1 :
````
[mmederic@node1 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a1:ae:61 brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.11/24 brd 10.1.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea1:ae61/64 scope link
       valid_lft forever preferred_lft forever
````
- table route node1.lan1 :

````
[mmederic@node1 ~]$ ip n s
10.1.1.1 dev enp0s8 lladdr 0a:00:27:00:00:0d REACHABLE
10.1.1.254 dev enp0s8 lladdr 08:00:27:90:8b:db REACHABLE
[mmederic@node1 ~]$ ping 10.1.2.12
PING 10.1.2.12 (10.1.2.12) 56(84) bytes of data.
64 bytes from 10.1.2.12: icmp_seq=1 ttl=63 time=0.814 ms
64 bytes from 10.1.2.12: icmp_seq=2 ttl=63 time=0.973 ms
64 bytes from 10.1.2.12: icmp_seq=3 ttl=63 time=1.02 ms
64 bytes from 10.1.2.12: icmp_seq=4 ttl=63 time=1.18 ms
^C
--- 10.1.2.12 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3130ms
rtt min/avg/max/mdev = 0.814/0.996/1.178/0.129 ms

````
- traceroute sur node1.lan1 vers node2.lan2 :
````
[mmederic@node1 ~]$ traceroute 10.1.2.12
traceroute to 10.1.2.12 (10.1.2.12), 30 hops max, 60 byte packets
 1  10.1.1.254 (10.1.1.254)  0.788 ms  0.757 ms  0.735 ms
 2  10.1.2.12 (10.1.2.12)  0.708 ms !X  1.907 ms !X  1.841 ms !X
````

## II. Interlude accès internet. 

![Yes Welcome.](</B2/TP2/images/Sans titre.jpeg>)

Nous pouvons, depuis routeur, ping une IP publique : 
````
[mmederic@router ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=22.9 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=24.9 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=23.7 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=113 time=24.9 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 22.857/24.089/24.941/0.877 ms
````

Nous pouvons également résoudre les noms publics : 
````
[mmederic@router ~]$ ping google.com
PING google.com (172.217.18.206) 56(84) bytes of data.
64 bytes from ham02s14-in-f206.1e100.net (172.217.18.206): icmp_seq=1 ttl=113 time=26.6 ms
64 bytes from ham02s14-in-f206.1e100.net (172.217.18.206): icmp_seq=2 ttl=113 time=28.8 ms
64 bytes from ham02s14-in-f206.1e100.net (172.217.18.206): icmp_seq=3 ttl=113 time=26.7 ms
64 bytes from ham02s14-in-f206.1e100.net (172.217.18.206): icmp_seq=4 ttl=113 time=25.0 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 25.006/26.776/28.794/1.345 ms
````

Pour l'accès internet des node des différents Lan : 

- Voici l'ajout des route par défaut (ici node2.lan1):
````
[mmederic@node2 ~]$ sudo ip route add default via 10.1.1.254 dev enp0s8
[mmederic@node2 ~]$ ip r s
default via 10.1.1.254 dev enp0s8
10.1.1.0/24 dev enp0s8 proto kernel scope link src 10.1.1.12 metric 100
10.1.2.0/24 via 10.1.1.254 dev enp0s8 proto static metric 100
````

- Ainsi que la configuration du serveur DNS : 
````
[mmederic@node2 ~]$ cat /etc/resolv.conf
# Generated by NetworkManager
search lan1.tp1
nameserver 1.1.1.1
````

- Nous pouvons ping le Internet :

    - Nous sommes bien sur node2.lan1 :

````
[mmederic@node2 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ac:b9:0e brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.12/24 brd 10.1.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feac:b90e/64 scope link
       valid_lft forever preferred_lft forever
`````

- Nous pouvons ping une IP publique :

````
[mmederic@node2 ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=112 time=24.9 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=112 time=24.1 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=112 time=25.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=112 time=25.2 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3020ms
rtt min/avg/max/mdev = 24.147/24.862/25.225/0.432 ms
````
- Nous pouvons résoudre les noms publics :
````
[mmederic@node2 ~]$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=52 time=27.2 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=52 time=25.3 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=52 time=31.1 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=52 time=28.3 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 25.315/27.969/31.112/2.098 ms
````

## III. Services réseau : 

### 1. DHCP. 

J'ai pas lu la demande de rendu, mais voici l'historique de mes commandes (en tous cas les plus importantes) : 

 - On a bien changé l'IP du dhcp : 
````
[mmederic@dhcp1 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ac:b9:0e brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.253/24 brd 10.1.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feac:b90e/64 scope link
       valid_lft forever preferred_lft forever
````
 - L'historique de mes commandes (sorry) : 
````
   28  sudo dnf install dhcp-server -y
   29  sudo vim /etc/dhcp/dhcpd.conf
   30  cat /etc/dhcp/dhcpd.conf
   31  sudo cat /etc/dhcp/dhcpd.conf
   32  systemctl enable --now dhcpd
   33  sudo systemctl enable --now dhcpd
   34  clear
   35  sudo firewall-cmd --list-all
   36  sudo firewall-cmd --add-service=dhcp
   37  sudo firewall-cmd --runtime-to-permanent
   38  sudo firewall-cmd --list-all
````

![Alt text](/B2/TP2/images/cce53b95907bc6a657c0b5f6de78d757.jpg)

- Voici le fichier de configuration du serveur DHCP : 
````
[mmederic@dhcp1 ~]$ sudo cat /etc/dhcp/dhcpd.conf
# create new
# specify domain name
option domain-name "Meow-Internet";

#specify DNS server's hostname or IP address
option domain-name-servers 1.1.1.1;

#default lease time
default-lease-time 600;

#max lease time
max-lease-time 7200;

# this DHCP server to be declared valid
authoritative;

#specify network address and subnetmask
subnet 10.1.1.0 netmask 255.255.255.0 {
        #specify range of lease IP address
        range dynamic-bootp 10.1.1.100 10.1.1.200;
        #specify broadcast address
        option broadcast-address 10.1.1.255;
        #specify gateway
        option routers 10.1.1.254;
}
````

- le service actif : 
````
[mmederic@dhcp1 ~]$ sudo systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Fri 2023-10-20 10:57:20 CEST; 5min ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 1611 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 4604)
     Memory: 5.2M
        CPU: 11ms
     CGroup: /system.slice/dhcpd.service
             └─1611 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid

Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Config file: /etc/dhcp/dhcpd.conf
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Database file: /var/lib/dhcpd/dhcpd.leases
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: PID file: /var/run/dhcpd.pid
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Source compiled to use binary-leases
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Wrote 0 leases to leases file.
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Listening on LPF/enp0s8/08:00:27:ac:b9:0e/10.1.1.0/24
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Sending on   LPF/enp0s8/08:00:27:ac:b9:0e/10.1.1.0/24
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Sending on   Socket/fallback/fallback-net
Oct 20 10:57:20 dhcp1.lan1.tp1 dhcpd[1611]: Server starting service.
Oct 20 10:57:20 dhcp1.lan1.tp1 systemd[1]: Started DHCPv4 Server Daemon.
````

Sur node1.lan1 on change la configuration de l'IP de statique à dynamique : 
````
[mmederic@node1 ~]$ sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s8
[sudo] password for mmederic:
NAME=enp0s8
DEVICE=enp0s8

BOOTPROTO=dhcp
ONBOOT=yes
````

On check si ça marche : 
````
[mmederic@node1 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a1:ae:61 brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.100/24 brd 10.1.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 421sec preferred_lft 421sec
    inet6 fe80::a00:27ff:fea1:ae61/64 scope link
       valid_lft forever preferred_lft forever
````

**Notre ip a changée en 10.1.1.100**
_____________
Nous aurions pu utiliser les commandes suivantes : 
````
[mmederic@node1 ~]$ sudo dhclient -r enp0s8
````
- puis

````
[mmederic@node1 ~]$ sudo dhclient -v enp0s8
````
afin de récupérer une adresse par le dhcp. 

![Alt text](/B2/TP2/images/6wnsgah6tdx51.jpg)

____________

Nous pouvons toujours ping node1.lan2 : 
````
[mmederic@node1 ~]$ ping 10.1.2.11
PING 10.1.2.11 (10.1.2.11) 56(84) bytes of data.
64 bytes from 10.1.2.11: icmp_seq=1 ttl=63 time=0.909 ms
64 bytes from 10.1.2.11: icmp_seq=2 ttl=63 time=1.13 ms
64 bytes from 10.1.2.11: icmp_seq=3 ttl=63 time=1.19 ms
64 bytes from 10.1.2.11: icmp_seq=4 ttl=63 time=1.05 ms
^C
--- 10.1.2.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3051ms
rtt min/avg/max/mdev = 0.909/1.069/1.192/0.106 ms
````

On a bien récupéré l'IP de la gateway : 
````
[mmederic@dhcp1 dhcpd]$ ip r s
default via 10.1.1.254 dev enp0s8
10.1.1.0/24 dev enp0s8 proto kernel scope link src 10.1.1.253 metric 100
10.1.2.0/24 via 10.1.1.254 dev enp0s8 proto static metric 100
``````

### 2. Web web web 

*On a changé notre hostname entre temps évidemment.* 

On installe notre cher nginx : 
````
[mmederic@web2 ~]$ sudo dnf install nginx -y
[...]
Installed:
  nginx-1:1.20.1-14.el9_2.1.x86_64 nginx-core-1:1.20.1-14.el9_2.1.x86_64 nginx-filesystem-1:1.20.1-14.el9_2.1.noarch rocky-logos-httpd-90.14-1.el9.noarch

Complete!
````

Voici notre cher fichier de conf : 
````
[mmederic@web2 ~]$ sudo cat /etc/nginx/conf.d/site_nul.conf
server {
        listen 80;
        listen [::]:80;

        root /var/www/site_nul;
        index index.html index.htm;

        server_name site_nul.tp2 www.site_nul.tp2;

        location / {
                try_files $uri $uri/ =404;
        }

}
````

Notre service est actif : 
````
[mmederic@web2 ~]$ sudo systemctl status nginx
● nginx.service - The nginx HTTP and reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: disabled)
     Active: active (running) since Fri 2023-10-20 12:52:42 CEST; 2min 44s ago
     [...]
````

Notre firewall : 
````
[mmederic@web2 ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
````

Notre commande ss : 
````
[mmederic@web2 ~]$ ss -ltpu | grep http
tcp   LISTEN 0      511          0.0.0.0:http      0.0.0.0:*
tcp   LISTEN 0      511             [::]:http         [::]:*
````

Nous pouvons curl : 
````
Initi@DESKTOP-IM5I5BK MINGW64 ~ (master)
$ curl site_nul.tp2
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   195  100   195    0     0  32098      0 --:--:-- --:--:-- --:--:-- 39000<html>
        <head>

                <title>MeoWelcome to le site Nul</title>
        </head>
        <body>
                <h1>Bonsoir c'est pas fou ici</h1>

        <p><em>Je souhaiterai remercier avant tout mon chat.</em></p>
        </body>
</html>

````

![This is the end](/B2/TP2/images/just-started-learning-networking-and-made-this-v0-di6uv0968dtb1.webp)
*Yes it ends like this*