#  Manifold Learning sur Visages : PCA vs LLE
## Visualisation de données haute-dimension avec le dataset Olivetti Faces

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg">
  <img src="https://img.shields.io/badge/Scikit--Learn-1.0+-orange.svg">
  <img src="https://img.shields.io/badge/Status-TP%20Académique-green.svg">
</p>

# Étude de la Variété des Visages : PCA vs LLE (Olivetti Faces)

  Ce projet explore la réduction de dimensionnalité appliquée à la reconnaissance faciale. L'objectif est de comparer une approche linéaire (**PCA**) avec une approche non-linéaire (**Locally Linear Embedding - LLE**) pour visualiser la structure intrinsèque du dataset **Olivetti Faces**.

## Objectifs du TP
- **Extraction de caractéristiques** : Transformer des images de 64x64 pixels en vecteurs de dimension 4096.
- **Visualisation 2D** : Projeter ces données de haute dimension dans un plan pour identifier des regroupements (clusters).
- **Analyse de Variété (Manifold Learning)** : Démontrer que les visages suivent une structure non-linéaire (pose, expressions).
- **Optimisation** : Étudier l'influence du nombre de voisins (K) et tester la variante **Modified LLE (MLLE)**.

## Le Dataset : Olivetti Faces
Le dataset, provenant des [AT&T Laboratories Cambridge](https://scikit-learn.org), contient :
- **400 images** en niveaux de gris.
- **40 individus** différents (10 images par personne).
- Des variations de lumière, d'expressions faciales (sourire/neutre) et de détails (lunettes/sans lunettes).

## Méthodologie & Algorithmes

### 1. PCA (Principal Component Analysis)
La PCA cherche à maximiser la variance globale. Elle identifie les **Eigenfaces** (vecteurs propres).
- **Limites** : Elle peine à séparer les individus car la rotation d'un visage est une transformation non-linéaire.

### 2. LLE (Locally Linear Embedding)
Le LLE préserve les relations de voisinage local.
- **Hypothèse** : Chaque visage est une combinaison linéaire de ses K voisins les plus proches.
- **Avantage** : Il "déplie" la variété des données pour mieux isoler les identités.

### 3. Modified LLE (MLLE)
  Une version optimisée pour plus de stabilité numérique, offrant une projection plus nette et robuste aux bruits.

## Installation & Utilisation
    Le projet utilise la bibliothèque [Scikit-Learn](https://scikit-learn.org).


    pip install numpy matplotlib scikit-learn


## Bibliothèques utilisées
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib import offsetbox
    from sklearn.datasets import fetch_olivetti_faces
    from sklearn.decomposition import PCA
    from sklearn.manifold import LocallyLinearEmbedding

#### Pour simplifier, l'objectif unique du TP est de répondre à cette question :
  Est-il possible de classer 400 photos de visages sur une simple feuille de papier (2D) tout en gardant les personnes identiques regroupées ensemble ?

```bash