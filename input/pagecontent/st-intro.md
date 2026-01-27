### Introduction

La présente spécification technique définit les modalités d’échange des informations de téléradiologie au moyen du standard **HL7 version 2.5.1**. Elle a pour objectif de préciser les profils de messages, segments, champs, cardinalités et règles d’usage nécessaires à l’interopérabilité entre les systèmes d’information impliqués dans les processus de téléradiologie, particulèrement les RIS et les plateformes de téléradiologie.

Cette spécification s’applique exclusivement aux flux identifiés dans le [Volume 1 - Etude fonctionnelle](./specifications_fonctionnelles.html).
Le choix du standard est également le fruit d'une [étude dédiée à retrouver en annexe](./norme_standard.html).

Les échanges sont basés sur des messages HL7 v2 conformes à la version **2.5.1**. Lorsque cela est applicable, la spécification s’appuie sur les profils du domaine [IHE Radiology](https://www.ihe.net/ihe_domains/radiology/), et notamment le profil [IHE Scheduled Workflow (SWF.b)](https://wiki.ihe.net/index.php/Scheduled_Workflow.b), afin d’assurer la cohérence des échanges avec les workflows d’imagerie existants. Les principes définis par le profil [IHE PAM-FR](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf) sont également pris en compte pour la gestion de l’identité patient, en particulier en ce qui concerne l’identification nationale de santé (INS). Enfin, les types de données HL7 v2 sont contraints, lorsque cela est applicable, par la spécification [Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure](https://www.interopsante.org/f/db43469b624f3039f9610d8cb6b27830ed6a9fe1/IHE_France_Constraints_on_HL7_data_types_for_ITI_V1.8.2.pdf), publiée par Interop'santé.

Il est précisé que les flux décrits dans la présente spécification portent principalement sur des **données structurées nécessaires à l’orchestration du workflow**.  
La transmission de la **demande d’examen formalisée sous forme de document clinique**, ainsi que celle d’éventuels **documents cliniques complémentaires**, n’est pas assurée par ces flux transactionnels et fait l’objet de flux documentaires distincts s'appuyant sur le [Volet de transmission d'un document CDA-R2 en HL7v2](https://interop.esante.gouv.fr/ig/hl7v2/trans-cda-r2/).

Cette articulation permet de maintenir une séparation claire entre :
- les **échanges transactionnels HL7 v2** dédiés au pilotage du workflow de téléradiologie ;
- et les **échanges documentaires CDA**, garantissant la conformité aux référentiels nationaux et la cohérence globale des échanges.
