#### Standard CDA

##### Présentation

Le standard [HL7 Clinical Document Architecture (CDA)](https://hl7.org/cda/stds/online-navigation/index.html) est un standard de structuration de documents cliniques spécifiant à la fois la structure et la sémantique des informations médicales, en vue de leur compréhension entre acteurs du système de santé. Il repose sur la syntaxe XML et ne définit pas de mécanisme de transport des documents.

Le standard HL7 CDA est porté par HL7, organisme accrédité par l’ANSI. La version 2 du standard (CDA R2) a par ailleurs été adoptée comme norme internationale ISO. Un document CDA est un document complet pouvant contenir du texte, des images et tout autre type de contenu multimédia. Les propriétés d'un document CDA sont les suivantes :

- Persistance : Tout au long de son existence, le CDA doit rester cohérent, accessible et inaltérable. La durée de vie du document dépendant du cadre législatif. 
- Intendance : L’organisation émettrice du document dématérialisé doit en assurer la gestion et le suivi, en mettant à disposition les éventuelles mises à jour.
- Responsabilité : tout document doit être authentifié par une signature. La personne signataire prend la responsabilité du contenue du document.
- Cohérence : Le document embarque le contexte (médical et de gestion) de son contenu.
- Intégralité : Chaque document est complet. Le contenu et le contexte restent indissociables.
- Lisibilité : Le document doit pouvoir être restitué aux personnes habilitées à le lire, dans une présentation prédéterminée par l’auteur du document, au travers d’un outil de visualisation banalisé tel qu’un navigateur Internet.

Un document CDA contient deux parties :

- Un entête (header) : contient les informations nécessaires à l'identification et à la gestion du document. Elle fournit des éléments d'authentification du document, le contexte de soin, les participants, etc.
- Le corps (body) : contient les informations médicales véhiculées par le document. Il peut être construit suivant 3 niveaux :
  - Niveau 1 : le corps contient un texte non structuré ou une image
  - Niveau 2 : le corps est organisé en sections contenant un bloc narratif
  - Niveau 3 : le corps se présente sous la forme d'un ensemble hiérarchisé de sections pouvant contenir des données structurées dans des entrées, en plus d'un bloc narratif.

##### Maturité et adoption

Le standard HL7 CDA R2 est très répandu à l'international et largement adopté dans le contexte français. Le standard HL7 CDA est le format de référence utilisé dans les volets métiers du CI-SIS disponibles sur [l'espace de Publication du CI-SIS](https://esante.gouv.fr/offres-services/ci-sis/espace-publication). Ce standard est également utilisé dans de nombreux profils spécifiés par IHE (profils des domaines IHE PCC, IHE PALM, IHE PHARM, …). Le niveau 3 est un format international de structuration et de transmission des documents médicaux. Il permet notamment une intégration automatique des informations contenues dans le document, dans le logiciel métier concerné. Ce niveau permet non seulement une interopérabilité syntaxique, mais également sémantique.

Afin de capitaliser l'expérience acquise et de favoriser la réutilisation des développements, la [doctrine du CI-SIS](https://interop.esante.gouv.fr/ig/doctrine/) incite à l'utilisation du standard CDA R2 niveau 3 pour structurer les documents, notamment en se conformant aux volets de référence suivants :

- [Structuration minimale de documents de santé](https://esante.gouv.fr/volet-structuration-minimale-de-documents-de-sante), qui définit la structure des données de l'entête d'un document CDA
- [Modèles de contenus CDA](https://esante.gouv.fr/volet-de-reference-modeles-de-contenus-cda), qui définit la structure des données du corps du document.

Par ailleurs, au moment de la présente étude, les orientations nationales et européennes en matière d’interopérabilité évoluent vers des approches plus adaptées aux échanges de données structurées et aux usages transactionnels. Dans ce contexte, le recours au standard CDA tend à être réservé aux documents cliniques établis, et son utilisation pour la mise en œuvre de nouveaux flux d’échange apparaît de moins en moins pertinente.

##### Outillage

Un document CDA peut être testé contre un schéma XSD via un éditeur de texte tel que Notepad++. Ce schéma permet uniquement de vérifier la structure du document ainsi que la conformité par rapport au standard.

La suite d'outil open source [ART-DECOR](https://docs.art-decor.org/) permet de créer et maintenir les modèles CDA et les jeux de valeurs. Elle permet de tester la conformité d'un document CDA, mais cette fois-ci par rapport à un modèle, grâce à la génération de schématrons. Il s'agit d'un langage permettant de valider la structure d'un document XML via un ensemble d'assertions. Les schematrons peuvent être utilisés de deux manières :

- En mode autonome : exécution directe des schematrons sur un document
- En mode intégré : via des plateformes de test comme [Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) (ANS et IHE)

L'outil Schematron Validator, accessible via le service EVS Client de Gazelle, combine la validation XSD et schematron. Il permet de vérifier qu'un document :

- Est bien formé (structure XML valide),
- Est conforme au schéma XSD,
- Respecte les règles métier définies dans le modèle.

##### CDA adapté au cas d'usage Téléradiologie

Le standard CDA est conçu pour structurer et échanger des documents cliniques persistants, porteurs de sens médical, tels que des comptes rendus, des lettres médicales ou des synthèses de prise en charge. Il vise à garantir la lisibilité humaine, la pérennité et la réutilisabilité clinique des documents échangés. Dans le cadre du volet Téléradiologie, les flux étudiés correspondent majoritairement à des échanges transactionnels et organisationnels (annulation de demande, décision de protocolisation, transmission d'informations post-acte), intervenant au fil du workflow de prise en charge. Ces échanges ne constituent pas des documents cliniques à proprement parlé mais relèvent d'une logique d'échanges métiers structurés, contextualisés et à durée de vie limitée.

Bien qu’il soit théoriquement possible de représenter les concepts métiers au sein de documents CDA, une telle approche ne serait pas adaptée à la finalité du standard. Le CDA est en effet conçu pour structurer des documents cliniques persistants, destinés à être partagés, archivés et réutilisés dans le temps, ce qui ne correspond pas à la nature des flux de téléradiologie, essentiellement transactionnels, contextuels et à durée de vie courte. La structuration documentaire apportée par CDA est en revanche pleinement pertinente en fin de workflow, à travers le compte-rendu d’imagerie, qui constitue le livrable clinique de référence, destiné à être partagé et archivé, notamment au sein du DMP du patient.

##### Synthèse

Le standard CDA est adapté à la structuration et à l'échange de documents cliniques pérennes, tels que le compte-rendu d'imagerie, qui constitue l'aboutissement du workflow de téléradiologie. En revanche, les flux intermédiaires étudiés dans ce volet relèvent d'échanges transactionnels et métiers qui ne s'inscrivent pas dans une logique documentaire.

De plus, les orientations actuelles en matière d'interopérabilité privilégient le recours à FHIR pour les nouveaux besoins d'échange.
