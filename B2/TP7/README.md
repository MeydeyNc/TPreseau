# 3-tier architecture et redondance. 

Voici les confs : 

- R1 : 
````
Current configuration : 1786 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
[...]
!
ip name-server 1.1.1.1
!
interface FastEthernet0/0
ip address dhcp
ip nat outside
ip virtual-reassembly
duplex auto
speed auto
!
interface FastEthernet1/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0.10
 encapsulation dot1Q 10
 ip address 10.7.10.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 10 ip 10.7.10.254
 standby 10 priority 150
 standby 10 preempt
!
!
interface FastEthernet1/0.30
 encapsulation dot1Q 30
 ip address 10.7.30.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 30 ip 10.7.30.254
!
ip dns server
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
no cdp log mismatch duplex
!        
````

- R2 :
````
hostname R2
!
[...]
!
ip name-server 1.1.1.1
!
!
interface FastEthernet0/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!
interface FastEthernet1/0.10
 encapsulation dot1Q 10
 ip address 10.7.10.253 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 10 ip 10.7.10.254
!
interface FastEthernet1/0.20
 encapsulation dot1Q 20
 ip address 10.7.20.253 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 20 ip 10.7.20.254
!
interface FastEthernet1/0.30
 encapsulation dot1Q 30
 ip address 10.7.30.253 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 30 ip 10.7.30.254
 standby 30 priority 150
 standby 30 preempt
!
ip dns server
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
!
````

- sur sw1 : 
````
Current configuration : 2103 bytes
!
! Last configuration change at 14:40:45 UTC Thu Dec 7 2023
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

 - sur sw2 : 
````
Building configuration...

Current configuration : 2103 bytes
!
! Last configuration change at 10:41:25 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw2
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

- sur sw3 :
````
Current configuration : 2020 bytes
!
! Last configuration change at 10:33:49 UTC Thu Dec 7 2023
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

- sur sw4:
````
Current configuration : 1926 bytes
!
! Last configuration change at 10:35:03 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw4
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

- sur sw5 :
````
Current configuration : 1725 bytes
!
! Last configuration change at 14:49:02 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw5
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

- sur sw6:
````
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw6
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

- sur sw7:
````
Current configuration : 1674 bytes
!
! Last configuration change at 10:10:29 UTC Thu Dec 7 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname sw7
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

On peut ping ynov depuis PC4 : 
````
PC4> ping ynov.com
ynov.com resolved to 104.26.11.233
````


