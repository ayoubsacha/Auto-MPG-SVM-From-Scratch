# Prédiction de la consommation automobile — Auto MPG

Projet de machine learning consacré à la prédiction de la consommation de véhicules à partir du jeu de données **Auto MPG**. Le rapport est présenté dans un notebook Jupyter rédigé en français. Il combine analyse exploratoire, explication des choix méthodologiques, implémentations réalisées à partir de zéro, expériences de robustesse et comparaisons avec des références scikit-learn.

## Objectifs

Le projet étudie deux tâches complémentaires à partir de la variable `mpg` :

- **Classification** : répartir les véhicules en trois classes de consommation, avec des seuils par quantiles et à largeur égale.
- **Régression** : prédire la valeur continue de `mpg` avec un SVR linéaire à perte ε-insensible.

Il examine aussi l’estimation des puissances moteur manquantes (`horsepower`) et l’influence de perturbations sur les cibles d’entraînement.

## Méthodes et contenu

Le notebook développe et explique les éléments suivants :

- Un standardiseur réutilisable `MyStandardScaler`, codé à la main, utilisant l’écart-type de population (`ddof=0`). Les statistiques sont apprises sur l’entraînement puis réutilisées pour transformer validation et test.
- Une imputation KNN faite maison : calcul de la distance euclidienne, mise à l’échelle indépendante des variables utilisées pour les distances, sélection des voisins et moyenne de leurs puissances.
- Un SVM linéaire entraîné avec la perte charnière, étendu aux trois classes par la stratégie un-contre-tous.
- Un SVM RBF multiclasse avec noyau gaussien et optimisation SMO écrits dans le notebook.
- Un SVR linéaire ε-insensible dont le problème dual est optimisé par une méthode proximale accélérée implémentée dans le notebook.
- Une validation croisée stratifiée à trois plis pour sélectionner les paramètres `C`, `gamma` et `epsilon`, sans utiliser le test pour le réglage.
- Une étude du bruit gaussien ajouté uniquement aux cibles d’entraînement et une étude de contamination de 5 à 20 % de ces cibles par des valeurs de ±15 mpg. Les évaluations utilisent des cibles de test propres.

Les méthodes scikit-learn sont utilisées comme références de comparaison et pour les utilitaires de soutien autorisés, notamment le partage des données et les métriques. Elles ne remplacent pas les implémentations requises de l’imputation KNN, de la standardisation, des SVM, du SVR ou de leurs optimiseurs.

## Méthodologie

Le notebook sépare les données en entraînement et test, avec une stratification fondée sur des tiers provisoires de `mpg` et la présence de valeurs manquantes dans `horsepower`. Ces bandes servent uniquement à répartir les observations. Les valeurs `mpg` du test ne servent ni à fixer les seuils finaux des classes, ni au réglage des modèles, ni à l’ajustement des transformations; le test est utilisé pour l’évaluation finale. Les traitements de validation croisée sont ajustés pli par pli.

Les sorties enregistrées dans le notebook proviennent d’une exécution réelle. Les conclusions distinguent les résultats de validation croisée, les mesures sur le test et la variabilité des expériences répétées. Les résultats restent liés à ce jeu de données et à cette partition.

## Prérequis

- Python **3.11 recommandé**.
- Git.
- Une connexion Internet au premier chargement du jeu de données par `seaborn.load_dataset("mpg")`, sauf si les données sont déjà en cache.

## Cloner et installer

Clonez le dépôt puis ouvrez son dossier :

```bash
git clone https://github.com/ayoubsacha/Auto-MPG-SVM-From-Scratch.git
cd Auto-MPG-SVM-From-Scratch
```

Créez et activez un environnement virtuel.

### Windows — PowerShell

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### macOS ou Linux

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Lancer le notebook

Depuis la racine du dépôt, avec l’environnement virtuel activé :

```bash
python -m notebook Auto_MPG_SVM.ipynb
```

Dans Jupyter, sélectionnez le noyau Python de `.venv`, puis exécutez les cellules dans l’ordre avec **Run All**. Le téléchargement de `mpg` peut être nécessaire lors de la première exécution. Les expériences répétées et les recherches de paramètres prennent plus de temps que les cellules d’analyse exploratoire.

## Fichiers du dépôt

| Fichier | Rôle |
|---|---|
| `Auto_MPG_SVM.ipynb` | Rapport scientifique, explications, implémentations, expériences, graphiques et sorties enregistrées. |
| `requirements.txt` | Dépendances Python nécessaires pour exécuter le notebook. |
| `README.md` | Présentation du projet et instructions d’installation et d’exécution. |

## Dépendances principales

NumPy, pandas, Matplotlib, Seaborn, scikit-learn, Jupyter Notebook et IPython Kernel. Les versions autorisées sont précisées dans `requirements.txt`.
