##### Flux 3 - Réponse à la demande d'examen d'imagerie

Ce flux repose sur l’utilisation de messages **ORU^R01**, conformes au standard **HL7 v2.5.1**.
  
Les segments ci-dessous sont définis sur la base du standard HL7 v2.5.1, complété par une **surcouche de contraintes spécifiques à la téléradiologie**, décrite dans les sections suivantes.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer la **décision du médecin effecteur** vis-à-vis de la demande d’examen d’imagerie.

Le champ **ORC-1 – Order Control** permet d’indiquer la décision prise sur la demande, à savoir sa **validation** ou son **refus**.
En cas de refus, un **motif de refus** peut être transmis lorsque cette information est disponible ; son renseignement est **optionnel**.

Le tableau ci-après décrit l’ensemble des champs **requis** du segment ORC, ainsi que certains champs **requis si connus** ou **optionnel**, dont l’usage est jugé pertinent au regard du workflow de téléradiologie.

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
        <p>Décision du médecin effecteur à distance vis-à-vis de la demande d'examen</p>
        <p><span class="hl7-color">OK</span> (Order/service accepted & OK) dans le cas d'une demande d'examen validée</p>
        <p><span class="hl7-color">OC</span> (Order/service canceled) dans le cas d'une demande d'examen refusée</p>
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
        <p>ORC-12</p>
      </td>
      <td>
        <p>Ordering Provider</p>
      </td>
      <td>
        <p>Informations relatives au Médecin effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-16 (Optionnel)</p>
      </td>
      <td>
        <p>Order Control Code Reason</p>
      </td>
      <td>
        <p>Motif du refus de la demande d'examen</p>
        <p>Peut être exprimé à l’aide d’un code renseigné dans CE-1 – Identifier, avec le système de codage correspondant précisé en CE-3 – Name of Coding System (code local ou standard).</p>
        <p>À défaut de codage disponible, un libellé en clair peut être renseigné dans CE-2 – Text.</p>
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
        <p>Qualifie le type d'organisation (voir <a href="specifications_techniques.html#segment-orc-common-order">Note 1</a>)</p>
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
        <p><span class="hl7-color">PLATEFORME_TELERADIOLOGIE</span></p>
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
        <p>Nom de l'organisation</p>
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
        <p>Identifiant de l'organisation destinataire du document</p>
      </td>
    </tr>
  </tbody>
</table>

##### Segment OBR (Observation Request)

Le segment **OBR** est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
      <td>
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

##### Groupe OBSERVATION - Protocole d'imagerie

Le **groupe OBSERVATION** est requis afin de véhiculer le **protocole d’imagerie** associé à l'examen.  
Le protocole d’imagerie est porté par un **segment OBX unique** au sein du groupe OBSERVATION. Deux alternatives d’encodage sont proposées, en fonction du niveau de structuration et du contenu du protocole à transmettre :

- **Protocole en clair** : transmission du protocole sous forme de texte lisible directement dans le message HL7, à l’aide du type de données **FT (Formatted Text)**.  
- **Protocole encapsulé** : transmission du protocole sous forme de document encapsulé (par exemple PDF, XML ou texte structuré), encodé en **base64** et véhiculé à l’aide du type de données **ED (Encapsulated Data)**.

Ces deux alternatives sont exclusives : un seul segment OBX est utilisé pour porter le protocole d’imagerie, avec le type de données adapté au mode de transmission retenu. Le choix de l’alternative relève des capacités des systèmes émetteurs et récepteurs et doit être cohérent avec les besoins métier du flux.
Le segment OBX portant sur le protocole est identifié par un code local "PROTOCOLE_IMAGERIE" dans **OBX-3**, <a href="./table_obs.html">documenté en annexe</a>.

###### Protocole d'imagerie en clair

Cette alternative permet de transmettre le **protocole d’imagerie en clair**, sous forme de texte formaté directement exploitable par un utilisateur.  
Le contenu peut inclure des retours à la ligne et une structuration légère facilitant la lecture humaine.  

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
        <p><span class="hl7-color">PROTOCOLE_IMAGERIE</span></p>
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
        <p><span class="hl7-color">Protocole d'imagerie médicale</span></p>
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
        <p>Protocole d'imagerie</p>
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

###### Protocole d'imagerie encapsulé

Cette alternative permet de transmettre le **protocole d’imagerie sous forme encapsulée**, en utilisant le type de données ED.  
Le protocole est encodé en **base64** et peut correspondre à un document structuré (PDF, XML, ou autre format convenu entre les acteurs).  

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
        <p><span class="hl7-color">ED</span> (Encapsuled Data)</p>
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
        <p><span class="hl7-color">PROTOCOLE_IMAGERIE</span></p>
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
        <p><span class="hl7-color">Protocole d'imagerie médicale</span></p>
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
        <p>Intégrer le protcole d'imagerie PDF en base64</p>
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
