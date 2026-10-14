## CAP PME : une PME peut-elle financer son investissement par l'emprunt ?

<p align="justify">
## Contexte
Avant de financer un investissement, un dirigeant de PME et son expert-comptable doivent savoir si l'entreprise pourra rembourser l'emprunt sans mettre sa trésorerie en danger. C'est la situation d'une biscuiterie industrielle de 60 salariés qui souhaite emprunter 3 M€ pour une nouvelle ligne de production. Une question se pose : la biscuiterie peut-elle financer sa nouvelle ligne de production de 3 M€ par un emprunt bancaire, et sinon, combien peut-elle raisonnablement emprunter ?

Pour l'aider à décider, j'ai construit un outil qui lit ses comptes, projette sa situation sur 5 ans et indique si elle peut rembourser ce nouvel emprunt.

## Données
Il s'agit d'un cas construit pour la démonstration, sur le modèle d'une biscuiterie industrielle de 60 salariés réalisant 12 M€ de chiffre d'affaires. Les comptes couvrent trois exercices (2023 à 2025) et suivent le format de la liasse fiscale française : 138 postes repérés par leur code officiel, regroupés en 23 agrégats pour l'analyse. Ils reproduisent les ratios moyens du secteur publiés par l'INSEE et les délais de paiement relevés par la Banque de France. Les autres postes, comme les stocks et les créances clients, découlent de l'activité selon des hypothèses plausibles, et les trois exercices sont cohérents entre eux : le bilan de fin d'année devient celui du début de l'année suivante, et le bilan s'équilibre chaque année.

L’outil fonctionne dès un exercice, mais trois sont recommandés : il en faut au moins deux pour calculer une évolution, et trois pour repérer une année atypique.

## Méthodologie
J’ai d’abord mis en place un format d’entrée universel des données. Pour utiliser l’outil, l’entreprise saisit manuellement les montants de sa liasse fiscale dans un fichier Excel type (*[télécharger le fichier type](https://github.com/Hines98/CAP-PME/blob/main/Fichier_type_etats_financiers.xlsx))*, où chaque montant est repéré par son code de liasse fiscale. Les intitulés des postes varient d’un cabinet comptable à l’autre, les codes officiels non. L’outil fonctionne ainsi pour n’importe quelle PME au régime réel. Un script Python vérifie ensuite les codes, signale les postes indispensables à l’outil final laissés vides, contrôle que l’actif égale le passif et que le résultat recalculé égale le résultat déclaré, car une projection construite sur des comptes faux conduirait à une décision fausse. Le script produit enfin un fichier de 23 agrégats, connecté à Power BI.

## Livrable
Le rapport Power BI compte six onglets, organisés dans l’ordre où l’utilisateur s’en sert : choisir ses hypothèses, faire le diagnostic de l’année de référence, définir l’emprunt, puis projeter la situation sur 5 ans jusqu’au verdict. Les taux de prévision se saisissent dans un panneau à gauche, commun à toutes les pages. Une modification se répercute donc immédiatement partout. Les pages qui peuvent signaler un risque affichent la même légende avec une icône rouge apparaît dès qu’un seuil critique est franchi.

- Choix des hypothèses (onglet « Repères historiques »): cet onglet aide l'utilisateur à choisir les taux de prévision qu'il saisit dans les cases de gauche (croissance des ventes, des charges, des dotations, investissements courants, taux d'impôt). Il affiche l'évolution passée de l'entreprise, année par année, et propose deux scénarios. Un scénario « tendance » qui prolonge l'évolution des comptes et un scénario « prudent » qui retient une croissance deux fois plus faible, avec des charges qui progressent au même rythme que les ventes, donc une marge qui cesse de s'améliorer. Je propose ces deux scénarios parce qu'une recommandation qui ne tient que dans le scénario favorable ne vaut rien. L'utilisateur reste libre de saisir ses propres taux.

- Diagnostic de départ (onglet « KPIs et ratios »): il présente la situation de l'année de référence (rentabilité (valeur ajoutée, EBE, résultat, capacité d'autofinancement), structure financière (trésorerie, besoin en fonds de roulement, liquidité) et endettement (dette, DSCR, couverture des intérêts)). C'est le point de départ de toute projection.

- Définition de l'emprunt (onglet « Hypothèses de financement »): l'utilisateur y saisit le montant, le taux et la durée de l'emprunt. La page calcule en regard le montant que l'entreprise pourrait emprunter en plus de ses emprunts actuels, compte tenu de sa capacité d'autofinancement et d'un niveau de sécurité qu'il choisit (le « DSCR cible »). L'onglet « Suivi des amortissements » détaille ensuite, année par année, les intérêts et le capital remboursés.

- Projection sur 5 ans (onglets « Prévisionnel 5 ans » et « Analyse financière prévisionnelle »): le premier projette le compte de résultat avec les intérêts du nouvel emprunt. Le second suit la trésorerie, la dette et les ratios chaque année avec les remboursements des emprunts existants et du nouvel emprunt qui sont retirés de la trésorerie. Il se termine par un verdict pour chaque année.

Le verdict de chaque année repose sur deux indicateurs. Le premier, le DSCR, compare ce que l’activité dégage dans l’année (la capacité d’autofinancement) aux remboursements de l’année : sous 1, l’entreprise ne peut pas payer ses échéances avec ses propres ressources. Le second est la trésorerie après remboursements : si elle devient négative, l’entreprise doit trouver de l’argent ailleurs pour faire face à ses dépenses. Les pages affichent aussi une alerte quand le ratio de liquidité passe sous 1, c’est-à-dire quand les dettes à payer dans l’année dépassent ce que l’entreprise peut encaisser dans le même délai. Ces trois seuils ne sont pas des conventions : chacun marque le point où l’entreprise ne peut plus faire face à ses paiements avec ses propres moyens. C’est pourquoi ils s’appliquent à toutes les entreprises. 


## Résultats clés
Pour la biscuiterie, les ventes ont progressé de 7,8% puis de 8,1% entre 2023 et 2025, et les charges d'exploitation de 7,1 % puis de 7,0 %. Le scénario tendance retient donc 8 % et 7 %, et le scénario prudent 4% et 4%. Les dotations suivent le même taux que les ventes, puisque l'entreprise investit chaque année une part de ses ventes. Les investissements courants sont fixés à 5 % du chiffre d'affaires, le niveau d'une année normale dans ses comptes (4,7 % en 2023, 3,8 % en 2025 ; 2024 est exceptionnelle à 9,9 %) et la moyenne des PME industrielles selon l'INSEE. L'impôt est au taux normal de 25 %.

***Les résultats ci-dessous sont obtenus avec les hypothèses du scénario prudent : ventes, charges d’exploitation et dotations en hausse de 4 % par an, investissements courants à 5 % du chiffre d’affaires, impôt à 25 %, et un emprunt de 3 M€ sur 7 ans à 3,55 %.***

Avec l'emprunt de 3 M€ sur 7 ans, le DSCR est de 0,74 la première année : l'entreprise devrait rembourser 1,04 M€ (dont 0,55 M€ pour ses emprunts déjà en cours), alors que son activité ne dégage que 0,78 M€. Le DSCR reste sous 1 pendant quatre ans. Pour comparaison, compte tenu de ses emprunts actuels et avec un DSCR cible de 1,40, la biscuiterie ne pourrait emprunter qu'environ 120 000 € de plus.

En réduisant le montant de l'emprunt, le DSCR repasse au-dessus de 1 la première année avec 1,55 M€ sur 7 ans, ou 2 M€ sur 10 ans. Ces montants sont un plafond, sans aucune marge de sécurité car le DSCR n'y dépasse 1 que d'un centième.

Enfin, la trésorerie devient négative dès la deuxième année, même sans le projet : (−145 000 €) en 2027, puis environ (−675 000 €) en 2029. Elle est d'ailleurs déjà passée de 869 000 € à 472 000 € entre 2023 et 2025. Les investissements courants, la hausse du besoin en fonds de roulement et le remboursement des emprunts actuels dépassent ce que l'activité dégage. 

Cette conclusion vaut aussi dans le scénario tendance : même avec une croissance de 8 % par an, la trésorerie reste négative les cinq années avec l'emprunt de 3 M€.

## Recommandations
La biscuiterie nedevrait pas financer la ligne de production par un emprunt de 3 M€. Pendant quatre ans, l'activité ne dégagerait pas assez pour couvrir les remboursements, et l'entreprise devrait puiser dans une trésorerie déjà en baisse. Il faudrait plutôt limiter l'emprunt à 2 M€ au maximum, sur 10 ans, et financer le reste par un apport des associés ou une aide publique. Mais avant tout engagement, l'entreprise doit mettre en place un plan d'amélioration de sa trésorerie puisque celle-ci se dégrade même sans le projet.

## Limites et suites possibles
L'outil reste à tester sur les comptes d'une vraie entreprise, et la saisie depuis la liasse fiscale est aujourd'hui manuelle.

Les comptes ne donnent pas le calendrier de remboursement des emprunts que la biscuiterie avait déjà avant le projet (2,04 M€ fin 2025). L'outil suppose qu'elle continue de rembourser 480 000 € par an, comme en 2025, jusqu'à épuisement. Si l'un de ces emprunts se terminait plus tôt, les remboursements baisseraient et le DSCR s'améliorerait plus vite. Ces anciens emprunts pèsent plus de la moitié des remboursements de la première année.

La projection n'attribue aucune vente supplémentaire à la nouvelle ligne de production, sauf si l'utilisateur relève lui-même le taux de croissance. Elle n'intègre pas non plus son amortissement, ni la possibilité de déduire une perte des bénéfices des années suivantes. Les résultats sont donc plutôt prudents.

Enfin, si la biscuiterie n'emprunte que 2 M€, l'outil suppose que le million restant (apport des associés ou aide publique) n'a pas à être remboursé. S'il s'agissait d'un prêt des associés ou d'un prêt aidé, ses échéances s'ajouteraient. Alors le DSCR baisserait et le plafond de 2 M€ serait trop élevé.

Pour aller plus loin, l'outil pourrait lire automatiquement les liasses fiscales au format PDF, intégrer le calendrier réel des emprunts et comparer les ratios à des références sectorielles publiques.

## Compétences mobilisées et liens
- Python (pandas) pour lire le fichier Excel, contrôler la cohérence comptable et préparer les données ;
- Power BI (Power Query et DAX) pour la projection sur 5 ans, le tableau d'amortissement et les scénarios paramétrables ; analyse financière (soldes intermédiaires de gestion, capacité d'autofinancement, DSCR, besoin en fonds de roulement).

Liens : [Notebook Python](https://github.com/Hines98/CAP-PME/blob/main/Script.ipynb) · [Fichier Excel type à remplir](https://github.com/Hines98/CAP-PME/raw/refs/heads/main/Etats_financiers_power_bi.xlsx) · [Référentiel liasse fiscale](https://github.com/Hines98/CAP-PME/blob/main/Referentiel_liasse.csv) · [Rapport Power BI (.pbix)] · [Rapport PDF]

</p>

