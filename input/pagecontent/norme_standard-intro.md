### Introduction

Le présent document présente l'ensemble des normes et standards susceptibles de répondre à la mise en œuvre des flux identifiés dans le document « [Spécifications fonctionnelles des échanges - Téléradiologie](.\specifications_fonctionnelles.html) ». L'objectif de cette étude est d'identifier, qualifier et comparer les standards pertinents pour supporter les échanges nécessaires à la pratique de la téléradiologie.

Les normes et standards étudiés au sein de cette étude sont les suivants :

| **Standard** | **Modèle de contenu** | **Mécanisme de transport associé** |
| --- | --- | --- |
| HL7 Version 2.x (v2) | ✔  |  Transport externe requis|
| DICOM | ✔  | ✔  (DICOM Upper Layer / DIMSE sur TCP/IP, DICOMweb) |
| HL7 CDA | ✔ | Transport externe requis |
| HL7 FHIR | ✔ | ✔ (HTTP(S), REST) |

<p style="text-align:center;">Table 1 : Normes et standards étudiés</p>

Les standards seront analysés notamment par rapport à leur capacité en matière de structuration du contenu et, le cas échéant, de modalités de transport. Cette étude s'inscrit dans un contexte de mise en œuvre opérationnelle contraint. L'un des objectifs structurants du volet Téléradiologie est de permettre le versement, au sein du Dossier Médical Partagé (DMP), des demandes d'examen d'imagerie et des comptes rendus produits dans le cadre de la téléradiologie. À la date de la présente étude, le DMP supporte exclusivement des documents cliniques structurés au format CDA. Par ailleurs, les échéances de mise en œuvre du volet imposent de privilégier des solutions limitant les impacts sur les systèmes existants, en particulier les logiciels de RIS et les systèmes d'information de téléradiologie déjà largement déployés. Ces éléments constituent des critères de choix déterminants, au même titre que la couverture fonctionnelle et technique des standards étudiés, et seront pris en compte dans l'analyse comparative et la conclusion de la présente étude.

Les versions des normes et standards étudiés dans le présent document sont celles disponibles à la date de réalisation de l'étude (décembre 2025).

L'étude présente un rappel synthétique du contexte du volet Téléradiologie. Elle propose ensuite, pour chacune des normes et standards étudiés, une analyse détaillée comprenant une description générale, leur maturité et leur niveau d’adoption au sein des systèmes de santé, l’existence d’outillage dédié, ainsi que leur pertinence au regard des cas d’usage identifiés.

Une synthèse comparative est ensuite proposée afin de faciliter la lecture et la mise en perspective des normes et standards évalués. Enfin, une analyse métier et technique croisée permet d'éclairer les choix de standardisation envisageables.

Cette étude s'appuie sur les recommandations et principes du Cadre d'interopérabilité des systèmes d'information de santé (CI-SIS), qui référence les normes et standards internationaux applicables au développement des volets métiers, et constitue le référentiel institutionnel national de doctrine pour l'interopérabilité du système de santé.