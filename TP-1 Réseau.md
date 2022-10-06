# TP-1 Réseau 
-
## 1.1
Les infos des cartes réseau :
`ipconfig /all`
 - *Interface :*
   Description. . . . . . . . . . . . . . : Intel(R) Wireless-AC 9461
   Adresse physique . . . . . . . . . . . : B8-9A-2A-4C-FE-78
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.16.233(préféré)
 - *Interface Ethernet :* 
    Je ne possède pas de port RJ45.
 - *Gateway :* 
    Passerelle par défaut. . . . . . . . . : 10.33.19.254

  - Pour obtenir l'adresse MAC de la passerelle :
    `arp -a`
Je reprends l'adresse IP de la passerelle et j'obtiens :
*10.33.19.254          00-c0-e7-e0-04-4e     dynamique*

Dans l'image ci-dessous, j'ai utilisé la commande `windows + e` afin d'ouvrir mes dossiers windows. Cheminer ensuite dans "Mon PC", y faire un clic-droit pour atteindre les propriétés et tomber ainsi sur le Panneau de Configuration. Enfin nous suivons le cheminement affiché ci-dessous.
![](https://i.imgur.com/z7BRR1y.png)

-

## 2.A

 ![](https://i.imgur.com/9apvEuZ.png)

Ci-dessus, nous pouvons voir que notre adresse IP a changé. Passant de `10.33.16.233` à `10.33.16.200`. 
Nous avons simplement été dans le même menu, onglet "propiété", puis IPV4. Enfin nous avons saisis les données retrouvés précédemment en prenant soin de modifier le dernier octet seulement.

- Explication :

Lors de notre changement d'adresse IP. Nous avons perdus effectivement l'accès à internent. En effet, notre adresse IP nous permettant de nous connecter à changé. Ce qui nous disqualifie ainsi de l'accès précédemment obtenu. Nous devons alors retrouver un accès à internet en redemandant une nouvelle ip au DNS. 

# II. Exploration locale en Duo 

### II.3 

![](https://i.imgur.com/kzkce6n.png)

Notre IP a bien changé : 

```
PS C:\Users\lucas>ipconfig /all
  
   
   Carte Ethernet Ethernet :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Realtek Gaming GbE Family Controller
   Adresse physique . . . . . . . . . . . : C0-18-03-59-30-32
   DHCP activé. . . . . . . . . . . . . . : Non
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::e1c2:fd45:f4f0:e17d%18(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.10.10.251(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :
   IAID DHCPv6 . . . . . . . . . . . : 163584003
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-29-6A-1A-C4-C0-18-03-59-30-32
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```
   
Les deux machines se joingent : 

``` 
PS C:\Users\titim> ping  10.10.10.250

Envoi d’une requête 'Ping'  10.10.10.250 avec 32 octets de données :
Réponse de 10.10.10.250 : octets=32 temps=1 ms TTL=128
Réponse de 10.10.10.250 : octets=32 temps=1 ms TTL=128
Réponse de 10.10.10.250 : octets=32 temps=1 ms TTL=128
Réponse de 10.10.10.250 : octets=32 temps=2 ms TTL=128

Statistiques Ping pour 10.10.10.250:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 2ms, Moyenne = 1ms
```

Voici l'adresse MAC du collègue : 

``` 
arp -a
Interface : 10.10.10.251 --- 0x12
  Adresse Internet      Adresse physique      Type
  10.10.10.250          b0-25-aa-47-c7-a4     dynamique
  10.10.10.255          ff-ff-ff-ff-ff-ff     statique
  169.254.139.228       b0-25-aa-47-c7-a4     dynamique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique![](https://i.imgur.com/vcmGB1k.png)
```

### II.4 

![](https://i.imgur.com/GbI9iFF.png)

On test l'accès internet : 
```
PS C:\Users\titim> ping 1.1.1.1

Envoi d’une requête 'Ping'  1.1.1.1 avec 32 octets de données :
Réponse de 1.1.1.1 : octets=32 temps=20 ms TTL=55
Réponse de 1.1.1.1 : octets=32 temps=20 ms TTL=55
Réponse de 1.1.1.1 : octets=32 temps=21 ms TTL=55
Réponse de 1.1.1.1 : octets=32 temps=20 ms TTL=55

Statistiques Ping pour 1.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 20ms, Maximum
```

Internet passe bien de l'autre côté : 

````
 PS C:\Users\titim> tracert 192.168.137.2

Détermination de l’itinéraire vers DESKTOP-0JKFI2T [192.168.137.2]
avec un maximum de 30 sauts :

  1     2 ms     1 ms     1 ms  DESKTOP-0JKFI2T [192.168.137.2]

Itinéraire déterminé.
````

### 5. Petit chat privé

##### PC serveur : 
```
PS C:\Users\Initi\netcat-1.11> .\nc.exe -l -p 8888
```
##### PC client: 
```
PS C:\Users\maxfe\Desktop\netcat-win32-1.11\netcat-1.11> .\nc.exe 192.168.137.1 8888
```
#### CONVERSATION : 
```
[fmaxance] : Salut !
[mmederic] : Salut
[mmederic] : ça dit quoi ?
[fmaxance] : rien de spécial mise à part que j'aime les pommes et toi ?
[mmederic] : bah écoute j'aime les pommes aussi
[fmaxance] : SUPER au revoir
```
##### Connexion en cours

```
PS C:\Users\mmederic> netstat -a -n -b

  TCP    192.168.137.1:8888     192.168.137.2:56320    ESTABLISHED
 [nc.exe]
```
##### Pour aller un peu plus loin

IP non définie : 
```
PS C:\Users\mmederic\netcat-1.11> ./nc.exe -l -p 8888

PS C:\Users\mmederic> netstat -a -n -b | Select-String 8888

  TCP    0.0.0.0:8888           0.0.0.0:0              LISTENING
```
N'importe qui peut se connecter sur le serveur car l'IP est non définie.


IP définie : 
```
PS C:\Users\mmederic\netcat-1.11> ./nc.exe -l -p 8888 -s 192.168.137.1
PS C:\Users\mmederic> netstat -a -n -b | Select-String 8888

  TCP    192.168.137.1:8888     0.0.0.0:0              LISTENING
```
### 6. Firewall
#### 🌞 Activez et configurez votre firewall

![](https://i.imgur.com/XNnmoOO.png)