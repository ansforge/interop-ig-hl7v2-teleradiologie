# Normes et Standards - Volet Téléradiologie v0.1.0-ballot

* [**Table of Contents**](toc.md)
* **Normes et Standards**

## Normes et Standards

 **Résumé de l'étude**
 Cette étude compare les principaux standards d’interopérabilité susceptibles de répondre aux besoins d’échange du volet Téléradiologie, au regard de critères fonctionnels, techniques et réglementaires. DICOM et HL7 CDA ont été écartés comme supports principaux, leur positionnement ne correspondant pas aux échanges transactionnels attendus. HL7 FHIR offre une couverture fonctionnelle complète et s’inscrit dans les orientations de long terme, mais sa mise en œuvre opérationnelle reste exigeante. À court terme, HL7 v2 apparaît comme la solution la plus pragmatique, en raison de sa maturité, de son adoption par l’écosystème et de l’existence de profils IHE largement industrialisés. 

### Introduction

Le présent document présente l’ensemble des normes et standards susceptibles de répondre à la mise en œuvre des flux identifiés dans le document « [Spécifications fonctionnelles des échanges - Téléradiologie](.\specifications_fonctionnelles.md) ». L’objectif de cette étude est d’identifier, qualifier et comparer les standards pertinents pour supporter les échanges nécessaires à la pratique de la téléradiologie.

Les normes et standards étudiés au sein de cette étude sont les suivants :

| | | |
| :--- | :--- | :--- |
| HL7 Version 2.x (v2) | ✔ | Transport externe requis |
| DICOM | ✔ | ✔ (DICOM Upper Layer / DIMSE sur TCP/IP, DICOMweb) |
| HL7 CDA | ✔ | Transport externe requis |
| HL7 FHIR | ✔ | ✔ (HTTP(S), REST) |

Table 1 : Normes et standards étudiés

Les standards seront analysés notamment par rapport à leur capacité en matière de structuration du contenu et, le cas échéant, de modalités de transport. Cette étude s’inscrit dans un contexte de mise en œuvre opérationnelle contraint. Un objectif central du volet Téléradiologie est de permettre le versement dans le DMP des demandes d’examen d’imagerie et des comptes rendus produits en contexte de téléradiologie. Deux contraintes encadrent cet objectif :

* Le format imposé par le DMP : à ce jour, le DMP n’accepte que des documents cliniques structurés au format CDA.
* La compatibilité avec l’existant : les délais de mise en œuvre imposent de minimiser les impacts sur les systèmes déjà déployés, notamment les RIS et les plateformes de téléradiologie.

Ces éléments constituent des critères de choix déterminants, au même titre que la couverture fonctionnelle et technique des standards étudiés, et seront pris en compte dans l’analyse comparative et la conclusion de la présente étude.

Les versions des normes et standards étudiés dans le présent document sont celles disponibles à la date de réalisation de l’étude (décembre 2025).

L’étude présente un rappel synthétique du contexte du volet Téléradiologie. Elle propose ensuite, pour chacune des normes et standards étudiés, une analyse détaillée comprenant une description générale, leur maturité et leur niveau d’adoption au sein des systèmes de santé, l’existence d’outillage dédié, ainsi que leur pertinence au regard des cas d’usage identifiés.

Une synthèse comparative est ensuite proposée afin de faciliter la lecture et la mise en perspective des normes et standards évalués. Enfin, une analyse métier et technique croisée permet d’éclairer les choix de standardisation envisageables.

Cette étude s’appuie sur les recommandations et principes du Cadre d’interopérabilité des systèmes d’information de santé (CI-SIS), qui référence les normes et standards internationaux applicables au développement des volets métiers, et constitue le référentiel institutionnel national de doctrine pour l’interopérabilité du système de santé.

### Présentation synthétique du volet Téléradiologie

Cette étude s’inscrit dans le cadre des besoins d’interopérabilité associés au volet « Téléradiologie ». Ce volet a pour objectif de décrire les échanges, et leur contenu, nécessaires à la prise en charge d’un patient lorsque l’interprétation radiologique est réalisée à distance, entre une structure d’imagerie (lieu de réalisation de l’acte) et une plateforme de téléradiologie (lieu d’interprétation).

Les échanges d’informations interviennent principalement entre :

* Le RIS (Système d’Information Radiologique) de la structure d’accueil du patient
* Le système d’information de la plateforme de téléradiologie

La présente étude couvre les échanges décrits dans la Spécification fonctionnelle des échanges - Téléradiologie, à savoir :

* La transmission d’une demande d’examen d’imagerie
* L’annulation d’une demande d’examen
* La réponse à une demande d’examen (acceptation avec protocole d’imagerie ou refus)
* La transmission d’informations complémentaires post-examen

Les concepts métiers à véhiculer dans ces flux sont décrits en [étape 4 et 5](./specifications_fonctionnelles.md#identification-des-concepts-véhiculés-dans-les-flux-dinformations-et-correspondance-avec-les-classes-et-attributs-du-MOS) de la spécification fonctionnelle et couvrent plusieurs catégories de données essentielles à la pratique de la téléradiologie :

* Données administratives et d’identification : identités patient et professionnels de santé, identifiants de demandes et d’examens, informations de structure
* Données cliniques et de prescription : motif d’examen, indications, contexte clinique fourni par le médecin de proximité
* Données de protocole d’imagerie : éléments nécessaires à la réalisation de l’acte, fournis par le radiologue distant
* Données techniques et informations post-acte : conditions de réalisation, données documentaires

Le choix final des normes ou standards devra permettre de couvrir l’intégralité des données véhiculées dans le cadre de la téléradiologie, ainsi que les scénarios d’échanges entre la structure d’imagerie et le service d’interprétation distant.

### Normes et Standards étudiés

Cette section présente les normes et standards susceptibles d’être utilisés pour structurer et, le cas échéant, transporter les données échangées dans le cadre du volet Téléradiologie. Les concepts métiers étudiés dans cette étude sont issus de la Spécification fonctionnelle des échanges Téléradiologie.

#### Standard DICOM

##### Présentation

Le standard [DICOM (Digital Imaging and Communications in Medicine)](https://www.dicomstandard.org/) est un standard international dédié à la gestion, au stockage, à la transmission et à la visualisation des images médicales. Il définit à la fois un format de fichier pour l’imagerie médicale et un ensemble de services réseau permettant l’échange de ces images et des métadonnées associées entre équipements et systèmes d’information d’imagerie (modalités, PACS, visionneuses). DICOM est nativement orienté vers les besoins associés aux domaines de l’imagerie médicale, notamment la radiologie, la médecine nucléaire, la radiothérapie et l’imagerie interventionnelle. Il constitue le socle technique permettant l’échange d’images médicales et d’informations associées au sein des systèmes d’imagerie.

##### Maturité et adoption

Le standard DICOM bénéficie d’un très haut niveau de maturité et d’une adoption quasi universelle dans le domaine de l’imagerie médicale. Il est implémenté par l’ensemble des constructeurs de modalités, de PACS, de solutions d’archivage et de visualisation d’images médicales. Son adoption massive et son interopérabilité éprouvée en font un standard incontournable pour la gestion des images médicales, tant au niveau national qu’international. La maturité et l’adoption du standard DICOM sont étroitement liées aux travaux menés depuis plus de vingt ans dans le cadre du domaine IHE Radiology, qui constitue historiquement l’un des premiers et des plus structurants domaines d’IHE. Créé à la fin des années 1990, le domaine IHE Radiology a précisément pour objectif de favoriser l’interopérabilité des systèmes d’imagerie médicale en s’appuyant sur une utilisation du standard DICOM.

Dans ce cadre, DICOM est utilisé comme socle pour la gestion et l’échange des objets d’imagerie (images, études, séries, métadonnées techniques). De nombreux profils IHE du domaine Radiology reposent ainsi directement sur DICOM, parmi lesquels figurent notamment :

* Scheduled Workflow (SWF), pour l’orchestration du cycle de vie des examens d’imagerie
* Post-Processing Workflow (PWF), pour la gestion des traitements d’images
* Consistent Presentation of Images (CPI), pour garantir une présentation cohérente des images entre systèmes

Ces profils, largement implémentés, témoignent de l’adoption massive et de la robustesse de DICOM dans les environnements d’imagerie médicale. Ils illustrent également le rôle central de DICOM dans les architectures d’imagerie, en particulier pour la manipulation, la circulation et la consultation des données d’imagerie.

##### Outillage

L’écosystème DICOM est riche et largement industrialisé. Il comprend notamment :

* des modalités d’imagerie conformes DICOM
* des PACS et archives d’imagerie
* des visionneuses DICOM
* des services réseau standardisés (C-STORE, C-FIND, C-MOVE, etc.)

Ces outils sont spécifiquement conçus pour la manipulation d’images médicales et de leurs métadonnées, dans des architectures d’imagerie dédiées.

##### Transport

Le standard DICOM intègre nativement des mécanismes de transport dédiés à l’échange d’objets d’imagerie médicale et de métadonnées associées. Ces mécanismes sont historiquement fondés sur des échanges point à point entre systèmes d’imagerie, reposant sur des services applicatifs définis par le standard et véhiculés sur des protocoles réseau standards.

DICOM supporte également des mécanismes plus récents basés sur les technologies web, regroupés sous l’appellation DICOMweb, permettant l’accès, la recherche et le transfert d’objets d’imagerie via des interfaces HTTP(S).

L’ensemble de ces mécanismes est spécifiquement et exclusivement conçu pour le transport et la manipulation d’objets d’imagerie.

##### DICOM adapté au cas d’usage Téléradiologie

Dans le cadre du volet Téléradiologie, le standard DICOM joue un rôle essentiel pour la mise à disposition et l’archivage des images médicales produites lors de la réalisation de l’acte d’imagerie. Toutefois, ce rôle se situe en dehors du périmètre des flux fonctionnels étudiés dans le présent volet. Le standard DICOM n’est pas conçu pour prendre en charge des échanges transactionnels ou décisionnels de type métier, ni pour gérer le cycle de vie des demandes ou des décisions médicales associées. À ce titre, il ne permet pas de répondre aux besoins fonctionnels identifiés dans les spécifications du volet Téléradiologie. Les mécanismes d’accès aux images (PACS, visionneuses, plateformes d’échange) sont généralement intégrés dans des architectures d’imagerie existantes.

##### Synthèse

Le standard DICOM est un composant fondamental des systèmes d’imagerie médicale et demeure indispensable pour la gestion, l’archivage et la consultation des images médicales.
 Néanmoins, il n’est pas adapté pour répondre aux flux fonctionnels du volet Téléradiologie tels que définis dans les spécifications, lesquels relèvent principalement d’échanges transactionnels, organisationnels et décisionnels entre systèmes d’information.

#### Standard CDA

##### Présentation

Le standard [HL7 Clinical Document Architecture (CDA)](https://hl7.org/cda/stds/online-navigation/index.html) est un standard de structuration de documents cliniques spécifiant à la fois la structure et la sémantique des informations médicales, en vue de leur compréhension entre acteurs du système de santé. Il repose sur la syntaxe XML et ne définit pas de mécanisme de transport des documents.

Le standard HL7 CDA est porté par HL7, organisme accrédité par l’ANSI. La version 2 du standard (CDA R2) a par ailleurs été adoptée comme norme internationale ISO. Un document CDA est un document complet pouvant contenir du texte, des images et tout autre type de contenu multimédia. Les propriétés d’un document CDA sont les suivantes :

* Persistance : Tout au long de son existence, le CDA doit rester cohérent, accessible et inaltérable. La durée de vie du document dépendant du cadre législatif.
* Intendance : L’organisation émettrice du document dématérialisé doit en assurer la gestion et le suivi, en mettant à disposition les éventuelles mises à jour.
* Responsabilité : tout document doit être authentifié par une signature. La personne signataire prend la responsabilité du contenue du document.
* Cohérence : Le document embarque le contexte (médical et de gestion) de son contenu.
* Intégralité : Chaque document est complet. Le contenu et le contexte restent indissociables.
* Lisibilité : Le document doit pouvoir être restitué aux personnes habilitées à le lire, dans une présentation prédéterminée par l’auteur du document, au travers d’un outil de visualisation banalisé tel qu’un navigateur Internet.

Un document CDA contient deux parties :

* Un entête (header) : contient les informations nécessaires à l’identification et à la gestion du document. Elle fournit des éléments d’authentification du document, le contexte de soin, les participants, etc.
* Le corps (body) : contient les informations médicales véhiculées par le document. Il peut être construit suivant 3 niveaux : 
* Niveau 1 : le corps contient un texte non structuré ou une image
* Niveau 2 : le corps est organisé en sections contenant un bloc narratif
* Niveau 3 : le corps se présente sous la forme d’un ensemble hiérarchisé de sections pouvant contenir des données structurées dans des entrées, en plus d’un bloc narratif.
 

##### Maturité et adoption

Le standard HL7 CDA R2 est très répandu à l’international et largement adopté dans le contexte français. Le standard HL7 CDA est le format de référence utilisé dans les volets métiers du CI-SIS disponibles sur [l’espace de Publication du CI-SIS](https://esante.gouv.fr/offres-services/ci-sis/espace-publication). Ce standard est également utilisé dans de nombreux profils spécifiés par IHE (profils des domaines IHE PCC, IHE PALM, IHE PHARM, …). Le niveau 3 est un format international de structuration et de transmission des documents médicaux. Il permet notamment une intégration automatique des informations contenues dans le document, dans le logiciel métier concerné. Ce niveau permet non seulement une interopérabilité syntaxique, mais également sémantique.

Afin de capitaliser l’expérience acquise et de favoriser la réutilisation des développements, la [doctrine du CI-SIS](https://interop.esante.gouv.fr/ig/doctrine/) incite à l’utilisation du standard CDA R2 niveau 3 pour structurer les documents, notamment en se conformant aux volets de référence suivants :

* [Structuration minimale de documents de santé](https://esante.gouv.fr/volet-structuration-minimale-de-documents-de-sante), qui définit la structure des données de l’entête d’un document CDA
* [Modèles de contenus CDA](https://esante.gouv.fr/volet-de-reference-modeles-de-contenus-cda), qui définit la structure des données du corps du document.

Par ailleurs, au moment de la présente étude, les orientations nationales et européennes en matière d’interopérabilité évoluent vers des approches plus adaptées aux échanges de données structurées et aux usages transactionnels. Dans ce contexte, le recours au standard CDA tend à être réservé aux documents cliniques établis, et son utilisation pour la mise en œuvre de nouveaux flux d’échange apparaît de moins en moins pertinente.

##### Outillage

Un document CDA peut être testé contre un schéma XSD via un éditeur de texte tel que Notepad++. Ce schéma permet uniquement de vérifier la structure du document ainsi que la conformité par rapport au standard.

La suite d’outil open source [ART-DECOR](https://docs.art-decor.org/) permet de créer et maintenir les modèles CDA et les jeux de valeurs. Elle permet de tester la conformité d’un document CDA, mais cette fois-ci par rapport à un modèle, grâce à la génération de schématrons. Il s’agit d’un langage permettant de valider la structure d’un document XML via un ensemble d’assertions. Les schematrons peuvent être utilisés de deux manières :

* En mode autonome : exécution directe des schematrons sur un document
* En mode intégré : via des plateformes de test comme [Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) (ANS et IHE)

L’outil Schematron Validator, accessible via le service EVS Client de Gazelle, combine la validation XSD et schematron. Il permet de vérifier qu’un document :

* Est bien formé (structure XML valide),
* Est conforme au schéma XSD,
* Respecte les règles métier définies dans le modèle.

##### CDA adapté au cas d’usage Téléradiologie

Le standard CDA est conçu pour structurer et échanger des documents cliniques persistants, porteurs de sens médical, tels que des comptes rendus, des lettres médicales ou des synthèses de prise en charge. Il vise à garantir la lisibilité humaine, la pérennité et la réutilisabilité clinique des documents échangés. Dans le cadre du volet Téléradiologie, les flux étudiés correspondent majoritairement à des échanges transactionnels et organisationnels (annulation de demande, décision de protocolisation, transmission d’informations post-acte), intervenant au fil du workflow de prise en charge. Ces échanges ne constituent pas des documents cliniques à proprement parlé mais relèvent d’une logique d’échanges métiers structurés, contextualisés et à durée de vie limitée.

Bien qu’il soit théoriquement possible de représenter les concepts métiers au sein de documents CDA, une telle approche ne serait pas adaptée à la finalité du standard. Le CDA est en effet conçu pour structurer des documents cliniques persistants, destinés à être partagés, archivés et réutilisés dans le temps, ce qui ne correspond pas à la nature des flux de téléradiologie, essentiellement transactionnels, contextuels et à durée de vie courte. La structuration documentaire apportée par CDA est en revanche pleinement pertinente en fin de workflow, à travers le compte-rendu d’imagerie, qui constitue le livrable clinique de référence, destiné à être partagé et archivé, notamment au sein du DMP du patient.

##### Synthèse

Le standard CDA est adapté à la structuration et à l’échange de documents cliniques pérennes, tels que le compte-rendu d’imagerie, qui constitue l’aboutissement du workflow de téléradiologie. En revanche, les flux intermédiaires étudiés dans ce volet relèvent d’échanges transactionnels et métiers qui ne s’inscrivent pas dans une logique documentaire.

De plus, les orientations actuelles en matière d’interopérabilité privilégient le recours à FHIR pour les nouveaux besoins d’échange.

#### Standard FHIR

##### Présentation

[FHIR](https://www.hl7.org/fhir/) (Fast Healthcare Interoperability Resources) est un standard élaboré par HL7 qui s’appuie sur un ensemble de ressources, des blocs de données modulaires, qui correspondent à des objets métiers, médicaux ou administratifs. Ces objets sont caractérisés par des éléments de données, des contraintes et des relations avec d’autres objets métiers.

Les ressources et éléments définis dans FHIR sont restreints et ont pour objectif de répondre aux besoins communs, afin de maintenir une simplicité d’utilisation du standard. Pour répondre aux besoins spécifiques, des extensions doivent être créées dans des guides d’implémentations (IG).

Dans le cadre français, l’association [Interop’Sante](https://www.interopsante.org/) a publié un [guide d’implémentation FHIR](https://hl7.fr/ig/fhir/core/) qui définit des profils FHIR pour répondre aux besoins spécifiques du système de santé français. Ces profils adaptent les ressources FHIR standard pour inclure des contraintes et des extensions spécifiques au contexte français.

##### Maturité et adoption

FHIR a mis en œuvre un modèle de maturité de ressources afin de fournir aux développeurs une idée de la maturité d’une ressource avant son utilisation et son implémentation. D’une manière générale, le standard FHIR dans sa version R4 offre encore peu de ressources à l’état normatif donc pouvant être considérées comme stables.

Dans sa version R5, seules 2 ressources supplémentaires sont passées à l’état normatif.

L’ANS exploite les ressources de ce standard dans la majorité des volets de la couche Service disponibles sur [l’espace de Publication](https://esante.gouv.fr/offres-services/ci-sis/espace-publication) du CI-SIS.

Il convient de souligner que, bien que le standard HL7 FHIR dispose à ce jour d’une version R5, les ressources présentées dans la suite du document s’appuient sur la version R4, conformément à la stratégie nationale en vigueur. Cette stratégie relative au choix des versions FHIR a été définie dans le cadre de travaux conduits conjointement par Interop’Santé et l’Agence du Numérique en Santé en 2023-2024, puis validée à l’issue d’une [concertation](https://participez.esante.gouv.fr/project/fhir-r5-ou-r4/presentation/presentation) portée par l’ANS.

##### Outillage

Des outils nombreux et matures sont disponibles pour implémenter et tester des systèmes basés sur le standard FHIR, couvrant la validation syntaxique, sémantique et la conformité aux guides d’implémentation.

Parmi les outils facilitant le développement et la validation des ressources FHIR figurent notamment :

* L’extension pour Visual Studio Code [FHIR Tools](https://marketplace.visualstudio.com/items?itemName=Yannick-Lagger.vscode-fhir-tools), facilitant l’édition, la validation et la navigation dans les ressources FHIR ;
* Un ensemble [d’outils de validation](http://hl7.org/fhir/R4/validation.html) permettant de vérifier la conformité des ressources aux spécifications FHIR et aux profils déclarés ;
* Des [serveurs FHIR publics de test](https://confluence.hl7.org/display/FHIR/Public+Test+Servers), dont HAPI, qui constitue à la fois un serveur de référence et une librairie de développement FHIR en Java.

Plusieurs frameworks et plateformes de tests spécialisés complètent cet outillage :

* Inferno : framework extensible de tests automatisés pour HL7® FHIR®, successeur de l’outil Crucible, permettant de définir et d’exécuter des tests rigoureux de conformité ;
* Touchstone (AEGIS) : plateforme d’accélération des implémentations FHIR®, reposant sur le moteur de tests **TestScript**, proposant des serveurs de référence (**WildFHIR**) et un large catalogue de scripts de tests open source ;
* Asbestos (IHE/NIST) : outil de test basé sur **TestScript**, principalement utilisé pour la validation des implémentations des profils IHE, notamment IHE MHD ; son code source est disponible sur GitHub ;
* Matchbox (AHDIS) : moteur de validation open source, disponible sur GitHub, largement utilisé pour vérifier la conformité des ressources FHIR aux profils nationaux et internationaux ;
* ConformanceLab (Interoplab) : plateforme de validation FHIR® permettant aux organisations de configurer, gérer et publier leur propre environnement de tests et de certification basé sur **TestScript**.

La [plateforme Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) est également utilisée pour tester les ressources FHIR. L’outil [matchbox](https://ahdis.github.io/matchbox/) est accessible via le [service de Validation EVS Client](https://interop.esante.gouv.fr/evs/home.seam). Il permet de vérifier si :

* La structure XML ou JSON des ressources est valide ;
* Les ressources sont conformes aux exigences FHIR ;
* Les ressources sont conformes aux exigences des profils issues des guides d’implémentation.

Pour tester des requêtes HTTP FHIR, il est possible d’utiliser des serveurs publiquement accessibles à des fins de test, notamment HAPI, via des outils de test d’API tels que Postman ou Insomnia. La plateforme Gazelle, via le service de Validation EVS Client, permet aux éditeurs de valider les ressources et les requêtes FHIR en les comparant à des modèles. La plateforme offre également la possibilité d’utiliser des simulateurs FHIR permettant aux éditeurs de tester leur système de façon autonome. Enfin, des évènements de tests, tels que les Projectathons permettent aux éditeurs de tester en situation réelle leur conformité aux spécifications ainsi que leur capacité à échanger avec des partenaires.

##### Ressources FHIR adaptées au cas d’usage

Dans le cadre de cette étude, l’analyse de l’adaptation du standard HL7 FHIR au volet « Téléradiologie » est menée à un niveau global de couverture des concepts métiers. Elle repose sur la mise en correspondance des concepts identifiés dans les spécifications fonctionnelles avec les ressources FHIR existantes, ou, le cas échéant, avec des attributs portés par ces ressources. Les ressources suivantes pourraient être utilisées et profilées si besoin pour représenter le contenu des flux d’informations. Si des profils de ces ressources existent déjà dans le guide d’implémentation FRCORE il est recommandé de les utiliser ou d’en hériter.

* Ressource [Patient](https://hl7.org/fhir/R4/patient.html) (NM N) : La ressource Patient permet de représenter les données concernant l’identification et les coordonnées (télécommunication et adresse) du patient ainsi que ses contacts.
* Ressource [Organization](https://hl7.org/fhir/R4/organization.html) (NM 3) : La ressource Organization permet de représenter une personne morale telle que le centre de téléradiologie.
* Ressource [Practitioner](https://hl7.org/fhir/R4/practitioner.html) (NM 3) : La ressource Practitioner permet de représenter un professionnel de santé.
* Ressource [PractitionerRole](https://hl7.org/fhir/R4/practitionerrole.html) (NM 2) : La ressource PractitionerRole permet de représenter la spécialité d’un professionnel de santé.
* Ressource [ServiceRequest](https://hl7.org/fhir/R4/servicerequest.html) (NM 2) : La ressource ServiceRequest permet de représenter une demande de service, comme par exemple une demande de diagnostic, de traitement ou d’opération à effectuer.
* Ressource [Appointment](https://hl7.org/fhir/R4/appointment.html) (NM 3) : La ressource Appointment permet de représenter un rendez vous ou une demande de rendez vous avec un professionnel de santé, un dispositif médical ou une unité de soin.
* Ressource [AppointmentResponse](https://hl7.org/fhir/R4/appointmentresponse.html) (NM 3) : La ressource AppointmentResponse permet de représenter la réponse à une demande de rendez vous.
* Ressource [Condition](https://hl7.org/fhir/R4/condition.html) (NM 3) : La ressource Condition permet de représenter une affection, un problème, un diagnostic rencontré par un patient.
* Ressource [DocumentReference](https://hl7.org/fhir/R4/documentreference.html) (NM 3) : La ressource DocumentReference permet de représenter un document stocké dans différents formats ou bien une référence vers ce document.
* Ressource [ImagingStudy](https://hl7.org/fhir/R4/imagingstudy.html) (NM 3) : La ressource ImagingStudy permet de représenter les métadonnées d’un objet DICOM.
* Ressource [GuidanceResponse](https://hl7.org/fhir/R4/guidanceresponse.html) (NM 2) : La ressource GuidanceResponse permet de représenter la réponse à la demande d’imagerie avec les éléments joints par le professionnel de santé effecteur.
* Ressource [Endpoint](https://hl7.org/fhir/R4/endpoint.html) (NM 2) : La ressource Endpoint permet de représenter un endpoint accessible comme un serveur (web,fhir,dicom,..)
* Ressource [Device](https://hl7.org/fhir/R4/device.html) (NM 2) : La ressource Device permet de représenter un équipement utilisé lors de la prise en charge du patient, que ce soit un DM ou un autre équipement .
* Ressource [MedicationAdministration](https://hl7.org/fhir/R4/medicationadministration.html) (NM 2) : La ressource MedicationAdministration permet de représenter l’injection ou la consommation d’un médicament pour un patient par un professionnel de santé.
* Ressource [BodyStructure](https://hl7.org/fhir/R4/bodystructure.html) (NM 1) : La ressource BodyStructure permet de représenter une structure anatomique du corps humain.

Suivant l’analyse des concepts métier identifiés dans la spécification fonctionnelle du volet ‘Téléradiologie’, on peut les mettre en correspondance avec les ressources FHIR présentées ci-dessus :

| | |
| :--- | :--- |
| **Patient** | Patient |
| **PSResponsable** | Practitioner |
| **PSEffecteur** | Practitioner |
| **IdentifiantDemandeExamen** | ServiceRequest |
| **StructureImagerie** | Organization |
| **PlateformeTeleradiologie** | Organization |
| **NatureDemande** | ServiceRequest |
| **DateDemande** | ServiceRequest |
| **IdentifiantRDV** | Appointment |
| **DateHeurePriseCharge** | Appointment |
| **JustificationDemande** | Condition |
| **Antecedents** | Condition |
| **MotifAnnulation** | Appointment |
| **MotifRefus** | AppointmentResponse |
| **DocumentDemandeExamen** | DocumentReference |
| **DocumentsTiers** | DocumentReference |
| **LocalisationAnatomique** | BodyStructure |
| **ModaliteImagerie** | ImagingStudy |
| **DecisionEffecteur** | GuidanceResponse |
| **ProtocoleImagerie** | ImagingStudy |
| **URLPartielleViewer** | Endpoint |
| **DuréeRétentionImages** | ImagingStudy |
| **DateRéalisationExamen** | ImagingStudy |
| **IdentificationMatériel** | Device |
| **ProduitsAdministres** | MedicationAdministration |
| **AccessionNumber** | ImagingStudy |
| **StudyInstanceUID** | ImagingStudy |
| **codeEvenement** | ImagingStudy |
| **roleProfessionnel** | PractitionerRole |

Table 2 : Mise en correspondance des concepts métier avec les ressources FHIR

##### Transport

FHIR propose plusieurs paradigmes d’échange pour répondre à différents cas d’usage :

* [REST](https://build.fhir.org/http.html) – Le plus répandu. Les ressources sont exposées via une API HTTP classique (GET, POST, PUT, DELETE). Adapté aux échanges synchrones et aux architectures web modernes.
* [Messaging](https://build.fhir.org/messaging.html) – Échange de messages structurés (Bundle de type “message”) déclenchés par un événement. Proche du fonctionnement HL7 v2, adapté aux workflows asynchrones.
* [Documents](https://build.fhir.org/documents.html) – Échange de documents cliniques complets et signés (Bundle de type “document”), similaire au CDA. Utilisé quand l’intégrité et la persistance du document sont essentielles.
* [Services](https://hl7.org/fhir/R4/services.html) (SOA/RPC) – Appels d’opérations personnalisées.

l’échange et l’interrogation des ressources peut se faire via différentes [interactions](https://build.fhir.org/exchange-module.html)

Différents niveaux [d’interactions](https://hl7.org/fhir/R4/http.html) sont possibles via REST :

* Instance (s’applique à une ressource en particulier) ;
* Type (s’applique à un ensemble de ressources de même type) ;
* Système (s’applique à l’ensemble du système).

Les interactions qui pourront s’appliquer dans le cas du volet « Téléradiologie » sont les interactions au niveau instance suivantes :

* [Create](https://hl7.org/fhir/R4/http.html#create) pour l’ajout d’une nouvelle ressource sur le serveur grâce à la méthode HTTP POST ;
* [Delete](https://hl7.org/fhir/R4/http.html#delete) pour la suppression d’une ressource sur le serveur grâce à la méthode HTTP DELETE;
* [Update](https://hl7.org/fhir/R4/http.html#update) pour le remplacement d’une ressource existante sur le serveur grâce à la méthode HTTP PUT ou PATCH. Enfin, le corps des requêtes HTTP est une ressource FHIR qui peut être [formatée](https://hl7.org/fhir/R4/http.html#mime-type) en XML, JSON ou RDF (Turtle).

###### Adaptation au cas d’usage

Il est important de noter que, pour les interactions décrites ci-dessous, les acteurs doivent être en mesure non seulement d’envoyer des données, mais également d’en recevoir. En termes d’architecture, chaque acteur devra par conséquent être à la fois client et serveur. Chaque acteur devra également travailler la gestion des authentifications, des autorisations, et autres besoins de sécurité fondamentaux ; ces aspects sortent du périmètre de la présente étude.

Le paradigme Messaging de FHIR pourrait être envisagé pour la gestion des accusés de réception et une communication asynchrone. Le paradigme REST permettrait de gérer les échanges de ressources simplement via des requêtes HTTP.

Pour chaque flux d’information identifié dans le volet “Téléradiologie”, les échanges FHIR via RESTpourraient s’articuler comme suit :

###### Transmettre une demande d’examen d’imagerie

La transmission d’une demande d’examen d’imagerie peut être réalisée grâce à l’envoi d’une ressource, par exemple DocumentReference ou ServiceRequest via une requête POST reposant sur l’interaction “[create](https://build.fhir.org/http.html#create)”.

Si la création de la ressource s’est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 1.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 1 - Diagramme d'échange FHIR pour le flux 1 - Transmission d'une demande d'examen d'imagerie

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Créer une demande d’examen d’imagerie
* Transmettre la demande d’examen d’imagerie
* Recevoir la demande d’imagerie

###### Annulation d’une demande d’examen d’imagerie

L’annulation d’une demande d’examen d’imagerie peut être réalisée grâce à la suppression d’une ressource créée dans le flux 1, par exemple DocumentReference ou ServiceRequest via une requête DELETE reposant sur l’interaction “[delete](https://build.fhir.org/http.html#delete)”.

Si la suppression de la ressource s’est correctement effectuée, le consommateur retourne un code http `200 OK`. En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 2 - Diagramme d'échange FHIR pour le flux 2 - Annulation d'une demande d'examen d'imagerie

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Créer une annulation d’une demande d’examen d’imagerie
* Transmettre l’annulation de la demande d’examen d’imagerie
* Recevoir l’annulation de la demande d’examen d’imagerie

###### Réponse à une demande d’examen d’imagerie

La réponse à une demande d’examen d’imagerie peut être réalisée grâce à l’envoi d’une ressource, par exemple ImagingStudy ou GuidanceResponse via une requête POST reposant sur l’interaction “[create](https://build.fhir.org/http.html#create)”.

Si la création de la ressource s’est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 3.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 3 - Diagramme d'échange FHIR pour le flux 3 - Réponse à une demande d'examen d'imagerie

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Etablir le protocole d’imagerie
* Générer la réponse métier à la demande
* Transmettre la réponse métier à la demande
* Recevoir la réponse métier à la demande

###### Transmettre un complément d’information post-examen

Le complément d’information post-examen d’imagerie peut être réalisé grâce à l’envoi d’une ressource, par exemple ImagingStudy ou DocumentReference via une requête POST reposant sur l’interaction “[create](https://build.fhir.org/http.html#create)”.

Si la création de la ressource s’est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 4.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

Figure 4 - Diagramme d'échange FHIR pour le flux 4 - Transmission d'un complément d'information post-examen

Ce flux permettrait de couvrir l’ensemble des processus suivants :

* Réaliser le ou les actes d’imagerie
* Générer un complément d’information post-examen
* Transmettre un complément d’information post-examen
* Recevoir un complément d’information post-examen

##### Synthèse

FHIR est un standard moderne, largement adopté dans le domaine de la santé, permettant l’échange de données de santé de manière structurée et interopérable avec cependant un nombre limité de ressources à l’état normatif.

L’analyse des ressources FHIR applicables au volet « Téléradiologie » montre que ce standard permet de couvrir l’ensemble des concepts métier identifiés. Le paradigme Messaging permet d’avoir un échange asynchrone entre les acteurs ainsi qu’une gestion des acquittements similaire à HL7v2. Pour un échange de ressources plus rapide et simple à mettre en place, le paradigme REST est également envisageable. Enfin, l’utilisation de FHIR implique que chaque acteur dispose d’un serveur FHIR, capable de jouer à la fois les rôles de client et de serveur, afin de supporter l’ensemble des échanges requis.

#### Standard HL7 version 2 (HL7 v2)

##### Présentation

[HL7 version 2 (HL7 v2)](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=185) est un standard de messagerie développé par l’organisation Health Level Seven International, destiné à l’échange d’informations entre systèmes d’information de santé. Il repose sur l’échange de messages structurés, composés de segments, de champs et de sous-composants, organisés selon des déclencheurs événementiels (triggers). Le standard définit la structure logique des messages ainsi que les règles de codage associées, sans imposer de modèle d’information unique. Cette approche confère à HL7 v2 une grande souplesse d’implémentation et explique en partie son adoption massive dans l’écosystème des systèmes d’information de santé.

Il est important de souligner que HL7 v2 n’impose pas le protocole de transport ni l’architecture des échanges. Le standard n’émet aucune hypothèse sur :

* la conception ou l’architecture des systèmes émetteurs et récepteurs
* le mode de communication sous-jacent (synchrone ou asynchrone)
* les mécanismes de transport, de sécurisation ou de routage des messages

Ainsi, le choix du protocole de transport est laissé à l’initiative des implémenteurs. Néanmoins, dans les usages historiques et recommandés, HL7 v2 est fréquemment associé au protocole MLLP (Minimal Lower Layer Protocol), qui permet l’échange de messages sur des connexions persistantes et facilite la gestion des accusés de réception techniques. Ces accusés de réception (ACK), permettent au système récepteur de notifier l’émetteur de la bonne réception et du traitement du message transmis. Les ACK peuvent être de nature :

* technique, attestant de la bonne réception et de la conformité syntaxique du message
* applicative, indiquant l’acceptation ou le rejet du message au regard de règles métier ou fonctionnelles.

L’intérêt de ces mécanismes d’accusés de réception réside dans la fiabilité des échanges et dans la maîtrise du cycle de vie des messages.

##### Maturité et adoption

HL7 v2 est un standard hautement mature, initialement publié à la fin des années 1980 et ayant fait l’objet de nombreuses évolutions successives au travers de plusieurs versions majeures, témoignant de sa stabilité, de sa robustesse. Dans l’écosystème français, il est solidement ancré dans le contexte intra-hospitalier au sein pratiques des systèmes d’information de santé, en particulier dans le domaine de l’imagerie médicale. Ce constat repose à la fois sur son usage historique largement répandu et sur les travaux menés dans le cadre du volet Téléradiologie, notamment au travers d’ateliers associant éditeurs de RIS et plateformes de téléradiologie. Ces échanges ont permis de confronter les besoins opérationnels aux capacités des standards existants et ont confirmé le niveau de maturité et d’industrialisation de HL7 v2 pour ce type de cas d’usage. Par ailleurs, le [Livre blanc Téléradiologie](https://industriels.esante.gouv.fr/sites/default/files/media/document/Livre-Blanc-TLR_vFinale.pdf) élaboré par l’Agence du Numérique en Santé en collaboration avec l’écosystème éditeur s’appuie sur des flux fondés sur le standard HL7 v2, renforçant ainsi ce constat.

De plus, le CI-SIS incite à l’utilisation du standard HL7v2 pour le transport des documents CDA en intra-hospitalier notamment en se conformant aux volets de référence suivants :

* [Transport d’un document CDA en HL7v2](https://esante.gouv.fr/volet-transport-dun-document-cda-r2-en-hl7-oru-oul-mdm)
* [Transmission au LPS d’un document CDA provenant d’un courriel MSSanté](https://esante.gouv.fr/volet-de-transmission-au-lps-dun-document-cda)

L’ancrage d’HL7 v2 au niveau français est également la conséquence des travaux de l’organisme InteropSanté, qui publie et maintient des spécifications nationales fondées sur HL7 v2, telles que [les contraintes françaises du profil IHE PAM](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf), [les contraintes françaises sur les types de données HL7 v2](https://www.interopsante.org/f/db43469b624f3039f9610d8cb6b27830ed6a9fe1/IHE_France_Constraints_on_HL7_data_types_for_ITI_V1.8.2.pdf), ainsi que les profils [ILW.FR](https://www.interopsante.org/f/794889b493c4434447de15737a285529b2967ca7/IHE_ILW_FR_Vol1_1.4.pdf) et [LTW.FR](https://www.interopsante.org/f/8e4f8de143d65c6fd3f5f2c372729f2c3ff636fd/IHE_LTW_FR_Vol1_1.4_TI.pdf) encadrant les échanges de demandes et de résultats d’examens de biologie, en contexte intra-établissement et inter-organisations.

Ces spécifications contribuent à une mise en œuvre homogène, interopérable et industrialisée du standard HL7 v2 au niveau national.

##### Outillage

L’écosystème HL7 v2 bénéficie d’un outillage industriel éprouvé, largement diffusé auprès des acteurs du secteur :

* Moteurs d’interfaces HL7 (Mirth Connect, Rhapsody, Cloverleaf, etc.), permettant la transformation, le routage et la supervision des flux
* Bibibliothèques logicielles dans la plupart des langages de développement courants (Java, .NET, Python, JavaScript…), telles que [HAPI HL7](https://github.com/hapifhir/hapi-hl7v2), [NHapi](https://github.com/nHapiNET/nHapi) ou [hl7apy](https://crs4.github.io/hl7apy/), facilitant la génération, le parsing, la validation et le transport des messages HL7 v2 au sein des systèmes d’information
* [Suite d’outil open source du NIST](https://hl7v2-igamt-2.nist.gov/home) permettant de créer et maintenir des guides d’implémentation HL7v2. Elle permet également de tester la conformité d’un message par rapport au guide généré
* [Les plateformes Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) (ANS et IHE) sont également utilisées pour tester les profils de message. L’outil GazelleHL7Validator intègre les fichiers de définitions. Accessible via le service de Validation EVS Client, il permet de vérifier si : 
* Le message est bien structuré
* Le message respecte les règles spécifiées dans les fichiers de définition
 

Cet outillage contribue à une mise en œuvre maîtrisée et sécurisée des échanges HL7 v2, y compris dans des environnements hétérogènes ou multi-éditeurs.

##### HL7v2 adapté au cas d’usage Téléradiologie

Le standard HL7 v2 est d’ores et déjà présent au sein du workflow global de la téléradiologie par l’intermédiaire du [volet de transmission d’un document CDA-R2 en HL7v2](https://interop.esante.gouv.fr/ig/hl7v2/trans-cda-r2/index.html), utilisé pour la transmission du compte-rendu d’imagerie depuis la plateforme de téléradiologie vers le RIS de la structure d’imagerie. Par ailleurs, le volet téléradiologie envisage également la transmission, en complément des éléments structurés de la demande d’examen, de documents associés tels que la demande d’examen formalisée ou tout document complémentaire permettant d’enrichir le contexte clinique. Ces flux complémentaires reposent également sur le volet de Transport de documents CDA en HL7 v2, renforçant ainsi la cohérence globale des échanges autour de ce standard.

Au-delà de ces usages existants, plusieurs profils IHE du [domaine IHE RADIOLOGY](https://www.ihe.net/ihe_domains/radiology/) s’appuient historiquement sur HL7 v2 pour structurer les échanges liés aux workflows d’imagerie. Le profil [IHE Scheduled Workflow (SWF.b)](https://www.ihe.net/uploadedFiles/Documents/Radiology/IHE_RAD_Suppl_SWF.b_Rev1-7_2019-08-09.pdf) définit notamment les transactions permettant d’orchestrer le cycle de vie d’un acte d’imagerie, depuis la prescription jusqu’à la production des résultats. Bien que le profil SWF.b ne couvre pas l’intégralité des cas d’usage spécifiques à la téléradiologie, en particulier les étapes de validation médicale distante ou de protocolisation, il propose néanmoins un ensemble de briques fonctionnelles pertinentes, telles que la gestion des demandes d’examen, des statuts associés ou des identifiants d’actes. Ces briques peuvent être mobilisées et adaptées dans le cadre des flux de téléradiologie, sans nécessiter l’adoption exhaustive du profil IHE.

De même, le profil [IHE PAM-FR](https://www.interopsante.org/f/07f0be9ab9647f72a3e896fd14620eeba4b1f504/Publication-IHE_FRANCE_PAM_National_Extension_v2.11.2.pdf) (Patient Administration Management France), bien qu’orienté vers la gestion administrative des patients et non vers les processus métiers propres à la téléradiologie, constitue une référence nationale pour la gestion de l’identité patient et des traits d’identification, notamment autour de l’INS. Les segments et champs HL7 v2 définis par ce profil peuvent ainsi être réutilisés pour garantir une gestion cohérente et conforme de l’identité du patient dans les flux de téléradiologie, indépendamment des messages métiers échangés.

Dans cette perspective, l’analyse présentée ci-après vise à démontrer la capacité du standard HL7 v2 à couvrir les concepts métiers identifiés dans les spécifications fonctionnelles du volet Téléradiologie. Les tableaux de couverture proposés s’appuient à la fois sur les usages courants d’HL7 v2 et sur les briques définies dans les profils IHE SWF.b et PAM-FR, afin d’illustrer de manière concrète et opérationnelle la couverture fonctionnelle du standard pour chacun des flux identifiés.

Contrairement à l’approche retenue pour HL7 FHIR, où la couverture des concepts métiers est analysée de manière globale au travers des ressources du modèle d’information, l’adaptation du standard HL7 v2 au volet « Téléradiologie » est étudiée flux par flux. Cette approche s’explique par la nature même du standard, dans lequel la structuration des échanges repose sur des profils de messages distincts, susceptibles de varier selon le type de flux et l’étape du workflow concernée. En conséquence, l’ordre et la logique de couverture des concepts métiers diffèrent de ceux présentés pour FHIR.

###### Flux 1 - Transmission de la demande d’examen d’imagerie

Dans le cadre du flux de transmission de la demande d’examen d’imagerie, les concepts métiers identifiés dans les spécifications fonctionnelles peuvent être portés par un message HL7 v2 de type ORM, historiquement utilisé pour la prescription et la gestion des actes d’imagerie. Les mappings présentés ci-dessous s’appuient sur les usages courants d’HL7 v2, ainsi que sur les recommandations issues des profils IHE SWF.b et PAM-FR lorsque celles-ci sont pertinentes, notamment pour la gestion de l’identité patient et des acteurs impliqués.

| | | | |
| :--- | :--- | :--- | :--- |
| **StructureImagerie** | ORM^O01 | MSH - Message Header / ORC - Common Order | MSH-3 Sending Application, MSH-4 Sending Facility /ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **PlateformeTeleradiologie** | ORM^O01 | MSH - Message Header/ ORC - Common Order | MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | ORM^O01 | PID - Patient Identification |   |
| **PSResponsable** | ORM^O01 | ORC - Common Order | ORC-10 Entered By, ORC-12 Ordering Provider |
| **PSEffecteur** | ORM^O01 | ORC - Common Order / OBR - Observation Request | ORC-11 Verified By / OBR-32 Principal Result Interpreter |
| **roleProfessionnel** | ORM^O01 | ORC - Common Order / OBR - Observation Request | ORC-10 Entered By / ORC-11 Verified By / ORC-12 Ordering Provider / OBR-32 Principal Result Interpreter |
| **IdentifiantDemandeExamen** | ORM^O01 | ORC - Common Order | ORC-2 Placer Order Number |
| **NatureDemande** | ORM^O01 | ORC - Common Order | ORC-1 Order Control |
| **DateDemande** | ORM^O01 | ORC - Common Order | ORC-9 Date/Time of Transaction |
| **IdentifiantRDV** | ORM^O01 | PV1 - Patient Visit | PV1-19 Visit Number |
| **DateHeurePriseCharge** | ORM^O01 | PV1 - Patient Visit | PV1-44 Admit Date/Time |
| **JustificationDemande** | ORM^O01 | ORC - Common Order / NTE - Notes and Comments | OBR-31 Reason for Study, NTE-3 Comment |
| **LocalisationAnatomique** | ORM^O01 | OBX - Observation/Result | OBX-2 = CE / TX, OBX-5 |
| **ModaliteImagerie** | ORM^O01 | OBX - Observation/Result | OBX-2 = CE / TX, OBX-5 |
| **Antecedents** | ORM^O01 | OBR - Observation Request | OBR-13 Relevant Clinical Information |

Table 3 : Couverture des concepts métier du flux 1 par le standard HL7v2

###### Flux 2 - Annulation de la demande d’examen d’imagerie

Le flux d’annulation de la demande d’examen d’imagerie vise à notifier la plateforme de téléradiologie de l’invalidation d’une demande précédemment transmise. HL7 v2 prévoit nativement ce cas d’usage au travers du profil de message ORM^O01. Le segment ORC (Common Order) et plus particulièrement son champ ORC-1 Order Control- Order Control, permet de gérer le cycle de vie des ordres, incluant leur création, modification et annulation. Ce mécanisme, largement utilisé dans les workflows d’imagerie décrits par le profil IHE SWF.b, garantit une gestion cohérente et tracée des annulations sans introduire de nouveaux messages spécifiques.

| | | | |
| :--- | :--- | :--- | :--- |
| **StructureImagerie** | ORM^O01 | MSH - Message Header / ORC - Common Order | MSH-3 Sending Application, MSH-4 Sending Facility /ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **PlateformeTeleradiologie** | ORM^O01 | MSH - Message Header | MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | ORM^O01 | PID - Patient Identification |   |
| **PSEffecteur** | ORM^O01 | ORC - Common Order | ORC-11 Verified By / OBR-32 Principal Result Interpreter |
| **roleProfessionnel** | ORM^O01 | ORC - Common Order | ORC-10 Entered By / ORC-11 Verified By / ORC-12 Ordering Provider / OBR-32 Principal Result Interpreter |
| **IdentifiantDemandeExamen** | ORM^O01 | ORC - Common Order | ORC-2 Placer Order Number |
| **NatureDemande** | ORM^O01 | ORC - Common Order | ORC-1 Order Control |
| **MotifAnnulation** | ORM^O01 | ORC - Common Order / NTE - Notes and Comments | ORC-16 Order Control Code Reason, NTE-3 Comment |

Table 4 : couverture des concepts métier du flux 2 par le standard HL7v2

###### Flux 3 - Réponse à la demande d’examen d’imagerie

Le flux de réponse à la demande d’examen d’imagerie correspond à la décision rendue par le médecin effecteur distant à l’issue de l’analyse de la demande initiale. Cette réponse peut se traduire par une acceptation de la demande, accompagnée d’un protocole d’imagerie, ou par un refus, éventuellement assorti d’un motif explicatif. HL7 v2 ne définit pas de message spécifique dédié à la notion de « réponse à une demande » dans un contexte de téléradiologie. En revanche, le standard propose plusieurs mécanismes permettant de porter cette information, notamment via des profils de message comme ORM^O01 ou ORU^R01 qui assurent la gestion des statuts d’ordre (segment ORC) et l’ajout d’informations cliniques ou opérationnelles dans les segments OBR, OBX ou NTE. Ces mécanismes sont historiquement mobilisés dans les workflows d’imagerie décrits par le profil IHE SWF.b.

| | | | |
| :--- | :--- | :--- | :--- |
| **PlateformeTeleradiologie** | ORM^O01 / ORU^R01 | MSH - Message Header / ORC - Common Order | MSH-3 Sending Application, MSH-4 Sending Facility /ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **StructureImagerie** | ORM^O01 / ORU^R01 | MSH - Message Header / ORC - Common Order | MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | ORM^O01 / ORU^R01 | PID - Patient Identification |   |
| **PSEffecteur** | ORM^O01 / ORU^R01 | ORC - Common Order | ORC-10 Entered By, ORC-12 Ordering Provider |
| **roleProfessionnel** | ORM^O01 / ORU^R01 | ORC - Common Order / OBR - Observation Request | ORC-10 Entered By / ORC-11 Verified By |
| **IdentifiantDemandeExamen** | ORM^O01 / ORU^R01 | ORC - Common Order | ORC-2 Placer Order Number |
| **DecisionEffecteur** | ORM^O01 / ORU^R01 | ORC - Common Order | ORC-1 Order Control |
| **MotifRefus** | ORM^O01 / ORU^R01 | ORC - Common Order / NTE - Notes and Comments | ORC-16 Order Control Code Reason, NTE-3 Comment |
| **ProtocoleImagerie** | ORM^O01 / ORU^R01 | OBX - Observation/Result | OBX-2 = ED/TX, OBX-5 |

Table 5 : couverture des concepts métier du flux 3 par le standard HL7v2

###### Flux 4 - Transmission d’un complément d’information post-acte d’imagerie

Le flux de transmission d’un complément d’information post-acte d’imagerie intervient à l’issue de la réalisation de l’examen. Il vise à transmettre au radiologue effecteur distant des éléments permettant de compléter le contexte d’interprétation et de rédaction du compte-rendu d’imagerie. Dans les implémentations HL7 v2 existantes, ce type de flux est fréquemment pris en charge au moyen de messages ORU^R01, utilisés pour la transmission d’observations et de résultats. Ce message permet de véhiculer une grande variété d’informations via des segments OBX, mais ne dispose pas de segments dédiés pour porter nativement les identifiants DICOM de l’examen. À l’inverse, le message OMI^O23, introduit pour répondre spécifiquement aux besoins du domaine de l’imagerie, propose le segment IPC (Imaging Procedure Control), permettant de structurer explicitement les informations techniques liées à la procédure d’imagerie, notamment l’Accession Number et le StudyInstanceUID. Ainsi, le message OMI^O23 est préconisé pour la couverture de flux.

| | | | |
| :--- | :--- | :--- | :--- |
| **StructureImagerie** | OMI^O23 | MSH - Message Header / ORC - Common Order | MSH-3 Sending Application, MSH-4 Sending Facility /ORC-21 Ordering Facility Name, ORC-22 Ordering Facility Address |
| **PlateformeTeleradiologie** | OMI^O23 | MSH - Message Header / ORC - Common Order | MSH-5 Receiving Application, MSH-6 Receiving Facility |
| **Patient** | OMI^O23 | PID - Patient Identification |   |
| **IdentifiantDemandeExamen** | OMI^O23 | ORC - Common Order | ORC-2 Placer Order Number |
| **IdentifiantRDV** | OMI^O23 | PV1 - Patient Visit | PV1-19 Visit Number |
| **AccessionNumber** | OMI^O23 | IPC - Imaging Procedure Control | IPC-2 Requested Procedure ID |
| **StudyInstanceUID** | OMI^O23 | IPC - Imaging Procedure Control | IPC-3 Study Instance UID |
| **DateRéalisationExamen** | OMI^O23 | OBR - Observation Request | OBR-7 Observation Date/Time |
| **LocalisationAnatomique** | OMI^O23 | OBX - Observation/Result | OBX-2 = CE / TX, OBX-5 |
| **ModaliteImagerie** | OMI^O23 | IPC - Imaging Procedure Control | IPC-5 Modality |
| **URLPartielleViewer** | OMI^O23 | OBX - Observation/Result | OBX-2 = ST / ED, OBX-5 |
| **DuréeRétentionImages** | OMI^O23 | TQ - Timing/Quantity | TQ1-6 Service Duration |
| **IdentificationMatériel** | OMI^O23 | IPC - Imaging Procedure Control | IPC-5 Modality |
| **ProduitsAdministres** | OMI^O23 | OBX - Observation/Result | OBX-2 = CE / TX, OBX-5 |
| **CodeEvenement (LOINC / CCAM)** | OMI^O23 | OBR - Observation Request | OBR-4 Universal Service Identifier |

Table 6 : couverture des concepts métier du flux 4 par le standard HL7v2

##### Synthèse

L’analyse des différents flux du volet Téléradiologie met en évidence la capacité du standard HL7 v2 à couvrir les concepts métiers échangés au sein des flux identifiés dans les spécifications fonctionnelles. Ce standard bénéficie d’un haut niveau de maturité, d’un large outillage industriel et d’une interopérabilité éprouvée dans le domaine de l’imagerie médicale. La capacité d’HL7 v2 à suivre les différentes étapes du traitement d’une demande d’examen et à gérer des accusés de réception contribue à sécuriser et tracer les échanges entre systèmes distants. L’utilisation conjointe de HL7 v2 et du protocole MLLP permet ainsi de répondre efficacement aux exigences de robustesse et de synchronisation attendues pour ce type de flux transactionnels. Par ailleurs, l’analyse montre que les profils IHE, en particulier IHE Scheduled Workflow (SWF.b) et IHE PAM-FR, apportent un cadre de référence pertinent pour l’usage d’HL7 v2 dans le domaine de l’imagerie. Les briques proposées par ces profils peuvent être mobilisées de manière ciblée, notamment pour la gestion du cycle de vie des demandes et pour la prise en compte des exigences nationales relatives à l’identité patient et à l’INS.

### Synthèse de l’étude

#### Synthèse de la couverture des objets métiers par chaque standard étudié

L’analyse de la couverture des objets métiers montre que les standards HL7 v2 et HL7 FHIR permettent de représenter l’ensemble des concepts métiers identifiés pour le volet Téléradiologie.

#### Synthèse comparative des normes et standards étudiés

Cette section présente une synthèse comparative des normes et standards analysés dans les sections précédentes. Les items de cette synthèse sont inspirés des documents suivants :

* La [doctrine du CI-SIS](https://interop.esante.gouv.fr/ig/doctrine/)
* « [Evaluating HIT Standards](https://www.himss.org/sites/hde/files/FileDownloads/2013-09-23-EvaluatingHITStandards-FINAL.pdf) » document sur la comparaison des standards publiés par l’organisation [HIMSS.](https://www.himss.org/)
* La méthode [CAMSS](https://joinup.ec.europa.eu/collection/common-assessment-method-standards-and-specifications-camss) (Common Assessment method for standards and specifications) soutenue par le programme de la commission européenne concernant les solutions d’interopérabilité pour les administrations publiques. Cette initiative vise à promouvoir la collaboration entre les états membres de l’union européenne dans la définition d’une méthode d’évaluation commune de standards pour le développement des services administratifs en ligne.

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| Couverture métier |   | Non étudiée | ✔ | ✔ |
| Adoption par l’écosystème Téléradiologie | ✔ | ✔ |   | ✔ |
| Rétrocompatibilité du standard ou de la norme | ✔ | ✔ |   | ✔ |
| Outillage**Des outils de tests sont mis en œuvre pour valider l’adhérence au standard.** | ✔ | ✔ | ✔ | ✔ |
| Tests**Des tests sont effectués pour des versions de travail (dites STU -Standards for Trial Use) et/ou pour les guides d’implémentation normatifs.** | ✔ | ✔ | ✔ | ✔ |
| Processus de prise en compte des améliorations | ✔ | ✔ | ✔ | ✔ |
| Existence de guides d’implémentation**Les guides référencent les standards de base avec au moins un cas d’usage et une optionalité sur les paramètres pour permettre les extensions.** | ✔ | ✔ | ✔ | ✔ |
| Adapté aux dispositifs mobiles | ✔ | ✔ | ✔ | ✔ |
| Stabilité de la documentation | ✔ | ✔ | ✔ | ✔ |
| Adoption par le marché et utilisation | ✔ | ✔ | ✔ | ✔ |
| Neutralité**les spécifications ne limitent pas la concurrence et l’innovation; les spécifications sont basées sur des développements scientifiques et technologiques de pointe.** | ✔ | ✔ | ✔ | ✔ |
| Qualité**la qualité est suffisante pour permettre le développement de produits et de services interopérables concurrents.** | ✔ | ✔ | ✔ | ✔ |
| Accessibilité**Les spécifications sont disponibles au public à des conditions raisonnables (y compris pour un prix raisonnable ou gratuitement).** | ✔ | ✔ | ✔ | ✔ |

Table 7 : Synthèse comparative des normes et standards étudiés

### Analyse et conclusion

#### Normes et Standards étudiés

Cette section a pour objectif de comparer les normes et standards étudiés dans ce document, en vue de choisir le plus approprié pour la spécification du volet « Téléradiologie ».

##### DICOM

Le standard DICOM est indispensable pour la gestion et la mise à disposition des images médicales, mais ne couvre pas les échanges fonctionnels et organisationnels du volet Téléradiologie.

##### CDA

Le standard HL7 CDA est adapté à la production et à l’échange de documents cliniques persistants, en particulier le compte-rendu d’imagerie, qui constitue le livrable clinique final du workflow. En dehors de la structuration du contenu de la demande d’examen déjà couvert par un volet CI-SIS dédié, l’utilisation de CDA pour les échanges intermédiaires n’est pas adapté au contexte de téléradiologie. De plus, les orientations européennes envisagées à moyen terme limitent l’intérêt d’engager de nouveaux travaux basés sur le standard CDA.

##### FHIR

Le standard HL7 FHIR permet de couvrir l’ensemble des concepts métier du volet Téléradiologie au travers de ressources structurées, largement adoptées dans le domaine de la santé. La mise en œuvre de FHIR suppose par ailleurs que chaque acteur dispose d’une infrastructure FHIR complète, capable d’assurer les rôles de client et de serveur pour supporter les flux d’échange.

##### HL7v2

L’analyse des flux du volet Téléradiologie montre que le standard HL7 v2 permet de couvrir l’ensemble des échanges identifiés. Il offre des mécanismes natifs de gestion des statuts et d’accusés de réception, adaptés aux flux transactionnels, notamment lorsqu’il est utilisé avec le protocole MLLP. Les profils IHE SWF.b et IHE PAM-FR fournissent par ailleurs des cadres de référence réutilisables pour le cycle de vie des demandes d’imagerie et la gestion de l’identité patient.

Largement adopté dans l’écosystème de l’imagerie médicale et déjà utilisé dans les volets de transport de documents CDA, HL7 v2 constitue une solution opérationnelle à court terme limitant les impacts sur les systèmes existants et compatible avec les contraintes de déploiement du volet.

### Conclusion

La présente étude a pour objectif d’identifier et de comparer les normes et standards susceptibles de répondre à la mise en œuvre des flux d’échange définis dans les spécifications fonctionnelles du volet Téléradiologie. L’analyse a porté sur un ensemble de standards largement utilisés dans le domaine de l’interopérabilité en santé, évalués au regard de plusieurs critères complémentaires : **la capacité à structurer les contenus métiers, la couverture des cas d’usage identifiés, la maturité et le niveau d’adoption au sein de l’écosystème, l’existence d’outillage, ainsi que l’adéquation aux contraintes organisationnelles, techniques et réglementaires du contexte national.**

Parmi les standards étudiés, **DICOM et HL7 CDA ont été écartés comme supports principaux des flux du volet Téléradiologie.** DICOM est spécifiquement dédié à la gestion, au stockage et à l’échange des objets d’imagerie médicale et ne vise pas la structuration des échanges métiers intervenant tout au long du workflow. Le standard HL7 CDA est, quant à lui, conçu pour la production de documents cliniques persistants, et pertinent en fin de parcours pour le compte-rendu d’imagerie. En revanche, son usage pour des échanges transactionnels intermédiaires à durée de vie courte ne correspond pas à son positionnement naturel. Par ailleurs, les orientations européennes et nationales récentes en matière d’interopérabilité privilégient désormais le standard HL7 FHIR pour les nouveaux besoins d’échange de données de santé structurées, ce qui limite la pertinence d’engager de nouveaux travaux fondés sur CDA dans ce contexte.

**L’analyse met en évidence que le standard HL7 FHIR présente une couverture fonctionnelle et technique complète des besoins du volet Téléradiologie.** Sa granularité, son modèle de données explicite et sa capacité à supporter des échanges transactionnels en font un standard particulièrement adapté aux cas d’usage identifiés. Par ailleurs, son alignement avec les orientations européennes en matière d’interopérabilité confirme son rôle structurant dans les trajectoires d’évolution à moyen et long terme des systèmes d’information de santé.

**L’étude montre également que le standard HL7 v2 est en mesure de couvrir l’ensemble des concepts métiers du volet Téléradiologie.** Il propose des mécanismes natifs adaptés à la gestion des échanges transactionnels, notamment pour le suivi de l’état de traitement des demandes et les accusés de réception. Son usage est bien maîtrisé par l’écosystème, en particulier dans le domaine de l’imagerie médicale, et s’appuie sur un outillage industriel éprouvé ainsi que sur des profils IHE largement diffusés.

**En conclusion, au regard des contraintes analysées dans cette étude, le standard HL7 v2 apparaît comme le plus à même de répondre aux besoins du volet Téléradiologie dans un contexte de mise en œuvre à court terme. HL7 v2 permet de couvrir l’ensemble des concepts métiers identifiés, tout en s’appuyant sur des mécanismes éprouvés pour la gestion de flux transactionnels. Sa maturité, son adoption éprouvée dans le domaine de l’imagerie médicale, ainsi que la disponibilité de profils IHE tels que PAM-FR et SWF.b permettent de capitaliser sur des briques existantes et largement industrialisées. Ce choix garantit ainsi une mise en œuvre pragmatique, limitant les impacts pour les éditeurs de RIS et de plateformes de téléradiologie tout en assurant la compatibilité avec les capacités actuelles du DMP.**

