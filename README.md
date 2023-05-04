# lighten_kml
Reduce the number of geographic coordinates in KML files

Réduire le nombre de coordonnées géographiques dans les fichiers KML

# Objectif
Passionné d'aéromodélisme, j'embarque les autopilotes **Pixhawk** et **ArduPilot** sur certains de mes modèles réduits.  

Ces autopilotes enregistrent durant le vol des tas de paramètres (ils font office de boite noire), parmi lesquels les coordonnées géographiques, ce qui me permet, de retour chez moi, d'afficher les tracés des vols en 3D dans Google Earth !  

Seulement l'autopilote enregistre les coordonnées toutes les 0.2 secondes et il n'y a pas moyen de changer cela. Pour des vols assez longs de plus de 30 minutes, le fichier kml généré devient très volumineux, et l'affichage du tracé perd en fluidité lorsqu'on effectue des translations, rotations ou zooms !  

J'ai donc créé un petit script awk qui réduit le nombre de coordonnées, par un facteur N. Exemple : si N = 5, alors je ne garde qu'une coordonnée sur 5, soit 1 coordonnée par seconde, ce qui reste tout à fait acceptable pour garder un tracé suffisamment précis. L'affichage en 3D devient du coup bien plus fluide ! :)

Pour info : le tracé du/des vol(s) est sauvegardé dans un fichier au format kml  

KML est un format de fichier utilisé pour afficher des données géographiques dans un navigateur Earth tel que Google Earth

# Exemple de résultat :

## Avant :

![Before treatment](/Examples/before.jpg "Before treatment")

## Après traitement (N=5) :

![After treatment](/Examples/after.jpg "After treatment")

Chaque ligne verticale représente une coordonnée géographique. Par rapport à l'image précédente, leur nombre a été divisé par 5.  
La qualité du tracé reste tout à fait acceptable.

# Utilsation   : 
Le script awk se lance depuis un shell :

awk [-v STEP=VAL] -f lighten_kml.awk inputFileName > outputFileName

## Exemple d'utilisation : 
awk -v STEP=5 -f lighten_kml.awk logsFlight.kml > logsFlightNew.kml
