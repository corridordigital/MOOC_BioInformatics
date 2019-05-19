# MOOC Bio-informatique 

## 1. Semaine 1 - ADN & séquence génomique 

### 1.1. La cellule, atome du vivant 

* Observée pour la première fois sur une fine couche de liège, appelées cellules du fait de leur taille (analogie : la cellule de moine)
* La cellule est l'unité du vivant, elle provient toujours d'une autre cellule. 
* La cellule est fonctionnellement autonome et séparée de l'extérieur par une membrane 
* l'analyse des génomes eucaryotes est bien plus complexe 

### 1.2. Au coeur de la cellule, la molécule d'ADN 

- Crick, Watson, Wilkins 
- Structure inférée grâce aux spectres de diffraction X-rays
- Elle est en lien direct avec le mécanisme de réplication
 
### 1.3. L'ADN code l'info génétique 

- Lire le code génétique = séquencer 
- Génome peut vouloir dire : la molécule d'ADN ou l'ensemble des gènes d'un organisme
- la séquence de 4 nucléotides code pour des acides aminés, constituant des protéines. Elle code aussi pour des signaux d'expressions des gènes 
- L'informatique est la science du traitement auto de l'info
- La bioinfo est donc le traitement auto de l'info bio
- On parle de Mb, Gb, Tb (Méga, Giga, Terabases) pour la taille du génome. L'amibe a bien plus de bases que l'homme 

### 1.4. Qu'est ce qu'un algorithme 

- Suite d'opérations à executer pour résoudre une classe de problèmes
- Propriétés attendues : 
  - Il se termine
  - Il est efficace 
  - Il est pertinent 

### 1.5. Compter les nucléotides

cf. Python notebook (simple)

### 1.6. Contenu en GC & AT des séquences 

- Ces quantités intéressent les biologistes : %GC et %TA et possèdent des interprétations biologiques 
- A-T : 2 liaisons, C-G : 3 liaisons (liaison plus forte)

### 1.7. Promenade sur l'ADN 

- Pas de ponctuation, pas de motifs dans les grosses masses de lettres  
- On a pensé au début à regrouper les lettres en triplets, à calquer des notes dessus
- Ensuite, on a associé à  chaque lettre un vecteur correspondant à une des 4 directions dans le plan. Ceci a donné lieu à un algorithme, le DNA Walk

### 1.8. Changer l'échelle du chemin 

- Le DNA Walk est limité par la résolution d'écran --> Solution : on change l'échelle du chemin. Au lieu de tracer tous les segments, on smooth. 10 segments par ex deviennent un seul, on choisit donc un facteur de compaction
- On a la notion de fenêtre, qui a une longueur variable.  
- Algo: 
  - Une 1ere fonction calcule le nb de A,T,C,G dans la fenêtre considérée 
  - On calcule le nb de pas à faire vers la droite et vers le haut (entiers relatifs)
  - On a les coordonées de l'extrémité du segment obtenu, que l'on trace
  - On déplace la fenêtre
- Cet algo produit des résults qui ont une interprétation biologique comme on va le voir dans la suite 

### 1.9. Prédire l'origine de réplications ?

- On applique l'algo à Borrelia burgdorferi (bacterie)
  - Une majorité de A & de C --> tracé vers le coin sup droit du graphique 
  - Ensuite, rebroussement puis retour à l'origine --> majorité de G & T dans la 2eme partie de la séquence, il y a donc biais de composition en nucléotides !  
  - Explication : cela est du au mécanisme de réplication asymétrique de l'ADN et au mécanisme de progression de l'ADN Polymérase (3' vers 5') au niveau de la fourche de réplication. Tout brin d'ADN est orienté
- On peut prédire l'origine de réplication, grâce à un algo plus quantitatif

### 1.10. Des fenêtres glissantes & recouvrantes 

- L'algo vu précédemment ne marche pas toujours (par ex sur Archea). On voudrait le systématiser, et le rendre quantitatif.
- On va utiliser des fenêtres glissantes & recouvrantes :
  - On calcule le nb de nucléotides & le ratio G/C dans une fenêtre glissante
  - Ratio = (nbG-nbC)/(nbG+nbC) = 0 si même quantité de C & G
  - Cette fenêtre est recouvrante, elle se déplace d'un pas < taille de la fenêtre 
  - On obtient une succession de valeurs réélles, qui permettent de tracer une courbe colinéaire à la séquence
  - On arrive ainsi à voir un point de rupture qui correspond au point de rupture visible sur le graph DNAWalk de Borrelia, et à l'origine de réplication
- 
