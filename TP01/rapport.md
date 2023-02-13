rapport 

Analyse forensic du contenu de la clé USB.

Tout d'abord, vérifier l'intégrité du contenu USB_Image :

Hash SHA-256 du fichier : 
 
a6fd7b3072187b2b6a31119f4580e58d5219fef157514c28d2de6df5ecf3185c  USB_Image

j'ai passé plusieur commandes dont :

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

même résultat que j'ai obtenu lors de la commande strings.
