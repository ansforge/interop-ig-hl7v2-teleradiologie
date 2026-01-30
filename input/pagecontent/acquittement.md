##### Description des contraintes à appliquer sur l'acquittement

###### Segment MSH (Header)

Le segment MSH reprend une partie des informations du message initial :

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th colspan="2">
        <p>Message initial</p>
      </th>
      <th colspan="2">
        <p>Message d'acquittement</p>
      </th>
    </tr>
    <tr>
      <th>
        <p>Champ</p>
      </th>
      <th>
        <p>Description</p>
      </th>
      <th>
        <p>Champ</p>
      </th>
      <th>
        <p>Description</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.3">MSH.3</a> - Sending Application​</p>
      </td>
      <td>
        <p>Application source du message à acquitter</p>
      </td>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.5">MSH.5</a> - Receiving Application​</p>
      </td>
      <td>
        <p>Application destinatrice de l'acquittement</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.4">MSH.4</a> - Sending Facility​</p>
      </td>
      <td>
        <p>Etablissement source du message à acquitter</p>
      </td>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.6">MSH.6</a> - Receiving Facility​</p>
      </td>
      <td>
        <p>Etablissement destinataire de l'acquittement</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.5">MSH.5</a> - Receiving Application​</p>
      </td>
      <td>
        <p>Application destinatrice du message à acquitter</p>
      </td>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.3">MSH.3</a> - Sending Application​</p>
      </td>
      <td>
        <p>Application source de l'acquittement</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.6">MSH.6</a> - Receiving Facility​</p>
      </td>
      <td>
        <p>Etablissement destinataire du message à acquitter</p>
      </td>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.4">MSH.4</a> - Sending Facility​</p>
      </td>
      <td>
        <p>Etablissement source de l'acquittement</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.11">MSH.11</a> - Processing Id​</p>
      </td>
      <td>
        <p>Identifiant de traitement</p>
      </td>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSH.11">MSH.11</a> - Processing Id​</p>
      </td>
      <td>
        <p>Identifiant de traitement</p>
      </td>
    </tr>
  </tbody>
</table>

Le tableau ci-après décrit l’ensemble des champs **requis** du segment MSH :

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th>
        <p>Champ</p>
      </th>
      <th>
        <p>Contenu</p>
      </th>
      <th>
        <p>Type donnée</p>
      </th>
      <th>
        <p>Caractère optionnel/obligatoire</p>
      </th>
    </tr>
    <tr>
      <td>
        <p>MSH-1</p>
      </td>
      <td>
        <p><span class="hl7-color">|</span></p>
        <p>séparateur de champ</p>
      </td>
      <td>
        <p>ST</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-2</p>
      </td>
      <td>
        <p><span class="hl7-color">^~\&</span></p>
        <p>séparateur de composant, répétition, caractère d'échappement, séparateur de sous-composants</p>
      </td>
      <td>
        <p>ST</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-3</p>
      </td>
      <td>
        <p>Application émettrice</p>
      </td>
      <td>
        <p>HD</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-4</p>
      </td>
      <td>
        <p>Organisation émettrice</p>
      </td>
      <td>
        <p>HD</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-5</p>
      </td>
      <td>
        <p>Application réceptrice</p>
      </td>
      <td>
        <p>HD</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-6</p>
      </td>
      <td>
        <p>Organisation réceptrice</p>
      </td>
      <td>
        <p>HD</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-7</p>
      </td>
      <td>
        <p>Date/time du message</p>
      </td>
      <td>
        <p>TS</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-9</p>
      </td>
      <td>
        <p>Type du message, selon l'évènement du message initial : 
          <br><span class="hl7-color">ACK^O01^ACK</span>
          <br><span class="hl7-color">ACK^R01^ACK</span>
          <br><span class="hl7-color">ACK^O23^ACK</span>  
        </p>  
      </td>
      <td>
        <p>MSG</p>
      </td>
      <td>
        <p>R</p>
        <p> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-10</p>
      </td>
      <td>
        <p>Identifiant du message</p>
      </td>
      <td>
        <p>ST</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-11</p>
      </td>
      <td>
        <p>Processing Id 
        <br><span class="hl7-color">P</span> : en production 
        <br><span class="hl7-color">T</span> : message de test 
        <br><span class="hl7-color">D</span> : environnement de debug
        </p>
      </td>
      <td>
        <p>PT</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-12</p>
      </td>
      <td>
        <p>Version du standard</p>
        <p><span class="hl7-color">2.5.1</span></p>
      </td>
      <td>
        <p>VID</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-17</p>
      </td>
      <td>
        <p>Code du pays</p>
        <p><span class="hl7-color">FRA</span></p>
      </td>
      <td>
        <p>ID</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>MSH-18</p>
      </td>
      <td>
        <p>Jeux de caractères, valeurs possibles :</p>
        <p><span class="hl7-color">UNICODE UTF-8</span> ou <span class="hl7-color">8859/15</span></p>
      </td>
      <td>
        <p>ID</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
  </tbody>
</table>

###### Segment MSA (Message Acknowledgment)

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th>
        <p>Champ requis</p>
      </th>
      <th>
        <p>Contenu</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSA.1">MSA.1</a> - Acknowledgment Code</p>
      </td>
      <td>
        <p>Code d'acquittement du message autorisé :</p>
        <p>·       <span class="hl7-color">AA</span>(Original mode: Application Accept - Enhanced mode: Application acknowledgment: Accept) : le message a été compris et intégré par l'application destinatrice qui prend la responsabilité du message et libère ainsi l'application productrice de toute obligation de le renvoyer.</p>
        <p>·       <span class="hl7-color">AE</span> (Original mode: Application Error - Enhanced mode: Application acknowledgment: Error) : le message contient des erreurs de syntaxe.   </p>
        <p>·       <span class="hl7-color">AR</span> (Original mode: Application Reject - Enhanced mode: Application acknowledgment: Reject)  : le message est rejeté pour une raison circonstancielle. Il peut être réémis plus tard. </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><a href="https://hl7-definition.caristix.com/v2/HL7v2.8/Fields/MSA.2">MSA.2</a> - Message Control Id</p>
      </td>
      <td>
        <p>Rappel l'identifiant du message acquitté correspondant au champ MSH.10 du message initial.</p>
      </td>
    </tr>
  </tbody>
</table>

###### Segment ERR (Error)

Ce segment est utilisé au niveau des messages d'acquittement dans le cas
où le champ MSA-1 prend la valeur AE (Application error) ou AR
(Application reject).

Le tableau ci-dessous liste les champs à renseigner pour le segment
ERR :

<table class="table-hl7v2">
  <tbody>
    <tr>
      <th>
        <p>Champ</p>
      </th>
      <th>
        <p>Contenu</p>
      </th>
      <th>
        <p>Type donnée</p>
      </th>
      <th>
        <p>Caractère optionnel/obligatoire</p>
      </th>
    </tr>
    <tr>
      <td>
        <p>ERR-2</p>
      </td>
      <td>
        <p>Localisation de l'erreur dans le cas d'une erreur de syntaxe du message initial.</p>
      </td>
      <td>
        <p>ERL</p>
      </td>
      <td>
        <p>O</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ERR-3</p>
      </td>
      <td>
        <p>Code erreur HL7 dont les valeurs sont à prendre dans la table HL7 0357 (nom symbolique messageErrorCondition)</p>
      </td>
      <td>
        <p>CE</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>ERR-4</p>
      </td>
      <td>
        <p>Sévérité de l'erreur dont les valeurs sont à prendre dans la table HL7 0516 (nom symbolique errorSeverity)</p>
      </td>
      <td>
        <p>ID</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
  </tbody>
</table>

<b>Exemple</b>

Entête MSH d'un message ORM^O01 dans le cadre du flux 1 :

```
MSH|^~\&|StructureApp|StructureFacility|TLRapp|TLRfacility|20260106134418||ORM^O01^ORM_O01|12345|P|2.5.1|||||FRA|UNICODE UTF-8|||1.0^CISIS_TLR_HL7_V2
```
Un acquittement positif retourné par le SI de téléradiologie :

```
MSH|^~\&|TLRapp|TLRfacility|StructureApp|StructureFacility|20260106134419||ACK^R01^ACK|12346|P|2.5|||||FRA|8859/15
MSA|AA|12345
```
Un acquittement négatif retourné par le SI de téléradiologie : version d'HL7
inconnue

```
MSH|^~\&|TLRapp|TLRfacility|StructureApp|StructureFacility|20260106134419||ACK^R01^ACK|12347|P|2.5|||||FRA|8859/15
MSA|AE|12345
ERR||MSH^1^12|203^ Unsupported version^messageErrorCondition|E
```