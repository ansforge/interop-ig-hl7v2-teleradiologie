##### Flux 4  - Transmission d'un complément d'information post-acte

Ce flux repose sur l’utilisation d'un messages **OMI^O23**, conformes au standard **HL7 v2.5.1**.

Les segments présentés dans cette partie font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les sections suivantes décrivent les contraintes appliquées aux segments du message OMI^O23 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est renseigné conformément au standard HL7v2.5.1 et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p>Valeur fixée à « <span class="hl7-color">SR »</span> (Response to send order/service status request)</p>
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
  </tbody>
</table>

###### Segment TQ1 (Timing/Quantity)

Le segment **TQ1 – Timing/Quantity** est utilisé pour véhiculer les informations temporelles relatives à l’**examen d’imagerie réalisé**.  
Il est renseigné conformément au standard HL7v2.5.1 et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p>Durée de rétention des images (jours)</p>
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

Le segment **OBR – Observation Request** est renseigné conformément au standard HL7v2.5.1 et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p><span class="hl7-color">COMPLEMENT_POST_ACTE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBR-4.2 (optionnel)</p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Transmission d'un complément d’information post-examen</span></p>
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
        <p>IPC-1.1</p>
      </td>
      <td>
        <p>Entity Identifier</p>
      </td>
      <td>
        <p>Accession Number</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-1.3</p>
      </td>
      <td>
        <p>Universal Id</p>
      </td>
      <td>
        <p>Identifiant de l'autorité d'affectation</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-1.4</p>
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
        <p>IPC-2</p>
      </td>
      <td>
        <p>Requested Procedure ID</p>
      </td>
      <td>
        <p></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-2.1</p>
      </td>
      <td>
        <p>Entity Identifier</p>
      </td>
      <td>
        <p>Code issu du <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-code-document-imagerie-cisis.html">JDV_CodeDocumentImagerie-CISIS</a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-2.3</p>
      </td>
      <td>
        <p>Universal Id</p>
      </td>
      <td>
        <p>OID du code system utilisé</p>
        <p><span class="hl7-color">1.2.250.1.213.1.1.4.322</span> pour TerminologieCISIS</p>
        <p><span class="hl7-color">1.2.840.10008.2.16.4</span> pour DCM</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-2.4</p>
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
        <p>IPC-3</p>
      </td>
      <td>
        <p>Study Instance UID (5)</p>
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
        <p>IPC-4.1</p>
      </td>
      <td>
        <p>Entity Identifier</p>
      </td>
      <td>
        <p>Code issu du <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-code-document-imagerie-cisis.html">JDV_CodeDocumentImagerie-CISIS</a></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-4.3</p>
      </td>
      <td>
        <p>Universal Id</p>
      </td>
      <td>
        <p>OID du code system utilisé</p>
        <p><span class="hl7-color">1.2.250.1.213.1.1.4.322</span> pour TerminologieCISIS</p>
        <p><span class="hl7-color">1.2.840.10008.2.16.4</span> pour DCM</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>IPC-4.4</p>
      </td>
      <td>
        <p>Universal Id Type</p>
      </td>
      <td>
        <p><span class="hl7-color">ISO</span></p>
      </td>
    </tr>
  </tbody>
</table>

<blockquote class="stu-note">
    <p>
    <b>(5) :</b> Bien que le type de donnée du champ IPC-3 soit EI (Entity Identifier) et que la spécification d'Interop'santé concernant <a href="https://www.interopsante.org/f/db43469b624f3039f9610d8cb6b27830ed6a9fe1/IHE_France_Constraints_on_HL7_data_types_for_ITI_V1.8.2.pdf">les types de données utilisables en France</a> prévoit le renseignement des couples EI.1 + EI.2 ou EI.1 + EI.3 + EI.4, cette contrainte ne s’applique pas dans le cas du Study Instance UID.  
    En effet, le Study Instance UID est un identifiant globalement unique et n’est pas associé à une autorité d’affectation distincte. À ce titre, seul le composant EI.1 (Entity Identifier) est requis pour véhiculer cet identifiant.
    Cette approche est conforme aux principes décrits dans le <a href = "https://esante.gouv.fr/sites/default/files/media_entity/documents/ci-sis_service_volet-partage-documents-sante_v1.16.4.pdf">volet Partage de documents de santé</a> section 3.4.56.5.
    </p>
</blockquote>

<br>

##### Groupe OBSERVATION - URL de viewer DRIMbox

Ce **groupe OBSERVATION** est utilisé afin de véhiculer l’**URL d’accès à la vieweuse DRIMbox**, permettant la consultation à distance des images issues de l’examen d’imagerie. Il est important de noter que la valeur associée correspond à une adresse partielle à compléter afin de permettre l’accès à la visionneuse DICOM implémentée par une solution DRIMBox associée au système RIS. En effet, il est nécessaire de compléter cette donnée avec l'identifiant du compte-rendu d'imagerie afin d'obtenir un lien d'accès fonctionnel. Une fois l’URL assemblée, celle-ci doit être mentionnée au sein du compte-rendu d’imagerie. Ce concept permet l’intégration au maillage DRIM-M du compte-rendu d’imagerie rédigé suite à la réalisation de l’acte d’imagerie.

L’URL de la vieweuse est portée par un **segment OBX unique** au sein du groupe OBSERVATION. Elle est transmise sous forme de texte encodé en base 64 afin d'éviter toute contrainte liée à la présence de caractères spéciaux.
La valeur portée dans **OBX-5** correspond à l'encodage en base 64 d'une URL partielle, incluant les éléments suivants : FQDN du point d'accès, service cible, paramètres StudyInstanceUID et AccessionNumber. Pour plus de précisions concernant le formalisme à appliquer dans le cadre de la construction de cette URL, se référer à la section 4.2.2 de la spécification projet DRIMBox visionneuse.  
Le segment OBX portant sur l'adresse d'accès à la visionneuse est identifié par un code local "URL_PARTIELLE_VIEWER" dans **OBX-3**, <a href="./table_obs.html">documenté en annexe</a>.

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
        <p><span class="hl7-color">URL_PARTIELLE_VIEWER</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">URL partielle d’accès à la visionneuse d’imagerie DRIMbox</span></p>
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
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.2</p>
      </td>
      <td>
        <p>Type</p>
      </td>
      <td>
        <p><span class="hl7-color">TEXT</span> (Machine readable text document)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.4</p>
      </td>
      <td>
        <p>Encoding</p>
      </td>
      <td>
        <p><span class="hl7-color">Base64</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-5.5</p>
      </td>
      <td>
        <p>Data</p>
      </td>
      <td>
        <p>URL partielle d’accès à la visionneuse d’imagerie DRIMbox</p>
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

##### Groupe OBSERVATION - Acte d'imagerie

Ce groupe obligatoire est composé d'un segment OBX permettant d’indiquer le **code de l'acte d'imagerie réalisée**.

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
        <p><span class="hl7-color">CODE_ACTE_IMAGERIE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Code de l'acte d'imagerie réalisée</span></p>
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
        <p>Valeur issue du <a href="https://ansforge.github.io/IG-terminologie-de-sante/ig/main/ValueSet-jdv-code-document-imagerie-cisis.html">JDV_CodeDocumentImagerie-CISIS</a></p>
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
        <p><span class="hl7-color">LN</span></p>
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
        <p>Valeur fixée à « <span class="hl7-color">F »</span></p>
      </td>
    </tr>
  </tbody>
</table>

##### Groupes OBSERVATION - Localisation anatomique

Les groupes **OBSERVATION – Localisation anatomique** sont **optionnel** dans le cadre du flux 4.  
Leur présence permet de transmettre les informations relatives à la localisation anatomique concernée par l’examen réalisé, ainsi que, le cas échéant, une précision topographique associée. La structure, le contenu et les contraintes applicables à ces groupes OBSERVATION sont strictement identiques à ceux définis pour le flux 1 **à l'exception du champ OBX-11 prenant la valeur "F" dans le cadre de ce flux**.
Pour le détail des segments OBX, se référer à la section dédiée du flux 1 : [Groupes OBSERVATION – Localisation anatomique](./specifications_techniques.html#groupes-observation---localisation-anatomique)

##### Groupe OBSERVATION - Modalité d'imagerie

Le groupe **OBSERVATION - Modalité d'imagerie** est optionnel dans le cadre du flux 4.
Sa présence permet de transmettre la modalité d'imagerie utilisée lors de l'examen. La structure, le contenu et les contraintes applicables à ce groupe OBSERVATION sont strictement identiques à ceux définis pour le flux 1 **à l'exception du champ OBX-11 prenant la valeur "F" dans le cadre de ce flux**.  
Pour le détail du segment OBX, se référer à la section dédiée du flux 1 : [Groupes OBSERVATION – Modalité d'imagerie](./specifications_techniques.html#groupe-observation---modalité-dimagerie)


##### Groupes OBSERVATION - Produit administré

Les groupes **OBSERVATION – Produit administré** sont **optionnels** et permettent de transmettre les informations relatives aux produits administrés lors d’un examen d’imagerie.  

Chaque ensemble d'informations associées à un produit donné est portée dans **un groupe OBSERVATION** et un segment OBX distincts.  
Les groupes sont répétables pour permettre la transmission d'informations associées à plusieurs produits administrés au cours du même examen.  
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
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
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
        <p>Valeur issue du JDV ATC niveau 2 “V09” ou “V10”.</p>
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
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
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
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
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
Les segments OBX portant sur l'appareil d'imagerie sont identifiés par un code local "APPAREIL_IMAGERIE" dans **OBX-3**, documenté en annexe. Ces segments sont différenciés à l’aide du champ **OBX-4 – Observation Sub-ID**.

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
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
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
        <p>Identifiant de l'appareil d'imagerie : <a href="./specifications_fonctionnelles.html#classe-appareilimagerieutilise">SupportIUD voir SFE 2.1.7.4.3</a>.</p>
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
        <p>&gt; OBX-3.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
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
