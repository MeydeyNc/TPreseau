# TP 1 Maîtrise réseau du Poste.

## I. Basics. 

![Alt text](so-basic-5b9ad1.jpg)

On commence par nos adresses MAC et IP Wifi. 
On utilise donc la commande : ``ipconfig /all`` sur windows donnant ceci : 
````
Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Dual Band Wireless-AC 8265
   Adresse physique . . . . . . . . . . . : 00-21-6B-E9-AF-BB
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::e17c:3f50:39d8:f2f3%22(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.76.174(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : jeudi 12 octobre 2023 13:33:04
   Bail expirant. . . . . . . . . . . . . : vendredi 13 octobre 2023 13:31:11
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
   IAID DHCPv6 . . . . . . . . . . . : 184557931
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2A-E0-47-03-98-FA-9B-16-E3-71
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
````

Dedans nous avons, 
notre adresse MAC : 
```
 Adresse physique . . . . . . . . . . . : 00-21-6B-E9-AF-BB
```

notre adresse IP : 
```
Adresse IPv4. . . . . . . . . . . . . .: 10.33.76.174(préféré)
```

notre masque de sous-réseau en notation décimal & CIDR: 
```
Masque de sous-réseau. . . . . . . . . : 255.255.240.0
En CIDR  . . . . . . . . . . . . . . . : 10.33.76.174/20
```

 Grâce à un joli outil le Internet nous avons l'adresse de réseau du LAN : 
 - ```10.33.64.0```

 L'adresse de broadcast du LAN : 
 - ```10.33.79.255```

 Le nombre d'adresses IP disponibles dans le réseau :
 - ```4094```


Notre hostname : 
```
PS C:\Users\Initi> hostname
DESKTOP-IM5I5BK
```

Ip passerelle réseau : 
``````
PS C:\Users\Initi> ipconfig /all | Select-String "Passerelle"

   Passerelle par défaut. . . . . . . . . : 10.33.79.254
``````

Adresse MAC de la passerelle du réseau : 
``````
PS C:\Users\Initi> arp -a | Select-String "10.33.79.254"

  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
``````

L'adresse IP du serveur DHCP :
``````
PS C:\Users\Initi> ipconfig /all | Select-String "Serveur DHCP"

   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
``````

L'adresse IP du serveur DNS : 
``````
PS C:\Users\Initi> Get-NetIPConfiguration -InterfaceIndex 22 | findstr "DNS"
DNSServer            : 8.8.8.8
                       1.1.1.1
``````

____________
![Alt text](vxnyl.jpg)

**J'ai changé d'ordinateur entre temps, je suis actuellement sur une tour en ethernet.** 

 
____________

 ipconfig sur la tour en ethernet :  
   ``````
   PS C:\Users\MedeWiKK> ipconfig /all

   Carte Ethernet Ethernet :

   Suffixe DNS propre à la connexion. . . : home
   Description. . . . . . . . . . . . . . : Realtek PCIe GBE Family Controller
   Adresse physique . . . . . . . . . . . : 34-97-F6-29-ED-A1
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6. . . . . . . . . . . . . .: 2a01:cb19:19d:e900:94a6:9b45:128f:e453(préféré)
   Adresse IPv6 temporaire . . . . . . . .: 2a01:cb19:19d:e900:8c71:acd0:858f:1855(préféré)
   Adresse IPv6 de liaison locale. . . . .: fe80::2e83:9598:fc36:5b63%3(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.1.13(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Bail obtenu. . . . . . . . . . . . . . : mercredi 18 octobre 2023 17:29:02
   Bail expirant. . . . . . . . . . . . . : jeudi 19 octobre 2023 17:28:59
   Passerelle par défaut. . . . . . . . . : fe80::46a6:1eff:fe68:ff6%3
                                       192.168.1.1
   Serveur DHCP . . . . . . . . . . . . . : 192.168.1.1
   ``````
____________


Avec la table de routage, on détermine notre route par défaut : 
``````
PS C:\Users\MedeWiKK> arp -a

Interface : 192.168.1.13 --- 0x3
  Adresse Internet      Adresse physique      Type
  192.168.1.1           44-a6-1e-68-0f-f6     dynamique
``````

## II. Go Further *& BEYOND*. 
![Fuzz Lightyear](5f5d4cfbcbcd9.jpeg)

On ajoute un host sur windows, pas aussi simple que Linux, on doit aller chercher le ficher host : *"C:\Windows\System32\drivers\etc\hosts"* et l'éditer avec un éditeur de texte.

Ce qui nous donne ceci lors du ping a postériori : 
``````
PS C:\Users\MedeWiKK> ping b2.hello.meow

Envoi d’une requête 'ping' sur b2.hello.meow [1.1.1.1] avec 32 octets de données :
Réponse de 1.1.1.1 : octets=32 temps<1ms TTL=64
Réponse de 1.1.1.1 : octets=32 temps<1ms TTL=64
Réponse de 1.1.1.1 : octets=32 temps<1ms TTL=64
Réponse de 1.1.1.1 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 1.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
``````

Adresse IP du serveur youtube : 
``````
PS C:\Users\MedeWiKK> netstat -af -p TCP | Select-String "192.168.1.13"
[...]
TCP    192.168.1.13:50351     207-182-151-170.xlhdns.com:https  ESTABLISHED
``````

Port du serveur auquel je suis connecté (443) : 
````
PS C:\Users\MedeWiKK> netstat -anf -p TCP | Select-String "192.168.1.13"
[...]
TCP    192.168.1.13:50351     207.182.151.170:443    ESTABLISHED
````

Port que mon PC a ouvert en local (50351) : 
````
PS C:\Users\MedeWiKK> netstat -anf -p TCP | Select-String "192.168.1.13"
[...]
TCP    192.168.1.13:50351     207.182.151.170:443    ESTABLISHED
````
______
**Retour sur mon ordinateur portable en wifi.**
_____


On utilise un nslookup : 
````
PS C:\Users\Initi> nslookup ynov.com
Serveur :   UnKnown
Address:  192.168.43.1

Réponse ne faisant pas autorité :
Nom :    ynov.com
Addresses:  2606:4700:20::681a:ae9
          2606:4700:20::ac43:4ae2
          2606:4700:20::681a:be9
          172.67.74.226
          104.26.10.233
          104.26.11.233
````

Nom de domaine de 174.43.238.89 :
````
PS C:\Users\Initi> nslookup 174.43.238.89
Serveur :   UnKnown
Address:  192.168.43.1

Nom :    89.sub-174-43-238.myvzw.com
Address:  174.43.238.89
````

On passe par 8 machines avant d'arriver à la machine demandée :
````
PS C:\Users\Initi> tracert www.ynov.com

Détermination de l’itinéraire vers www.ynov.com [104.26.11.233]
avec un maximum de 30 sauts :

  1     2 ms     1 ms     1 ms  10.33.79.254
  2     4 ms     2 ms     3 ms  145.117.7.195.rev.sfr.net [195.7.117.145]
  3     4 ms     3 ms     4 ms  237.195.79.86.rev.sfr.net [86.79.195.237]
  4     5 ms     5 ms     9 ms  196.224.65.86.rev.sfr.net [86.65.224.196]
  5    13 ms    14 ms    13 ms  12.148.6.194.rev.sfr.net [194.6.148.12]
  6    12 ms    12 ms    13 ms  12.148.6.194.rev.sfr.net [194.6.148.12]
  7    16 ms    12 ms    12 ms  141.101.67.48
  8    12 ms    13 ms    12 ms  172.71.124.4
  9    12 ms    12 ms    12 ms  104.26.11.233
````

IP publique ynov, 2ème IP donnée ci-dessous: 
````
PS C:\Users\Initi> nslookup myip.opendns.com resolver1.opendns.com
Serveur :   dns.opendns.com
Address:  208.67.222.222

Réponse ne faisant pas autorité :
Nom :    myip.opendns.com
Address:  195.7.117.146
````

On scan le réseau pour avoir les machines présentes : 
````
PS C:\Users\Initi> arp -a
[...]
Interface : 10.33.76.174 --- 0x16
  Adresse Internet      Adresse physique      Type
  10.33.64.136          e0-0a-f6-6d-2d-fd     dynamique
  10.33.65.106          d8-f2-ca-3b-76-ee     dynamique
  10.33.68.35           b0-3c-dc-ae-ab-6e     dynamique
  10.33.71.99           b0-3c-dc-ae-ab-6e     dynamique
  10.33.71.111          b0-3c-dc-ae-ab-6e     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
[...]
````

## III. Le requin-chat. 
![requin-chat](images.jpeg)

 - Pour la [Capture ARP](TPreseau\B2\TP1\arp.pcap) 
J'ai utilisé comme seul filtre : "arp". 

 - Pour la [Capture DNS](TPreseau\B2\TP1\dns.pcap) j'ai utilisé "dns" comme filtre.

  - Pour la [Capture TCP](TPreseau\B2\TP1\tcp.pcap) j'ai utilisé "ip.addr == 10.33.76.174 && tcp" comme filtre, l'ip spécifié étant mon ip.


