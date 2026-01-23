# Volume 2 : Détail des transactions - Volet Téléradiologie v0.1.0

* [**Table of Contents**](toc.md)
* **Volume 2 : Détail des transactions**

## Volume 2 : Détail des transactions

### Introduction

La présente spécification technique définit les modalités d’échange des informations de téléradiologie au moyen du standard **HL7 version 2.5.1**. Elle a pour objectif de préciser les profils de messages, segments, champs, cardinalités et règles d’usage nécessaires à l’interopérabilité entre les systèmes d’information impliqués dans les processus de téléradiologie, particulèrement les RIS et les plateformes de téléradiologie.

Cette spécification s’applique exclusivement aux flux identifiés dans la [Spécification Fonctionnelle des Echanges](./specifications_fonctionnelles.md). Elle ne constitue pas une implémentation exhaustive du standard HL7 v2, mais en restreint l’usage aux éléments nécessaires pour couvrir les cas d’usage fonctionnels définis.

Les échanges sont basés sur des messages HL7 v2 conformes à la version **2.5.1**. Lorsque cela est applicable, la spécification s’appuie sur les profils du domaine **IHE Radiology**, et notamment le profil **IHE Scheduled Workflow (SWF.b)**, afin d’assurer la cohérence des échanges avec les workflows d’imagerie existants. Les principes définis par le profil **IHE PAM-FR** sont également pris en compte pour la gestion de l’identité patient, en particulier en ce qui concerne l’identification nationale de santé (INS).

Il est précisé que les flux décrits dans la présente spécification portent principalement sur des **données structurées nécessaires à l’orchestration du workflow**.
 La transmission de la **demande d’examen formalisée sous forme de document clinique**, ainsi que celle d’éventuels **documents cliniques complémentaires**, n’est pas assurée par ces flux transactionnels et fait l’objet de **flux documentaires distincts**, venant les compléter.

Cette articulation permet de maintenir une séparation claire entre :

* les **échanges transactionnels HL7 v2** dédiés au pilotage du workflow de téléradiologie ;
* et les **échanges documentaires CDA**, garantissant la conformité aux référentiels nationaux et la cohérence globale des échanges.

### Profils de message

La présente partie décrit les **profils de messages HL7 v2** retenus pour supporter les flux d’échange du volet Téléradiologie.
 Pour chaque flux identifié, le **type de message HL7 v2** associé est précisé, ainsi que la **structure générale des segments** utilisés afin de couvrir les concepts métiers attendus.

Les profils de message définissent :

* le **type de message HL7 v2** et l’événement associé ;
* l’**ordre des segments** ;
* les **segments requis, optionnels ou répétables** ;
* le rôle fonctionnel de chaque segment dans le cadre du flux considéré.

Cette description vise à fournir une **vision structurante des messages échangés**, indépendamment des contraintes fines appliquées à chaque champ ou composant.

#### Description des messages HL7 v2

La description des messages ORU et MDM est basée sur le contenu du document et les métadonnées complémentaires à véhiculer dans le cadre du partage et de l’échange.

Les données utiles pour publication sur le DMP et pour l’envoi par MSSanté de(s) document(s) sont stockées à la fois dans le segment PID du message HL7, dans le document CDA-R2 conforme au [volet du CI_SIS Structuration minimale des documents de santé](https://esante.gouv.fr/volet-structuration-minimale-de-documents-de-sante) et dans des segments OBX du message HL7 spécifiant les métadonnées complémentaires.

Le développeur doit valoriser tous les segments et champs obligatoires des messages HL7v2 afin de répondre au standard d’interopérabilité des messages.

Ci-dessous sont représentées les structures de messages HL7v2 proposées pour la transmission de document(s) CDA-R2 en HL7v2.

##### Message ORM^O01^ORM_O01 en HL7 v2.5.1

###### Profil du message ORU_R01

Le profil du message ORU_R01 est le suivant :

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
  * Usage: RE
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
  * Meaning: Common Order : demande de traitement sur un document
  * Usage: R
  * Card.: [1..1]
  * § HL7: 4
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
  * Meaning: Document et expression des métadonnées de document relatives au masquage du document aux PS et de visibilité au patient.
  * Usage: R
  * Card.: [1..1]
  * § HL7: 7
* Segment:  [{PRT}] (note 1)
  * Meaning: Participation : Expéditeur du document, destinataire(s) MSSanté, adresse mail sur laquelle le destinataire peut répondre. Segment PRT pré-adopté de la version 2.9
  * Usage: R/C
  * Card.: [1..*]
  * § HL7: 7 (v2.9)
* Segment:  [{NTE}]
  * Meaning: Comment of the result
  * Usage: O
  * Card.: [0..*]
  * § HL7: 2
* Segment:  }
  * Meaning: --- OBSERVATION end
  * Usage:  
  * Card.:  
  * § HL7:  

**Note (1) :** **le segment PRT est utilisé uniquement avec l’OBX qui porte la demande de traitement sur le document. Dans ce cas il est requis et conditionnel (sa valeur dépend de la demande exprimée : envoi de la demande de traitement sur le DMP et/ou envoi vers un ou des destinataire(s) via MSSanté).**

Le message ORU peut transmettre une ou deux instances de documents CDA-R2. Le CREATEUR peut ainsi transmettre un document au format CDA-R2 niveau 1 et un deuxième document de contenu clinique identique au format CDA-R2 niveau 3. Chaque document possède son propre identifiant (fonctionnalité non applicable au SEGUR vague 2).

Dans le cadre de ce volet, spécifique à un échange entre un système (CREATEUR) et une PFI (GESTIONNAIRE), l’occurrence ORDER_OBSERVATION est utilisée pour transmettre une demande de traitement sur le(s) document(s) : transmission initiale/remplacement/suppression de document(s). Seuls les segments ORC, OBR et le groupe de segments OBSERVATION de l’occurrence ORDER_OBSERVATION sont à renseigner.

Les contraintes apportées par ce volet sur les données des différents segments du message ORU sont décrites à la [section dédiée](volume2.md#contraintes-appliquées-aux-messages-mdm-et-oru-dans-le-contexte-de-ce-volet).

###### Description fonctionnelle du message ORU

**Figure 17 : Structure fonctionnelle du message ORU_R01**

Les groupes en rouge sur le schéma représentent les éléments spécifiques à ce volet :

* Un premier groupe de segments OBSERVATION contenant le document médical au format CDA-R2 codé en base64 suivi de segments PRT, pré-adoptés depuis la version 2.9 du standard, permettant ainsi de renseigner le cas échéant les informations de l’expéditeur, le(s) destinataire(s) MSSanté et l’adresse mail de réponse.
* Un deuxième groupe OBSERVATION contenant le cas échéant le même document médical spécifié dans un autre format, codé en base64. Le contenu clinique des documents est identique, seul le format est différent. Cette possibilité n’est pas utilisée dans le contexte du SEGUR vague2 (la version PDF du compte-rendu est insérée dans une section dédiée du document CDA Niv3).

Les groupes de segments OBSERVATION suivants (répétables) véhiculent les métadonnées spécifiques à la publication sur le DMP et/ou à l’envoi par la MSSanté. Ces métadonnées sont communes aux deux formats du document. Ces métadonnées sont décrites dans la [section dédiée](volume2.md#contraintes-appliqu%C3%A9es-aux-messages-mdm-et-oru-dans-le-contexte-de-ce-volet).

#### Réponses et acquittements

Pour l’ensemble des flux décrits ci-dessus :

* Les messages HL7 font l’objet d’un **acquittement technique HL7 v2** (`ACK`) ;
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
  * Contenu: Date/time du message
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
* Champ: PID-18 (*Note 1*)
  * Contenu: N° de dossier administratif
  * Type donnée: CX
  * Caractère optionnel/obligatoire: RE

Le PID-3 doit être identique aux identifiants de patient portés par le document CDA (recordTarget/patientRole/id).

Pour le segment PV1, ce volet ajoute les contraintes suivantes :

* Champ: PV1-2
  * Contenu: Classe du patient 
  * Type donnée: IS
  * Caractère optionnel/obligatoire: R
* Champ: PV1-19 *(Note 1*) et (*Note 2*)
  * Contenu: Identifiant de la venue
  * Type donnée: CX
  * Caractère optionnel/obligatoire:  C (Note 2)
* Champ: PV1-44 (*Note 1*)
  * Contenu: Date d'entrée du patient
  * Type donnée: TS
  * Caractère optionnel/obligatoire: RE
* Champ: PV1-45(*Note 1*)
  * Contenu: Date de sortie du patient
  * Type donnée: TS
  * Caractère optionnel/obligatoire: RE

**Note 1** : **A noter que ces champs sont à renseigner, s’ils sont connus, par l’acteur CREATEUR afin de pouvoir calculer des indicateurs.**

**Note 2** : **Le champ PV1-19 est requis lorsque le PV1-2 prend la valeur E, I, O ou R. Si PV1-2 prend la valeur N alors PV1-19 est requis si connu.**

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

Les **groupes OBSERVATION** (segments OBX), non contraints et optionnels dans le cadre du profil IHE SWF, sont **explicitement contraints par le volet téléradiologie**. Ces contraintes permettent notamment de structurer et de normaliser la transmission d’informations complémentaires nécessaires à la réalisation et à l’interprétation de l’examen d’imagerie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer les informations relatives à la **demande d’examen d’imagerie**. Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie.

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
  * ?: Identifiant de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-9
  * ?: Date/Time of Transaction
  * ?: Date à laquelle la demande d'examen a été réalisée
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-11 (Requis si connu)
  * ?: Verified By
  * ?: Informations relatives au professionel de santé effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-12
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé responsable de la structure d’imagerie qui accueille le patient et supervise la réalisation de l’acte d’imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-14 (Requis si connu)
  * ?: Call Back Phone Number
  * ?: Numéro de téléphone à appeler pour obtenir des précisions sur la demande d'examen d'imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-17
  * ?: Entering Organization
  * ?: Informations relatives à la structure d'imagerie d'accueil du patient

##### Segment OBR (Observation Request)

Le segment **OBR** est utilisé pour véhiculer des informations relatives à la **demande d’examen d’imagerie**.
 Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Ce segment permet notamment de préciser :

* la **modalité d’imagerie demandée** (champ OBR-4),
* les **antécédents pertinents du patient pour l’examen** (champ OBR-13),
* ainsi que les **références à la demande** d’origine, par répétition des informations portées dans le segment ORC, notamment au niveau des champs **OBR-2** et **OBR-16**.

Les champs présentés dans le tableau ci-après sont **requis** ou **requis si connus**, selon leur pertinence dans le cadre du workflow de téléradiologie.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-1)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code de la modalité d'imagerie
  * ?: Utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Libellé
  * ?: 
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Système de codage dont est issu le code
  * ?:  DCM
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-13 (Requis si connu)
  * ?: Relevant Clinical Information
  * ?: Antécédents du patient pertinent dans le cadre de l'examen demandé
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé responsable (identique à l'ORC-12)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-31
  * ?: Reason for Study
  * ?: JustificationDemande

##### Groupes OBSERVATION - Localisation anatomique

Ces groupes **OBSERVATION** sont utilisés afin de véhiculer les informations relatives à la **localisation anatomique concernée par la demande d’examen d’imagerie**. Ces informations permettent de préciser la zone anatomique à explorer et, le cas échéant, d’apporter un niveau de détail complémentaire facilitant l’interprétation et la réalisation de l’examen.

La localisation anatomique est portée par un **premier segment OBX obligatoire**, pouvant être complété par un **second segment OBX optionnel** destiné à préciser la topographie de manière plus fine. Les segments OBX portant sur la localisation anatomique sont identifiés par un code local “LOCALISATION_ANATOMIQUE” dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

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
  * ?: Libellé 
  * ?: Localisation anatomique examinée dans le cadre de l’examen d’imagerie
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?:  
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.1
  * ?: Code 
  * ?: Valeur issue du JDV [JDV_RegionAnatomique-CISIS](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-region-anatomique-cisis.html)
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-5.3
  * ?: Name Of Coding System
  * ?: DCM
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
  * ?: CE(Coded Entry)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-3
  * ?: Observation Identifier
  * ?: ** **
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.1 
  * ?: Code 
  * ?: LOCALISATION_ANATOMIQUE
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.2 
  * ?: Libellé 
  * ?: Localisation anatomique examinée dans le cadre de l’examen d’imagerie
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
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

##### Groupe OBSERVATION - Taille corporel

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
  * ?: Libellé 
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
  * ?: Libellé 
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
  * ?: Libellé 
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
 Un **motif d’annulation** peut être véhiculé lorsque cette information est disponible ; son renseignement est **optionnel**.

* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: **Segment ORC**
  * ?: **Common Order**
  * ?:  
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-1
  * ?: Order control
  * ?: Valeur fixée à « CA (Canceled)
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
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-14 (Requis si connu de l'expéditeur)
  * ?: Call Back Phone Number
  * ?: Numéro de téléphone à appeler pour obtenir des précisions sur la demande d'examen d'imagerieCe champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-16 (Optionnel)
  * ?: Order Control Code Reason
  * ?: Code du motif d'annulation de la demande d'examen
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-17
  * ?: Entering Organization
  * ?: Informations relatives à la structure d'imagerie d'accueil du patient

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
  * ?: Identifiant de la demande d'examen (identique à l'ORC-1)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code de la modalité d'imagerie
  * ?: Utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Libellé
  * ?: 
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Système de codage dont est issu le code
  * ?:  DCM
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé responsable (identique à l'ORC-12)

##### Flux 3 - Réponse à la demande d’examen d’imagerie

Ce flux repose sur l’utilisation de messages **ORU^R01**, conformes au standard **HL7 v2.5.1**.

Contrairement aux **flux 1, 2 et 4**, ce flux **ne s’appuie sur aucun profil IHE du domaine Radiology**, aucun cas d’usage équivalent n’étant actuellement couvert par les profils IHE dans ce contexte.
 Les segments ci-dessous sont définis sur la base du standard HL7 v2.5.1, complété par une **surcouche de contraintes spécifiques à la téléradiologie**, décrite dans les sections suivantes.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer la **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie.

Le champ **ORC-1 – Order Control** permet d’indiquer la décision prise sur la demande, à savoir sa **validation** ou son **refus**. En cas de refus, un **motif de refus** peut être transmis lorsque cette information est disponible ; son renseignement est **optionnel**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus** ou **optionnel**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie..

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
  * ?: Identifiant de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-12
  * ?: Ordering Provider
  * ?: Informations relatives au Médecin effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-16 (Optionnel)
  * ?: Order Control Code Reason
  * ?: Code du motif de refus de la demande d'examen
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-17
  * ?: Entering Organization
  * ?: Informations relatives à la plateforme de Téléradiologie

##### Segment OBR (Observation Request)

Le segment **OBR** est utilisé pour véhiculer des informations relatives à la **réponse à la demande d’examen d’imagerie**.
 Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-1)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code de la modalité d'imagerie
  * ?: Utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Libellé
  * ?: 
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Système de codage dont est issu le code
  * ?:  DCM
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-16
  * ?: Ordering Provider
  * ?: Informations relatives au professionnel de santé effecteur à distance (identique à l'ORC-12)

##### Groupe OBSERVATION - Protocole d’imagerie

Le **groupe OBSERVATION** est requis afin de véhiculer le **protocole d’imagerie** associé à l’examen.
 Le protocole d’imagerie est porté par un **segment OBX unique** au sein du groupe OBSERVATION. Deux alternatives d’encodage sont proposées, en fonction du niveau de structuration et du contenu du protocole à transmettre :

* **Protocole en clair** : transmission du protocole sous forme de texte lisible directement dans le message HL7, à l’aide du type de données **FT (Formatted Text)**.
* **Protocole encapsulé** : transmission du protocole sous forme de document encapsulé (par exemple PDF, XML ou texte structuré), encodé en **base64** et véhiculé à l’aide du type de données **ED (Encapsulated Data)**.

Ces deux alternatives sont exclusives : un seul segment OBX est utilisé pour porter le protocole d’imagerie, avec le type de données adapté au mode de transmission retenu. Le choix de l’alternative relève des capacités des systèmes émetteurs et récepteurs et doit être cohérent avec les besoins métier du flux. Le segment OBX portant sur le protocole est identifié par un code local “PROTOCOLE_IMAGERIE” dans **OBX-3**, documenté en annexe.

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
  * ?: Libellé 
  * ?: Protocole d'imagerie médicale
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?: Protocole d'imagerie

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
  * ?: Libellé 
  * ?: Protocole d'imagerie médicale
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
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

Le segment **ORC** est utilisé pour véhiculer les informations relatives l’ordre d’origine et d’assurer la traçabilité des informations transmises. Il est renseigné conformément aux spécifications du profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
  * ?: Identifiant de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-3
  * ?: Filler Order Number
  * ?: Identifiant de la demande d'examen d'imagerie
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-5
  * ?: Order Status
  * ?: Valeur fixée à « SC (Scheduled)
* Composition du segment ORC : Usage = Required / Cardinalité = [1..1]: ORC-9
  * ?: Date/Time of Transaction
  * ?: Date à laquelle la demande d'examen a été réalisée

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

Le segment **OBR – Observation Request** est utilisé pour véhiculer les informations de contexte relatives à l’**examen d’imagerie ayant été réalisé**. Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: Elément requis
  * ?: Description
  * ?: Valeur
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: **Segment OBR**
  * ?: **Observation Request**
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-2
  * ?: Placer Order Number
  * ?: Identifiant de la demande d'examen (identique à l'ORC-1)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: OBR-4
  * ?: Universal Service Identifier
  * ?:  
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.1
  * ?: Code LOINC de l’acte d’imagerie
  * ?: Utiliser le [JDV_CodeDocumentImagerieCisis-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-code-document-imagerie-cisis.html)
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.2
  * ?: Libellé
* Composition du segment OBR : Usage = Required / Cardinalité = [1..1]: >OBR-4.3
  * ?: Système de codage dont est issu le code
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
  * ?: Code de la modalité d'imagerie
  * ?: Utiliser le [JDV_modalitedemandeActeImagerie-CISIS ](https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html)
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: >IPC-5.2
  * ?: Libellé
  * ?: 
* Composition du segment IPC : Usage = Required / Cardinalité = [1..1]: >IPC-5.3
  * ?: Système de codage dont est issu le code
  * ?:  DCM

##### Groupe OBSERVATION - URL de viewer DRIMbox

Ce **groupe OBSERVATION** est utilisé afin de véhiculer l’**URL d’accès à la vieweuse DRIMbox**, permettant la consultation à distance des images issues de l’examen d’imagerie.

L’URL de la vieweuse est portée par un **segment OBX unique** au sein du groupe OBSERVATION. Elle est transmise sous forme de texte. La valeur portée dans **OBX-5** correspond à une URL complète, pouvant inclure des paramètres de requête nécessaires à l’accès sécurisé à la vieweuse. Les caractères spéciaux éventuellement présents dans l’URL sont encodés conformément aux règles d’échappement HL7 v2.5.1, afin d’assurer l’intégrité de l’information transmise. Le segment OBX portant sur le protocole est identifié par un code local “URL_VIEWER_DRIMBOX” dans **OBX-3**, documenté en annexe.

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
  * ?: Libellé 
  * ?: URL de la visionneuse DRIMbox
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-5
  * ?: Observation Value
  * ?: URL du viewer DRIMbox
* Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Groupes OBSERVATION - Localisation anatomique

Les groupes **OBSERVATION – Localisation anatomique** sont **optionnel** dans le cadre du flux 4.
 Leur présence permet de transmettre les informations relatives à la localisation anatomique concernée par l’examen réalisé, ainsi que, le cas échéant, une précision topographique associée. La structure, le contenu et les contraintes applicables à ces groupes OBSERVATION sont **strictement identiques** à ceux définis pour le flux 1.
 Pour le détail des segments OBX, se référer à la section dédiée du flux 1 : [Groupes OBSERVATION – Localisation anatomique](./st_flux1.md#Groupes-OBSERVATION---Localisation-anatomique)

##### Groupes OBSERVATION - Produit administré

Les groupes **OBSERVATION – Produit administré** sont **optionnels** et permettent de transmettre les informations relatives aux produits administrés lors d’un examen d’imagerie.

Chaque information du produit est portée dans **un groupe OBSERVATION** et un segment OBX distincts.
 Les groupes sont répétables pour permettre la transmission de plusieurs produits administrés au cours du même examen.
 Pour assurer la cohérence des informations :

* le **type de produit** et le **numéro de lot** sont **indissociables**,
* la **quantité administrée** est facultative mais recommandée lorsque le produit est renseigné.

Les segments OBX portant sur le produit administré sont identifiés par un code local “PRODUIT_ADMINISTRE” dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION – Type de produit

Ce groupe OBSERVATION permet de transmettre le **type de produit administré**. La valeur est codée à partir du **Jeu de Valeurs ATC niveau 2**, limité aux classes :

* **V09** – Produits de diagnostic
* **V10** – Produits thérapeutiques

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
  * ?: Libellé 
  * ?: Produit administré lors de l'examen d'imagerie
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
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
  * ?: Libellé 
  * ?: Produit administré lors de l'examen d'imagerie
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Numéro de lot du radiopharmaceutique adminsitré
* Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Groupe OBSERVATION – Quantité de produit administré

Ce groupe OBSERVATION permet de transmettre la **quantité réellement administrée** du produit. Le segment OBX unique au sein de ce groupe porte la valeur dans **OBX-5** et l’unité de mesure dans **OBX-6** (par exemple millilitres ou milligrammes).
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
  * ?: Libellé 
  * ?: Produit administré lors de l'examen d'imagerie
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
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

Les groupes **OBSERVATION – Appareil d’imagerie utilisé** sont **optionnels**. Lorsqu’ils sont présents, ils permettent de transmettre les informations relatives à l’**appareil d’imagerie ayant été utilisé pour la réalisation de l’examen**, en particulier dans le cas des techniques irradiantes. Les informations relatives à l’appareil sont portées dans **deux groupes OBSERVATION distincts** :

* un groupe dédié à l’**identifiant unique de l’appareil d’imagerie**,
* un groupe dédié au **modèle de l’appareil d’imagerie**.

Ces groupes peuvent être utilisés conjointement ou indépendamment, selon le niveau d’information disponible, l’identifiant de l’appareil constituant l’information principale de référence. Les segments OBX portant sur le produit administré sont identifiés par un code local “APPAREIL_IMAGERIE” dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION – Identifiant de l’appareil d’imagerie

Ce groupe OBSERVATION permet de transmettre l’**identifiant unique de l’appareil d’imagerie utilisé** lors de l’examen. L’identifiant correspond au **Support IUD**, tel que communiqué via un dispositif d’identification automatique (AIDC) ou, le cas échéant, via son marquage en clair. Le groupe contient un **segment OBX unique** portant la valeur de l’identifiant dans **OBX-5**.

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
  * ?: Libellé 
  * ?: Appareil d'imagerie utilisé lors de l'examen
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Identifiant de l'appareil d'imagerie : SupportIUD voir SFE 2.1.7.4.3
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

###### Groupe OBSERVATION – Modèle de l’appareil d’imagerie

Ce groupe OBSERVATION permet de transmettre le **modèle de l’appareil d’imagerie utilisé**. La valeur est exprimée sous forme de texte libre et correspond à la dénomination du modèle fournie par le constructeur. Le groupe contient un **segment OBX unique** portant le modèle de l’appareil dans **OBX-5**.
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
  * ?: Libellé 
  * ?: Appareil d'imagerie utilisé lors de l'examen
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: > OBX-3.3 
  * ?: Name of Coding system
  * ?: TLRMETADATA
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-4
  * ?: Observation Sub-ID
  * ?: **Voir règle commune d’utilisation du Sub-ID : **[Utilisation du champ OBX-4 ](specifications_techniques.md#utilisation-du-champ-obx-4--observation-sub-id)
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-5
  * ?: Observation Value
  * ?: Modèle de l’appareil d’imagerie utilisé
* Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]: OBX-11
  * ?: Observation Result Status
  * ?: Valeur fixée à « F » 

##### Utilisation du champ OBX-4 – Observation Sub-ID

Dans le cadre de la présente spécification, le champ **OBX-4 – Observation Sub-ID** est utilisé pour assurer le **regroupement logique et la différenciation** de plusieurs segments **OBX** se rapportant à un même concept métier.

Cette règle s’applique notamment aux cas suivants (liste non exhaustive) :

* produits administrés,
* appareil d’imagerie utilisé,
* localisation anatomique et précision topographique,

###### Principe général

Lorsque plusieurs segments **OBX** sont utilisés pour décrire une même entité métier, ces segments :

* partagent le **même OBX-3 – Observation Identifier**,
* sont différenciés et associés à l’aide du champ **OBX-4 – Observation Sub-ID**.

Le Sub-ID est structuré sous la forme **n.m**, où :

* **n** correspond à l’identifiant d’une occurrence d’un même concept métier (par exemple un produit administré ou un appareil d’imagerie),
* **m** identifie la nature de l’information portée par le segment OBX au sein de cette occurrence.

Cette structuration permet :

* de regrouper explicitement les segments OBX décrivant une même entité,
* de gérer plusieurs occurrences d’un même concept dans un message,
* de conserver une structure lisible et interopérable.

###### Contraintes d’utilisation

* Tous les segments OBX partageant un même **OBX-3** et un même **n** dans **OBX-4** sont considérés comme décrivant une **même occurrence métier**.
* Les valeurs possibles de **m** et leur signification sont définies dans les sections spécifiques à chaque flux.
* L’utilisation du champ **OBX-4** est **obligatoire** dès lors que plusieurs segments OBX partagent le même **OBX-3** dans un message.

###### Exemple d’utilisation – Produit administré

Dans l’exemple ci-dessous, deux produits administrés sont transmis dans un message.
 Chaque produit est décrit à l’aide de trois segments OBX : type de produit, numéro de lot et quantité administrée.

```
OBX|1|CE|PRODUIT_ADMINISTRE^Produit administré|1.1|V09^Produits de diagnostic^ATC||||
OBX|2|TX|PRODUIT_ADMINISTRE^Produit administré|1.2|LOT123456||||
OBX|3|NM|PRODUIT_ADMINISTRE^Produit administré|1.3|120|mL|||
OBX|4|CE|PRODUIT_ADMINISTRE^Produit administré|2.1|V10^Produits thérapeutiques^ATC||||
OBX|5|TX|PRODUIT_ADMINISTRE^Produit administré|2.2|LOT789012||||
OBX|6|NM|PRODUIT_ADMINISTRE^Produit administré|2.3|80|mL|||

```

