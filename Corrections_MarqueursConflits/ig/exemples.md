# Exemples de messages - Volet Téléradiologie v0.1.0-ballot

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
<<<<<<< 22-contenu---rédaction-specification-technique
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|000001|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
PV1||O|||||||||||||||||000897406^^^CHU-X&000897406&M^VN^^20210409|||||||||||||||||||||||||20260103134418|
=======
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
PV1||O|||||||||||||||||000897406^^^CHU-X&000897406&M^VN^^20210409|
>>>>>>> main
ORC|NW|OPN101^^1.2.250.1.748.12345678.12^ISO|||||||20260106134418||801234564895^Eric^Thomas^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS|801234567897^Hoda^Adam^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS||^PRN^CP^^^^^^^^^+3360708091|||STRUCTURE_IMAGERIE^^TLR_TYPE_ORGANISATION||||Structure-Y^^^^^ASIP-SANTE-ST&1.2.250.1.71.4.2.2&ISO^FINEG^^^300017985
OBR||OPN101^^1.2.250.1.748.12345678.12^ISO||TRANSMISSION_DEMANDE^Transmission d’une demande d’examen d'imagerie^TLR_OBR_PROCEDURE|||||||||JustificationDemande|||801234567897^Hoda^Adam^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS|
NTE|||Commentaire sur la finalité de l'examen|FINALITE_EXAMEN^^HL70364
OBX|1|CE|MODALITE_IMAGERIE^Modalité d’imagerie utilisée ou prévue pour réaliser l’examen^TLR_OBSERVATION||MR^Résonance magnétique^DCM||||||O
NTE|||Commentaire sur la modalité|MODALITE_IMAGERIE^^HL70364
OBX|2|CE|REGION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.1|77407^tête et/ou cou^SNT||||||O
OBX|3|CE|REGION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.2|24028007^côté droit^SNT||||||O
OBX|4|FT|11322-5^History of General health Narrative^LN||Antécédents majeur du patient|||MAJEUR^^HL70078|||O
OBX|5|NM|8302-2^Body height^LN||170|cm|||||O
OBX|6|NM|29463-7^Body weight^LN||68|kg|||||O
OBX|7|CE|82810-3^Pregnancy status^LN||N^^expandedYes-NoIndicator||||||O

```

### Flux 2 - Annulation de la demande d’examen (ORM^O01)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 ORM^O01** conforme au volet Téléradiologie pour **l’annulation d’une demande d’examen d’imagerie**.

Le message montre comment le **RIS** notifie l’annulation au **SI de téléradiologie**. Les segments **ORC** et **OBR** sont remplis de manière similaire au flux 1, avec les spécificités suivantes :

* **ORC-1** fixé à `CA` pour indiquer l’annulation de la demande ;
* possibilité de véhiculer un **motif d’annulation** dans **ORC-16**, soit par code local (CE-1/CE-3) soit par texte libre (CE-2) ;
* le **groupe OBSERVATION (OBX)** est optionnel et peut être omis.

```
<<<<<<< 22-contenu---rédaction-specification-technique
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134518||ORM^O01^ORM_O01|000002|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
PV1||O|||||||||||||||||000897406^^^CHU-X&000897406&M^VN^^20210409|||||||||||||||||||||||||20260103134418|
ORC|CA|OPN101^^1.2.250.1.748.12345678.12^ISO|||||||20260106134518|||801234567897^Hoda^Adam^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS||||^Motif d'annulation de la demande|STRUCTURE_IMAGERIE^^TLR_TYPE_ORGANISATION||||Structure-Y^^^^^ASIP-SANTE-ST&1.2.250.1.71.4.2.2&ISO^FINEG^^^300017985
=======
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
PV1||O|||||||||||||||||000897406^^^CHU-X&000897406&M^VN^^20210409|
ORC|CA|OPN101^^1.2.250.1.748.12345678.12^ISO|||||||20260106134418|||801234567897^Hoda^Adam^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS|||||STRUCTURE_IMAGERIE^^TLR_TYPE_ORGANISATION||||Structure-Y^^^^^ASIP-SANTE-ST&1.2.250.1.71.4.2.2&ISO^FINEG^^^300017985
>>>>>>> main
OBR||OPN101^^1.2.250.1.748.12345678.12^ISO||ANNULATION_DEMANDE^Annulation d’une demande d’examen^TLR_OBR_PROCEDURE||||||||||||801234567897^Hoda^Adam^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS

```

### Flux 3 - Réponse à la demande d’examen d’imagerie (ORU^R01)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 ORU^R01** conforme au volet Téléradiologie.

Le message permet de véhiculer :

* la **décision du PS effecteur** vis-à-vis de la demande (acceptation ou refus) via le champ **ORC-1** (`OK` pour acceptation, `OC` pour refus) ;
* le ou les **protocoles d’imagerie** associés, lorsqu’il s’agit d’une acceptation, portés dans les segments **OBX**.

```
<<<<<<< 22-contenu---rédaction-specification-technique
MSH|^~\&|TLRapp|TLRfacility|StructureApp|StructureFacility|20260106164418||ORU^R01^ORU_R01|000003|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
ORC|OK|OPN101^^1.2.250.1.748.12345678.12^ISO||||||||||801234564895^Eric^Thomas^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS|||||PLATEFORME_TLR^^TLR_TYPE_ORGANISATION||||Plateforme-Y^^^^^ASIP-SANTE-ST&1.2.250.1.71.4.2.2&ISO^FINEG^^^300017986
=======
MSH|^~\&|TLRapp|TLRfacility|StructureApp|StructureFacility|20260106134418||ORU^R01^ORU_R01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
ORC|OK|OPN101^^1.2.250.1.748.12345678.12^ISO||||||||||801234564895^Eric^Thomas^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS||||MotifRefus|PLATEFORME_TLR^^TLR_TYPE_ORGANISATION||||Plateforme-Y^^^^^ASIP-SANTE-ST&1.2.250.1.71.4.2.2&ISO^FINEG^^^300017986
>>>>>>> main
OBR||OPN101^^1.2.250.1.748.12345678.12^ISO||REPONSE_DEMANDE^Réponse à une demande d’examen d'imagerie^TLR_OBR_PROCEDURE||||||||||||801234564895^Eric^Thomas^^^DR^^^ASIP-SANTE- PS&1.2.250.1.71.4.2.1&ISO^D^^^IDNPS
OBX|1|ED|PROTOCOLE_IMAGERIE^Protocole d'imagerie médicale^TLR_OBSERVATION||^TEXT^^base64^Pendggfbubzbdy12gggvt||||||F

```

### Flux 4 - Transmission d’un complément d’information post-examen (OMI^O23)

L’exemple ci-dessous illustre un message **HL7 v2.5.1 OMI^O23** conforme au volet Téléradiologie pour la **transmission d’un complément d’information post-examen**.

Ces informations sont transmises au **SI de téléradiologie** afin de permettre la **rédaction du compte rendu** par le téléradiologue et sa **publication dans le DMP** via le RIS.

```
<<<<<<< 22-contenu---rédaction-specification-technique
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106184518||ORM^O01^ORM_O01|000004|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
PV1||O|||||||||||||||||000897406^^^CHU-X&000897406&M^VN^^20210409|||||||||||||||||||||||||20260103134418|20260107134418
ORC|SR|OPN101^^1.2.250.1.748.12345678.12^ISO|
=======
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|20260106134418|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
PID|||279035121518989^^^ASIP-SANTE-INS-NIR&1.2.250.1.213.1.4.10&ISO^INS^^20101207||PAT-TROIS^DOMINIQUE^DOMINIQUE^^^^L||19790328|F|||28 Av de Breteuil^^PARIS^^75007^FRA^H^^^^^^^~^^^^^^BDL^^63220|||||||405660^^^AUT-AFFECTATION&1204567809&M^AN^^20101205|||||||||||||N|VALI
PV1||O|||||||||||||||||000897406^^^CHU-X&000897406&M^VN^^20210409|
ORC|SC|OPN101^^1.2.250.1.748.12345678.12^ISO|
>>>>>>> main
TQ1||||||730^jours|20260106184418
OBR||OPN101^^1.2.250.1.748.12345678.12^ISO||COMPLEMENT_POST_ACTE^Transmission d'un complément d’information post-examen^TLR_OBR_PROCEDURE|
IPC|ACN101^^1.2.250.1.925.994044.27^ISO|24590-2^^2.16.840.1.113883.6.1^ISO|1.2.250.1.213.4.5.2.1.101|24590-2^^2.16.840.1.113883.6.1^ISO|
OBX|1|TX|URL_PARTIELLE_VIEWER^URL partielle d’accès à la visionneuse d’imagerie DRIMbox^TLR_OBSERVATION||URL||||||F
OBX|2|CE|CODE_ACTE_IMAGERIE^Code de l'acte d'imagerie réalisée^TLR_OBSERVATION||24590-2^résonance magnétique cerveau^LN||||||F
OBX|3|CE|REGION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.1|77407^tête et/ou cou^SNT||||||F
OBX|4|CE|REGION_ANATOMIQUE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION|1.2|24028007^côté droit^SNT||||||F
OBX|5|CE|MODALITE_IMAGERIE^Localisation anatomique examinée dans le cadre de l’examen d’imagerie^TLR_OBSERVATION||MR^Résonance magnétique^DCM||||||F
OBX|6|CE|PRODUIT_ADMINISTRE^Produit administré lors de l'examen d'imagerie^TLR_OBSERVATION|1.1|TypeProduit^^ATC|||||F
OBX|7|NM|PRODUIT_ADMINISTRE^Produit administré lors de l'examen d'imagerie^TLR_OBSERVATION|1.2|0123456789|||||F
OBX|8|NM|PRODUIT_ADMINISTRE^Produit administré lors de l'examen d'imagerie^TLR_OBSERVATION|1.3|1|ml||||F
OBX|9|TX|APPAREIL_IMAGERIE^Appareil d'imagerie utilisé lors de l'examen^TLR_OBSERVATION|1.1|1234567896363||||||F
OBX|10|TX|APPAREIL_IMAGERIE^Appareil d'imagerie utilisé lors de l'examen^TLR_OBSERVATION|1.2|Modèle||||||F

```

