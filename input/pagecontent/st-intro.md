### Introduction

La présente spécification technique définit les modalités d’échange des informations de téléradiologie au moyen du standard **HL7 version 2.5.1**. Elle a pour objectif de préciser les profils de messages, segments, champs, cardinalités et règles d’usage nécessaires à l’interopérabilité entre les systèmes d’information impliqués dans les processus de téléradiologie, particulèrement les RIS et les plateformes de téléradiologie.

Cette spécification s’applique exclusivement aux flux identifiés dans la [Spécification Fonctionnelle des Echanges](./specifications_fonctionnelles.html). Elle ne constitue pas une implémentation exhaustive du standard HL7 v2, mais en restreint l’usage aux éléments nécessaires pour couvrir les cas d’usage fonctionnels définis.

Les échanges sont basés sur des messages HL7 v2 conformes à la version **2.5.1**. Lorsque cela est applicable, la spécification s’appuie sur les profils du domaine **IHE Radiology**, et notamment le profil **IHE Scheduled Workflow (SWF.b)**, afin d’assurer la cohérence des échanges avec les workflows d’imagerie existants. Les principes définis par le profil **IHE PAM-FR** sont également pris en compte pour la gestion de l’identité patient, en particulier en ce qui concerne l’identification nationale de santé (INS).

Il est précisé que les flux décrits dans la présente spécification portent principalement sur des **données structurées nécessaires à l’orchestration du workflow**.  
La transmission de la **demande d’examen formalisée sous forme de document clinique**, ainsi que celle d’éventuels **documents cliniques complémentaires**, n’est pas assurée par ces flux transactionnels et fait l’objet de **flux documentaires distincts**, venant les compléter.

Cette articulation permet de maintenir une séparation claire entre :
- les **échanges transactionnels HL7 v2** dédiés au pilotage du workflow de téléradiologie ;
- et les **échanges documentaires CDA**, garantissant la conformité aux référentiels nationaux et la cohérence globale des échanges.
