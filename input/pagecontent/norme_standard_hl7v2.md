#### Standard HL7 version 2 (HL7 v2)

##### Présentation

[HL7 version 2 (HL7 v2)](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=185) est un standard de messagerie développé par l'organisation Health Level Seven International, destiné à l'échange d'informations entre systèmes d'information de santé. Il repose sur l'échange de messages structurés, composés de segments, de champs et de sous-composants, organisés selon des déclencheurs événementiels (triggers). Le standard définit la structure logique des messages ainsi que les règles de codage associées, sans imposer de modèle d'information unique. Cette approche confère à HL7 v2 une grande souplesse d'implémentation et explique en partie son adoption massive dans l'écosystème des systèmes d'information de santé.

Il est important de souligner que HL7 v2 ne prescrit pas le protocole de transport ni l'architecture des échanges. Le standard n'émet aucune hypothèse sur :

- la conception ou l'architecture des systèmes émetteurs et récepteurs
- le mode de communication sous-jacent (synchrone ou asynchrone)
- les mécanismes de transport, de sécurisation ou de routage des messages

Ainsi, le choix du protocole de transport est laissé à l'initiative des implémenteurs. Néanmoins, dans les usages historiques et recommandés, HL7 v2 est fréquemment associé au protocole MLLP (Minimal Lower Layer Protocol), qui permet l'échange de messages sur des connexions persistantes et facilite la gestion des accusés de réception techniques. Ces accusés de réception (ACK), permettent au système récepteur de notifier l'émetteur de la bonne réception et du traitement du message transmis. Les ACK peuvent être de nature :

- technique, attestant de la bonne réception et de la conformité syntaxique du message
- applicative, indiquant l'acceptation ou le rejet du message au regard de règles métier ou fonctionnelles.

L'intérêt de ces mécanismes d'accusés de réception réside dans la fiabilité des échanges et dans la maîtrise du cycle de vie des messages.

##### Maturité et adoption

HL7 v2 est un standard hautement mature, initialement publié à la fin des années 1980 et ayant fait l’objet de nombreuses évolutions successives au travers de plusieurs versions majeures, témoignant de sa stabilité, de sa robustesse. Dans l’écosystème français, il est solidement ancré dans le contexte intra-hospitalier au sein pratiques des systèmes d’information de santé, en particulier dans le domaine de l’imagerie médicale. Ce constat repose à la fois sur son usage historique largement répandu et sur les travaux menés dans le cadre du volet Téléradiologie, notamment au travers d’ateliers associant éditeurs de RIS et plateformes de téléradiologie. Ces échanges ont permis de confronter les besoins opérationnels aux capacités des standards existants et ont confirmé le niveau de maturité et d’industrialisation de HL7 v2 pour ce type de cas d’usage.
Par ailleurs, le [Livre blanc Téléradiologie](https://industriels.esante.gouv.fr/sites/default/files/media/document/Livre-Blanc-TLR_vFinale.pdf) élaboré par l’Agence du Numérique en Santé en collaboration avec l’écosystème éditeur s’appuie sur des flux fondés sur le standard HL7 v2, renforçant ainsi ce constat. 

De plus, le CI-SIS incite à l'utilisation du standard HL7v2 pour le transport des documents CDA en intra-hospitalier notamment en se conformant aux volets de référence suivants :

- [Transport d'un document CDA en HL7v2](https://esante.gouv.fr/volet-transport-dun-document-cda-r2-en-hl7-oru-oul-mdm)
- [Transmission au LPS d'un document CDA provenant d'un courriel MSSanté](https://esante.gouv.fr/volet-de-transmission-au-lps-dun-document-cda)

L'ancrage d'HL7 v2 au niveau français est également la conséquence des travaux de l’organisme InteropSanté, qui publie et maintient des spécifications nationales fondées sur HL7 v2, telles que [les contraintes françaises du profil IHE PAM](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf), [les contraintes françaises sur les types de données HL7 v2](https://www.interopsante.org/f/db43469b624f3039f9610d8cb6b27830ed6a9fe1/IHE_France_Constraints_on_HL7_data_types_for_ITI_V1.8.2.pdf), ainsi que les profils [ILW.FR](https://www.interopsante.org/f/794889b493c4434447de15737a285529b2967ca7/IHE_ILW_FR_Vol1_1.4.pdf) et [LTW.FR](https://www.interopsante.org/f/8e4f8de143d65c6fd3f5f2c372729f2c3ff636fd/IHE_LTW_FR_Vol1_1.4_TI.pdf) encadrant les échanges de demandes et de résultats d’examens de biologie, en contexte intra-établissement et inter-organisations. 

Ces spécifications contribuent à une mise en œuvre homogène, interopérable et industrialisée du standard HL7 v2 au niveau national.

##### Outillage

L'écosystème HL7 v2 bénéficie d'un outillage industriel éprouvé, largement diffusé auprès des acteurs du secteur :

- Moteurs d'interfaces HL7 (Mirth Connect, Rhapsody, Cloverleaf, etc.), permettant la transformation, le routage et la supervision des flux
- Bibibliothèques logicielles dans la plupart des langages de développement courants (Java, .NET, Python, JavaScript…), telles que [HAPI HL7](https://github.com/hapifhir/hapi-hl7v2), [NHapi](https://github.com/nHapiNET/nHapi) ou [hl7apy](https://crs4.github.io/hl7apy/), facilitant la génération, le parsing, la validation et le transport des messages HL7 v2 au sein des systèmes d’information
- [Suite d'outil open source du NIST](https://hl7v2-igamt-2.nist.gov/home) permettant de créer et maintenir des guides d'implémentation HL7v2. Elle permet également de tester la conformité d'un message par rapport au guide généré
- [Les plateformes Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) (ANS et IHE) sont également utilisées pour tester les profils de message. L'outil GazelleHL7Validator intègre les fichiers de définitions. Accessible via le service de Validation EVS Client, il permet de vérifier si :
  - Le message est bien structuré
  - Le message respecte les règles spécifiées dans les fichiers de définition

Cet outillage contribue à une mise en œuvre maîtrisée et sécurisée des échanges HL7 v2, y compris dans des environnements hétérogènes ou multi-éditeurs.

##### HL7v2 adapté au cas d'usage Téléradiologie

Le standard HL7 v2 est d'ores et déjà présent au sein du workflow global de la téléradiologie par l'intermédiaire du [volet de transmission d'un document CDA-R2 en HL7v2](https://interop.esante.gouv.fr/ig/hl7v2/trans-cda-r2/index.html), utilisé pour la transmission du compte-rendu d'imagerie depuis la plateforme de téléradiologie vers le RIS de la structure d'imagerie. Par ailleurs, le volet téléradiologie envisage également la transmission, en complément des éléments structurés de la demande d'examen, de documents associés tels que la demande d'examen formalisée ou tout document complémentaire permettant d'enrichir le contexte clinique. Ces flux complémentaires reposent également sur le volet de Transport de documents CDA en HL7 v2, renforçant ainsi la cohérence globale des échanges autour de ce standard.

Au-delà de ces usages existants, plusieurs profils IHE du [domaine IHE RADIOLOGY](https://www.ihe.net/ihe_domains/radiology/) s'appuient historiquement sur HL7 v2 pour structurer les échanges liés aux workflows d'imagerie. Le profil [IHE Scheduled Workflow (SWF.b)](https://www.ihe.net/uploadedFiles/Documents/Radiology/IHE_RAD_Suppl_SWF.b_Rev1-7_2019-08-09.pdf) définit notamment les transactions permettant d'orchestrer le cycle de vie d'un acte d'imagerie, depuis la prescription jusqu'à la production des résultats. Bien que le profil SWF.b ne couvre pas l'intégralité des cas d'usage spécifiques à la téléradiologie, en particulier les étapes de validation médicale distante ou de protocolisation, il propose néanmoins un ensemble de briques fonctionnelles pertinentes, telles que la gestion des demandes d'examen, des statuts associés ou des identifiants d'actes. Ces briques peuvent être mobilisées et adaptées dans le cadre des flux de téléradiologie, sans nécessiter l'adoption exhaustive du profil IHE.

De même, le profil [IHE PAM-FR](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf) (Patient Administration Management France), bien qu'orienté vers la gestion administrative des patients et non vers les processus métiers propres à la téléradiologie, constitue une référence nationale pour la gestion de l'identité patient et des traits d'identification, notamment autour de l'INS. Les segments et champs HL7 v2 définis par ce profil peuvent ainsi être réutilisés pour garantir une gestion cohérente et conforme de l'identité du patient dans les flux de téléradiologie, indépendamment des messages métiers échangés.

Dans cette perspective, l'analyse présentée ci-après vise à démontrer la capacité du standard HL7 v2 à couvrir les concepts métiers identifiés dans les spécifications fonctionnelles du volet Téléradiologie. Les tableaux de couverture proposés s'appuient à la fois sur les usages courants d'HL7 v2 et sur les briques définies dans les profils IHE SWF.b et PAM-FR, afin d'illustrer de manière concrète et opérationnelle la couverture fonctionnelle du standard pour chacun des flux identifiés.

###### Flux 1 - Transmission de la demande d'examen d'imagerie

Dans le cadre du flux de transmission de la demande d'examen d'imagerie, les concepts métiers identifiés dans les spécifications fonctionnelles peuvent être portés par un message HL7 v2 de type ORM, historiquement utilisé pour la prescription et la gestion des actes d'imagerie. Les mappings présentés ci-dessous s'appuient sur les usages courants d'HL7 v2, ainsi que sur les recommandations issues des profils IHE SWF.b et PAM-FR lorsque celles-ci sont pertinentes, notamment pour la gestion de l'identité patient et des acteurs impliqués.

| **Concept métier** | **Message HL7v2** | **Segment** | **Champ(s) HL7 v2** |
| --- | --- | --- | --- |
| **StructureImagerie** | ORM^O01 | MSH - Message Header / ORC - Common Order| MSH-3 Sending Application, MSH-4 Sending Facility / <br>ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **PlateformeTeleradiologie** | ORM^O01 | MSH - Message Header/ ORC - Common Order| MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | ORM^O01 | PID - Patient Identification ||
| **PSResponsable** | ORM^O01 | ORC - Common Order| ORC-10 Entered By, ORC-12 Ordering Provider |
| **PSEffecteur** | ORM^O01 | ORC - Common Order / OBR - Observation Request| ORC-11 Verified By / ORC-32 Principal Result Interpreter |
| **roleProfessionnel** | ORM^O01 | ORC - Common Order / OBR - Observation Request| ORC-10 Entered By / ORC-11 Verified By / ORC-12 Ordering Provider / ORC-32 Principal Result Interpreter |
| **IdentifiantDemandeExamen** | ORM^O01 | ORC - Common Order| ORC-2 Placer Order Number|
| **NatureDemande** | ORM^O01 | ORC - Common Order| ORC-1 Order Control|
| **DateDemande** | ORM^O01 | ORC - Common Order| ORC-9 Date/Time of Transaction |
| **IdentifiantRDV** | ORM^O01 | PV1 - Patient Visit| PV1-19 Visit Number |
| **DateHeurePriseCharge** | ORM^O01 | PV1 - Patient Visit| PV1-44 Admit Date/Time |
| **JustificationDemande** | ORM^O01 | ORC - Common Order / NTE - Notes and Comments| ORC-31 Reason for Study, NTE-3 Comment |
| **LocalisationAnatomique** | ORM^O01 | OBX - Observation/Result| OBX-2 = CE / TX, OBX-5 |
| **ModaliteImagerie** | ORM^O01 | OBX - Observation/Result| OBX-2 = CE / TX, OBX-5 |
| **Antecedents** | ORM^O01 | OBR - Observation Request| ORC-31 Relevant Clinical Information |

<p style="text-align:center;">Table 3 : Couverture des concepts métier du flux 1 par le standard HL7v2</p>

###### Flux 2 - Annulation de la demande d'examen d'imagerie

Le flux d'annulation de la demande d'examen d'imagerie vise à notifier la plateforme de téléradiologie de l'invalidation d'une demande précédemment transmise. HL7 v2 prévoit nativement ce cas d'usage au travers du profil de message ORM^O01. Le segment ORC (Common Order) et plus particulièrement son champ ORC-1 Order Control- Order Control, permet de gérer le cycle de vie des ordres, incluant leur création, modification et annulation. Ce mécanisme, largement utilisé dans les workflows d'imagerie décrits par le profil IHE SWF.b, garantit une gestion cohérente et tracée des annulations sans introduire de nouveaux messages spécifiques.

| **Concept métier** | **Message HL7v2** | **Segment** | **Champ(s) HL7 v2** |
| --- | --- | --- | --- |
| **StructureImagerie** | ORM^O01 | MSH - Message Header / ORC - Common Order| MSH-3 Sending Application, MSH-4 Sending Facility / <br>ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **PlateformeTeleradiologie** | ORM^O01 | MSH - Message Header | MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | ORM^O01 | PID - Patient Identification ||
| **PSEffecteur** | ORM^O01 | ORC - Common Order | ORC-11 Verified By / ORC-32 Principal Result Interpreter |
| **roleProfessionnel** | ORM^O01 | ORC - Common Order| ORC-10 Entered By / ORC-11 Verified By / ORC-12 Ordering Provider / ORC-32 Principal Result Interpreter |
| **IdentifiantDemandeExamen** | ORM^O01 | ORC - Common Order| ORC-2 Placer Order Number|
| **NatureDemande** | ORM^O01 | ORC - Common Order| ORC-1 Order Control|
| **MotifAnnulation** | ORM^O01 | ORC - Common Order / NTE - Notes and Comments| ORC-16 Order Control Code Reason, NTE-3 Comment |

<p style="text-align:center;">Table 4 : couverture des concepts métier du flux 2 par le standard HL7v2</p>

###### Flux 3 - Réponse à la demande d'examen d'imagerie

Le flux de réponse à la demande d'examen d'imagerie correspond à la décision rendue par le médecin effecteur distant à l'issue de l'analyse de la demande initiale. Cette réponse peut se traduire par une acceptation de la demande, accompagnée d'un protocole d'imagerie, ou par un refus, éventuellement assorti d'un motif explicatif. HL7 v2 ne définit pas de message spécifique dédié à la notion de « réponse à une demande » dans un contexte de téléradiologie. En revanche, le standard propose plusieurs mécanismes permettant de porter cette information, notamment via des profils de message comme ORM^O01 ou ORU^R01 qui assurent la gestion des statuts d'ordre (segment ORC) et l'ajout d'informations cliniques ou opérationnelles dans les segments OBR, OBX ou NTE. Ces mécanismes sont historiquement mobilisés dans les workflows d'imagerie décrits par le profil IHE SWF.b.

| **Concept métier** | **Message HL7v2** | **Segment** | **Champ(s) HL7 v2** |
| --- | --- | --- | --- |
| **PlateformeTeleradiologie** | ORM^O01 / ORU^R01 | MSH - Message Header / ORC - Common Order| MSH-3 Sending Application, MSH-4 Sending Facility / <br>ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **StructureImagerie** | ORM^O01 / ORU^R01 | MSH - Message Header / ORC - Common Order| MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | ORM^O01 / ORU^R01 | PID - Patient Identification ||
| **PSEffecteur** | ORM^O01 / ORU^R01 | ORC - Common Order| ORC-10 Entered By, ORC-12 Ordering Provider |
| **roleProfessionnel** | ORM^O01 / ORU^R01 | ORC - Common Order / OBR - Observation Request| ORC-10 Entered By / ORC-11 Verified By |
| **IdentifiantDemandeExamen** | ORM^O01 / ORU^R01 | ORC - Common Order| ORC-2 Placer Order Number|
| **DecisionEffecteur** | ORM^O01 / ORU^R01 | ORC - Common Order| ORC-1 Order Control|
| **MotifRefus** | ORM^O01 / ORU^R01 | ORC - Common Order / NTE - Notes and Comments| ORC-16 Order Control Code Reason, NTE-3 Comment |
| **ProtocoleImagerie** | ORM^O01 / ORU^R01 | OBX - Observation/Result| OBX-2 = ED/TX, OBX-5 |

<p style="text-align:center;">Table 5 : couverture des concepts métier du flux 3 par le standard HL7v2</p>

###### Flux 4 - Transmission d'un complément d'information post-acte d'imagerie

Le flux de transmission d'un complément d'information post-acte d'imagerie intervient à l'issue de la réalisation de l'examen. Il vise à transmettre au radiologue effecteur distant des éléments permettant de compléter le contexte d'interprétation et de rédaction du compte-rendu d'imagerie. Dans les implémentations HL7 v2 existantes, ce type de flux est fréquemment pris en charge au moyen de messages ORU^R01, utilisés pour la transmission d’observations et de résultats. Ce message permet de véhiculer une grande variété d’informations via des segments OBX, mais ne dispose pas de segments dédiés pour porter nativement les identifiants DICOM de l’examen. À l’inverse, le message OMI^O23, introduit pour répondre spécifiquement aux besoins du domaine de l’imagerie, propose le segment IPC (Imaging Procedure Control), permettant de structurer explicitement les informations techniques liées à la procédure d’imagerie, notamment l’Accession Number et le StudyInstanceUID. Ainsi, le message OMI^O23 est préconisé pour la couverture de flux.

| **Concept métier** | **Message HL7v2** | **Segment** | **Champ(s) HL7 v2** |
| --- | --- | --- | --- |
| **StructureImagerie** | OMI^O23 | MSH - Message Header / ORC - Common Order| MSH-3 Sending Application, MSH-4 Sending Facility / <br>ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **PlateformeTeleradiologie** | OMI^O23 | MSH - Message Header / ORC - Common Order| MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | OMI^O23 | PID - Patient Identification ||
| **IdentifiantDemandeExamen** | OMI^O23 | ORC - Common Order| ORC-2 Placer Order Number|
| **IdentifiantRDV** | OMI^O23 | PV1 - Patient Visit| PV1-19 Visit Number |
| **AccessionNumber** | OMI^O23 | IPC - Imaging Procedure Control| IPC-2 Requested Procedure ID |
| **StudyInstanceUID** | OMI^O23 | IPC - Imaging Procedure Control| IPC-3 Study Instance UID |
| **DateRéalisationExamen** | OMI^O23 | OBR - Observation Request| OBR-7 Observation Date/Time |
| **LocalisationAnatomique** | OMI^O23 | OBX - Observation/Result| OBX-2 = CE / TX, OBX-5 |
| **ModaliteImagerie** | OMI^O23 | IPC - Imaging Procedure Control| IPC-5 Modality |
| **URLViewerDRIMBOX** | OMI^O23 | OBX - Observation/Result| OBX-2 = ST / ED, OBX-5 |
| **DuréeRétentionImages** | OMI^O23 | OBX - Observation/Result| OBX-2 = NM / TX, OBX-5 |
| **IdentificationMatériel** | OMI^O23 | IPC - Imaging Procedure Control| IPC-5 Modality |
| **ProduitsAdministres** | OMI^O23 | OBX - Observation/Result| OBX-2 = CE / TX, OBX-5 |
| **CodeEvenement (LOINC / CCAM)** | OMI^O23 | OBR - Observation Request| OBR-4 Universal Service Identifier |

<p style="text-align:center;">Table 6 : couverture des concepts métier du flux 4 par le standard HL7v2</p>

##### Synthèse

L'analyse des différents flux du volet Téléradiologie met en évidence la capacité du standard HL7 v2 à couvrir les concepts métiers échangés au sein des flux identifiés dans les spécifications fonctionnelles. Ce standard bénéficie d'un haut niveau de maturité, d'un large outillage industriel et d'une interopérabilité éprouvée dans le domaine de l'imagerie médicale. La capacité d’HL7 v2 à suivre les différentes étapes du traitement d’une demande d’examen et à gérer des accusés de réception contribue à sécuriser et tracer les échanges entre systèmes distants. L'utilisation conjointe de HL7 v2 et du protocole MLLP permet ainsi de répondre efficacement aux exigences de robustesse et de synchronisation attendues pour ce type de flux transactionnels. Par ailleurs, l'analyse montre que les profils IHE, en particulier IHE Scheduled Workflow (SWF.b) et IHE PAM-FR, apportent un cadre de référence pertinent pour l'usage d'HL7 v2 dans le domaine de l'imagerie. Les briques proposées par ces profils peuvent être mobilisées de manière ciblée, notamment pour la gestion du cycle de vie des demandes et pour la prise en compte des exigences nationales relatives à l'identité patient et à l'INS.
