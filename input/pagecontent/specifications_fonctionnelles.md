### Méthode

La structure de la présente spécification fonctionnelle s’appuie sur la [méthode d’élaboration des spécifications fonctionnelles des échanges élaborée par l’ANS](https://esante.gouv.fr/sites/default/files/media_entity/documents/2022.02.01_MethodeSpecificationEchange.V2.5.pdf).

La mise en œuvre de cette méthode correspond à la prise en compte de différentes étapes :

- Étape 0 : Cadre juridique et orientations organisationnelles

- Étape 1 : Organisation du contexte métier

- Étape 2 : Définition des processus collaboratifs

- Étape 3 : Description des processus collaboratifs et identification des flux

- Étape 4 : Identification des concepts véhiculés dans les flux d’informations et correspondance avec les classes et attributs du MOS (Modèle des Objets de Santé)

- Étape 5 : Modélisation des flux d’informations

### Cadre juridique et orientations organisationnelles

Le présent document présente l'étude correspondant à la rédaction d’une spécification fonctionnelle des échanges de données propres au domaine de la téléradiologie.

La téléradiologie désigne spécifiquement les actes de télédiagnostic radiologiques correspondant à « une prise en charge médicale radiologique à distance, réalisée en l’absence de radiologue sur place, que ce soit de manière ponctuelle en situation d’urgence ou de façon régulière hors urgence » (pour plus de précisions, se référer à la « [Charte de Téléradiologie ](https://www.conseil-national.medecin.fr/sites/default/files/2025-06/charteteleradiologie.pdf)» rédigée par le Conseil national professionnel de radiologie). Cette pratique permet à un radiologue externe à une structure d’imagerie donnée d’interpréter des examens d’imagerie réalisés en son sein.

L’étude menée concerne la modélisation des interactions mises en œuvre entre les différents systèmes d’information impliqués permettant le partage de données nécessaire à l’établissement d’un diagnostic distant basé sur l’interprétation de données d’imagerie médicale. Il est important de souligner qu’un soin a été apporté afin de concilier les travaux menés dans ce cadre avec le corpus documentaire associé au projet institutionnel « DRIM-M », définissant un maillage national permettant le partage de données d’imagerie.

Il est à noter que, de manière générale, les spécifications fonctionnelles des échanges correspondent à des référentiels d’interopérabilité qui n'ont ni vocation à définir la structure interne et l’urbanisation des systèmes d’information ni vocation à aborder la gestion des habilitations. Cette gestion des habilitations relatives à l’accès aux données d’imagerie d’un patient doit faire l'objet d'une étude préalable avant toute implémentation de ces interfaces dans le respect du cadre réglementaire de l'échange et du partage de données de santé applicables.

Par ailleurs, les contraintes de sécurité concernant les flux échangés ne sont pas traitées dans ce document. En effet, les aspects relatifs à la sécurité sont du ressort du système d’information implémentant de tels mécanismes.

Les situations de prise en charge d’urgence concernant un patient et impliquant une réorganisation des processus ainsi qu’un ajustement des mécanismes décrits dans la suite du document sont également considérées comme étant hors périmètre de cette étude.

#### Exemple de cas d'usage 

Cette section présente deux exemples, non exclusifs, d’appel à un service de téléradiologie par une structure d’imagerie. Ces deux exemples sont représentatifs d’un cas d’usage nominal associé au domaine de la téléradiologie (hors situation de prise en charge d’urgence d’un patient notamment). Les présentes spécifications ne s’appliquent pas uniquement aux cas d’usages mentionnés et peuvent faire intervenir des acteurs autres que ceux mentionnés. La dynamique d’échanges décrite au travers de ces cas d’usage est illustrée de manière détaillée au sein du diagramme de séquence présenté en [section Illustrations](#diagramme-de-séquence) de ces spécifications.

**<u>Contexte 1 :</u>** Un patient consulte son médecin traitant pour une douleur à l’avant-bras suite à une chute. Ce dernier lui indique la nécessité de réaliser un examen d’imagerie afin d’établir un diagnostic. Une demande d’examen d’imagerie en ce sens est alors rédigée par le médecin traitant et remise au patient. Le patient se rend au sein d’une structure d’imagerie afin de réaliser l’examen d’imagerie. Etant donné que la structure d’imagerie dispose de l’ensemble des équipements nécessaires à la prise en charge du patient mais qu’aucun radiologue n’est disponible afin d’interpréter les images médicales produites, il est décidé de faire appel à une plateforme de téléradiologie afin d’établir un diagnostic relatif au patient.

**<u>Cas d'usage 1 :</u>** Le patient reçu au sein de la structure d’imagerie est pris en charge par un professionnel de santé de proximité. Ce dernier formalise au besoin la demande d’examen d’imagerie propre au patient. La demande d’examen d’imagerie ainsi constituée est envoyée à la plateforme de téléradiologie adéquate afin qu’un radiologue distant puisse évaluer la pertinence de l’acte d’imagerie ciblé par la demande. Une fois cette analyse effectuée, en réponse à la réception de la demande d’examen d’imagerie, le radiologue distant transmet un protocole d’imagerie correspondant à l’examen devant être réalisé au sein de la structure d’imagerie. Sous la responsabilité du professionnel de santé de proximité, et en accord avec le protocole d’imagerie rédigé par le radiologue distant, un manipulateur d’électroradiologie médicale réalise l’acte de radiologie au sein de la structure d’imagerie. Les images médicales obtenues à l’issue de cet acte ainsi que diverses informations complémentaires sont mises à disposition du radiologue distant afin que celui-ci puisse établir un diagnostic concernant le patient. L’ensemble des éléments composant ce diagnostic sont consignés au sein d’un compte-rendu d’imagerie rédigé sous la responsabilité du radiologue distant. Une fois validé, le compte rendu d’imagerie est publié par la structure d’imagerie dans le DMP du patient pris en charge. Cette publication permet la consultation du document par un professionnel de santé tier autorisé ainsi que par le patient, selon les règles de visibilité applicables.

**<u>Contexte 2 :</u>** Un patient hospitalisé au sein d’un établissement de santé est ausculté par un médecin de proximité. Ce dernier lui indique la nécessité de réaliser un examen d’imagerie afin d’évaluer l’évolution de sa pathologie. Etant donné que l’établissement de santé dispose de l’ensemble des équipements d’imagerie nécessaires à la prise en charge du patient mais qu’aucun radiologue n’est disponible afin d’interpréter les images médicales produites, il est décidé de faire appel à une plateforme de téléradiologie afin d’établir un diagnostic relatif au patient.

**<u>Cas d'usage 2 :</u>** Le médecin de proximité ayant ausculté le patient formalise une demande d’examen d’imagerie. La demande d’examen d’imagerie ainsi constituée est envoyée à la plateforme de téléradiologie adéquate afin qu’un radiologue distant puisse évaluer la demande initialement formulée par le médecin de proximité. Une fois cette analyse effectuée, en réponse à la réception de la demande d’examen d’imagerie, le radiologue distant transmet un protocole d’imagerie correspondant à l’examen devant être réalisé au sein de la structure d’imagerie. Sous la responsabilité du professionnel de santé de proximité, et en accord avec le protocole d’imagerie rédigé par le radiologue distant, un manipulateur d’électroradiologie médicale réalise l’acte de radiologie au sein de la structure d’imagerie. Les images médicales obtenues à l’issue de cet acte ainsi que diverses informations complémentaires sont mises à disposition du radiologue distant afin que celui-ci puisse établir un diagnostic concernant le patient. L’ensemble des éléments composant ce diagnostic sont consignés au sein d’un compte-rendu d’imagerie rédigé sous la responsabilité du radiologue distant. Une fois validé, le compte rendu d’imagerie est publié par la structure d’imagerie dans le DMP du patient pris en charge. Cette publication permet la consultation du document par un professionnel de santé tier autorisé ainsi que par le patient, selon les règles de visibilité applicables.

#### Définitions et cadre juridique

##### Téléradiologie

La téléradiologie (également nommée télémédecine en imagerie) peut être définie de la manière suivante : « Prise en charge médicale radiologique à distance au service d’un patient en l'absence d'un radiologue sur place, soit en urgence de façon ponctuelle, soit de façon régulière en dehors de l’urgence » (définition issue de la [charte de téléradiologie](https://www.conseil-national.medecin.fr/sites/default/files/2025-06/charteteleradiologie.pdf) rédigée par le Conseil national professionnel de radiologie).

La pratique de la téléradiologie peut être assimilée à la téléconsultation au sens de la loi HPST (Hôpital, Patients, Santé, Territoires). De plus, l'acte de téléradiologie est, comme tout acte de télémédecine, un acte médical à part entière au sens défini dans le CSP (Code de la Santé Publique), voir articles L6316-1, R6316-3 et plus généralement les décrets n° 2010-1229 du 19 octobre 2010 relatif à la télémédecine et n° 2021-707 du 3 juin 2021 relatif à la télésanté. Cet acte est pratiqué à distance d’un patient par un radiologue effecteur de l’acte suite à la sollicitation d’un médecin demandeur. Il doit donc répondre aux mêmes obligations de moyens, de sécurité et de qualité, et se trouve encadré par les règles de déontologie médicale et de bonnes pratiques professionnelles applicables.

Le recours à la pratique de la téléradiologie doit être justifié et s’inscrire dans l’organisation des soins en vue de l’intérêt du patient. La mise en œuvre d’un projet territorial de téléradiologie implique une contractualisation globale entre le ou les établissements demandeurs et la ou les plateformes de téléradiologie effectrices. Ce contrat inclut notamment les aspects techniques, adaptés à la pratique médicale, juridiques, en termes de responsabilités respectives, et de qualité́ (technique et médicale). Cette organisation doit faire l’objet d’un modèle économique associant couverture des frais de fonctionnement et rémunération du radiologue. La téléradiologie ne doit pas remplacer, sans raison valable, une prise en charge radiologique sur place par un radiologue local. Elle ne peut pallier des problèmes démographiques territoriaux qui doivent mettre en oeuvre une autre solution. De plus, la téléradiologie doit permettre au médecin en contact direct avec le patient d’accéder à une médecine radiologique de qualité impliquant un radiologue (télédiagnostic).

En outre, une nouvelle démarche d’amélioration des pratiques ou « audit par les pairs » s’impose à tous les acteurs impliqués dès lors que les rayonnements ionisants sont mis en oeuvre, selon la norme NF S99‑300. La téléradiologie étant l’un des domaines audités. Cette évaluation se rapproche d’une démarche essentiellement à visée pédagogique sans mesure contraignante.

Pour plus de précisions concernant le cadre politique et législatif associé à la pratique de la téléradiologie, il est possible de se référer aux documents suivants :

- Guide de bonnes pratiques HAS : <https://www.has-sante.fr/jcms/c_2971634/fr/teleimagerie-guide-de-bonnes-pratiques>

- Charte de la téléradiologie G4 : <https://www.conseil-national.medecin.fr/publications/editions/charte-teleradiologie>

- Norme NF S99-300 : <https://www.boutique.afnor.org/fr-fr/norme/nf-s99300/demarche-qualite-en-imagerie-medicale/fa200225/264032>

- Eclairage télémédecine Direction de l’information légale et administrative : <https://www.vie-publique.fr/eclairage/18473-la-telemedecine-une-solution-pour-faciliter-lacces-aux-soins>.

##### Médecin demandeur

Le médecin demandeur établit la demande d’examen d'imagerie dédiée au patient et réceptionne le compte-rendu d’imagerie produit à l’issue de l’acte. Au sein de la demande d’examen formalisée, le médecin demandeur, qui aura au préalable procédé à l’examen clinique du patient, doit exposer la situation clinique du patient et exprimer la justification de l’examen d’imagerie. Le médecin demandeur, dans le cadre de la rédaction de la demande d’examen d’imagerie, doit indiquer tout élément pertinent et utile à la bonne prise en charge du patient : antériorités médicales et chirurgicales, existence d’examens antérieurs radiologiques ou autres. Par ailleurs, le médecin demandeur a la responsabilité de l’utilisation qui sera faite des informations mentionnées au sein du compte‐rendu d’imagerie transmis par le radiologue distant, et du contrôle de sa bonne intégration dans le dossier médical partagé du patient.

##### Professionnel de santé de proximité

Le professionnel de santé de proximité est une personne physique habilitée intervenant au sein de la structure d’imagerie. Selon l’organisation locale, ce rôle peut être assuré par un médecin ou par un manipulateur d’électroradiologie médicale. Le professionnel de santé de proximité est responsable de la prise en charge du patient au sein de la structure d’imagerie et veille à la bonne réalisation des actes d’imagerie. Lorsque ce rôle est assuré par un manipulateur d’électroradiologie médicale celui-ci agit sous la responsabilité d’un médecin, conformément au cadre réglementaire en vigueur.

##### Médecin effecteur

Le médecin effecteur analyse la pertinence de la demande d’examen d’imagerie formalisée par le médecin demandeur. En cas de validation de la demande d’examen d’imagerie, le médecin effecteur transmet à la structure d’imagerie un protocole d’imagerie adapté à celle-ci, interprète les images produites à l’issue de l’acte, rédige le compte-rendu d’imagerie (dont il est l’auteur) et le transmet à la structure d'imagerie qui accueille le patient.

Les médecins spécialistes de radiologie et d’imagerie médicale, dont fait partie le médecin effecteur dans le contexte de la téléradiologie, répondent à l’article L4021-3 issu du Code de la Santé Publique.

##### Demande d’examen d’imagerie

Le document « Demande d’examen d’imagerie » doit permettre de justifier la pertinence d’un ou plusieurs actes à réaliser concernant le patient. Ce document doit contenir à minima les informations suivantes qui pourront être complétées avec d’autres éléments utiles, formalisés par écrit, joints et qui seront archivés :

- Données administratives liées à la prise en charge (identification du patient, du demandeur et de la structure, date/heure, coordonnées du patient ou de son représentant : adresse, téléphone, etc.).

- Contexte clinique, antécédents médico-chirurgicaux.

- Objectif / finalité de l’examen d’imagerie à réaliser (examen à visée diagnostique ou dans le cadre d’un suivi par exemple).

- Région anatomique ciblée par l’acte.

- Terrain à risque et contre-indications éventuelles (allergie, insuffisance rénale, pacemaker etc.).

- Résultats d’examens de biologie et examens d’imagerie antérieurement pratiqués, si applicable.

- Type/technique d’examen d’imagerie souhaité.

- Délai souhaité de réalisation de l’acte.

- Attestation de prise de connaissance du patient et recueil de son consentement libre et éclairé.

Pour plus de précisions concernant le document « Demande d’examen d’imagerie », se référer au volet CI-SIS dédié : « [Volet Demande d’actes d’imagerie](https://esante.gouv.fr/volet-img-demande-dactes-dimagerie)».

Juridiquement, le document « Demande d’examen d’imagerie » répond notamment aux articles R1333-52 et R1333-53 issus du Code de la Santé Publique.

L’obligation de mise à disposition au sein de l’environnement Dossier Médical Partagé des documents correspondant aux Demandes d’examens d’imagerie relatives à un patient est effective à compter du 31/12/2025. Les conditions d’alimentation du Dossier Médical Partagé associé au patient pour lequel un acte d’imagerie est envisagé sont définies au travers des obligations règlementaires générales ainsi qu’au moyen de l’article L1111-15 issu du Code de la Santé Publique.

##### Compte-rendu d’imagerie

Juridiquement, le document « Compte-rendu d’imagerie » répond notamment à l’arrêté du 22 septembre 2006 relatif aux informations dosimétriques devant figurer dans un compte-rendu d'acte impliquant des rayonnements ionisants.

Le compte-rendu d’imagerie comporte à minima les informations suivantes :

- Identification du patient (nom, prénom, sexe, date de naissance, nom de jeune fille) et du médecin effecteur (identité et fonction).

- Date de réalisation du ou des actes d’imagerie.

- Eléments de justification du ou des actes d’imagerie et de la procédure réalisée, en tenant compte des guides de prescription et des guides de procédures mentionnés respectivement aux articles R1333-69 et R1333-70 issus du Code de la Santé Publique.

- Identification du matériel utilisé pour les techniques les plus irradiantes : radiologie interventionnelle, scanographie et radiothérapie.

- Informations utiles à l’estimation de la dose reçue par le patient au cours de la procédure.

Ainsi, le document « Compte-rendu d’imagerie » doit être conforme à une structure composée de quatre chapitres :

- Indications

- Technique

- Résultats

- Synthèse et conclusion

Pour plus de précisions concernant le document « Compte-rendu d’imagerie », se référer au volet CI-SIS dédié : « [Volet Compte-rendu d’imagerie ](https://esante.gouv.fr/volet-imagerie-cr-imagerie)».

Les conditions de mise à disposition d’un compte-rendu d’imagerie au sein du Dossier Médical Partagé associé au patient concerné par l’acte d’imagerie sont définies au travers des obligations règlementaires générales ainsi qu’au moyen de l’article L1111-15 issu du Code de la Santé Publique. Par conséquent, en dehors des situations de séjour hospitalier, l’ensemble des comptes-rendus d’imagerie produits doivent être versés au sein de l’environnement Dossier Médical Partagé du patient concerné.

Enfin, il est important de noter l’émergence d’un dispositif permettant le partage et l’accès aux données d’imagerie médicale au niveau national : le projet DRIM-M. Celui-ci résulte d’un partenariat entre radiologues, médecins nucléaires et pouvoirs publics. L’un des aspects intrinsèques au projet DRIM-M consiste à permettre la visualisation d’images médicales depuis la consultation du compte-rendu d’imagerie associé. Ainsi, afin de s’intégrer au maillage défini au travers du projet DRIM-M, les comptes-rendus d’imagerie doivent faire apparaître un ensemble d’informations relatives à cet usage (lien d’accès permettant la visualisation des images associées au compte-rendu, durée de rétention des données auprès de l’archive d’imagerie médicale, …).

### Lectorat cible

Les lecteurs cibles de la présente spécification sont principalement des chefs de projets et développeurs ainsi que toute personne concernée par les travaux de mise en conformité et qui spécifient des projets avec des interfaces interopérables des structures d'imagerie et des plateformes de téléradiologie.

### Organisation du contexte métier

La pratique de la téléradiologie peut être découpée en plusieurs groupes de processus associés à un contexte collaboratif entre un site demandeur d’une expertise médicale (structure d’imagerie) et un site distant en mesure de répondre à ce besoin (plateforme de téléradiologie). Dans ce cadre, trois groupes de processus sont distingués :

- Le premier groupe concerne la demande d’examen d’imagerie. Il couvre les actions nécessaires à la création, la transmission, l’annulation, la validation, le refus, la modification ou la publication d’une demande d’examen d’imagerie.

- Le deuxième groupe est relatif à la réalisation du ou des actes d’imagerie. Il englobe les actions nécessaires à la préparation, au déroulement et au partage d’un ou plusieurs examens d’imagerie.

- Le troisième groupe concerne la production et la diffusion du compte rendu d’imagerie. Ce groupe rassemble les processus associés à la rédaction, la validation (signature) et à la mise à disposition du compte rendu.

Il est important de noter que le système RIS, correspondant au système d’information de la structure d’imagerie, est considéré comme étant l’entité responsable des documents Demande d’Examen d’Imagerie et Compte-Rendu d’Imagerie. Cela implique que le système RIS est identifié comme tel au sein de ces documents et qu’il est responsable de la gestion de leur cycle de vie.

**<u>Note 1 :</u>** Le document compte-rendu d’imagerie est rédigé au sein de la plateforme de téléradiologie par un professionnel de santé effecteur, puis, au moyen d’un flux à destination du système RIS, transmis à la structure d’imagerie. Malgré le fait que le ce dernier soit identifié au sein du compte-rendu d’imagerie en tant qu’entité responsable de celui-ci, étant donné que le document a été rédigé depuis un environnement distant, le système RIS ne doit apporter aucune modification au compte-rendu d’imagerie réceptionné, en amont du processus de publication auprès de l’environnement DMP.

**<u>Note 2 :</u>** Il peut être pertinent de relever qu’une unique Demande d’Examen d’Imagerie peut conduire à la réalisation de plusieurs actes d’imagerie et donc à la production de plusieurs comptes-rendus d’imagerie. Cet aspect est pris en compte au sein de la présente étude, dans les limites du périmètre défini ci-dessous.

**<u>Note 3 :</u>** Dans le cadre des groupes de processus associés à la rédaction/validation de la demande d’examen d’imagerie ainsi que la construction du compte-rendu d’imagerie, le professionnel de santé impliqué peut être amené à consulter le DMP du patient concerné. Cela pourrait lui permettre de prendre connaissance d’éventuels antécédents ou d’éléments de compréhension complémentaires concernant le contexte de prise en charge du patient. Cependant, étant donné que les interactions entre les systèmes d’information mis en jeu dans le cadre de la téléradiologie et l’environnement DMP ne sont pas couverts par la présente étude, de tels mécanismes ne seront pas détaillés au sein de la description des processus ci-après. En revanche, la notion de transmission des antécédents relatifs au patient sera abordée au travers des flux décrits ci-après.

L’ensemble des informations précisées ci-dessus peuvent être illustrées au sein d’un diagramme de paquetage afin de représenter schématiquement les différentes composantes du domaine « Téléradiologie ».

<div class="figure" style="text-align: center;">
    <img src="F1_ContexteMetier.png"
         alt="Organisation du contexte métier de l’étude Téléradiologie"
         title="F1_ContexteMetier"
         style="width:5.75577in;height:5.67708in">

    <p>
        Figure 1 – Organisation du contexte métier de l’étude Téléradiologie
    </p>
</div>

Seuls les \<\<Processus\>\> identifiés avec la couleur orange sont inclus dans le périmètre de la présente étude et feront l’objet d’une modélisation détaillée dans la suite de la présente étude.  
Les \<\<Processus\>\> identifiés avec une couleur bleue ne sont pas couverts par cette étude pour les raisons suivantes :

- Soit il s’agit d’actions informelles et/ou couvertes par un mécanisme propriétaire ;

- Soit il s’agit d’aspects déjà spécifiés au sein de volets dédiés du Cadre d’Interopérabilité des Systèmes d’Information de Santé :

  - Le volet « Transmission d'un document CDA-R2 en HL7v2 » encadre les modalités d’échange de documents de santé rédigés au format CDA (quel que soit le niveau de structuration mis en œuvre).

  - Le volet « Structuration minimale des documents de santé » définit les règles de structuration des en-têtes de documents de santé rédigés au format CDA.

  - Le volet « IMG-CR-IMG – Compte-rendu d’imagerie » spécifie la structuration du corps d’un compte-rendu d’imagerie rédigé au format CDA (niveau N3). Ce volet n’est applicable qu’aux systèmes d’information en mesure d’assurer la gestion d’un compte-rendu d’imagerie présentant un tel niveau de structuration. Dans le cas où le corps du compte-rendu d’imagerie est constitué d’un document PDF (niveau N1), seul le volet CI-SIS mentionné au point précédent est applicable.

### Définition des processus collaboratifs

Les différents processus collaboratifs retenus dans le périmètre de la présente étude seront représentés au sein de ce chapitre au moyen de diagrammes représentant les personnes, systèmes et rôles mis en jeu. La dénomination des «Rôles» revêt un caractère générique. En revanche, les «Système» et «Personne» mentionnés correspondent à des entités définies respectivement au sein du Livre Blanc Téléradiologie ainsi qu’en section 2.2.2 de la présente étude. Par ailleurs, la notion de «Personne» peut recouvrir plusieurs personnes physiques, professionnels de santé en l’occurrence, dans le cas où un mécanisme de délégation est mis en oeuvre.

#### Processus collaboratif « Transmettre une demande d’examen d’imagerie »

<div class="figure" style="text-align: center;">
    <img src="F2_TransmissionDemande.png"
    alt="Processus collaboratif « Transmettre une demande d’examen d’imagerie »"
    title="F2_TransmissionDemande"
    style="width:6.3in;height:3.77778in">

    <p>
        Figure 2 : Processus collaboratif « Transmettre une demande d’examen d’imagerie »
    </p>
</div>

<table>
<caption style="caption-side: bottom;"><p>Table 1 : Définition du processus collaboratif « Transmettre une demande d'examen d'imagerie »</p></caption>
<colgroup>
<col style="width: 21%" />
<col style="width: 78%" />
</colgroup>
<thead>
<tr>
<th><strong>Service attendu</strong></th>
<th>Le Créateur transmet au Consommateur les éléments clés associés à une demande d'examen d'imagerie pour un patient.</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Pré-conditions</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Post-conditions</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Contraintes fonctionnelles</strong></td>
<td>Si la demande d’examen rédigée est connue (contexte de planification), en complément des éléments clés associés à la demande d'examen d'imagerie véhiculés dans la transaction, le Créateur initie au moins une transaction supplémentaire correspondant au document Demande d'examen d'imagerie complet (numérisé).</td>
</tr>
<tr>
<td><strong>Scénario nominal</strong></td>
<td>Le Créateur transmet une demande d’examen d’imagerie au Consommateur. Cette demande peut être accompagnée d’un ou plusieurs documents complémentaires.<br />
Le Consommateur réceptionne et analyse la demande d’examen d’imagerie. Si applicable, le consommateur prend également connaissance des informations portées le(s) document(s) annexes.</td>
</tr>
</tbody>
</table>

| **Acteur** | **Description** |
|----|----|
| Créateur | Le rôle de Créateur, incarné par le système RIS, est de transmettre une demande d’examen d’imagerie à destination du Consommateur. Cette interaction peut être complétée par un ou plusieurs documents annexes. |
| Consommateur | Le rôle de Consommateur, incarné par le SI de téléradiologie, est de recevoir la demande d’examen d’imagerie, qui peut être accompagnée d’un ou plusieurs documents associés. |

Table 2 : Définition des acteurs du processus « Transmettre une demande d'examen d'imagerie »

#### Processus collaboratif « Annuler une demande d’examen d’imagerie »

<div class="figure" style="text-align: center;">
    <img src="F3_AnnulationDemande.png"
    alt="Processus collaboratif « Annuler une demande d’examen d’imagerie »"
    title="F3_AnnulationDemande"
    style="width:6.05556in;height:3.78291in">

    <p>
        Figure 3 : Processus collaboratif « Annuler une demande d’examen d’imagerie »
    </p>
</div>

<table>
<caption style="caption-side: bottom;"><p>Table 3 : Définition du processus collaboratif « Annuler une demande d'examen d’imagerie »</p></caption>
<colgroup>
<col style="width: 21%" />
<col style="width: 78%" />
</colgroup>
<thead>
<tr>
<th><strong>Service attendu</strong></th>
<th>Le Créateur annule une demande d’examen d’imagerie envoyée préalablement au Consommateur.</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Pré-conditions</strong></td>
<td>L’envoi d’une annulation n’est possible qu’après l’envoi préalable d’une demande d’examen. Par ailleurs, une fois le processus « Transmettre un complément d’information post-examen » lancé, l’annulation de la demande n’est plus autorisée.</td>
</tr>
<tr>
<td><strong>Post-conditions</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Contraintes fonctionnelles</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Scénario nominal</strong></td>
<td>Le Créateur annule une demande d’examen d’imagerie transmise préalablement au Consommateur.<br />
Le Consommateur réceptionne l’annulation de la demande d’examen.</td>
</tr>
</tbody>
</table>

| **Acteur** | **Description** |
|----|----|
| Créateur | Le rôle de Créateur, incarné par le système RIS, est d’annuler une demande d’examen d’imagerie, transmise en amont au SI de téléradiologie. |
| Consommateur | Le rôle de Consommateur, incarné par le SI de téléradiologie, est de recevoir et acquitter l’annulation de la demande d’examen d’imagerie. |

Table 4 : Définition des acteurs du processus « Annuler une demande d’examen d’imagerie »

#### Processus collaboratif « Répondre à une demande d’examen d’imagerie »

<div class="figure" style="text-align: center;">
    <img src="F4_ReponseDemande.png"
    alt="Processus collaboratif « Répondre à une demande d’examen d’imagerie »"
    title="F4_ReponseDemande"
    style="width:6.30556in;height:3.01242in">

    <p>
        Figure 4 : Processus collaboratif « Répondre à une demande d’examen d’imagerie »
    </p>

</div>

<table>
<caption style="caption-side: bottom;"><p>Table 5 : Définition du processus collaboratif « Répondre à une demande d’examen d’imagerie »</p></caption>
<colgroup>
<col style="width: 21%" />
<col style="width: 78%" />
</colgroup>
<thead>
<tr>
<th><strong>Service attendu</strong></th>
<th>Le Créateur fournit une réponse métier à la demande d’examen d’imagerie précédemment reçue.<br />
Cette réponse formalise la décision prise concernant la demande (acceptation ou refus) et, en cas d’acceptation, inclut le protocole d’imagerie associé.</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Pré-conditions</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Post-conditions</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Contraintes fonctionnelles</strong></td>
<td><p>En cas d’acceptation de la demande :</p>
<p>La réponse doit comporter un indicateur d’acquittement positif signifiant l’acceptation de la demande, ainsi que le protocole d’examen élaboré par le médecin effecteur à distance.</p>
<p>En cas de refus de la demande :</p>
<p>La réponse doit comporter un indicateur de refus qui peut être accompagné de la nature du refus. Dans ce cas, aucun protocole n’est fourni.</p></td>
</tr>
<tr>
<td><strong>Scénario nominal</strong></td>
<td><p>Le Créateur fournit une réponse métier au Consommateur concernant la demande d’examen d’imagerie précédemment reçue.</p>
<p>Cette réponse indique la décision prise (acceptation ou refus).</p>
<p>En cas d’acceptation, elle inclut le protocole d’imagerie validé.</p>
<p>Le Consommateur réceptionne la réponse métier et en prend connaissance afin d’intégrer la décision et, si applicable, les informations portées par le protocole d’imagerie dans son environnement.</p></td>
</tr>
</tbody>
</table>

| **Acteur** | **Description** |
|----|----|
| Créateur | Le rôle de Créateur, incarné par le SI de téléradiologie, est de transmettre la réponse métier établi par le téléradiologue à destination du système RIS |
| Consommateur | Le rôle de Consommateur, incarné par le système RIS, est de recevoir la réponse métier à la demande d’examen d’imagerie. |

Table 6 : Définition des acteurs du processus « Répondre à une demande d’examen d’imagerie »

#### Processus collaboratif « Transmettre un complément d’information post-examen »

<div class="figure" style="text-align: center;">
    <img src="F5_TransmissionInfos.png"
    alt="Processus collaboratif « Transmettre un complément d’information post-examen »"
    title="F5_TransmissionInfos"
    style="width:6.3in;height:3.55368in">

    <p>
        Figure 5 : Processus collaboratif « Transmettre un complément d’information post-examen »
    </p>
</div>

<table>
<caption style="caption-side: bottom;"><p>Table 7 : Définition du processus collaboratif « Transmettre un complément d'information post-examen »</p></caption>
<colgroup>
<col style="width: 21%" />
<col style="width: 78%" />
</colgroup>
<thead>
<tr>
<th><strong>Service attendu</strong></th>
<th>Le Créateur transmet un complément d’information au Consommateur suite à la réalisation du ou des actes d’imagerie.</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Pré-conditions</strong></td>
<td>Réalisation du ou des actes d’imagerie au sein de la structure d’imagerie.</td>
</tr>
<tr>
<td><strong>Post-conditions</strong></td>
<td>Mise à disposition des images médicales produites.</td>
</tr>
<tr>
<td><strong>Contraintes fonctionnelles</strong></td>
<td>N/A</td>
</tr>
<tr>
<td><strong>Scénario nominal</strong></td>
<td>Le Créateur transmet un complément d’information suite à la réalisation du ou des actes au Consommateur.<br />
Le Consommateur réceptionne ces informations et en prend connaissance.</td>
</tr>
</tbody>
</table>

| **Acteur** | **Description** |
|----|----|
| Créateur | Le rôle de Créateur, incarné par le système RIS, est de transmettre un complément d’information à destination de la plateforme de téléradiologie suite à la réalisation du ou des actes d’imagerie au sein de la structure d’imagerie. |
| Consommateur | Le rôle de Consommateur, incarné par le SI de téléradiologie, est de recevoir le complément d’information. |

Table 8 : Définition des acteurs du processus « Transmettre un complément d’information post-examen »

### Description des processus collaboratifs et identification des flux

Les actions et flux associés aux différents processus collaboratifs retenus dans le périmètre de la présente étude seront décrits au sein de ce chapitre au moyen de diagrammes d’activité.

#### Transmettre une demande d’examen d’imagerie

Ce processus constitue le point d’entrée du workflow lié à la pratique de la téléradiologie. Il décrit la transmission d’une demande d’examen d’imagerie, depuis le système RIS associé à la structure d’imagerie, vers un SI de de téléradiologie.

Le diagramme d’activité ci-dessous illustre les actions de création, d’envoi et de réception de la demande d’examen d’imagerie, ainsi que les flux qui leur sont associés entre les acteurs impliqués.

<div class="figure" style="text-align: center;">
    <img src="F6_Flux1Activity.png"
    alt="Processus collaboratif « Transmettre une demande d'examen d'imagerie »"
    title="F6_Flux1Activity"
    style="width:5.2631in;height:3.11043in">

    <p>
        Figure 6 : Processus collaboratif « Transmettre une demande d'examen d'imagerie »
    </p>
</div>

##### Description des actions

| **Action** | **Description** |
|----|----|
| Créer une demande d’examen d’imagerie | Le Créateur génère une demande d’examen d’imagerie. |
| Transmettre la demande d’examen d’imagerie | Le Créateur transmet au Consommateur la demande d’examen d’imagerie. |
| Recevoir la demande d’examen d’imagerie | Le Consommateur reçoit la demande d’examen d’imagerie. |

Table 9 : Description des actions

##### Identification des flux

| **Flux** | **Processus** | **Emetteur** | **Récepteur** | **Obligatoire** |
|:--:|:--:|:--:|:--:|:--:|
| Flux 1 - TransmissionDemandeIMG | Transmettre une demande d’examen d’imagerie | Créateur | Consommateur | Oui |

Table 10 : Identification des flux

#### Annuler une demande d’examen d’imagerie

Ce processus permet au système RIS d’informer la plateforme de téléradiologie de l’annulation d’une demande d’examen d’imagerie précédemment transmise.

Le diagramme d’activité ci-dessous illustre l’action de transmission de l’annulation d’une demande d’examen d’imagerie, ainsi que le flux associé entre les acteurs impliqués.

<div class="figure" style="text-align: center;">
    <img src="F7_Flux2Activity.png"
    alt="Processus collaboratif « Annuler une demande d'examen d'imagerie »"
    title="F7_Flux2Activity"
    style="width:5.50647in;height:3.25426in">

    <p>
        Figure 7 : Processus collaboratif « Annuler une demande d'examen d'imagerie »
    </p>
</div>

##### Description des actions

| **Action** | **Description** |
|----|----|
| Créer une annulation d’une demande d’examen d’imagerie | Le Créateur génère une annulation de demande d’examen d’imagerie. |
| Transmettre l’annulation de la demande d’examen d’imagerie | Le Créateur transmet l’annulation de la demande d’examen d’imagerie. |
| Recevoir l’annulation de la demande d’examen d’imagerie | Le Consommateur reçoit l’annulation de la demande d’examen d’imagerie. |

Table 11 : Description des actions

##### Identification des flux

| **Flux** | **Processus** | **Emetteur** | **Récepteur** | **Obligatoire** |
|:--:|:--:|:--:|:--:|:--:|
| Flux 2 - AnnulationDemandeIMG | Annuler une demande d’examen d’imagerie | Créateur | Consommateur | Non |

Table 12 : Identification des flux

#### Répondre à une demande d’examen d’imagerie

Ce processus intervient à la suite de la réception et de l’analyse d’une demande d’examen d’imagerie par la plateforme de téléradiologie. Il décrit la fourniture d’une réponse métier au système RIS demandeur, précisant la décision prise concernant la demande (acceptation ou refus) et, en cas d’acceptation, le protocole d’imagerie adapté pour la réalisation de l’examen.

Le diagramme d’activité ci-dessous illustre les différentes actions réalisées dans le cadre du processus de fourniture d’une réponse métier à une demande d’examen d’imagerie.  
Il décrit les étapes de décision (acceptation ou refus de la demande), la préparation de la réponse correspondante, sa transmission ainsi que le flux associé entre les acteurs impliqués.

<div class="figure" style="text-align: center;">
    <img src="F8_Flux3Activity.png"
    alt="Processus collaboratif « Répondre à une demande d’examen d’imagerie »"
    title="F8_Flux3Activity"
    style="width:5.27779in;height:4.85776in">

    <p>
        Figure 8 : Processus collaboratif « Répondre à une demande d’examen d’imagerie »
    </p>
</div>

##### Description des actions

| **Action** | **Description** |
|----|----|
| Etablir le protocole d’imagerie | Le créateur établi le protocole d’imagerie. |
| Générer la réponse métier à la demande | Le créateur génère la réponse métier à la demande qui peut contenir un protocole d’imagerie. |
| Transmettre la réponse métier à la demande | Le créateur transmet la réponse métier à la demande d’examen d’imagerie. |
| Recevoir la réponse métier à la demande | Le consommateur reçoit la réponse métier à la demande d’examen d’imagerie. |

Table 13 : Description des actions

##### Identification des flux

| **Flux** | **Processus** | **Emetteur** | **Récepteur** | **Obligatoire** |
|:--:|:--:|:--:|:--:|:--:|
| Flux 3 - ReponseDemandeIMG | Répondre à une demande d’examen d’imagerie | Créateur | Consommateur | Oui |

Table 14 : Identification des flux

#### Transmettre un complément d’information post-examen

Ce processus intervient suite à la réalisation de l’examen d’imagerie basé sur le protocole préalablement réceptionné. Il permet de transmettre au SI de téléradiologie un ensemble d’informations complémentaires nécessaires à la production du compte rendu d’imagerie.

Le diagramme d’activité ci-dessous illustre l’action de transmission des informations complémentaires suite à la réalisation du ou des actes d’imagerie, ainsi que le flux associé entre les acteurs impliqués

<div class="figure" style="text-align: center;">
    <img src="F9_Flux4Activity.png"
    alt="Processus collaboratif « Transmettre un complément d’information post-examen »"
    title="F9_Flux4Activity"
    style="width:5.12032in;height:4.00219in">

    <p>
        Figure 9 : Processus collaboratif « Transmettre un complément d’information post-examen »
    </p>
</div>

##### Description des actions

| **Action** | **Description** |
|----|----|
| Réaliser le ou les actes d’imagerie | Le créateur réalise le ou les actes d’imagerie. |
| Générer un complément d’information post-examen | Le créateur génère un complément d’information suite à la réalisation du ou des actes d’imagerie. |
| Transmettre un complément d’information post-examen | Le créateur transmet au consommateur un complément d’information suite à la réalisation du ou des actes d’imagerie. |
| Recevoir un complément d’information post-examen. | Le consommateur reçoit le complément d’information suite à la réalisation du ou des actes d’imagerie. |

Table 15 : Description des actions

##### Identification des flux

| **Flux** | **Processus** | **Emetteur** | **Récepteur** | **Obligatoire** |
|:--:|:--:|:--:|:--:|:--:|
| Flux 4 - TransmissionComplementIMG | Transmettre un complément d’information post-examen | Créateur | Consommateur | Oui |

Table 16 : Identification des flux

#### Synthèse des flux d’informations

| **Flux** | **Processus** | **Emetteur** | **Récepteur** | **Obligatoire** |
|----|----|----|----|----|
| Flux 1 - TransmissionDemandeIMG | Transmettre une demande d’examen d’imagerie | Créateur | Consommateur | Oui |
| Flux 2 - AnnulationDemandeIMG | Annuler une demande d’examen d’imagerie | Créateur | Consommateur | Non |
| Flux 3 - ReponseDemandeIMG | Fournir une réponse métier à la demande d’examen d’imagerie | Créateur | Consommateur | Oui |
| Flux 4 - TransmissionComplementIMG | Transmettre un complément d’information post-examen | Créateur | Consommateur | Oui |

Table 17 : Synthèse des flux

### Identification des concepts véhiculés dans les flux d’informations et correspondance avec les classes et attributs du MOS

#### Concepts métier – Factorisation par concept

<table>
<caption style="caption-side: bottom;"><p>Table 18 : Concepts métier – Factorisation par Concepts</p></caption>
<colgroup>
<col style="width: 32%" />
<col style="width: 56%" />
<col style="width: 10%" />
</colgroup>
<thead>
<tr>
<th><strong>Concept</strong></th>
<th><strong>Description</strong></th>
<th><strong>Flux</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Patient</td>
<td>Personne physique bénéficiaire de l’acte d’imagerie. Le patient est caractérisé par l’intégralité des traits INS (voir le <a href="https://industriels.esante.gouv.fr/sites/default/files/media/document/ANS_Referentiel_Identite-Nationaled-de-Sante_V2.1.pdf">référentiel ANS de l’INS</a>).</td>
<td>Flux 1, 2, 3, 4</td>
</tr>
<tr>
<td>PSResponsable</td>
<td><p>Professionnel de santé de la structure d’imagerie qui accueille le patient et supervise la réalisation de l’acte d’imagerie. Le PSResponsable est caractérisé par les éléments suivants :</p>
<ul>
<li><p>Horodatage de la participation de l’auteur</p></li>
<li><p>Identifiant PS_IdNat</p></li>
<li><p>Code profession</p></li>
<li><p>Nom du professionnel</p></li>
<li><p>Point de contact du professionnel</p></li>
<li><p>Identifiant Struct_IdNat de la structure associée au PS</p></li>
<li><p>Nom de la structure associée au PS</p></li>
</ul></td>
<td>Flux 1, 2</td>
</tr>
<tr>
<td>PSEffecteur</td>
<td><p>Médecin effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie. Il interprète et communique les résultats suite à la réalisation de l’acte d’imagerie, réalise le CR d’imagerie (dont il est l’auteur) et le transmet à la structure d'imagerie qui accueille le patient. Le PSEffecteur est caractérisé par les éléments suivants :</p>
<ul>
<li><p>Horodatage de la participation de l’auteur</p></li>
<li><p>Identifiant PS_IdNat</p></li>
<li><p>Code profession</p></li>
<li><p>Point de contact du professionnel</p></li>
<li><p>Nom du professionnel</p></li>
<li><p>Identifiant Struct_IdNat de la structure associée au PS</p></li>
<li><p>Nom de la structure associée au PS</p></li>
</ul></td>
<td>Flux 3</td>
</tr>
<tr>
<td>IdentifiantDemandeExamen</td>
<td>Order Placer Number. Identifiant de la Demande d’examen d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie. Cet attribut est composé d’un élément relatif à l'autorité d'affectation et d’un élément représentant l’identifiant distribué par cette autorité.</td>
<td>Flux 1, 2, 3, 4</td>
</tr>
<tr>
<td>StructureImagerie</td>
<td><p>Établissement ou entité organisationnelle disposant d’un parc d’équipements permettant la réalisation d’actes d’imagerie médicale (cabinet, service hospitalier, centre d’imagerie). Le concept StructureImagerie est caractérisé par les éléments suivants :</p>
<ul>
<li><p>Identifiant Struct_IdNat de la structure</p></li>
<li><p>Dénomination de la structure</p></li>
</ul></td>
<td>Flux 1, 2, 3, 4</td>
</tr>
<tr>
<td>PlateformeTeleradiologie</td>
<td>Désigne l’ensemble organisationnel et technique de la plateforme de téléradiologie. Elle regroupe les informations relatives à la structure de téléradiologie (entité opératrice) ainsi qu’au SI de téléradiologie (système applicatif sous-jacent).</td>
<td>Flux 1, 2, 3, 4</td>
</tr>
<tr>
<td>NatureDemande</td>
<td>Statut de la demande d’examen (Nouvelle demande ou annulation d’une demande).</td>
<td>Flux 1, 2</td>
</tr>
<tr>
<td>DateDemande</td>
<td>Date et heure associées à la rédaction de la demande d’examen d’imagerie.</td>
<td>Flux 1</td>
</tr>
<tr>
<td>IdentifiantRDV</td>
<td>Identifie le rendez-vous du patient associé à la réalisation de l’acte d’imagerie et permet de faire le lien entre la demande d’examen et la gestion des rendez-vous au sein de l’établissement d’accueil du patient.</td>
<td>Flux 1, 4</td>
</tr>
<tr>
<td>DateHeurePriseCharge</td>
<td>Date et heure correspondant à une prise en charge du patient/usager par un professionnel ou par une structure.</td>
<td>Flux 1</td>
</tr>
<tr>
<td>JustificationDemande</td>
<td>Éléments de contexte pertinents tels que les indications ; les symptômes ; les signes cliniques.</td>
<td>Flux 1</td>
</tr>
<tr>
<td>Antecedents</td>
<td>Description des antécédents médicaux relatifs au patient et pertinents dans le cadre de sa prise en charge.</td>
<td>Flux 1</td>
</tr>
<tr>
<td>MotifAnnulation</td>
<td>Motif d’annulation de la demande d’examen d’imagerie.</td>
<td>Flux 2</td>
</tr>
<tr>
<td>MotifRefus</td>
<td>Motif du refus de la demande d’examen d’imagerie par le médecin effecteur.</td>
<td>Flux 3</td>
</tr>
<tr>
<td>DocumentDemandeExamen</td>
<td>Document correspondant à la demande d’examen d’imagerie rédigée.</td>
<td>Flux 1</td>
</tr>
<tr>
<td>DocumentsTiers</td>
<td>Documents complémentaires associés à la demande d’examen d’imagerie.</td>
<td>Flux 1</td>
</tr>
<tr>
<td>LocalisationAnatomique</td>
<td>Localisation anatomique examinée dans le cadre de l’acte d’imagerie. Une ou plusieurs régions anatomiques peuvent être ciblées.</td>
<td>Flux 1, 4</td>
</tr>
<tr>
<td>ModaliteImagerie</td>
<td>Modalité d’imagerie utilisée ou prévue pour réaliser l’examen. Code issu du JDV_modalitedemandeActeImagerie-CISIS (1.2.250.1.213.1.1.5.660).</td>
<td>Flux 1, 4</td>
</tr>
<tr>
<td>DecisionEffecteur</td>
<td>Décision rendue par le médecin effecteur après analyse de la demande d’examen d’imagerie, indiquant si celle-ci est acceptée ou refusée.</td>
<td>Flux 3</td>
</tr>
<tr>
<td>ProtocoleImagerie</td>
<td>Document définissant les conditions de réalisation de l’examen d’imagerie.</td>
<td>Flux 3</td>
</tr>
<tr>
<td>URLViewerDRIMBOX</td>
<td>Eléments permettant la construction d’une URL d’accès à la visionneuse DICOM implémentée par une solution DRIMBox associée au système RIS. Une fois l’URL assemblée, celle-ci doit être mentionnée au sein du compte-rendu d’imagerie. Ce concept permet l’intégration au maillage DRIM-M du compte-rendu d’imagerie rédigé suite à la réalisation de l’acte d’imagerie.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>DuréeRétentionImages</td>
<td>Durée de rétention propre à l’archive impliquée concernant les images médicales associées à l’acte d’imagerie effectué. Cette information doit apparaître explicitement au sein du compte-rendu d’imagerie.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>DateRéalisationExamen</td>
<td>Date et heure correspondant à la réalisation de l’acte d’imagerie.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>IdentificationMatériel</td>
<td>Identification du matériel utilisé pour les techniques les plus irradiantes : radiologie interventionnelle, scanographie et radiothérapie.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>ProduitsAdministres</td>
<td>Regroupe l’ensemble des produits administrés au patient dans le cadre de la réalisation de l’examen d’imagerie. Il permet d’identifier chaque produit utilisé, ses modalités d’administration et toute information pertinente liée à son usage lors de l’examen.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>AccessionNumber</td>
<td>Accession Number. Identifiant de la procédure d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie. Cet attribut est composé d’un élément relatif à l'autorité d'affectation et d’un élément représentant l’identifiant distribué par cette autorité.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>StudyInstanceUID</td>
<td>StudyInstanceUID. Identifiant de l’examen d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie.</td>
<td>Flux 4</td>
</tr>
<tr>
<td>codeEvenement</td>
<td><p>Code de l’évènement correspondant à l’acte d’imagerie réalisé.</p>
<p>Doit être présent : Code(s) LOINC issu(s) du jdv-code-document-imagerie-cisis (1.2.250.1.213.1.1.5.687)</p>
<p>Peut être présent : Code(s) CCAM de l’acte d’imagerie</p></td>
<td>Flux 4</td>
</tr>
<tr>
<td>roleProfessionnel</td>
<td>Indique le rôle joué par le professionnel dans le cadre des échanges de téléradiologie.</td>
<td>Flux 1, 2, 3</td>
</tr>
</tbody>
</table>

#### Mise en équivalence MOS

Au travers de ce chapitre une mise en correspondance sera effectuée entre les concepts métier précédemment présentés et les concepts issus du modèle des objets de santé (MOS). L’objectif du MOS étant de définir un ensemble de concepts, décrits de manière homogène et neutre vis-à-vis des technologies, et d’offrir une description commune et mutualisée des informations traitées par les systèmes d’information. Le MOS peut être consulté à l’adresse suivante : <https://mos.esante.gouv.fr/0.html>.

Le tableau présenté ci-dessous contient les éléments suivants :

- Concept métier identifié au sein de la section 2.7.1 du présent document ;

- Concept(s) MOS correspondant avec la relation liant le concept métier au concept MOS. La relation peut être de trois types : " extension ", " restriction " ou " équivalence ". Dans le cas où l’association entre le concept métier et le concept MOS n’est pas applicable, cela sera également signalé au moyen d’un trait diagonal.

<table style="width:100%;">
<caption style="caption-side: bottom;"><p>Table 19 : Mise en équivalence MOS</p></caption>
<colgroup>
<col style="width: 31%" />
<col style="width: 21%" />
<col style="width: 24%" />
<col style="width: 22%" />
</colgroup>
<thead>
<tr>
<th><strong>Concept</strong></th>
<th><strong>Extension</strong></th>
<th><strong>Restriction</strong></th>
<th><strong>Equivalence</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Patient</td>
<td>PersonnePhysique</td>
<td><p>PersonnePriseCharge</p>
<p>PersonnePhysique</p></td>
<td></td>
</tr>
<tr>
<td>PSResponsable</td>
<td></td>
<td><p>Professionnel</p>
<p>ExerciceProfessionnel</p></td>
<td></td>
</tr>
<tr>
<td>PSEffecteur</td>
<td></td>
<td><p>Professionnel</p>
<p>ExerciceProfessionnel</p></td>
<td></td>
</tr>
<tr>
<td>IdentifiantDemandeExamen</td>
<td></td>
<td></td>
<td>identifiantDemande</td>
</tr>
<tr>
<td>StructureImagerie</td>
<td></td>
<td>EntiteGeographique</td>
<td></td>
</tr>
<tr>
<td>PlateformeTeleradiologie</td>
<td></td>
<td>EntiteGeographique</td>
<td></td>
</tr>
<tr>
<td>NatureDemande</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>DateDemande</td>
<td></td>
<td></td>
<td>dateDemande</td>
</tr>
<tr>
<td>IdentifiantRDV</td>
<td></td>
<td></td>
<td>idRdv</td>
</tr>
<tr>
<td>DateHeurePriseCharge</td>
<td></td>
<td></td>
<td><p>datePriseRdv</p>
<p>dateDebutRdv</p></td>
</tr>
<tr>
<td>JustificationDemande</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Antecedents</td>
<td>NoteLiaison</td>
<td></td>
<td></td>
</tr>
<tr>
<td>MotifAnnulation</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>MotifRefus</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>DocumentDemandeExamen</td>
<td>Document</td>
<td></td>
<td>typeDocument</td>
</tr>
<tr>
<td>DcoumentsTiers</td>
<td>Document</td>
<td></td>
<td></td>
</tr>
<tr>
<td>LocalisationAnatomique</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>ModaliteImagerie</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>DecisionEffecteur</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>ProtocoleImagerie</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>URLViewerDRIMBOX</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>DuréeRétentionImages</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>DateRéalisationExamen</td>
<td></td>
<td></td>
<td>DateHeure</td>
</tr>
<tr>
<td>IdentificationMatériel</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>ProduitsAdministres</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>AccessionNumber</td>
<td></td>
<td></td>
<td>Identifiant</td>
</tr>
<tr>
<td>StudyInstanceUID</td>
<td></td>
<td></td>
<td>Identifiant</td>
</tr>
<tr>
<td>modaliteImagerie</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>codeEvenement</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>roleProfessionnel</td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Modélisation des flux d’informations

#### Flux 1 – TransmissionDemandeIMG

<div class="figure" style="text-align: center;">
    <img src="F10_Classes-Flux1.png"
    alt="TransmissionDemandeIMG"
    title="F10_Classes-Flux1"
    style="width:6.37865in;height:4.80719in">

    <p>
        Figure 10 : Flux 1 – TransmissionDemandeIMG
    </p>
</div>

##### Classe DemandeExamenImagerie

Représente l’ensemble des informations nécessaires pour formaliser la demande de réalisation d’un examen d’imagerie. Regroupe les éléments cliniques, administratifs et organisationnels transmis par le prescripteur afin de justifier l’examen et de permettre au médecin effecteur d’en évaluer la pertinence et la faisabilité.

| **Nom** | **Description** |
|----|----|
| identifiantDemande : \[1..1\] Identifiant | Order Placer Number. Identifiant de la Demande d’examen d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie. Cet attribut est composé d’un élément relatif à l'autorité d'affectation et d’un élément représentant l’identifiant distribué par cette autorité. |
| dateDemande : Date \[1..1\] | Date à laquelle la demande a été réalisée. |
| natureDemande : Code \[1..1\] | Nature de la demande d’examen (Nouvelle demande ou annulation d’une demande). |
| JustificationDemande : Texte \[1..1\] | Éléments de contexte pertinents tels que les indications, les symptômes, l’historique clinique. |
| finaliteExamen : Texte \[0..1\] | Question posée à travers la demande. |

Table 20 : Attributs de la classe « DemandeExamenImagerie »

##### Classe DocumentDemande

Document formalisant la demande d’examen d’imagerie.

| **Nom** | **Description** |
|----|----|
| document : ObjetBinaire \[1..1\] | Demande d’examen d’imagerie rédigée. |
| typeDocument : Code \[1..1\] | Type de document. Code issu du JDV_J07_XdsTypeCode_CISIS (1.2.250.1.213.1.1.5.471). |

Table 21 : Attributs de la classe « DocumentDemande »

##### Classe DocumentTiers

Documents complémentaires associés à la demande d’examen. Représente tout élément additionnel utile à l’évaluation ou à la prise en charge du patient, tels que des comptes rendus, résultats, justificatifs ou documents cliniques pertinents.

| **Nom** | **Description** |
|----|----|
| document : ObjetBinaire \[1..1\] | Document additionnel utile à l’évaluation ou à la prise en charge du patient. |
| typeDocument : code \[1..1\] | Type de document. Code issu du JDV_J07_XdsTypeCode_CISIS (1.2.250.1.213.1.1.5.471). |

Table 22 : Attributs de la classe « DocumenTiers »

##### Classe RendezVous

Représente la rencontre planifiée entre le patient et la structure d’imagerie pour la réalisation de l’examen d’imagerie.

| **Nom** | **Description** |
|----|----|
| idRdv : Identifiant \[1..1\] | Identifiant du rendez-vous du patient associé à la réalisation de l’acte ou des actes d’imagerie. |
| datePriseRdv : DateHeure \[0..1\] | Date de la prise de rendez-vous. |
| dateDebutRdv : DateHeure \[0..1\] | Date de début du rendez-vous. |

Table 23 : Attributs de la classe « RendezVous »

##### Classe PersonnePriseCharge

Personne physique bénéficiaire de soins, d’examens, d’actes de prévention ou de services.

<table>
<caption style="caption-side: bottom;"><p>Table 24 : Attributs de la classe « PersonnePriseCharge »</p></caption>
<colgroup>
<col style="width: 31%" />
<col style="width: 68%" />
</colgroup>
<thead>
<tr>
<th><strong>Nom</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>INS : INS [1..1]</td>
<td><p>L'INS référence les données de santé et se compose des éléments suivants :</p>
<ul>
<li><p>Un matricule INS : le numéro d’inscription au répertoire national d’identification des personnes physiques (NIR) ou le numéro identifiant d’attente (NIA) pour les personnes en instance d’attribution d’un NIR (Art. R. 1111-8-1.-I du CSP)</p></li>
<li><p>Des traits d'identité de l'état civil : nom de naissance, prénom (liste des prénoms de naissance), date de naissance, sexe et lieu de naissance ;</p></li>
<li><p>Des traits complémentaires provenant du Référentiel National d'IdentitoVigilance (RNIV) : premier prénom de l'acte de naissance, prénom utilisé et nom utilisé.</p></li>
</ul></td>
</tr>
</tbody>
</table>

##### Classe PersonnePhysique

Informations de la personne physique disjointes des informations constituant l'identité INS.

| **Nom** | **Description** |
|----|----|
| tailleCorporelle : Mesure \[0..1\] | Taille du corps de la personne exprimée dans une unité de mesure explicite (m, cm, etc.). Synonymes : grandeur corporelle, grandeur du corps, hauteur corporelle, hauteur du corps, longueur corporelle. |
| poidsCorporel : Mesure \[0..1\] | Masse du corps de la personne exprimée dans une unité de mesure explicite (kg, g, etc.). |
| statutGrossesse : Code \[0..1\] | Indique si la personne est enceinte ou non, sur la base des informations disponibles ou déclarées. Cet attribut permet de préciser la présence, l’absence ou l’absence d’information concernant une éventuelle grossesse. Code issu du JDV_StatutGrossesse_CISIS (1.2.250.1.213.1.1.5.671). |

Table 25 : Attributs de la classe « PersonnePhysique »

##### Classe ModaliteImagerie

En fonction du contexte, décrit le type de modalité d’imagerie utilisée ou prévue pour réaliser l’examen.

| **Nom** | **Description** |
|----|----|
| modaliteImagerie : Code \[1..1\] | Modalité d’imagerie utilisée ou prévue pour réaliser l’examen. Code issu du JDV_modalitedemandeActeImagerie-CISIS (1.2.250.1.213.1.1.5.660). |
| commentaire : Texte \[0..1\] | Commentaire facultatif pour apporter des précisions sur la modalité d’imagerie sollicitée. |

Table 26 : Attributs de la classe « ModaliteImagerie »

##### Classe LocalisationAnatomique

Décrit la ou les régions du corps concernées par un examen d’imagerie. En fonction du contexte, peut représenter à la fois les zones effectivement examinées et les localisations demandées par le prescripteur.

| **Nom** | **Description** |
|----|----|
| localisationAnatomique : Code \[1..1\] | Localisation anatomique examinée dans le cadre de l’examen d’imagerie. Code issu du JDV_RegionAnatomique -CISIS (1.2.250.1.213.1.1.5.695). |
| precisionTopographique : Code \[0..1\] | En complément de la localisation anatomique, une précision topographique peut être associée à la localisation anatomique. Code issu du JDV_ModificateurTopographique-CISIS (1.2.250.1.213.1.1.5.688). |

Table 27 : Attributs de la classe « Attributs de la classe « LocalisationAnatomique »

##### Classe Antecedents

Ensemble d’informations relatives aux antécédents médicaux significatifs concernant le patient pris en charge.

| **Nom** | **Description** |
|----|----|
| description : Texte \[1..1\] | Exposé de l’antécédent médical concernant le patient pris en charge. |
| pertinenceAntecedent : Indicateur \[0..1\] | Détermine le degré d’importance applicable à la prise en compte de l’antécédent médical. |

##### Classe Professionnel

Personnel médical qui participe à la prise en charge du patient. Représente aussi bien le professionnel de santé responsable au sein de la structure d’imagerie que le médecin effecteur à distance (téléradiologue), chacun contribuant à l’organisation, la réalisation ou l’interprétation de l’examen d’imagerie.

| **Nom** | **Description** |
|----|----|
| idNat_PS : Identifiant \[1..1\]  | Identification nationale principale du professionnel. Cette identification est obtenue par la concaténation du type d'identifiant national de personne (provenant de la nomenclature CodeSystem-TRE-G08-TypeIdentifiantPersonne) et de l'identifiant de la personne physique provenant, selon le type d’identifiant, soit d’un référentiel national, soit d’un référentiel local propre à la structure d’exercice de la personne physique. Voir [Modèle des objets de santé (MOS) – idNat_PS](https://mos.esante.gouv.fr/2.html#_48b9384f-52ff-4000-b466-fdb3040ca703). |
| roleProfessionnel : Code \[1..1\] | Indique le rôle joué par le professionnel dans le cadre des échanges de téléradiologie. Permet de distinguer s’il s’agit du professionnel de santé demandeur ou du professionnel de santé effecteur. |
| telecommunication : Telecommunication \[0..\*\] | Adresse(s) de télécommunication du professionnel (numéro de téléphone, adresse email, URL, etc.). |

Table  : Attributs de la classe « Professionnel »

##### Classe ExerciceProfessionnel

Informations décrivant notamment la profession exercée, l’identité d’exercice d’un professionnel et le cadre de son exercice (civil, militaire, etc.).

| **Nom** | **Description** |
|----|----|
| civiliteExercice : Code \[0..1\] | Civilité d’exercice du professionnel. |
| nomExercice :Texte \[1..1\] | Nom sous lequel exerce le professionnel. |
| prenomExercice : Texte \[0..1\]  | Prénom sous lequel exerce le professionnel. |
| profession : Code \[1..1\]  | Profession exercée ou future profession de l'étudiant. Code issu du JDV_J01_XdsAuthorSpecialty_CISIS (1.2.250.1.213.1.1.5.461). |

Table 28 : Attributs de la classe « ExerciceProfessionnel »

##### Classe Structure

Représente une entité organisationnelle. En fonction du contexte, peut correspondre à la structure d’imagerie accueillant le patient ou à la plateforme de téléradiologie opérant à distance. La classe Structure regroupe les informations nécessaires pour identifier l’organisation.

| **Nom** | **Description** |
|----|----|
| idNat_struct : Identifiant \[1..1\] | Identification nationale de l'Entité initiée pour les besoins du SI-CPS. Cette identification est obtenue par la concaténation du type d'identifiant national de structure (provenant de la nomenclature CodeSystem-TRE-G07-TypeIdentifiantStructure) et de l'identifiant de la structure. Voir [Modèle des objets de santé (MOS) – idNat_struct](https://mos.esante.gouv.fr/4.html#_86304fbf-ab15-4640-993a-242c61794854) |
| denominationStructure : Texte \[1..1\] | Nom sous lequel l’entité exerce son activité. Dans le cas d'un établissement enregistré dans le FINESS, cet attribut correspond à la notion de "raison sociale d'un établissement" renseignée dans le FINESS. |

Table 29 : Attributs de la classe « Structure »

##### Classe SystemeInformation

Décrit les caractéristiques du système d’information utilisé par une structure pour émettre ou recevoir des flux. Permet d’identifier et de qualifier l’application ou le service impliqué dans l’échange, qu’il s’agisse du système expéditeur ou du système destinataire du flux concerné.

| **Nom**                          | **Description**        |
|----------------------------------|------------------------|
| nomApplication : Texte \[1..1\]  | Nom de l’application.  |
| nomOrganisation : Texte \[1..1\] | Nom de l’organisation. |

Table 30 : Attributs de la classe « SystemeInformation »

#### Flux 2 – AnnulationDemandeIMG

<div class="figure" style="text-align: center;">
    <img src="F11_Classes-Flux2.png"
    alt="AnnulationDemandeIMG"
    title="F11_Classes-Flux2"
    style="width:6.20976in;height:3.9013in">

    <p>
        Figure 11 : Flux 2 – AnnulationDemandeIMG
    </p>
</div>

##### Classe AnnulationExamenImagerie

Représente l’ensemble des informations nécessaires pour formaliser l’annulation d’une demande d’examen préalablement transmise.

| **Nom** | **Description** |
|----|----|
| identifiantDemande : \[1..1\] Identifiant | Order Placer Number. Identifiant de la Demande d’examen d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie. Cet attribut est composé d’un élément relatif à l'autorité d'affectation et d’un élément représentant l’identifiant distribué par cette autorité. |
| natureDemande : Code \[1..1\] | Nature de la demande d’examen (Nouvelle demande ou annulation d’une demande). |
| motifAnnulation : Texte \[0..1\] | Motif d’annulation de la demande d’examen d’imagerie. |

Table 31 : Attributs de la classe « AnnulationExamenImagerie »

##### Classe PersonnePriseCharge

Cf [2.1.8.1.5](#classe-personneprisecharge)

##### Classe Professionnel

Cf [2.1.8.1.10](#classe-professionnel)

##### Classe ExerciceProfessionnel

Cf [2.1.8.1.11](#classe-exerciceprofessionnel)

##### Classe Structure

Cf [2.1.8.1.12](#classe-structure)

##### Classe SystemeInformation

Cf [2.1.8.1.13](#classe-systemeinformation)

#### Flux 3 – ReponseDemandeIMG

<div class="figure" style="text-align: center;">
    <img src="F12_Classes-Flux3.png"
    alt="ReponseDemandeIMG"
    title="F12_Classes-Flux3"
    style="width:6.29266in;height:4.5106in">

    <p>
        Figure 12 : Flux 3 – ReponseDemandeIMG
    </p>
</div>

##### Classe ReponseDemandeImagerie

Représente les informations constituant la réponse du médecin effecteur à une demande d’examen d’imagerie préalablement transmise.

| **Nom** | **Description** |
|----|----|
| identifiantDemande : Identifiant \[1..1\] | Order Placer Number. Identifiant de la Demande d’examen d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie. Cet attribut est composé d’un élément relatif à l'autorité d'affectation et d’un élément représentant l’identifiant distribué par cette autorité. |
| decisionEffecteur : Booléen \[1..1\] | Décision rendue par le médecin effecteur après analyse de la demande d’examen d’imagerie, indiquant si celle-ci est acceptée ou refusée. |
| motifRefus : Texte \[0..1\] | Si la demande est refusée par le médecin effecteur, permet de renseigner le motif du refus. |

Table 32 : Attributs de la classe « ReponseDemandeImagerie »

##### Classe ProtocoleImagerie

Représente le protocole d’imagerie élaboré par le médecin effecteur.

| **Nom** | **Description** |
|----|----|
| protocole : Texte \[1..1\] | Document définissant les conditions de réalisation de l’examen d’imagerie. |

Table 33 : Attributs de la classe « ProtocoleImagerie »

##### Classe PersonnePriseCharge

Cf [2.1.8.1.5](#classe-personneprisecharge)

##### Classe Professionnel

Cf [2.1.8.1.10](#classe-professionnel)

##### Classe ExerciceProfessionnel

Cf [2.1.8.1.11](#classe-exerciceprofessionnel)

##### Classe Structure

Cf [2.1.8.1.12](#classe-structure)

##### Classe SystemeInformation

Cf [2.1.8.1.13](#classe-systemeinformation)

#### Flux 4 – TransmissionComplementIMG

<div class="figure" style="text-align: center;">
    <img src="F13_Classes-Flux4.png"
    alt="TransmissionComplementIMG"
    title="F13_Classes-Flux4"
    style="width:6.42807in;height:3.72964in">

    <p>
        Figure 13  : Flux 4 – TransmissionComplementIMG
    </p>
</div>

##### Classe ExamenImagerie

Regroupe l’ensemble des informations permettant d’identifier un examen d’imagerie réalisé.

<table>
<caption style="caption-side: bottom;"><p>Table 34 : Attributs de la classe « ExamenImagerie »</p></caption>
<colgroup>
<col style="width: 43%" />
<col style="width: 56%" />
</colgroup>
<thead>
<tr>
<th><strong>Nom</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>studyInstanceUID : Identifiant [1..1]</td>
<td>StudyInstanceUID. Identifiant de l’examen d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie.</td>
</tr>
<tr>
<td>accessionNumber : Identifiant [1..1]</td>
<td>Accession Number. Identifiant de la procédure d’imagerie, attribué par le système RIS hébergé au sein de la structure d’imagerie. Cet attribut est composé d’un élément relatif à l'autorité d'affectation et d’un élément représentant l’identifiant distribué par cette autorité.</td>
</tr>
<tr>
<td>dateExamenImagerie : DateHeure [1..1]</td>
<td>Date et heure correspondant à la réalisation de l’examen d’imagerie.</td>
</tr>
<tr>
<td>codeEvenement : Code [1..1]</td>
<td><p>Code de l’évènement correspondant à l’acte d’imagerie réalisé.</p>
<p>Doit être présent : Code LOINC issu du jdv-code-document-imagerie-cisis (1.2.250.1.213.1.1.5.687)</p>
<p>Peut être présent : Code(s) CCAM de l’acte d’imagerie.</p></td>
</tr>
</tbody>
</table>

##### Classe Images

Regroupe les informations relatives aux images produites lors d’un examen d’imagerie et les modalités permettant leur consultation ou transfert.

| **Nom** | **Description** |
|----|----|
| urlViewerDrimBox : Texte \[1..1\] | Eléments permettant la construction d’une URL d’accès à la visionneuse DICOM implémentée par une solution DRIMBox associée au système RIS. Une fois l’URL assemblée, celle-ci doit être mentionnée au sein du compte-rendu d’imagerie. |
| dureeRetentionImages : Duree \[1..1\] | Durée de rétention propre à l’archive impliquée concernant les images médicales associées à l’acte ou aux actes d’imagerie effectué. Cette information doit apparaître explicitement au sein du compte-rendu d’imagerie. |

Table 35 : Attributs de la classe « Images»

##### Classe AppareilImagerieUtilise

Permet d’identifier l’équipement d’imagerie utilisé pour réaliser l’examen.

| **Nom** | **Description** |
|----|----|
| identifiantAppareilImagerie : SupportIUD \[1..1\]  | Le support IUD est la manière dont l'IUD est communiqué grâce à l'AIDC et, le cas échéant, son marquage en clair. Correspond à l’identifiant unique d’un appareil d’imagerie médical dans le cas où une technique irradiante est mise en oeuvre (radiologie interventionnelle, scanographie et radiothérapie). |
| modele : Texte \[0..1\]  | Modèle de l’appareil d’imagerie utilisé. |

Table 36 : Attributs de la classe « AppareilImagerieUtilise »

##### Classe ProduitsAdministres

Permet d’identifier le ou les radiopharmaceutiques administrés au patient dans le cadre d’un examen d’imagerie.

| **Nom** | **Description** |
|----|----|
| quantiteAdministree : Texte \[0..1\] | Pour chaque produit radiopharmaceutique administré, il est possible de préciser la dose, la quantité administrée. |
| produitAdministre : Code \[1..1\] | Chaque produit radiopharmaceutique administré doit être identifié pour assurer sa traçabilité. Code issu du jdv ATC niveau 2 "V09" ou "V10". |
| numeroLot : Numerique \[1..1\] | Chaque produit radiopharmaceutique administré doit être associé à son numéro de lot pour assurer sa traçabilité. |

Table 37 : Attributs de la classe « ProduitsAdministres »

##### Classe DemandeExamenImagerie

Cf [2.1.8.1.1](#classe-demandeexamenimagerie)

##### Classe RendezVous

Cf [2.1.8.1.4](#classe-rendezvous)

##### Classe PersonnePriseCharge

Cf [2.1.8.1.5](#classe-personneprisecharge)

##### Classe ModaliteImagerie

Cf [2.1.8.1.7](#classe-modaliteimagerie)

##### Classe LocalisationAnatomique

Cf [2.1.8.1.8](#classe-localisationanatomique)

##### Classe SystemeInformation

Cf [2.1.8.1.13](#classe-systemeinformation)

### Illustrations

####  Diagramme de séquence

<div class="figure" style="text-align: center;">
    <img src="DiagSeq-SFE.png"
    alt="Diagramme de séquence"
    title="DiagSeq-SFE"
    style="width:6.15625in;height:8.99008in">
</div>
