---
title: Suivi du projet
---

<style>
    @media screen and (min-width: 76em) {
        .md-sidebar--primary {
            display: none !important;
        }
    }
</style>

# Suivi de projet

## Semaine 1-2 (12–25 janvier)

### Activités : État de l'art et plannification du projet

#### Travail réalisé
- A fait l'état de l'art sur les protein Language Models (ESM2) et sur la famille des Cytochromes P450
- A recherché des bases de données à utiliser
- A produit un premier prototype conceptuel 
- A identifié une méthodologie pour constituer les jeux d'entrainement et de test
- A plannifié le projet

#### Difficultés rencontrées
N-A
#### Décisions et ajustements
Faire une première ébauche puis la raffiner dans une deuxième itération. 

## Semaine 3-4(26–8 Fév)

### Activités : Constitution des datasets 
#### Travail réalisé
- A constitué les trainsets et testsets
- A nettoyé les données et assuré la reproductibilité 
- A présenté et a justifié les choix au superviseur

#### Difficultés rencontrées
Les séquences contenues dans les clusters UniRef90 et UniRef50 sont fait à partir de l'ensemble des séquences disponibles   
-> on peut avoir des séquences d'hominidés dans les clusters et potentiellement du data leakage. 

#### Décisions et ajustements

Prendre UniRef100 pour le moment et bien décrire la méthodologie afin d'être plus stringent lors de la deuxième itération + assurer la reproductibilité des datasets.


## Semaine 5-6 (8–22 février)

### Activités : Implémentation du finetuning
#### Travail réalisé
- A Étudié le fonctionnement de ESM2
- Implémenté le code pour le finetuning 
- A automatisé les scripts pour le finetuning sur ComputeCanada
- Testé le fonctionnement et des paramètres



#### Difficultés rencontrées
Problèmes avec la libraire pyarrow sur ComputeCanada 
Queueing long sur ComputeCanada si 2 gpu sont demandés
#### Décisions et ajustements
Problèmes réglés pour la librarie Arrow.  
Pour les GPUs, un seul sera utilisé (queueing court) + décisions de se concentrer sur le trainset de mammifères car plus petit (seulement 5h d'entrainement)

Pour la perennité du projet :  
- ajouter l'outil MLflow pour assurer une meilleure reproductibilité des entraînements.  
- utiliser Docker pour la pipeline (avec conversion en Apptainer container pour rouler sur ComputeCanada )  


## Semaine 7-8 (22–7 mars)

### Activités : Benchmark et analyses de l'apprentissage
#### Travail réalisé
- A ajouté MLflow et des métriques de suivi
- A ajouté une fonction pour générer un fichier texte résumant les résultats après l'évaluation en fin de finetuning
- A analysé des courbes de training
- A processé les embeddings des séquences du testsetet et a généré des visualisations pour analyser l'apprentissage
- A présenté au lab meeting (semaine de relâche)

#### Difficultés rencontrées
Des outliers étranges dans la visualisation des embeddings requiert un approfondissement  
Le nom des gènes n'est pas directement accessible et homogène. Il faut donc manuellement les labelliser.

#### Décisions et ajustements
Investiguer sur les outliers  
Ajouter une visualisation par famille de gènes CYP et par taxon (par espèce)  
Rallonger si besoin le temps alloué pour cette étape car il n'y a pas d'alternatives pour la labellisation.

## Semaine 9 (8–15 mars)

### Activités : Implémentation du fitness scores et tâches annexes de la semaine dernière


#### Travail réalisé
- A investigué sur les outliers.
- A ajouté une visualisation par famille de gènes CYP et par taxon (par espèce).
- A implémenté le score de fitness et la pipeline pour mesurer la corrélation de la fitness avec les scores d'un autre prédicteur reconnu (modèle AlphaMissense).
- A réalisé une pipeline de mesure de fitness à partir de fichier de séquences mutées.

#### Difficultés rencontrées

Pour les séquences mutées des CYPs scorés par AlphaMissense, il faut d'abord extraire les séquences de références pour chaque gène.  
Pour obtenir les scores de l'autre prédicteur, il faut utiliser le logiciel VEP et recouper les données avec une autre base de données. 

#### Décisions et ajustements
Rallonger si besoin le temps alloué pour cette étape car il n'y a pas d'alternatives pour le calcul de corrélation.

## Semaine 10-11 (16–29 mars)

### Activités : Obtenir les scores d'AlphaMissense et deuxième investigation 

#### Travail réalisé
- A extrait les séquences de références pour chaque séquence mutée.
- A implémenté une pipeline avec VEP pour obtenir les scores de l'autre prédicteur (AlphaMissense).
- A obtenu les scores d'AlphaMissense. 
- A réinvestigué sur les outliers avec l'outil Blastp et la base de données UniProtKB car en présentant les résultats, il y avait des incohérences sur la cause de certains outliers.  


#### Difficultés rencontrées
Les outliers sont le fruit d'un problème plus complexe que prévu.  
En effet, d'une part, certaines séquences ne sont pas des séquences de CYPs mais vu qu'elles contiennent le mot CYP dans le cluster name, elles se retrouvent dans nos datasets(ex: CYP reductase = enzyme qui interagit avec les CYP).  
Mais plus grave, certaines sequences de référence sont tout simplement absentes de nos trainsets. En fait, extraire directement des séquences depuis la base de données UniRef n'est totalement adapté pour notre cas d'usage car du fait du fonctionnement de cette base de données certaines sequences de référence ont une annotation différente et sont donc non annotés comme des CYPs.  
#### Décisions et ajustements
Refaire les datasets et trouver une manière plus rigoureuse de les constituer.  
Réentrainer les modèles et régénérer les résultats si le temps le permet. (Au moins pour les mammifères et les hominidés)  

## Semaine 12 (30-5 avril)

### Activités : Recherche d'une nonvelle méthode de construction des datasets
#### Travail réalisé
- A établi une nouvelle manière de construire les datasets en s'aidant d'une base de données de référence (UniProtKB), UniRef et un outil appelé ID Mapping developpé pour mapper les IDs de UniRef avec d'autres base de données.  
- A généré une partie des données avec la nouvelle manière pour voir.  
#### Difficultés rencontrées
Manque de temps pour réentrainer et regénérer l'ensemble des trainsets déjà créés.

#### Décisions et ajustements
Au vu du temps qui reste, on gardera le modèle finetuné sur les mammifères avec les anciennes données car le modèle semble avoir appris. Aussi, les outliers sont vraiment rares quand on observe les données.    
Si le temps le permet, les datasets avec la nouvelle méthode seront générés mais sinon on ira de l'avant 



## Semaine 13-14 (6-17 avril)

### Activités : Finalisation des analyses
### Travail réalisé
- A généré les score de fitness  
- A mesuré la corrélation entre les scores du modèle et d'AlphaMissense. L'a mis en figure  
- A recoupé les résultats avec la base de données ClinVar qui recense des variants cliniquement observés (= sur des patients) pour voir si la corrélation pour ces variants est la même. 
- A identifié des haplotypes (combinaisons de mutations connues) qui pourraient être utilisé   
#### Difficultés rencontrées
Pour les haplotypes, nous souhaitons avoir des mutations qui impliquent seulement un changement d'acide aminé et non une suppression ou une insertion. En effet, une suppression raccourcit la séquence et une insertion la rallonge alors qu'on souhaite conserver la même longueur de séquence,
Or, les haplotypes sont parfois des mélanges de plusieurs de ces cas.
Aussi, certains CYP ne sont pas bien documentés dans la littérature
#### Décisions et ajustements
Dans un premier temps, on partira avec CYP2D6 qui est le CYP le plus connu dans la littérature et qui possède 60 haplotypes qui pourraient nous intéressés. 


## Semaine 14-16 (17–30 avril)

### Activités : Dernières analyses + Présentation + Rapport 
### Travail réalisé
- A mesuré les scores de fitness de plusieurs positions mutées dans une séquence possédant plusieurs mutations.  
- A généré des profils de fitness par position pour chaque séquence. 
- A regénéré des figures pour le rapport.  
- A rédigé le rapport.   
- A préparé la prsensetation et s'est pratiqué.  
#### Difficultés rencontrées
L'épistasie est une interation assez subtile donc la mesurer demande des méthodes précises et bien selectionner les exemples de référence qui serviront pour les comparaisons.

#### Décisions et ajustements
- va présenter son travail au lab meeting.
- va approfondir les résultats durant l'été.
