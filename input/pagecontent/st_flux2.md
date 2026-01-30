##### Flux 2 - Annulation de la demande d'examen d'imagerie

Ce flux repose sur l’utilisation d'un message **ORM^O01**, conforme au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer l’**annulation d’une demande d’examen d’imagerie**, conformément au profil **IHE Scheduled Workflow (SWF)** .

La structure du segment ORC est **identique à celle du flux 1**, à l’exception du champ **ORC-1 – Order Control**, dont la valeur est fixée à **CA (Cancel Order)**.  
Un **motif d’annulation** peut être véhiculé lorsque cette information est disponible, son renseignement est **optionnel**.

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
        <p>Valeur fixée à « <span class="hl7-color">CA</span> » (Canceled)</p>
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
        <p>Date à laquelle la demande d'examen a été annulée</p>
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
        <p>Informations relatives au Médecin effecteur à distance qui analyse la pertinence de l’examen demandé en lien avec le médecin demandeur, valide la demande d’examen et défini le protocole d’imagerie</p>
        <p>Ce champ est à renseigner s'il est connu de l'expéditeur au moment de l'envoi de la demande d'examen d'imagerie</p>
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
        <p>Nom de l'autorité d'affectation</p>
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
        <p>ORC-16 (Optionnel)</p>
      </td>
      <td>
        <p>Order Control Code Reason</p>
      </td>
      <td>
        <p>Motif d'annulation de la demande d'examen (type CE)</p>
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
        <p>Identifiant de l'organisation destinataire</p>
      </td>
    </tr>
  </tbody>
</table>

##### Segment OBR (Observation Request)

Le segment **OBR** est utilisé pour véhiculer des informations relatives à la **demande d’examen d’imagerie**.  
Il est renseigné conformément au profil **IHE Scheduled Workflow (SWF)** et fait l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie**.

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
        <p><span class="hl7-color">ANNULATION_DEMANDE</span></p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&gt; OBR-4.2 (optionnel)  </p>
      </td>
      <td>
        <p>Display name </p>
      </td>
      <td>
        <p><span class="hl7-color">Annulation d’une demande d’examen</span></p>
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
