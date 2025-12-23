# Normes et Standards - Volet Téléradiologie v0.1.0

* [**Table of Contents**](toc.md)
* **Normes et Standards**

## Normes et Standards

### Introduction

Le présent document présente l’ensemble des normes et standards susceptibles de répondre à la mise en œuvre des flux identifiés dans le document « Spécifications fonctionnelles des échanges - Téléradiologie ». L’objectif de cette étude est d’identifier, qualifier et comparer les standards pertinents pour supporter les échanges nécessaires au parcours de téléradiologie.

Les normes et standards étudiés au sein de cette étude sont les suivants :

* HL7 Version 2.x (v2)
* DICOM (Digital Imaging and Communications in Medicine)
* Standard HL7 CDA : Clinical Document Architecture
* HL7 FHIR

Les standards seront analysés notamment sur leur capacité en matière de structuration du contenu et, le cas échéant, de modalités de transport. Cette étude s’inscrit également dans un contexte de mise en œuvre opérationnelle contraint. L’un des objectifs structurants du volet Téléradiologie est de permettre le versement, au sein du Dossier Médical Partagé (DMP), des demandes d’actes d’imagerie et des comptes rendus produits dans le cadre de la téléradiologie. À la date de la présente étude, le DMP supporte exclusivement des documents cliniques structurés au format CDA. Par ailleurs, les échéances de mise en œuvre du volet imposent de privilégier des solutions limitant les impacts sur les systèmes existants, en particulier les logiciels de RIS et les plateformes de téléradiologie déjà largement déployés. Ces éléments constituent des critères de choix déterminants, au même titre que la couverture fonctionnelle et technique des standards étudiés, et seront pris en compte dans l’analyse comparative et la conclusion de la présente étude.

Les versions des normes et standards étudiés dans le présent document sont celles disponibles à la date de réalisation de l’étude (décembre 2025).

La section 2 propose un rappel synthétique du contexte du volet Téléradiologie. La section 3 présente individuellement chaque norme ou standard étudié, en détaillant pour chacun :

* Une description générale ;
* Sa maturité et son niveau d’adoption dans les systèmes de santé ;
* L’existence d’outillage ;
* Sa pertinence au regard des cas d’usage identifiés.

Un tableau comparatif est proposé en section 5 afin de faciliter la lecture et la mise en perspective des standards évalués. Une analyse métier et technique croisée est fournie en section 6 pour éclairer les choix de standardisation envisageables.

Cette étude s’appuie sur les recommandations et principes du Cadre d’interopérabilité des systèmes d’information de santé (CI-SIS), qui référence les normes et standards internationaux applicables au développement des volets métiers, et constitue le référentiel de doctrine pour l’interopérabilité du système de santé.

### Présentation synthétique du volet Téléradiologie

Cette étude s’inscrit dans le cadre des besoins d’interopérabilité associés au volet « Téléradiologie ». Ce volet a pour objectif de décrire les échanges nécessaires à la prise en charge d’un patient lorsque l’interprétation radiologique est réalisée à distance, entre une structure d’imagerie (lieu de réalisation de l’acte) et une plateforme de téléradiologie (lieu d’interprétation).

Les échanges d’informations interviennent principalement entre :

* Le RIS de la structure d’accueil du patient
* Le système d’information de la plateforme de téléradiologie

La présente étude couvre les échanges décrits dans la Spécification fonctionnelle des échanges - Téléradiologie, à savoir :

* La transmission d’une demande d’examen d’imagerie
* L’annulation d’une demande d’examen
* La réponse à une demande (acceptation avec protocole d’imagerie ou refus)
* La transmission d’informations complémentaires post-examen

Les concepts métiers à véhiculer dans ces flux sont décrits en étape 4 et 5 de la spécification fonctionnelle et couvrent plusieurs catégories de données essentielles au parcours de téléradiologie :

* Données administratives et d’identification : identités patient et professionnels, identifiants de demandes et d’examens, informations de structure.
* Données cliniques et de prescription : motif d’examen, indications, contexte clinique fourni par le médecin de proximité.
* Données de protocole d’imagerie : éléments nécessaires à la réalisation de l’acte, fournis par le radiologue distant.
* Données techniques et informations post-acte : paramètres de réalisation, incidents, observations du manipulateur.

Le choix final des normes ou standards devra permettre de couvrir l’intégralité des données manipulées dans le cadre de la téléradiologie, ainsi que les scénarios d’échanges entre la structure d’imagerie et le service d’interprétation distant.

### Normes et Standards

Cette section présente les normes et standards susceptibles d’être utilisés pour structurer ou, le cas échéant, transporter les données échangées dans le cadre du volet Téléradiologie. Les concepts métiers pris en compte dans cette étude sont issues de la Spécification fonctionnelle des échanges Téléradiologie.

#### Standard DICOM

##### Présentation

Le standard [DICOM (Digital Imaging and Communications in Medicine)](https://www.dicomstandard.org/) est un standard international dédié à la gestion, au stockage, à la transmission et à la visualisation des images médicales. Il définit à la fois un format de fichier pour les images d’imagerie médicale et un ensemble de services réseau permettant l’échange de ces images et des métadonnées associées entre équipements et systèmes d’information d’imagerie (modalités, PACS, visionneuses). DICOM est nativement orienté vers les besoins des domaines de l’imagerie médicale, notamment la radiologie, la médecine nucléaire, la radiothérapie et l’imagerie interventionnelle. Il constitue le socle technique des échanges d’images et d’informations associées au sein des systèmes d’imagerie.

##### Maturité et adoption

Le standard DICOM bénéficie d’un très haut niveau de maturité et d’une adoption quasi universelle dans le domaine de l’imagerie médicale. Il est implémenté par l’ensemble des constructeurs de modalités, de PACS, de solutions d’archivage et de visualisation d’images médicales. Son adoption massive et son interopérabilité éprouvée en font un standard incontournable pour la gestion des images médicales, tant au niveau national qu’international.

##### Outillage

L’écosystème DICOM est riche et largement industrialisé. Il comprend notamment :

* des modalités d’imagerie conformes DICOM
* des PACS et archives d’imagerie
* des visionneuses DICOM
* des services réseau standardisés (C-STORE, C-FIND, C-MOVE, etc.)

Ces outils sont spécifiquement conçus pour la manipulation d’images médicales et de leurs métadonnées, dans des architectures d’imagerie dédiées.

##### DICOM adapté au cas d’usage Téléradiologie

Dans le cadre du volet Téléradiologie, le standard DICOM joue un rôle essentiel pour la mise à disposition et la consultation des images médicales produites lors de la réalisation de l’acte d’imagerie. Toutefois, ce rôle se situe en dehors du périmètre des flux fonctionnels étudiés dans le présent volet. Le standard DICOM n’est pas conçu pour véhiculer des échanges transactionnels ou décisionnels de type métier, ni pour gérer le cycle de vie des demandes ou des décisions médicales associées. À ce titre, il ne permet pas de répondre aux besoins fonctionnels identifiés dans les spécifications du volet Téléradiologie, en dehors de la fourniture d’un accès aux images. Les mécanismes d’accès aux images (PACS, visionneuses, plateformes d’échange) sont généralement intégrés dans des architectures d’imagerie existantes et peuvent être référencés dans les flux du volet Téléradiologie (par exemple via une URL de visionneuse), sans que DICOM ne constitue le standard d’échange principal pour ces flux.

##### Synthèse

Le standard DICOM est un composant fondamental des systèmes d’imagerie médicale et demeure indispensable pour la gestion, l’archivage et la consultation des images médicales.
 Néanmoins, il n’est pas adapté pour répondre aux flux fonctionnels du volet Téléradiologie tels que définis dans les spécifications, lesquels relèvent principalement d’échanges transactionnels, organisationnels et décisionnels entre systèmes d’information.

#### Standard CDA

##### Présentation

Le standard [HL7 Clinical Document Architecture (CDA)](https://hl7.org/cda/stds/online-navigation/index.html) est un standard de structuration de documents cliniques spécifiant à la fois la structure et la sémantique des informations médicales, en vue de leur échange entre acteurs du système de santé. Il repose sur la syntaxe XML et ne définit pas de mécanisme de transport des documents.

HL7 CDA est certifiée par l’ANSI et la version 2 a été adoptée en tant que norme ISO.

Un document CDA contient deux parties :

* Un entête (header) : contient les informations nécessaires à l’identification et à la gestion du document. Elle fournit des éléments d’authentification du document, le contexte de soin, les participants, etc.
* Le corps (body) : contient les informations médicales véhiculées par le document. Il peut être construit suivant 3 niveaux : 
* Niveau 1 : le corps contient un texte non structuré ou une image
* Niveau 2 : le corps est organisé en sections contenant un bloc narratif
* Niveau 3 : le corps se présente sous la forme d’un ensemble hiérarchisé de sections pouvant contenir des données structurées dans des entrées, en plus d’un bloc narratif.
 

##### Maturité et adoption

Le standard HL7 CDA R2 est très répandu à l’international et largement adopté dans le contexte français. L’Agence du Numérique en Santé (ANS) l’exploite notamment dans 28 des 30 volets de la couche Contenu disponibles sur [l’espace de Publication du CI-SIS](https://esante.gouv.fr/offres-services/ci-sis/espace-publication). Ce standard est également utilisé dans de nombreux profils spécifiés par IHE (profils des domaines IHE PCC, IHE PALM, IHE PHARM, …). Le niveau 3 est un format international de structuration et de transmission des documents médicaux. Il permet notamment une intégration automatique des informations contenues dans le document, dans le logiciel métier concerné. Ce niveau permet non seulement une interopérabilité syntaxique, mais également sémantique.

Afin de capitaliser l’expérience acquise et de favoriser la réutilisation des développements, la [doctrine du CI-SIS](https://esante.gouv.fr/sites/default/files/media_entity/documents/CI-SIS_DOCTRINE_20210803_V1.1.pdf) incite à l’utilisation du standard CDA R2 niveau 3 pour structurer les documents, notamment en se conformant aux volets de référence suivants :

* [Structuration minimale de documents de santé](https://esante.gouv.fr/volet-structuration-minimale-de-documents-de-sante), qui définit la structure des données de l’entête d’un document CDA
* [Modèles de contenus CDA](https://esante.gouv.fr/volet-de-reference-modeles-de-contenus-cda), qui définit la structure des données du corps du document.

##### Outillage

Un document CDA peut être testé contre un schéma XSD via un éditeur de texte tel que Notepad++. Ce schéma permet uniquement de vérifier la structure du document ainsi que la conformité par rapport au standard.

La suite d’outil open source [ART-DECOR](https://docs.art-decor.org/) permet de créer et maintenir les modèles CDA et les jeux de valeurs. Elle permet de tester la conformité d’un document CDA, mais cette fois-ci par rapport à un modèle, grâce à la génération de schématrons. Il s’agit d’un langage permettant de valider la structure d’un document XML via un ensemble d’assertions.

Les [plateformes Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) (ANS et IHE) sont également utilisées pour tester les documents. L’outil Schematron Validator intègre schéma XSD et schematrons. Accessible via le service de Validation EVS Client, il permet de vérifier si :

* Le document est bien structuré
* Le document est conforme au schéma XML
* Le document respecte les règles spécifiées dans le modèle

##### CDA adapté au cas d’usage Téléradiologie

Le standard CDA est conçu pour structurer et échanger des documents cliniques persistants, porteurs de sens médical, tels que des comptes rendus, des lettres médicales ou des synthèses de prise en charge. Il vise à garantir la lisibilité humaine, la pérennité et la réutilisabilité clinique des documents échangés. Dans le cadre du volet Téléradiologie, les flux étudiés correspondent majoritairement à des échanges transactionnels et organisationnels (annulation de demande, décision de protocolisation, transmission d’informations post-acte), intervenant au fil du workflow de prise en charge. Ces échanges ne constituent pas des documents cliniques à part entière mais relèvent d’une logique d’échanges métiers structurés, contextualisés et à durée de vie limitée.

À ce titre, seul le flux relatif à la demande d’examen d’imagerie (flux 1) s’inscrit dans une logique documentaire et fait déjà l’objet d’une structuration CDA, par l’intermédiaire du volet CI-SIS dédié à la demande d’acte d’imagerie. Ce volet permet de représenter de manière standardisée les éléments cliniques et administratifs nécessaires à la prescription de l’examen, indépendamment des mécanismes de transport utilisés. Pour les autres flux du périmètre, bien qu’il soit théoriquement possible de représenter les concepts métiers au sein de documents CDA, une telle approche introduirait une complexité non justifiée et ne correspondrait pas à l’usage naturel du standard. En effet, la structuration documentaire apportée par CDA est déjà pleinement mobilisée en fin de workflow à travers le compte-rendu d’imagerie, qui constitue le livrable clinique de référence, destiné à être partagé et archivé, notamment au sein du DMP du patient.

Par ailleurs, au moment de la présente étude, les orientations nationales et européennes en matière d’interopérabilité privilégient le standard FHIR pour les nouveaux besoins d’échange, en particulier pour les cas d’usage transactionnels et les échanges de données cliniques structurées. Cette dynamique s’inscrit dans une logique de remplacement progressif du standard CDA pour les nouveaux flux.

##### Synthèse

Le standard CDA est particulièrement adapté à la structuration et à l’échange de documents cliniques pérennes, tels que le compte-rendu d’imagerie, qui constitue l’aboutissement du workflow de téléradiologie. En revanche, les flux intermédiaires étudiés relèvent d’échanges transactionnels et métiers qui ne s’inscrivent pas dans une logique documentaire.

Bien que techniquement envisageable, l’utilisation de CDA pour ces flux introduirait une complexité inutile et serait redondante avec la structuration déjà assurée en fin de processus. De plus, les orientations actuelles en matière d’interopérabilité privilégient le recours à FHIR pour les nouveaux besoins d’échange.

#### Standard FHIR

##### Présentation

[FHIR](https://www.hl7.org/fhir/) (Fast Healthcare Interoperability Resources) est un standard élaboré par HL7 qui s’appuie sur un ensemble de ressources, des blocs de données modulaires, qui correspondent à des objets métiers, médicaux ou administratifs. Ces objets sont caractérisés par des éléments de données, des contraintes et des relations avec d’autres objets métiers.

Les ressources et éléments définis dans FHIR sont restreints et ont pour objectif de répondre aux besoins communs, afin de maintenir une simplicité d’utilisation du standard. Pour répondre aux besoins spécifiques, des extensions doivent être créées dans des guides d’implémentations (IG)

##### Maturité et adoption

FHIR a mis en œuvre un modèle de maturité de ressources afin de fournir aux développeurs une idée de la maturité d’une ressource avant son utilisation et son implémentation. D’une manière générale, le standard FHIR dans sa version R4 offre encore peu de ressources à l’état normatif donc pouvant être considérées comme stables.

Dans sa version R5, seules 2 ressources supplémentaires sont passées à l’état normatif.

L’ANS exploite les ressources de ce standard dans 12 des 16 volets de la couche Service disponibles sur [l’espace de Publication](https://esante.gouv.fr/offres-services/ci-sis/espace-publication) du CI-SIS.

Plusieurs volets publiés dans le domaine du médico-social font appel à ce standard en limitant l’utilisation à quelques ressources. La majorité des données étant portée par un document CDA ([SI-MDPH – SI-SdO (Suivi des orientations)](https://interop.esante.gouv.fr/ig/cda/tddui/NormesStandards_TransfertDonneesDUI_V1.0.pdf#%5B%7B%22num%22%3A23%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C81%2C551%2C0%5D), [SI-SdO – SI-ESMS (Suivi des orientations)](https://esante.gouv.fr/volet-si-esms-viatrajectoire-module-ph))

Il convient de souligner que, bien que FHIR propose actuellement une version R5, les ressources mentionnées dans la suite du document seront basées sur la version R4, afin de se conformer aux guides d’implémentation de l’ANS et de maintenir une interopérabilité avec les différents systèmes mis en place sur le territoire français.

##### Outillage

Des outils sont élaborés pour implémenter et tester des systèmes basés sur le standard FHIR, dont :

* L’extension pour Visual Studio Code [FHIR tools](https://marketplace.visualstudio.com/items?itemName=Yannick-Lagger.vscode-fhir-tools);
* Un ensemble [d’outils de validation](http://hl7.org/fhir/R4/validation.html) des ressources FHIR ;
* [Des serveurs](https://confluence.hl7.org/display/FHIR/Public+Test+Servers) publiquement accessibles à des fins de tests, dont HAPI, une librairie de développement des ressources FHIR en Java.

La [plateforme Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) est également utilisée pour tester les ressources FHIR. L’outil [matchbox](https://ahdis.github.io/matchbox/) est accessible via le [service de Validation EVS Client](https://interop.esante.gouv.fr/evs/home.seam). Il permet de vérifier si :

* La structure XML ou JSON des ressources est valide ;
* Les ressources sont conformes aux exigences FHIR ;
* Les ressources sont conformes aux exigences des profils

##### Ressources FHIR adaptées au cas d’usage

Le standard FHIR offre la possibilité de construire un document. Chaque document FHIR correspond à une ressource Bundle (NM N) de type « document » rassemblant des ressources indépendantes dans des entrées. La première de ces entrées est obligatoirement constituée d’une ressource Composition qui organise le contenu du document à l’aide de sections. Chaque section peut contenir des informations descriptives (titre, auteur, texte…) et peut référencer une autre ressource contenue dans une entrée du bundle.

Dans le cadre du volet “téléradiologie” les ressources suivantes pourraient être utilisées et profilées si besoin pour représenter le contenu des flux d’informations :

* Ressource [Patient](https://hl7.org/fhir/R4/patient.html) (NM N) : La ressource Patient permet de représenter les données concernant l’identification et les coordonnées (télécommunication et adresse) de l’usager ainsi que ses contacts. Un profil français de cette ressource existe, nommé [FrPatient](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-patient-ins.html), pour prendre en compte des spécificités françaises, comme la gestion de l’INS par exemple.
* Ressource [Organization](https://hl7.org/fhir/R4/organization.html) (NM 3) : La ressource Organization permet de représenter une personne morale telle que l’ESSMS. Un profil français, [FrOrganization](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-organization.html), existe également pour cette ressource.
* Ressource [Practitioner](https://hl7.org/fhir/R4/practitioner.html) (NM 3) : La ressource Practitioner permet de représenter un professionnel de santé. Un profil français,[FRPractitioner](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-practitioner.html) existe également
* Ressource [PractitionerRole](https://hl7.org/fhir/R4/practitionerrole.html) (NM 2) : La ressource PractitionerRole permet de représenter la spécialité d’un professionnel de santé. Un profile français, [FRPractitionerRole](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-practitioner-role.html) existe également.
* Ressource [ServiceRequest](https://hl7.org/fhir/R4/servicerequest.html) (NM 2) : La ressource ServiceRequest permet de représenter une demande de service, comme par exemple une demande de diagnostic, de traitement ou d’opérations à effectuer.
* Ressource [Appointment](https://hl7.org/fhir/R4/appointment.html) (NM 3) : La ressource Appointment permet de représenter un rendez vous ou une demande de rendez vous avec un professionnel de santé, un dispositif médical ou une unité de soin. Un profil français, [FRAppointment](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-appointment.html) existe également.
* Ressource [AppointmentResponse](https://hl7.org/fhir/R4/appointmentresponse.html) (NM 3) : La ressource AppointmentResponse permet de représenter la réponse à une demande de rendez vous.
* Ressource [Condition](https://hl7.org/fhir/R4/condition.html) (NM 3) : La ressource Condition permet de représenter une affection, un problème, un diagnostic rencontré par un patient.
* Ressource [DocumentReference](https://hl7.org/fhir/R4/documentreference.html) (NM 3) : La ressource DocumentReference permet de représenter un document stocké dans différent format ou bien une référence vers ce document.
* Ressource [ImagingStudy](https://hl7.org/fhir/R4/imagingstudy.html) (NM 3) : La ressource ImagingStudy permet de représenter les métadonnées d’un objet DICOM.
* Ressource [GuidanceResponse](https://hl7.org/fhir/R4/guidanceresponse.html) (NM 2) : La ressource GuidanceResponse permet de représenter la réponse à la demande d’imagerie avec les éléments joints par le professionnel de santé effecteur.
* Ressource [Endpoint](https://hl7.org/fhir/R4/endpoint.html) (NM 2) : La ressource Endpoint permet de représenter un endpoint accessible comme un serveur (web,fhir,dicom,..)
* Ressource [Device](https://hl7.org/fhir/R4/device.html) (NM 2) : La ressource Device permet de représenter un équipement utilisé lors de la prise en charge du patient, que ce soit un DM ou un autre équipement .
* Ressource [MedicationAdministration](https://hl7.org/fhir/R4/medicationadministration.html) (NM 2) : La ressource MedicationAdministration permet de représenter l’injection ou la consommation d’un médicament pour un patient par un professionnel de santé.

| | |
| :--- | :--- |
| Patient | Patient |
| PSResponsable | Practitioner |
| PSEffecteur | Practitioner |
| IdentifiantDemandeExamen | ServiceRequest |
| StructureImagerie | Organization |
| PlateformeTeleradiologie | Organization |
| NatureDemande | ServiceRequest |
| DateDemande | ServiceRequest |
| IdentifiantRDV | Appointment |
| DateHeurePriseCharge | Appointment |
| JustificationDemande | Condition |
| Antecedents | Condition |
| MotifAnnulation | Appointment |
| MotifRefus | AppointmentResponse |
| DocumentDemandeExamen | DocumentReference |
| DocumentsTiers | DocumentReference |
| LocalisationAnatomique | BodyStructure |
| ModaliteImagerie | ImagingStudy |
| DecisionEffecteur | GuidanceResponse |
| ProtocoleImagerie | ImagingStudy |
| URLViewerDRIMBOX | Endpoint |
| DuréeRétentionImages | ImagingStudy |
| DateRéalisationExamen | ImagingStudy |
| IdentificationMatériel | Device |
| ProduitsAdministres | MedicationAdministration |
| AccessionNumber | ImagingStudy |
| StudyUID | ImagingStudy |
| codeEvenement | ImagingStudy |
| roleProfessionnel | PractitionerRole |

Table 1 : Mise en correspondance des concepts métier avec les ressources FHIR

##### Transport

Le standard FHIR utilise [l’API REST](https://build.fhir.org/http.html) pour l’échange et l’interrogation des ressources via différentes [interactions](https://build.fhir.org/exchange-module.html)

Différents niveaux [d’interactions](https://hl7.org/fhir/R4/http.html) sont possibles pour une API REST:

* Instance (s’applique à une ressource en particulier) ;
* Type (s’applique à un ensemble de ressources de même type) ;
* Système (s’applique à l’ensemble du système).

Les interactions qui pourront s’appliquer dans le cas du volet « Téléradiologie » sont les interactions au niveau instance suivantes :

* [Create](https://hl7.org/fhir/R4/http.html#create) pour l’ajout d’une nouvelle ressource sur le serveur grâce à la méthode HTTP POST ;
* [Delete](https://hl7.org/fhir/R4/http.html#delete) pour la suppression d’une ressource sur le serveur grâce à la méthode HTTP DELETE;
* [Update](https://hl7.org/fhir/R4/http.html#update) pour le remplacement d’une ressource existante sur le serveur grâce à la méthode HTTP PUT ou PATCH. Enfin, le corps des requêtes HTTP est une ressource FHIR qui peut être [formatée](https://hl7.org/fhir/R4/http.html#mime-type) en XML, JSON ou RDF (Turtle).

Comme évoqué précédemment, les ressources peuvent être concaténées au sein de ressource Bundle. Dans le cas d’un Bundle de type Document, le endpoint à utiliser sera `'base/Bundle'`.

Les interactions FHIR implémentent le protocole RESTful, couramment utilisé dans de nombreux domaines. Le [Richardson REST Maturity Model](http://martinfowler.com/articles/richardsonMaturityModel.html) définit 4 niveaux de maturité d’une API REST (de 0 à 3), FHIR se situe au niveau 2 mais l’utilisation d’extensions peut permettre d’atteindre le niveau 3. L’API FHIR est largement utilisée pour échanger des données de santé

Pour tester des requêtes HTTP FHIR, il est possible d’utiliser des serveurs publiquement accessibles à des fins de test, notamment HAPI, via des outils de test d’API tels que Postman ou Insomnia. La plateforme Gazelle, via le service de Validation EVS Client, permet aux éditeurs de valider les ressources et les requêtes FHIR en les comparant à des modèles. La plateforme offre également la possibilité d’utiliser des simulateurs FHIR permettant aux éditeurs de tester leur système de façon autonome. Enfin, de nombreux évènements de tests, tels que les Connectathons, et Projectathons permettent aux éditeurs de tester en situation réelle leur conformité aux spécifications ainsi que leur capacité à échanger avec des partenaires.

###### Adaptation au cas d’usage

Il est important de noter que, pour les interactions décrites ci-dessous, les acteurs doivent être en mesure non seulement d’envoyer des données, mais également d’en recevoir. En termes d’architecture, chaque acteur devra par conséquent être à la fois client et serveur. Chaque acteur devra également travailler la gestion des authentifications, des autorisations, et autres besoins de sécurité fondamentaux ; ces aspects sortent du périmètre de la présente étude.

###### Transmettre une demande d’examen d’imagerie

la transmission d’une demande d’examen d’imagerie peut être réalisée grâce à l’envoie d’une ressource, par exemple DocumentReference ou ServiceRequest via une requête POST reposant sur l’interaction “[create](https://build.fhir.org/http.html#create)”.

Si la création de la ressource s’est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 1.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 1 - Diagramme d'échange FHIR pour le flux 1 - Transmission d'une demande d'examen d'imagerie

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Créer une demande d’examen d’imagerie
* Transmettre la demande d’examen d’imagerie
* Recevoir la demande d’imagerie

###### Annulation d’une demande d’imagerie

L’annulation d’une demande d’imagerie peut être réalisée grâce à la suppression d’une ressource, par exemple Appointment via une requête DELETE reposant sur l’interaction “[delete]((https://build.fhir.org/http.md#delete)").

Si la suppression de la ressource s’est correctement effectuée, le consommateur retourne un code http `200 OK`. En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 2 - Diagramme d'échange FHIR pour le flux 2 - Annulation d'une demande d'examen d'imagerie

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Créer une annulation d’une demande d’examen d’imagerie
* Transmettre l’annulation de la demande d’examen d’imagerie
* Recevoir l’annulation de la demande d’examen d’imagerie

###### Réponse à une demande d’examen d’imagerie

la réponse à une demande d’examen d’imagerie peut être réalisée grâce à l’envoie d’une ressource, par exemple ImagingStudy ou GuidanceResponse via une requête POST reposant sur l’interaction “[create](https://build.fhir.org/http.html#create)”.

Si la création de la ressource s’est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 1.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 3 - Diagramme d'échange FHIR pour le flux 3 - Réponse à une demande d'examen d'imagerie

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Etablir le protocole d’imagerie
* Générer la réponse métier à la demande
* Transmettre la réponse métier à la demande
* Recevoir la réponse métier à la demande

###### Transmettre un complément d’information post-examen

Le complément d’information post-examen d’imagerie peut être réalisée grâce à l’envoie d’une ressource, par exemple ImagingStudy ou DocumentReference via une requête POST reposant sur l’interaction “[create](https://build.fhir.org/http.html#create)”.

Si la création de la ressource s’est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 1.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 4 - Diagramme d'échange FHIR pour le flux 4 - Transmission d'un complément d'information post-examen

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Réaliser le ou les actes d’imagerie
* Générer un complément d’information post-examen
* Transmettre un complément d’information post-examen
* Recevoir un complément d’information post-examen

##### Synthèse

FHIR est un standard moderne, largement adopté dans le domaine de la santé, permettant l’échange de données de santé de manière structurée et interopérable.

L’analyse des ressources FHIR applicables au volet « Téléradiologie » montre que ce standard permet de couvrir l’ensemble des concepts métier identifiés. La notion d’acquittement n’est toutefois pas explicitement modélisée en FHIR et doit être traitée via les mécanismes standards HTTP ou des ressources dédiées comme OperationOutcome.

Enfin, l’utilisation de FHIR implique que chaque acteur dispose d’un serveur FHIR, capable de jouer à la fois les rôles de client et de serveur, afin de supporter l’ensemble des échanges requis.

#### Standard HL7 version 2 (HL7 v2)

##### Présentation

[HL7 version 2 (HL7 v2)](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=185) est un standard de messagerie développé par l’organisation Health Level Seven International, destiné à l’échange d’informations entre systèmes d’information de santé. Il repose sur l’échange de messages structurés, composés de segments, de champs et de sous-composants, organisés selon des déclencheurs événementiels (triggers). Le standard définit la structure logique des messages ainsi que les règles de codage associées, sans imposer de modèle d’information unique. Cette approche confère à HL7 v2 une grande souplesse d’implémentation et explique en partie son adoption massive dans l’écosystème des systèmes d’information de santé.

Il est important de souligner que HL7 v2 ne prescrit pas le protocole de transport ni l’architecture des échanges. Le standard n’émet aucune hypothèse sur :

* la conception ou l’architecture des systèmes émetteurs et récepteurs
* le mode de communication sous-jacent (synchrone ou asynchrone)
* les mécanismes de transport, de sécurisation ou de routage des messages

Ainsi, le choix du protocole de transport est laissé à l’initiative des implémenteurs. Néanmoins, dans les usages historiques et recommandés, HL7 v2 est fréquemment associé au protocole MLLP (Minimal Lower Layer Protocol), qui permet l’échange de messages sur des connexions persistantes et facilite la gestion des accusés de réception techniques. Ces accusés de réception (ACK), permettent au système récepteur de notifier l’émetteur de la bonne réception et du traitement du message transmis. Les ACK peuvent être de nature :

* technique, attestant de la bonne réception et de la conformité syntaxique du message
* applicative, indiquant l’acceptation ou le rejet du message au regard de règles métier ou fonctionnelles.

L’intérêt de ces mécanismes d’accusés de réception réside dans la fiabilité des échanges et dans la maîtrise du cycle de vie des messages.

##### Maturité et adoption

HL7 v2 est un standard hautement mature, déployé de manière généralisée dans l’écosystème des systèmes d’information de santé. Afin de capitaliser l’expérience acquise et de favoriser la réutilisation des développements, la doctrine du CI-SIS incite à l’utilisation du HL7v2 pour le transport des documents CDA notamment en se conformant aux volets de référence suivants :

* [Transport d’un document CDA en HL7v2](https://esante.gouv.fr/volet-transport-dun-document-cda-r2-en-hl7-oru-oul-mdm)
* [Transmission au LPS d’un document CDA provenant d’un courriel MSSanté](https://esante.gouv.fr/volet-de-transmission-au-lps-dun-document-cda)

Cette reconnaissance institutionnelle renforce sa légitimité en tant que standard de référence pour les échanges transactionnels entre systèmes, dans une logique de continuité avec les infrastructures déjà en place.

Par ailleurs, il est aujourd’hui largement utilisé par les éditeurs de RIS, PACS et plateformes de téléradiologie, ce qui garantit une interopérabilité immédiate avec les systèmes existants.

##### Outillage

L’écosystème HL7 v2 bénéficie d’un outillage industriel éprouvé, largement diffusé auprès des acteurs du secteur :

* Moteurs d’interfaces HL7 (Mirth Connect, Rhapsody, Cloverleaf, etc.), permettant la transformation, le routage et la supervision des flux ;
* Bibliothèques logicielles dans la plupart des langages courants facilitant l’intégration applicative ;
* [Suite d’outil open source du NIST](https://hl7v2-igamt-2.nist.gov/home) permettant de créer et maintenir des guides d’implémentation HL7v2. Elle permet également de tester la conformité d’un message par rapport au guide généré ;
* [Les plateformes Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) (ANS et IHE) sont également utilisées pour tester les profils de message. L’outil GazelleHL7Validator intègre les fichiers de définitions. Accessible via le service de Validation EVS Client, il permet de vérifier si : 
* Le message est bien structuré
* Le message respecte les règles spécifiées dans les fichiers de définition
 

Cet outillage contribue à une mise en œuvre maîtrisée et sécurisée des échanges HL7 v2, y compris dans des environnements hétérogènes ou multi-éditeurs.

##### HL7v2 adapté au cas d’usage Téléradiologie

Le standard HL7 v2 est d’ores et déjà présent au sein du workflow global de la téléradiologie par l’intermédiaire du volet Transport de document CDA en HL7 v2, utilisé pour la transmission du compte-rendu d’imagerie depuis la plateforme de téléradiologie vers le RIS de la structure d’imagerie. Par ailleurs, le volet téléradiologie envisage également la transmission, en complément des éléments structurés de la demande d’examen, de documents associés tels que la demande d’examen formalisée ou tout document complémentaire permettant d’enrichir le contexte clinique. Ces flux complémentaires reposent également sur le volet de Transport de documents CDA en HL7 v2, renforçant ainsi la cohérence globale des échanges autour de ce standard.

Au-delà de ces usages existants, plusieurs profils IHE s’appuient historiquement sur HL7 v2 pour structurer les échanges liés aux workflows d’imagerie. Le profil [IHE Scheduled Workflow (SWF.b)](https://www.ihe.net/uploadedFiles/Documents/Radiology/IHE_RAD_Suppl_SWF.b_Rev1-7_2019-08-09.pdf) définit notamment les transactions permettant d’orchestrer le cycle de vie d’un acte d’imagerie, depuis la prescription jusqu’à la production des résultats. Bien que le profil SWF.b ne couvre pas l’intégralité des cas d’usage spécifiques à la téléradiologie, en particulier les étapes de validation médicale distante ou de protocolisation, il propose néanmoins un ensemble de briques fonctionnelles pertinentes, telles que la gestion des demandes d’examen, des statuts associés ou des identifiants d’actes. Ces briques peuvent être mobilisées et adaptées dans le cadre des flux de téléradiologie, sans nécessiter l’adoption exhaustive du profil.

De même, le profil [IHE PAM-FR](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf) (Patient Administration Management France), bien qu’orienté vers la gestion administrative des patients et non vers les processus métiers propres à la téléradiologie, constitue une référence nationale pour la gestion de l’identité patient et des traits d’identification, notamment autour de l’INS. Les segments et champs HL7 v2 définis par ce profil peuvent ainsi être réutilisés pour garantir une gestion cohérente et conforme de l’identité du patient dans les flux de téléradiologie, indépendamment des messages métiers échangés.

Dans cette perspective, l’analyse présentée ci-après vise à démontrer la capacité du standard HL7 v2 à couvrir les concepts métiers identifiés dans les spécifications fonctionnelles du volet Téléradiologie. Les tableaux de couverture proposés s’appuient à la fois sur les usages courants d’HL7 v2 et sur les briques définies dans les profils IHE SWF.b et PAM-FR, afin d’illustrer de manière concrète et opérationnelle la couverture fonctionnelle du standard pour chacun des flux identifiés.

###### Flux 1 - Transmission de la demande d’examen d’imagerie

Dans le cadre du flux de transmission de la demande d’examen d’imagerie, les concepts métiers identifiés dans les spécifications fonctionnelles peuvent être portés par un message HL7 v2 de type ORM, historiquement utilisé pour la prescription et la gestion des actes d’imagerie. Les mappings présentés ci-dessous s’appuient sur les usages courants d’HL7 v2, ainsi que sur les recommandations issues des profils IHE SWF.b et PAM-FR lorsque celles-ci sont pertinentes, notamment pour la gestion de l’identité patient et des acteurs impliqués.

| | | | |
| :--- | :--- | :--- | :--- |
| **StructureImagerie** | ORM^O01 | MSH / ORC | MSH-3, MSH-4ORC-21, ORC-22 |
| **PlateformeTeleradiologie** | ORM^O01 | MSH / ORC | MSH-5, MSH-6 |
| **Patient** | ORM^O01 | PID | PID-3, PID-5, PID-7, PID-8, PID-11 |
| **PSResponsable** | ORM^O01 | ORC | ORC-10, ORC-12 |
| **PSEffecteur** | ORM^O01 | ORC / OBR | ORC-11 / OBR-32 |
| **roleProfessionnel** | ORM^O01 | ORC / OBR | ORC-10 / ORC-11 / ORC-12 / OBR-32 |
| **IdentifiantDemandeExamen** | ORM^O01 | ORC | ORC-2 |
| **NatureDemande** | ORM^O01 | ORC | ORC-1 |
| **DateDemande** | ORM^O01 | ORC | ORC-9 |
| **IdentifiantRDV** | ORM^O01 | PV1 | PV1-19 |
| **DateHeurePriseCharge** | ORM^O01 | PV1 | PV1-44 |
| **JustificationDemande** | ORM^O01 | OBR / NTE | OBR-31, NTE-3 |
| **LocalisationAnatomique** | ORM^O01 | OBX | OBX-2 = CE / TX, OBX-5 |
| **ModaliteImagerie** | ORM^O01 | OBX | OBX-2 = CE / TX, OBX-5 |
| **Antecedents** | ORM^O01 | OBR | OBR-13 |

Table 2 : Couverture des concepts métier du flux 1 par le standard HL7v2

###### Flux 2 - Annulation de la demande d’examen d’imagerie

Le flux d’annulation de la demande d’examen d’imagerie vise à notifier la plateforme de téléradiologie de l’invalidation d’une demande précédemment transmise. HL7 v2 prévoit nativement ce cas d’usage au travers du segment ORC (Common Order) et plus particulièrement du champ ORC-1 - Order Control, qui permet de gérer le cycle de vie des ordres, incluant leur création, modification et annulation. Ce mécanisme, largement utilisé dans les workflows d’imagerie décrits par le profil IHE SWF.b, garantit une gestion cohérente et tracée des annulations sans introduire de nouveaux messages spécifiques.

| | | | |
| :--- | :--- | :--- | :--- |
| **StructureImagerie** | ORM^O01 | MSH / ORC | MSH-3, MSH-4ORC-21, ORC-22 |
| **PlateformeTeleradiologie** | ORM^O01 | MSH / ORC | MSH-5, MSH-6 |
| **Patient** | ORM^O01 | PID | PID-3, PID-5, PID-7, PID-8, PID-11 |
| **PSEffecteur** | ORM^O01 | ORC / OBR | ORC-11 / OBR-32 |
| **roleProfessionnel** | ORM^O01 | ORC / OBR | ORC-11 / OBR-32 |
| **IdentifiantDemandeExamen** | ORM^O01 | ORC | ORC-2 |
| **NatureDemande** | ORM^O01 | ORC | ORC-1 |
| **MotifAnnulation** | ORM^O01 | ORC / NTE | ORC-16, NTE-3 |

Table 3 : couverture des concepts métier du flux 2 par le standard HL7v2

###### Flux 3 - Réponse à la demande d’examen d’imagerie

Le flux de réponse à la demande d’examen d’imagerie correspond à la décision rendue par le médecin effecteur distant à l’issue de l’analyse de la prescription initiale. Cette réponse peut se traduire par une acceptation de la demande, accompagnée de la définition d’un protocole d’imagerie, ou par un refus, éventuellement assorti d’un motif explicatif. HL7 v2 ne définit pas de message spécifique dédié à la notion de « réponse à une demande » dans un contexte de téléradiologie. En revanche, le standard propose plusieurs mécanismes permettant de porter cette information, notamment via la gestion des statuts d’ordre (segment ORC) et l’ajout d’informations cliniques ou opérationnelles dans les segments OBR, OBX ou NTE. Ces mécanismes sont historiquement mobilisés dans les workflows d’imagerie décrits par le profil IHE SWF.b.

| | | | |
| :--- | :--- | :--- | :--- |
| **PlateformeTeleradiologie** | ORM^O01 / ORU^R01 | MSH / ORC | MSH-3, MSH-4ORC-21, ORC-22 |
| **StructureImagerie** | ORM^O01 / ORU^R01 | MSH / ORC | MSH-5, MSH-6 |
| **Patient** | ORM^O01 / ORU^R01 | PID | PID-3, PID-5, PID-7, PID-8, PID-11 |
| **PSEffecteur** | ORM^O01 / ORU^R01 | ORC | ORC-10, ORC-12 |
| **roleProfessionnel** | ORM^O01 / ORU^R01 | ORC / OBR | ORC-10 / ORC-11 |
| **IdentifiantDemandeExamen** | ORM^O01 / ORU^R01 | ORC | ORC-2 |
| **DecisionEffecteur** | ORM^O01 / ORU^R01 | ORC | ORC-1 |
| **MotifRefus** | ORM^O01 / ORU^R01 | ORC / NTE | ORC-16, NTE-3 |
| **ProtocoleImagerie** | ORM^O01 / ORU^R01 | OBX | OBX-5 |

Table 4 : couverture des concepts métier du flux 3 par le standard HL7v2

###### Flux 4 - Transmission d’un complément d’information post-acte d’imagerie

Le flux de transmission d’un complément d’information post-acte d’imagerie intervient à l’issue de la réalisation de l’examen. Il vise à transmettre au radiologue effecteur distant, ou à la plateforme de téléradiologie, des éléments permettant de compléter le contexte d’interprétation et de rédaction du compte-rendu d’imagerie. HL7 v2 permet de porter ce type d’information au travers de messages de résultats, en particulier le message ORU, combinant des segments OBR et OBX. Cette approche est historiquement utilisée dans les workflows d’imagerie pour la diffusion d’informations liées à l’examen réalisé.

| | | | |
| :--- | :--- | :--- | :--- |
| **StructureImagerie** | ORU^R01 | MSH / ORC | MSH-3, MSH-4ORC-21, ORC-22 |
| **PlateformeTeleradiologie** | ORU^R01 | MSH / ORC | MSH-5, MSH-6 |
| **Patient** | ORU^R01 | PID | PID-3, PID-5, PID-7, PID-8, PID-11 |
| **IdentifiantDemandeExamen** | ORU^R01 | ORC | ORC-2 |
| **IdentifiantRDV** | ORU^R01 | PV1 | PV1-19 |
| **AccessionNumber** | ORU^R01 | OBR | OBR-3 |
| **StudyUID** | ORU^R01 | OBR | OBR-4 |
| **DateRéalisationExamen** | ORU^R01 | OBR | OBR-7 |
| **LocalisationAnatomique** | ORU^R01 | OBX | OBX-2 = CE / TX, OBX-5 |
| **ModaliteImagerie** | ORU^R01 | OBX | OBX-2 = CE / TX, OBX-5 |
| **URLViewerDRIMBOX** | ORU^R01 | OBX | OBX-2 = ST / TX, OBX-5 |
| **DuréeRétentionImages** | ORU^R01 | OBX | OBX-2 = NM / TX, OBX-5 |
| **IdentificationMatériel** | ORU^R01 | OBX | OBX-2 = CE / TX, OBX-5 |
| **ProduitsAdministres** | ORU^R01 | OBX | OBX-2 = CE / TX, OBX-5 |
| **codeEvenement (LOINC / CCAM)** | ORU^R01 | OBX | OBX-3 |

Table 5 : couverture des concepts métier du flux 4 par le standard HL7v2

##### Synthèse

L’analyse des différents flux du volet Téléradiologie met en évidence la capacité du standard HL7 v2 à couvrir, de manière cohérente et opérationnelle, les échanges nécessaires à la mise en œuvre des flux identifiés dans les spécifications fonctionnelles. Ce standard bénéficie d’un haut niveau de maturité, d’un large outillage industriel et d’une interopérabilité éprouvée, en particulier dans le domaine de l’imagerie médicale. La capacité d’HL7 v2 à gérer nativement les statuts d’ordre et à fournir des mécanismes d’accusés de réception constitue à ce titre un élément structurant pour garantir la cohérence, la traçabilité et la fiabilité des échanges entre systèmes distants. L’utilisation conjointe de HL7 v2 et du protocole MLLP permet ainsi de répondre efficacement aux exigences de robustesse et de synchronisation attendues pour ce type de flux transactionnels. Par ailleurs, l’analyse montre que les profils IHE, en particulier IHE Scheduled Workflow (SWF.b) et IHE PAM-FR, apportent un cadre de référence pertinent pour l’usage d’HL7 v2 dans le domaine de l’imagerie. Les briques proposées par ces profils peuvent être mobilisées de manière ciblée, notamment pour la gestion du cycle de vie des demandes et pour la prise en compte des exigences nationales relatives à l’identité patient et à l’INS.

Enfin, si HL7 v2 montre certaines limites en matière de structuration fine des contenus cliniques complexes, celles-ci peuvent être compensées par l’adossement à des standards complémentaires, tels que les documents CDA pour la production et la diffusion du compte-rendu d’imagerie, ou les standards d’imagerie médicale pour l’accès aux images. Dans cette perspective, HL7 v2 s’impose comme un standard socle pertinent pour l’orchestration des flux de téléradiologie, au sein d’une architecture d’interopérabilité plus large et cohérente.

### Synthèse

#### Synthèse de la couverture des objets métiers par chaque standard étudié

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| Patient |   | N/A | ✔ | ✔ |
| PSResponsable |   | N/A | ✔ | ✔ |
| PSEffecteur |   | N/A | ✔ | ✔ |
| IdentifiantDemandeExamen |   | N/A | ✔ | ✔ |
| StructureImagerie |   | N/A | ✔ | ✔ |
| PlateformeTeleradiologie |   | N/A | ✔ | ✔ |
| NatureDemande |   | N/A | ✔ | ✔ |
| DateDemande |   | N/A | ✔ | ✔ |
| IdentifiantRDV |   | N/A | ✔ | ✔ |
| DateHeurePriseCharge |   | N/A | ✔ | ✔ |
| JustificationDemande |   | N/A | ✔ | ✔ |
| Antecedents |   | N/A | ✔ | ✔ |
| MotifAnnulation |   | N/A | ✔ | ✔ |
| MotifRefus |   | N/A | ✔ | ✔ |
| DocumentDemandeExamen |   | N/A | ✔ | ✔ |
| DocumentsTiers |   | N/A | ✔ | ✔ |
| LocalisationAnatomique |   | N/A | ✔ | ✔ |
| ModaliteImagerie |   | N/A | ✔ | ✔ |
| DecisionEffecteur |   | N/A | ✔ | ✔ |
| ProtocoleImagerie |   | N/A | ✔ | ✔ |
| URLViewerDRIMBOX |   | N/A | ✔ | ✔ |
| DuréeRétentionImages |   | N/A | ✔ | ✔ |
| DateRéalisationExamen |   | N/A | ✔ | ✔ |
| IdentificationMatériel |   | N/A | ✔ | ✔ |
| ProduitsAdministres |   | N/A | ✔ | ✔ |
| AccessionNumber |   | N/A | ✔ | ✔ |
| StudyUID |   | N/A | ✔ | ✔ |
| codeEvenement |   | N/A | ✔ | ✔ |
| roleProfessionnel |   | N/A | ✔ | ✔ |

Table 6 : Couverture des conepts métier par les différents normes et standards étudiés

#### Synthèse comparative des normes et standards étudiés

Cette section présente une synthèse comparative des normes et standards analysés dans les sections précédentes. Les items de cette synthèse sont inspirés des documents suivants :

* La [doctrine du CI-SIS](https://esante.gouv.fr/sites/default/files/media_entity/documents/CI-SIS_DOCTRINE_20210803_V1.1.pdf)
* « [Evaluating HIT Standards](https://www.himss.org/sites/hde/files/FileDownloads/2013-09-23-EvaluatingHITStandards-FINAL.pdf) » document sur la comparaison des standards publiés par l’organisation [HIMSS.](https://www.himss.org/)
* La méthode [CAMSS](https://joinup.ec.europa.eu/collection/common-assessment-method-standards-and-specifications-camss) (Common Assessment method for standards and specifications) soutenue par le programme de la commission européenne concernant les solutions d’interopérabilité pour les administrations publiques. Cette initiative vise à promouvoir la collaboration entre les états membres de l’union européenne dans la définition d’une méthode d’évaluation commune de standards pour le développement des services administratifs en ligne.

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| Outillage**Des outils de tests sont mis en œuvre pour valider l’adhérence au standard.** | ✔ | ✔ | ✔ | ✔ |
| Tests**Des tests sont effectués pour des versions de travail (dites STU -Standards for Trial Use) et/ou pour les guides d’implémentation normatifs.** |   | ✔ | ✔ | ✔ |
| Processus de prise en compte des améliorations | ✔ | ✔ | ✔ | ✔ |
| Existence de guides d’implémentation**Les guides référencent les standards de base avec au moins un cas d’usage et une optionalité sur les paramètres pour permettre les extensions.** |   | ✔ | ✔ | ✔ |
| Adapté aux dispositifs mobiles |   | ✔ | ✔ | ✔ |
| Stabilité de la documentation | ✔ | ✔ | ✔ | ✔ |
| Adoption par le marché et utilisation | ✔ | ✔ | ✔ | ✔ |
| Neutralité**les spécifications ne limitent pas la concurrence et l’innovation; les spécifications sont basées sur des développements scientifiques et technologiques de pointe.** | ✔ | ✔ | ✔ | ✔ |
| Qualité**la qualité est suffisante pour permettre le développement de produits et de services interopérables concurrents.** | ✔ | ✔ | ✔ | ✔ |
| Accessibilité**Les spécifications sont disponibles au public à des conditions raisonnables (y compris pour un prix raisonnable ou gratuitement).** | ✔ | ✔ | ✔ | ✔ |
| Couverture métier |   | N/A | ✔ | ✔ |

Table 7 : Synthèse comparative des normes et standards étudiés

### Analyse et conclusion

#### Normes et Standards étudiés

Cette section a pour objectif de comparer les normes et standards étudiés dans ce document, en vue de choisir le plus approprié pour la spécification du volet « Téléradiologie ».

##### DICOM

Le standard DICOM est indispensable pour la gestion et la mise à disposition des images médicales, mais ne couvre pas les échanges fonctionnels et organisationnels du volet Téléradiologie. Il est donc considéré comme hors périmètre pour la couverture des flux étudiés, tout en restant un composant essentiel du système d’imagerie.

##### CDA

Le standard HL7 CDA est adapté à la production et à l’échange de documents cliniques persistants, en particulier le compte-rendu d’imagerie, qui constitue le livrable clinique final du workflow. En dehors du flux de demande d’examen déjà couvert par un volet CI-SIS dédié, l’utilisation de CDA pour les échanges intermédiaires n’apporte pas de valeur ajoutée et introduit une complexité non souhaitée.

##### FHIR

Le standard HL7 FHIR permet de modéliser finement les concepts métiers associés aux cas d’usage du volet Téléradiologie et de supporter des échanges orientés ressources via des API REST. Il offre des capacités étendues en matière de structuration, d’évolutivité et d’interopérabilité sémantique.

##### HL7v2

Le standard HL7 v2 permet de couvrir l’ensemble des flux du volet Téléradiologie, en particulier les échanges transactionnels liés à la demande d’examen, à son annulation, à la décision de protocolisation et à la transmission d’informations post-acte. Sa structuration événementielle, associée aux mécanismes d’accusés de réception, garantit la robustesse et la cohérence des échanges entre systèmes distants.

Largement adopté dans l’écosystème de l’imagerie médicale et déjà utilisé dans les volets de transport de documents CDA, HL7 v2 constitue une solution immédiatement opérationnelle, limitant les impacts sur les systèmes existants et compatible avec les contraintes de déploiement du volet.

### Conclusion

La présente étude avait pour objectif d’identifier et de comparer les normes et standards susceptibles de répondre à la mise en œuvre des flux d’échange définis dans les spécifications fonctionnelles du volet Téléradiologie. L’analyse a porté sur un ensemble de standards largement utilisés dans le domaine de l’interopérabilité en santé, évalués au regard de plusieurs critères complémentaires : la capacité à structurer les contenus métiers, la couverture des cas d’usage identifiés, la maturité et le niveau d’adoption au sein de l’écosystème, l’existence d’outillage, ainsi que l’adéquation aux contraintes organisationnelles, techniques et réglementaires du contexte national.

L’étude met en évidence que le standard HL7 FHIR présente, d’un point de vue strictement fonctionnel et technique, une couverture particulièrement adaptée aux besoins du volet Téléradiologie. Sa granularité, son modèle d’information explicite, sa capacité à supporter des échanges transactionnels et son alignement avec les orientations européennes en matière d’interopérabilité en font un standard particulièrement pertinent et largement promu comme cible pour les futurs échanges de données de santé.

Toutefois, le choix d’un standard pour la mise en œuvre opérationnelle du volet ne peut se limiter à une analyse théorique de couverture fonctionnelle. Plusieurs contraintes de premier ordre ont été prises en compte dans cette étude. En particulier, l’un des objectifs structurants du volet Téléradiologie est de permettre le versement des demandes d’actes et des comptes rendus d’imagerie au sein du Dossier Médical Partagé (DMP), qui supporte à ce jour exclusivement des documents cliniques structurés au format CDA. Par ailleurs, les échéances de mise en œuvre imposent de privilégier des solutions limitant les impacts sur les systèmes existants, notamment les logiciels de RIS et les plateformes de téléradiologie déjà largement déployés. Dans ce contexte, le standard HL7 version 2 apparaît comme le choix le plus adapté pour accompagner la mise en œuvre du volet Téléradiologie. Son adoption massive au sein de l’écosystème, son inscription dans les orientations nationales, notamment à travers les volets de transport de documents CDA, ainsi que sa robustesse éprouvée pour la gestion de flux transactionnels, en font une solution pragmatique et immédiatement opérationnelle. Les profils IHE associés, en particulier IHE SWF.b et IHE PAM-FR, permettent en outre de s’appuyer sur des briques existantes et reconnues pour structurer les échanges liés au workflow d’imagerie et à la gestion administrative des patients. Ainsi, bien que FHIR constitue un standard particulièrement pertinent et appelé à jouer un rôle central dans les évolutions futures de l’interopérabilité en santé, le choix de HL7 v2 s’impose dans le cadre de ce volet comme la solution la plus à même de répondre aux contraintes opérationnelles actuelles, tout en garantissant la continuité des usages, la maîtrise des impacts pour les éditeurs et la conformité aux capacités actuelles du DMP. Ce choix s’inscrit dans une logique pragmatique, permettant une mise en œuvre efficace à court terme, tout en laissant ouverte la possibilité d’évolutions ultérieures vers des architectures fondées sur FHIR, en cohérence avec les trajectoires nationales et européennes.

