### Analyse et conclusion

#### Normes et Standards étudiés

Cette section a pour objectif de comparer les normes et standards étudiés dans ce document, en vue de choisir le plus approprié pour la spécification du volet « Téléradiologie ».

##### DICOM

Le standard DICOM est indispensable pour la gestion et la mise à disposition des images médicales, mais ne couvre pas les échanges fonctionnels et organisationnels du volet Téléradiologie.

##### CDA

Le standard HL7 CDA est adapté à la production et à l'échange de documents cliniques persistants, en particulier le compte-rendu d'imagerie, qui constitue le livrable clinique final du workflow. En dehors de la structuration du contenu de la demande d'examen déjà couvert par un volet CI-SIS dédié, l'utilisation de CDA pour les échanges intermédiaires n'est pas adapté au contexte de téléradiologie. De plus, les orientations européennes envisagées à moyen terme limitent l'intérêt d’engager de nouveaux travaux basés sur le standard CDA.

##### FHIR

Le standard HL7 FHIR permet de couvrir l’ensemble des concepts métier du volet Téléradiologie au travers de ressources structurées, largement adoptées dans le domaine de la santé. Les mécanismes d’acquittement ne sont pas modélisés nativement et reposent sur les échanges HTTP ou sur des ressources spécifiques telles qu’OperationOutcome. La mise en œuvre de FHIR suppose par ailleurs que chaque acteur dispose d’une infrastructure FHIR complète, capable d’assurer les rôles de client et de serveur pour supporter les flux d’échange.

D’une manière générale, le standard FHIR, dans sa version R4, repose encore sur un nombre limité de ressources à l’état normatif, pouvant être considérées comme pleinement stables et rétrocompatibles. Dans la version R5, seules deux ressources supplémentaires ont accédé à cet état normatif, ce qui implique une vigilance particulière quant à la gestion des évolutions et à la rétrocompatibilité dans le cadre de mises en œuvre opérationnelles.

##### HL7v2

L’analyse des flux du volet Téléradiologie montre que le standard HL7 v2 permet de couvrir l’ensemble des échanges identifiés. Il offre des mécanismes natifs de gestion des statuts et d’accusés de réception, adaptés aux flux transactionnels, notamment lorsqu’il est utilisé avec le protocole MLLP. Les profils IHE SWF.b et IHE PAM-FR fournissent par ailleurs des cadres de référence réutilisables pour le cycle de vie des demandes d’imagerie et la gestion de l’identité patient.

Largement adopté dans l'écosystème de l'imagerie médicale et déjà utilisé dans les volets de transport de documents CDA, HL7 v2 constitue une solution opérationnelle à court terme limitant les impacts sur les systèmes existants et compatible avec les contraintes de déploiement du volet.

### Conclusion

**La présente étude a pour objectif d'identifier et de comparer les normes et standards susceptibles de répondre à la mise en œuvre des flux d'échange définis dans les spécifications fonctionnelles du volet Téléradiologie. L'analyse a porté sur un ensemble de standards largement utilisés dans le domaine de l'interopérabilité en santé, évalués au regard de plusieurs critères complémentaires : la capacité à structurer les contenus métiers, la couverture des cas d'usage identifiés, la maturité et le niveau d'adoption au sein de l'écosystème, l'existence d'outillage, ainsi que l'adéquation aux contraintes organisationnelles, techniques et réglementaires du contexte national.**

**Parmi les standards étudiés, DICOM et HL7 CDA ont été écartés comme supports principaux des flux du volet Téléradiologie. DICOM est spécifiquement dédié à la gestion, au stockage et à l’échange des objets d’imagerie médicale et ne vise pas la structuration des échanges métiers intervenant tout au long du workflow. Le standard HL7 CDA est, quant à lui, conçu pour la production de documents cliniques persistants, et pertinent en fin de parcours pour le compte-rendu d’imagerie. En revanche, son usage pour des échanges transactionnels intermédiaires à durée de vie courte ne correspond pas à son positionnement naturel. Par ailleurs, les orientations européennes et nationales récentes en matière d’interopérabilité privilégient désormais le standard HL7 FHIR pour les nouveaux besoins d’échange de données de santé structurées, ce qui limite la pertinence d’engager de nouveaux travaux fondés sur CDA dans ce contexte.**

**L’analyse met en évidence que le standard HL7 FHIR présente une couverture fonctionnelle et technique complète des besoins du volet Téléradiologie. Sa granularité, son modèle de données explicite et sa capacité à supporter des échanges transactionnels en font un standard particulièrement adapté aux cas d’usage identifiés. Par ailleurs, son alignement avec les orientations européennes en matière d’interopérabilité confirme son rôle structurant dans les trajectoires d’évolution à moyen et long terme des systèmes d’information de santé.**

**L’étude montre également que le standard HL7 v2 est en mesure de couvrir l’ensemble des concepts métiers du volet Téléradiologie. Il propose des mécanismes natifs adaptés à la gestion des échanges transactionnels, notamment pour le suivi de l’état de traitement des demandes et les accusés de réception. Son usage est bien maîtrisé par l’écosystème, en particulier dans le domaine de l’imagerie médicale, et s’appuie sur un outillage industriel éprouvé ainsi que sur des profils IHE largement diffusés.**

**En conclusion, au regard des contraintes analysées dans cette étude, le standard HL7 v2 apparaît comme le plus à même de répondre aux besoins du volet Téléradiologie dans un contexte de mise en œuvre à court terme. HL7 v2 permet de couvrir l’ensemble des concepts métiers identifiés, tout en s’appuyant sur des mécanismes éprouvés pour la gestion de flux transactionnels. Sa maturité, son adoption éprouvée dans le domaine de l’imagerie médicale, ainsi que la disponibilité de profils IHE tels que PAM-FR et SWF.b permettent de capitaliser sur des briques existantes et largement industrialisées. Ce choix garantit ainsi une mise en œuvre pragmatique, limitant les impacts pour les éditeurs de RIS et de plateformes de téléradiologie tout en assurant la compatibilité avec les capacités actuelles du DMP.**
