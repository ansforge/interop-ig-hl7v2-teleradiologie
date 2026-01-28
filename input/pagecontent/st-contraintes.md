### Contraintes applicables aux profils de message

Cette section précise les **contraintes d’implémentation** applicables aux profils de message identifiés précédemment.  
Elle est structurée selon deux niveaux complémentaires.

#### Contraintes communes à l’ensemble des messages

Un premier sous-ensemble de contraintes s’applique **de manière transversale à l’ensemble des messages HL7 v2 échangés**, quel que soit le flux concerné.  
Ces contraintes portent notamment sur les segments suivants :

- **MSH (Message Header)** : identification du message, des acteurs émetteur et récepteur, gestion des versions, horodatage, identifiants de message ;
- **PID (Patient Identification)** : identité du patient, traits d’identification et conformité aux exigences nationales, notamment en lien avec l’INS ;
- **PV1 (Patient Visit)** : contexte de prise en charge et éléments nécessaires à la qualification du séjour ou de l’acte.

Ces contraintes communes garantissent une **cohérence globale des échanges**, une identification fiable des acteurs et du patient, ainsi qu’une homogénéité de mise en œuvre entre les flux.

##### Eléments de contrôle du message ORU ou MDM

###### Le segment MSH -- Header du message

Les éléments de contrôle du message HL7 sont portés par le segment d'entête MSH. Le tableau ci-dessous liste les champs à renseigner pour le segment MSH :

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
        <p><span class="hl7-color">|</span> séparateur de champ</p>
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
        <p><span class="hl7-color">^~\&</span> : séparateur de composant, répétition, caractère d'échappement, séparateur de sous-composants</p>
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
        <p>Horodatage du message</p>
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
        Type du message 
<br> <span class="hl7-color">ORM^O01^ORM_O01</span>
<br><span class="hl7-color">ORU^R01^ORU_R01</span>
<br><span class="hl7-color">OMI^O23^OMI_O23</span>
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
<br><span class="hl7-color"> P </span> : en production 
<br><span class="hl7-color"> T </span> : message de test 
 <br><span class="hl7-color"> D </span>: environnement de debug</p>
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
<br><span class="hl7-color"> 2.5.1</span>
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
        <p><span class="hl7-color">UNICODE UTF-8 ou 8859/15</span></p>
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
        <p>MSH-21</p>
      </td>
      <td>
        <p>Identifiant du profil de message</p>
        <p>MSH-21.1 : Entity Identifier (<span class="hl7-color">2.1</span>)</p>
        <p>MSH-21.2 : Namespace Id</p>
        <p><span class="hl7-color">CISIS_TLR_HL7_V2</span> </p>
      </td>
      <td>
        <p>EI</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
  </tbody>
</table>

###### Exemples

Entête MSH d'un message ORM :

`MSH|^~\&|RIS|CHU_X|SI-TLR|PLAT-TLR|202310030830||ORM^O01^ORM_O01|12345|P|2.5.1|||||FRA|8859/15|||2.1^ CISIS_TLR_HL7_V2`

##### Les données concernant le patient et la venue du patient

Le message HL7 est centré sur un seul patient. Les informations concernant le patient sont décrites par le segment requis PID. Le segment PV1, requis, représente la venue courante du patient.

Ces deux segments doivent être renseignés conformément à la spécification « [PAM -- National extension France » version 2.11](https://www.interopsante.org/publications) publiée en 2024. Si l'INS est véhiculé, le segment PID doit suivre les contraintes décrites dans l'annexe CI-SIS « [Prise en charge de l'identifiant National de Santé (INS) dans les standards d'interopérabilité et les volets du CI-SIS](https://esante.gouv.fr/annexe-prise-en-charge-de-lins-dans-les-volets-du-ci-sis) ».

Pour le segment PID, ce volet ajoute une contrainte particulière sur le PID-18 par rapport à PAM.FR. Il doit être renseigné si connu afin de pouvoir calculer des indicateurs, dans le contexte de l'alimentation du DMP.

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
        <p>PID-3</p>
      </td>
      <td>
        <p>Identifiants du patient</p>
      </td>
      <td>
        <p>CX</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>PID-5</p>
      </td>
      <td>
        <p>Nom du patient</p>
      </td>
      <td>
        <p>XPN</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>PID-18 (2)</p>
      </td>
      <td>
        <p>N° de dossier administratif</p>
      </td>
      <td>
        <p>CX</p>
      </td>
      <td>
        <p>RE</p>
      </td>
    </tr>
  </tbody>
</table>

Le PID-3 doit être identique aux identifiants de patient portés par le document CDA (recordTarget/patientRole/id).

Pour le segment PV1, ce volet ajoute les contraintes suivantes :

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
        <p>PV1-2</p>
      </td>
      <td>
        <p>Classe du patient </p>
      </td>
      <td>
        <p>IS</p>
      </td>
      <td>
        <p>R</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>PV1-19 (2)(4) </p>
      </td>
      <td>
        <p>Identifiant de la venue</p>
      </td>
      <td>
        <p>CX</p>
      </td>
      <td>
        <p> C (3)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>PV1-44 (2)</p>
      </td>
      <td>
        <p>Date d'entrée du patient</p>
      </td>
      <td>
        <p>TS</p>
      </td>
      <td>
        <p>RE</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>PV1-45 (2)</p>
      </td>
      <td>
        <p>Date de sortie du patient</p>
      </td>
      <td>
        <p>TS</p>
      </td>
      <td>
        <p>RE</p>
      </td>
    </tr>
  </tbody>
</table>

<blockquote class="stu-note">
    <p>
    <b>(2) :</b> A noter que ces champs sont à renseigner, s'ils sont connus, par le système expéditeur afin de pouvoir calculer des indicateurs.
    </p>
</blockquote>

<blockquote class="stu-note">
    <p>
    <b>(3) :</b> Le champ PV1-19 est requis lorsque le PV1-2 prend la valeur E, I, O ou R. Si PV1-2 prend la valeur N alors PV1-19 est requis si connu.
    </p>
</blockquote>

<blockquote class="stu-note">
    <p>
    <b>(4) :</b> Dans le cadre du volet Téléradiologie, le champ PV1-19 Visit Number est utilisé pour véhiculer l’identifiant du rendez-vous issu des flux SIU.
    </p>
</blockquote>

<br>

#### Contraintes spécifiques au volet Téléradiologie

Un second niveau de contraintes est défini **spécifiquement pour chaque flux**, en fonction du type de message et du rôle fonctionnel attendu.  
Ces contraintes portent notamment sur les segments métiers suivants, selon les flux :

- **ORC (Common Order)** : gestion de la demande, de son cycle de vie et de ses états ;
- **OBR (Observation Request)** : description de l’examen, des actes et de leurs identifiants ;
- **OBX (Observation Result)** : transmission d’informations cliniques structurées ou de références documentaires ;
- **IPC (Imaging Procedure Control)** : partage du contexte de réalisation des études et procédures d’imagerie.

Pour chaque flux, les contraintes précisent :

- les **segments obligatoires et optionnels** ;
- les **champs requis, conditionnels ou interdits** ;
- les **règles de cardinalité, de codage et de valeurs attendues** ;
- les éventuelles **références aux profils IHE ou spécifications nationales** applicables.

{% include st_flux1.md %}

<br>

{% include st_flux2.md %}

<br>

{% include st_flux3.md %}

<br>

{% include st_flux4.md %}