# TP-4

## I.1

Epic Games launcher - TCP : 

````
PS C:\Windows\system32> netstat -b

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.19.231:49685     20.199.120.182:https   ESTABLISHED
  WpnService
 [svchost.exe]
  TCP    10.33.19.231:52109     52.155.161.106:https   CLOSE_WAIT
 [SystemSettings.exe]
  TCP    10.33.19.231:52652     104.18.13.173:https    ESTABLISHED
 [EpicWebHelper.exe]
  TCP    10.33.19.231:52656     ec2-54-172-165-126:https  ESTABLISHED
 [EpicGamesLauncher.exe]
  TCP    10.33.19.231:52658     ec2-34-197-109-138:https  ESTABLISHED
 [EpicGamesLauncher.exe]
 ````
IP SRC : 10.33.19.231
IP DEST : 13.224.131.35

PORT SRC : 54922
PORT DEST : 80

[PCAP ](./tp4_EpicGameClient.pcapng)
 
 
 Gmail - TCP: 
 
 ````
 PS C:\Windows\system32> netstat -b

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.19.231:52109     52.155.161.106:https   CLOSE_WAIT
 [SystemSettings.exe]
  TCP    10.33.19.231:52249     a865a9e11bc2c0d65:https  ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52250     ec2-35-165-176-211:https  ESTABLISHED
 [firefox.exe]
 ````
IP SRC : 10.33.19.231
IP DEST : 142.250.179.101

PORT SRC : 52380
PORT DEST : 443
 
 
 [PCAP ](./tp4_Gmail.pcapng) 
 
 Hackmd.io - TCP: 
 
 ````
  PS C:\Windows\system32> netstat -b

Connexions actives
 
   TCP    10.33.19.231:52418     140:https              ESTABLISHED
 [firefox.exe]
 ````
IP SRC : 10.33.19.231
IP DEST : 75.2.77.152

PORT SRC : 52417
PORT DEST : 443

 [PCAP](./tp4_Hackmdio.pcapng) 
 
Microsoft TEAMS - TCP: 

````
PS C:\Windows\system32> netstat -b -n

Connexions actives

  TCP    10.33.19.231:52552     96.16.249.19:443       ESTABLISHED
 [SearchApp.exe]
  TCP    10.33.19.231:52554     52.113.194.132:443     ESTABLISHED
 [Teams.exe]
  TCP    10.33.19.231:52555     13.107.246.43:443      ESTABLISHED
 [SearchApp.exe]
  TCP    10.33.19.231:52556     204.79.197.222:443     ESTABLISHED
 [SearchApp.exe]
  TCP    10.33.19.231:52557     152.199.21.118:443     ESTABLISHED
 [SearchApp.exe]
  TCP    10.33.19.231:52558     204.79.197.222:443     ESTABLISHED
 [SearchApp.exe]
  TCP    10.33.19.231:52559     52.113.194.132:443     ESTABLISHED
 [Teams.exe]
  TCP    10.33.19.231:52560     52.112.120.193:443     ESTABLISHED
````
IP SRC : 10.33.19.231
IP DEST : 52.111.231.0

PORT SRC : 52589
PORT DEST : 443

[PCAP](./tp4_Teams.pcapng) 

Twitch.tv - TCP : 

````
PS C:\Windows\system32> netstat -b -n

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.19.231:52109     52.155.161.106:443     CLOSE_WAIT
 [SystemSettings.exe]
  TCP    10.33.19.231:52251     20.90.152.133:443      ESTABLISHED
  WpnService
 [svchost.exe]
  TCP    10.33.19.231:52550     20.54.232.160:443      TIME_WAIT
  TCP    10.33.19.231:52552     96.16.249.19:443       CLOSE_WAIT
 [SearchApp.exe]
  TCP    10.33.19.231:52557     152.199.21.118:443     CLOSE_WAIT
 [SearchApp.exe]
  TCP    10.33.19.231:52595     34.107.221.82:80       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52596     34.117.237.239:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52597     34.107.221.82:80       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52598     34.120.208.123:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52599     92.122.50.48:80        TIME_WAIT
  TCP    10.33.19.231:52600     34.213.140.56:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52602     216.58.214.67:80       TIME_WAIT
  TCP    10.33.19.231:52603     34.120.115.102:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52606     44.238.39.101:443      TIME_WAIT
  TCP    10.33.19.231:52608     44.238.39.101:443      TIME_WAIT
  TCP    10.33.19.231:52609     34.218.214.159:443     TIME_WAIT
  TCP    10.33.19.231:52610     34.214.139.174:443     TIME_WAIT
  TCP    10.33.19.231:52611     93.184.220.29:80       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52613     35.186.227.140:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52615     99.83.179.177:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52616     18.155.152.42:80       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52620     18.155.153.48:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52625     151.101.2.217:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52626     216.58.214.67:80       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52627     54.164.66.83:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52629     18.155.153.48:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52630     18.179.124.93:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52631     18.155.152.42:80       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52632     64.233.184.154:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52633     52.219.136.214:443     TIME_WAIT
  TCP    10.33.19.231:52635     216.58.209.234:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52638     20.54.232.160:443      ESTABLISHED
  CDPUserSvc_373f9
 [svchost.exe]
  TCP    10.33.19.231:52639     18.155.145.43:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52640     151.101.62.167:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52645     151.101.2.167:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52646     54.191.87.3:443        ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52648     199.232.174.167:443    ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52649     35.82.168.40:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52650     52.38.244.113:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52651     151.101.62.167:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52652     18.155.145.97:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52659     151.101.62.167:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52660     151.101.62.167:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52661     151.101.62.167:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52662     18.155.136.131:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52663     18.155.136.131:443     TIME_WAIT
  TCP    10.33.19.231:52666     18.155.136.131:443     TIME_WAIT
  TCP    10.33.19.231:52667     18.155.136.131:443     TIME_WAIT
  TCP    10.33.19.231:52669     18.155.153.81:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52670     18.155.153.81:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52671     18.155.153.81:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52672     18.155.153.81:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52674     18.155.153.97:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52676     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52677     18.155.153.5:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52678     35.82.19.90:443        ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52680     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52681     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52682     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52683     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52684     23.160.0.254:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52685     52.223.198.2:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52686     54.217.99.96:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52687     18.155.145.3:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52688     18.155.153.79:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52692     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52693     18.155.146.190:443     TIME_WAIT
  TCP    10.33.19.231:52696     18.155.145.3:443       TIME_WAIT
  TCP    10.33.19.231:52697     18.155.145.94:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52699     18.155.145.6:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52701     18.155.145.6:443       TIME_WAIT
  TCP    10.33.19.231:52702     52.223.195.77:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52706     18.155.145.48:443      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52707     23.160.0.0:443         ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52708     54.216.38.40:443       ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52709     18.155.138.228:80      ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52710     18.155.146.190:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52711     18.155.146.190:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52712     18.155.146.190:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52713     18.155.146.190:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52714     18.155.146.190:443     ESTABLISHED
 [firefox.exe]
  TCP    10.33.19.231:52715     18.155.146.190:443     ESTABLISHED
 [firefox.exe]
  TCP    127.0.0.1:52591        127.0.0.1:52592        ESTABLISHED
 [firefox.exe]
  TCP    127.0.0.1:52592        127.0.0.1:52591        ESTABLISHED
 [firefox.exe]
  TCP    127.0.0.1:52593        127.0.0.1:52594        ESTABLISHED
 [firefox.exe]
  TCP    127.0.0.1:52594        127.0.0.1:52593        ESTABLISHED
 [firefox.exe]
````
IP SRC : 52.223.195.77
IP DEST : 10.33.19.231

PORT SRC : 443
PORT DEST : 52702

[PCAP](./tp4_Twitch.pcapng) 

## II. 1. 

Nous avons utilisé git bash afin d'avoir toute la capture demandée : 
````
$ ssh mmederic@gaston
mmederic@gaston's password:
Last login: Thu Nov 10 10:02:12 2022 from 10.4.1.1
[mmederic@gaston ~]$
[mmederic@gaston ~]$
[mmederic@gaston ~]$ exit
logout
Connection to gaston closed.
````
PCAP : 

Repérer la connexion ssh depuis la VM : 

````
[mmederic@gaston ~]$ ss
tcp      ESTAB    0         52                              10.4.1.11:ssh               10.4.1.1:58207
````

J'utilise la commande pour repérer la connexion depuis ma machine : 

````
PS C:\Users\Initi> netstat -n -q
TCP    10.4.1.1:58253         10.4.1.11:22           ESTABLISHED
````

[capture du 3-way handshake](./tp4_ssh.pcapng)

## II. 2.

Routeur actif. 
Route par défaut activée sur gaston. 

## III. 2. 

 Voici le cat du premier fichier du named.conf : 

````
[mmederic@dns ~]$ [mmederic@dns ~]$ sudo cat /etc/named.conf
[sudo] password for mmederic:
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
        listen-on port 53 { 127.0.0.1; any; };
        listen-on-v6 port 53 { ::1; };
        directory       "/var/named";
        dump-file       "/var/named/data/cache_dump.db";
        statistics-file "/var/named/data/named_stats.txt";
        memstatistics-file "/var/named/data/named_mem_stats.txt";
        secroots-file   "/var/named/data/named.secroots";
        recursing-file  "/var/named/data/named.recursing";
        allow-query     { localhost; any; };
        allow-query-cache {localhost; any; };

        /*
         - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
         - If you are building a RECURSIVE (caching) DNS server, you need to enable
           recursion.
         - If your recursive DNS server has a public IP address, you MUST enable access
           control to limit queries to your legitimate users. Failing to do so will
           cause your server to become part of large scale DNS amplification
           attacks. Implementing BCP38 within your network would greatly
           reduce such attack surface
        */
        recursion yes;

        dnssec-validation yes;

        managed-keys-directory "/var/named/dynamic";
        geoip-directory "/usr/share/GeoIP";

        pid-file "/run/named/named.pid";
        session-keyfile "/run/named/session.key";

        /* https://fedoraproject.org/wiki/Changes/CryptoPolicy */
        include "/etc/crypto-policies/back-ends/bind.config";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "." IN {
        type hint;
        file "named.ca";
};

zone "tp4.b1" IN {
        type master;
        file "tp4.b1.db";
        allow-update {none; };
        allow-query {any; };
};

zone "1.4.10.in-addr.arpa" IN {
        type master;
        file "tp4.b1.rev";
        allow-update { none; };
        allow-query { any; };
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";
````

 Le cat du fichier zone : 

````
[mmederic@dns ~]$ [mmederic@dns ~]$ sudo cat /var/named/tp4.b1.db


$TTL 86400
@ IN SOA dns-server.tp4.b1. admin.tp4.b1. (
        2019061800 ;Serial
        3600 ;Refresh
        1800 ;Retry
        604800 ;Expire
        86400 ;Minimum TTL
)

@ IN NS dns-server.tp4.b1.

dns-server IN A 10.4.1.201
gatson      IN A 10.4.1.11
````
 Le cat du fichier zone inverse : 

````
[mmederic@dns ~]$ sudo cat /var/named/tp4.b1.rev


$TTL 86400
@ IN SOA dns-server.tp4.b1. admin.tp4.b1. (
        2019061800 ;Serial
        3600 ;Refresh
        1800 ;Retry
        604800 ;Expire
        86400 ;Minimum TTL
)

@ IN NS dns-server.tp4.b1.

201 IN PTR dns-server.tp4.b1.
11 IN PTR node1.tp4.b1.
````
 Voici le systemctl status : 

````
[mmederic@dns ~]$ sudo systemctl status named
● named.service - Berkeley Internet Name Domain (DNS)
     Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; vendor preset: disabled)
     Active: active (running) since Thu 2022-11-10 11:45:16 CET; 25s ago
   Main PID: 4057 (named)
      Tasks: 6 (limit: 4800)
     Memory: 22.8M
        CPU: 81ms
     CGroup: /system.slice/named.service
             └─4057 /usr/sbin/named -u named -c /etc/named.conf

Nov 10 11:45:16 dns named[4057]: network unreachable resolving './NS/IN': 2001:dc3::35#53
Nov 10 11:45:16 dns named[4057]: zone tp4.b1/IN: loaded serial 2019061800
Nov 10 11:45:16 dns named[4057]: all zones loaded
Nov 10 11:45:16 dns named[4057]: running
Nov 10 11:45:16 dns systemd[1]: Started Berkeley Internet Name Domain (DNS).
Nov 10 11:45:16 dns named[4057]: network unreachable resolving './DNSKEY/IN': 2001:500:a8::e#53
Nov 10 11:45:16 dns named[4057]: network unreachable resolving './DNSKEY/IN': 2001:7fd::1#53
Nov 10 11:45:16 dns named[4057]: network unreachable resolving './DNSKEY/IN': 2001:500:2d::d#53
Nov 10 11:45:16 dns named[4057]: managed-keys-zone: Initializing automatic trust anchor management for zone '.'; DNS>
Nov 10 11:45:16 dns named[4057]: resolver priming query complete
````
 Le sudo ss pour vérifier : 

````
[mmederic@dns ~]$ sudo ss -ltunp
Netid   State    Recv-Q   Send-Q     Local Address:Port      Peer Address:Port   Process
udp     UNCONN   0        0             10.4.1.201:53             0.0.0.0:*       users:(("named",pid=4057,fd=31))
udp     UNCONN   0        0             10.4.1.201:53             0.0.0.0:*       users:(("named",pid=4057,fd=30))
udp     UNCONN   0        0              127.0.0.1:53             0.0.0.0:*       users:(("named",pid=4057,fd=25))
udp     UNCONN   0        0              127.0.0.1:53             0.0.0.0:*       users:(("named",pid=4057,fd=24))
udp     UNCONN   0        0              127.0.0.1:323            0.0.0.0:*       users:(("chronyd",pid=663,fd=5))
udp     UNCONN   0        0                  [::1]:53                [::]:*       users:(("named",pid=4057,fd=34))
udp     UNCONN   0        0                  [::1]:53                [::]:*       users:(("named",pid=4057,fd=35))
udp     UNCONN   0        0                  [::1]:323               [::]:*       users:(("chronyd",pid=663,fd=6))
tcp     LISTEN   0        10            10.4.1.201:53             0.0.0.0:*       users:(("named",pid=4057,fd=33))
tcp     LISTEN   0        10            10.4.1.201:53             0.0.0.0:*       users:(("named",pid=4057,fd=32))
tcp     LISTEN   0        10             127.0.0.1:53             0.0.0.0:*       users:(("named",pid=4057,fd=28))
tcp     LISTEN   0        10             127.0.0.1:53             0.0.0.0:*       users:(("named",pid=4057,fd=26))
tcp     LISTEN   0        128              0.0.0.0:22             0.0.0.0:*       users:(("sshd",pid=720,fd=3))
tcp     LISTEN   0        4096           127.0.0.1:953            0.0.0.0:*       users:(("named",pid=4057,fd=23))
tcp     LISTEN   0        10                 [::1]:53                [::]:*       users:(("named",pid=4057,fd=36))
tcp     LISTEN   0        10                 [::1]:53                [::]:*       users:(("named",pid=4057,fd=37))
tcp     LISTEN   0        128                 [::]:22                [::]:*       users:(("sshd",pid=720,fd=4))
tcp     LISTEN   0        4096               [::1]:953               [::]:*       users:(("named",pid=4057,fd=38))
````

## III. 3. 

Nous pouvons ping ``google.com`` avec node1 (gaston) :

````
[mmederic@gaston ~]$ [mmederic@gaston ~]$ ping google.com
PING google.com (216.58.214.78) 56(84) bytes of data.
64 bytes from fra15s10-in-f78.1e100.net (216.58.214.78): icmp_seq=1 ttl=112 time=21.5 ms
64 bytes from fra15s10-in-f14.1e100.net (216.58.214.78): icmp_seq=2 ttl=112 time=23.0 ms
64 bytes from fra15s10-in-f78.1e100.net (216.58.214.78): icmp_seq=3 ttl=112 time=23.2 ms
64 bytes from fra15s10-in-f14.1e100.net (216.58.214.78): icmp_seq=4 ttl=112 time=22.2 ms
64 bytes from fra15s10-in-f14.1e100.net (216.58.214.78): icmp_seq=5 ttl=112 time=22.5 ms
^C
--- google.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4973ms
rtt min/avg/max/mdev = 21.453/22.474/23.236/0.625 ms
````

On effectue un nslookup : 

````
PS C:\Windows\system32> nslookup gaston.tp4.b1 10.4.1.201
Serveur :   dns-server.tp4.b1
Address:  10.4.1.201

Nom :    gaston.tp4.b1
Address:  10.4.1.11
````

[capture requête DNS](./tp4_Resolve_DNS.pcapng)

