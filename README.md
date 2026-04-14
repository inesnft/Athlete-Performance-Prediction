# Athlete Performance Prediction

English Version below.

## Version francaise

Ce projet analyse des donnees de football europeen (avec un focus important sur l'Angleterre) pour predire la performance des matchs a partir de statistiques disponibles avant ou pendant la rencontre.

Le notebook final du projet est **Model_2nde_half.ipynb**. Les autres notebooks servent principalement a l'exploration des donnees, a la construction progressive des features, et aux essais de modeles.

### Ce que le projet implemente

- Chargement des donnees depuis des CSV locaux et/ou depuis GitHub (format `;`).
- Nettoyage des donnees (gestion des valeurs manquantes, conversion des dates, filtrages par pays).
- Feature engineering avance:
	- variables mi-temps et seconde mi-temps (buts, ecarts, scenario du match),
	- cumuls et moyennes de ligue/saison,
	- rolling averages (forme recente),
	- indicateurs de forme equipe (buts marques/encaisses, points par match).
- Pipelines de pretraitement `scikit-learn` (`SimpleImputer`, `StandardScaler`, `OneHotEncoder`, `ColumnTransformer`).
- Entrainement de plusieurs modeles de regression et classification selon les objectifs:
	- `LinearRegression`, `Ridge`, `ElasticNet`,
	- `RandomForestRegressor`, `HistGradientBoostingRegressor`,
	- approches de classification dans le notebook final (Random Forest, Gradient Boosting, Logistic Regression, SVM).
- Evaluation par metriques (`MAE`, `R2`, accuracy, rapports de classification, matrice de confusion).
- Validation croisee et optimisation d'hyperparametres (`GridSearchCV`, `RandomizedSearchCV`).
- Interpretation des modeles (importance des variables et analyse des residus selon le notebook).

### Detail des notebooks

#### Model_2nde_half.ipynb (notebook final)

- Objectif principal: predire un resultat plus realiste en utilisant les informations de premiere mi-temps (ex: buts en seconde mi-temps et resultat final).
- Construction de nombreuses features temporelles et contextuelles (ligue, saison, forme recente, points, scenario mi-temps).
- Preparation des jeux d'entree/sortie avec attention a la fuite de donnees.
- Entrainement et comparaison de plusieurs modeles de classification.
- Validation croisee (Stratified K-Fold), comparaison inter-modeles, puis fine-tuning des meilleurs candidats.
- Analyse des performances (accuracy, confusion matrix, rapport detaille) et importance des features.

#### Project_only_England.ipynb (exploration + essais)

- Construction d'un sous-dataset Angleterre a partir du dataset europeen.
- EDA de base (volume de matchs, repartition par equipes, inspection des colonnes).
- Tests de pipelines en deux configurations:
	- numerique uniquement,
	- numerique + categoriel (avec OneHotEncoder).
- Comparaison de modeles (Linear Regression, Random Forest, Ridge, ElasticNet), mesure MAE/R2.
- Premiers essais de tuning (GridSearch) et discussion des effets de la haute dimension apres encodage categoriel.

#### Projet_final.ipynb (exploration + benchmark regression)

- Preparation d'un jeu Angleterre et definition de la cible `TotalGoals`.
- Feature engineering de forme recente (moyennes glissantes sur les 5 derniers matchs).
- Benchmark de modeles de regression (`Ridge`, `Random Forest`, `HistGradientBoosting`).
- Optimisation des hyperparametres (GridSearch + RandomizedSearch).
- Analyse post-modele: importance des variables (permutation importance) et analyse des residus.

#### Projet_AAA.ipynb (notebook d'essais)

- Notebook de tests preliminaires sur le dataset europeen.
- Exploration de la structure des donnees (pays, equipes, volume de matchs).
- Visualisations de distribution et premiers tests de selection/filtrage d'equipes.
- Sert de base de reflexion pour orienter les choix de nettoyage et de modelisation dans les notebooks suivants.

### Donnees

Les jeux de donnees sont presents a la racine du projet et dans le dossier `datasets/`.

---

## English Version

This project analyzes European football data (with a strong focus on England) to predict match performance using pre-match and first-half statistics.

The final project notebook is **Model_2nde_half.ipynb**. The other notebooks are mainly for data exploration, feature engineering experiments, and model trials.

### What is implemented

- Data loading from local CSV files and/or GitHub (semicolon-separated format).
- Data cleaning (missing values, date conversion, country filtering).
- Advanced feature engineering:
	- first-half and second-half variables (goals, differences, game state),
	- league/season cumulative indicators,
	- rolling averages (recent form),
	- team form indicators (goals scored/conceded, points per match).
- `scikit-learn` preprocessing pipelines (`SimpleImputer`, `StandardScaler`, `OneHotEncoder`, `ColumnTransformer`).
- Training of multiple regression and classification models depending on the objective:
	- `LinearRegression`, `Ridge`, `ElasticNet`,
	- `RandomForestRegressor`, `HistGradientBoostingRegressor`,
	- classification approaches in the final notebook (Random Forest, Gradient Boosting, Logistic Regression, SVM).
- Evaluation with metrics (`MAE`, `R2`, accuracy, classification reports, confusion matrix).
- Cross-validation and hyperparameter tuning (`GridSearchCV`, `RandomizedSearchCV`).
- Model interpretation (feature importance and residual analysis, depending on notebook).

### Notebook details

#### Model_2nde_half.ipynb (final notebook)

- Main objective: build a more realistic prediction setup using first-half information (for second-half goals and final outcome).
- Extensive temporal/contextual feature engineering (league, season, recent form, points, halftime scenario).
- Careful input/target preparation with leakage-aware feature selection.
- Training and comparison of multiple classification models.
- Stratified cross-validation and fine-tuning of best candidates.
- Performance analysis (accuracy, confusion matrix, detailed classification report) and feature importance.

#### Project_only_England.ipynb (exploration + experiments)

- Builds an England-only subset from the European dataset.
- Basic EDA (match volume, team distribution, column inspection).
- Pipeline tests in two settings:
	- numeric-only,
	- numeric + categorical (with OneHotEncoder).
- Model comparisons (Linear Regression, Random Forest, Ridge, ElasticNet), using MAE/R2.
- Early hyperparameter tuning tests (GridSearch) and discussion of high-dimensional categorical encoding effects.

#### Projet_final.ipynb (exploration + regression benchmark)

- Prepares an England dataset and defines `TotalGoals` as target.
- Recent-form feature engineering (rolling means over last 5 matches).
- Regression benchmark (`Ridge`, `Random Forest`, `HistGradientBoosting`).
- Hyperparameter tuning (GridSearch + RandomizedSearch).
- Post-model analysis: permutation feature importance and residual diagnostics.

#### Projet_AAA.ipynb (trial notebook)

- Preliminary experiments on the European dataset.
- Data structure exploration (countries, teams, match volume).
- Distribution visualizations and early filtering/selection tests.
- Serves as a foundation for cleaning and modeling decisions used in later notebooks.

### Data

Datasets are available at the project root and in the `datasets/` folder.
