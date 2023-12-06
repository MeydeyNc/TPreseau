# TP-5 

## I. Tester.

On a tenté de récupérer les fichiers à l'aide du fichier de partage temporaire de VBox == ça s'est révélé infructeux. 

On passe à un fauduleux ``CTRL + C ; CTRL + V``  grâce à notre fabuleux SSH. 

On récupère donc les fichiers dans un dossier 'app' directement sur notre /home/hostname/

Maintenant on va essayer l'app ! 

Nous avons été confrontés à quelques erreurs : 

L'IP définie de base dans le script ne correspond ni à notre réseau, ni à notre host. 

J'ai donc changé cette ip de base pour celle de notre host :

````
[mmederic@host ~]$ vi ./app/server.py
[mmederic@host ~]$ cat ./app/server.py | grep "host"
host = '10.1.10.10' # string vide signifie, dans ce conetxte, toutes les IPs de la machine
[mmederic@host ~]$ ip a | grep "enp0s8"
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    inet 10.1.10.10/24 brd 10.1.10.255 scope global noprefixroute enp0s8
````

On lance le script : 
- Entre temps on a compris que c'était dév en Python. 

````
[mmederic@host ~]$ sudo python ./app/server.py
13337
Le serveur tourne sur 10.1.10.10:13337
````

On ss pour voir que le script tourne bien : 
````
[mmederic@host ~]$ ss -lntpu | grep "13337"
tcp   LISTEN 0      1         10.1.10.10:13337      0.0.0.0:*
````

On va maintenant lancer le client : 
````
[mmederic@host ~]$ sudo python ./app/client.py
[sudo] password for mmederic:
Veuillez saisir une opération arithmétique : 4+5
````

 On a une réponse du sever, il voit bien la connexion, reçoit l'opération et renvoie la réponse.
````
Un client ('10.1.10.10', 36224) s'est connecté.
Le client ('10.1.10.10', 36224) a envoyé 4+5
Réponse envoyée au client ('10.1.10.10', 36224) : 9.
````

On ne reçoit pas la réponse dans la console du client, cependant grâce aux logs on l'a : 
````
2023-11-28 11:19:13 INFO Connexion réussie à 10.1.10.10:13337
2023-11-28 11:19:16 INFO Message envoyé au serveur 10.1.10.10 : 4+5
2023-11-28 11:19:16 INFO Réponse reçue du serveur 10.1.10.10 : b'9'
````

## II. Intégrer. 


### 1. Environnement. 

````
[mmederic@host ~]$ sudo mkdir /opt/calculatrice
[mmederic@host ~]$ sudo mv ./app/server.py /opt/calculatrice/
[mmederic@host ~]$ sudo mv ./app/client.py /opt/calculatrice/
````

### 2. systemd service.

````
[mmederic@host system]$ sudo touch calculatrice.service
[mmederic@host system]$ sudo chmod a+rwx calculatrice.service
````

#### B. Service basique. 

Le système est bien actif : 
````
[mmederic@host system]$ sudo systemctl status calculatrice
● calculatrice.service - Super calculatrice réseau
     Loaded: loaded (/etc/systemd/system/calculatrice.service; disabled; preset: disabled)
     Active: active (running) since Tue 2023-11-28 11:59:40 CET; 4min 50s ago
````

On ss pour voir le service qui tourne derrière le port connu : 
````
[mmederic@host ~]$ sudo ss -lntpu | grep 13337
tcp   LISTEN 0      1         10.1.10.10:13337      0.0.0.0:*    users:(("python",pid=1861,fd=4))
````

#### C. Amélioration du service. 

On vient de modifier notre fichier calculatrice : 
````
[mmederic@host ~]$ cat /etc/systemd/system/calculatrice.service
$ sudo cat /etc/systemd/system/calculatrice.service
[Unit]
Description=Super calculatrice réseau

[Service]
ExecStart=/usr/bin/python /opt/calculatrice/server.py
Restart=on-failure
RestartSec=30

[Install]
WantedBy=multi-user.target
````

Voici un cat du fichier de conf de calculatrice.service : 
````
[mmederic@host ~]$ cat /etc/systemd/system/calculatrice.service
$ sudo cat /etc/systemd/system/calculatrice.service
[Unit]
Description=Super calculatrice réseau

[Service]
ExecStart=/usr/bin/python /opt/calculatrice/server.py
Restart=always
RestartSec=1
ExecStartPre=/usr/bin/firewall-cmd --add-port=13337/tcp
ExecStopPost=/usr/bin/firewall-cmd --remove-port=13337/tcp

[Install]
WantedBy=multi-user.target
````

On va kill le process : 
````
[mmederic@host ~]$ systemctl status calculatrice.service
● calculatrice.service - Super calculatrice réseau
     Loaded: loaded (/etc/systemd/system/calculatrice.service; disabled; preset: disabled)
     Active: active (running) since Tue 2023-11-28 22:38:51 CET; 2s ago
    Process: 3039 ExecStartPre=/usr/bin/firewall-cmd --add-port=13337/tcp (code=exited, status=0/SUCCESS)
   Main PID: 3040 (python)
      Tasks: 2 (limit: 4590)
     Memory: 5.6M
        CPU: 293ms
     CGroup: /system.slice/calculatrice.service
             └─3040 /usr/bin/python /opt/calculatrice/server.py
[mmederic@host ~]$ kill 3040
-bash: kill: (3040) - Operation not permitted
[mmederic@host ~]$ sudo !!
sudo kill 3040
[mmederic@host ~]$ systemctl status calculatrice.service
● calculatrice.service - Super calculatrice réseau
     Loaded: loaded (/etc/systemd/system/calculatrice.service; disabled; preset: disabled)
     Active: active (running) since Tue 2023-11-28 22:39:25 CET; 2s ago

Nov 28 22:39:24 host systemd[1]: Starting Super calculatrice réseau...
Nov 28 22:39:25 host firewall-cmd[3050]: success
Nov 28 22:39:25 host systemd[1]: Started Super calculatrice réseau.
Nov 28 22:39:25 host python[3051]: Le serveur tourne sur 10.1.10.10:13337
````

Le process killed a bien été redémarré tournant déjà sur un port définit.

On check dans le firewall : 
````
[mmederic@host ~]$ sudo firewall-cmd --list-all | grep ports
  ports: 13337/tcp
````


### 3. Monitoring. 

On install netdata, il est ok et on a accès a l'overlay : 
````
[mmederic@host ~]$ systemctl status netdata
● netdata.service - Real time performance monitoring
     Loaded: loaded (/usr/lib/systemd/system/netdata.service; enabled; preset: enabled)
     Active: active (running) since Tue 2023-11-28 22:56:20 CET; 2min 22s ago
````

On vient de config netdata pour le port 13337 qui est celui de notre service : 
````
[mmederic@host netdata]$ cat go.d/portcheck.conf
## All available configuration options, their descriptions and default values:
## https://github.com/netdata/go.d.plugin/tree/master/modules/portcheck

update_every: 1
autodetection_retry: 0
#priority: 70000

jobs:
 - name: HostedCalculatrice
   host: 10.0.2.15
   ports:
        - 13337
        - 22
````


## III. Héberger

#### 1. Interface bridge

On vient de faire la conf avec une NAT qui est en pont. 

#### 2. Firewall : 

Nous n'avons pas de ports ouverts inutilement : 
````
[mmederic@host netdata]$ sudo firewall-cmd --list-all | grep ports
  ports: 19999/tcp 13337/tcp
````

#### 3. Serveur SSH

On change la conf de sshd pour qu'il écoute sur la carte NAT : 
````
[mmederic@host ~]$ ss -lntpu | grep 22
tcp   LISTEN 0      128        10.0.2.15:22         0.0.0.0:*
````

#### 4. Serveur Calculatrice. 

On édite pour que le serveur écoute que sur la carte NAT : 
````
[mmederic@host ~]$ ss -lntpu | grep 13337
tcp   LISTEN 0      1          10.0.2.15:13337      0.0.0.0:*
````