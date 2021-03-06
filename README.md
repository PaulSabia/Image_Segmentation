# Image_Segmentation

## Objectif du projet 

L’IA est aujourd’hui omniprésente dans la littérature scientifique de l’imagerie médicale, d’autant plus depuis le développement de nouveaux algorithmes appelés réseaux de neurones convolutifs. En effet, à ce jour, l’IA est très utile dans le domaine de l’imagerie, sur deux volets : la classification des images et la segmentation des organes.

Pour ce projet, nous appliquerons la segmentation sur des images de microcircuits neuronaux de la mouche *Drosophila melanogaster*. Ces images sont tirés de l'article scientifique *An Integrated Micro- and Macroarchitectural Analysis of the Drosophila Brain by Computer-Assisted Serial Section Electron Microscopy* qui présente les avancées dans l’étude des microstructures neurophiles afin d’établir une comparaison entre vertébrés et insectes.

## Les données 

Pour ce projet, le dataset est constitué de 30 images de train, 30 images de test, ainsi que 30 images labels correspondantes aux images d'entrainement. Nous appliquerons la data augmentation agin de grossir notre dataset et obtenir un modèle plus pertinent. 

**Image original**

![](Images/original.png)

**Image label**

![](Images/label.png)

## Data Augmentation

Pour la data augmentation, nous faisons le choix d'utiliser le module **skimage**. Nous aurions également pu utiliser *ImageDataGenerator()* de **Keras**, cependant cette méthode nous limite. En effet, lors de l'utilisation de cette fonction, seul les images modifiées sont utilisées pour l'entrainement et non les originales.

Nous optons pour un flip horizontale, ainsi qu'une transformation affine de chaque image. Grâce à cette méthode nous passons de 30 à **90 images d'entrainement**. 

**exemple de transformation affine :**

![](Images/affinetransform.PNG)

## Le Modèle 

Pour le modèle nous choisissons l'architecture Unet car il peut reconstruire l'image. Unet est utilisée dans la segmentation d'imagerie médical et plus particulièrement les images de microscopie biologique. 

Dans la segmentation, nous devons reconstruire l'image à partir du vecteur de caractéristiques créé par CNN :

![](Images/unet.PNG)

L'architecture ressemble à un **«U»** et contient deux chemins : **Compression** et **Expansion**.

La partie **Compression** permet de capturer le contexte dans l'image. Nous avons des couches de convolution, des couches de max pooling. Le nombre de filtre double après chaque bloc afin que l'architecture puisse apprendre les structures complexes.

Le deuxième chemin, **Expansion** symétrique, est utilisé pour permettre une localisation précise à l'aide de convolutions transposées. La convolution transposée est le processus opposé d'une convolution normale.

## Résultats

Au bout de **100 epochs**, nous obtenons une précision d'environ **84%** sur les données de validation.

**Courbe accuracy :**

![](Images/accuracy.PNG)

**Courbe loss :**

![](Images/loss.PNG)

## Test du Modèle

![](Images/predictions.PNG)

La prédiction de gauche est réalisée avec le modèle sans data augmentation contrairement à l'image de droite. Nous pouvons remarquer qu'avec une data augmentation nous obtenons un résulat légèrement plus net.

## Conclusion

Notre modèle **Unet** segmente correctement nos images et nous donne des **résultats satisfaisants**. Nous avons pu remarquer l'utilité de la data augmentation qui nous donne de meilleurs résulats. 
