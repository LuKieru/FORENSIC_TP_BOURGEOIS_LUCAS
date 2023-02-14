## Exercice : 

Contexte :

Une demande a été faite : depuis ce fichier, déterminer le nombre total d'IRIS dans la commune de Lyon.

###### IRIS =  Ilots Regroupés pour l'Information Statistique

>Via une ligne de commande, le but est d'obtenir le nombre de lignes dans le fichier 'consommation-annuelle-residentielle-par-adresse.csv' qui contiennent la ville de LYON dans la colonne NOM_Commune.




<details>
  <summary>Réponse</summary>
  
  ### Réponse entière
  ```
  awk -F";" '{print $9}' consommation-annuelle-residentielle-par-adresse.csv | grep "LYON" | wc -l
  ```
  
  1. 
```
awk -F";"
```
  	* Va donner le type de séparation dans le fichier CSV (donc ici, le point virgule qui par défaut est simplement une virgule). Cette partie dont le -F est important car sans spécification du format de séparation, le résultat change complètement la façon de lire le fichier et donc le résultat.
  	
  2. 
```
  '{print $9}'
```
     	* Cette partie va aller récupérer la colonne 9, celle des noms de commune.
     	
  3. 
``` consommation-annuelle-residentielle-par-adresse.csv
```
  	* Ici, c'est le nom du fichier ou il la commande va se faire
  	
  4.	
```
| grep "LYON" | wc -l
```
	* Cette dernière partie va compléter la commande : on va chercher uniquement la chaine de caractères "LYON" et compter les lignes qui les contiennent.

Enfin, le résultat qui doit être obtenu est le suivant : 12421, dans le fichier il y a 12421 lignes qui contiennent la commune de LYON : 

###### Il y a alors 12421 IRIS dans la commune de LYON.

  
</details>


