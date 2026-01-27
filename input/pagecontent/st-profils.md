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

Le développeur doit valoriser tous les segments et champs obligatoiresdes messages HL7v2 afin de répondre au standard d'interopérabilité des messages.

Ci-dessous sont représentées les structures de messages HL7v2 proposées pour la transmission de document(s) CDA-R2 en HL7v2.

##### Flux 1 - Message ORM^O01^ORM_O01 en HL7 v2.5.1

Le flux 1 repose sur l’échange d’un message **ORM^O01** conforme à la norme **HL7 v2.5.1**, utilisé pour la **transmission d’une demande d’examen d’imagerie** dans le cadre du volet Téléradiologie.

La structure du message est **conforme au profil IHE RAD – Scheduled Workflow (SWF)**. Une **surcouche de contraintes spécifiques Téléradiologie** vient compléter ce cadre afin de couvrir des besoins fonctionnels non pris en charge nativement par IHE SWF.

###### Description technique

Le message est composé des segments principaux suivants :

- **MSH** : en-tête du message et informations de routage ;
- **PID / PV1** : identification du patient et du contexte de prise en charge ;
- **ORC** : informations de commande de l’examen, conformément à IHE SWF ;
- **OBR** : prescription de l’examen d’imagerie (modalité, indications, antécédents), conformément à IHE SWF ;
- **Groupes OBSERVATION (OBX)** : portage d’informations complémentaires spécifiques au volet Téléradiologie, non contraintes par IHE SWF.

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments ainsi que leur caractère requis, optionnel ou répétable.

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
      <p>§ HL7</p>
    </th>
  </tr>
    <tr>
      <td>
        <p>MSH</p>
      </td>
      <td>
        <p>Message Header</p>
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
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> PID</p>
      </td>
      <td>
        <p>Patient Identification</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  PV1</p>
      </td>
      <td>
        <p>Patient Visit</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>{</p>
      </td>
      <td>
        <p>--- ORDER begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> ORC</p>
      </td>
      <td>
        <p>Common Order : **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>{</p>
      </td>
      <td>
        <p>--- ORDER_DETAIL begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> OBR</p>
      </td>
      <td>
        <p>Observation Request</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> [{NTE}]</p>
      </td>
      <td>
        <p>Comments on the order</p>
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
        <p> {</p>
      </td>
      <td>
        <p>--- OBSERVATION begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  OBX</p>
      </td>
      <td>
        <p>Le cas échéant, véhicule le protocole d'imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>7</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  [{NTE}]</p>
      </td>
      <td>
        <p>Comment of the result</p>
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
        <p> }</p>
      </td>
      <td>
        <p>--- OBSERVATION end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **ORM^O01** du flux 1 permet au système demandeur de transmettre au système réalisateur l’ensemble des informations nécessaires à la **prise en charge et à la planification d’un examen d’imagerie dans un contexte de Téléradiologie**.

Outre les éléments standards de commande et de prescription portés par les segments **ORC** et **OBR**, ce flux s’appuie sur des **groupes OBSERVATION (OBX)** afin de véhiculer des informations fonctionnelles complémentaires indispensables à la bonne réalisation de l’examen, telles que :
- la **localisation anatomique** et, le cas échéant, une **précision topographique**
- des **données patient pertinentes** pour l’examen (taille, poids, statut de grossesse)

Ces groupes OBSERVATION sont **contraints par la présente spécification**, tant sur le plan sémantique que structurel (identification des OBX, cardinalités, types de données), afin de garantir une interprétation homogène par l’ensemble des acteurs.

Le diagramme ci-dessous illustre le **fonctionnement global du message**, les interactions entre les segments principaux ainsi que le rôle des **OBX spécifiques Téléradiologie** dans le cadre du flux 1.

<br>

##### Flux 2 - Message ORM^O01^ORM_O01 en HL7 v2.5.1

Le flux 2 repose sur l’échange d’un message **ORM^O01** conforme à la norme **HL7 v2.5.1**, utilisé pour **l' annulation de demande d’examen d’imagerie** dans le cadre du volet Téléradiologie.

Ce flux est **structurellement très proche du flux 1** et s’appuie lui aussi sur le **profil IHE RAD – Scheduled Workflow (SWF)**, notamment pour les segments **ORC** et **OBR**, qui conservent les mêmes principes de structuration et de valorisation que pour la demande initiale.

La principale différence avec le flux 1 concerne l’utilisation du **groupe OBSERVATION (OBX)** qui est optionnel dans le cadre de ce flux.

###### Description technique

Le message est composé des segments principaux suivants :

- **MSH** : en-tête du message et informations de routage
- **PID / PV1** : identification du patient et du contexte de prise en charge
- **ORC** : informations de demande, avec une action positionnée à l’annulation
- **OBR** : rappel des éléments de prescription nécessaires à l’identification de la demande annulée

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
      <p>§ HL7</p>
    </th>
  </tr>
    <tr>
      <td>
        <p>MSH</p>
      </td>
      <td>
        <p>Message Header</p>
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
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> PID</p>
      </td>
      <td>
        <p>Patient Identification</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  PV1</p>
      </td>
      <td>
        <p>Patient Visit</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>{</p>
      </td>
      <td>
        <p>--- ORDER begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> ORC</p>
      </td>
      <td>
        <p>Common Order : **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>{</p>
      </td>
      <td>
        <p>--- ORDER_DETAIL begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> OBR</p>
      </td>
      <td>
        <p>Observation Request</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> [{NTE}]</p>
      </td>
      <td>
        <p>Comments on the order</p>
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
        <p> {</p>
      </td>
      <td>
        <p>--- OBSERVATION begin</p>
      </td>
      <td>
        <p>O</p>
      </td>
      <td>
        <p>[0..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  OBX</p>
      </td>
      <td>
        <p>Le cas échéant, véhicule le protocole d'imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>7</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  [{NTE}]</p>
      </td>
      <td>
        <p>Comment of the result</p>
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
        <p> }</p>
      </td>
      <td>
        <p>--- OBSERVATION end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
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
Il est utilisé pour la **réponse à une demande d’examen d’imagerie**, en particulier pour notifier la **décision du médecin effecteur**.

Contrairement aux flux 1, 2 et 4, ce flux **ne s’appuie sur aucun profil IHE** existant.  
En effet, les cas d’usage couverts par ce flux, notamment la transmission d’une décision médicale structurée en réponse à une demande d’imagerie, ne disposent pas d’un équivalent direct dans les profils IHE RAD.  
Le message ORU^R01 est donc défini sur la base du standard HL7 v2.5.1, complété par une **surcouche de contraintes spécifiques au volet Téléradiologie**.

###### Description technique

Le message est structuré autour des segments suivants :

- **MSH** : en-tête du message et informations de routage
- **PID / PV1** : identification du patient et du contexte de prise en charge
- **ORC** : décision du médecin effecteur sur la demande d’examen (validation ou refus), avec la possibilité de préciser un **motif de refus** le cas échéant
- **OBR** : rappel de la demande d’examen concernée
- **Groupes OBSERVATION (OBX)** : transmission des informations spécifiques au volet Téléradiologie, notamment le **protocole d’imagerie**, exprimé soit en clair, soit sous forme de contenu encapsulé.

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments, ainsi que leur caractère requis, optionnel ou répétable.

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
      <p>§ HL7</p>
    </th>
  </tr>
    <tr>
      <td>
        <p>MSH</p>
      </td>
      <td>
        <p>Message Header</p>
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
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_RESULT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> PID</p>
      </td>
      <td>
        <p>Patient Identification</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  PV1</p>
      </td>
      <td>
        <p>Patient Visit</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>{</p>
      </td>
      <td>
        <p>--- ORDER_OBSERVATION begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> ORC</p>
      </td>
      <td>
        <p>Common Order : **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> OBR</p>
      </td>
      <td>
        <p>Observation Request</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> [{NTE}]</p>
      </td>
      <td>
        <p>Comments on the order</p>
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
        <p>[{</p>
      </td>
      <td>
        <p>--- TIMING begin</p>
      </td>
      <td>
        <p>O</p>
      </td>
      <td>
        <p>[0..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> TQ1</p>
      </td>
      <td>
        <p>Timing Quantity</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>}]</p>
      </td>
      <td>
        <p>--- TIMING end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> {</p>
      </td>
      <td>
        <p>--- OBSERVATION begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  OBX</p>
      </td>
      <td>
        <p>Le cas échéant, véhicule le protocole d'imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>7</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  [{NTE}]</p>
      </td>
      <td>
        <p>Comment of the result</p>
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
        <p> }</p>
      </td>
      <td>
        <p>--- OBSERVATION end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **ORU^R01** du flux 3 permet au système réalisateur de transmettre au système demandeur la **réponse à la demande d’examen d’imagerie**.

Le segment **ORC** porte la **décision du médecin effecteur**, exprimée de manière structurée :
- validation de la demande d’examen ;
- ou refus de la demande, accompagné le cas échéant d’un **motif de refus** optionnel.

Le segment **OBR** rappel l’identification de la demande.

Le **groupe OBSERVATION (OBX)** est **requis dans ce flux** et permet de véhiculer le **protocole d’imagerie**, selon l’une des modalités suivantes :

- protocole exprimé en clair dans le message
- protocole encapsulé sous forme de contenu binaire

Ces OBSERVATION sont structurées et identifiées conformément aux règles définies dans la surcouche Téléradiologie, notamment via l’utilisation de codes locaux dans **OBX-3**.

Le diagramme ci-dessous illustre le **fonctionnement du flux 3** :

<br>

##### Flux 4 - Message OMI^O23^OMI_023 en HL7 v2.5.1

Le flux 4 repose sur l’échange d’un message **OMI^O23** conforme à la norme **HL7 v2.5.1**.  
Il est utilisé pour la **transmission d’informations complémentaires post-acte** à la suite de la réalisation d’un examen d’imagerie dans le cadre du volet Téléradiologie.

Ce flux s’appuie sur les principes du **profil IHE RAD – Scheduled Workflow (SWF)**, dans la mesure où il s’inscrit dans la continuité du cycle de vie de la demande d’examen d’imagerie et de sa réalisation.  
Les segments structurants du message, notamment **ORC** et **OBR**, sont ainsi valorisés conformément aux règles définies par IHE SWF, complétées par une **surcouche de contraintes spécifiques au volet Téléradiologie**.

Le message **OMI^O23** permet de transmettre des informations qui ne sont pas nécessairement disponibles au moment de la prescription ou de la réponse à la demande, mais qui sont connues **après la réalisation effective de l’examen**.

###### Description technique

Le message est structuré autour des segments suivants :

- **MSH** : en-tête du message et informations de routage
- **PID / PV1** : identification du patient et du contexte de prise en charge
- **ORC** : informations de demande initiale
- **OBR** : informations relatives à l’examen réalisé
- **TQ1** : informations temporelles, notamment la date de réalisation de l’examen et la durée de rétention des images
- **IPC** : informations relatives à l'examen d'imagerie et a la modalité
- **Groupes OBSERVATION (OBX)** : transmission des compléments d’information post-acte spécifiques au volet Téléradiologie

Le tableau ci-dessous décrit la **structure HL7 v2 du message**, l’ordre des segments ainsi que leur caractère requis, optionnel ou répétable.

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
      <p>§ HL7</p>
    </th>
  </tr>
    <tr>
      <td>
        <p>MSH</p>
      </td>
      <td>
        <p>Message Header</p>
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
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> PID</p>
      </td>
      <td>
        <p>Patient Identification</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  PV1</p>
      </td>
      <td>
        <p>Patient Visit</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT_VISIT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> </p>
      </td>
      <td>
        <p>--- PATIENT end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>{</p>
      </td>
      <td>
        <p>--- ORDER begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> ORC</p>
      </td>
      <td>
        <p>Common Order : **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> OBR</p>
      </td>
      <td>
        <p>Observation Request</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p> [{NTE}]</p>
      </td>
      <td>
        <p>Comments on the order</p>
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
        <p>[{</p>
      </td>
      <td>
        <p>--- TIMING begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> TQ1</p>
      </td>
      <td>
        <p>Timing Quantity</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>}]</p>
      </td>
      <td>
        <p>--- TIMING end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p> {</p>
      </td>
      <td>
        <p>--- OBSERVATION begin</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  OBX</p>
      </td>
      <td>
        <p>Le cas échéant, véhicule le protocole d'imagerie</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..1]</p>
      </td>
      <td>
        <p>7</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  [{NTE}]</p>
      </td>
      <td>
        <p>Comment of the result</p>
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
        <p> }</p>
      </td>
      <td>
        <p>--- OBSERVATION end</p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>  IPC</p>
      </td>
      <td>
        <p>Imaging Procedure Control Segment</p>
      </td>
      <td>
        <p>R</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p>4</p>
      </td>
    </tr>
  </tbody>
</table>

###### Description fonctionnelle

Le message **OMI^O23** du flux 4 permet au système réalisateur de transmettre au système demandeur des **compléments d’information post-acte** relatifs à un examen d’imagerie déjà réalisé.

Les segments **ORC** et **OBR** assurent le **rattachement** de ces informations à la demande d’examen initiale, conformément aux règles du profil **IHE SWF** et aux contraintes spécifiques définies par le volet Téléradiologie.

Les **groupes OBSERVATION (OBX)** jouent un rôle central dans ce flux.  
Ils permettent notamment de véhiculer :

- l’**URL de la visionneuse DRIMbox** donnant accès aux images ;
- les informations relatives aux **produits administrés** (type, numéro de lot, quantité) ;
- les informations sur l’**appareil d’imagerie utilisé** ;
- la **localisation anatomique** et les éventuelles précisions topographiques associées.

L’utilisation de ces groupes OBSERVATION est encadrée par des règles de structuration, de codification et de liaison entre segments, définies dans la surcouche Téléradiologie.

Le diagramme ci-dessous illustre le **fonctionnement du flux 4** :

<div class="figure" style='text-align: center;'>
    <img src="fig17.png" alt="Figure 17" title="Figure 17 : Structure fonctionnelle du message ORU_R01" style="width:80%;">
    <figcaption><b>Figure 17 : Structure fonctionnelle du message ORU_R01</b></figcaption>
</div>
<br>

Les groupes en rouge sur le schéma représentent les éléments spécifiques à ce volet :

-   Un premier groupe de segments OBSERVATION contenant le document
    médical au format CDA-R2 codé en base64 suivi de segments PRT,
    pré-adoptés depuis la version 2.9 du standard, permettant ainsi de
    renseigner le cas échéant les informations de l'expéditeur, le(s)
    destinataire(s) MSSanté et l'adresse mail de réponse.

-   Un deuxième groupe OBSERVATION contenant le cas échéant le même
    document médical spécifié dans un autre format, codé en base64. Le
    contenu clinique des documents est identique, seul le format est
    différent. Cette possibilité n'est pas utilisée dans le contexte du
    SEGUR vague2 (la version PDF du compte-rendu est insérée dans une
    section dédiée du document CDA Niv3).

Les groupes de segments OBSERVATION suivants (répétables) véhiculent les métadonnées spécifiques à la publication sur le DMP et/ou à l'envoi par la MSSanté. Ces métadonnées sont communes aux deux formats du document. Ces métadonnées sont décrites dans la [section dédiée](volume2.html#contraintes-appliqu%C3%A9es-aux-messages-mdm-et-oru-dans-le-contexte-de-ce-volet).

<br>

#### Réponses et acquittements

Pour l’ensemble des flux décrits ci-dessus :
- Les messages HL7 font l’objet d’un **acquittement technique HL7 v2** (`ACK`) ;
- Les règles d’acquittement suivent les mécanismes natifs du standard HL7 v2.5.1.

Les modalités d’acquittement applicatif, le cas échéant, sont précisées dans les sections dédiées de la présente spécification.