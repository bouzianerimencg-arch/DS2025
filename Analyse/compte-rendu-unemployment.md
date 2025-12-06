# Compte rendu du notebook *Unemployment.ipynb*

## Objectif du notebook
- Présenter le contexte de l’étude du chômage (source des données, période couverte, pays/région étudiée).
- Formuler les questions principales : évolution du taux de chômage, comparaison entre groupes (sexe, âge, région), et facteurs explicatifs possibles.

## Données utilisées
- Description de la source de données (institution statistique, organisme international, etc.).
- Variables principales : taux de chômage, période (année/trimestre/mois), caractéristiques socio‑démographiques (âge, sexe, région, niveau d’éducation, etc.).
- Bref rappel des traitements préalables : nettoyage des données, gestion des valeurs manquantes, filtrage éventuel.

## Méthodologie
- Outils utilisés : Python, bibliothèques (pandas, numpy, matplotlib/seaborn, etc.).
- Types d’analyses effectuées :
  - Statistiques descriptives (moyenne, médiane, écart‑type, minimum/maximum).
  - Visualisations (séries temporelles, histogrammes, boxplots, graphiques par catégorie).
  - Éventuelle modélisation (régression ou autre) pour expliquer le taux de chômage.

## Résultats principaux
- Tendance générale du chômage sur la période (hausse, baisse, stabilité).
- Différences majeures entre groupes (par sexe, âge, région, ou autre segmentation pertinente).
- Points marquants mis en évidence par les graphiques (pics, creux, ruptures de tendance, saisons).

## Interprétation et discussion
- Interprétation économique des évolutions observées (crises, réformes, chocs externes, etc.).
- Limites de l’analyse :
  - Qualité ou granularité des données.
  - Absence de certaines variables explicatives.
- Pistes d’analyses complémentaires ou d’amélioration (ajout d’autres données, modèles plus avancés).
- df = pd.read_csv("/kaggle/input/global-youth-unemployment-dataset/youth_unemployment_global.csv")

plt.savefig("unemployment_trend.png", dpi=150, bbox_inches="tight")

## Résultats principaux

### Évolution temporelle du chômage

![Évolution du taux de chômage](img/unemployment_trend.png)

### Comparaison par groupe d’âge

![Taux de chômage par groupe d’âge](img/age_unemployment.png)


### Tendance générale du chômage

![Évolution du taux de chômage](img/unemployment_trend.png)

Le graphique montre la tendance du taux de chômage sur la période étudiée.

### Différences par groupe

![Taux de chômage par groupe d’âge](img/age_unemployment.png)

Ce graphique illustre les écarts de chômage entre classes d’âge.

## Conclusion
- Rappel synthétique de ce que l’étude montre sur l’évolution du chômage.
- Enseignements clés pour la prise de décision ou pour des travaux futurs.
