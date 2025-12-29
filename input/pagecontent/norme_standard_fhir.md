#### Standard FHIR 
##### Présentation
[FHIR](https://www.hl7.org/fhir/) (Fast Healthcare Interoperability Resources) est un standard élaboré par HL7 qui s’appuie sur un ensemble de ressources, des blocs de données modulaires, qui correspondent à des objets métiers, médicaux ou administratifs. Ces objets sont caractérisés par des éléments de données, des contraintes et des relations avec d’autres objets métiers.

Les ressources et éléments définis dans FHIR sont restreints et ont pour objectif de répondre aux besoins communs, afin de maintenir une simplicité d’utilisation du standard. Pour répondre aux besoins spécifiques, des extensions doivent être créées dans des guides d'implémentations (IG).

Dans le cadre français, l’[Agence du Numérique en Santé (ANS)](https://www.esante.gouv.fr/) a publié un [guide d'implémentation FHIR](https://hl7.fr/ig/fhir/core/) qui définit des profils FHIR pour répondre aux besoins spécifiques du système de santé français. Ces profils adaptent les ressources FHIR standard pour inclure des contraintes et des extensions spécifiques au contexte français.
##### Maturité et adoption
FHIR a mis en œuvre un modèle de maturité de ressources afin de fournir aux développeurs une
idée de la maturité d’une ressource avant son utilisation et son implémentation. D’une manière
générale, le standard FHIR dans sa version R4 offre encore peu de ressources à l’état normatif donc pouvant être considérées comme stables.

Dans sa version R5, seules 2 ressources supplémentaires sont passées à l'état normatif.

L’ANS exploite les ressources de ce standard dans 12 des 16 volets de la couche Service
disponibles sur [l’espace de Publication](https://esante.gouv.fr/offres-services/ci-sis/espace-publication) du CI-SIS.

Plusieurs volets publiés dans le domaine du médico-social font appel à ce standard en limitant l'utilisation à quelques ressources. La majorité des données étant portée par un document CDA ([SI-MDPH – SI-SdO (Suivi des orientations)](https://interop.esante.gouv.fr/ig/cda/tddui/NormesStandards_TransfertDonneesDUI_V1.0.pdf#%5B%7B%22num%22%3A23%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C81%2C551%2C0%5D), [SI-SdO – SI-ESMS (Suivi des orientations)](https://esante.gouv.fr/volet-si-esms-viatrajectoire-module-ph))

Il convient de souligner que, bien que FHIR propose actuellement une version R5, les ressources mentionnées dans la suite du document seront basées sur la version R4, afin de se conformer aux guides d’implémentation de l’ANS et de maintenir une interopérabilité avec les différents systèmes mis en place sur le territoire français.

##### Outillage
Des outils sont élaborés pour implémenter et tester des systèmes basés sur le standard FHIR, dont :

* L’extension pour Visual Studio Code [FHIR tools](https://marketplace.visualstudio.com/items?itemName=Yannick-Lagger.vscode-fhir-tools);
* Un ensemble [d’outils de validation](http://hl7.org/fhir/R4/validation.html) des ressources FHIR ;
* [Des serveurs](https://confluence.hl7.org/display/FHIR/Public+Test+Servers) publiquement accessibles à des fins de tests, dont HAPI, une librairie de
développement des ressources FHIR en Java.

La [plateforme Gazelle](https://www.ihe-europe.net/testing-IHE/gazelle) est également utilisée pour tester les ressources FHIR. L'outil [matchbox](https://ahdis.github.io/matchbox/) est accessible via le [service de Validation EVS Client](https://interop.esante.gouv.fr/evs/home.seam). Il permet de vérifier si :

* La structure XML ou JSON des ressources est valide ;
* Les ressources sont conformes aux exigences FHIR ;
* Les ressources sont conformes aux exigences des profils issues des guides d'implémentation.

##### Ressources FHIR adaptées au cas d'usage

Dans le cadre du volet "téléradiologie" les ressources suivantes pourraient être utilisées et profilées si besoin pour représenter le contenu des flux d'informations :

* Ressource [Patient](https://hl7.org/fhir/R4/patient.html) (NM N) : La ressource Patient permet de représenter les données
concernant l’identification et les coordonnées (télécommunication et adresse) du patient ainsi que ses contacts. Un profil français de cette ressource existe, nommé [FrPatient](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-patient-ins.html), pour
prendre en compte des spécificités françaises, comme la gestion de l’INS par exemple.

* Ressource [Organization](https://hl7.org/fhir/R4/organization.html) (NM 3) : La ressource Organization permet de représenter une personne morale telle que le centre de téléradiologie. Un profil français, [FrOrganization](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-organization.html), existe également
pour cette ressource.

* Ressource [Practitioner](https://hl7.org/fhir/R4/practitioner.html) (NM 3) : La ressource Practitioner permet de représenter un professionnel de santé. Un profil français,[FRPractitioner](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-practitioner.html) existe également

* Ressource [PractitionerRole](https://hl7.org/fhir/R4/practitionerrole.html) (NM 2) : La ressource PractitionerRole permet de représenter la spécialité d'un professionnel de santé. Un profil français, [FRPractitionerRole](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-practitioner-role.html) existe également.

* Ressource [ServiceRequest](https://hl7.org/fhir/R4/servicerequest.html) (NM 2) : La ressource ServiceRequest permet de représenter une demande de service, comme par exemple une demande de diagnostic, de traitement ou d'opérations à effectuer.

* Ressource [Appointment](https://hl7.org/fhir/R4/appointment.html) (NM 3) : La ressource Appointment permet de représenter un rendez vous ou une demande de rendez vous avec un professionnel de santé, un dispositif médical ou une unité de soin. Un profil français, [FRAppointment](https://hl7.fr/ig/fhir/core/StructureDefinition-fr-core-appointment.html) existe également.

* Ressource [AppointmentResponse](https://hl7.org/fhir/R4/appointmentresponse.html) (NM 3) : La ressource AppointmentResponse permet de représenter la réponse à une demande de rendez vous.

* Ressource [Condition](https://hl7.org/fhir/R4/condition.html) (NM 3) : La ressource Condition permet de représenter une affection, un problème, un diagnostic rencontré par un patient.

* Ressource [DocumentReference](https://hl7.org/fhir/R4/documentreference.html) (NM 3) : La ressource DocumentReference permet de représenter un document stocké dans différents formats ou bien une référence vers ce document.

* Ressource [ImagingStudy](https://hl7.org/fhir/R4/imagingstudy.html) (NM 3) : La ressource ImagingStudy permet de représenter les métadonnées d'un objet DICOM.

* Ressource [GuidanceResponse](https://hl7.org/fhir/R4/guidanceresponse.html) (NM 2) : La ressource GuidanceResponse permet de représenter la réponse à la demande d'imagerie avec les éléments joints par le professionnel de santé effecteur.

* Ressource [Endpoint](https://hl7.org/fhir/R4/endpoint.html) (NM 2) : La ressource Endpoint permet de représenter un endpoint accessible comme un serveur (web,fhir,dicom,..)

* Ressource [Device](https://hl7.org/fhir/R4/device.html) (NM 2) : La ressource Device permet de représenter un équipement utilisé lors de la prise en charge du patient, que ce soit un DM ou un autre équipement .

* Ressource [MedicationAdministration](https://hl7.org/fhir/R4/medicationadministration.html) (NM 2) : La ressource MedicationAdministration permet de représenter l'injection ou la consommation d'un médicament pour un patient par un professionnel de santé.

* Ressource [BodyStructure](https://hl7.org/fhir/R4/bodystructure.html) (NM 1) : La ressource BodyStructure permet de représenter une structure anatomique du corps humain.

<table>
<colgroup>
<col style="width: 32%" />
<col style="width: 56%" />
</colgroup>
<thead>
<tr>
<th><strong>Concept métier</strong></th>
<th><strong>Couverture par des ressources FHIR</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Patient</td>
<td>Patient</td>
</tr>
<tr>
<td>PSResponsable</td>
<td>Practitioner</td>
</tr>
<tr>
<td>PSEffecteur</td>
<td>Practitioner</td>
</tr>
<tr>
<td>IdentifiantDemandeExamen</td>
<td>ServiceRequest</td>
</tr>
<tr>
<td>StructureImagerie</td>
<td>Organization</td>
</tr>
<tr>
<td>PlateformeTeleradiologie</td>
<td>Organization</td>
</tr>
<tr>
<td>NatureDemande</td>
<td>ServiceRequest</td>
</tr>
<tr>
<td>DateDemande</td>
<td>ServiceRequest</td>
</tr>
<tr>
<td>IdentifiantRDV</td>
<td>Appointment</td>
</tr>
<tr>
<td>DateHeurePriseCharge</td>
<td>Appointment</td>
</tr>
<tr>
<td>JustificationDemande</td>
<td>Condition</td>
</tr>
<tr>
<td>Antecedents</td>
<td>Condition</td>
</tr>
<tr>
<td>MotifAnnulation</td>
<td>Appointment</td>
</tr>
<tr>
<td>MotifRefus</td>
<td>AppointmentResponse</td>
</tr>
<tr>
<td>DocumentDemandeExamen</td>
<td>DocumentReference</td>
</tr>
<tr>
<td>DocumentsTiers</td>
<td>DocumentReference</td>
</tr>
<tr>
<td>LocalisationAnatomique</td>
<td>BodyStructure</td>
</tr>
<tr>
<td>ModaliteImagerie</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>DecisionEffecteur</td>
<td>GuidanceResponse</td>
</tr>
<tr>
<td>ProtocoleImagerie</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>URLViewerDRIMBOX</td>
<td>Endpoint</td>
</tr>
<tr>
<td>DuréeRétentionImages</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>DateRéalisationExamen</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>IdentificationMatériel</td>
<td>Device</td>
</tr>
<tr>
<td>ProduitsAdministres</td>
<td>MedicationAdministration</td>
</tr>
<tr>
<td>AccessionNumber</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>StudyInstanceUID</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>codeEvenement</td>
<td>ImagingStudy</td>
</tr>
<tr>
<td>roleProfessionnel</td>
<td>PractitionerRole</td>
</tr>
</tbody>
</table>
<p style="text-align:center;">Table 1 : Mise en correspondance des concepts métier avec les ressources FHIR</p>

##### Transport

Le standard FHIR utilise [l'API REST](https://build.fhir.org/http.html) pour l'échange et l'interrogation des ressources via différentes [interactions](https://build.fhir.org/exchange-module.html)

Différents niveaux [d’interactions](https://hl7.org/fhir/R4/http.html) sont possibles pour une API REST:

* Instance (s’applique à une ressource en particulier) ;
* Type (s’applique à un ensemble de ressources de même type) ;
* Système (s’applique à l’ensemble du système).

Les interactions qui pourront s’appliquer dans le cas du volet « Téléradiologie » sont les interactions au niveau instance suivantes :

* [Create](https://hl7.org/fhir/R4/http.html#create) pour l’ajout d’une nouvelle ressource sur le serveur grâce à la méthode HTTP POST ;
* [Delete](https://hl7.org/fhir/R4/http.html#delete) pour la suppression d'une ressource sur le serveur grâce à la méthode HTTP DELETE;
* [Update](https://hl7.org/fhir/R4/http.html#update) pour le remplacement d’une ressource existante sur le serveur grâce à la méthode HTTP PUT ou PATCH.
Enfin, le corps des requêtes HTTP est une ressource FHIR qui peut être [formatée](https://hl7.org/fhir/R4/http.html#mime-type) en XML, JSON ou RDF (Turtle).

Comme évoqué précédemment, les ressources peuvent être concaténées au sein de ressource Bundle. Dans le cas d'un Bundle de type Document, le endpoint à utiliser sera `'base/Bundle'`.

Les interactions FHIR implémentent le protocole RESTful, couramment utilisé dans de nombreux
domaines. Le [Richardson REST Maturity Model](http://martinfowler.com/articles/richardsonMaturityModel.html) définit 4 niveaux de maturité d’une API REST (de 0
à 3), FHIR se situe au niveau 2 mais l’utilisation d’extensions peut permettre d’atteindre le niveau 3. L’API FHIR est largement utilisée pour échanger des données de santé

Pour tester des requêtes HTTP FHIR, il est possible d’utiliser des serveurs publiquement accessibles à des fins de test, notamment HAPI, via des outils de test d’API tels que Postman ou Insomnia. La plateforme Gazelle, via le service de Validation EVS Client, permet aux éditeurs de valider les ressources et les requêtes FHIR en les comparant à des modèles. La plateforme offre également la possibilité d’utiliser des simulateurs FHIR permettant aux éditeurs de tester leur système de façon autonome.
Enfin, de nombreux évènements de tests, tels que les Connectathons, et Projectathons permettent aux éditeurs de tester en situation réelle leur conformité aux spécifications ainsi que leur capacité à échanger avec des partenaires.

###### Adaptation au cas d'usage 

Il est important de noter que, pour les interactions décrites ci-dessous, les acteurs doivent être en mesure non seulement d’envoyer des données, mais également d’en recevoir. En termes
d’architecture, chaque acteur devra par conséquent être à la fois client et serveur.
Chaque acteur devra également travailler la gestion des authentifications, des autorisations, et autres besoins de sécurité fondamentaux ; ces aspects sortent du périmètre de la présente étude.

###### Transmettre une demande d'examen d'imagerie

La transmission d’une demande d’examen d’imagerie peut être réalisée grâce à l'envoi d'une ressource, par exemple DocumentReference ou ServiceRequest via une requête POST reposant sur l'interaction "[create](https://build.fhir.org/http.html#create)".

Si la création de la ressource s'est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 1.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

 <div style="text-align:center;"> {%include flux1.svg%} </div>

<p style="text-align:center;">Figure 1 - Diagramme d'échange FHIR pour le flux 1 - Transmission d'une demande d'examen d'imagerie</p>

 Ce flux permettrait de couvrir l'ensemble des processus suivants :

* Créer une demande d'examen d'imagerie
* Transmettre la demande d'examen d'imagerie
* Recevoir la demande d'imagerie

###### Annulation d'une demande d'examen d'imagerie

L'annulation d'une demande d'examen d'imagerie peut être réalisée grâce à la suppression d'une ressource créée dans le flux 1, par exemple DocumentReference ou ServiceRequest via une requête DELETE reposant sur l'interaction "[delete]((https://build.fhir.org/http.html#delete)").

Si la suppression de la ressource s'est correctement effectuée, le consommateur retourne un code http `200 OK`. En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

<div style="text-align:center;"> {%include flux2.svg%} </div>

<p style="text-align:center;">Figure 2 - Diagramme d'échange FHIR pour le flux 2 - Annulation d'une demande d'examen d'imagerie</p>

 Ce flux permettrait de couvrir l'ensemble des processus suivants :

* Créer une annulation d'une demande d'examen d'imagerie
* Transmettre l'annulation de la demande d'examen d'imagerie
* Recevoir l'annulation de la demande d'examen d'imagerie

###### Réponse à une demande d'examen d'imagerie

 La réponse à une demande d’examen d’imagerie peut être réalisée grâce à l'envoi d'une ressource, par exemple ImagingStudy ou GuidanceResponse via une requête POST reposant sur l'interaction "[create](https://build.fhir.org/http.html#create)".

 Si la création de la ressource s'est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 3.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

<div style="text-align:center;"> {%include flux3.svg%} </div>

<p style="text-align:center;">Figure 3 - Diagramme d'échange FHIR pour le flux 3 - Réponse à une demande d'examen d'imagerie</p>

 Ce flux permettrait de couvrir l'ensemble des processus suivants :

* Etablir le protocole d'imagerie
* Générer la réponse métier à la demande
* Transmettre la réponse métier à la demande
* Recevoir la réponse métier à la demande

###### Transmettre un complément d'information post-examen

 Le complément d'information post-examen d’imagerie peut être réalisé grâce à l'envoi d'une ressource, par exemple ImagingStudy ou DocumentReference via une requête POST reposant sur l'interaction "[create](https://build.fhir.org/http.html#create)".

 Si la création de la ressource s'est correctement effectuée, le consommateur retourne un code http `201 created` accompagné de la ressource créée (flux 4.2). En cas d’échec, le consommateur doit répondre avec le code HTTP approprié. Une ressource [OperationOutcome](https://hl7.org/fhir/operationoutcome.html) doit également y être associée pour véhiculer les messages d’erreurs identifiant la nature de l’erreur.

<div style="text-align:center;"> {%include flux4.svg%} </div>

<p style="text-align:center;">Figure 4 - Diagramme d'échange FHIR pour le flux 4 - Transmission d'un complément d'information post-examen</p>

 Ce flux permettrait de couvrir l'ensemble des processus suivants :

* Réaliser le ou les actes d'imagerie
* Générer un complément d'information post-examen
* Transmettre un complément d'information post-examen
* Recevoir un complément d'information post-examen

##### Synthèse

FHIR est un standard moderne, largement adopté dans le domaine de la santé, permettant l’échange de données de santé de manière structurée et interopérable.

L’analyse des ressources FHIR applicables au volet « Téléradiologie » montre que ce standard permet de couvrir l’ensemble des concepts métier identifiés.
La notion d’acquittement n’est toutefois pas explicitement modélisée en FHIR et doit être traitée via les mécanismes standards HTTP ou des ressources dédiées comme OperationOutcome.

Enfin, l’utilisation de FHIR implique que chaque acteur dispose d’un serveur FHIR, capable de jouer à la fois les rôles de client et de serveur, afin de supporter l’ensemble des échanges requis.