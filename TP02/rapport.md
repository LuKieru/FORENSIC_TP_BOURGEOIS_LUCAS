## Exercice : 

Obtenir le nombre de lignes dans le fichier qui contient la ville LYON dans la colonne 9.






###### réponse : 

>  !   awk -F";" '{print $9}' consommation-annuelle-residentielle-par-adresse.csv | grep "LYON" | wc -l

