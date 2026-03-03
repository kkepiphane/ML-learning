#  Manifold Learning sur Visages : PCA vs LLE
## Visualisation de données haute-dimension avec le dataset Olivetti Faces

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg">
  <img src="https://img.shields.io/badge/Scikit--Learn-1.0+-orange.svg">
  <img src="https://img.shields.io/badge/Status-TP%20Académique-green.svg">
</p>

## Objectifs du TP
- **Numérisation** : Transformer 400 images (64×64) en vecteurs de dimension 4096
- **Visualisation 2D** : Projeter ces données pour identifier des clusters d'individus
- **Comparaison** : Évaluer approches linéaire (PCA) vs non-linéaire (LLE)
- **Optimisation** : Étudier l'influence du paramètre de voisinage (K)

## Dataset : Olivetti Faces
- **400 images** en niveaux de gris (10 par individu)
- **40 sujets** avec variations :
  -  Luminosité
  -  Expressions (sourire/neutre)
  -  Accessoires (lunettes)
  -  Rotation légère

##  Algorithmes Implémentés

### 1. PCA (Principal Component Analysis)
**Approche linéaire** : Maximise la variance globale via les Eigenfaces
-  **Limite** : La rotation d'un visage est non-linéaire → mauvais clustering

### 2. LLE (Locally Linear Embedding)
**Approche non-linéaire** : Préserve les relations de voisinage
-  **Avantage** : "Déplie" la variété des visages → meilleure séparation

### 3. Modified LLE (MLLE)
Version optimisée pour plus de stabilité numérique

## Résultats Visuels

| Méthode   | K   | Résultat           | Qualité    |
|---------  |---  |----------          |---------   |
| PCA       | -   | Mélange complet    | Faible     |
| LLE       | 5   | Fragmentation      | Bruité     |
| LLE       | 15  | Clusters distincts | Optimal    |
| LLE       | 50  | Fusion des classes | Trop lissé |
| MLLE      | 15  | Très net           | Excellent  |




## Bibliothèques utilisées
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib import offsetbox
    from sklearn.datasets import fetch_olivetti_faces
    from sklearn.decomposition import PCA
    from sklearn.manifold import LocallyLinearEmbedding

```bash