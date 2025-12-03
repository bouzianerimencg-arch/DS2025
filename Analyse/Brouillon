# Compte Rendu d'Analyse : Modèle de Classification avec Régression Logistique

## 1. Introduction

### 1.1 Contexte
Ce projet s'inscrit dans le cadre d'une analyse de données visant à construire un modèle de classification binaire. Le code fourni illustre un pipeline complet de machine learning, depuis le prétraitement des données jusqu'à l'optimisation des hyperparamètres.

### 1.2 Problématique
L'objectif principal est de développer un modèle de classification capable de prédire une variable binaire (classes 0 et 1) avec une performance optimale. La problématique centrale concerne l'identification des meilleurs hyperparamètres pour un modèle de régression logistique, tout en gérant les défis liés aux données réelles (valeurs manquantes, variables mixtes, etc.).

### 1.3 Objectifs
- Construire un pipeline de prétraitement robuste gérant les données numériques et catégorielles
- Optimiser les hyperparamètres d'un modèle de régression logistique via Grid Search
- Évaluer la performance du modèle optimisé sur des données de test
- Identifier les limites du modèle et proposer des axes d'amélioration

---

## 2. Méthodologie

### 2.1 Données et Prétraitement

#### 2.1.1 Structure des données
Le jeu de données synthétique comprend :
- **Variables numériques** : `numerical_col_1`, `numerical_col_2`, `id_col`
- **Variables catégorielles** : `categorical_col_1`, `categorical_col_2`, `mixed_col`
- **Taille** : 100 observations avec introduction artificielle de valeurs manquantes

#### 2.1.2 Justification des choix de prétraitement

**Gestion des valeurs manquantes :**
- **Variables numériques** : Imputation par la moyenne (`SimpleImputer(strategy="mean")`)
  - *Justification* : Préserve la distribution centrale des données sans introduire de biais majeur
  - *Alternative possible* : Médiane pour des distributions asymétriques
  
- **Variables catégorielles** : Imputation par le mode (`SimpleImputer(strategy="most_frequent")`)
  - *Justification* : Maintient la cohérence avec les catégories existantes et préserve les proportions

**Encodage des variables catégorielles :**
- **Méthode** : One-Hot Encoding avec `handle_unknown="ignore"`
  - *Justification* : Permet au modèle linéaire d'interpréter les catégories sans imposer d'ordre artificiel
  - *Avantage* : Gère les nouvelles catégories en production sans erreur
  - *Limitation* : Augmente la dimensionnalité (problématique si nombreuses catégories)

**Normalisation des variables numériques :**
- **Méthode** : StandardScaler avec `with_mean=False`
  - *Justification* : Compatible avec les matrices creuses issues du One-Hot Encoding
  - *Effet* : Centre les données autour de 0 et réduit l'échelle, améliorant la convergence du modèle
  - *Note* : Le paramètre `with_mean=False` est crucial pour préserver la structure sparse

**Architecture du Pipeline :**
Le `ColumnTransformer` permet d'appliquer des transformations différentes selon le type de variable, garantissant un traitement cohérent entre l'entraînement et le déploiement.

### 2.2 Choix de l'algorithme

#### 2.2.1 Régression Logistique
**Justifications :**
1. **Interprétabilité** : Les coefficients permettent de comprendre l'impact de chaque variable
2. **Efficacité computationnelle** : Convergence rapide, adapté aux datasets de taille modérée
3. **Baseline solide** : Performance de référence avant d'explorer des modèles plus complexes
4. **Probabilités calibrées** : Sortie naturelle de probabilités de classe

**Paramètres de base :**
- `max_iter=1000` : Garantit la convergence même avec des données complexes
- `random_state=42` : Reproductibilité des résultats

### 2.3 Optimisation des Hyperparamètres

#### 2.3.1 Grid Search CV
**Grille d'hyperparamètres explorée :**
```python
param_grid = {
    'C': [0.001, 0.01, 0.1, 1, 10, 100],  # Régularisation
    'solver': ['liblinear', 'lbfgs', 'saga']  # Algorithmes d'optimisation
}
```

**Justification du paramètre C (Regularization Strength) :**
- Contrôle le compromis biais-variance
- Valeurs faibles (0.001) : Régularisation forte → modèle simple, risque de sous-apprentissage
- Valeurs élevées (100) : Régularisation faible → modèle complexe, risque de surapprentissage
- Plage logarithmique : Exploration efficace de l'espace des paramètres

**Justification des solvers :**
- **liblinear** : Efficace pour petits datasets, supporte la régularisation L1 et L2
- **lbfgs** : Recommandé pour datasets moyens, convergence rapide
- **saga** : Adapté aux grands datasets, supporte toutes les pénalités

**Validation croisée (CV=5) :**
- Réduit la variance de l'estimation de performance
- Évite le surapprentissage sur les données d'entraînement
- 5 folds : Compromis entre précision de l'estimation et coût computationnel

---

## 3. Résultats et Discussion

### 3.1 Résultats de l'Optimisation

**Meilleurs hyperparamètres identifiés :**
- `C = 0.001`
- `solver = 'liblinear'`

**Interprétation :**
- La régularisation forte (C=0.001) suggère que le modèle bénéficie de la simplicité
- Cela peut indiquer :
  - Un ratio signal/bruit défavorable dans les données
  - Présence de multicolinéarité entre variables
  - Nécessité de feature engineering plus poussé

### 3.2 Métriques de Performance

| Métrique | Valeur | Interprétation |
|----------|--------|----------------|
| **Accuracy CV** | 0.6750 | Performance moyenne sur les folds d'entraînement |
| **Accuracy Test** | 0.6500 | Performance sur données non vues |
| **Différence CV-Test** | -0.0250 | Légère dégradation, pas de surapprentissage majeur |

### 3.3 Analyse de la Matrice de Confusion

**Résultats pour la classe 0 (minoritaire, 7 échantillons) :**
- Précision : 0.00
- Rappel : 0.00
- F1-Score : 0.00
- **Interprétation** : Le modèle ne détecte **aucune** instance de la classe 0

**Résultats pour la classe 1 (majoritaire, 13 échantillons) :**
- Précision : 0.65
- Rappel : 1.00
- F1-Score : 0.79
- **Interprétation** : Le modèle prédit systématiquement la classe 1

### 3.4 Diagnostic du Problème Principal

#### 3.4.1 Déséquilibre de Classes Sévère
**Ratio de classes dans le test set : 7:13 (35% vs 65%)**

Le modèle a appris une stratégie triviale : **prédire systématiquement la classe majoritaire**. Cela explique :
- L'accuracy de 65% (= proportion de la classe 1)
- Le rappel parfait (1.00) pour la classe 1
- L'échec complet sur la classe 0

#### 3.4.2 Impact de la Régularisation Forte
Le choix de `C=0.001` (régularisation maximale) a poussé le modèle vers la solution la plus simple : ignorer les patterns minoritaires et prédire uniquement la classe majoritaire.

### 3.5 Analyse des Erreurs

**Types d'erreurs :**
1. **Faux Négatifs (Type II)** : 7 instances de classe 0 mal classées en classe 1
   - Impact critique : Le modèle manque complètement la classe minoritaire
   
2. **Faux Positifs (Type I)** : 0 (car toutes les prédictions sont classe 1)
   - Impact : Le modèle ne prend aucun risque

**Coût métier potentiel :**
Si la classe 0 représente un événement rare mais important (ex : fraude, défaillance), le modèle actuel est **inutilisable en production**.

---

## 4. Conclusion

### 4.1 Limites Identifiées

#### 4.1.1 Limites Structurelles
1. **Déséquilibre de classes critique** (35%/65%)
   - Biais systématique vers la classe majoritaire
   - Métriques trompeuses (accuracy élevée mais modèle non discriminant)

2. **Taille du dataset insuffisante**
   - 100 observations dont seulement 20 en test
   - Split 80/20 amplifie le problème de déséquilibre
   - Validation croisée sur 80 observations limite la robustesse

3. **Données synthétiques**
   - Ne reflètent pas la complexité du monde réel
   - Absence de corrélations réelles entre features et target

#### 4.1.2 Limites Méthodologiques
1. **Métrique d'évaluation inadaptée**
   - Accuracy seule masque le problème de déséquilibre
   - Absence de métriques orientées classe minoritaire

2. **Absence de feature engineering**
   - Aucune interaction entre variables
   - Pas d'analyse exploratoire préalable

3. **Choix algorithmique limité**
   - Un seul algorithme testé (régression logistique)
   - Pas de comparaison avec des méthodes plus robustes au déséquilibre

### 4.2 Pistes d'Amélioration Prioritaires

#### 4.2.1 Traitement du Déséquilibre de Classes

**Approche 1 : Rééquilibrage des données**
```python
from imblearn.over_sampling import SMOTE
from imblearn.under_sampling import RandomUnderSampler
from imblearn.pipeline import Pipeline as ImbPipeline

# SMOTE pour suréchantillonnage intelligent
smote = SMOTE(sampling_strategy=0.8, random_state=42)

# Ou combinaison SMOTE + Undersampling
pipeline_sampling = ImbPipeline([
    ('over', SMOTE(sampling_strategy=0.5)),
    ('under', RandomUnderSampler(sampling_strategy=0.8))
])
```
**Avantages** : Crée des exemples synthétiques de la classe minoritaire basés sur les k-plus proches voisins

**Approche 2 : Pondération des classes**
```python
from sklearn.utils.class_weight import compute_class_weight

# Calcul automatique des poids inversement proportionnels aux fréquences
class_weights = compute_class_weight('balanced', 
                                      classes=np.unique(y_train), 
                                      y=y_train)

log_reg = LogisticRegression(class_weight='balanced', max_iter=1000)
```
**Avantages** : Pénalise davantage les erreurs sur la classe minoritaire sans modifier les données

**Approche 3 : Ajustement du seuil de décision**
```python
# Au lieu de predict(), utiliser predict_proba() avec seuil personnalisé
y_proba = model.predict_proba(X_test)[:, 1]
threshold = 0.3  # Favorise la détection de la classe minoritaire
y_pred_adjusted = (y_proba >= threshold).astype(int)
```

#### 4.2.2 Optimisation des Métriques d'Évaluation

**Métriques recommandées pour déséquilibre :**

1. **F1-Score (macro ou weighted)**
```python
from sklearn.metrics import f1_score

# Grid Search avec F1-Score comme métrique
grid_search = GridSearchCV(
    estimator=log_reg,
    param_grid=param_grid,
    cv=StratifiedKFold(n_splits=5),
    scoring='f1_macro',  # Moyenne non pondérée des F1 de chaque classe
    n_jobs=-1
)
```

2. **ROC-AUC**
```python
from sklearn.metrics import roc_auc_score, roc_curve

# Courbe ROC
fpr, tpr, thresholds = roc_curve(y_test, y_proba)
auc_score = roc_auc_score(y_test, y_proba)

# Visualisation
plt.plot(fpr, tpr, label=f'AUC = {auc_score:.2f}')
plt.plot([0, 1], [0, 1], 'k--')
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve')
plt.legend()
```

3. **Precision-Recall Curve**
```python
from sklearn.metrics import precision_recall_curve, average_precision_score

precision, recall, thresholds = precision_recall_curve(y_test, y_proba)
ap_score = average_precision_score(y_test, y_proba)
```
**Justification** : Plus informative que ROC pour datasets déséquilibrés

#### 4.2.3 Exploration d'Algorithmes Alternatifs

**Algorithmes robustes au déséquilibre :**

1. **Random Forest avec pondération**
```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    class_weight='balanced',
    n_estimators=100,
    max_depth=10,
    random_state=42
)
```
**Avantages** : Gère naturellement les interactions, moins sensible au déséquilibre

2. **XGBoost avec scale_pos_weight**
```python
from xgboost import XGBClassifier

xgb = XGBClassifier(
    scale_pos_weight=len(y_train[y_train==0]) / len(y_train[y_train==1]),
    max_depth=5,
    learning_rate=0.1
)
```
**Avantages** : Performances supérieures, gestion native du déséquilibre

3. **Ensemble de modèles (Stacking/Voting)**
```python
from sklearn.ensemble import VotingClassifier

ensemble = VotingClassifier(
    estimators=[
        ('lr', LogisticRegression(class_weight='balanced')),
        ('rf', RandomForestClassifier(class_weight='balanced')),
        ('xgb', XGBClassifier(scale_pos_weight=ratio))
    ],
    voting='soft'
)
```

#### 4.2.4 Amélioration du Pipeline de Données

**Feature Engineering recommandé :**
```python
from sklearn.preprocessing import PolynomialFeatures

# Interactions entre variables
poly = PolynomialFeatures(degree=2, interaction_only=True)

# Intégration dans le pipeline
numeric_poly = Pipeline([
    ("imputer", SimpleImputer(strategy="mean")),
    ("poly", PolynomialFeatures(degree=2)),
    ("scaler", StandardScaler())
])
```

**Feature Selection :**
```python
from sklearn.feature_selection import SelectKBest, f_classif

# Sélection des k meilleures features
selector = SelectKBest(score_func=f_classif, k=10)

# Ajout au pipeline
preprocessor = ColumnTransformer([
    ("num", numeric_poly, NUM_COLS),
    ("cat", categorical, CAT_COLS)
])

full_pipeline = Pipeline([
    ("preprocess", preprocessor),
    ("feature_selection", selector),
    ("model", log_reg)
])
```

#### 4.2.5 Validation Croisée Stratifiée
```python
from sklearn.model_selection import StratifiedKFold

# Garantit la représentation des classes dans chaque fold
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

grid_search = GridSearchCV(
    estimator=model,
    param_grid=param_grid,
    cv=skf,  # Au lieu de cv=5
    scoring='f1_macro'
)
```
**Justification** : Essentiel pour datasets déséquilibrés, évite les folds sans classe minoritaire

### 4.3 Plan d'Action Recommandé

**Phase 1 - Court terme (Gains rapides) :**
1. Implémenter `class_weight='balanced'` dans la régression logistique
2. Changer la métrique de Grid Search vers F1-Score macro
3. Utiliser StratifiedKFold pour la validation croisée
4. Ajuster le seuil de décision via courbe Precision-Recall

**Phase 2 - Moyen terme (Amélioration substantielle) :**
1. Collecter plus de données (objectif : 500+ observations)
2. Appliquer SMOTE pour générer des exemples synthétiques de classe 0
3. Tester Random Forest et XGBoost avec pondération
4. Implémenter une analyse exploratoire approfondie (EDA)

**Phase 3 - Long terme (Optimisation avancée) :**
1. Feature engineering basé sur la connaissance métier
2. Ensemble learning (combinaison de modèles)
3. Hyperparameter tuning avec Bayesian Optimization (plus efficace que Grid Search)
4. Monitoring en production avec drift detection

### 4.4 Synthèse Finale

Ce projet illustre un piège classique du machine learning : **des métriques apparemment acceptables (65% d'accuracy) masquant un modèle défaillant**. L'analyse approfondie révèle que le modèle a appris une stratégie triviale non utilisable en production.

**Points positifs :**
- Pipeline de prétraitement bien structuré et reproductible
- Approche méthodique (Grid Search, validation croisée)
- Code modulaire et maintenable

**Enseignements clés :**
1. L'accuracy seule est insuffisante pour évaluer un modèle
2. Le déséquilibre de classes doit être traité dès la conception
3. L'analyse de la matrice de confusion est indispensable
4. Un modèle simple (C=0.001) n'est pas toujours meilleur

**Recommandation finale :**  
Avant tout déploiement, implémenter au minimum les solutions de Phase 1, viser un **F1-Score macro > 0.60** et un **rappel sur classe 0 > 0.50** pour garantir l'utilité opérationnelle du modèle.
