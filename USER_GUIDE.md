# The Scripting Project - Documentation d'utilisation

## I. Généralités : Les fonctionnalités du script
Le script vous proposera de faire différentes demandes, *actions* ou *informations*, sur différentes cibles :
- Utilisateur
- Ordinateur

### a. Les actions
#### Pour un utilisateur
Vous pourrez :
- Créer un utilisateur
- Supprimer un utilisateur
- Modifier le mot de passe d'un utilisateur

#### Pour un ordinateur
Vous pourrez :
- Redémarrer l'ordinateur
- Eteindre l'ordinateur

### b. Les informations
#### Pour un utilisateur
Vous pourrez :
- Savoir les dates de connexion d'un utilisateur
- Savoir si l'utilisateur existe

#### Pour un ordinateur
Vous pourrez :
- Savoir le type de système d'exploitation de l'ordinateur client
- Savoir depuis combien de temps l'ordinateur client est allumé, sopit son *uptime*

## II. Bien utiliser le script
Tout d'abord, il faut vous connecter sur l'ordinateur SRVLX01 :
- Identifiant : wilder
- Mot de passe : Azerty1*

Une fois connecté, vérifier d'être bien sur le dossier **/home/wilder**, avec la commande `pwd`. Dans ce dossier, vous trouverez :
- Le dossier Documents, où s'enregistrera les différentes demandes d'informations.
- Le dossier TheScriptingProject, où se trouve le script.

Pour appeler le script, il faudra taper les commandes suivantes (tout en restant dans le dossier /home/wilder) :
```
su root
# Vous avez besoin d'être sous l'utilisateur Root pour pouvoir accéder au dossier /var/log
# où s'enregistrera tout au long du script, les différents évènements de vos choix.
./TheScriptingProject/mainMenu.sh
```
Vous arriverez sur ce menu :  
![image](https://github.com/Mirhazka/TheScriptingProject/blob/01852d03be1038891719fed6f40fa1f3f5d5c759/Ressources/appelScript%26menu.png)  

Chacun de vos choix, vous amènes à des sous-menus où à la fin, vous pourrez :
- Soit faire des actions
- Soit faire des demandes d'informations.
Ce script, vous permettra d'agir sur la machine cliente CLILIN01, grâce à une connexion SSH.

## III. Les différentes options
Ce script permet d'agir sur une machine distante via une connexion SSH. Vous aurez donc besoin de connaitre :
- Le nom d'utilisateur sur qui vous souhaitez vous connecter
- L'adresse IP de la machine cible
- Le mot de passe de l'utilisateur correspondant

A plusieurs reprises dans le script, une connexion SSH devra s'établir, cela se verra sous cette forme `wilder@172.16.10.30's password`.

## IV. F.A.Q
***Questions : Où sont enregistrés les informations que j'aurais demandé ?***  
*Réponse*  
Les informations que vous aurez demandé lors du scripting, seront enregistrés dans le dossier /home/wilder/Documents/ sous la forme suivante : `info_Cible_Date.txt`; avec :
- *Cible* : Le nom de l'utilisateur ou de l'ordinateur cible
- *Date* : Date du recueil des informations au format *yyyymmdd*

***Questions : Vous avez parlé de journalisation, où pourrais-je retrouver ces informations ?***  
*Réponse*  
Les informations de journalisation seront enregistrés dans le dossier **/var/log/** et dans le fichier `log_evt.log`.  
Les enregistrements seront sous la forme suivante : *Date-Heure-Utilisateur-Evenement*, avec :
- *Date* : Date de l'évènement au format *yyymmdd*
- *Heure* : Heure de l'évènement au format *hhmmss*
- *Utilisateur* : Nom de l'utilisateur courant utilisant la machine **SRVLX01** exécutant le script
- *Evenements* : Action effectué lors de l'utilisation du script :
  - Les différents choix dans le menu et les sous-menu;
  - Lors des actions ou des demandes d'informations, chaque étape sera détaillé.
