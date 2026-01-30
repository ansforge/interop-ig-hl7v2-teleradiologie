<p style="padding: 5px; border-radius: 5px; border: 2px solid maroon; background: #ffffe6; width: 65%">
<b>Brief description of this Implementation Guide</b><br>
This implementation guide is part of the Service layer of the French Health Information Systems Interoperability Framework (CI-SIS) and aims to harmonize health data exchange practices in the field of teleradiology.

Based on use cases described in Volume 1 – Functional Study, the guide defines system actors, applicable transactions, collaborative workflows, and data flows. Volume 2 – Transaction Details specifies the technical implementation rules for the selected standards enabling these workflows.

The project scope focuses on modeling and specifying interactions between information systems required to share imaging data for remote radiological diagnosis.
</p>

{% if site.data.info.releaselabel == 'ci-build' %}
<div style="width: 65%">
    <blockquote class="stu-note">
    <p>Cet Implementation Guide n'est pas la version courante, il s'agit de la version en intégration continue soumise à des changements fréquents uniquement destinée à suivre les travaux en cours. La version courante sera accessible via l'URL canonique suite à la première release : http://interop.esante.gouv.fr/ig/fhir/[code - ig]</p>
    </blockquote>
</div>
{% endif %}

<div class="figure">
    <img src="ci-sis-logo.png" alt="CI-SIS" title="Logo du CI-SIS" style="width:100%;">
</div>

<div class="draft-content">
<p>
<b>QUESTIONS OUVERTES:</b><br>
<p><strong>Modalité de transmission du compte rendu</strong></p>
<p>Les modalités selon lesquelles le téléradiologue est informé du mode de transmission du compte rendu (CR), par exemple via MSS ou publication dans le DMP ne sont pas définies à ce stade.</p>

<br>

<p><strong>Gestion de la séquence des flux dits "complémentaires"</strong></p>
<p>Les modalités permettant à la plateforme de téléradiologie d’identifier et d’ordonner les messages ORU/MDM complémentaires associés à une demande d’examen, ainsi que les mécanismes permettant de déterminer le dernier message de la séquence de flux complémentaires, ne font pas l’objet d’une définition normative à l'heure actuelle.</p>
</p>
</div>

<br>

### Introduction

Ce document fait partie de la couche Service du [Cadre d'Interopérabilité des Systèmes d'Information de santé (CI-SIS)](https://esante.gouv.fr/offres-services/ci-sis/espace-publication). Les spécifications associées entendent définir et harmoniser les modalités de partage des données de santé propres au domaine de la téléradiologie (pour plus de précisions, se référer à la section « Périmètre du projet » ci-dessous).

La partie [« Volume 1 - Etude fonctionnelle »](./specifcations_fonctionnelles.html) associée à ce guide d'implémentation décrit, à titre d'exemple et de façon non-exhaustive, un ensemble de cas d'usage. Sur la base de ces cas d'usage, sont ensuite définis des acteurs du système d'information (au sens d'IHE) et des transactions applicables entre ces acteurs. Les processus collaboratifs applicables au domaine de la téléradiologie sont ensuite décrits et les flux entre les acteurs précédemment identifiés sont également définis.

La partie [« Volume 2 - Détail des transactions »](./specifications_techniques.html) associée à ce guide d'implémentation décrit les règles d'implémentation des standards retenus au sein de la partie « Normes et Standards » afin de permettre la mise en œuvre des processus collaboratifs mentionnés au sein de l'étude fonctionnelle.

### Périmètre du projet

La pratique de la téléradiologie correspond aux actes de télédiagnostic radiologiques réalisés par un radiologue exerçant à distance de la structure au sein de laquelle l'examen d'imagerie a été produit. Un tel service peut être mis en œuvre de manière ponctuelle, en situation d'urgence, ou de façon régulière dans un contexte de planification.

L'étude menée porte sur la modélisation et la spécification des interactions mises en œuvre entre les différents systèmes d'information afin de permettre **le partage d'éléments nécessaire à l'établissement d'un diagnostic distant** basé sur l'interprétation de données d'imagerie médicale.

Il est à noter que les spécifications d'interopérabilité présentées dans ce volet correspondent à des référentiels qui n'ont ni vocation à définir la structure interne et l'urbanisation des systèmes d'information ni vocation à aborder la gestion des habilitations. Cette gestion des habilitations relatives à l'accès aux données d'imagerie d'un patient doit faire l'objet d'une étude préalable avant toute implémentation de ces interfaces, dans le respect du cadre réglementaire de l'échange et du partage de données de santé applicables.

Les contraintes de sécurité concernant les flux de données associés à la pratique de la téléradiologie ne sont pas abordées au sein du présent document. Celles-ci sont du ressort de chaque responsable d'implémentation qui se trouve dans l'obligation de se conformer au cadre juridique en la matière. L'ANS propose un ensemble de référentiels dédiés à la politique de sécurité (la PGSSI-S) et des mécanismes de sécurisation sont définis au sein des volets de la couche Transport du Cadre d'Interopérabilité des systèmes d'information de santé (CI-SIS).

#### Lectorat cible

Le présent guide d'implémentation s'adresse principalement aux chefs de projets et développeurs ainsi que toute personne concernée par des travaux spécifiant des **interfaces interopérables entre structures d'imagerie et plateformes de téléradiologie**.

### Standards utilisés

Les données véhiculées dans ce volet ainsi que les interactions entre les systèmes reposent sur le standard HL7 v2.5.1.

#### Messages HL7 v2 profilés

Les messages HL7v2 profilés dans le cadre de ce guide d'implémentation sont les suivants :

- ORM^O01^ORM_O01
- ORU^R01^ORU_R01
- OMI^O23^OMI_O23

### Propriété intellectuelle

{% include ip-statements.xhtml %}
