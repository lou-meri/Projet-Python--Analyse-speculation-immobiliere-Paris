### Dépendances techniques
Voir requirements.txt pour la liste complète des packages.

### Sources de données
DVF géolocalisées (data.gouv.fr) - Transactions immobilières 2023
INSEE - Dossier complet des arrondissements de Paris
OpenData Paris - Contours géographiques des arrondissements

### Licence MIT
Projet académique - Libre de réutilisation avec mention de la source.

### Auteur
Lou Meri

### Version
1.0.0 - Décembre 2025

# Analyse : Spéculation immobilière et accès au logement à Paris

Projet d'analyse statistique étudiant le lien entre la spéculation immobilière et l'accès au logement dans les arrondissements parisiens.

## Description du projet

Ce projet analyse les relations entre :
- **La spéculation immobilière** (prix élevés, vacance, rotation des biens)
- **L'accès au logement** (prix relatifs, caractéristiques socio-démographiques)

**Période d'analyse** : Données 2023  
**Zone géographique** : 20 arrondissements de Paris intramuros  
**Sources de données** : DVF (Demandes de Valeurs Foncières), INSEE, OpenData Paris

## Objectifs

1. Quantifier le niveau de spéculation immobilière par arrondissement
2. Identifier les déterminants de la spéculation
3. Analyser l'impact sur l'accès au logement
4. Produire des visualisations et un rapport complet

## Structure du projet

Speculation-immobiliere-et-acces-au-logement/

requirements.txt # Dépendances Python
.gitignore # Fichiers ignorés par Git
README.md # Ce fichier

notebooks/ # Notebooks d'analyse (à exécuter dans l'ordre)
─ 01_import_final_paris.ipynb # Import des données
─ 02_nettoyage_fusion_preparation.ipynb # Nettoyage et fusion
─ 03_analyse_statistique_et_visualisation.ipynb # Analyses finales

─ data/ # Données (créé automatiquement lors de l'exécution des notebooks)
─── raw/ # Données brutes téléchargées
─── processed/ # Données nettoyées et fusionnées
─── external/ # Données externes (contours géo)

─ output/ # Résultats finaux (créé automatiquement lors de l'exécution des notebooks)
─── rapport_final_analyse.md # Rapport complet
─── rapport_synthese_complet.png # Visualisations synthèse


## Installation et exécution

### 1. Cloner le dépôt

git clone https://github.com/lou-meri/Projet-Python--Analyse-speculation-immobiliere-Paris
cd Speculation-immobiliere-et-acces-au-logement

### 2. Installer les dépendances

pip install -r requirements.txt


### 3. Exécuter les notebooks dans l'ordre :
01_import_final_paris.ipynb - Télécharge et importe les données
02_nettoyage_fusion_preparation.ipynb - Nettoie et fusionne les données
03_analyse_statistique_et_visualisation.ipynb - Effectue les analyses finales


## Résumé du Projet : Analyse de la Spéculation Immobilière et de l'Accès au Logement à Paris

### 1. Collecte et Intégration des Données

Le projet a débuté par la collecte systématique de trois sources de données principales. Les données de transactions immobilières (DVF) pour l'année 2023 ont été téléchargées depuis data.gouv.fr, fournissant 80 964 transactions initiales sur Paris intramuros. Les données socio-démographiques de l'INSEE ont été récupérées via une archive contenant près de 2 000 indicateurs par arrondissement. Enfin, les contours géographiques des 20 arrondissements parisiens ont été obtenus via l'API OpenData de Paris, permettant les futures représentations cartographiques.

### 2. Nettoyage et Préparation des Données

Une phase de nettoyage a été menée sur les données DVF, conservant uniquement les ventes de logements (maisons et appartements) après élimination des valeurs aberrantes sur les prix au mètre carré, les surfaces et les valeurs foncières. Ce filtrage a abouti à 34 137 transactions exploitables. Pour les données INSEE, une sélection ciblée de 18 variables pertinentes a été opérée parmi les 1 977 disponibles, focalisant sur les indicateurs de logement, de vacance et de structure démographique.

### 3. Construction des Indicateurs et Fusion

Des indicateurs synthétiques ont été calculés à l'échelle de l'arrondissement. À partir des données DVF, nous avons construit le nombre de transactions, le prix médian au mètre carré, et surtout un ratio de spéculation (Q3/médiane) mesurant l'écart interne au marché. Les données INSEE ont permis de calculer le taux de vacance des logements et la part des ménages seuls. La fusion de ces deux bases a abouti à un jeu de données unifié de 20 observations (arrondissements) et 33 variables, incluant un indice composite de spéculation normalisé intégrant trois dimensions : disparité des prix, vacance et niveau absolu des prix.

### 4. Analyse Exploratoire et Statistique

Une analyse descriptive a révélé la grande hétérogénéité du marché parisien, avec des prix médians variant de 8 881 à 15 385 €/m² et des taux de vacance de 6,57% à 16,33%. L'analyse des corrélations a mis en lumière des relations significatives, notamment la forte corrélation positive entre le prix et l'indice de spéculation (r=0,732), et la corrélation négative entre le prix et le nombre de transactions (r=-0,650), indiquant une moindre liquidité des marchés les plus chers.

### 5. Modélisation par Régression Linéaire

Un modèle de régression a été estimé pour expliquer l'indice de spéculation. Les résultats confirment le rôle déterminant du prix au mètre carré (coefficient significativement positif) et, dans une moindre mesure, du taux de vacance. La part des ménages seuls s'est avérée non significative. Le modèle présente un R² ajusté de 0,732, indiquant une bonne capacité explicative, bien qu'une hétéroscédasticité des résidus ait été observée.

### 6. Segmentation par Clustering

Une analyse de clustering (K-means) a été conduite pour segmenter les arrondissements. Après validation par le score de silhouette, une segmentation en deux clusters a été retenue. Elle distingue clairement un "Paris central spéculatif" (9 arrondissements, dont les 1er à 8e et le 10e), caractérisé par des prix élevés, une spéculation positive et une faible liquidité, d'un "Paris périphérique populaire" (11 arrondissements, du 9e au 20e sauf le 10e), aux prix plus modérés, à la spéculation faible et à la forte liquidité.

### 7. Synthèse et Perspectives

Le travail a permis de constituer une base de données riche et exploitable, d'élaborer des indicateurs pertinents pour capturer le phénomène spéculatif multidimensionnel, et de mettre en évidence la fracture entre un centre-ville sous tension spéculative et une périphérie au marché plus accessible. Les analyses statistiques et économétriques ont validé les hypothèses de liens entre prix, vacance et comportements spéculatifs. Les résultats offrent des bases pour des analyses plus poussées, telles que l'intégration de données temporelles ou l'étude d'effets de seuil et de causalité.


### Livrables
Rapport Markdown complet
Cartes thématiques
Synthèse statistique
Présentation rapide
