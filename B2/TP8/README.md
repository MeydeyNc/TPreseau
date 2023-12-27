On a donc 2 batiments reliés entre eux . 


Meow Orginis : Bat 1 : 

3 étages et 1 sous-sol. Disposions particulières des équipes dans le batiment. 
Penser à différencier le placement des équipes et de la salle serveur. 

 -- 3 tier infra -- 

On a au moins les vlans.
Pas de partage de vlans entre les deux sites. 

 - Dev : **10.8.10.0/23**
    - Tests 
    - Git 
    - Prod
    - Serveur
    - internet

 - Admin Sys/Rés/Sécu : **10.8.20.0/28**
    - cameras --> Sécu
    - Serveurs 
    - All Vlans --> Sys & Réz
    - internet

 - Bureaux (pdg, RH, clientèle) **10.8.30.0/26**
    - accès serveur DB
    - internet 

 - Serveurs : **10.8.40.0/28**

 - Clients : **10.8.50.0/24**
    - internet

 - cameras : **10.8.60.0/28**
    - serveur DB unique 
    - monitoring distant ?

 - Téléphones IP : **10.8.70.0/23**

 - Télévisions : **10.8.80.0/28**

 - Imprimantes : **10.8.90.0/28**

### Tableau des IPs : 

- ***Meow Origins :*** 

| Machine & Réseau | 10.8.10.0/23 | 10.8.20.0/28 | 10.8.30.0/26 | 10.8.40.0/28 | 10.8.50.0/24 | 10.8.60.0/28 | 10.8.70.0/23 | 10.8.80.0/28 | 10.8.90.0/28 | 10.8.1.0/30 |
|------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|----------|-----------|-----------|
|MeowOriginsR1|10.8.10.1|10.8.20.14|10.8.30.62|10.8.40.14|10.8.50.254|10.8.60.14|10.8.70.1|10.8.80.14|10.8.90.14|10.8.1.1
|DevLead4|10.8.10.8|X|X|X|X|X|X|X|X|X|
|Dev10|10.8.10.10|X|X|X|X|X|X|X|X|X|
|Dev34|10.8.10.34|X|X|X|X|X|X|X|X|X|
|Dev68|10.8.10.68|X|X|X|X|X|X|X|X|X|
|LeadDev1|10.8.10.100|X|X|X|X|X|X|X|X|X|
|Dev70|10.8.10.71|X|X|X|X|X|X|X|X|X|
|Dev105|10.8.10.105|X|X|X|X|X|X|X|X|X|
|Dev132|10.8.10.132|X|X|X|X|X|X|X|X|X|
|AdminRes1|X|10.8.20.1|X|X|X|X|X|X|X|X|
|AdminSys1|X|10.8.20.2|X|X|X|X|X|X|X|X|
|SecurityTeam|X|10.8.20.3|X|X|X|X|X|X|X|X|
|Bureau1|X|X|10.8.30.10|X|X|X|X|X|X|X|
|Bureau2|X|X|10.8.30.11|X|X|X|X|X|X|X|
|RH1|X|X|10.8.30.12|X|X|X|X|X|X|X|
|RH2|X|X|10.8.30.13|X|X|X|X|X|X|X|
|PDG|X|X|10.8.30.14|X|X|X|X|X|X|X|
|Accueil1|X|X|10.8.30.15|X|X|X|X|X|X|X|
|Accueil2|X|X|10.8.30.16|X|X|X|X|X|X|X|
|Accueil3|X|X|10.8.30.17|X|X|X|X|X|X|X|
|Git.Meow.Origins|X|X|X|10.8.40.1|X|X|X|X|X|X|
|Test.Meow.Origins|X|X|X|10.8.40.2|X|X|X|X|X|X|
|Prod.Meow.Origins|X|X|X|10.8.40.3|X|X|X|X|X|X|
|dns.meow.origins|X|X|X|10.8.40.4|X|X|X|X|X|X|
|dhcp.meow.origins|X|X|X|10.8.40.5|X|X|X|X|X|X|
|Client.Meow.Origins|X|X|X|X|10.8.50.101|X|X|X|X|X|
|Client.Meow.Origins|X|X|X|X|10.8.50.198|X|X|X|X|X|
|cam.acc.1|X|X|X|X|X|10.8.60.2|X|X|X|X|
|cam.acc.2|X|X|X|X|X|10.8.60.3|X|X|X|X|
|cam.et1.1|X|X|X|X|X|10.8.60.4|X|X|X|X|
|cam.et1.2|X|X|X|X|X|10.8.60.5|X|X|X|X|
|cam.et2.2|X|X|X|X|X|10.8.60.6|X|X|X|X|
|cam.et3.1|X|X|X|X|X|10.8.60.7|X|X|X|X|
|cam.et3.2|X|X|X|X|X|10.8.60.8|X|X|X|X|
|tel.ip.1|X|X|X|X|X|X|10.8.70.101|X|X|X|
|tel.ip.2|X|X|X|X|X|X|10.8.70.102|X|X|X|
|tel.ip.3|X|X|X|X|X|X|10.8.70.103|X|X|X|
|tel.ip.4|X|X|X|X|X|X|10.8.70.104|X|X|X|
|tel.ip.5|X|X|X|X|X|X|10.8.70.105|X|X|X|
|tv.acc.1|X|X|X|X|X|X|X|10.8.80.1|X|X|
|tv.acc.2|X|X|X|X|X|X|X|10.8.80.2|X|X|
|tv.et1.1|X|X|X|X|X|X|X|10.8.80.3|X|X|
|tv.et1.2|X|X|X|X|X|X|X|10.8.80.4|X|X|
|tv.et2.1|X|X|X|X|X|X|X|10.8.80.5|X|X|
|tv.et2.2|X|X|X|X|X|X|X|10.8.80.6|X|X|
|tv.et3.1|X|X|X|X|X|X|X|10.8.80.7|X|X|
|tv.et3.2|X|X|X|X|X|X|X|10.8.80.8|X|X|
|imp.acc|X|X|X|X|X|X|X|X|10.8.90.1|X|
|imp.et1|X|X|X|X|X|X|X|X|10.8.90.2|X|
|imp.et2|X|X|X|X|X|X|X|X|10.8.90.3|X|
|imp.et3|X|X|X|X|X|X|X|X|10.8.90.4|X|


- ***Meow & Beyond :***

| Machine & Réseau | 10.8.11.0/23 | 10.8.21.0/28 | 10.8.31.0/26 | 10.8.41.0/28 | 10.8.51.0/24 | 10.8.61.0/28 | 10.8.71.0/23 | 10.8.81.0/28 | 10.8.91.0/28 | 10.8.1.0/30 |
|------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|----------|-----------|-----------|
|Meow&BeyondR2|10.8.11.1|10.8.21.14|10.8.31.62|10.8.41.14|10.8.51.254|10.8.61.14|10.8.71.1|10.8.81.14|10.8.91.14|10.8.1.2|
|Lead.Dev.MB.1|10.8.11.1|X|X|X|X|X|X|X|X|X|
|Lead.Dev.MB.2|10.8.11.2|X|X|X|X|X|X|X|X|X|
|Dev.MB.12|10.8.11.12|X|X|X|X|X|X|X|X|X|
|Dev.MB.6|10.8.11.6|X|X|X|X|X|X|X|X|X|
|Admin.MB.Sys|X|10.8.21.1|X|X|X|X|X|X|X|X|
|Admin.MB.Res|X|10.8.21.2|X|X|X|X|X|X|X|X|
|Accueil.MB.1|X|X|10.8.31.1|X|X|X|X|X|X|X|
|Accueil.MB.2|X|X|10.8.31.2|X|X|X|X|X|X|X|
|Serveur.MB.test|X|X|X|10.8.41.1|X|X|X|X|X|X|
|dhcp.MB.1|X|X|X|10.8.41.2|X|X|X|X|X|X|
|Client.MB.1|X|X|X|X|10.8.51.100|X|X|X|X|X|
|Client.MB.20|X|X|X|X|10.8.51.120|X|X|X|X|X|
|cam.MB.1|X|X|X|X|X|10.8.61.1|X|X|X|X|
|cam.MB.2|X|X|X|X|X|10.8.61.2|X|X|X|X|
|cam.MB.3|X|X|X|X|X|10.8.61.3|X|X|X|X|
|cam.MB.4|X|X|X|X|X|10.8.61.4|X|X|X|X|
|cam.MB.5|X|X|X|X|X|10.8.61.5|X|X|X|X|
|tel.MB.1|X|X|X|X|X|X|10.8.71.12|X|X|X|
|tel.MB.2|X|X|X|X|X|X|10.8.71.16|X|X|X|
|tv.MB.acc1|X|X|X|X|X|X|X|10.8.81.1|X|X|
|tv.MB.acc2|X|X|X|X|X|X|X|10.8.81.2|X|X|
|tv.MB.bat1|X|X|X|X|X|X|X|10.8.81.3|X|X|
|tv.MB.bat2|X|X|X|X|X|X|X|10.8.81.4|X|X|
|imp.MB.bat1|X|X|X|X|X|X|X|X|10.8.91.1|X|
|imp.MB.bat2|X|X|X|X|X|X|X|X|10.8.91.2|X|

### Tableau des VLANs :

- ***Meow Origins :*** 

| VLAN | VLAN 10 **devMO** | VLAN 20 **AdminsMO** | VLAN 30 **BureauxMO** | VLAN 40 **ServeursMO** | VLAN 50 **ClientsMO** | VLAN 60 **CamerasMO** | VLAN 70 **VoIPMO** | VLAN 80 **TVsMO** | VLAN 90 **ImprimantesMO** |
|------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|----------|-----------|
|Réseau|10.8.10.0/23|10.8.20.0/28|10.8.30.0/26|10.8.40.0/28|10.8.50.0/24|10.8.60.0/28|10.8.70.0/23|10.8.80.0/28|10.8.90.0/28|


- ***Meow & Beyond :*** 

| VLAN | VLAN 11 **devMB** | VLAN 21 **AdminsMB** | VLAN 31 **BureauxMB** | VLAN 41 **ServeursMB** | VLAN 51 **ClientsMB** | VLAN 61 **CamerasMB** | VLAN 71 **VoIPMB** | VLAN 81 **TVsMB** | VLAN 91 **ImprimantesMB** |
|------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|----------|-----------|
|Réseau|10.8.11.0/23|10.8.21.0/28|10.8.31.0/26|10.8.41.0/28|10.8.51.0/24|10.8.61.0/28|10.8.71.0/23|10.8.81.0/28|10.8.91.0/28|

### Client des VLANs :

- ***Meow Origins :*** 

| VLAN | VLAN 10 **devMO** | VLAN 20 **AdminsMO** | VLAN 30 **BureauxMO** | VLAN 40 **ServeursMO** | VLAN 50 **ClientsMO** | VLAN 60 **CamerasMO** | VLAN 70 **VoIPMO** | VLAN 80 **TVsMO** | VLAN 90 **ImprimantesMO** |
|------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|----------|-----------|
|MeowOriginsR1|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|
|DevLead4|:cat:|X|X|X|X|X|X|X|X|X|
|Dev10|:cat:|X|X|X|X|X|X|X|X|X|
|Dev34|:cat:|X|X|X|X|X|X|X|X|X|
|Dev68|:cat:|X|X|X|X|X|X|X|X|X|
|LeadDev1|:cat:|X|X|X|X|X|X|X|X|X|
|Dev70|:cat:|X|X|X|X|X|X|X|X|X|
|Dev105|:cat:|X|X|X|X|X|X|X|X|X|
|Dev132|:cat:|X|X|X|X|X|X|X|X|X|
|AdminRes1|X|:cat:|X|X|X|X|X|X|X|X|
|AdminSys1|X|:cat:|X|X|X|X|X|X|X|X|
|SecurityTeam|X|:cat:|X|X|X|X|X|X|X|X|
|Bureau1|X|X|:cat:|X|X|X|X|X|X|X|
|Bureau2|X|X|:cat:|X|X|X|X|X|X|X|
|RH1|X|X|:cat:|X|X|X|X|X|X|X|
|RH2|X|X|:cat:|X|X|X|X|X|X|X|
|PDG|X|X|:cat:|X|X|X|X|X|X|X|
|Accueil1|X|X|:cat:|X|X|X|X|X|X|X|
|Accueil2|X|X|:cat:|X|X|X|X|X|X|X|
|Accueil3|X|X|:cat:|X|X|X|X|X|X|X|
|Git.Meow.Origins|X|X|X|:cat:|X|X|X|X|X|X|
|Test.Meow.Origins|X|X|X|:cat:|X|X|X|X|X|X|
|Prod.Meow.Origins|X|X|X|:cat:|X|X|X|X|X|X|
|dns.meow.origins|X|X|X|:cat:|X|X|X|X|X|X|
|dhcp.meow.origins|X|X|X|:cat:|X|X|X|X|X|X|
|Client.Meow.Origins|X|X|X|X|:cat:|X|X|X|X|X|
|Client.Meow.Origins|X|X|X|X|:cat:|X|X|X|X|X|
|cam.acc.1|X|X|X|X|X|:cat:|X|X|X|X|
|cam.acc.2|X|X|X|X|X|:cat:|X|X|X|X|
|cam.et1.1|X|X|X|X|X|:cat:|X|X|X|X|
|cam.et1.2|X|X|X|X|X|:cat:|X|X|X|X|
|cam.et2.2|X|X|X|X|X|:cat:|X|X|X|X|
|cam.et3.1|X|X|X|X|X|:cat:|X|X|X|X|
|cam.et3.2|X|X|X|X|X|:cat:|X|X|X|X|
|tel.ip.1|X|X|X|X|X|X|:cat:|X|X|X|
|tel.ip.2|X|X|X|X|X|X|:cat:|X|X|X|
|tel.ip.3|X|X|X|X|X|X|:cat:|X|X|X|
|tel.ip.4|X|X|X|X|X|X|:cat:|X|X|X|
|tel.ip.5|X|X|X|X|X|X|:cat:|X|X|X|
|tv.acc.1|X|X|X|X|X|X|X|:cat:|X|X|
|tv.acc.2|X|X|X|X|X|X|X|:cat:|X|X|
|tv.et1.1|X|X|X|X|X|X|X|:cat:|X|X|
|tv.et1.2|X|X|X|X|X|X|X|:cat:|X|X|
|tv.et2.1|X|X|X|X|X|X|X|:cat:|X|X|
|tv.et2.2|X|X|X|X|X|X|X|:cat:|X|X|
|tv.et3.1|X|X|X|X|X|X|X|:cat:|X|X|
|tv.et3.2|X|X|X|X|X|X|X|:cat:|X|X|
|imp.acc|X|X|X|X|X|X|X|X|:cat:|X|
|imp.et1|X|X|X|X|X|X|X|X|:cat:|X|
|imp.et2|X|X|X|X|X|X|X|X|:cat:|X|
|imp.et3|X|X|X|X|X|X|X|X|:cat:|X|


- ***Meow & Beyond :***

| VLAN | VLAN 11 **devMB** | VLAN 21 **AdminsMB** | VLAN 31 **BureauxMB** | VLAN 41 **ServeursMB** | VLAN 51 **ClientsMB** | VLAN 61 **CamerasMB** | VLAN 71 **VoIPMB** | VLAN 81 **TVsMB** | VLAN 91 **ImprimantesMB** |
|------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|----------|-----------|
|Meow&BeyondR2|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|:cat:|
|Lead.Dev.MB.1|:cat:|X|X|X|X|X|X|X|X|X|
|Lead.Dev.MB.2|:cat:|X|X|X|X|X|X|X|X|X|
|Dev.MB.12|:cat:|X|X|X|X|X|X|X|X|X|
|Dev.MB.6|:cat:|X|X|X|X|X|X|X|X|X|
|Admin.MB.Sys|X|:cat:|X|X|X|X|X|X|X|X|
|Admin.MB.Res|X|:cat:|X|X|X|X|X|X|X|X|
|Accueil.MB.1|X|X|:cat:|X|X|X|X|X|X|X|
|Accueil.MB.2|X|X|:cat:|X|X|X|X|X|X|X|
|Serveur.MB.test|X|X|X|:cat:|X|X|X|X|X|X|
|dhcp.MB.1|X|X|X|:cat:|X|X|X|X|X|X|
|Client.MB.1|X|X|X|X|:cat:|X|X|X|X|X|
|Client.MB.20|X|X|X|X|:cat:|X|X|X|X|X|
|cam.MB.1|X|X|X|X|X|:cat:|X|X|X|X|
|cam.MB.2|X|X|X|X|X|:cat:|X|X|X|X|
|cam.MB.3|X|X|X|X|X|:cat:|X|X|X|X|
|cam.MB.4|X|X|X|X|X|:cat:|X|X|X|X|
|cam.MB.5|X|X|X|X|X|:cat:|X|X|X|X|
|tel.MB.1|X|X|X|X|X|X|:cat:|X|X|X|
|tel.MB.2|X|X|X|X|X|X|:cat:|X|X|X|
|tv.MB.acc1|X|X|X|X|X|X|X|:cat:|X|X|
|tv.MB.acc2|X|X|X|X|X|X|X|:cat:|X|X|
|tv.MB.bat1|X|X|X|X|X|X|X|:cat:|X|X|
|tv.MB.bat2|X|X|X|X|X|X|X|:cat:|X|X|
|imp.MB.bat1|X|X|X|X|X|X|X|X|:cat:|X|
|imp.MB.bat2|X|X|X|X|X|X|X|X|:cat:|X|


R1MOrigins : 
````
R1#sh running-config
Building configuration...

interface FastEthernet0/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 10.8.1.1 255.255.255.252
 duplex auto
 speed auto
!
interface FastEthernet1/0
 no ip address
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0.10
 encapsulation dot1Q 10
 ip address 10.8.10.1 255.255.254.0
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.20
 encapsulation dot1Q 20
 ip address 10.8.20.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.30
 encapsulation dot1Q 30
 ip address 10.8.30.62 255.255.255.192
 ip helper-address 10.90.0.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.40
 encapsulation dot1Q 40
 ip address 10.8.40.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.50
 encapsulation dot1Q 50
 ip address 10.8.50.254 255.255.255.0
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.60
 encapsulation dot1Q 60
 ip address 10.8.60.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.70
 encapsulation dot1Q 70
 ip address 10.8.70.1 255.255.254.0
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.80
 encapsulation dot1Q 80
 ip address 10.8.80.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.90
 encapsulation dot1Q 90
 ip address 10.8.90.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0
 no ip address
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet2/0.10
 encapsulation dot1Q 10
 ip address 10.8.10.1 255.255.254.0
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.20
 encapsulation dot1Q 20
 ip address 10.8.20.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.30
 encapsulation dot1Q 30
 ip address 10.8.30.62 255.255.255.192
 ip helper-address 10.90.0.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.40
 encapsulation dot1Q 40
 ip address 10.8.40.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.50
 encapsulation dot1Q 50
 ip address 10.8.50.254 255.255.255.0
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.60
 encapsulation dot1Q 60
 ip address 10.8.60.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.70
 encapsulation dot1Q 70
 ip address 10.8.70.1 255.255.254.0
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.80
 encapsulation dot1Q 80
 ip address 10.8.80.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0.90
 encapsulation dot1Q 90
 ip address 10.8.90.14 255.255.255.240
 ip helper-address 10.8.40.5
 ip nat inside
 ip virtual-reassembly
!
ip forward-protocol nd
ip route 10.11.0.0 255.255.254.0 10.8.40.5
ip route 10.21.0.0 255.255.255.240 10.8.40.5
ip route 10.31.0.0 255.255.255.192 10.8.40.5
ip route 10.41.0.0 255.255.255.240 10.8.40.5
ip route 10.51.0.0 255.255.255.0 10.8.40.5
ip route 10.61.0.0 255.255.255.240 10.8.40.5
ip route 10.71.0.0 255.255.254.0 10.8.40.5
ip route 10.81.0.0 255.255.255.240 10.8.40.5
ip route 10.91.0.0 255.255.255.240 10.8.40.5
!
!
no ip http server
no ip http secure-server
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
````

R1M&B : 
````

R2#sh running-config
Building configuration...

interface FastEthernet0/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 10.8.1.2 255.255.255.252
 duplex auto
 speed auto
!
interface FastEthernet1/0
 no ip address
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0.11
 encapsulation dot1Q 11
 ip address 10.8.11.1 255.255.254.0
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.21
 encapsulation dot1Q 21
 ip address 10.8.21.14 255.255.255.240
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.31
 encapsulation dot1Q 31
 ip address 10.8.31.62 255.255.255.192
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.41
 encapsulation dot1Q 41
 ip address 10.8.41.14 255.255.255.240
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.51
 encapsulation dot1Q 51
 ip address 10.8.51.254 255.255.255.0
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.61
 encapsulation dot1Q 61
 ip address 10.8.61.14 255.255.255.240
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.71
 encapsulation dot1Q 71
 ip address 10.8.71.1 255.255.254.0
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.81
 encapsulation dot1Q 81
 ip address 10.8.81.14 255.255.255.240
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet1/0.91
 encapsulation dot1Q 91
 ip address 10.8.91.14 255.255.255.240
 ip helper-address 10.8.41.2
 ip nat inside
 ip virtual-reassembly
!
interface FastEthernet2/0
 no ip address
 shutdown
 duplex auto
 speed auto
!
ip forward-protocol nd
ip route 0.0.0.0 0.0.0.0 FastEthernet0/1
ip route 10.8.10.0 255.255.254.0 10.8.40.5
ip route 10.8.20.0 255.255.255.240 10.8.40.5
ip route 10.8.30.0 255.255.255.192 10.8.40.5
ip route 10.8.40.0 255.255.255.240 10.8.40.5
ip route 10.8.50.0 255.255.255.0 10.8.40.5
ip route 10.8.60.0 255.255.255.240 10.8.40.5
ip route 10.8.70.0 255.255.254.0 10.8.40.5
ip route 10.8.80.0 255.255.255.240 10.8.40.5
ip route 10.8.90.0 255.255.255.240 10.8.40.5
!
!
no ip http server
no ip http secure-server
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
````

CoreSw1 : 
````
CoreSw1#sh running-config
Building configuration...

Current configuration : 2072 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname CoreSw1
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

CoreSw2 : 
````
CoreSw2#sh running-config
Building configuration...

Current configuration : 2072 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname CoreSw2
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

DistSw1 : 
````
DistSw1#sh running-config
Building configuration...

Current configuration : 1902 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname DistSw1
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

DistSw2 : 
````
DistSw2#sh running-config
Building configuration...

Current configuration : 1783 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname DistSw2
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

AccSw1 : 
````
AccSw1#sh running-config
Building configuration...

Current configuration : 1800 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname AccSw1
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

AccSw2 : 
````
AccSw2#sh running-config
Building configuration...

Current configuration : 2054 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname AccSw2
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

AccSw3 : 
````
AccSw3#sh running-config
Building configuration...

Current configuration : 1850 bytes
!
! Last configuration change at 16:28:07 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname AccSw3
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

AccSw4 : 
````
AccSw4#sh running-config
Building configuration...

Current configuration : 1748 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname AccSw4
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

AccSw5 : 
````
AccSw5#sh running-config
Building configuration...

Current configuration : 2258 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname AccSw5
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

sw1MB : 
````
sw1MB#sh running-config
Building configuration...

Current configuration : 2258 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw1MB
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

sw1Bat2MB:
````
sw1Bat2MB#sh running-config
Building configuration...

Current configuration : 2258 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw2Bat2MB
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

sw2Bat1MB : 
````
sw2Bat1MB#sh running-config
Building configuration...

Current configuration : 2258 bytes
!
! Last configuration change at 16:28:06 UTC Sat Dec 23 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw2Bat1MB
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

DHCPMO : 
````
[mmederic@localhost ~]$ sudo cat /etc/dhcp/dhcpd.conf
#
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
#
option domain-name      "tp8-domain";

option domain-name-servers      1.1.1.1;

default-lease-time      600;

max-lease-time  7200;

authoritative;


subnet 10.8.10.0 netmask 255.255.254.0 {
        range dynamic-bootp 10.8.10.5 10.8.10.253;
        option routers 10.8.10.1;
}

subnet 10.8.20.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.20.1 10.8.20.13;
        option routers 10.8.20.14;
}

subnet 10.8.30.0 netmask 255.255.255.192 {
        range dynamic-bootp 10.8.30.1 10.8.30.60;
        option routers 10.8.30.62;
}

subnet 10.8.40.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.40.1 10.8.40.13;
        option routers 10.8.40.14;
}

subnet 10.8.50.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.8.50.100 10.8.50.200;
        option routers 10.8.50.254;
}

subnet 10.8.60.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.60.1 10.8.60.13;
        option routers 10.8.60.14;
}

subnet 10.8.70.0 netmask 255.255.254.0 {
        range dynamic-bootp 10.8.70.5 10.8.70.253;
        option routers 10.8.70.1;
}

subnet 10.8.80.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.80.1 10.8.80.13;
        option routers 10.8.80.14;
}

subnet 10.8.90.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.90.1 10.8.90.13;
        option routers 10.8.90.14;
}
````

it works : 
````
[mmederic@dhcp ~]$ systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Tue 2023-12-19 18:47:56 CET; 2h 55min ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 803 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 11038)
     Memory: 7.6M
        CPU: 10ms
     CGroup: /system.slice/dhcpd.service
             └─803 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid
````

DHCPM&B : 
````
[mmederic@dhcpmb ~]$ sudo cat /etc/dhcp/dhcpd.conf
#
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
#
option domain-name      "tp8-domain";

option domain-name-servers      1.1.1.1;

default-lease-time      600;

max-lease-time  7200;

authoritative;


subnet 10.8.11.0 netmask 255.255.254.0 {
        range dynamic-bootp 10.8.11.5 10.8.11.253;
        option routers 10.8.11.1;
}

subnet 10.8.21.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.21.1 10.8.21.13;
        option routers 10.8.21.14;
}

subnet 10.8.31.0 netmask 255.255.255.192 {
        range dynamic-bootp 10.8.31.1 10.8.31.60;
        option routers 10.8.31.62;
}

subnet 10.8.41.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.41.1 10.8.41.13;
        option routers 10.8.41.14;
}

subnet 10.8.51.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.8.51.100 10.8.51.200;
        option routers 10.8.51.254;
}

subnet 10.8.61.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.61.1 10.8.61.13;
        option routers 10.8.61.14;
}

subnet 10.8.71.0 netmask 255.255.254.0 {
        range dynamic-bootp 10.8.71.5 10.8.71.253;
        option routers 10.8.71.1;
}

subnet 10.8.81.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.81.1 10.8.81.13;
        option routers 10.8.81.14;
}

subnet 10.8.91.0 netmask 255.255.255.240 {
        range dynamic-bootp 10.8.91.1 10.8.91.13;
        option routers 10.8.91.14;
}
````

it works : 
````
[mmederic@dhcpmb ~]$ systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Tue 2023-12-19 18:47:56 CET; 2h 55min ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 803 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 11038)
     Memory: 7.6M
        CPU: 10ms
     CGroup: /system.slice/dhcpd.service
             └─803 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid
````

DNS : 
````
[mmederic@dns ~]$ sudo cat /etc/named.conf
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
#       listen-on port 53 { 127.0.0.1; };
#       listen-on-v6 port 53 { ::1; };
        directory       "/var/named";
        dump-file       "/var/named/data/cache_dump.db";
        statistics-file "/var/named/data/named_stats.txt";
        memstatistics-file "/var/named/data/named_mem_stats.txt";
        secroots-file   "/var/named/data/named.secroots";
        recursing-file  "/var/named/data/named.recursing";
        allow-query     { localhost; };

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

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";

# primary forward and reverse zones
//forward zone
zone "MeowOrigins.lan" IN {
     type master;
     file "meoworigins.lan.db";
     allow-update { none; };
    allow-query {any; };
};
//reverse zone
zone "MeowBeyond.lan" IN {
     type master;
     file "meowbeyond.lan.db";
     allow-update { none; };
    allow-query { any; };
};
````

````
sudo cat /var/named/meoworigins.lan.db
[sudo] password for mmederic:
$TTL 86400
@ IN SOA dns-primary.meoworigins.lan. admin.meoworigins.lan. (
    2019061800 ;Serial
    3600 ;Refresh
    1800 ;Retry
    604800 ;Expire
    86400 ;Minimum TTL
)

;Name Server Information
@ IN NS dns-primary.meoworigins.lan.

;IP for Name Server
dns-primary IN A 10.8.40.4

;A Record for IP address to Hostname
GitMoewOrigins IN A 10.8.40.1
TestMeowOrigins IN A 10.8.40.2
ProdMeowOrigins IN A 10.8.40.3
DHCPMeowOrigins IN A 10.8.40.5
````

````
sudo cat /var/named/meowobeyond.lan.db
[sudo] password for mmederic:
$TTL 86400
@ IN SOA dns-primary.meoworigins.lan. admin.meoworigins.lan. (
    2019061800 ;Serial
    3600 ;Refresh
    1800 ;Retry
    604800 ;Expire
    86400 ;Minimum TTL
)

;Name Server Information
@ IN NS dns-primary.meoworigins.lan.

;A Record for IP address to Hostname
TestMeowBeyond IN A 10.8.41.1
DHCPMeowBeyond IN A 10.8.41.2
````
