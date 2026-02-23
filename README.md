## Contexte
Dans le cadre de l'accompagnement des PME dans leur développement, les cabinets d'expertise comptable ont besoin d'outils structurés pour aider leurs clients à préparer une première levée de fonds. Ces entreprises doivent pouvoir présenter aux investisseurs régionaux des projections financières crédibles et des indicateurs de performance solides, tout en évaluant leur capacité réelle d'endettement.

L'outil CAP PME s'appuie sur le bilan et le compte de résultat d'une année de référence pour générer automatiquement des projections financières sur 3 à 5 ans et produire une analyse investisseurs complète. Le projet répond à ce besoin en fournissant un tableau de bord Power BI complet permettant aux experts-comptables de piloter la performance financière de leurs clients PME et de produire une lecture investisseurs professionnelle.

## Objectifs
Développer un outil de pilotage Power BI permettant d'analyser la santé financière actuelle d'une PME, de projeter son évolution sur 3 à 5 ans, et d'estimer sa capacité de financement soutenable pour préparer une levée de fonds. Plus spécifiquement :
- Analyser la performance historique via 15 KPIs financiers clés (rentabilité, liquidité, endettement)
- Projeter l'évolution financière à moyen terme avec des hypothèses paramétrables
- Évaluer la soutenabilité du financement avec des indicateurs pro forma destinés aux investisseurs
- Calculer la capacité d'endettement maximale compatible avec la santé financière de l'entreprise

## Données
Un unique fichier excel avec au moins deux feuilles : "Compte de résultat" et "Bilan"
Struture de chacune des feuilles : les libellés comptables en lignes et les années en colonnes


## Livrable
On a un rapport Power BI avec plusieurs onglets.

- (1) KPIs & Ratios - Année de Référence : un onglet présentant  15 indicateurs de l'année de référence organisés en 3 catégories (performance opérationnele, endettement, structure financière et liquidité) avec des codes couleurs automatiques selon secteur d'activité et des commentaires d'interprétation intégrés (BFR/CA, DSCR)
- (2) Hypothèses investisseurs : un onglet de saisie des paramètres de financement (montant, taux, durée)
- (3) Capacité de financement soutenable : un onglet qui calcule le montant maximal d'emprunt compatible avec la CAF et l'annuité maximale soutenable
- (4) Suivi des amortissements : onglet présentant le tableau d'amortissement dynamique (annuités constantes)
- (5) Prévisionnel X ans - Exploitation : cet onglet présente le compte de résultat prévisionnel complet sur un horizon de 5 ans maximum avec des paramètres pour des scénarios multiples
- (7) Analyse Financière Prévisionnelle : cet onglet présente les mêmes indicateurs que dans l'onglet (1)
- (8) Lecture investisseurs -Pro forma : onglet présentant les indicateurs pro forma (DSCR, couverture des intérêts pro forma, trésorerie après service de la dette, trésorerie après service de la dette sur CA) sur la base des hypothèses investisseurs et les messages d'interprétation selon seuils

NB : 
- Consultez le guide utilisateur pour retrouver les formules de calcul des KPIs
- Les projections s'appuient sur des paramètres métier saisis par l'expert-comptable : hypothèses d'activité (croissance du CA, évolution des charges...), hypothèses de structure (BFR, CAPEX) et hypothèses de financement (montant, taux, durée, DSCR cible). Ces paramètres permettent de générer des scénarios multiples et de tester la sensibilité du modèle.

