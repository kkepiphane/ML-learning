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

## Résultats Marquants

| Méthode | Type | Observation Principale |
|---------|------|------------------------|
| PCA     | Linéaire | Données compressées au centre, mélange des classes. |
| LLE (K=15) | Non-Linéaire | Formation de trajectoires logiques (pose/sourire). |
| MLLE | Optimisé | Meilleure séparation des 40 clusters d'individus. |

## Concepts Clés Abordés

- **Vecteurs Propres** : Utilisés comme coordonnées de projection dans le LLE.
- **Valeurs Propres** : Mesurent l'erreur de reconstruction (on cherche à minimiser les plus petites).
- **Hyperparamètre K** : Équilibre entre structure locale et globale.

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


**Question fondamentale :** Est-il possible de classer 400 photos de visages sur une simple feuille de papier (2D) tout en gardant les personnes identiques regroupées ensemble ?

## Problématique et Sous-objectifs

### 1. Passer de l'Image au Chiffre (Numérisation)
Une image de 64x64 pixels est illisible pour un ordinateur tel quel.

- **L'étape** : Transformer chaque photo en un vecteur de 4096 nombres.
- **Le défi** : On a trop d'informations (4096 dimensions). C'est impossible à visualiser.

### 2. Comparer deux "Manières de Voir" (Linéaire vs Non-Linéaire)
C'est le cœur de votre recherche. Vous testez deux théories :

**La théorie PCA (Linéaire)** : On pense que les visages changent de façon simple (ex: juste plus ou moins de lumière). On cherche les "Eigenfaces" (les traits dominants).
- *Résultat attendu* : C'est souvent décevant car un visage qui tourne n'est pas linéaire.

**La théorie LLE (Non-Linéaire)** : On pense que pour reconnaître quelqu'un, il faut regarder ses voisins proches (les photos qui lui ressemblent presque trait pour trait). On essaie de "déplier" la peau du visage pour l'étaler à plat.
- *Résultat attendu* : C'est beaucoup plus précis pour séparer les 40 individus.

### 3. Maîtriser le curseur de la "Localité" (Le paramètre K)
L'objectif est d'apprendre à régler l'algorithme :
- Si je regarde **trop peu de voisins** (K petit), je ne vois pas la forme globale.
- Si je regarde **trop de voisins** (K grand), je mélange tout le monde.
- **Le but** : Trouver le "juste milieu" (souvent K=15) où chaque individu forme un petit groupe distinct sur votre graphique.
