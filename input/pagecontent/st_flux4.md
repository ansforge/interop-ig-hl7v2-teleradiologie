##### Flux 4  - Transmission d'un complément d'information post-acte

Ce flux repose sur l’utilisation d'un messages **OMI^O23**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les **groupes OBSERVATION** (segments OBX), non contraints et optionnels dans le cadre du profil IHE SWF, sont **explicitement contraints par le volet téléradiologie** afin de permettre la transmission normalisée des informations post-acte nécessaires, telles que les produits administrés, l’appareil d’imagerie utilisé ou les informations de restitution des images.

Les sections suivantes décrivent les contraintes appliquées aux segments du message OMI^O23 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est renseigné conformément aux spécifications du profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p>ORC-3</p>
      </td>
      <td>
        <p>Filler Order Number</p>
      </td>
      <td>
        <p>Identifiant de la demande d'examen d'imagerie</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-5</p>
      </td>
      <td>
        <p>Order Status</p>
      </td>
      <td>
        <p>Valeur fixée à « <span class="hl7-color">SC</span> (Scheduled)</p>
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
        <p></p>
      </td>
    </tr>
  </tbody>
</table>

###### Segment TQ1 (Timing/Quantity)

Le segment **TQ1 – Timing/Quantity** est utilisé pour véhiculer les informations temporelles relatives à l’**examen d’imagerie réalisé**.  
Il est renseigné conformément aux spécifications du profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du segment TQ1 : Usage = Required / Cardinalité = [1..1]</p>
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
        <p><strong>Segment TQ1</strong></p>
      </td>
      <td>
        <p><strong>Timing/Quantity</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>TQ1-6</p>
      </td>
      <td>
        <p>Service Duration</p>
      </td>
      <td>
        <p>Durée de rétention des images</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>TQ1-7</p>
      </td>
      <td>
        <p>Start date/time</p>
      </td>
      <td>
        <p>Date/heure de l'examen d'imagerie</p>
      </td>
    </tr>
  </tbody>
</table>

<br>

##### Segment OBR (Observation Request)

Le segment **OBR – Observation Request** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p>Code LOINC de l’acte d’imagerie</p>
      </td>
      <td>
        <p>Utiliser le <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-code-document-imagerie-cisis.html">JDV_CodeDocumentImagerieCisis-CISIS </a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt;OBR-4.2</p>
      </td>
      <td>
        <p>Libellé</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt;OBR-4.3</p>
      </td>
      <td>
        <p>Système de codage dont est issu le code</p>
      </td>
      <td>
        <p> <span class="hl7-color">LN</span></p>
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
        <p>Informations relatives au professionnel de santé effecteur à distance (identique à l'ORC-12)</p>
      </td>
    </tr>
  </tbody>
</table>

<br>

##### Segment IPC (Imaging Procedure Control)

Le segment **IPC – Imaging Procedure Control** est utilisé dans le cadre du **flux 4** pour véhiculer les informations spécifiques à la **procédure d’imagerie réalisée**.  
Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du segment IPC : Usage = Required / Cardinalité = [1..1]</p>
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
        <p><strong>Segment IPC</strong></p>
      </td>
      <td>
        <p><strong>Imaging Procedure Control</strong></p>
      </td>
      <td>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-1</p>
      </td>
      <td>
        <p>Accession Identifier</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-2</p>
      </td>
      <td>
        <p>Requested Procedure ID</p>
      </td>
      <td>
        <p>Accession number</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-3</p>
      </td>
      <td>
        <p>Study Instance UID</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-4</p>
      </td>
      <td>
        <p>Scheduled Procedure Step ID</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt;IPC-5.1</p>
      </td>
      <td>
        <p>Code de la modalité d'imagerie</p>
      </td>
      <td>
        <p>Utiliser le <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-modalite-demande-acte-imagerie-cisis.html">JDV_modalitedemandeActeImagerie-CISIS </a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt;IPC-5.2</p>
      </td>
      <td>
        <p>Libellé</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&gt;IPC-5.3</p>
      </td>
      <td>
        <p>Système de codage dont est issu le code</p>
      </td>
      <td>
        <p> <span class="hl7-color">DCM</span></p>
      </td>
    </tr>
  </tbody>
</table>

<br>

##### Groupe OBSERVATION - URL de viewer DRIMbox

Ce **groupe OBSERVATION** est utilisé afin de véhiculer l’**URL d’accès à la vieweuse DRIMbox**, permettant la consultation à distance des images issues de l’examen d’imagerie.  

L’URL de la vieweuse est portée par un **segment OBX unique** au sein du groupe OBSERVATION. Elle est transmise sous forme de texte.
La valeur portée dans **OBX-5** correspond à une URL complète, pouvant inclure des paramètres de requête nécessaires à l’accès sécurisé à la vieweuse. Les caractères spéciaux éventuellement présents dans l’URL sont encodés conformément aux règles d’échappement HL7 v2.5.1 (6), afin d’assurer l’intégrité de l’information transmise.
Le segment OBX portant sur le protocole est identifié par un code local "URL_VIEWER_DRIMBOX" dans **OBX-3**, <a href="./table_obs.html">documenté en annexe</a>.

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
        <p><span class="hl7-color">TX</span> (Text Data)</p>
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
        <p><span class="hl7-color">URL_VIEWER_DRIMBOX</span></p>
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
        <p><span class="hl7-color">URL de la visionneuse DRIMbox</span></p>
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
        <p><span class="hl7-color">TLR_OBSERVATION</span></p>
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
        <p>URL du viewer DRIMbox</p>
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

<blockquote class="stu-note">
    <p>
    <b>(6) :</b> Les séquences d’échappement sont encadrées par le caractère d’échappement défini dans MSH-2 ( `\`) et permettent de représenter notamment :
    </p>
    <ul>
      <li>le séparateur de champs (|) via \F\ ;</li>
      <li>le séparateur de composants (^) via \S\ ;</li>
      <li>le séparateur de répétitions (~) via \R\ ;</li>
      <li>le séparateur de sous-composants (&) via \T\ ;</li>
      <li>le caractère d’échappement lui-même (\) via \E\.</li>
    </ul>
</blockquote>

##### Groupes OBSERVATION - Localisation anatomique

Les groupes **OBSERVATION – Localisation anatomique** sont **optionnel** dans le cadre du flux 4.  
Leur présence permet de transmettre les informations relatives à la localisation anatomique concernée par l’examen réalisé, ainsi que, le cas échéant, une précision topographique associée. La structure, le contenu et les contraintes applicables à ces groupes OBSERVATION sont strictement identiques à ceux définis pour le flux 1.  
Pour le détail des segments OBX, se référer à la section dédiée du flux 1 : [Groupes OBSERVATION – Localisation anatomique](./st_flux1.html#Groupes-OBSERVATION---Localisation-anatomique)

##### Groupes OBSERVATION - Produit administré

Les groupes **OBSERVATION – Produit administré** sont **optionnels** et permettent de transmettre les informations relatives aux produits administrés lors d’un examen d’imagerie.  

Chaque information du produit est portée dans **un groupe OBSERVATION** et un segment OBX distincts.  
Les groupes sont répétables pour permettre la transmission de plusieurs produits administrés au cours du même examen.  
Pour assurer la cohérence des informations :  
- le **type de produit** et le **numéro de lot** sont **indissociables**,
- la **quantité administrée** est facultative mais recommandée lorsque le produit est renseigné.

Les segments OBX portant sur le produit administré sont identifiés par un code local "PRODUIT_ADMINISTRE" dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION – Type de produit

Ce groupe OBSERVATION permet de transmettre le **type de produit administré**.  La valeur est codée à partir du **Jeu de Valeurs ATC niveau 2**, limité aux classes :

- V09 – Produits de diagnostic  
- V10 – Produits thérapeutiques  

Un segment OBX unique au sein de ce groupe porte la valeur codée dans **OBX-5**.  
Ce groupe est obligatoirement associé au groupe **Numéro de lot**.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]</p>
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
        <p><span class="hl7-color">PRODUIT_ADMINISTRE</span></p>
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
        <p><span class="hl7-color">Produit administré lors de l'examen d'imagerie</span></p>
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
        <p><span class="hl7-color">TLR_OBSERVATION</span></p>
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
        <p>Valeur issue du JDV ATC niveau 2 “V09” ou “V10”.</a></p>
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
        <p><span class="hl7-color">ATC</span></p>
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

###### Groupe OBSERVATION – Numéro de lot

Ce groupe OBSERVATION permet de transmettre le **numéro de lot** du produit administré, garantissant la traçabilité et l’identification précise du produit.  
Le segment OBX unique au sein de ce groupe porte le numéro de lot dans **OBX-5**.  
Ce groupe doit être présent si le groupe Type de produit est renseigné.

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="3">
        <p>Composition du groupe OBSERVATION: Usage = C / Cardinalité = [0..1]</p>
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
        <p><span class="hl7-color">PRODUIT_ADMINISTRE</span></p>
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
        <p><span class="hl7-color">Produit administré lors de l'examen d'imagerie</span></p>
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
        <p><span class="hl7-color">TLR_OBSERVATION</span></p>
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
        <p>Numéro de lot du radiopharmaceutique adminsitré</p>
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

###### Groupe OBSERVATION – Quantité de produit administré

Ce groupe OBSERVATION permet de transmettre la quantité réellement administrée du produit. Le segment OBX unique au sein de ce groupe porte la valeur dans **OBX-5** et l’unité de mesure dans **OBX-6** (par exemple millilitres ou milligrammes).  
La quantité est **optionnelle** mais fortement recommandée lorsque le produit est renseigné.  

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
        <p><span class="hl7-color">PRODUIT_ADMINISTRE</span></p>
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
        <p><span class="hl7-color">Produit administré lors de l'examen d'imagerie</span></p>
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
        <p><span class="hl7-color">TLR_OBSERVATION</span></p>
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
        <p>Valeur fixée à n.3</p>
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
        <p>Volume de radiopharmeutique administré</p>
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

##### Groups OBSERVATION - Appareil d'imagerie utilisé

Les groupes **OBSERVATION – Appareil d’imagerie utilisé** sont **optionnels**. Lorsqu’ils sont présents, ils permettent de transmettre les informations relatives à l’appareil d’imagerie ayant été utilisé pour la réalisation de l’examen, en particulier dans le cas des techniques irradiantes.
Les informations relatives à l’appareil sont portées dans **deux groupes OBSERVATION distincts** :

- un groupe dédié à l’**identifiant unique de l’appareil d’imagerie**,  
- un groupe dédié au **modèle de l’appareil d’imagerie**.

Ces groupes peuvent être utilisés conjointement ou indépendamment, selon le niveau d’information disponible, l’identifiant de l’appareil constituant l’information principale de référence.
Les segments OBX portant sur le produit administré sont identifiés par un code local "APPAREIL_IMAGERIE" dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

###### Groupe OBSERVATION – Identifiant de l’appareil d’imagerie

Ce groupe OBSERVATION permet de transmettre l’identifiant unique de l’appareil d’imagerie utilisé lors de l’examen. L’identifiant correspond au **Support IUD**, tel que communiqué via un dispositif d’identification automatique (AIDC) ou, le cas échéant, via son marquage en clair.
Le groupe contient un **segment OBX unique** portant la valeur de l’identifiant dans **OBX-5**.  

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
        <p><span class="hl7-color">TX</span> (Text Data)</p>
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
        <p><span class="hl7-color">APPAREIL_IMAGERIE</span></p>
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
        <p><span class="hl7-color">Appareil d'imagerie utilisé lors de l'examen</span></p>
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
        <p><span class="hl7-color">TLR_OBSERVATION</span></p>
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
        <p>Identifiant de l'appareil d'imagerie : SupportIUD voir SFE 2.1.7.4.3</p>
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

###### Groupe OBSERVATION – Modèle de l’appareil d’imagerie

Ce groupe OBSERVATION permet de transmettre le modèle de l’appareil d’imagerie utilisé. La valeur est exprimée sous forme de texte libre et correspond à la dénomination du modèle fournie par le constructeur.
Le groupe contient un **segment OBX unique** portant le modèle de l’appareil dans **OBX-5**.  
Ce groupe est **optionnel** et vient compléter l’identifiant de l’appareil lorsqu’une information plus détaillée sur l’équipement est requise. 

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
        <p><span class="hl7-color">TX</span> (Text Data)</p>
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
        <p><span class="hl7-color">APPAREIL_IMAGERIE</span></p>
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
        <p><span class="hl7-color">Appareil d'imagerie utilisé lors de l'examen</span></p>
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
        <p><span class="hl7-color">TLR_OBSERVATION</span></p>
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
        <p>Modèle de l’appareil d’imagerie utilisé</p>
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
