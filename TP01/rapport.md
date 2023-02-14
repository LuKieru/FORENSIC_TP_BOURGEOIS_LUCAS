# Rapport d'analyse Forensique 
###sur l'objet suivant : Clé USB trouvée sur le parking.

## Rappel du contexte :

Un agent a trouvé une clé USB près du parking du commissariat. Il l'a donc apportée au service forensic pour savoir si cette clé était malveillante ou non avant de la brancher.

## H2 Analyse :

Avant toute analyse, on s'assure qu'elle n'a pas été branchée sur les postes du commissariat. L'agent a donc bien fait de venir le service forensic directement puisqu'on ne sait ce qu'elle contient.

Au préalable, on branchera cette clé sur aucun terminal relié au réseau du commissariat. Ici, nous la brancherons sur un poste que l'on nomme **Station blanche**** puisqu'elle n'est reliée à aucun réseau et est dédiée à l'analyse de supports comme par exemple cette clé USB.

## H2 Début de l'analyse :

Nous sommes donc sur un environnement Linux, Ubuntu. Après avoir branché cette clé, voici les étapes effectuées :

Tout d'abord, vérifier l'intégrité du contenu USB_Image :
```
SHA256sum USB_Image
```

la réponse : 
 
```
a6fd7b3072187b2b6a31119f4580e58d5219fef157514c28d2de6df5ecf3185c  USB_Image
```

Ensuite, par "tatonnement", j'ai passé plusieur commandes dont :

file USB_Image :
USB_Image: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "MSDOS5.0", sectors/cluster 8, reserved sectors 1418, 
Media descriptor 0xf8, sectors/track 63, heads 255, hidden sectors 2048, sectors 7677952 (volumes > 32 MB), 
FAT (32 bit), sectors/FAT 7483, reserved 0x1, serial number 0xa84d68d6, unlabeled

strings USB.Image :

..         
JVJV
ECRET  PNG 
JVJV
[Trash Info]
Path=secret.png
DeletionDate=2023-02-10T22:21:51
IHDR
sRGB
gAMA


après passage de la commande "strings" sur le fichier USB_Image, en faisant défiler les résultats dans un fichier : 
j'ai aperçu la ligne : "path=secret.png"

j'ai alors lancé une commande pour tester le disque et donc tenter de récupérer des fichiers puis quelques images 
ont pu être récupérées.
commande : 
photorec USB.Image

Parmis ces images,fichiers (6 au total : 2 jpg, 3 png et 1 fichier ini ) : des photo d'animaux 
et 2 contenant le contenu suivant : BOSCH {1MAG3}

le fichier ini contenait lui : 
[Trash Info]
Path=secret.png
DeletionDate=2023-02-10T22:21:51

C'est le même résultat que j'ai obtenu lors de la commande strings.


Rapport réalisé le 13/02/2023 à 16:09 par Lucas Bourgeois

