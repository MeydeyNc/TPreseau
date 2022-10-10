# TP-2 Ethernet, IP et ARP
---
## I. Set up IP

Afin d'avoir un tunnel entre les deux machines. 
Tout d'abord je travaille avec VirtualBox. 
J'ai choisi l'adresse : 
````
Carte Ethernet VirtualBox Host-Only Network :
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
````
Ma VM a pour adresse : 
````
192.168.56.2
````
addresse de réseau : 
````
192.168.56.0/22
````
adresse de Broadcast : 
````
brd ff:ff:ff:ff:ff:ff
````

## II. 

Pour l'adresse MAC de ma VM: 
````
arp - a 

Interface : 192.168.56.1 --- 0x28
  Adresse Internet      Adresse physique      Type
  192.168.56.2          08-00-27-15-f6-66     dynamique
````
L'adresse intéressant ici est l'adresse physique ou adresse MAC. 

Pour l'addresse MAC de ma gateway : 
````
arp - a 

10.33.19.254          00-c0-e7-e0-04-4e     dynamique
````

Manipuler la table arp : 
```
PS C:\WINDOWS\system32> arp -a

Interface : 10.33.17.10 --- 0x7
  Adresse Internet      Adresse physique      Type
  10.33.16.90           34-6f-24-c4-bd-65     dynamique
  10.33.19.254          00-c0-e7-e0-04-4e     dynamique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.56.1 --- 0x28
  Adresse Internet      Adresse physique      Type
  192.168.56.2          08-00-27-15-f6-66     dynamique
  192.168.59.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
PS C:\WINDOWS\system32> arp -d
PS C:\WINDOWS\system32> arp -a

Interface : 10.33.17.10 --- 0x7
  Adresse Internet      Adresse physique      Type
  10.33.19.254          00-c0-e7-e0-04-4e     dynamique
```
Ici nous comprenons bien que la commande a fonctionné. 
Nous rééffectuons des pings : 
````
PS C:\WINDOWS\system32> ping 192.168.56.2

Envoi d’une requête 'Ping'  192.168.56.2 avec 32 octets de données :
Réponse de 192.168.56.2 : octets=32 temps=1 ms TTL=64
Réponse de 192.168.56.2 : octets=32 temps<1ms TTL=64
Réponse de 192.168.56.2 : octets=32 temps<1ms TTL=64
Réponse de 192.168.56.2 : octets=32 temps=1 ms TTL=64

Statistiques Ping pour 192.168.56.2:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 1ms, Moyenne = 0ms
PS C:\WINDOWS\system32> arp -a

Interface : 10.33.17.10 --- 0x7
  Adresse Internet      Adresse physique      Type
  10.33.19.254          00-c0-e7-e0-04-4e     dynamique

Interface : 192.168.56.1 --- 0x28
  Adresse Internet      Adresse physique      Type
  192.168.56.2          08-00-27-15-f6-66     dynamique
````
Nous pouvons constater la réapparition de l'adresse IP ping précédemment (celle de notre VM).

## III. 

Dans le PCAP joint, "trames ARP DORA" nous constatons les 4 trames intéressantes des informations de la nouvelle demande.

Pour la trame Discover : 
La source vient de 0.0.0.0, notre ordi qui demande une nouvelle IP. 
La destination est 255.255.255.255, le DHCP via le masque. 

Pour la trame Offer : 
Le DHCP nous propose une IP depuis la passerelle qui passe par le masque. 

Pour la trame Request : 
Depuis notre PC on envoie le choix de l'IP. Via le masque au DHCP. 

Pour la trame Acknowledge : 
C'est le DHCP qui nous répond pour dire qu'il accepte le choix d'IP. 

1. IP utilisé : 10.33.17.10
2. IP Adresse passerelle du réseau : 10.33.19.254
3. DNS joignable : 8.8.8.8 (Google)

