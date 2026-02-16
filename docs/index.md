---
title: Vue d'ensemble du projet
---

<style>
    @media screen and (min-width: 76em) {
        .md-sidebar--primary {
            display: none !important;
        }
    }
</style>

# Vue d'ensemble du projet

!!! info "Informations générales"
    **Session**: Hiver 2026  
    **Auteur(s)**: M-S H 
    **Thème(s)**: LLMs, Bioinformatique, Génomique
    **Superviseur(s)**: Dpt Bioinfo

## Description du projet

> :bulb: N'oubliez pas d'effacer ou mettre en commentaires les notes (`>`) en début de section

### Contexte

Le cytochrome P450 (CYP) est une famille de protéines enzymatiques qui joue un rôle crucial dans le métabolisme des médicaments, des hormones, et de nombreux autres substrats dans les organismes. Cependant, les mutations dans cette famille de gènes peuvent entraîner des perturbations de leur fonction, affectant ainsi la santé du patient et sa réponse aux traitements. Ceci dit, l'étude des effets des mutations sur les protéines CYP est complexe en raison de l'épistasie, un phénomène dans lequel l'effet combiné de plusieurs mutations ne peut pas être prédit simplement par l'addition de leurs effets individuels. Parallèlement, les récents progrès en apprentissage profond ont conduit au développement de Protein Large Language Models (pLLM), tels qu’ESM2, entraînés sur de vastes bases de données de séquences protéiques. Ces modèles sont capables d’extraire des représentations informatives à partir de la seule séquence en acides aminés, ouvrant de nouvelles perspectives pour la prédiction des effets des mutations. Néanmoins, leur capacité à modéliser des phénomènes complexes tels que l’épistasie reste encore peu explorée, en particulier pour des familles protéiques spécifiques comme les CYP.

### Problématique

La plupart des approches actuelles de prédiction de l’impact des mutations protéiques se concentrent sur des mutations individuelles comme le modèle AlphaMissense. Or, dans de nombreux cas biologiques, l’effet combiné de plusieurs mutations est non additif, en raison d’interactions épistatiques entre résidus. De plus, cette limitation est particulièrement critique pour les CYP, car ces protéines présentent souvent plusieurs mutations simultanées, dont les interactions peuvent fortement moduler l’activité enzymatique, et les données expérimentales couvrant l’ensemble des combinaisons possibles restent rares et coûteuses à obtenir. La problématique de ce projet est donc de déterminer si un protein Language Model, tel qu’ESM2, peut être spécialisé par fine-tuning sur la famille des CYP afin de prédire l’impact épistatique de mutations multiples sur ces protéines. L’étude de cette question est motivée par l’importance biologique et médicale des CYP, ainsi que par le potentiel des pLLM à capturer des relations complexes au sein des séquences protéiques.

### Proposition et objectifs

Le projet propose de développer un modèle prédictif basé sur le fine-tuning du modèle ESM2, spécifiquement adapté à la famille des cytochromes P450. Les jeux de données seront constitués à partir de séquences d’acides aminés issues de la base de données UniProt. Trois modèles distincts seront entraînés : un modèle fine-tuné sur les CYP de mammifères, un modèle fine-tuné sur les CYP des métazoaires, et un modèle fine-tuné sur les CYP des
eucaryotes. Le modèle ESM2 pré-entraîné sans fine-tuning sera utilisé comme référence comparative, et les évaluations porteront sur des séquences de CYP humaines et de grands singes. Les principaux objectifs du projet sont de prédire l’impact fonctionnel cumulatif de mutations simples, doubles et multiples dans les protéines CYP, d’évaluer l’apport du fine-tuning par rapport au modèle générique, de comparer l’effet du niveau de spécialisation phylogénétique sur les performances de prédiction, et de proposer un pipeline reproductible pour l’analyse de l’épistasie dans une famille protéique donnée.

### Méthodologie

Les séquences d’acides aminés des protéines CYP seront extraites de la base UniProt pour trois groupes d’organismes : mammifères, métazoaires et eucaryotes. Ces données seront ensuite nettoyées, annotées et alignées afin d’identifier les positions mutables et de constituer des jeux de données adaptés à l’entraînement. À partir des séquences de référence, des variants comportant des mutations simples, doubles ou multiples seront générés afin d’évaluer les effets cumulés et non additifs. Le fine-tuning du modèle ESM2 sera réalisé en Python à l’aide de PyTorch et de la librairie Transformers, en ajustant les hyperparamètres et les poids du modèle pour chaque ensemble phylogénétique. L’entraînement sera effectué sur l’infrastructure Compute Canada via Slurm, en produisant trois modèles distincts correspondant aux groupes d’organismes. Les performances de ces modèles fine-tunés seront comparées à celles du modèle ESM2 non fine-tuné afin d’évaluer l’impact du fine-tuning et de la spécialisation phylogénétique. Enfin, la validation combinera des tests avec des séquences de CYP humaines et des mutations documentées scientifiquement. La gestion du projet essayera d’être itérative afin de garantir des résultats et un MVP qui pourra être utilisée par le laboratoire à la fin du projet.

### Validation et Évaluation

L’évaluation sera réalisée sur des séquences CYP indépendantes, provenant d’humains et de grands singes, en comparant les performances des modèles fine-tunés à celles du modèle ESM2 non fine-tuné. L’analyse de l’épistasie consistera à examiner l’écart entre l’effet prédit des mutations combinées et la somme des effets individuels, permettant ainsi de mesurer la capacité des modèles à capturer les interactions non additives. Cela sera validé à l’aide de mutations documentées dans la littérature et l’expertise du laboratoire. Par ailleurs, l’étude de la perplexité des modèles, ainsi que l’analyse des matrices d’attention et des embeddings, permettront d’évaluer l’impact du fine-tuning sur la capacité prédictive des modèles. Ces analyses offriront également un aperçu de l’interprétabilité des résultats en vérifiant la plausibilité biologique des interactions identifiées et en mettant en évidence les sites clés impliqués dans l’épistasie.

## Échéancier

!!! info
    Le suivi complet est disponible dans la page [Suivi de projet](suivi.md).

| Activités                      | Début   |   Fin   | Livrable                            | Statut      |
|--------------------------------|---------|---------|-------------------------------------|-------------|
| Kick-off du projet             | 12 jan. | 12 jan. | Description du projet               | ✅ Terminé  |
| État de l'art                  | 12 jan. | 25 jan. | Rapport de synthèse + références    | ✅ Terminé  |
| Constitution des datasets      | 26 jan. |  8 fév. | Trainsets et testsets + README      | ✅ Terminé  |
| Implémentation et finetuning   |  8 fév. | 22 fév. | Code fonctionnel                    | 🔄 En cours |
| Benchmark et analyses des perfs| 22 fév. |  7 mar. | Pipeline d'analyses + graph de perfs| ⏳ À venir  |
| Itération 2 avec amélioration  |  8 mar. | 22 mar. | Code amélioré et datasets rafinés   | ⏳ À venir  |
| Validation et test finaux      | 23 mar. |  6 avr. | Rapport de validation               | ⏳ À venir  |
| Finalisation des analyses      |  7 avr. | 17 avr. | Rapport d’analyses final            | ⏳ À venir  |
| Présentation + Rapport         | 17 avr. | 30 avr. | Présentation + Rapport              | ⏳ À venir  |
