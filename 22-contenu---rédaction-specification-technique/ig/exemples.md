# Exemples de messages - Volet Téléradiologie v0.1.0

* [**Table of Contents**](toc.md)
* **Exemples de messages**

## Exemples de messages

### Flux 1 - Transmission de la demande d’examen (ORM^O01)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 ORM^O01** conforme au volet Téléradiologie.
 Il présente une demande d’examen d’imagerie transmise par le RIS vers le SI de téléradiologie, incluant les informations administratives et de prise en charge du patient, les éléments de prescription portés par les segments **ORC** et **OBR**, ainsi que des **groupes OBSERVATION (OBX)** spécifiques à la téléradiologie.

Les segments **OBX** illustrés dans cet exemple véhiculent notamment :

* la **localisation anatomique** de l’examen ;
* des **données morphologiques du patient** (taille, poids) ;
* le **statut de grossesse**, lorsque cette information est connue et pertinente.

```
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SATE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS||PAT-TROIS^DOMINIQUE^Dominique^^^^L|PAT-TROIS^Dominique^^^^^D|19790328|F|||^^^^^^BDL^^51215~23 AV TORCATIS ^^PIA^^66380^FRA^H|||||||||||||||||||N||VALI
PV1||O|||||||||||||||||IdentifiantRendezVous|
ORC|NW|IdentifiantDemandeExamen|||||||DateDemande|||PSResponsable|||||STRUCTURE_IMAGERIE^^TLR_TYPE_ORGANISATION||||IdentifiantOrganisation
OBR||IdentifiantDemandeExamen||MR^Résonance magnétique^DCM||||||||||||PSResponsable|||||||||||||||JustificationDemande
OBX|1|CE|LOCALISATION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.1|77407^tête et/ou cou^SNT||||||F
OBX|2|CE|LOCALISATION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.2|24028007^côté droit^SNT||||||F
OBX|2|NM|8302-2^Body height^LN||170|cm|||||F
OBX|3|NM|29463-7^Body weight^LN||68|kg|||||F
OBX|4|CE|82810-3^Pregnancy status^LN||N^^expandedYes-NoIndicator||||||F

```

### Flux 2 - Annulation de la demande d’examen (ORM^O01)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 ORM^O01** conforme au volet Téléradiologie pour **l’annulation d’une demande d’examen d’imagerie**.

Le message montre comment le **RIS** notifie l’annulation au **SI de téléradiologie**. Les segments **ORC** et **OBR** sont remplis de manière similaire au flux 1, avec les spécificités suivantes :

* **ORC-1** fixé à `CA` pour indiquer l’annulation de la demande ;
* possibilité de véhiculer un **motif d’annulation** dans **ORC-16**, soit par code local (CE-1/CE-3) soit par texte libre (CE-2) ;
* le **groupe OBSERVATION (OBX)** est optionnel et peut être omis.

```
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||ATHENEA^PI~279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS||PAT-TROIS^DOMINIQUE^Dominique^^^^L|PAT-TROIS^Dominique^^^^^D|19790328|F|||^^^^^^BDL^^51215~23 AV TORCATIS ^^PIA^^66380^FRA^H|||||||||||||||||||N||VALI
PV1||O|||||||||||||||||IdentifiantRendezVous|
ORC|CA|IdentifiantDemandeExamen|||||||DateDemande|||PSResponsable|||||STRUCTURE_IMAGERIE^^TLR_TYPE_ORGANISATION||||IdentifiantOrganisation
OBR||IdentifiantDemandeExamen||MR^Résonance magnétique^DCM||||||||||||PSResponsable

```

#### Flux 3 - Réponse à la demande d’examen d’imagerie (ORU^R01)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 ORU^R01** conforme au volet Téléradiologie.

Le message permet de véhiculer :

* la **décision du PS effecteur** vis-à-vis de la demande (acceptation ou refus) via le champ **ORC-1** (`OK` pour acceptation, `OC` pour refus) ;
* le ou les **protocoles d’imagerie** associés, lorsqu’il s’agit d’une acceptation, portés dans les segments **OBX**.

```
MSH|^~\&|TLRapp|TLRfacility|StructureApp|StructureFacility|20260106134418||ORU^R01^ORU_R01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||ATHENEA^PI~279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS||PAT-TROIS^DOMINIQUE^Dominique^^^^L|PAT-TROIS^Dominique^^^^^D|19790328|F|||^^^^^^BDL^^51215~23 AV TORCATIS ^^PIA^^66380^FRA^H|||||||||||||||||||N||VALI
ORC|OK|IdentifiantDemandeExamen||||||||||PSEffecteur||||MotifRefus|PLATEFORME_TELERADIOLOGIE^^TLR_TYPE_ORGANISATION||||IdentifiantOrganisation
OBR||IdentifiantDemandeExamen||MR^Résonance magnétique^DCM||||||||||||PSEffecteur
OBX|1|FT|PROTOCOLE_IMAGERIE^Protocole d'imagerie médicale^TLR_OBSERVATION||Paramètres d’acquisition : kV : 120…||||||F

```

#### Flux 4 - Transmission d’un complément d’information post-examen (OMI^O23)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 OMI^O23** conforme au volet Téléradiologie pour la **transmission d’un complément d’information post-examen**.

Ces informations sont transmises au **SI de téléradiologie** afin de permettre la **rédaction du compte rendu** par le téléradiologue et sa **publication dans le DMP** via le RIS.

```
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||ATHENEA^PI~279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS||PAT-TROIS^DOMINIQUE^Dominique^^^^L|PAT-TROIS^Dominique^^^^^D|19790328|F|||^^^^^^BDL^^51215~23 AV TORCATIS ^^PIA^^66380^FRA^H|||||||||||||||||||N||VALI
PV1||O|||||||||||||||||IdentifiantRendezVous|
ORC|NW|20260106134418|A compléter||SC||||DateDemande|
TQ1||||||Durée de rétention des images|Date/heure de l'examen d'imagerie
OBR||IdentifiantDemandeExamen||24590-2^résonance magnétique cerveau^LN||||||||||||PSResponsable|
IPC|Accession Identifier|Accession number|Study Instance UID|Scheduled Procedure Step ID|MR^Résonance magnétique^DCM
OBX|1|TX|URL_VIEWER_DRIMBOX^URL de la visionneuse DRIMbox^TLR_OBSERVATION||URL||||||F
OBX|2|CE|LOCALISATION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.1|77407^tête et/ou cou^SNT||||||F
OBX|3|CE|LOCALISATION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.2|24028007^côté droit^SNT||||||F
OBX|4|CE|PRODUIT_ADMINISTRE^Produit administré lors de l'examen d'imagerie^TLR_OBSERVATION|1.1|TypeProduit^^ATC|||||F
OBX|5|NM|PRODUIT_ADMINISTRE^Produit administré lors de l'examen d'imagerie^TLR_OBSERVATION|1.2|0123456789|||||F
OBX|6|NM|PRODUIT_ADMINISTRE^Produit administré lors de l'examen d'imagerie^TLR_OBSERVATION|1.3|1|ml||||F
OBX|7|TX|APPAREIL_IMAGERIE^Appareil d'imagerie utilisé lors de l'examen^TLR_OBSERVATION|1.1|1234567896363||||||F
OBX|8|TX|APPAREIL_IMAGERIE^Appareil d'imagerie utilisé lors de l'examen^TLR_OBSERVATION|1.2|Modèle||||||F

```

