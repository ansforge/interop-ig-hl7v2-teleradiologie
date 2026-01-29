##### Flux 1 - Transmission de la demande d'examen d'imagerie

Ce flux repose sur l’utilisation d'un messages **ORM^O01**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les **groupes OBSERVATION** (segments OBX), non contraints et optionnels dans le cadre du profil IHE SWF, sont **explicitement contraints par le volet téléradiologie**. Ces contraintes permettent notamment de structurer et de normaliser la transmission d’informations complémentaires nécessaires à la compréhension de la demande d’examen d’imagerie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie.  

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du segment ORC : Usage = Required / Cardinalité = [1..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment ORC</strong></p>
      </td>
      <td>
        <p><strong>Common Order</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-1</p>
      </td>
      <td>
        <p>Order control</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">NW</span> » (New order/service)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-2</p>
      </td>
      <td>
        <p>Placer Order Number</p>
      </td>
      <td>
        <p>Identifiant de la demande d'examen d'imagerie (Order Placer Number)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-9</p>
      </td>
      <td>
        <p>Date/Time of Transaction</p>
      </td>
      <td>
        <p>Date à laquelle la demande d'examen a été réalisée</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-11 (Requis si connu)</p>
      </td>
      <td>
        <p>Verified By</p>
      </td>
      <td>
        <p>Informations relatives au professionnel de santé effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie</p>
        <p>Ce champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-12</p>
      </td>
      <td>
        <p>Ordering Provider</p>
      </td>
      <td>
        <p>Informations relatives au professionnel de santé responsable de la structure d’imagerie qui accueille le patient et supervise la réalisation de l’acte d’imagerie</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-12.1</p>
      </td>
      <td>
        <p>Person Identifier</p>
      </td>
      <td>
        <p>Identifiant du professionnel</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-12.2</p>
      </td>
      <td>
        <p>Family Name</p>
      </td>
      <td>
        <p>Nom d'exercice du professionnel</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-12.3</p>
      </td>
      <td>
        <p>Given Name</p>
      </td>
      <td>
        <p>Prénom d'exercice du professionnel</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-12.9</p>
      </td>
      <td>
        <p>Assigning Authority</p>
      </td>
      <td>
        <p>Autorité d'affectation de l'identifiant du PS</p>
      </td>
    </tr>    
    <tr>
      <td>
        <p>&gt; &gt; ORC-12.9.1 (optionnel)</p>
      </td>
      <td>
        <p>Namespace Id</p>
      </td>
      <td>
        <p>Nom de l'aurotité d'affectation</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; &gt; ORC-12.9.2</p>
      </td>
      <td>
        <p>Universal Id</p>
      </td>
      <td>
        <p>Autorité d'affectation de l'identifiant du PS (OID de gestion de personnes) : <span class="hl7-color">1.2.250.1.71.4.2.1</span></p>
      </td>
    </tr>
        <tr>
      <td>
        <p>&gt; &gt; ORC-12.9.3</p>
      </td>
      <td>
        <p>Universal Id Type</p>
      </td>
      <td>
        <p><span class="hl7-color">ISO</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-12.13</p>
      </td>
      <td>
        <p>Identifier Type Code</p>
      </td>
      <td>
        <p>Type d'identifiant du professionnel (valeur issue de la <a href="https://www.interopsante.org/publications">Table 0203 - Interop'Santé</a> présent dan le document "Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure dans le périmètre d’IHE France")</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-14 (Requis si connu)</p>
      </td>
      <td>
        <p>Call Back Phone Number</p>
      </td>
      <td>
        <p>Numéro de téléphone à appeler pour obtenir des précisions sur la demande d'examen d'imagerie</p>
        <p>Ce champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-17</p>
      </td>
      <td>
        <p>Entering Organization</p>
      </td>
      <td>
        <p>Qualifie le type d'organisation  (5)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-17.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">STRUCTURE_IMAGERIE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-17.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">TLR_TYPE_ORGANISATION</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-21</p>
      </td>
      <td>
        <p>Ordering Facility Name</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-21.1</p>
      </td>
      <td>
        <p>OrganizationName</p>
      </td>
      <td>
        <p>Nom de l'organisation (structure d'imagerie)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-21.6</p>
      </td>
      <td>
        <p>Assigning Authority</p>
      </td>
      <td>
        <p>Autorité d'affectation de l'identifiant de l'organisation</p>
        <p><span class="hl7-color">1.2.250.1.71.4.2.2</span> (OID de gestion des structures pour préciser une entité juridique ou une entité géographique), N° FINESS ou N° FINEG pour identifier une organisation intra-établissement (service, UF, pôle…).</p>
        <p><a href="https://www.interopsante.org/publications">Cf Contraintes sur les types de données HL7 v2.5 applicables aux profils d'intégration du cadre technique IT Infrastructure dans le périmètre d'IHE France</a>.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-21.7</p>
      </td>
      <td>
        <p>Identifier Type Code</p>
      </td>
      <td>
        <p>Type d'identifiant (valeur issue de la <a href="https://www.interopsante.org/publications">Table 0203 - Interop'Santé</a> présent dan le document "Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure dans le périmètre d’IHE France") : <span class="hl7-color">FINEJ</span> (FINESS d'entité juridique) ou <span class="hl7-color">FINEG</span> (FINESS d'entité géographique) ou <span class="hl7-color">IDNST</span> ou <span class="hl7-color">UF</span> (UF), <span class="hl7-color">SVR</span> (service).</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; ORC-21.10</p>
      </td>
      <td>
        <p>Organization number</p>
      </td>
      <td>
        <p>Identifiant de l'organisation</p>
      </td>
    </tr>
  </tbody>
</table>

<blockquote class="stu-note">
    <p>
    <b>(5) :</b> Conformément au profil IHE RAD – Scheduled Workflow (SWF), le champ ORC-17 – Entering Organization est renseigné dans les flux concernés.
    Dans le cadre du volet Téléradiologie, ce champ est utilisé pour qualifier le type d’organisation à l’origine du message (par exemple : structure d’imagerie, plateforme de téléradiologie), sur la base d’une <a href="./table_orga.html">table de valeurs locale documentée</a>.

    L’identification de l’organisation est portée dans le champ ORC-21 – Ordering Facility Name, de type XON, permettant de véhiculer un identifiant structuré et pérenne, conformément aux principes retenus dans le CI-SIS.
    Ce découplage permet de respecter les exigences IHE tout en garantissant une identification robuste.
    </p>
</blockquote>

##### Segment OBR (Observation Request)

Le segment **OBR** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Dans le cadre du volet **Téléradiologie**, le champ **OBR-4 – Universal Service Identifier** est utilisé afin de véhiculer un **code local identifiant la procédure métier portée par le message**.
Les valeurs autorisées dans **OBR-4** sont définies dans une [table de codes locaux](./table_obr.html), commune à l’ensemble des flux du volet Téléradiologie.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du segment OBR : Usage = Required / Cardinalité = [1..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBR</strong></p>
      </td>
      <td>
        <p><strong>Observation Request</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBR-2</p>
      </td>
      <td>
        <p>Placer Order Number</p>
      </td>
      <td>
        <p>Identifiant de la demande d'examen (identique à l'ORC-2)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBR-4</p>
      </td>
      <td>
        <p>Universal Service Identifier</p>
      </td>
      <td>
        <p>Code local identifiant la procédure métier portée par le message </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBR-4.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">TRANSMISSION_DEMANDE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBR-4.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Transmission d’une demande d’examen d'imagerie</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBR-4.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color"><span class="hl7-color">TLR_OBR_PROCEDURE</span></span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBR-13</p>
      </td>
      <td>
        <p>Relevant Clinical Information</p>
      </td>
      <td>
        <p>Justification de la demande d'examen</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBR-16</p>
      </td>
      <td>
        <p>Ordering Provider</p>
      </td>
      <td>
        <p>Informations relatives au professionnel de santé responsable (identique à l'ORC-12)</p>
      </td>
    </tr>
  </tbody>
</table>

##### Segment NTE (Notes and Comments)

Le segment **NTE** peut être utilisé en complément du segment **OBR** afin de véhiculer un ou des **commentaires libres** relatifs à la **finalité de l’examen**.

La structure et l’utilisation du segment **NTE** sont **conformes au standard HL7 v2.5.1**. Des **contraintes spécifiques** s’applique toutefois lorsque ce segment est utilisé pour porter des informations relatives à la finalité de l’examen telles que définies dans le présent volet.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du segment NTE : Usage = Optional / Cardinalité = [0..*]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment NTE</strong></p>
      </td>
      <td>
        <p><strong>Notes and Comments</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>NTE-3</p>
      </td>
      <td>
        <p>Comment</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>NTE-4</p>
      </td>
      <td>
        <p>Comment Type</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&gt; NTE-4.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Valeur fixée à : <span class="hl7-color">FINALITE_EXAMEN</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; NTE-4.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">HL70364</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupe OBSERVATION - Modalité d'imagerie

Ce groupe obligatoire est composé d'un segment OBX permettant d’indiquer la **modalité d'imagerie souhaitée** pour l’examen demandé.

Le segment **NTE** peut être utilisé en complément du segment **OBX** afin de véhiculer un ou des **commentaires libres** relatifs à la **modalité d’imagerie demandée**.

###### Segment OBX - Modalité d'imagerie

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">CE</span> (Coded Entry)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">MODALITE_IMAGERIE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Modalité d’imagerie utilisée ou prévue pour réaliser l’examen</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color"><span class="hl7-color">TLR_OBSERVATION</span></span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.1</p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Valeur issue du JDV <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html">JDV_modalitedemandeActeImagerie-CISIS</a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.3</p>
      </td>
      <td>
        <p>Name Of Coding System</p>
      </td>
      <td>
        <p><span class="hl7-color">terminologie-cisis-fr</span> ou <span class="hl7-color">DCM</span> en fonction de l'appartenance du code à l'un des systèmes de codage</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Segment NTE - Commentaire sur la modalité

La structure et l’utilisation du segment **NTE** sont **conformes au standard HL7 v2.5.1**. Des **contraintes spécifiques** s’applique toutefois lorsque ce segment est utilisé pour porter des informations relatives à la modalité d’imagerie, telles que définies dans le présent volet.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du segment NTE : Usage = Optional / Cardinalité = [0..*]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment NTE</strong></p>
      </td>
      <td>
        <p><strong>Notes and Comments</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>NTE-3</p>
      </td>
      <td>
        <p>Comment</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>NTE-4</p>
      </td>
      <td>
        <p>Comment Type</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&gt; NTE-4.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Valeur fixée à : <span class="hl7-color">MODALITE_IMAGERIE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; NTE-4.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">HL70364</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupes OBSERVATION - Localisation anatomique

Ces groupes **OBSERVATION** sont utilisés afin de véhiculer les informations relatives à la **localisation anatomique concernée par la demande d’examen d’imagerie**.
Ces informations permettent de préciser la zone anatomique à explorer et, le cas échéant, d’apporter un niveau de détail complémentaire facilitant l’interprétation et la réalisation de l’examen.

La localisation anatomique est portée par un **premier segment OBX obligatoire**, pouvant être complété par un **second segment OBX optionnel** destiné à préciser la topographie de manière plus fine.
Les segments OBX portant sur la localisation anatomique sont identifiés par un code local "LOCALISATION_ANATOMIQUE" dans **OBX-3**, <a href="./table_obs.html">documenté en annexe</a>. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION - Localisation anatomique principale

Ce groupe est composé d'un segment OBX obligatoire permettant d’indiquer la **localisation anatomique principale** de l’examen demandé.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Required / Cardinalité = [1..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">CE</span> (Coded Entry)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">LOCALISATION_ANATOMIQUE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Localisation anatomique examinée dans le cadre de l’examen d’imagerie</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color"><span class="hl7-color">TLR_OBSERVATION</span></span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-4</p>
      </td>
      <td>
        <p>Observation Sub-ID</p>
      </td>
      <td>
        <p>Valeur fixée à n.1</p>
        <p><strong>Voir règle commune d’utilisation du Sub-ID : </strong><a href ="./sub-id.html">Utilisation du champ OBX-4 </a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.1</p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Valeur issue du JDV <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-region-anatomique-cisis.html">JDV_RegionAnatomique-CISIS</a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.3</p>
      </td>
      <td>
        <p>Name Of Coding System</p>
      </td>
      <td>
        <p><span class="hl7-color">SNT</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>

###### Groupe OBSERVATION - Précision topographique

Ce groupe est composé d'un segment OBX optionnel permettant de compléter la localisation anatomique principale par une **précision topographique**.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">CE</span> (Coded Entry)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">LOCALISATION_ANATOMIQUE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Localisation anatomique examinée dans le cadre de l’examen d’imagerie</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color"><span class="hl7-color">TLR_OBSERVATION</span></span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-4</p>
      </td>
      <td>
        <p>Observation Sub-ID</p>
      </td>
      <td>
        <p>Valeur fixée à n.2</p>
        <p><strong>Voir règle commune d’utilisation du Sub-ID : </strong><a href ="./sub-id.html">Utilisation du champ OBX-4 </a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.1</p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Valeur issue du JDV <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modificateur-topographique-cisis.html">JDV_ModificateurTopographique-CISIS</a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.3</p>
      </td>
      <td>
        <p>Name Of Coding System</p>
      </td>
      <td>
        <p><span class="hl7-color">SNT</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupe OBSERVATION - Antécédents

Ce groupe **OBSERVATION** optionnel et répétable permet de véhiculer les **antécédents médicaux du patient jugés pertinents pour la réalisation de l’examen d’imagerie**.

Les antécédents sont transmis sous forme de texte libre dans le champ **OBX-5**. Le champ **OBX-8**, optionnel, est utilisé comme indicateur de pertinence, permettant de qualifier le niveau d’impact des antécédents transmis vis-à-vis de l’examen d’imagerie demandé.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">FT</span> (Formated Text)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">11322-5</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">History of General health Narrative</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">LN</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p>Antécédents</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-8 (optionnel)</p>
      </td>
      <td>
        <p>Abnormal flag</p>
      </td>
      <td>
        <p>Pertinence de l'antécédent</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-8.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Valeur possible :</p>
        <p><span class="hl7-color">SANS_IMPACT</span></p>
        <p><span class="hl7-color">PERTINENT</span></p>
        <p><span class="hl7-color">MAJEUR</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">HL70078</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupe OBSERVATION - Taille corporelle

Ce groupe **OBSERVATION** optionnel est utilisé afin de véhiculer la **taille corporelle du patient**, lorsque celle-ci est nécessaire à la réalisation de l’examen d’imagerie. La taille du patient est véhiculée par l'intermédiaire d'un segment OBX.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">NM</span> (Numeric)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">8302-2</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Body height</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">LN</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p>Taille du patient</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-6</p>
      </td>
      <td>
        <p>Units</p>
      </td>
      <td>
        <p>Unité</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupe OBSERVATION - Poids corporel

Ce groupe **OBSERVATION** optionnel est utilisé afin de véhiculer le **poids corporel du patient**, lorsque cette donnée est nécessaire pour la réalisation de l’examen d’imagerie. Le poids du patient est véhiculé par l'intermédiaire d'un segment OBX.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">NM</span> (Numeric)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">29463-7</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Body weight</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">LN</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p>Poids du patient</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-6</p>
      </td>
      <td>
        <p>Units</p>
      </td>
      <td>
        <p>Unité</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupe OBSERVATION - Statut grossesse

Ce groupe **OBSERVATION** optionnel est utilisé afin de véhiculer le **statut de grossesse** de la personne prise en charge, lorsque cette information est pertinente pour la réalisation de l’examen d’imagerie.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = Optional / Cardinalité = [0..1]</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Elément requis</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Valeur</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Segment OBX</strong></p>
      </td>
      <td>
        <p><strong>Observation/Result</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-1</p>
      </td>
      <td>
        <p>Set Id - Obx</p>
      </td>
      <td>
        <p>Numéro de séquence du segment</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-2</p>
      </td>
      <td>
        <p>Value Type</p>
      </td>
      <td>
        <p><span class="hl7-color">CE</span> (Coded Entry)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-3</p>
      </td>
      <td>
        <p>Observation Identifier</p>
      </td>
      <td>
        <p><strong> </strong></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.1  </p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p><span class="hl7-color">82810-3</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Pregnancy status</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.3 </p>
      </td>
      <td>
        <p>Name of Coding system</p>
      </td>
      <td>
        <p><span class="hl7-color">LN</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-5</p>
      </td>
      <td>
        <p>Observation Value</p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.1</p>
      </td>
      <td>
        <p>Code </p>
      </td>
      <td>
        <p>Table HL7 : 0136 :</p>
        <p>·      <span class="hl7-color"> Y</span> (Yes) -> Personne prise en charge enceinte </p>
        <p>·       <span class="hl7-color">N</span> (No) -> Personne prise en charge non enceinte</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.3</p>
      </td>
      <td>
        <p>Name Of Coding System</p>
      </td>
      <td>
        <p><span class="hl7-color">expandedYes-NoIndicator</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBX-11</p>
      </td>
      <td>
        <p>Observation Result Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">O » (Order detail description only (no result))</span></p>
      </td>
    </tr>
  </tbody>
</table>