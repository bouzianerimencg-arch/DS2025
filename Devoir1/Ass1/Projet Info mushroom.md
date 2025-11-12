<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Donne-moi un maximum d'informations détaillées et structurées sur le jeu de données 'Mushroom' disponible à cette adresse : [https://archive.ics.uci.edu/dataset/73/mushroom](https://archive.ics.uci.edu/dataset/73/mushroom). Je souhaite connaître notamment sa description complète, le contexte scientifique, les caractéristiques des variables, le nombre d'instances, les classes cibles, la présence de données manquantes, les usages courants en apprentissage automatique, et tout autre détail pertinent pour bien comprendre et exploiter ce jeu.

Le jeu de données "Mushroom" disponible sur le site UCI Machine Learning Repository est un ensemble multivarié utilisé principalement pour des tâches de classification en biologie, visant à déterminer si un champignon est comestible ou toxique.

Description complète et contexte scientifique :

- Ce jeu comprend des descriptions hypothétiques correspondant à 23 espèces de champignons à lamelles des familles Agaricus et Lepiota.
- Chaque champignon est classé comme comestible (edible) ou toxique (poisonous). La classe "d'édibilité inconnue" a été regroupée avec la classe toxique par précaution.
- Il n'existe pas de règle simple pour déterminer la comestibilité d’un champignon, ce qui justifie l'intérêt de ce jeu pour des modèles d'apprentissage automatique.

Caractéristiques des variables :

- Le jeu contient 8124 instances (exemples).
- Il comporte 22 caractéristiques, toutes catégorielles, décrivant des attributs physiques comme la forme et la surface du chapeau, la couleur, la présence de meurtrissures, l’odeur, les caractéristiques des lamelles (attache, espacement, taille, couleur), la forme de la tige, la couleur au-dessus et en-dessous de l’anneau, le type de voile, la couleur des spores, etc.
- Une variable cible "poisonous" indique si le champignon est comestible (e) ou toxique (p).

Données manquantes :

- Le jeu présente des valeurs manquantes pour 2480 instances, exclusivement dans l’attribut "stalk-root" (racine de la tige), marquées par un "?".
- Les autres attributs ne comportent pas de données manquantes.

Classes cibles et distribution :

- Deux classes cibles : edible (4208 instances, 51.8%) et poisonous (3916 instances, 48.2%).

Usages en apprentissage automatique :

- Ce jeu est un classique pour les tâches de classification binaire.
- Il sert souvent à expérimenter des algorithmes de classification supervisée pour prédire la comestibilité des champignons.
- Les caractéristiques catégorielles et la présence de valeurs manquantes en font un bon cas d’étude pour le prétraitement des données, la sélection de variables, et la construction de règles métier (par exemple, certains attributs d’odeur sont fortement prédictifs).
- Les performances modèles de référence montrent qu’une simple règle basée sur l’attribut "odor" permet d’atteindre une très haute précision, proche de 99%.

Autres détails pertinents :

- Le jeu date de 1987, basé sur l’Audubon Society Field Guide.
- Les données sont sous licence Creative Commons Attribution 4.0.
- Fichiers principaux : données brutes, fichier noms, readme, index.
- Nombreuses publications scientifiques utilisent ce jeu pour des expérimentations en machine learning.

En résumé, le jeu Mushroom est un jeu de données multivarié catégoriel de taille moyenne, destiné à la classification binaire comestible vs toxique, très utilisé en apprentissage automatique pour illustrer les méthodes de classification, avec des caractéristiques issues de la biologie des champignons, et des données partiellement manquantes sur un attribut clé.[^2][^4][^7]
<span style="display:none">[^1][^10][^3][^5][^6][^8][^9]</span>

<div align="center">⁂</div>

[^1]: https://archive.ics.uci.edu/dataset/73/mushroom

[^2]: https://mldata-static.ml.tu-berlin.de/repository/data/viewslug/datasets-uci-mushroom/1.html

[^3]: https://www.nature.com/articles/s41598-021-87602-3

[^4]: https://archive.ics.uci.edu/ml/datasets/mushroom

[^5]: https://archive.ics.uci.edu/dataset/848/secondary+mushroom+dataset

[^6]: https://www.scikit-yb.org/en/latest/api/datasets/mushroom.html

[^7]: https://www.kaggle.com/code/aavigan/uci-mushroom-data

[^8]: https://www.openml.org/d/24

[^9]: https://www.cs.toronto.edu/~delve/data/mushrooms/mushroomDetail.html

[^10]: https://cubig.ai/store/products/194/mushroom-classification-dataset

