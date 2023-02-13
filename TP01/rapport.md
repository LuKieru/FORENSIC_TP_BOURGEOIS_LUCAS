rapport 

Analyse forensic du contenu de la clé USB.

Tout d'abord, vérifier l'intégrité du contenu USB_Image :

Hash SHA-256 du fichier : 
 
a6fd7b3072187b2b6a31119f4580e58d5219fef157514c28d2de6df5ecf3185c  USB_Image

commande file USB_Image :
USB_Image: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "MSDOS5.0", sectors/cluster 8, reserved sectors 1418, 
Media descriptor 0xf8, sectors/track 63, heads 255, hidden sectors 2048, sectors 7677952 (volumes > 32 MB), 
FAT (32 bit), sectors/FAT 7483, reserved 0x1, serial number 0xa84d68d6, unlabeled

commande strings USB.Image :

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

