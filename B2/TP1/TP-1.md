# TP 1 Maitrise réseau du Poste.

## I. Basics. 

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


