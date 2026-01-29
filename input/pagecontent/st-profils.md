### Profils de message

La présente partie décrit les **profils de messages HL7 v2** retenus pour supporter les flux d’échange du volet Téléradiologie.  
Pour chaque flux identifié, le **type de message HL7 v2** associé est précisé, ainsi que la **structure générale des segments** utilisés afin de couvrir les concepts métiers attendus.

Les profils de message définissent :
- le **type de message HL7 v2** et l’événement associé ;
- l’**ordre des segments** ;
- les **segments requis, optionnels ou répétables** ;
- le rôle fonctionnel de chaque segment dans le cadre du flux considéré.

Des exemples représentatifs de chacun des profils de message conformes au volet Téléradiologie sont fournis [en annexe](./exemples.html).

#### Description des messages HL7 v2

L'implémentation doit valoriser l'intégralité des segments et champs obligatoires applicables aux messages HL7v2 afin de répondre au standard d'interopérabilité afférent.

Ci-dessous sont représentées les structures de messages **HL7 v2**, présentées selon deux vues complémentaires :
- une **vue technique**, sous forme de tableaux, décrivant de manière exhaustive la **structure des profils de messages** (segments, cardinalités et ordonnancement) ;
- une **vue fonctionnelle**, plus synthétique, matérialisée par des **diagrammes**, centrée sur les segments utilisés dans le cadre du volet Téléradiologie. 

##### Flux 1 - Message ORM^O01^ORM_O01 en HL7 v2.5.1

Le flux 1 repose sur l’échange d’un message **ORM^O01** conforme à la norme **HL7 v2.5.1**, utilisé pour la **transmission d’une demande d’examen d’imagerie** dans le cadre du volet Téléradiologie.

La structure du message est **conforme au profil IHE RAD – Scheduled Workflow (SWF)**. Une **surcouche de contraintes spécifiques au domaine de la Téléradiologie** vient compléter ce cadre afin de couvrir des besoins fonctionnels non pris en charge nativement par IHE SWF.

###### Description technique

Le message est composé des segments principaux suivants :

- **MSH** : en-tête du message et informations de routage ;
- **PID / PV1** : identification du patient et du contexte de prise en charge ;
- **ORC / OBR** : informations liées à la demande d’examen, conformément à IHE SWF ;
- **Groupes OBSERVATION (OBX)** : supporte les informations complémentaires spécifiques au volet Téléradiologie, non contraintes par IHE SWF.

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments ainsi que leur caractère requis, optionnel ou répétable.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th><p>Segment</p></th>
      <th><p>Meaning</p></th>
      <th><p>Usage</p></th>
      <th><p>Card.</p></th>
      <th><p>§ HL7</p></th>
    </tr>
    <tr>
      <td><p>MSH</p></td>
      <td><p>Message Header</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Header)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>PID</p></td>
      <td><p>Patient Identification</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PD1]</p></td>
      <td><p>Additional Demographics</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Patient)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT_VISIT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>PV1</p></td>
      <td><p>Patient Visit</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PV2]</p></td>
      <td><p>Patient Visit – Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT_VISIT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- INSURANCE begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>IN1</p></td>
      <td><p>Insurance</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[IN2]</p></td>
      <td><p>Insurance Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[IN3]</p></td>
      <td><p>Insurance Certification</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- INSURANCE end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[GT1]</p></td>
      <td><p>Guarantor</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{AL1}]</p></td>
      <td><p>Allergy Information</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>{</p></td>
      <td><p>--- ORDER begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>ORC</p></td>
      <td><p>Common Order</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[</p></td>
      <td><p>--- ORDER_DETAIL begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>OBR</p></td>
      <td><p>Order Detail / Observation Request</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[RQD]</p></td>
      <td><p>Requisition Detail</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[RQ1]</p></td>
      <td><p>Requisition Detail-1</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[RXO]</p></td>
      <td><p>Pharmacy/Treatment Order</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[ODS]</p></td>
      <td><p>Dietary Orders, Supplements, and Preferences</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[ODT]</p></td>
      <td><p>Diet Tray Instructions</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Order Detail)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[CTD]</p></td>
      <td><p>Contact Data</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>11</p></td>
    </tr>
    <tr>
      <td><p>[{DG1}]</p></td>
      <td><p>Diagnosis</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- OBSERVATION begin</p></td>
      <td><p>1</p></td>
      <td><p>[1..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>OBX</p></td>
      <td><p>Observation / Result</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Observation)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- OBSERVATION end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>]</p></td>
      <td><p>--- ORDER_DETAIL end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[{FT1}]</p></td>
      <td><p>Financial Transaction</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{CTI}]</p></td>
      <td><p>Clinical Trial Identification</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[BLG]</p></td>
      <td><p>Billing</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>}</p></td>
      <td><p>--- ORDER end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **ORM^O01** du flux 1 permet au système demandeur (RIS) de transmettre au système effecteur (SI Téléradiologie) l’ensemble des informations associées à la prise en charge du patient ainsi que les éléments relatifs à une demande d'examen d'imagerie le concernant.

Outre les éléments standards concernant la demande et la prescription portés par les segments **ORC** et **OBR**, ce flux s’appuie sur des **groupes OBSERVATION (OBX)** afin de véhiculer des informations fonctionnelles complémentaires indispensables à la bonne réalisation de l’examen, telles que :
- la **localisation anatomique** et, le cas échéant, une **précision topographique**
- les **antécédents médicaux du patient**
- des **données morphologiques pertinentes** pour la planification de l’examen d'imagerie (taille, poids, statut de grossesse)

Ces OBSERVATION sont structurées et identifiées conformément aux règles définies dans la partie [Contraintes applicables aux profils de message](./specifications_techniques.html#flux-1---transmission-de-la-demande-dexamen-dimagerie), notamment via l’utilisation de codes locaux dans **OBX-3**.

Le diagramme ci-dessous illustre le **fonctionnement global du message**, les interactions entre les segments principaux ainsi que le rôle des **OBX spécifiques Téléradiologie** dans le cadre du flux 1.

<br>

##### Flux 2 - Message ORM^O01^ORM_O01 en HL7 v2.5.1

Le flux 2 repose sur l’échange d’un message **ORM^O01** conforme à la norme **HL7 v2.5.1**, utilisé pour **l' annulation d'une demande d’examen d’imagerie** dans le cadre du volet Téléradiologie.

Ce flux est **structurellement très proche du flux 1** et s’appuie lui aussi sur le **profil IHE RAD – Scheduled Workflow (SWF)**, notamment pour les segments **ORC** et **OBR**, qui conservent les mêmes principes de structuration et de valorisation que pour la demande initiale.

La principale différence structurelle en comparaison avec le flux 1 concerne l’utilisation du **groupe OBSERVATION (OBX)** qui est optionnel dans le cadre de ce flux.

###### Description technique

Le message est composé des segments principaux suivants :

- **MSH** : en-tête du message et informations de routage
- **PID / PV1** : identification du patient et du contexte de prise en charge
- **ORC / OBR** : informations de demande, avec une action positionnée à l’annulation

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th><p>Segment</p></th>
      <th><p>Meaning</p></th>
      <th><p>Usage</p></th>
      <th><p>Card.</p></th>
      <th><p>§ HL7</p></th>
    </tr>
    <tr>
      <td><p>MSH</p></td>
      <td><p>Message Header</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Header)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>PID</p></td>
      <td><p>Patient Identification</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PD1]</p></td>
      <td><p>Additional Demographics</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Patient)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT_VISIT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>PV1</p></td>
      <td><p>Patient Visit</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PV2]</p></td>
      <td><p>Patient Visit – Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT_VISIT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- INSURANCE begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>IN1</p></td>
      <td><p>Insurance</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[IN2]</p></td>
      <td><p>Insurance Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[IN3]</p></td>
      <td><p>Insurance Certification</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- INSURANCE end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[GT1]</p></td>
      <td><p>Guarantor</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{AL1}]</p></td>
      <td><p>Allergy Information</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p> </p></td>
      <td><p>--- PATIENT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>{</p></td>
      <td><p>--- ORDER begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>ORC</p></td>
      <td><p>Common Order</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[</p></td>
      <td><p>--- ORDER_DETAIL begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>OBR</p></td>
      <td><p>Order Detail / Observation Request</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[RQD]</p></td>
      <td><p>Requisition Detail</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[RQ1]</p></td>
      <td><p>Requisition Detail-1</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[RXO]</p></td>
      <td><p>Pharmacy/Treatment Order</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[ODS]</p></td>
      <td><p>Dietary Orders, Supplements, and Preferences</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[ODT]</p></td>
      <td><p>Diet Tray Instructions</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Order Detail)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[CTD]</p></td>
      <td><p>Contact Data</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>11</p></td>
    </tr>
    <tr>
      <td><p>[{DG1}]</p></td>
      <td><p>Diagnosis</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- OBSERVATION begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>OBX</p></td>
      <td><p>Observation / Result</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Observation)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- OBSERVATION end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>]</p></td>
      <td><p>--- ORDER_DETAIL end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[{FT1}]</p></td>
      <td><p>Financial Transaction</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{CTI}]</p></td>
      <td><p>Clinical Trial Identification</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[BLG]</p></td>
      <td><p>Billing</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>}</p></td>
      <td><p>--- ORDER end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **ORM^O01** du flux 2 permet au système demandeur de notifier au système effecteur **l’annulation d’une demande d’examen d’imagerie précédemment transmise**.

Les segments **ORC** et **OBR** assurent l’identification de la demandee concernée et portent les informations nécessaires à sa mise à jour dans les systèmes récepteurs, conformément aux règles définies par le profil **IHE SWF**.

Le diagramme ci-dessous illustre le **fonctionnement du message d’annulation** :

<br>

##### Flux 3 - Message ORU^R01^ORU_R01 en HL7 v2.5.1

Le flux 3 repose sur l’échange d’un message **ORU^R01** conforme à la norme **HL7 v2.5.1**.  
Il est utilisé pour la **réponse à une demande d’examen d’imagerie**, en particulier pour notifier la **décision du médecin effecteur** (approbation/refus de la demande).

Contrairement aux flux 1 et 2, ce flux **ne s’appuie sur aucun profil IHE** existant.  
En effet, les cas d’usage couverts par ce flux, notamment la transmission d’une décision médicale en réponse à une demande d’imagerie, ne disposent pas d’un équivalent direct dans les profils IHE RAD.  
Le message ORU^R01 est donc défini sur la base du standard HL7 v2.5.1, complété par une **surcouche de contraintes spécifiques au volet Téléradiologie**.

###### Description technique

Le message est structuré autour des segments suivants :

- **MSH** : en-tête du message et informations de routage
- **PID** : identification du patient
- **ORC / OBR** : décision du médecin effecteur sur la demande d’examen (validation ou refus), avec la possibilité de préciser un **motif de refus** le cas échéant
- **Groupes OBSERVATION (OBX)** : transmission des informations spécifiques au volet Téléradiologie, notamment le **protocole d’imagerie**, exprimé soit en clair, soit sous forme de contenu encapsulé.

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments, ainsi que leur caractère requis, optionnel ou répétable **conformément au volet Téléradiologie**.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th><p>Segment</p></th>
      <th><p>Meaning</p></th>
      <th><p>Usage</p></th>
      <th><p>Card.</p></th>
      <th><p>§ HL7</p></th>
    </tr>
    <tr>
      <td><p>MSH</p></td>
      <td><p>Message Header</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{SFT}]</p></td>
      <td><p>Software Segment</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>{</p></td>
      <td><p>--- PATIENT_RESULT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[</p></td>
      <td><p>--- PATIENT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>PID</p></td>
      <td><p>Patient Identification</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PD1]</p></td>
      <td><p>Additional Demographics</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Patient)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{NK1}]</p></td>
      <td><p>Next of Kin / Associated Parties</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[</p></td>
      <td><p>--- VISIT begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>PV1</p></td>
      <td><p>Patient Visit</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PV2]</p></td>
      <td><p>Patient Visit – Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>]</p></td>
      <td><p>--- VISIT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>]</p></td>
      <td><p>--- PATIENT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>{</p></td>
      <td><p>--- ORDER_OBSERVATION begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>ORC</p></td>
      <td><p>Common Order</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>OBR</p></td>
      <td><p>Observation Request</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Order)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- TIMING_QTY begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>TQ1</p></td>
      <td><p>Timing / Quantity</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[{TQ2}]</p></td>
      <td><p>Timing / Quantity Order Sequence</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- TIMING_QTY end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[CTD]</p></td>
      <td><p>Contact Data</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>11</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- OBSERVATION begin</p></td>
      <td><p>C</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>OBX</p></td>
      <td><p>Observation / Result</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Observation)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- OBSERVATION end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[{FT1}]</p></td>
      <td><p>Financial Transaction</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{CTI}]</p></td>
      <td><p>Clinical Trial Identification</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- SPECIMEN begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>SPM</p></td>
      <td><p>Specimen</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[{OBX}]</p></td>
      <td><p>Observation related to Specimen</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- SPECIMEN end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>}</p></td>
      <td><p>--- ORDER_OBSERVATION end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>}</p></td>
      <td><p>--- PATIENT_RESULT end</p></td>
      <td><p> </p></td>
      <td><p> </p></td>
      <td><p> </p></td>
    </tr>
    <tr>
      <td><p>[DSC]</p></td>
      <td><p>Continuation Pointer</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>2</p></td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **ORU^R01** du flux 3 permet au système effecteur de transmettre au système demandeur la **réponse à la demande d’examen d’imagerie**.

Le segment **ORC** porte la **décision du médecin effecteur**, exprimée de manière :
- validation de la demande d’examen ;
- ou refus de la demande, accompagné le cas échéant d’un **motif de refus** optionnel.

Le segment **OBR** rappelle l’identification de la demande d'examen d'imagerie.

Le **groupe OBSERVATION (OBX)** est **conditionné à la valeur du champ ORC-1**. Il est **optionnel en cas de refus de la demande** et **obligatoire en cas d’acceptation**, afin de permettre la transmission d’**un ou plusieurs protocoles d’imagerie** selon l’une des modalités suivantes :

- protocole exprimé en clair dans le message
- protocole encapsulé sous forme de contenu binaire

Ces OBSERVATION sont structurées et identifiées conformément aux règles définies dans la partie [Contraintes applicables aux profils de message](./specifications_techniques.html#flux-3---réponse-à-la-demande-dexamen-dimagerie), notamment via l’utilisation de codes locaux dans **OBX-3**.

Le diagramme ci-dessous illustre le **fonctionnement du flux 3** :

<br>

##### Flux 4 - Message OMI^O23^OMI_023 en HL7 v2.5.1

Le flux 4 repose sur l’échange d’un message **OMI^O23** conforme à la norme **HL7 v2.5.1**.  
Il est utilisé pour la **transmission d’informations complémentaires post-acte** à la suite de la réalisation d’un examen d’imagerie dans le cadre du volet Téléradiologie.

Le message **OMI^O23** permet de transmettre des informations qui ne sont pas nécessairement disponibles au moment de la construction de la demande d'examen, mais qui sont connues **après la réalisation effective de l’examen**.

Bien que le message **OMI^O23** soit décrit dans le **profil IHE RAD – Scheduled Workflow (SWF)**, le cas d’usage couvert par IHE ne répond pas entièrement aux besoins spécifiques du volet **Téléradiologie**.  
En conséquence, le message **OMI^O23** est défini sur la base du **standard HL7 v2.5.1** et enrichi par une **surcouche de contraintes propres au volet Téléradiologie**.  

###### Description technique

Le message est structuré autour des segments suivants :

- **MSH** : en-tête du message et informations de routage
- **PID / PV1** : identification du patient et du contexte de prise en charge
- **ORC** : informations de demande initiale
- **OBR** : informations relatives à l’examen réalisé
- **TQ1** : informations temporelles, notamment la date de réalisation de l’examen et la durée de rétention des images
- **IPC** : informations relatives à l'examen d'imagerie
- **Groupes OBSERVATION (OBX)** : transmission des compléments d’information post-acte spécifiques au volet Téléradiologie

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments ainsi que leur caractère requis, optionnel ou répétable.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th><p>Segment</p></th>
      <th><p>Meaning</p></th>
      <th><p>Usage</p></th>
      <th><p>Card.</p></th>
      <th><p>§ HL7</p></th>
    </tr>
    <tr>
      <td><p>MSH</p></td>
      <td><p>Message Header</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{SFT}]</p></td>
      <td><p>Software Segment</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Header)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[</p></td>
      <td><p>--- PATIENT begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>PID</p></td>
      <td><p>Patient Identification</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PD1]</p></td>
      <td><p>Additional Demographics</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Patient)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[</p></td>
      <td><p>--- PATIENT_VISIT begin</p></td>
      <td><p>R</p></td>
      <td><p>[R..1]</p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>PV1</p></td>
      <td><p>Patient Visit</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>[PV2]</p></td>
      <td><p>Patient Visit – Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>]</p></td>
      <td><p>--- PATIENT_VISIT end</p></td>
      <td><p></p></td>
      <td><p></p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- INSURANCE begin</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>IN1</p></td>
      <td><p>Insurance</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[IN2]</p></td>
      <td><p>Insurance Additional Info</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[IN3]</p></td>
      <td><p>Insurance Additional Info – Cert.</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- INSURANCE end</p></td>
      <td><p></p></td>
      <td><p></p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>[GT1]</p></td>
      <td><p>Guarantor</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{AL1}]</p></td>
      <td><p>Allergy Information</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>3</p></td>
    </tr>
    <tr>
      <td><p>]</p></td>
      <td><p>--- PATIENT end</p></td>
      <td><p></p></td>
      <td><p></p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>{</p></td>
      <td><p>--- ORDER begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..*]</p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>ORC</p></td>
      <td><p>Common Order</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- TIMING begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..*]</p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>TQ1</p></td>
      <td><p>Timing / Quantity</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[{TQ2}]</p></td>
      <td><p>Timing / Quantity Order Sequence</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- TIMING end</p></td>
      <td><p></p></td>
      <td><p></p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>OBR</p></td>
      <td><p>Observation Request</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Order)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>[CTD]</p></td>
      <td><p>Contact Data</p></td>
      <td><p>O</p></td>
      <td><p>[0..1]</p></td>
      <td><p>11</p></td>
    </tr>
    <tr>
      <td><p>[{DG1}]</p></td>
      <td><p>Diagnosis</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>6</p></td>
    </tr>
    <tr>
      <td><p>[{</p></td>
      <td><p>--- OBSERVATION begin</p></td>
      <td><p>R</p></td>
      <td><p>[1..*]</p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>OBX</p></td>
      <td><p>Observation / Result</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>7</p></td>
    </tr>
    <tr>
      <td><p>[{NTE}]</p></td>
      <td><p>Notes and Comments (Observation)</p></td>
      <td><p>O</p></td>
      <td><p>[0..*]</p></td>
      <td><p>2</p></td>
    </tr>
    <tr>
      <td><p>}]</p></td>
      <td><p>--- OBSERVATION end</p></td>
      <td><p></p></td>
      <td><p></p></td>
      <td><p></p></td>
    </tr>
    <tr>
      <td><p>IPC</p></td>
      <td><p>Imaging Procedure Control</p></td>
      <td><p>R</p></td>
      <td><p>[1..1]</p></td>
      <td><p>4</p></td>
    </tr>
    <tr>
      <td><p>}</p></td>
      <td><p>--- ORDER end</p></td>
      <td><p></p></td>
      <td><p></p></td>
      <td><p></p></td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **OMI^O23** du flux 4 permet au système demandeur (RIS) de transmettre au système effecteur (SI de Téléradiologie) des **compléments d’information post-acte** relatifs à un examen d’imagerie déjà réalisé.

Les segments **ORC** et **OBR** assurent le **rattachement** de ces informations à la demande d’examen initiale.

Les **groupes OBSERVATION (OBX)** jouent un rôle central dans ce flux.  
Ils permettent notamment de véhiculer :

- des éléments constitutifs de l’**URL de la visionneuse DRIMbox** donnant accès aux images ;
- le **code de l'acte d'imagerie** réalisée
- la **modalité d'imagerie** utilisée lors de l'examen
- les informations relatives aux **produits administrés** dans le cadre de la procédure (type, numéro de lot, quantité) ;
- les informations sur l’**appareil d’imagerie utilisé** ;
- la **localisation anatomique** ciblée par l'examen et les éventuelles précisions topographiques associées.

L’utilisation de ces groupes OBSERVATION est encadrée par des règles de structuration, de codification et de liaison entre segments, définies dans la partie relatives aux [contraintes spécifiques du volet](./specifications_techniques.html#flux-4----transmission-dun-complément-dinformation-post-acte).

Le diagramme ci-dessous illustre le **fonctionnement du flux 4** :

<div class="figure" style='text-align: center;'>
    <img src="fig17.png" alt="Figure 17" title="Figure 17 : Structure fonctionnelle du message ORU_R01" style="width:80%;">
    <figcaption><b>Figure 17 : Structure fonctionnelle du message ORU_R01</b></figcaption>
</div>

<br>

##### Acquittements

Pour l’ensemble des flux décrits ci-dessus, les messages HL7 font l’objet d’un **acquittement technique HL7 v2** (ACK). Les mécanismes d’acquittement s’appuient sur les fonctionnalités natives du standard HL7 v2.5.1.
Les règles applicables à la structure et au contenu des messages d’acquittement sont décrites ultérieurement dans [une partie dédiée](./acquittement.html).

###### Profil du message ACK

Le profil du message ACK est le suivant :

<table class="table-hl7v2">
  <tbody>
  <tr>
    <th>
      <p>Segment</p>
    </th>
    <th>
      <p>Meaning</p>
    </th>
    <th>
      <p>Usage</p>
    </th>
    <th>
      <p>Card.</p>
    </th>
    <th>
      <p>HL7 §</p>
    </th>
  </tr>
    <tr>
      <td>
        <p>MSH</p>
      </td>
      <td>
        <p>Message header</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>2</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>[{SFT}]</p>
      </td>
      <td>
        <p>Software segment</p>
      </td>
      <td>
        <p>O</p>
      </td>
      <td>
        <p>[0..*]</p>
      </td>
      <td>
        <p>2</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>[UAC]</p>
      </td>
      <td>
        <p>User Authentication credential- Utilisé uniquement dans la version 2.6</p>
      </td>
      <td>
        <p>O</p>
      </td>
      <td>
        <p>[0..1]</p>
      </td>
      <td>
        <p>2</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSA</p>
      </td>
      <td>
        <p>Message Acknowledgement</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>2</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>[{ERR}]</p>
      </td>
      <td>
        <p>Error</p>
      </td>
      <td>
        <p>C</p>
      </td>
      <td>
        <p>[0..*]</p>
      </td>
      <td>
        <p>2</p>
      </td>
    </tr>
  </tbody>
</table>
