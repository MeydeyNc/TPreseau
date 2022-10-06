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

