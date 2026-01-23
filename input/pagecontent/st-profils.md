### Profils de message

La présente partie décrit les **profils de messages HL7 v2** retenus pour supporter les flux d’échange du volet Téléradiologie.  
Pour chaque flux identifié, le **type de message HL7 v2** associé est précisé, ainsi que la **structure générale des segments** utilisés afin de couvrir les concepts métiers attendus.

Les profils de message définissent :
- le **type de message HL7 v2** et l’événement associé ;
- l’**ordre des segments** ;
- les **segments requis, optionnels ou répétables** ;
- le rôle fonctionnel de chaque segment dans le cadre du flux considéré.

Cette description vise à fournir une **vision structurante des messages échangés**, indépendamment des contraintes fines appliquées à chaque champ ou composant.
#### Description des messages HL7 v2

La description des messages ORU et MDM est basée sur le contenu du
document et les métadonnées complémentaires à véhiculer dans le cadre du
partage et de l'échange.

Les données utiles pour publication sur le DMP et pour l'envoi par
MSSanté de(s) document(s) sont stockées à la fois dans le segment PID du
message HL7, dans le document CDA-R2 conforme au [volet du CI_SIS Structuration minimale des documents de santé](https://esante.gouv.fr/volet-structuration-minimale-de-documents-de-sante) et dans des segments OBX du message HL7 spécifiant les métadonnées complémentaires.

Le développeur doit valoriser tous les segments et champs obligatoires
des messages HL7v2 afin de répondre au standard d'interopérabilité des
messages.

Ci-dessous sont représentées les structures de messages HL7v2 proposées
pour la transmission de document(s) CDA-R2 en HL7v2.

##### Message ORM^O01^ORM_O01 en HL7 v2.5.1

###### Profil du message ORU_R01

Le profil du message ORU_R01 est le suivant :
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
        <p>RE</p>
      </td>
      <td>
        <p>[0..1]</p>
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
        <p>Common Order : demande de traitement sur un document</p>
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
        <p>Document et expression des métadonnées de document relatives au masquage du document aux PS et de visibilité au patient.</p>
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
        <p>  [{PRT}] (note 1)</p>
      </td>
      <td>
        <p>Participation : Expéditeur du document, destinataire(s) MSSanté, adresse mail sur laquelle le destinataire peut répondre. Segment PRT pré-adopté de la version 2.9</p>
      </td>
      <td>
        <p>R/C</p>
      </td>
      <td>
        <p>[1..*]</p>
      </td>
      <td>
        <p>7 (v2.9)</p>
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
**Note (1) :** _le segment PRT est utilisé uniquement avec l'OBX qui porte la
demande de traitement sur le document. Dans ce cas il est requis et
conditionnel (sa valeur dépend de la demande exprimée : envoi de la
demande de traitement sur le DMP et/ou envoi vers un ou des
destinataire(s) via MSSanté)._

Le message ORU peut transmettre une ou deux instances de documents
CDA-R2. Le CREATEUR peut ainsi transmettre un document au format CDA-R2
niveau 1 et un deuxième document de contenu clinique identique au format
CDA-R2 niveau 3. Chaque document possède son propre identifiant
(fonctionnalité non applicable au SEGUR vague 2).

Dans le cadre de ce volet, spécifique à un échange entre un système
(CREATEUR) et une PFI (GESTIONNAIRE), l'occurrence ORDER_OBSERVATION est
utilisée pour transmettre une demande de traitement sur le(s)
document(s) : transmission initiale/remplacement/suppression de
document(s). Seuls les segments ORC, OBR et le groupe de segments
OBSERVATION de l'occurrence ORDER_OBSERVATION sont à renseigner.

Les contraintes apportées par ce volet sur les données des différents
segments du message ORU sont décrites à la [section dédiée](volume2.html#contraintes-appliquées-aux-messages-mdm-et-oru-dans-le-contexte-de-ce-volet).

###### Description fonctionnelle du message ORU

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

#### Réponses et acquittements

Pour l’ensemble des flux décrits ci-dessus :
- Les messages HL7 font l’objet d’un **acquittement technique HL7 v2** (`ACK`) ;
- Les règles d’acquittement suivent les mécanismes natifs du standard HL7 v2.5.1.

Les modalités d’acquittement applicatif, le cas échéant, sont précisées dans les sections dédiées de la présente spécification.