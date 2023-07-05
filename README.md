# Journal intime numérique pour psychologue

## Objectif

Ce projet vise à développer un outil pour un psychologue qui conseille à ses patients d'écrire sur un journal intime numérique entre les séances. L'outil doit être capable d'utiliser ces écrits pour aider le psychologue dans son travail sans être obligé de lire chacun des textes.

Le code est divisé en plusieurs notebooks (`1_analyse`, `2_elastiquesearch`, etc.) et utilise un fichier CSV comme base de données initiale, qui a ensuite été modifié pour être envoyé sur Elastic Search.

## partie 1: Analyse des données et premier modèle

A partir du jeu de données et à l'aide la librairie Spacy, vous pouvez même essayez texthero:  notre choix c'est porter sur SPACY 
- étudier la répartition des textes par émotions
- identifiez quels mots sont susceptibles d'être des stopword
- pour chaque sentiment, identifiez les 30 mots les plus courants pour chaque sentiment en dehors des stopwords
- A partir de ces 30 mots, définissez une métrique de proximité entre les sentiments et affichez-la sur une matrice type heatmap.
- Créer deux premiers pre-processing (Bag of words et TF IDF) en gérant les étapes de tokenisation, de gestion de la ponctuation, des émojis, des stopwords, de lemmatisation ou de streaming puis implémenter un modèle de machine learning de scikit learn.

Le rendu du premier de temps se fera dans un notebook nommé `1_analyse`.

## partie 2: Stocker les données avec Elastic Search

### Mise en place
→ Démarrer un container à partir de l’image docker.elastic.co/elasticsearch/elasticsearch:7.17.10
● en mode détaché -d
● monter le volume /usr/share/elasticsearch/data en local
● utiliser le mapping de port -p 9200:9200
● utiliser la variable -e "discovery.type=single-node"
● le nom du container sera --name elastic

→ Visualiser les logs du container 
→ appeler la route racine “/”

### Mapper et importer les données
Poster le mapping d’un index nommé “notes”, contenant :


un champ ‘confidence” qui est un float

Alimenter l’index “notes” à l’aide du jeu de données et de la librairie Faker. 

Bonus: Mettez en place un pipeline utilisant le modèle TF-IDF que vous avez développé avec scikit-learn pour remplir les champs “emotion” et “confidence”.

“patient_lastname”: Faker
“patient_firstname”: Faker
text”: CSV
“date”: Faker
“patient_left”: Faker
“emotion”: Model
‘confidence”: Model

Le code pour cette partie se trouve dans le notebook `2_elastiquesearch`.

### Requêtes a effectuer pour TESTER la BDD

1- En recherchant dans la base elastic search, aboutissez à un data frame permettant d’afficher la répartition des sentiments des textes pour un patient (nom/prénom)

2- Élaborez une matrice de sentiments contradictoire (toujours en utilisant la base elastic search.
On veut savoir parmi les documents classifiés comme happy, quel pourcentage contient le mot “sadness”. Puis quel pourcentage contient “fear” …
Et cela pour tous les sentiment.
On représente les résultats dans une HeatMap

3- Pour chacune des étapes du deuil (denial, anger, bargaining, depression, and acceptance) rechercher le nombre de text correspondants à l’aide:
d’une recherche pleine
d’une fuzzy recherche.

4- Rechercher les textes:
qui doivent matcher l’expression “good day” (must)
chez les patients encore en consultation (filter)
qui contiennent si possible “to rest” (should)
qui ne doivent pas avoir seuil de confiance inférieur à 0.5 s’il existe. 
Observer la répartition de ces résultats par sentiment



## partie 3: Utiliser Hugging Face

Hugging Face est une entreprise qui propose des services liés à l'apprentissage automatique, en particulier dans le domaine du traitement du langage naturel (NLP). Parmi les services proposés, on peut citer la mise à disposition de modèles pré-entraînés, la possibilité de fine tuner ces modèles et de les évaluer sur des jeux de données, ainsi que la possibilité de publier ses propres modèles dans le Hub Hugging Face.

Dans cette partie du projet, vous devrez choisir un modèle de classification NLP dans Hugging Face, le fine tuner et l'évaluer sur le jeu de données. Vous devrez ensuite publier le modèle dans le Hub Hugging Face.

## partie 4: Créer une application de Suivi

Dans cette partie du projet, vous devrez créer une application permettant au psychologue de suivre l'évolution des sentiments de ses patients à partir des textes qu'ils ont écrits dans leur journal intime numérique.
