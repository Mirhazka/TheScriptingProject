# The Scripting Project - Documentation d'installation pour Administrateurs

## I. Prérequis techniques

### 1) Client

- Nom : CLILIN01
- Distribution : Ubuntu 24.04 LTS
- Compte utilisateur : wilder (dans le groupe sudo)
- Mot de passe : Azerty1*
- Adresse IP fixe : 172.16.10.30/24

### 2) Serveur

- Nom : SRVLX01
- Distribution : Debian 12 sans GUI
- Compte : root
- Mot de passe : Azerty1*
- Adresse IP fixe : 172.16.10.10/24

### 3) Outils & Logiciels

Pour l'application du script, les deux ordinateurs devront être configuré avec l'outils SSH.

## II. Configuration du serveur SRVLX01

### 1) Configuration système

Ce serveur aura les spécificités suivantes :
- CPU : 2 coeurs;
- RAM : Minimum 512 Mo, Maximum 2048 Mo;
- Stockage : Disque dur HDD de 32 Go;
- Carte réseaux :
  - N°1 : Connecté au NET pour recevoir les mises à jours systèmes & pouvoir installés les paquets. Ce qui correspond à une interface réseau NAT sur VirtualBox.
  - N°2 : Connecté au réseau interne du laboratoire pour pouvoir communiquer avec l'ordinateur client. Ce qui correspond à une interface réseau interne sur VirtualBox.

### 2) Configuration réseaux

La carte réseau N°1 est automatiquement configuré par VirtualBox, ici nous allons configuré la carté réseau N°2.  
Pour cela, il faut aller modifier le fichier /etc/netplan/<nomdufichier>.yaml avec la commande suivante : `sudo nano /etc/netplan/<nomdufichier>.yaml`. A l'intérieur de ce fichier, faites les modifications suivantes :
```
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    ethernets:
        ens18:
            dhcp4: true
        ens19:
            dhcp4: no
            addresses:
            - 172.16.10.10/24
    version: 2
```
Puis enregistré le fichier et appliquer les changements avec la commande `sudo netplan apply`. Vérifier l'application des changements avec `ip a` qui vous doit vous afficher :
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
  link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
  inet 127.0.0.1/8 scope host lo
  valid_lft forever preferred_lft forever
  inet6 ::1/128 scope host noprefixroute
  valid_lft forever preferred_lft forever
2: ens18: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
  link/ether bc:24:11:0b:e9:0c brd ff:ff:ff:ff:ff:ff
  altname enp0s18
  inet 10.3.0.10/24 metric 100 brd 10.3.0.255 scope global dynamic ens18
  valid_lft 5613sec preferred_lft 5613sec
  inet6 fe80::be24:11ff:fe0b:e90c/64 scope link
  valid_lft forever preferred_lft forever
3: ens19: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
  link/ether bc:24:11:23:d2:94 brd ff:ff:ff:ff:ff:ff
  altname enp0s19
  inet 172.16.10.10/24 brd 172.16.10.255 scope global ens19
  valid_lft forever preferred_lft forever
  inet6 fe80::be24:11ff:fe23:d294/64 scope link
  valid_lft forever preferred_lft forever
```

### 3) Configuration SSH

Le serveur SRVLX01 est celui qui demande les connexions SSH, il est donc le `client`du serveur SSH qui lui sera installé sur le client **CLILIN01**. Mais d'abord, il faut installer le service client sur le serveur avec la commande `sudo apt-get install openssh-client -y`. Maintenant qu'il est installé, et à la conditions que le serveur sur le client **CLILIN01** est opérationnel, vous pouvez vous connecter à distance avec la commande `ssh wilder@172.16.10.30`. Le mot de passe de `wilder`vous sera demandé, une fois la connexion établie, vous aurez le contrôle à distance du client **CLILIN01**.
```
wilder@SRVLX01:~$ ssh wilder@172.16.10.30
wilder@172.16.10.30's password:
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-48-generic x86_64)

* Documentation:  https://help.ubuntu.com
* Management:     https://landscape.canonical.com
* Support:        https://ubuntu.com/pro

La maintenance de sécurité étendue pour Applications n'est pas activée.

16 mises à jour peuvent être appliquées immédiatement.
Pour afficher ces mises à jour supplémentaires, exécuter : apt list --upgradable

Activez ESM Apps pour recevoir des futures mises à jour de sécurité supplémentaires.
Visitez https://ubuntu.com/esm ou executez : sudo pro status

Last login: Thu Nov 14 14:41:13 2024 from 172.16.10.10
wilder@CLILIN01:~$
```

## III. Configuration du client CLILIN01

### 1) Configuration système

Ce client aura les spécificités suivantes :
- CPU : 2 coeurs;
- RAM : Minimum 512 Mo, Maximum 2048 Mo;
- Stockage : Disque dur HDD de 32 Go;
- Carte réseaux :
  - N°1 : Connecté au NET pour recevoir les mises à jours systèmes & pouvoir installés les paquets. Ce qui correspond à une interface réseau NAT sur VirtualBox.
  - N°2 : Connecté au réseau interne du laboratoire pour pouvoir communiquer avec l'ordinateur client. Ce qui correspond à une interface réseau interne sur VirtualBox.

### 2) Configuration réseaux

Le client **CLILIN01** aura la même configuration que le serveur **SRVLX01** sauf pour l'adresse IP qui sera `172.16.10.30/24`. Sinon c'est les mêmes étapes que précédemment.

### 3) Configuration SSH

Comme expliqué plus haut, le client **CLILIN01** recevra les demandes de connexion et sera donc le serveur SSH. Il faut donc installer OpenSSH-Server avec la commande `sudo apt-get install openssh-server -y`. Une fois installé, faites la commande `systemctl status ssh` ce qui affichera :
```
wilder@CLILIN01:~$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
    Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Active: active (running) since Thu 2024-11-14 12:21:46 CET; 2h 11min ago
TriggeredBy: ● ssh.socket
    Docs: man:sshd(8)
            man:sshd_config(5)
    Process: 3038 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
Main PID: 3040 (sshd)
    Tasks: 1 (limit: 9446)
    Memory: 3.3M (peak: 4.2M)
        CPU: 78ms
    CGroup: /system.slice/ssh.service
            └─3040 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

nov. 14 12:22:05 CLILIN01 sshd[3041]: Accepted password for wilder from 172.16.10.10 port 52874 ssh2
nov. 14 12:22:05 CLILIN01 sshd[3041]: pam_unix(sshd:session): session opened for user wilder(uid=1000) by     wilder(uid=0)
nov. 14 12:29:28 CLILIN01 sshd[3172]: Accepted password for wilder from 172.16.10.10 port 46424 ssh2
nov. 14 12:29:28 CLILIN01 sshd[3172]: pam_unix(sshd:session): session opened for user wilder(uid=1000) by     wilder(uid=0)
nov. 14 12:29:28 CLILIN01 sshd[3172]: pam_unix(sshd:session): session closed for user wilder
nov. 14 12:29:35 CLILIN01 sshd[3220]: Accepted password for wilder from 172.16.10.10 port 41340 ssh2
nov. 14 12:29:35 CLILIN01 sshd[3220]: pam_unix(sshd:session): session opened for user wilder(uid=1000) by     wilder(uid=0)
nov. 14 12:29:35 CLILIN01 sshd[3220]: pam_unix(sshd:session): session closed for user wilder
nov. 14 14:32:47 CLILIN01 sshd[3667]: Accepted password for wilder from 10.20.0.3 port 36430 ssh2
nov. 14 14:32:47 CLILIN01 sshd[3667]: pam_unix(sshd:session): session opened for user wilder(uid=1000) by     wilder(uid=0)
```
Le service peut ne pas être démarré ni être activé au démarrage, si c'est le cas, il faudra faire les commandes `systemctl enable ssh && systemctl restart ssh`.

## IV. Installation du script
Dans ce dépôt, vous trouverez dans le dossier [Script](https://github.com/Mirhazka/TheScriptingProject/tree/e6577aead3f5328b820f33959231b882e64c09a3/Script) le script principal `mainMenu.sh` et les sous-scripts dans les dossiers **user** & **computer**. Le script principal est le menu de départ du script qui appel, via un menu intéractif avec l'utilisateur, soit des fonctions soit d'autres scripts.
