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
- Aimplémenté le score de fitness et la pipeline pour mesurer la corrélation de la fitness avec les scores d'un autre prédicteur reconnu (modèle AlphaMissense).
- Aréalisé une pipeline de mesure de fitness à partir de fichier de séquences mutées.

#### Difficultés rencontrées

Pour les séquences mutées, il faut d'abord extraire les séquences de références pour chaque gène.  
Pour obtenir les scores de l'autre prédicteur, il faut utiliser le logiciel VEP et recouper les données avec une autre base de données. 

#### Décisions et ajustements
Rallonger si besoin le temps alloué pour cette étape car il n'y a pas d'alternatives pour le calcul de corrélation.

## Semaine 10-11 (16–29 mars)

### Activités : Itération 2 avec amélioration


#### Travail réalisé
#### Difficultés rencontrées
#### Décisions et ajustements


## Semaine 12 (30-5 avril)

### Activités : Validation et test finaux 
#### Travail réalisé
#### Difficultés rencontrées
#### Décisions et ajustements



## Semaine 13-14 (6-17 avril)

### Activités : Finalisation des analyses
### Travail réalisé
#### Difficultés rencontrées
#### Décisions et ajustements



## Semaine 14-16 (17–30 avril)

### Activités : Présentation + Rapport 
### Travail réalisé
#### Difficultés rencontrées
#### Décisions et ajustements

