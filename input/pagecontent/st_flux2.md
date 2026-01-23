##### Flux 2 - Annulation de la demande d'examen d'imagerie

Ce flux repose sur l’utilisation d'un messages **ORM^O01**, conformes au standard **HL7 v2.5.1**.

Les segments sont renseignés conformément au profil **IHE Scheduled Workflow (SWF)**, lorsqu’il est applicable, et font l’objet d’une **surcouche de contraintes spécifiques à la téléradiologie** afin de répondre aux besoins métier du contexte de téléradiologie.

Les parties suivantes détaillent les contraintes appliquées aux segments du message ORM^O01 dans le cadre de ce flux.

###### Segment ORC (Common Order)

Le segment **ORC** est utilisé pour véhiculer l’**annulation d’une demande d’examen d’imagerie**, conformément au profil **IHE Scheduled Workflow (SWF)** .

La structure du segment ORC est **identique à celle du flux 1**, à l’exception du champ **ORC-1 – Order Control**, dont la valeur est fixée à **CA (Cancel Order)**.  
Un **motif d’annulation** peut être véhiculé lorsque cette information est disponible ; son renseignement est **optionnel**.

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
        <p>Valeur fixée à « <span class="hl7-color">CA</span> (Canceled)</p>
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
        <p>ORC-12</p>
      </td>
      <td>
        <p>Ordering Provider</p>
      </td>
      <td>
        <p>Informations relatives au Professionnel de santé de la structure d’imagerie qui accueille le patient et supervise la réalisation de l’acte d’imagerie</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ORC-14 (Requis si connu de l'expéditeur)</p>
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
        <p>Code du motif d'annulation de la demande d'examen</p>
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
