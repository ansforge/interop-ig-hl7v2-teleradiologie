##### Flux 1 - Transmission de la demande d'examen d'imagerie

Ce flux repose sur l’utilisation d'un messages **ORM^O01**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les **groupes OBSERVATION** (segments OBX), non contraints et optionnels dans le cadre du profil IHE SWF, sont **explicitement contraints par le volet téléradiologie**. Ces contraintes permettent notamment de structurer et de normaliser la transmission d’informations complémentaires nécessaires à la réalisation et à l’interprétation de l’examen d’imagerie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer les informations relatives à la **demande d’examen d’imagerie**.
Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p>Valeur fixée à « <span class="hl7-color">NW</span> (New order/service)</p>
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
        <p>Identifiant de la demande d'examen d'imagerie</p>
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
        <p>Informations relatives au professionel de santé effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie</p>
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
        <p>Informations relatives à la structure d'imagerie d'accueil du patient</p>
      </td>
    </tr>
  </tbody>
</table>

##### Segment OBR (Observation Request)

Le segment **OBR** est utilisé pour véhiculer des informations relatives à la **demande d’examen d’imagerie**.  
Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

Ce segment permet notamment de préciser :  
- la **modalité d’imagerie demandée** (champ OBR-4),  
- les **antécédents pertinents du patient pour l’examen** (champ OBR-13),  
- ainsi que les **références à la demande** d’origine, par répétition des informations portées dans le segment ORC, notamment au niveau des champs **OBR-2** et **OBR-16**.

Les champs présentés dans le tableau ci-après sont **requis** ou **requis si connus**, selon leur pertinence dans le cadre du workflow de téléradiologie.

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
        <p>Identifiant de la demande d'examen (identique à l'ORC-1)</p>
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
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt;OBR-4.1</p>
      </td>
      <td>
        <p>Code de la modalité d'imagerie</p>
      </td>
      <td rowspan="2">
        <p>Utiliser le <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html">JDV_modalitedemandeActeImagerie-CISIS </a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt;OBR-4.2</p>
      </td>
      <td>
        <p>Libellé</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&gt;OBR-4.3</p>
      </td>
      <td>
        <p>Système de codage dont est issu le code</p>
      </td>
      <td>
        <p> <span class="hl7-color">DCM</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>OBR-13 (Requis si connu)</p>
      </td>
      <td>
        <p>Relevant Clinical Information</p>
      </td>
      <td>
        <p>Antécédents du patient pertinent dans le cadre de l'examen demandé</p>
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
    <tr>
      <td>
        <p>OBR-31</p>
      </td>
      <td>
        <p>Reason for Study</p>
      </td>
      <td>
        <p>JustificationDemande</p>
      </td>
    </tr>
  </tbody>
</table>

<br>

##### Groupes OBSERVATION - Localisation anatomique

Ces groupes **OBSERVATION** sont utilisés afin de véhiculer les informations relatives à la **localisation anatomique concernée par la demande d’examen d’imagerie**.
Ces informations permettent de préciser la zone anatomique à explorer et, le cas échéant, d’apporter un niveau de détail complémentaire facilitant l’interprétation et la réalisation de l’examen.

La localisation anatomique est portée par un **premier segment OBX obligatoire**, pouvant être complété par un **second segment OBX optionnel** destiné à préciser la topographie de manière plus fine.
Les segments OBX portant sur la localisation anatomique sont identifiés par un code local "LOCALISATION_ANATOMIQUE" dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

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
        <p>Libellé </p>
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
        <p><span class="hl7-color"><span class="hl7-color">TLRMETADATA</span></span></p>
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
        <p><strong>Voir règle commune d’utilisation du Sub-ID : </strong><a href ="specifications_techniques.html#utilisation-du-champ-obx-4--observation-sub-id">Utilisation du champ OBX-4 </a></p>
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
        <p><span class="hl7-color">DCM</span></p>
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
        <p>Valeur fixée à « <span class="hl7-color">F</span> » </p>
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
        <p><span class="hl7-color">CE</span>(Coded Entry)</p>
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
        <p>Libellé </p>
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
        <p><span class="hl7-color"><span class="hl7-color">TLRMETADATA</span></span></p>
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
        <p><strong>Voir règle commune d’utilisation du Sub-ID : </strong><a href ="specifications_techniques.html#utilisation-du-champ-obx-4--observation-sub-id">Utilisation du champ OBX-4 </a></p>
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
        <p>Valeur fixée à « <span class="hl7-color">F</span> » </p>
      </td>
    </tr>
  </tbody>
</table>

<br>

##### Groupe OBSERVATION - Taille corporel

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
        <p>Libellé </p>
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
        <p>Valeur fixée à « <span class="hl7-color">F</span> » </p>
      </td>
    </tr>
  </tbody>
</table>

<br>

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
        <p>Libellé </p>
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
        <p>Valeur fixée à « <span class="hl7-color">F</span> » </p>
      </td>
    </tr>
  </tbody>
</table>

<br>

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
        <p>Libellé </p>
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
        <p>Valeur fixée à « <span class="hl7-color">F</span> » </p>
      </td>
    </tr>
  </tbody>
</table>