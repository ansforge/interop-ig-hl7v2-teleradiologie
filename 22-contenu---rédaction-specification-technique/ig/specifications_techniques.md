# Volume 2 : Détail des transactions - Volet Téléradiologie v0.1.0

* [**Table of Contents**](toc.md)
* **Volume 2 : Détail des transactions**

## Volume 2 : Détail des transactions

### Introduction

La présente spécification technique définit les modalités d’échange des informations de téléradiologie au moyen du standard **HL7 version 2.5.1**. Elle a pour objectif de préciser les profils de messages, segments, champs, cardinalités et règles d’usage nécessaires à l’interopérabilité entre les systèmes d’information impliqués dans les processus de téléradiologie, particulèrement les RIS et les plateformes de téléradiologie.

Cette spécification s’applique exclusivement aux flux identifiés dans le [Volume 1 - Etude fonctionnelle](./specifications_fonctionnelles.md). Le choix du standard est également le fruit d’une [étude dédiée à retrouver en annexe](./norme_standard.md).

Les échanges sont basés sur des messages HL7 v2 conformes à la version **2.5.1**. Lorsque cela est applicable, la spécification s’appuie sur les profils du domaine [IHE Radiology](https://www.ihe.net/ihe_domains/radiology/), et notamment le profil [IHE Scheduled Workflow (SWF.b)](https://wiki.ihe.net/index.php/Scheduled_Workflow.b), afin d’assurer la cohérence des échanges avec les workflows d’imagerie existants. Les principes définis par le profil [IHE PAM-FR](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf) sont également pris en compte pour la gestion de l’identité patient, en particulier en ce qui concerne l’identité nationale de santé (INS). Enfin, les types de données HL7 v2 sont contraints, lorsque cela est applicable, par la spécification [Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure](https://www.interopsante.org/f/db43469b624f3039f9610d8cb6b27830ed6a9fe1/IHE_France_Constraints_on_HL7_data_types_for_ITI_V1.8.2.pdf), publiée par Interop’santé.

Il est pertinent de préciser que les flux décrits dans la présente spécification portent principalement sur des **données structurées nécessaires à l’orchestration du workflow**.
 La transmission de la **demande d’examen d’imagerie formalisée sous forme de document clinique**, ainsi que celle d’éventuels **documents cliniques complémentaires**, n’est pas assurée par ces flux transactionnels et fait l’objet de flux documentaires distincts s’appuyant sur le [Volet de transmission d’un document CDA-R2 en HL7v2](https://interop.esante.gouv.fr/ig/hl7v2/trans-cda-r2/).

### Evènements déclenchants

La présente partie décrit, pour chaque flux métier inclus dans le périmètre du volet Téléradiologie, le **message HL7 v2** et l’**événement HL7 v2 associé** utilisés pour supporter l’échange.

* Flux métier: **Transmission de la demande d’examen d’imagerie**
  * Structure de message HL7 v2: ORM_O01
  * Événement HL7 v2: O01 – Order message (Order Control = NW)
* Flux métier: **Annulation de la demande d’examen d’imagerie (1)**
  * Structure de message HL7 v2: ORM_O01
  * Événement HL7 v2: O01 – Order message (Order Control = CA)
* Flux métier: **Réponse à la demande d’examen d’imagerie**
  * Structure de message HL7 v2: ORU_R01
  * Événement HL7 v2: R01 – Unsolicited transmission of observation (Order Control = OK ou OC)
* Flux métier: **Transmission d’un complément d’information post-acte**
  * Structure de message HL7 v2: OMI_O23
  * Événement HL7 v2: O23 – Imaging Order Message (Order Control = NW)

>  **(1) :** Le flux d'annulation est un flux **optionnel** dans le cadre du volet Téléradiologie. Son implémentation **n’est pas obligatoire** et peut être omise sans remettre en cause la conformité globale des échanges. 

### Interactions entre les acteurs

La présente partie décrit les interactions entre les acteurs du volet Téléradiologie, au travers de diagrammes de séquence illustrant les échanges de messages HL7 v2 identifiés précédemment.

Les interactions sont présentées flux par flux. Chaque diagramme s’appuie sur le **profil de messages HL7 v2 retenu**. Le [diagramme de séquence complet est fourni en annexe](./diag_sequence.md).

#### Flux 1 et 2 Transmission/Annulation d’une demande d’examen d’imagerie

Ce diagramme décrit les échanges techniques entre le RIS de la structure d’imagerie et le SI de téléradiologie pour la transmission et la gestion d’une demande d’examen d’imagerie.

 Figure 1 – Diagramme de séquence des flux 1 et 2 

La demande d’examen est transmise du RIS vers le SI de téléradiologie au moyen d’un message **HL7 v2 ORM^O01**.

Les options techniques suivantes sont représentées :

* lorsque la demande d’examen est disponible sous forme de document structuré, le RIS peut transmettre ce document au SI de téléradiologie en s’appuyant sur les transactions définies au sein du **volet de transmission de documents CDA-R2 en HL7 v2** ;
* lorsque plusieurs documents complémentaires sont associés à la demande, ceux-ci peuvent être transmis individuellement au SI de téléradiologie au travers de mécanismes également définis au sein du **volet transmission CDA-R2 en HL7 v2**.

Enfin, le diagramme illustre la **possibilité d’annulation de la demande d’examen** par le RIS, notifiée au SI de téléradiologie au moyen d’un message **HL7 v2 ORM^O01**, en cohérence avec les règles de gestion HL7 v2 et le profil IHE SWF.

#### Flux 3 Réponse à la demande d’examen d’imagerie

Ce diagramme décrit les échanges techniques consécutifs à la consultation et à l’évaluation d’une demande d’examen par le professionnel de santé effecteur au sein du SI de téléradiologie.

 Figure 2 – Diagramme de séquence du flux 3 

Après réception de la demande d’examen d’imagerie, le professionnel de santé effecteur procède à son **évaluation** (acceptation ou refus).
 Le résultat de cette évaluation est notifié à la structure d’imagerie par l’émission d’un message **HL7 v2 ORU^R01** depuis le SI de téléradiologie.

Les cas suivants sont couverts :

* **Acceptation de la demande** :
 le message **ORU^R01** contient un ou plusieurs **protocoles d’imagerie**, véhiculés dans les segments **OBX** ;
 le champ **ORC-1 (Order Control)** est valorisé à **OK**.
* **Refus de la demande** :
 le message **ORU^R01** est transmis **sans protocole d’imagerie** ;
 le champ **ORC-1 (Order Control)** est valorisé à **OC**.

#### Flux 4 Transmission d’un complément d’information post-examen

Ce diagramme décrit les échanges techniques intervenant après l’acceptation de la demande d’examen et la transmission du protocole d’imagerie.

 Figure 3 – Diagramme de séquence du flux 4 

À l’issue de cette acceptation, l’examen d’imagerie est réalisé au sein de la structure d’imagerie.
 Une fois l’examen effectué, le RIS transmet au SI de téléradiologie un ensemble de **compléments d’information post-examen**, destinés à permettre la **rédaction du compte rendu** par le professionnel de santé effecteur.

Ces informations sont transmises via un message **OMI^O23** conforme au profil IHE SWF.

Après rédaction du **compte rendu d’examen d’imagerie**, celui-ci est transmis par le SI de téléradiologie vers le RIS, afin de permettre sa **publication dans le DMP du patient**.

### Profils de message

La présente partie décrit les **profils de messages HL7 v2** retenus pour supporter les flux d’échange du volet Téléradiologie.
 Pour chaque flux identifié, le **type de message HL7 v2** associé est précisé, ainsi que la **structure générale des segments** utilisés afin de couvrir les concepts métiers attendus.

Les profils de message définissent :

* le **type de message HL7 v2** et l’événement associé ;
* l’**ordre des segments** ;
* les **segments requis, optionnels ou répétables** ;
* le rôle fonctionnel de chaque segment dans le cadre du flux considéré.

Des exemples représentatifs de chacun des profils de message conformes au volet Téléradiologie sont fournis [en annexe](./exemples.md).

#### Description des messages HL7 v2

L’implémentation doit valoriser l’intégralité des segments et champs obligatoires applicables aux messages HL7v2 afin de répondre au standard d’interopérabilité afférent.

Ci-dessous sont représentées les structures de messages **HL7 v2**, présentées selon deux vues complémentaires :

* une **vue technique**, sous forme de tableaux, décrivant de manière exhaustive la **structure des profils de messages** (segments, cardinalités et ordonnancement) ;
* une **vue fonctionnelle**, plus synthétique, matérialisée par des **diagrammes**, centrée sur les segments utilisés dans le cadre du volet Téléradiologie.

##### Flux 1 - Message ORM^O01^ORM_O01 en HL7 v2.5.1

Le flux 1 repose sur l’échange d’un message **ORM^O01** conforme à la norme **HL7 v2.5.1**, utilisé pour la **transmission d’une demande d’examen d’imagerie** dans le cadre du volet Téléradiologie.

La structure du message est **conforme au profil IHE RAD – Scheduled Workflow (SWF)**. Une **surcouche de contraintes spécifiques au domaine de la Téléradiologie** vient compléter ce cadre afin de couvrir des besoins fonctionnels non pris en charge nativement par IHE SWF.

###### Description technique

Le message est composé des segments principaux suivants :

* **MSH** : en-tête du message et informations de routage ;
* **PID / PV1** : identification du patient et du contexte de prise en charge ;
* **ORC** : informations liées à la demande d’examen, conformément à IHE SWF ;
* **OBR** : prescription de l’examen d’imagerie (modalité, indications, antécédents), conformément à IHE SWF ;
* **Groupes OBSERVATION (OBX)** : supporte les informations complémentaires spécifiques au volet Téléradiologie, non contraintes par IHE SWF.

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments ainsi que leur caractère requis, optionnel ou répétable.

* Segment: MSH
  * Meaning: Message Header
  * Usage: R
  * Card.: [1..1]
  * § HL7: 2
* Segment:  
  * Meaning: --- PATIENT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PID
  * Meaning: Patient Identification
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PV1
  * Meaning: Patient Visit
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  
  * Meaning: --- PATIENT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment: {
  * Meaning: --- ORDER begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  ORC
  * Meaning: Common Order
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment: {
  * Meaning: --- ORDER_DETAIL begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  OBR
  * Meaning: Observation Request
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment:  [{NTE}]
  * Meaning: Comments on the order
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  {
  * Meaning: --- OBSERVATION begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  OBX
  * Meaning: Observation
  * Usage: R
  * Card.: [1..1]
  * § HL7: 7
* Segment:  [{NTE}]
  * Meaning: Comment
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  }
  * Meaning: --- OBSERVATION end
  * Usage:  
  * Card.:  
  * § HL7:  

###### Description fonctionnelle

Le message **ORM^O01** du flux 1 permet au système demandeur (RIS) de transmettre au système effecteur (SI Téléradiologie) l’ensemble des informations associées à la prise en charge du patient ainsi que les éléments relatifs à une demande d’examen d’imagerie le concernant.

Outre les éléments standards concernant la demande et la prescription portés par les segments **ORC** et **OBR**, ce flux s’appuie sur des **groupes OBSERVATION (OBX)** afin de véhiculer des informations fonctionnelles complémentaires indispensables à la bonne réalisation de l’examen, telles que :

* la **localisation anatomique** et, le cas échéant, une **précision topographique**
* des **données morphologiques pertinentes** pour la planification de l’examen d’imagerie (taille, poids, statut de grossesse)

Ces groupes OBSERVATION sont **contraints par la présente spécification**, tant sur le plan sémantique que structurel (identification des OBX, cardinalités, types de données), afin de garantir une interprétation homogène par l’ensemble des acteurs.

Le diagramme ci-dessous illustre le **fonctionnement global du message**, les interactions entre les segments principaux ainsi que le rôle des **OBX spécifiques Téléradiologie** dans le cadre du flux 1.

##### Flux 2 - Message ORM^O01^ORM_O01 en HL7 v2.5.1

Le flux 2 repose sur l’échange d’un message **ORM^O01** conforme à la norme **HL7 v2.5.1**, utilisé pour **l’ annulation d’une demande d’examen d’imagerie** dans le cadre du volet Téléradiologie.

Ce flux est **structurellement très proche du flux 1** et s’appuie lui aussi sur le **profil IHE RAD – Scheduled Workflow (SWF)**, notamment pour les segments **ORC** et **OBR**, qui conservent les mêmes principes de structuration et de valorisation que pour la demande initiale.

La principale différence structurelle en comparaison avec le flux 1 concerne l’utilisation du **groupe OBSERVATION (OBX)** qui est optionnel dans le cadre de ce flux.

###### Description technique

Le message est composé des segments principaux suivants :

* **MSH** : en-tête du message et informations de routage
* **PID / PV1** : identification du patient et du contexte de prise en charge
* **ORC** : informations de demande, avec une action positionnée à l’annulation
* **OBR** : rappel des éléments de prescription nécessaires à l’identification de la demande annulée

* Segment: MSH
  * Meaning: Message Header
  * Usage: R
  * Card.: [1..1]
  * § HL7: 2
* Segment:  
  * Meaning: --- PATIENT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PID
  * Meaning: Patient Identification
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PV1
  * Meaning: Patient Visit
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  
  * Meaning: --- PATIENT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment: {
  * Meaning: --- ORDER begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  ORC
  * Meaning: Common Order
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment: {
  * Meaning: --- ORDER_DETAIL begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  OBR
  * Meaning: Observation Request
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment:  [{NTE}]
  * Meaning: Comments on the order
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  {
  * Meaning: --- OBSERVATION begin
  * Usage: O
  * Card.: [0..*]
  * § HL7:  
* Segment:  OBX
  * Meaning: Observation
  * Usage: R
  * Card.: [1..1]
  * § HL7: 7
* Segment:  [{NTE}]
  * Meaning: Comment
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  }
  * Meaning: --- OBSERVATION end
  * Usage:  
  * Card.:  
  * § HL7:  

###### Description fonctionnelle

Le message **ORM^O01** du flux 2 permet au système demandeur de notifier au système effecteur **l’annulation d’une demande d’examen d’imagerie précédemment transmise**.

Les segments **ORC** et **OBR** assurent l’identification de la demandee concernée et portent les informations nécessaires à sa mise à jour dans les systèmes récepteurs, conformément aux règles définies par le profil **IHE SWF**.

Le diagramme ci-dessous illustre le **fonctionnement du message d’annulation** :

##### Flux 3 - Message ORU^R01^ORU_R01 en HL7 v2.5.1

Le flux 3 repose sur l’échange d’un message **ORU^R01** conforme à la norme **HL7 v2.5.1**.
 Il est utilisé pour la **réponse à une demande d’examen d’imagerie**, en particulier pour notifier la **décision du médecin effecteur** (approbation/refus de la demande).

Contrairement aux flux 1, 2 et 4, ce flux **ne s’appuie sur aucun profil IHE** existant.
 En effet, les cas d’usage couverts par ce flux, notamment la transmission d’une décision médicale en réponse à une demande d’imagerie, ne disposent pas d’un équivalent direct dans les profils IHE RAD.
 Le message ORU^R01 est donc défini sur la base du standard HL7 v2.5.1, complété par une **surcouche de contraintes spécifiques au volet Téléradiologie**.

###### Description technique

Le message est structuré autour des segments suivants :

* **MSH** : en-tête du message et informations de routage
* **PID** : identification du patient
* **ORC** : décision du médecin effecteur sur la demande d’examen (validation ou refus), avec la possibilité de préciser un **motif de refus** le cas échéant
* **OBR** : rappel de la demande d’examen concernée
* **Groupes OBSERVATION (OBX)** : transmission des informations spécifiques au volet Téléradiologie, notamment le **protocole d’imagerie**, exprimé soit en clair, soit sous forme de contenu encapsulé.

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments, ainsi que leur caractère requis, optionnel ou répétable.

* Segment: MSH
  * Meaning: Message Header
  * Usage: R
  * Card.: [1..1]
  * § HL7: 2
* Segment:  
  * Meaning: --- PATIENT_RESULT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  
  * Meaning: --- PATIENT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PID
  * Meaning: Patient Identification
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT begin
  * Usage: O
  * Card.: [0..1]
  * § HL7:  
* Segment:  PV1
  * Meaning: Patient Visit
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  
  * Meaning: --- PATIENT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment: {
  * Meaning: --- ORDER_OBSERVATION begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  ORC
  * Meaning: Common Order
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment:  OBR
  * Meaning: Observation Request
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment:  [{NTE}]
  * Meaning: Comment
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment: [{
  * Meaning: --- TIMING begin
  * Usage: O
  * Card.: [0..*]
  * § HL7:  
* Segment:  TQ1
  * Meaning: Timing Quantity
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment: }]
  * Meaning: --- TIMING end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  {
  * Meaning: --- OBSERVATION begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  OBX
  * Meaning: Observation
  * Usage: R
  * Card.: [1..1]
  * § HL7: 7
* Segment:  [{NTE}]
  * Meaning: Comment
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  }
  * Meaning: --- OBSERVATION end
  * Usage:  
  * Card.:  
  * § HL7:  

###### Description fonctionnelle

Le message **ORU^R01** du flux 3 permet au système effecteur de transmettre au système demandeur la **réponse à la demande d’examen d’imagerie**.

Le segment **ORC** porte la **décision du médecin effecteur**, exprimée de manière :

* validation de la demande d’examen ;
* ou refus de la demande, accompagné le cas échéant d’un **motif de refus** optionnel.

Le segment **OBR** rappelle l’identification de la demande d’examen d’imagerie.

Le **groupe OBSERVATION (OBX)** est **conditionné à la valeur du champ ORC-1**. Il est **optionnel en cas de refus de la demande** et **obligatoire en cas d’acceptation**, afin de permettre la transmission d’**un ou plusieurs protocoles d’imagerie** selon l’une des modalités suivantes :

* protocole exprimé en clair dans le message
* protocole encapsulé sous forme de contenu binaire

Ces OBSERVATION sont structurées et identifiées conformément aux règles définies dans la partie [Contraintes applicables aux profils de message](./st-contraintes.md), notamment via l’utilisation de codes locaux dans **OBX-3**.

Le diagramme ci-dessous illustre le **fonctionnement du flux 3** :

##### Flux 4 - Message OMI^O23^OMI_023 en HL7 v2.5.1

Le flux 4 repose sur l’échange d’un message **OMI^O23** conforme à la norme **HL7 v2.5.1**.
 Il est utilisé pour la **transmission d’informations complémentaires post-acte** à la suite de la réalisation d’un examen d’imagerie dans le cadre du volet Téléradiologie.

Ce flux s’appuie sur les principes du **profil IHE RAD – Scheduled Workflow (SWF)**, dans la mesure où il s’inscrit dans la continuité du cycle de vie de la demande d’examen d’imagerie et de sa réalisation.
 Les segments structurants du message, notamment **ORC** et **OBR**, sont ainsi valorisés conformément aux règles définies par IHE SWF, complétées par une **surcouche de contraintes spécifiques au volet Téléradiologie**.

Le message **OMI^O23** permet de transmettre des informations qui ne sont pas nécessairement disponibles au moment de la construction de la demande d’examen, mais qui sont connues **après la réalisation effective de l’examen**.

###### Description technique

Le message est structuré autour des segments suivants :

* **MSH** : en-tête du message et informations de routage
* **PID / PV1** : identification du patient et du contexte de prise en charge
* **ORC** : informations de demande initiale
* **OBR** : informations relatives à l’examen réalisé
* **TQ1** : informations temporelles, notamment la date de réalisation de l’examen et la durée de rétention des images
* **IPC** : informations relatives à l’examen d’imagerie et à la modalité
* **Groupes OBSERVATION (OBX)** : transmission des compléments d’information post-acte spécifiques au volet Téléradiologie

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments ainsi que leur caractère requis, optionnel ou répétable.

* Segment: MSH
  * Meaning: Message Header
  * Usage: R
  * Card.: [1..1]
  * § HL7: 2
* Segment:  
  * Meaning: --- PATIENT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PID
  * Meaning: Patient Identification
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT begin
  * Usage: R
  * Card.: [1..1]
  * § HL7:  
* Segment:  PV1
  * Meaning: Patient Visit
  * Usage: R
  * Card.: [1..1]
  * § HL7: 3
* Segment:  
  * Meaning: --- PATIENT_VISIT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  
  * Meaning: --- PATIENT end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment: {
  * Meaning: --- ORDER begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  ORC
  * Meaning: Common Order
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment:  OBR
  * Meaning: Observation Request
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment:  [{NTE}]
  * Meaning: Comment
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment: [{
  * Meaning: --- TIMING begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  TQ1
  * Meaning: Timing Quantity
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
* Segment: }]
  * Meaning: --- TIMING end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  {
  * Meaning: --- OBSERVATION begin
  * Usage: R
  * Card.: [1..*]
  * § HL7:  
* Segment:  OBX
  * Meaning: Observation
  * Usage: R
  * Card.: [1..1]
  * § HL7: 7
* Segment:  [{NTE}]
  * Meaning: Comment
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  }
  * Meaning: --- OBSERVATION end
  * Usage:  
  * Card.:  
  * § HL7:  
* Segment:  IPC
  * Meaning: Imaging Procedure Control Segment
  * Usage: R
  * Card.: [1..*]
  * § HL7: 4

###### Description fonctionnelle

Le message **OMI^O23** du flux 4 permet au système demandeur (RIS) de transmettre au système effecteur (SI de Téléradiologie) des **compléments d’information post-acte** relatifs à un examen d’imagerie déjà réalisé.

Les segments **ORC** et **OBR** assurent le **rattachement** de ces informations à la demande d’examen initiale, conformément aux règles du profil **IHE SWF** et aux contraintes spécifiques définies par le volet Téléradiologie.

Les **groupes OBSERVATION (OBX)** jouent un rôle central dans ce flux.
 Ils permettent notamment de véhiculer :

* des éléments constitutifs de l’**URL de la visionneuse DRIMbox** donnant accès aux images ;
* les informations relatives aux **produits administrés** dans le cadre de la procédure (type, numéro de lot, quantité) ;
* les informations sur l’**appareil d’imagerie utilisé** ;
* la **localisation anatomique** ciblée par l’examen et les éventuelles précisions topographiques associées.

L’utilisation de ces groupes OBSERVATION est encadrée par des règles de structuration, de codification et de liaison entre segments, définies dans la surcouche Téléradiologie.

Le diagramme ci-dessous illustre le **fonctionnement du flux 4** :

**Figure 17 : Structure fonctionnelle du message ORU_R01**

#### Réponses et acquittements

Pour l’ensemble des flux décrits ci-dessus :

* Les messages HL7 font l’objet d’un **acquittement technique HL7 v2** (ACK) ;
* Les règles d’acquittement suivent les mécanismes natifs du standard HL7 v2.5.1.

Les modalités d’acquittement applicatif, le cas échéant, sont précisées dans les sections dédiées de la présente spécification.

### Contraintes applicables aux profils de message

Cette section précise les **contraintes d’implémentation** applicables aux profils de message identifiés précédemment.
 Elle est structurée selon deux niveaux complémentaires.

#### Contraintes communes à l’ensemble des messages

Un premier sous-ensemble de contraintes s’applique **de manière transversale à l’ensemble des messages HL7 v2 échangés**, quel que soit le flux concerné.
 Ces contraintes portent notamment sur les segments suivants :

* **MSH (Message Header)** : identification du message, des acteurs émetteur et récepteur, gestion des versions, horodatage, identifiants de message ;
* **PID (Patient Identification)** : identité du patient, traits d’identification et conformité aux exigences nationales, notamment en lien avec l’INS ;
* **PV1 (Patient Visit)** : contexte de prise en charge et éléments nécessaires à la qualification du séjour ou de l’acte.

Ces contraintes communes garantissent une **cohérence globale des échanges**, une identification fiable des acteurs et du patient, ainsi qu’une homogénéité de mise en œuvre entre les flux.

##### Eléments de contrôle du message ORU ou MDM

###### Le segment MSH – Header du message

Les éléments de contrôle du message HL7 sont portés par le segment d’entête MSH. Le tableau ci-dessous liste les champs à renseigner pour le segment MSH :

* Champ: MSH-1
  * Contenu: | séparateur de champ
  * Type donnée: ST
  * Caractère optionnel/obligatoire: R
* Champ: MSH-2
  * Contenu: ^~\& : séparateur de composant, répétition, caractère d'échappement, séparateur de sous-composants
  * Type donnée: ST
  * Caractère optionnel/obligatoire: R
* Champ: MSH-3
  * Contenu: Application émettrice
  * Type donnée: HD
  * Caractère optionnel/obligatoire: R
* Champ: MSH-4
  * Contenu: Organisation émettrice
  * Type donnée: HD
  * Caractère optionnel/obligatoire: R
* Champ: MSH-5
  * Contenu: Application réceptrice
  * Type donnée: HD
  * Caractère optionnel/obligatoire: R
* Champ: MSH-6
  * Contenu: Organisation réceptrice
  * Type donnée: HD
  * Caractère optionnel/obligatoire: R
* Champ: MSH-7
  * Contenu: Horodatage du message
  * Type donnée: TS
  * Caractère optionnel/obligatoire: R
* Champ: MSH-9
  * Contenu: Type du messageORM^O01^ORM_O01ORU^R01^ORU_R01OMI^O23^OMI_O23
  * Type donnée: MSG
  * Caractère optionnel/obligatoire: R 
* Champ: MSH-10
  * Contenu: Identifiant du message
  * Type donnée: ST
  * Caractère optionnel/obligatoire: R
* Champ: MSH-11
  * Contenu: Processing Id  P  : en production  T  : message de test  D : environnement de debug
  * Type donnée: PT
  * Caractère optionnel/obligatoire: R
* Champ: MSH-12
  * Contenu: Version du standard 2.5.1
  * Type donnée: VID
  * Caractère optionnel/obligatoire: R
* Champ: MSH-17
  * Contenu: FRA
  * Type donnée: ID
  * Caractère optionnel/obligatoire: R
* Champ: MSH-18
  * Contenu: Jeux de caractères, valeurs possibles :UNICODE UTF-8 ou 8859/15
  * Type donnée: ID
  * Caractère optionnel/obligatoire: R
* Champ: MSH-21
  * Contenu: Identifiant du profil de messageMSH-21.1 : Entity Identifier (2.1)MSH-21.2 : Namespace IdCISIS_TLR_HL7_V2 
  * Type donnée: EI
  * Caractère optionnel/obligatoire: R

###### Exemples

Entête MSH d’un message ORM :

`MSH|^~\&|RIS|CHU_X|SI-TLR|PLAT-TLR|202310030830||ORM^O01^ORM_O01|12345|P|2.5.1|||||FRA|8859/15|||2.1^ CISIS_TLR_HL7_V2`

##### Les données concernant le patient et la venue du patient

Le message HL7 est centré sur un seul patient. Les informations concernant le patient sont décrites par le segment requis PID. Le segment PV1, requis, représente la venue courante du patient.

Ces deux segments doivent être renseignés conformément à la spécification « [PAM – National extension France » version 2.11](https://www.interopsante.org/publications) publiée en 2024. Si l’INS est véhiculé, le segment PID doit suivre les contraintes décrites dans l’annexe CI-SIS « [Prise en charge de l’identifiant National de Santé (INS) dans les standards d’interopérabilité et les volets du CI-SIS](https://esante.gouv.fr/annexe-prise-en-charge-de-lins-dans-les-volets-du-ci-sis) ».

Pour le segment PID, ce volet ajoute une contrainte particulière sur le PID-18 par rapport à PAM.FR. Il doit être renseigné si connu afin de pouvoir calculer des indicateurs, dans le contexte de l’alimentation du DMP.

* Champ: PID-3
  * Contenu: Identifiants du patient
  * Type donnée: CX
  * Caractère optionnel/obligatoire: R
* Champ: PID-5
  * Contenu: Nom du patient
  * Type donnée: XPN
  * Caractère optionnel/obligatoire: R
* Champ: PID-18 (2)
  * Contenu: N° de dossier administratif
  * Type donnée: CX
  * Caractère optionnel/obligatoire: RE

Le PID-3 doit être identique aux identifiants de patient portés par le document CDA (recordTarget/patientRole/id).

Pour le segment PV1, ce volet ajoute les contraintes suivantes :

* Champ: PV1-2
  * Contenu: Classe du patient 
  * Type donnée: IS
  * Caractère optionnel/obligatoire: R
* Champ: PV1-19 (2)(4) 
  * Contenu: Identifiant de la venue
  * Type donnée: CX
  * Caractère optionnel/obligatoire:  C (3)
* Champ: PV1-44 (2)
  * Contenu: Date d'entrée du patient
  * Type donnée: TS
  * Caractère optionnel/obligatoire: RE
* Champ: PV1-45 (2)
  * Contenu: Date de sortie du patient
  * Type donnée: TS
  * Caractère optionnel/obligatoire: RE

>  **(2) :** A noter que ces champs sont à renseigner, s'ils sont connus, par le système expéditeur afin de pouvoir calculer des indicateurs. 

>  **(3) :** Le champ PV1-19 est requis lorsque le PV1-2 prend la valeur E, I, O ou R. Si PV1-2 prend la valeur N alors PV1-19 est requis si connu. 

>  **(4) :** Dans le cadre du volet Téléradiologie, le champ PV1-19 Visit Number est utilisé pour véhiculer l’identifiant du rendez-vous issu des flux SIU. 

#### Contraintes spécifiques au volet Téléradiologie

Un second niveau de contraintes est défini **spécifiquement pour chaque flux**, en fonction du type de message et du rôle fonctionnel attendu.
 Ces contraintes portent notamment sur les segments métiers suivants, selon les flux :

* **ORC (Common Order)** : gestion de la demande, de son cycle de vie et de ses états ;
* **OBR (Observation Request)** : description de l’examen, des actes et de leurs identifiants ;
* **OBX (Observation Result)** : transmission d’informations cliniques structurées ou de références documentaires ;
* **IPC (Imaging Procedure Control)** : partage du contexte de réalisation des études et procédures d’imagerie.

Pour chaque flux, les contraintes précisent :

* les **segments obligatoires et optionnels** ;
* les **champs requis, conditionnels ou interdits** ;
* les **règles de cardinalité, de codage et de valeurs attendues** ;
* les éventuelles **références aux profils IHE ou spécifications nationales** applicables.

##### Flux 1 - Transmission de la demande d’examen d’imagerie

Ce flux repose sur l’utilisation d’un messages **ORM^O01**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les **groupes OBSERVATION** (segments OBX), non contraints et optionnels dans le cadre du profil IHE SWF, sont **explicitement contraints par le volet téléradiologie**. Ces contraintes permettent notamment de structurer et de normaliser la transmission d’informations complémentaires nécessaires à la compréhension de la demande d’examen d’imagerie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie.

* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: **Segment ORC**
  * ?: **Common Order**
  * ?:  
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-1
  * ?: Order control
  * ?: Valeur fixée à « NW » (New order/service)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen d'imagerie (Order Placer Number)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-9
  * ?: Date/Time of Transaction
  * ?: Date à laquelle la demande d'examen a été réalisée
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-11 (Requis si connu)
  * ?: Verified By
  * ?: Informations relatives au professionnel de santé effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-12
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé responsable de la structure d’imagerie qui accueille le patient et supervise la réalisation de l’acte d’imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-14 (Requis si connu)
  * ?: Call Back Phone Number
  * ?: Numéro de téléphone à appeler pour obtenir des précisions sur la demande d'examen d'imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-17
  * ?: Entering Organization
  * ?: Qualifie le type d'organisation (5)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-17.1 
  * ?: Code 
  * ?: STRUCTURE_IMAGERIE
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-17.3 
  * ?: Name of Coding system
  * ?: TLR_TYPE_ORGANISATION
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-21
  * ?: Ordering Facility Name
  * ?: 
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.1
  * ?: OrganizationName
  * ?: Nom de l'organisation (structure d'imagerie)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.6
  * ?: Assigning Authority
  * ?: Autorité d'affectation de l'identifiant de l'organisation1.2.250.1.71.4.2.2 (OID de gestion des structures pour préciser une entité juridique ou une entité géographique), N° FINESS ou N° FINEG pour identifier une organisation intra-établissement (service, UF, pôle…).[Cf Contraintes sur les types de données HL7 v2.5 applicables aux profils d'intégration du cadre technique IT Infrastructure dans le périmètre d'IHE France](https://www.interopsante.org/publications).
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.7
  * ?: Identifier Type Code
  * ?: Type d'identifiant (valeur issue de la [Table 0203 - Interop'Santé](https://www.interopsante.org/publications) présent dan le document "Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure dans le périmètre d’IHE France") : FINEJ (FINESS d'entité juridique) ou FINEG (FINESS d'entité géographique) ou IDNST ou UF (UF), SVR (service).
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.10
  * ?: Organization number
  * ?: Identifiant de l'organisation

>  **(5) :** Conformément au profil IHE RAD – Scheduled Workflow (SWF), le champ ORC-17 – Entering Organization est renseigné dans les flux concernés. Dans le cadre du volet Téléradiologie, ce champ est utilisé pour qualifier le type d’organisation à l’origine du message (par exemple : structure d’imagerie, plateforme de téléradiologie), sur la base d’une [table de valeurs locale documentée](./table_orga.md). L’identification de l’organisation est portée dans le champ ORC-21 – Ordering Facility Name, de type XON, permettant de véhiculer un identifiant structuré et pérenne, conformément aux principes retenus dans le CI-SIS. Ce découplage permet de respecter les exigences IHE tout en garantissant une identification robuste. 

##### Segment OBR (Observation Request)

Le segment **OBR** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Les champs présentés dans le tableau ci-après sont **requis** ou **requis si connus**, selon leur pertinence dans le cadre du workflow de téléradiologie.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-2)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code
  * ?: Code de la modalité d'imagerie, utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Display name
  * ?: 
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Name of Coding system
  * ?:  DCM
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-13 (Requis si connu)
  * ?: Relevant Clinical Information
  * ?: Antécédents du patient pertinents dans le cadre de l'examen demandé
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé responsable (identique à l'ORC-12)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-31
  * ?: Reason for Study
  * ?: Justification de la demande d'examen (type CE)Lorsque la justification peut être exprimée à l’aide d’un code, celui-ci doit être renseigné dans CE-1, avec le système de codage associé précisé en CE-3.À défaut de codage disponible, la justification peut être transmise sous forme de texte libre dans CE-2 – Text.

##### Groupes OBSERVATION - Localisation anatomique

Ces groupes **OBSERVATION** sont utilisés afin de véhiculer les informations relatives à la **localisation anatomique concernée par la demande d’examen d’imagerie**. Ces informations permettent de préciser la zone anatomique à explorer et, le cas échéant, d’apporter un niveau de détail complémentaire facilitant l’interprétation et la réalisation de l’examen.

La localisation anatomique est portée par un **premier segment OBX obligatoire**, pouvant être complété par un **second segment OBX optionnel** destiné à préciser la topographie de manière plus fine. Les segments OBX portant sur la localisation anatomique sont identifiés par un code local “LOCALISATION_ANATOMIQUE” dans **OBX-3**, [documenté en annexe](./table_obs.md). Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION - Localisation anatomique principale

Ce groupe est composé d’un segment OBX obligatoire permettant d’indiquer la **localisation anatomique principale** de l’examen demandé.

* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-2
  * ?: Value Type
  * ?: CE (Coded Entry)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.1 
  * ?: Code 
  * ?: LOCALISATION_ANATOMIQUE
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Localisation anatomique examinée dans le cadre de l’examen d’imagerie
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.1**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.1
  * ?: Code 
  * ?: Valeur issue du JDV [JDV_RegionAnatomique-CISIS](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-region-anatomique-cisis.html)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.3
  * ?: Name Of Coding System
  * ?: SNT
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Groupe OBSERVATION - Précision topographique

Ce groupe est composé d’un segment OBX optionnel permettant de compléter la localisation anatomique principale par une **précision topographique**.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: CE (Coded Entry)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: LOCALISATION_ANATOMIQUE
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Localisation anatomique examinée dans le cadre de l’examen d’imagerie
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.2**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-5.1
  * ?: Code 
  * ?: Valeur issue du JDV [JDV_ModificateurTopographique-CISIS](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modificateur-topographique-cisis.html)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-5.3
  * ?: Name Of Coding System
  * ?: SNT
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Groupe OBSERVATION - Taille corporelle

Ce groupe **OBSERVATION** optionnel est utilisé afin de véhiculer la **taille corporelle du patient**, lorsque celle-ci est nécessaire à la réalisation de l’examen d’imagerie. La taille du patient est véhiculée par l’intermédiaire d’un segment OBX.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: NM (Numeric)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: 8302-2
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Body height
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: LN
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Taille du patient
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-6
  * ?: Units
  * ?: Unité
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Groupe OBSERVATION - Poids corporel

Ce groupe **OBSERVATION** optionnel est utilisé afin de véhiculer le **poids corporel du patient**, lorsque cette donnée est nécessaire pour la réalisation de l’examen d’imagerie. Le poids du patient est véhiculé par l’intermédiaire d’un segment OBX.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: NM (Numeric)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: 29463-7
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Body weight
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: LN
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Poids du patient
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-6
  * ?: Units
  * ?: Unité
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Groupe OBSERVATION - Statut grossesse

Ce groupe **OBSERVATION** optionnel est utilisé afin de véhiculer le **statut de grossesse** de la personne prise en charge, lorsque cette information est pertinente pour la réalisation de l’examen d’imagerie.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: CE (Coded Entry)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: 82810-3
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Pregnancy status
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: LN
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-5.1
  * ?: Code 
  * ?: Table HL7 : 0136 :·  Y (Yes) -> Personne prise en charge enceinte · N (No) -> Personne prise en charge non enceinte
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-5.3
  * ?: Name Of Coding System
  * ?: expandedYes-NoIndicator
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Flux 2 - Annulation de la demande d’examen d’imagerie

Ce flux repose sur l’utilisation d’un messages **ORM^O01**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer l’**annulation d’une demande d’examen d’imagerie**, conformément au profil **IHE Scheduled Workflow (SWF)** .

La structure du segment ORC est **identique à celle du flux 1**, à l’exception du champ **ORC-1 – Order Control**, dont la valeur est fixée à **CA (Cancel Order)**.
 Un **motif d’annulation** peut être véhiculé lorsque cette information est disponible, son renseignement est **optionnel**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus** ou **optionnel**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie.

* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: **Segment ORC**
  * ?: **Common Order**
  * ?:  
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-1
  * ?: Order control
  * ?: Valeur fixée à « CA » (Canceled)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-9
  * ?: Date/Time of Transaction
  * ?: Date à laquelle la demande d'examen a été annulée
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-11 (Requis si connu)
  * ?: Verified By
  * ?: Informations relatives au Médecin effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-12
  * ?: Ordering Provider
  * ?: Informations relatives au Professionnel de santé de la structure d’imagerie qui accueille le patient et supervise la réalisation de l’acte d’imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-14 (Requis si connu)
  * ?: Call Back Phone Number
  * ?: Numéro de téléphone à appeler pour obtenir des précisions sur la demande d'examen d'imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-16 (Optionnel)
  * ?: Order Control Code Reason
  * ?: Motif d'annulation de la demande d'examen (type CE)Peut être exprimé à l’aide d’un code renseigné dans CE-1 – Identifier, avec le système de codage correspondant précisé en CE-3 – Name of Coding System (code local ou standard).À défaut de codage disponible, un libellé en clair peut être renseigné dans CE-2 – Text.
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-17
  * ?: Entering Organization
  * ?: Qualifie le type d'organisation (voir [Note 1](specifications_techniques.md#segment-orc-common-order))
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-17.1 
  * ?: Code 
  * ?: STRUCTURE_IMAGERIE
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-17.3 
  * ?: Name of Coding system
  * ?: TLR_TYPE_ORGANISATION
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-21
  * ?: Ordering Facility Name
  * ?: 
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.1
  * ?: OrganizationName
  * ?: Nom de l'organisation
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.6
  * ?: Assigning Authority
  * ?: Autorité d'affectation de l'identifiant de l'organisation1.2.250.1.71.4.2.2 (OID de gestion des structures pour préciser une entité juridique ou une entité géographique), N° FINESS ou N° FINEG pour identifier une organisation intra-établissement (service, UF, pôle…).[Cf Contraintes sur les types de données HL7 v2.5 applicables aux profils d'intégration du cadre technique IT Infrastructure dans le périmètre d'IHE France](https://www.interopsante.org/publications).
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.7
  * ?: Identifier Type Code
  * ?: Type d'identifiant (valeur issue de la [Table 0203 - Interop'Santé](https://www.interopsante.org/publications) présent dan le document "Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure dans le périmètre d’IHE France") : FINEJ (FINESS d'entité juridique) ou FINEG (FINESS d'entité géographique) ou IDNST ou UF (UF), SVR (service).
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.10
  * ?: Organization number
  * ?: Identifiant de l'organisation destinataire

##### Segment OBR (Observation Request)

Le segment **OBR** est utilisé pour véhiculer des informations relatives à la **demande d’examen d’imagerie**.
 Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-2)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code
  * ?: Code de la modalité d'imagerie, utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Display name
  * ?: 
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Name of Coding system
  * ?:  DCM
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé responsable (identique à l'ORC-12)

##### Flux 3 - Réponse à la demande d’examen d’imagerie

Ce flux repose sur l’utilisation de messages **ORU^R01**, conformes au standard **HL7 v2.5.1**.

Les segments ci-dessous sont définis sur la base du standard HL7 v2.5.1, complété par une **surcouche de contraintes spécifiques à la téléradiologie**, décrite dans les sections suivantes.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer la **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie.

Le champ **ORC-1 – Order Control** permet d’indiquer la décision prise sur la demande, à savoir sa **validation** ou son **refus**. En cas de refus, un **motif de refus** peut être transmis lorsque cette information est disponible ; son renseignement est **optionnel**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus** ou **optionnel**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie.

* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: **Segment ORC**
  * ?: **Common Order**
  * ?:  
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-1
  * ?: Order control
  * ?: Décision du médecin effecteur à distance vis-à-vis de la demande d'examenOK (Order/service accepted & OK) dans le cas d'une demande d'examen validéeOC (Order/service canceled) dans le cas d'une demande d'examen refusée
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen d'imagerie (Order Placer Number)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-12
  * ?: Ordering Provider
  * ?: Informations relatives au Médecin effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-16 (Optionnel)
  * ?: Order Control Code Reason
  * ?: Motif du refus de la demande d'examen (type CE)Peut être exprimé à l’aide d’un code renseigné dans CE-1 – Identifier, avec le système de codage correspondant précisé en CE-3 – Name of Coding System (code local ou standard).À défaut de codage disponible, un libellé en clair peut être renseigné dans CE-2 – Text.
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-17
  * ?: Entering Organization
  * ?: Qualifie le type d'organisation (voir [Note 1](specifications_techniques.md#segment-orc-common-order))
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-17.1 
  * ?: Code 
  * ?: PLATEFORME_TELERADIOLOGIE
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-17.3 
  * ?: Name of Coding system
  * ?: TLR_TYPE_ORGANISATION
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-21
  * ?: Ordering Facility Name
  * ?: 
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.1
  * ?: OrganizationName
  * ?: Nom de l'organisation
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.6
  * ?: Assigning Authority
  * ?: Autorité d'affectation de l'identifiant de l'organisation1.2.250.1.71.4.2.2 (OID de gestion des structures pour préciser une entité juridique ou une entité géographique), N° FINESS ou N° FINEG pour identifier une organisation intra-établissement (service, UF, pôle…).[Cf Contraintes sur les types de données HL7 v2.5 applicables aux profils d'intégration du cadre technique IT Infrastructure dans le périmètre d'IHE France](https://www.interopsante.org/publications).
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.7
  * ?: Identifier Type Code
  * ?: Type d'identifiant (valeur issue de la [Table 0203 - Interop'Santé](https://www.interopsante.org/publications) présent dan le document "Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure dans le périmètre d’IHE France") : FINEJ (FINESS d'entité juridique) ou FINEG (FINESS d'entité géographique) ou IDNST ou UF (UF), SVR (service).
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: > ORC-21.10
  * ?: Organization number
  * ?: Identifiant de l'organisation destinataire du document

##### Segment OBR (Observation Request)

Le segment **OBR** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-2)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code
  * ?: Code de la modalité d'imagerie, utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Display name
  * ?: 
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Name of coding system
  * ?:  DCM
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé effecteur à distance (identique à l'ORC-12)

##### Groupe OBSERVATION - Protocole d’imagerie

Le **groupe OBSERVATION** est requis dans le cadre d’une demande d’examen d’imagerie acceptée (ORC-1 = OK) afin de véhiculer le **protocole d’imagerie** associé à l’examen. Ce groupe est **répétable** afin de permettre, le cas échéant, la transmission de plusieurs protocoles d’imagerie distincts.
 Le protocole d’imagerie est porté par un **segment OBX unique** au sein du groupe OBSERVATION. Deux alternatives d’encodage sont proposées, en fonction du niveau de structuration et du contenu du protocole à transmettre :

* **Protocole en clair** : transmission du protocole sous forme de texte lisible directement dans le message HL7, à l’aide du type de données **FT (Formatted Text)**.
* **Protocole encapsulé** : transmission du protocole sous forme de document encapsulé (par exemple PDF, XML ou texte structuré), encodé en **base64** et véhiculé à l’aide du type de données **ED (Encapsulated Data)**.

Ces deux alternatives sont exclusives : un seul segment OBX est utilisé pour porter le protocole d’imagerie, avec le type de données adapté au mode de transmission retenu. Le choix de l’alternative relève des capacités des systèmes émetteurs et récepteurs et doit être cohérent avec les besoins métier du flux. Le segment OBX portant sur le protocole est identifié par un code local “PROTOCOLE_IMAGERIE” dans **OBX-3**, [documenté en annexe](./table_obs.md).

###### Protocole d’imagerie en clair

Cette alternative permet de transmettre le **protocole d’imagerie en clair**, sous forme de texte formaté directement exploitable par un utilisateur.
 Le contenu peut inclure des retours à la ligne et une structuration légère facilitant la lecture humaine.

* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-2
  * ?: Value Type
  * ?: FT (Formated Text)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-3
  * ?: Observation Identifier
  * ?: 
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.1 
  * ?: Code 
  * ?: PROTOCOLE_IMAGERIE
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Protocole d'imagerie médicale
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?: Protocole d'imagerie
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Protocole d’imagerie encapsulé

Cette alternative permet de transmettre le **protocole d’imagerie sous forme encapsulée**, en utilisant le type de données ED.
 Le protocole est encodé en **base64** et peut correspondre à un document structuré (PDF, XML, ou autre format convenu entre les acteurs).

* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-2
  * ?: Value Type
  * ?: ED (Encapsuled Data)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.1 
  * ?: Code 
  * ?: PROTOCOLE_IMAGERIE
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Protocole d'imagerie médicale
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.2
  * ?: Type
  * ?: TEXT (Machine readable text document)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.4
  * ?: Encoding
  * ?: Base64
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.5
  * ?: Data
  * ?: Intégrer le protcole d'imagerie PDF en base64
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Flux 4 - Transmission d’un complément d’information post-acte

Ce flux repose sur l’utilisation d’un messages **OMI^O23**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les **groupes OBSERVATION** (segments OBX), non contraints et optionnels dans le cadre du profil IHE SWF, sont **explicitement contraints par le volet téléradiologie** afin de permettre la transmission normalisée des informations post-acte nécessaires, telles que les produits administrés, l’appareil d’imagerie utilisé ou les informations de restitution des images.

Les sections suivantes décrivent les contraintes appliquées aux segments du message OMI^O23 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est renseigné conformément aux spécifications du profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: **Segment ORC**
  * ?: **Common Order**
  * ?:  
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-1
  * ?: Order control
  * ?: Valeur fixée à « NW (New order/service)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen d'imagerie (Order Placer Number)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-3
  * ?: Filler Order Number
  * ?: Identifiant de la demande d'examen d'imagerie (Order Placer Number)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-5
  * ?: Order Status
  * ?: Valeur fixée à « SC (Scheduled)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-9
  * ?: Date/Time of Transaction
  * ?: 

###### Segment TQ1 (Timing/Quantity)

Le segment **TQ1 – Timing/Quantity** est utilisé pour véhiculer les informations temporelles relatives à l’**examen d’imagerie réalisé**.
 Il est renseigné conformément aux spécifications du profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment TQ1 : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment TQ1 : Usage = Required / Cardinalité = [1..1]: **Segment TQ1**
  * ?: **Timing/Quantity**
  * ?:  
* Composition du segment TQ1 : Usage = Required / Cardinalité = [1..1]: TQ1-6
  * ?: Service Duration
  * ?: Durée de rétention des images
* Composition du segment TQ1 : Usage = Required / Cardinalité = [1..1]: TQ1-7
  * ?: Start date/time
  * ?: Date/heure de l'examen d'imagerie

##### Segment OBR (Observation Request)

Le segment **OBR – Observation Request** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-2)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code
  * ?: Code LOINC de l’acte d’imagerie, utiliser le [JDV_CodeDocumentImagerieCisis-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-code-document-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Display name
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Name of Coding system
  * ?:  LN
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé effecteur à distance (identique à l'ORC-12)

##### Segment IPC (Imaging Procedure Control)

Le segment **IPC – Imaging Procedure Control** est utilisé dans le cadre du **flux 4** pour véhiculer les informations spécifiques à la **procédure d’imagerie réalisée**.
 Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: **Segment IPC**
  * ?: **Imaging Procedure Control**
  * ?:  
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: IPC-1
  * ?: Accession Identifier
  * ?: 
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: IPC-2
  * ?: Requested Procedure ID
  * ?: Accession number
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: IPC-3
  * ?: Study Instance UID
  * ?: 
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: IPC-4
  * ?: Scheduled Procedure Step ID
  * ?: 
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: >IPC-5.1
  * ?: Code
  * ?: Code de la modalité d'imagerie, utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: >IPC-5.2
  * ?: Display name
  * ?: 
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: >IPC-5.3
  * ?: Name of Coding system
  * ?:  DCM

##### Groupe OBSERVATION - URL de viewer DRIMbox

Ce **groupe OBSERVATION** est utilisé afin de véhiculer l’**URL d’accès à la vieweuse DRIMbox**, permettant la consultation à distance des images issues de l’examen d’imagerie.

L’URL de la vieweuse est portée par un **segment OBX unique** au sein du groupe OBSERVATION. Elle est transmise sous forme de texte. La valeur portée dans **OBX-5** correspond à une URL complète, pouvant inclure des paramètres de requête nécessaires à l’accès sécurisé à la vieweuse. Les caractères spéciaux éventuellement présents dans l’URL sont encodés conformément aux règles d’échappement HL7 v2.5.1 (6), afin d’assurer l’intégrité de l’information transmise. Le segment OBX portant sur le protocole est identifié par un code local “URL_VIEWER_DRIMBOX” dans **OBX-3**, [documenté en annexe](./table_obs.md).

* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-2
  * ?: Value Type
  * ?: TX (Text Data)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.1 
  * ?: Code 
  * ?: URL_VIEWER_DRIMBOX
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.2 
  * ?: Display name 
  * ?: URL de la visionneuse DRIMbox
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?: URL du viewer DRIMbox
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

>  **(6) :** Les séquences d’échappement sont encadrées par le caractère d’échappement défini dans MSH-2 ( `\`) et permettent de représenter notamment : 
* le séparateur de champs (|) via \F\ ;
* le séparateur de composants (^) via \S\ ;
* le séparateur de répétitions (~) via \R\ ;
* le séparateur de sous-composants (&) via \T\ ;
* le caractère d’échappement lui-même (\) via \E\.

##### Groupes OBSERVATION - Localisation anatomique

Les groupes **OBSERVATION – Localisation anatomique** sont **optionnel** dans le cadre du flux 4.
 Leur présence permet de transmettre les informations relatives à la localisation anatomique concernée par l’examen réalisé, ainsi que, le cas échéant, une précision topographique associée. La structure, le contenu et les contraintes applicables à ces groupes OBSERVATION sont strictement identiques à ceux définis pour le flux 1.
 Pour le détail des segments OBX, se référer à la section dédiée du flux 1 : [Groupes OBSERVATION – Localisation anatomique](./st_flux1.md#Groupes-OBSERVATION---Localisation-anatomique)

##### Groupes OBSERVATION - Produit administré

Les groupes **OBSERVATION – Produit administré** sont **optionnels** et permettent de transmettre les informations relatives aux produits administrés lors d’un examen d’imagerie.

Chaque ensemble d’informations associées à un produit donné est portée dans **un groupe OBSERVATION** et un segment OBX distincts.
 Les groupes sont répétables pour permettre la transmission d’informations associées à plusieurs produits administrés au cours du même examen.
 Pour assurer la cohérence des informations :

* le **type de produit** et le **numéro de lot** sont **indissociables**,
* la **quantité administrée** est facultative mais recommandée lorsque le produit est renseigné.

Les segments OBX portant sur le produit administré sont identifiés par un code local “PRODUIT_ADMINISTRE” dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION – Type de produit

Ce groupe OBSERVATION permet de transmettre le **type de produit administré**. La valeur est codée à partir du **Jeu de Valeurs ATC niveau 2**, limité aux classes :

* V09 – Produits de diagnostic
* V10 – Produits thérapeutiques

Un segment OBX unique au sein de ce groupe porte la valeur codée dans **OBX-5**.
 Ce groupe est obligatoirement associé au groupe **Numéro de lot**.

* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: CE (Coded Entry)
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: PRODUIT_ADMINISTRE
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Produit administré lors de l'examen d'imagerie
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.1**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?:  
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-5.1
  * ?: Code 
  * ?: Valeur issue du JDV ATC niveau 2 “V09” ou “V10”.</a>
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-5.3
  * ?: Name Of Coding System
  * ?: ATC
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Groupe OBSERVATION – Numéro de lot

Ce groupe OBSERVATION permet de transmettre le **numéro de lot** du produit administré, garantissant la traçabilité et l’identification précise du produit.
 Le segment OBX unique au sein de ce groupe porte le numéro de lot dans **OBX-5**.
 Ce groupe doit être présent si le groupe Type de produit est renseigné.

* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: NM (Numeric)
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: PRODUIT_ADMINISTRE
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Produit administré lors de l'examen d'imagerie
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.2**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Numéro de lot du radiopharmaceutique adminsitré
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Groupe OBSERVATION – Quantité de produit administré

Ce groupe OBSERVATION permet de transmettre la quantité réellement administrée du produit. Le segment OBX unique au sein de ce groupe porte la valeur dans **OBX-5** et l’unité de mesure dans **OBX-6** (par exemple millilitres ou milligrammes).
 La quantité est **optionnelle** mais fortement recommandée lorsque le produit est renseigné.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: NM (Numeric)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: PRODUIT_ADMINISTRE
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Produit administré lors de l'examen d'imagerie
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.3**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Volume de radiopharmeutique administré
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-6
  * ?: Units
  * ?: Unité
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Groups OBSERVATION - Appareil d’imagerie utilisé

Les groupes **OBSERVATION – Appareil d’imagerie utilisé** sont **optionnels**. Lorsqu’ils sont présents, ils permettent de transmettre les informations relatives à l’appareil d’imagerie ayant été utilisé pour la réalisation de l’examen, en particulier dans le cas des techniques irradiantes. Les informations relatives à l’appareil sont portées dans **deux groupes OBSERVATION distincts** :

* un groupe dédié à l’**identifiant unique de l’appareil d’imagerie**,
* un groupe dédié au **modèle de l’appareil d’imagerie**.

Ces groupes peuvent être utilisés conjointement ou indépendamment, selon le niveau d’information disponible, l’identifiant de l’appareil constituant l’information principale de référence. Les segments OBX portant sur le produit administré sont identifiés par un code local “APPAREIL_IMAGERIE” dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION – Identifiant de l’appareil d’imagerie

Ce groupe OBSERVATION permet de transmettre l’identifiant unique de l’appareil d’imagerie utilisé lors de l’examen. L’identifiant correspond au **Support IUD**, tel que communiqué via un dispositif d’identification automatique (AIDC) ou, le cas échéant, via son marquage en clair. Le groupe contient un **segment OBX unique** portant la valeur de l’identifiant dans **OBX-5**.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: TX (Text Data)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: APPAREIL_IMAGERIE
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Appareil d'imagerie utilisé lors de l'examen
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.1**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Identifiant de l'appareil d'imagerie : SupportIUD voir SFE 2.1.7.4.3
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Groupe OBSERVATION – Modèle de l’appareil d’imagerie

Ce groupe OBSERVATION permet de transmettre le modèle de l’appareil d’imagerie utilisé. La valeur est exprimée sous forme de texte libre et correspond à la dénomination du modèle fournie par le constructeur. Le groupe contient un **segment OBX unique** portant le modèle de l’appareil dans **OBX-5**.
 Ce groupe est **optionnel** et vient compléter l’identifiant de l’appareil lorsqu’une information plus détaillée sur l’équipement est requise.

* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: **Segment OBX**
  * ?: **Observation/Result**
  * ?:  
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-1
  * ?: Set Id - Obx
  * ?: Numéro de séquence du segment
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-2
  * ?: Value Type
  * ?: TX (Text Data)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: APPAREIL_IMAGERIE
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Display name 
  * ?: Appareil d'imagerie utilisé lors de l'examen
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLR_OBSERVATION
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: Valeur fixée à n.2**Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](./sub-id.md)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Modèle de l’appareil d’imagerie utilisé
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

