# Abstract

# Introduction
## Problématique - dans la vie quotidienne
![Graphique cantité de déchets](/images/graphique_quantite_dechets.png)
Chaque année, les États-Unis produisent plus de 250 millions de tonnes de déchets ménagers. Environ un tiers est recyclé ou composté, le reste étant soit incinéré, soit enterré dans des terrains de décharge. Des études montrent que nous pourrions réutiliser plus de 70% des déchets enfouis dans la terre, notamment des matériaux tels que le verre, le métal ou le papier. En recyclant les déchets métalliques par exemple, nous consommons jusqu'à 95% moins d'énergie que de les extraire et de les transformer depuis leur forme naturelle. Même si en Europe les choses semblent un peu meilleures, car le pourcentage de déchets ménagers recyclés ou compostés est d’environ 46% (ou de 54% en Belgique), cela ne représente que la moitié de la quantité produite [2]. Contrairement à cela, de nombreux pays en développement n’ont pas de système de recyclage mis en place et même certains qui ont un indice de développement humain élevé déclarent avoir un pourcentage de déchets ménagers recyclés proche de zéro. (1% en Turquie et au Chili) [3, 4]. Ces pourcentages moyens qui sont relativement faibles, comparés au taux de recyclage cible de 75%, empêchent à l'objectif actuel de l'humanité d’avoir un développement durable , en réduisant les réserves naturelles de certaines ressources, telles que les métaux, ou en créant d'énormes décharges générant des quantités considérables des gaz à effet de serre et autres.
## Le facteur humain
Une méthode possible pour augmenter la quantité de déchets recyclés ou compostés est de créer un meilleur système de recyclage, car même dans les pays où un système de collecte sélective de déchets est mis en place, il est sujet aux erreurs humaines. La contamination des lots collectés par d'autres matériaux et substances à cause d'erreurs humaines dans la classification des matériaux pourrait avoir un impact important sur la quantité totale de matériaux recyclés et sur la qualité du produit secondaire [4]. 
![Types de platique](/images/types_de_plastique.png)
Même si aucun rapport officiel à grande échelle présentant la quantité de déchets classés par erreur ne puisse être trouvé, différentes sources non officielles s'accordent sur un pourcentage des déchets plastiques totale mal classées compris entre 20 et 40% selon les pays européens, et ce nombre peut aller au-dessus de 60% en Australie. Globalement, à peu près 70% de déchets se retrouvent dans la bonne catégorie de recyclage, selon les mêmes sources non officielles. Ceci motive l’idée de créer un système de tri automatique des déchets, qui trie les déchets à la source afin d’éviter le problème de contamination.
# Méthodologie 
## Computer vision - vision par l'ordinateur
![Diagramme displicines](/images/diagramme_disciplines.png)
Le domaine d'étude des éléments d'une image à l'aide d'un ordinateur s'appelle la vision par ordinateur et se situe au croisement de multiples disciplines différentes: physique (pour l'optique et la formation d'images), biologie et psychologie (comprendre comment le cerveau traite l'information visuelle), informatique , mathématiques et ingénierie. Il est apparu pour la première fois dans les années 1960 [5], puis l’idée des réseaux de neurones convolutionnels a été développée quelques décennies plus tard [6]. 
![Graphique evolution puissance de calcul](/images/graphique_evolution.png)
En raison de leur forte demande en puissance de calcul, la popularité des CNN n'a augmenté de manière substantielle qu'à la fin du troisième millénaire, lorsque le développement des GPU (processeurs graphiques) a réduit le temps de calcul de ces algorithmes grâce à la programmation parallèle et à un grand nombre de noyaux. C’est aussi le moment où de grands ensembles de données étiquetées sont disponibles sur (et grâce à l') Internet. Environ une décennie plus tard, en 2012, le taux d'erreur des réseaux de neurones convolutionnels a diminué (leur précision a monté en flèche) grâce au développement de l'architecture AlexNet.
## Les réseaux de neurones
En commençant par ce qui est un réseau neuronal artificiel, nous pouvons l'expliquer comme suit: un réseau neuronal artificiel est un agrégat de plusieurs algorithmes d'apprentissage automatique travaillant en tandem pour traiter des entrées de données complexes, dans notre cas, des images. 
![Réseaux de neurones artificiels](/images/reseaux_neurones.png)
Plus généralement, un réseau de neurones est un modèle du cerveau humain extrêmement simplifié, composé de neurones artificiels, généralement structurés en plusieurs couches, et d'un ensemble de fonctions reliant ces neurones, l'analogie de la synapsis. La force de ce système est qu’il n’est pas nécessaire de programmer des règles spécifiques aux tâches, car le système apprend par lui-même en analysant des exemples déjà connus. Mais c'est la définition d'un réseau de neurones normal. Le mot convolutif, en informatique, désigne une sorte de fonction qui mappe un tuple de séquences dans une séquence de tuples. Dans ce cas, la différence fondamentale entre un tuple et une collection est que le premier tient compte de l’ordre, tandis que la dernière ne le fait pas. 
![Réseaux de neurones convolutifs](/images/reseaux_neurones_conv.png)
En réunissant les choses, nous pouvons dire qu'un réseau de neurones convolutifs fonctionne en recherchant des modèles dans une image.
## Le jeu de données
La collection d'images, le jeu de données que nous avons utilisé pour ce projet est identique à celui du projet Classification of Trash for Recyclability Status et est composée de 2527 images, classées en 6 classes, correspondant aux six catégories de poubelle aux États-Unis: carton, papier, verre, métal, plastique et déchets. 
![Catégories de déchets](/images/categories.png)
Pour utiliser le même ensemble de données en Belgique, les classes carton et papier et plastique et métal doivent être fusionnées dans deux autres classes, mais cela peut se faire facilement au moment de la prédiction. De plus, afin d’accélérer le temps de traitement et d’éliminer les différences de résolution entre les images, puisqu’une partie a été prise avec un appareil photo de 8 mp et une partie avec un appareil photo de 12 mp, nous avons réduit leur taille, pour que le plus long  bord ait 1024 pixels (réduisant ainsi l’entrée du réseau environ 16 fois). Cette valeur est considérablement plus grande que la résolution 299 x 299 utilisée par Inception et 224 x 224 utilisée par VGG, mais nous a permis de tester différents modèles et de jouer avec des techniques d'accroissement de données telles que le zoom et la rotation, sans perte de qualité de l'image.
## Augumentation de données
Étant donné que notre ensemble de données contenait un petit nombre d'images, au moins en comparaison avec l'ensemble de données ImageNet, qui était  utilisé initialement pour entrainer les modèles et qui compte actuellement plus de 14 millions d'images, nous avons utilisé quelques techniques d'accroissement de données pour l'augmenter artificiellement. Pour le modèle Inception, nous avons utilisé les transformations: cisaillement, zoom, retournement horizontal, rotation, décalage en largeur et en décalage en hauteur.
![Augumentation de données](/images/transformations.png)
# Les architectures des réseaux des neurones convolutifs 
La création d'un modèle d'apprentissage approfondi personnalisé nécessite de nombreuses ressources de calcul et de nombreuses données d'entrainement. Cependant, il existe déjà des modèles tels que Inception, VGG, DenseNet, ResNet, etc., qui fonctionnent assez bien pour classer les images de différentes catégories.
Étant un bon compromis entre la précision et le nombre d'opérations, on a choisi d’utiliser un modèle pré-entrainé Inception v3 [7] et un modèle VGG16 [8] pour comparaison.
![Les modeles des reseaux de neurones](/images/modeles.png)
La création d'un modèle d'apprentissage approfondi personnalisé nécessite de nombreuses ressources de calcul et de nombreuses données d'entrainement. Cependant, il existe déjà des modèles tels que Inception, VGG, DenseNet, ResNet, etc., qui fonctionnent assez bien pour classer les images de différentes catégories. 
## Inception V3
![Inception V3](/images/inceptionV3.png)
InceptionV3 est le premier modèle que nous avons abordé dans notre projet. Son architecture a pour objectif de réduire l’utilisation des ressources informatiques dans le cadre d’une classification très précise des images, en augmentant la taille et la profondeur, et en utilisant la faible densité des couches. Il dispose de 42 couches profondes et utilise des images avec une résolution de 299 par 299.
Ce modèle est composé de deux parties:
- La partie qui extrait des caractéristiques composé d’un réseau de neurones convolutifs.
- La partie pour la classification composé de couches entièrement connectées et softmax.
## VGG16
![VGG16](/images/vgg16.png)
## Les couches de neurones
Ces differents modeles sont constitués de plusieurs types de couches combinées.
### La couche de convolution 
Elle est la composante clé de réseaux de neurones convolutifs. Elle est utilisée pour repérer la présence d’un ensemble de motifs dans les images.
![Couche de convolution](/images/convolution.png)
![Resultat après le filtrage](/images/convolution2.png)
### La couche de pooling
Elle reçoit plusieurs feature maps (descripteurs) et réduit leur taille, tout en conservant leurs caractéristiques importantes.
![Pooling](/images/pooling.jpg)
### La couche de correction ReLU 
Elle joue le rôle de fonction d’activation en remplaçant toutes les valeurs négatives reçues en entrée par des zéros.
![ReLU](/images/relu.png)
### La couche fully-connected
Elle constitue tout le temps la dernière couche d’un réseau de neurones. Elle reçoit un vecteur en entrée et donne en sortie un nouveau vecteur de taille différente, contenant les probabilités que l’image analysée appartient à une certaine classe et obtenu en appliquant une combinaison linéaire aux valeurs reçues. 
![Fully_connected](/images/fully_connected.png)
# Transfer learning
L’apprentissage par transfert fonctionne en utilisant des modèles déjà entrainés sur de plus grands jeux de données pour, en même temps, réduire le temps d’entrainement et améliorer la détection. Dans ce contexte, on va entrainer seulement les dernières couches pour les adapter à la nouvelle liste des classes. 

Une autre manière de diminuer le temps d’entrainement est en utilisant un GPU :
Intel Xeon Quad 24GB RAM: 13h08
GeForce RTX 2070 8GB: 1h42

Pendant le training, les premières couches des réseaux de neurones convolutifs apprennent à identifier les motifs généraux. Cette partie d’extraction des caractéristiques peut être après réutilisée pour construire un nouveau modèle.

L’entrainement initial de ces deux modèles (IncetionV3 et VGG16 )est fait en utilisant le dataset ImageNet qui contient approx. 14 million des images appartenant aux 1000 classes.

# Résultats
## Le modèle VGG16
Avec le modèle VGG16 nous obtenons une précision catégorique d’environ 51%.
Certaines classes de déchets sont très mal prédites.
La mauvaise prédiction du verre et du plastique s’explique par le fait que les images dans le dataset se ressemblent beaucoup. On peut améliorer la précision de ce modèle en utilisant l’apprentissage par transfert – 85±3%
![](/images/glass_plastic.png)
## Le modèle Inception v3 pré-entrainé
Pour le système de recyclage américain (6 catégories), 80% des prédictions sont bonnes.
Pour le système de recyclage belge (4 catégories), 85% des prédictions sont bonnes.
Une précision moyenne d’approximativement 81±2%, ce qui correspond à nos attentes. La variation de la précision dépend du jeu d’images utilisées pour tester le modèle.
