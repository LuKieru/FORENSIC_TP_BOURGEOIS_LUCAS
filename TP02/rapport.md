## Exercice : 

Via une ligne de commande, le but est d'obtenir le nombre de lignes dans le fichier 'consommation-annuelle-residentielle-par-adresse.csv' qui contiennent la ville de LYON dans la colonne NOM_Commune.







<!DOCTYPE html>
<head>
<head>
</head>
<body>
    <details>
        <summary>Réponse</summary>
         awk -F";" '{print $9}' consommation-annuelle-residentielle-par-adresse.csv | grep "LYON" | wc -l
         
         awk -F";" 
         
         Va donner le type de séparation dans le fichier CSV (donc ici, le point virgule qui par défaut est simplement une virgule). Cette partie dont le -F est important car sans spécification du format de séparation, le résultat change complètement la façon de lire le fichier et donc le résultat.
         
         
         '{print $9}'
         
         Cette partie va aller récupérer la colonne 9, celle des noms de commune.
         
         
         consommation-annuelle-residentielle-par-adresse.csv
         
         Ici, c'est le nom du fichier ou il la commande va se faire
         
         
         | grep "LYON" | wc -l
         
         Cette dernière partie va compléter la commande : on va chercher uniquement les caractères "LYON" et compter les lignes qui les contiennent.
         
         Enfin, le résultat qui doit être obtenu est le suivant : 12421, dans le fichier il y a 12421 lignes qui contiennent la commune de LYON.
         
        
    </details>
</body>
</html>
