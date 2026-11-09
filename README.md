# Prédiction Auto MPG avec des SVM

Ce projet étudie la prédiction de la consommation automobile à partir du jeu de données Auto MPG. Il traite `mpg` comme une cible de classification en trois classes et comme une cible continue de régression. Le notebook est rédigé en français et contient les explications théoriques, les implémentations faites maison, les expériences et les comparaisons de référence avec scikit-learn.

## Prérequis

- Python 3.11 recommandé (Python 3.10 à 3.12 devrait convenir aux dépendances listées).
- Une connexion Internet au premier chargement du jeu de données Seaborn, sauf si celui-ci est déjà présent dans le cache local.

## Installation

Depuis ce dossier, créez et activez un environnement virtuel :

```bash
python -m venv .venv
```

Sous Windows PowerShell :

```powershell
.\.venv\Scripts\Activate.ps1
```

Sous macOS ou Linux :

```bash
source .venv/bin/activate
```

Installez ensuite les dépendances :

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Lancer le notebook

```bash
python -m notebook Auto_MPG_SVM.ipynb
```

Dans l’interface Jupyter, choisissez le noyau Python de l’environnement créé, puis exécutez les cellules dans l’ordre avec **Run All**. Le chargement de `seaborn.load_dataset("mpg")` peut nécessiter Internet lors de la première exécution.

## Organisation du notebook

Le notebook présente les données et l’analyse exploratoire, justifie le choix des variables, puis implémente `MyStandardScaler` et l’imputation KNN sans standardiseur ni imputeur intégrés. Il compare ensuite les discrétisations de la cible, entraîne un SVM linéaire, un SVM RBF multiclasse un-contre-tous et un SVR linéaire ε-insensible faits maison, et évalue ces résultats face aux références scikit-learn. Une validation croisée à trois plis choisit les grilles C, γ et ε sans consulter le test; le notebook compare aussi les deux discrétisations et utilise une séparation stratifiée. Deux études répétées évaluent, sur le test propre, le bruit gaussien des cibles d’entraînement et la contamination de 5 à 20 % des cibles par des anomalies de ±15 mpg, avec comparaison à `LinearRegression`. Les sorties du notebook sont calculées à l’exécution; aucune performance n’est inventée à l’avance.
