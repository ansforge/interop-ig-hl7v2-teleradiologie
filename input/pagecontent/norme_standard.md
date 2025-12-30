### Introduction

Le présent document présente l'ensemble des normes et standards susceptibles de répondre à la mise en œuvre des flux identifiés dans le document « [Spécifications fonctionnelles des échanges - Téléradiologie](.\spécifications_fonctionnelles.html) ». L'objectif de cette étude est d'identifier, qualifier et comparer les standards pertinents pour supporter les échanges nécessaires au parcours de téléradiologie.

Les normes et standards étudiés au sein de cette étude sont les suivants :

| **Standard** | **Modèle de contenu** | **Mécanisme de transport associé** |
| --- | --- | --- |
| HL7 Version 2.x (v2) | ✔  |  Transport externe requis|
| DICOM | ✔  | ✔  (DICOM Upper Layer / DIMSE sur TCP/IP, DICOMweb) |
| HL7 CDA | ✔ | Transport externe requis |
| HL7 FHIR | ✔ | ✔ (HTTP(S), REST) |

<p style="text-align:center;">Table 1 : Normes et standards étudiés</p>

Les standards seront analysés notamment par rapport à leur capacité en matière de structuration du contenu et, le cas échéant, de modalités de transport. Cette étude s'inscrit également dans un contexte de mise en œuvre opérationnelle contraint. L'un des objectifs structurants du volet Téléradiologie est de permettre le versement, au sein du Dossier Médical Partagé (DMP), des demandes d'actes d'imagerie et des comptes rendus produits dans le cadre de la téléradiologie. À la date de la présente étude, le DMP supporte exclusivement des documents cliniques structurés au format CDA. Par ailleurs, les échéances de mise en œuvre du volet imposent de privilégier des solutions limitant les impacts sur les systèmes existants, en particulier les logiciels de RIS et les plateformes de téléradiologie déjà largement déployés. Ces éléments constituent des critères de choix déterminants, au même titre que la couverture fonctionnelle et technique des standards étudiés, et seront pris en compte dans l'analyse comparative et la conclusion de la présente étude.

Les versions des normes et standards étudiés dans le présent document sont celles disponibles à la date de réalisation de l'étude (décembre 2025).

L'étude présente un rappel synthétique du contexte du volet Téléradiologie. Elle propose ensuite, pour chacune des normes et standards étudiés, une analyse détaillée comprenant une description générale, leur maturité et leur niveau d’adoption au sein des systèmes de santé, l’existence d’outillage, ainsi que leur pertinence au regard des cas d’usage identifiés.

Une synthèse comparative est ensuite proposée afin de faciliter la lecture et la mise en perspective des normes et standards évalués. Enfin, une analyse métier et technique croisée vient éclairer les choix de standardisation envisageables.

Cette étude s'appuie sur les recommandations et principes du Cadre d'interopérabilité des systèmes d'information de santé (CI-SIS), qui référence les normes et standards internationaux applicables au développement des volets métiers, et constitue le référentiel de doctrine pour l'interopérabilité du système de santé.

<br>

### Présentation synthétique du volet Téléradiologie

Cette étude s'inscrit dans le cadre des besoins d'interopérabilité associés au volet « Téléradiologie ». Ce volet a pour objectif de décrire les échanges, et leur contenu, nécessaires à la prise en charge d'un patient lorsque l'interprétation radiologique est réalisée à distance, entre une structure d'imagerie (lieu de réalisation de l'acte) et une plateforme de téléradiologie (lieu d'interprétation).

Les échanges d'informations interviennent principalement entre :

- Le RIS (Système d'Information Radiologique) de la structure d'accueil du patient
- Le système d'information de la plateforme de téléradiologie

La présente étude couvre les échanges décrits dans la Spécification fonctionnelle des échanges - Téléradiologie, à savoir :

- La transmission d'une demande d'examen d'imagerie
- L'annulation d'une demande d'examen
- La réponse à une demande (acceptation avec protocole d'imagerie ou refus)
- La transmission d'informations complémentaires post-examen

Les concepts métiers à véhiculer dans ces flux sont décrits en étape 4 et 5 de la spécification fonctionnelle et couvrent plusieurs catégories de données essentielles au parcours de téléradiologie :

- Données administratives et d'identification : identités patient et professionnels, identifiants de demandes et d'examens, informations de structure.
- Données cliniques et de prescription : motif d'examen, indications, contexte clinique fourni par le médecin de proximité.
- Données de protocole d'imagerie : éléments nécessaires à la réalisation de l'acte, fournis par le radiologue distant.
- Données techniques et informations post-acte : paramètres de réalisation, incidents, observations du manipulateur.

Le choix final des normes ou standards devra permettre de couvrir l'intégralité des données manipulées dans le cadre de la téléradiologie, ainsi que les scénarios d'échanges entre la structure d'imagerie et le service d'interprétation distant.

<br>

### Normes et Standards étudiés

Cette section présente les normes et standards susceptibles d'être utilisés pour structurer et, le cas échéant, transporter les données échangées dans le cadre du volet Téléradiologie. Les concepts métiers étudiés dans cette étude sont issus de la Spécification fonctionnelle des échanges Téléradiologie.

{% include norme_standard_dicom.md %}

<br>

{% include norme_standard_cda.md %}

<br>

{% include norme_standard_fhir.md %}

<br>

{% include norme_standard_hl7v2.md %}

<br>

### Synthèse

#### Synthèse de la couverture des objets métiers par chaque standard étudié

L’analyse de la couverture des objets métiers montre que les standards HL7 v2 et HL7 FHIR permettent de représenter l’ensemble des concepts métiers identifiés pour le volet Téléradiologie.

#### Synthèse comparative des normes et standards étudiés

Cette section présente une synthèse comparative des normes et standards analysés dans les sections précédentes. Les items de cette synthèse sont inspirés des documents suivants :

- La [doctrine du CI-SIS](https://esante.gouv.fr/sites/default/files/media_entity/documents/CI-SIS_DOCTRINE_20210803_V1.1.pdf)
- « [Evaluating HIT Standards](https://www.himss.org/sites/hde/files/FileDownloads/2013-09-23-EvaluatingHITStandards-FINAL.pdf) » document sur la comparaison des standards publiés par l'organisation [HIMSS.](https://www.himss.org/)
- La méthode [CAMSS](https://joinup.ec.europa.eu/collection/common-assessment-method-standards-and-specifications-camss) (Common Assessment method for standards and specifications) soutenue par le programme de la commission européenne concernant les solutions d'interopérabilité pour les administrations publiques. Cette initiative vise à promouvoir la collaboration entre les états membres de l'union européenne dans la définition d'une méthode d'évaluation commune de standards pour le développement des services administratifs en ligne.

| **Critères d'évaluation** | **DICOM** | **CDA** | **FHIR** | **HL7v2** |
| --- | --- | --- | --- | --- |
| Couverture métier || Non étudiée | ✔   | ✔   |
| Adoption par l'écosystème Téléradiologie |✔ | ✔  |    | ✔   |
| Rétrocompatibilité du standard ou de la norme | ✔   | ✔   |   | ✔   |
| Outillage<br><br>_Des outils de tests sont mis en œuvre pour valider l'adhérence au standard._ | ✔   | ✔   | ✔   | ✔   |
| Tests<br><br>_Des tests sont effectués pour des versions de travail (dites STU -Standards for Trial Use) et/ou pour les guides d'implémentation normatifs._ |  ✔   | ✔   | ✔   | ✔   |
| Processus de prise en compte des améliorations | ✔   | ✔   | ✔   | ✔   |
| Existence de guides d'implémentation<br><br>_Les guides référencent les standards de base avec au moins un cas d'usage et une optionalité sur les paramètres pour permettre les extensions._ |  ✔   | ✔   | ✔   | ✔   |
| Adapté aux dispositifs mobiles |  ✔   | ✔   | ✔   | ✔   |
| Stabilité de la documentation | ✔   | ✔   | ✔   | ✔   |
| Adoption par le marché et utilisation | ✔   | ✔   | ✔   | ✔   |
| Neutralité<br><br>_les spécifications ne limitent pas la concurrence et l'innovation; les spécifications sont basées sur des développements scientifiques et technologiques de pointe._ | ✔   | ✔   | ✔   | ✔   |
| Qualité<br><br>_la qualité est suffisante pour permettre le développement de produits et de services interopérables concurrents._ | ✔   | ✔   | ✔   | ✔   |
| Accessibilité<br><br>_Les spécifications sont disponibles au public à des conditions raisonnables (y compris pour un prix raisonnable ou gratuitement)._ | ✔   | ✔   | ✔   | ✔   |

<p style="text-align:center;">Table 7 : Synthèse comparative des normes et standards étudiés</p>

<br>

### Analyse et conclusion

#### Normes et Standards étudiés

Cette section a pour objectif de comparer les normes et standards étudiés dans ce document, en vue de choisir le plus approprié pour la spécification du volet « Téléradiologie ».

##### DICOM

Le standard DICOM est indispensable pour la gestion et la mise à disposition des images médicales, mais ne couvre pas les échanges fonctionnels et organisationnels du volet Téléradiologie.

##### CDA

Le standard HL7 CDA est adapté à la production et à l'échange de documents cliniques persistants, en particulier le compte-rendu d'imagerie, qui constitue le livrable clinique final du workflow. En dehors du flux de demande d'examen déjà couvert par un volet CI-SIS dédié, l'utilisation de CDA pour les échanges intermédiaires n'est pas adapté au contexte de téléradiologie. De plus, les orientations européennes limitent l'intérêt d’engager de nouveaux travaux basé sur le standard sur CDA.

##### FHIR

Le standard HL7 FHIR permet de couvrir l’ensemble des concepts métier du volet Téléradiologie au travers de ressources structurées, largement adoptées dans le domaine de la santé. Les mécanismes d’acquittement ne sont pas modélisés nativement et reposent sur les échanges HTTP ou sur des ressources spécifiques telles qu’OperationOutcome. La mise en œuvre de FHIR suppose par ailleurs que chaque acteur dispose d’une infrastructure FHIR complète, capable d’assurer les rôles de client et de serveur pour supporter les flux d’échange.

D’une manière générale, le standard FHIR, dans sa version R4, repose encore sur un nombre limité de ressources à l’état normatif, pouvant être considérées comme pleinement stables et rétrocompatibles. Dans la version R5, seules deux ressources supplémentaires ont accédé à cet état normatif, ce qui implique une vigilance particulière quant à la gestion des évolutions et à la rétrocompatibilité dans le cadre de mises en œuvre opérationnelles.

##### HL7v2

L’analyse des flux du volet Téléradiologie montre que le standard HL7 v2 permet de couvrir l’ensemble des échanges identifiés. Il offre des mécanismes natifs de gestion des statuts et d’accusés de réception, adaptés aux flux transactionnels, notamment lorsqu’il est utilisé avec le protocole MLLP. Les profils IHE SWF.b et IHE PAM-FR fournissent par ailleurs des cadres de référence réutilisables pour le cycle de vie des demandes d’imagerie et la gestion de l’identité patient.

Largement adopté dans l'écosystème de l'imagerie médicale et déjà utilisé dans les volets de transport de documents CDA, HL7 v2 constitue une solution opérationnelle à court terme limitant les impacts sur les systèmes existants et compatible avec les contraintes de déploiement du volet.

### Conclusion

**La présente étude a pour objectif d'identifier et de comparer les normes et standards susceptibles de répondre à la mise en œuvre des flux d'échange définis dans les spécifications fonctionnelles du volet Téléradiologie. L'analyse a porté sur un ensemble de standards largement utilisés dans le domaine de l'interopérabilité en santé, évalués au regard de plusieurs critères complémentaires : la capacité à structurer les contenus métiers, la couverture des cas d'usage identifiés, la maturité et le niveau d'adoption au sein de l'écosystème, l'existence d'outillage, ainsi que l'adéquation aux contraintes organisationnelles, techniques et réglementaires du contexte national.**

**Parmi les standards étudiés, DICOM et HL7 CDA ont été écartés comme supports principaux des flux du volet Téléradiologie. DICOM est spécifiquement dédié à la gestion, au stockage et à l’échange des objets d’imagerie médicale et ne vise pas la structuration des échanges métiers intervenant tout au long du workflow. Le standard HL7 CDA est, quant à lui, conçu pour la production de documents cliniques persistants, est pertinent en fin de parcours pour le compte-rendu d’imagerie. En revanche, son usage pour des échanges transactionnels intermédiaires à durée de vie courte ne correspond pas à son positionnement naturel. Par ailleurs, les orientations européennes et nationales récentes en matière d’interopérabilité privilégient désormais le standard HL7 FHIR pour les nouveaux besoins d’échange de données de santé structurées, ce qui limite la pertinence d’engager de nouveaux travaux fondés sur CDA dans ce contexte.**

**L’analyse met en évidence que le standard HL7 FHIR présente une couverture fonctionnelle et technique complète des besoins du volet Téléradiologie. Sa granularité, son modèle de données explicite et sa capacité à supporter des échanges transactionnels en font un standard particulièrement adapté aux cas d’usage identifiés. Par ailleurs, son alignement avec les orientations européennes en matière d’interopérabilité confirme son rôle structurant dans les trajectoires d’évolution à moyen et long terme des systèmes d’information de santé.**

**L’étude montre également que le standard HL7 v2 est en mesure de couvrir l’ensemble des concepts métiers du volet Téléradiologie. Il propose des mécanismes natifs adaptés à la gestion des échanges transactionnels, notamment pour le suivi de l’état de traitement des demandes et les accusés de réception. Son usage est bien maîtrisé par l’écosystème, en particulier dans le domaine de l’imagerie médicale, et s’appuie sur un outillage industriel éprouvé ainsi que sur des profils IHE largement diffusés.**

**En conclusion, au regard des contraintes analysées dans cette étude, le standard HL7 v2 apparaît comme le plus à même de répondre aux besoins du volet Téléradiologie dans un contexte de mise en œuvre à court terme. HL7 v2 permet de couvrir l’ensemble des concepts métiers identifiés, tout en s’appuyant sur des mécanismes éprouvés pour la gestion de flux transactionnels. Sa maturité, son adoption éprouvée dans le domaine de l’imagerie médicale, ainsi que la disponibilité de profils IHE tels que PAM-FR et SWF.b permettent de capitaliser sur des briques existantes et largement industrialisées. Ce choix garantit ainsi une mise en œuvre pragmatique, limitant les impacts pour les éditeurs de RIS et de plateformes de téléradiologie tout en assurant la compatibilité avec les capacités actuelles du DMP.**
