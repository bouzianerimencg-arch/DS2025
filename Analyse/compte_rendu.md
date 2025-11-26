
# Compte Rendu : Prédiction des Scores en Mathématiques des Étudiants

## 1. Introduction et Objectif
Ce projet vise à prédire les scores en mathématiques d’un groupe d’étudiants à partir de données issues de [cette analyse Kaggle](https://www.kaggle.com/code/umitka/students-math-scores-prediction-with-linear-regres). L’objectif est de comprendre les facteurs déterminants la performance des élèves et d’appliquer des méthodes de régression pour faire des prédictions fiables.

## 2. Démarche Méthodologique
- Import des bibliothèques Python pour l’analyse (pandas, numpy, sklearn, matplotlib, seaborn).
- Chargement du dataset académique.
- Encodage des variables catégorielles pour traitement machine learning.
- Séparation du jeu de données en variables explicatives (features) et variable cible (score de maths).
- Découpage en ensembles d’entraînement, de validation et de test (60% / 20% / 20%).
- Entraînement d’un modèle de Régression Linéaire puis d’une Forêt Aléatoire avec recherche de meilleurs hyperparamètres (GridSearchCV).
- Évaluation par R² (coefficient de détermination) et RMSE (erreur quadratique moyenne).
- Analyse de l’importance des variables et visualisations des distributions des scores.

## 3. Résultats et Analyse
- **Performance de la Forêt Aléatoire sur test :**
  - R² = 0,837
  - RMSE = 6,30
- **Facteurs prédictifs principaux :**
  - *Score en lecture* (influence > 0.50)
  - *Score en écriture* (influence ~0.30)
  - Le sexe est un facteur modéré (0.10-0.20), et les autres variables démographiques sont secondaires.
- **Distribution des scores selon le sexe :**
  - Légère sur-performance médiane des garçons, présence de plus d’outliers faibles chez les filles, mais distribution comparable globalement.
- **Distribution des scores de maths :**
  - Pic autour de 80, majorité dans [60, 90], sans valeurs manquantes.
- **Résidus et fiabilité :**
  - La distribution des résidus (erreurs de prédiction) est centrée et presque normale, sans biais ni variance extrêmes.

## 4. Conclusions
- Les notes en lecture et écriture sont les *meilleurs prédicteurs du score de maths*.
- Les données démographiques (niveau des parents, origine, préparation aux tests) ont un rôle bien moins significatif.
- Les modèles appliqués fournissent une bonne qualité prédictive, tant en global qu’à l’échelle individuelle.
- Cette approche montre la robustesse de l’utilisation de l’apprentissage automatique pour la prédiction de la performance scolaire.

## 5. Synthèse visuelle (exemple)
- Prédictions individuelles sur 5 profils : scores prévus entre 64 et 81.
- Visualisations disponibles pour :
  - Importance des variables
  - Distribution des scores par sexe
  - Distribution générale des scores et des résidus
