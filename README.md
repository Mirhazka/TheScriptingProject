# The Scripting Project - Documentation Générale

## I. Présentation du projet & Objectifs
### 1) Le projet
Le projet consiste à créer un script qui s’exécute sur une machine et effectue des tâches sur des machines distantes. L’ensemble des machines sont sur le même réseau.  

Les tâches sont des actions ou des requêtes d’information.  

L’objectif est de mettre en pratique plusieurs compétences techniques et collaboratives dans un projet de scripts orienté client/serveur. Il s'agit de créer un script bash pour un environnement Linux, à exécuter entre un serveur et un client Linux, et un script PowerShell pour un environnement Windows, à exécuter entre un serveur et un client Windows. Ce projet inclut le travail en équipe pour mener à bien chaque étape, la documentation détaillée du processus, et la démonstration du résultat final.  

Mise en pratique des compétences suivantes :
- Mettre en place une architecture client/serveur
- Créer et gérer des scripts bash et PowerShell
- Réaliser un projet en équipe
- Documenter toutes les étapes
- Faire une démonstration de la réalisation finale

En somme, il s’agit d’un projet complet de développement et de déploiement de scripts, avec documentation et présentation.

Le projet contient 2 objectifs, 1 objectif principal et 1 objectif secondaire.

### 2) Les objectifs
#### a) Objectif principal
Objectif principal :
- Depuis une machine Windows Server, on exécute un script PowerShell qui cible des ordinateurs Windows.
- Depuis une machine Debian, on exécute un script shell qui cible des ordinateurs Ubuntu.

L’objectif principal est validé si :
- Il est complètement réalisé et fonctionnel
- La documentation est réalisée et correcte
- La présentation finale montre les 2 points précédents

#### b) Objectif secondaire
Depuis un serveur, cibler une machine cliente avec un type d’OS différent
L’objectif secondaire est optionnel et amènera en cas de réalisation validée, à une meilleure évaluation.

## II. Membres du groupe de projet
Pour ce projet, nous formons une équipe de 3 personnes. Le temps alloué pour ce projet est de 4 semaines et à chaque semaine les rôles de chacun des membres du groupe changeait entre :
- Scrum Master
- Product Owner
- Technicien TSSR

Cela nous a permit d'approfondir nos connaissances sur la méthode agile SCRUM.
Pour ce projet, mon rôle d'un point de vue technique a été la conception du script dans le langage *shell*.
Ce sur quoi mettra l'accent ce dépôt. Pour avoir le dépôt complet du projet, cliquez [ici](https://github.com/WildCodeSchool/TSSR-BDX-0924-P2-G2.git).

## III. Choix techniques
Pour rappel, ce projet fonctionne sous deux environnements : **Windows** et **Linux**

### 1) Windows
#### a) Client
- Nom : CLIWIN01
- Distribution : Windows 10
- Compte utilisateur : wilder (dans le groupe des admins locaux)
- Mot de passe : Azerty1*
- Adresse IP fixe : 172.16.10.20/24

#### b) Serveur
- Nom : SRVWIN01
- Distribution : Windows Serveur 2022 avec GUI
- Compte : Administrator (dans le groupe des admins locaux)
- Mot de passe : Azerty1*
- Adresse IP fixe : 172.16.10.5/24

### 2) Linux
#### a) Client
- Nom : CLILIN01
- Distribution : Ubuntu 24.04 LTS
- Compte utilisateur : wilder (dans le groupe sudo)
- Mot de passe : Azerty1*
- Adresse IP fixe : 172.16.10.30/24

#### b) Serveur
- Nom : SRVLX01
- Distribution : Debian 12 sans GUI
- Compte : root
- Mot de passe : Azerty1*
- Adresse IP fixe : 172.16.10.10/24

