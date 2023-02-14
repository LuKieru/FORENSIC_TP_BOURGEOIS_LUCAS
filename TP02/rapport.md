## Exercice : 

Obtenir le nombre de lignes dans le fichier qui contient la ville LYON dans la colonne 9.







<!DOCTYPE html>
<head>
<head>
</head>
<body>
    <details>
        <summary>Réponse</summary>
         awk -F";" '{print $9}' consommation-annuelle-residentielle-par-adresse.csv | grep "LYON" | wc -l
    </details>
</body>
</html>
