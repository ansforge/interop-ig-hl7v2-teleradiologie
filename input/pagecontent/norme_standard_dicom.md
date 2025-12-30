#### Standard DICOM

##### Présentation

Le standard [DICOM (Digital Imaging and Communications in Medicine)](https://www.dicomstandard.org/) est un standard international dédié à la gestion, au stockage, à la transmission et à la visualisation des images médicales. Il définit à la fois un format de fichier pour l'imagerie médicale et un ensemble de services réseau permettant l'échange de ces images et des métadonnées associées entre équipements et systèmes d'information d'imagerie (modalités, PACS, visionneuses). DICOM est nativement orienté vers les besoins des domaines de l'imagerie médicale, notamment la radiologie, la médecine nucléaire, la radiothérapie et l'imagerie interventionnelle. Il constitue le socle technique des échanges d'images et d'informations associées au sein des systèmes d'imagerie.

##### Maturité et adoption

Le standard DICOM bénéficie d'un très haut niveau de maturité et d'une adoption quasi universelle dans le domaine de l'imagerie médicale. Il est implémenté par l'ensemble des constructeurs de modalités, de PACS, de solutions d'archivage et de visualisation d'images médicales. Son adoption massive et son interopérabilité éprouvée en font un standard incontournable pour la gestion des images médicales, tant au niveau national qu'international.
La maturité et l’adoption du standard DICOM sont étroitement liées aux travaux menés depuis plus de vingt ans dans le cadre du domaine IHE Radiology, qui constitue historiquement l’un des premiers et des plus structurants domaines d’IHE. Créé à la fin des années 1990, le domaine IHE Radiology a précisément pour objectif de favoriser l’interopérabilité des systèmes d’imagerie médicale en s’appuyant sur une utilisation du standard DICOM.

Dans ce cadre, DICOM est utilisé comme socle pour la gestion et l’échange des objets d’imagerie (images, études, séries, métadonnées techniques). De nombreux profils IHE du domaine Radiology reposent ainsi directement sur DICOM, parmi lesquels figurent notamment :
- Scheduled Workflow (SWF), pour l’orchestration du cycle de vie des examens d’imagerie
- Post-Processing Workflow (PWF), pour la gestion des traitements d’images
- Consistent Presentation of Images (CPI), pour garantir une présentation cohérente des images entre systèmes

Ces profils, largement implémentés, témoignent de l’adoption massive et de la robustesse de DICOM dans les environnements d’imagerie médicale. Ils illustrent également le rôle central de DICOM dans les architectures d’imagerie, en particulier pour la manipulation, la circulation et la consultation des données d’imagerie.

##### Outillage

L'écosystème DICOM est riche et largement industrialisé. Il comprend notamment :

- des modalités d'imagerie conformes DICOM
- des PACS et archives d'imagerie
- des visionneuses DICOM
- des services réseau standardisés (C-STORE, C-FIND, C-MOVE, etc.)

Ces outils sont spécifiquement conçus pour la manipulation d'images médicales et de leurs métadonnées, dans des architectures d'imagerie dédiées.

##### Transport

Le standard DICOM intègre nativement des mécanismes de transport dédiés à l’échange d’objets d’imagerie médicale et de métadonnées associées. Ces mécanismes sont historiquement fondés sur des échanges point à point entre systèmes d’imagerie, reposant sur des services applicatifs définis par le standard et véhiculés sur des protocoles réseau standards.

DICOM supporte également des mécanismes plus récents basés sur les technologies web, regroupés sous l’appellation DICOMweb, permettant l’accès, la recherche et le transfert d’objets d’imagerie via des interfaces HTTP(S). 

L’ensemble de ces mécanismes est spécifiquement et exclusivement conçu pour le transport et la manipulation d’objets d’imagerie.

##### DICOM adapté au cas d'usage Téléradiologie

Dans le cadre du volet Téléradiologie, le standard DICOM joue un rôle essentiel pour la mise à disposition et la consultation des images médicales produites lors de la réalisation de l'acte d'imagerie. Toutefois, ce rôle se situe en dehors du périmètre des flux fonctionnels étudiés dans le présent volet. Le standard DICOM n'est pas conçu pour véhiculer des échanges transactionnels ou décisionnels de type métier, ni pour gérer le cycle de vie des demandes ou des décisions médicales associées. À ce titre, il ne permet pas de répondre aux besoins fonctionnels identifiés dans les spécifications du volet Téléradiologie, en dehors de la fourniture d'un accès aux images. Les mécanismes d'accès aux images (PACS, visionneuses, plateformes d'échange) sont généralement intégrés dans des architectures d'imagerie existantes et peuvent être référencés dans les flux du volet Téléradiologie (par exemple via une URL de visionneuse), sans que DICOM ne constitue le standard d'échange principal pour ces flux.

##### Synthèse

Le standard DICOM est un composant fondamental des systèmes d'imagerie médicale et demeure indispensable pour la gestion, l'archivage et la consultation des images médicales.  
Néanmoins, il n'est pas adapté pour répondre aux flux fonctionnels du volet Téléradiologie tels que définis dans les spécifications, lesquels relèvent principalement d'échanges transactionnels, organisationnels et décisionnels entre systèmes d'information.
