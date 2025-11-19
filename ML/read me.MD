## Compte rendu descriptif de la base de données Wine Quality

### Présentation générale
La base de données Wine Quality provient du dépôt UCI Machine Learning Repository. Elle contient des échantillons de vins blancs annotés par leurs propriétés physico-chimiques et une note de qualité sensorielle.

### Variables
- **fixed acidity** : acidité fixe
- **volatile acidity** : acidité volatile
- **citric acid** : acide citrique
- **residual sugar** : sucre résiduel
- **chlorides** : chlorures
- **free sulfur dioxide** : dioxyde de soufre libre
- **total sulfur dioxide** : dioxyde de soufre total
- **density** : densité
- **pH** : pH
- **sulphates** : sulfates
- **alcohol** : taux d'alcool

### Variable cible
- **quality** : qualité du vin (score sensoriel), converti en classification binaire (mauvais = 0 pour qualité ≤ 5, bon = 1 sinon).

### Structure des données
- Données organisées sous forme de DataFrame pandas.
- 11 caractéristiques numériques pour chaque échantillon.
- Tâche typique : classification binaire ou régression de la qualité.

### Statistiques et corrélations
- Corrélations entre variables chimiques présentes.
- Relations notables entre densité et sucre, pH et acidité, etc.
- Utilisées pour l’analyse, la visualisation et la modélisation (ex. KNN).

