### Evènements déclenchants

La présente partie décrit, pour chaque flux métier inclus dans le périmètre du volet Téléradiologie, le **message HL7 v2** et l’**événement HL7 v2 associé** utilisés pour supporter l’échange.

<table>
  <tbody>
    <tr>
      <th>
        <p>Flux métier</p>
      </th>
      <th>
        <p>Structure de message HL7 v2</p>
      </th>
      <th>
        <p>Événement HL7 v2</p>
      </th>
    </tr>
    <tr>
      <td>
        <p><strong>Transmission de la demande d’examen d’imagerie</strong></p>
      </td>
      <td>
        <p>ORM_O01</p>
      </td>
      <td>
        <p>O01 – Order message (Order Control = NW)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><strong>Annulation de la demande d’examen d’imagerie (1)</strong></p>
      </td>
      <td>
        <p>ORM_O01</p>
      </td>
      <td>
        <p>O01 – Order message (Order Control = CA)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><strong>Réponse à la demande d’examen d’imagerie</strong></p>
      </td>
      <td>
        <p>ORU_R01</p>
      </td>
      <td>
        <p>R01 – Unsolicited transmission of observation (Order Control = OK ou OC)</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><strong>Transmission d’un complément d’information post-acte</strong></p>
      </td>
      <td>
        <p>OMI_O23</p>
      </td>
      <td>
        <p>O23 – Imaging Order Message (Order Control = NW)</p>
      </td>
    </tr>
  </tbody>
</table>

<blockquote class="stu-note">
    <p>
    <b>(1) :</b> Le flux d'annulation est un flux <strong>optionnel</strong> dans le cadre du volet Téléradiologie. Son implémentation <strong>n’est pas obligatoire</strong> et peut être omise sans remettre en cause la conformité globale des échanges.
    </p>
</blockquote>

<br>

### Interactions entre les acteurs

La présente partie décrit les interactions entre les acteurs du volet Téléradiologie, au travers de diagrammes de séquence illustrant les échanges de messages HL7 v2 identifiés précédemment.

Les interactions sont présentées flux par flux. Chaque diagramme s’appuie sur le **profil de messages HL7 v2 retenu**. Le [diagramme de séquence complet est fourni en annexe](./diag_sequence.html).

#### Flux 1 et 2 - Transmission/Annulation d'une demande d'examen d'imagerie

Ce diagramme décrit les échanges techniques entre le RIS de la structure d’imagerie et le SI de téléradiologie pour la transmission et la gestion d’une demande d’examen d’imagerie.

<div style="
    text-align: center;
    margin: 1.5em auto;
">
    <img src="DiagSequ12.png"
         alt="Diagramme de séquence des flux 1 et 2"
         title="Diagramme de séquence des flux 1 et 2"
         style="
            max-width: 900px;
            width: 100%;
            height: auto;
            display: block;
            margin: 0 auto;
         ">

    <p style="
        font-size: 0.9em;
        color: #555;
        margin-top: 0.5em;
    ">
        Figure 1 – Diagramme de séquence des flux 1 et 2
    </p>
</div>

La demande d’examen est transmise du RIS vers le SI de téléradiologie au moyen d’un message **HL7 v2 ORM^O01^ORM_O01**.

Les options techniques suivantes sont représentées :

- lorsque la demande d’examen est disponible sous forme de document structuré, le RIS **doit** transmettre ce document au SI de téléradiologie en s'appuyant sur les transactions définies au sein du [volet de transmission de documents CDA-R2 en HL7 v2](./https://interop.esante.gouv.fr/ig/hl7v2/trans-cda-r2/index.html) ;
- lorsque plusieurs documents complémentaires sont associés à la demande, ceux-ci peuvent être transmis individuellement au SI de téléradiologie au travers de mécanismes également définis au sein du [volet de transmission de documents CDA-R2 en HL7 v2](./https://interop.esante.gouv.fr/ig/hl7v2/trans-cda-r2/index.html).

Enfin, le diagramme illustre la **possibilité d’annulation de la demande d’examen** par le RIS, notifiée au SI de téléradiologie au moyen d’un message **HL7 v2 ORM^O01^ORM_O01**, en cohérence avec les règles de gestion HL7 v2 et le profil IHE SWF.

#### Flux 3 Réponse à la demande d'examen d'imagerie

Ce diagramme décrit les échanges techniques consécutifs à la consultation et à l’évaluation d’une demande d’examen par le professionnel de santé effecteur au sein du SI de téléradiologie.

<div style="
    text-align: center;
    margin: 1.5em auto;
">
    <img src="Sequence3.png"
         alt="Diagramme de séquence du flux 3"
         title="Diagramme de séquence du flux 3"
         style="
            max-width: 900px;
            width: 100%;
            height: auto;
            display: block;
            margin: 0 auto;
         ">

    <p style="
        font-size: 0.9em;
        color: #555;
        margin-top: 0.5em;
    ">
        Figure 2 – Diagramme de séquence du flux 3
    </p>
</div>

Après réception de la demande d'examen d'imagerie, le professionnel de santé effecteur procède à son **évaluation** (acceptation ou refus).  
Le résultat de cette évaluation est notifié à la structure d’imagerie par l’émission d’un message **HL7 v2 ORU^R01^ORU_R01** depuis le SI de téléradiologie.

Les cas suivants sont couverts :

- **Acceptation de la demande** :  
  le message **ORU^R01** contient un ou plusieurs **protocoles d’imagerie**, véhiculés dans les segments **OBX** ;  
  le champ **ORC-1 (Order Control)** est valorisé à **OK**.

- **Refus de la demande** :  
  le message **ORU^R01** est transmis **sans protocole d’imagerie** ;  
  le champ **ORC-1 (Order Control)** est valorisé à **OC**.


#### Flux 4 Transmission d'un complément d'information post-examen

Ce diagramme décrit les échanges techniques intervenant après l’acceptation de la demande d’examen et la transmission du protocole d’imagerie.

<div style="
    text-align: center;
    margin: 1.5em auto;
">
    <img src="Sequence4.png"
         alt="Diagramme de séquence du flux 4"
         title="Diagramme de séquence du flux 4"
         style="
            max-width: 1000px;
            width: 100%;
            height: auto;
            display: block;
            margin: 0 auto;
         ">

    <p style="
        font-size: 0.9em;
        color: #555;
        margin-top: 0.5em;
    ">
        Figure 3 – Diagramme de séquence du flux 4
    </p>
</div>

À l’issue de cette acceptation, l’examen d’imagerie est réalisé au sein de la structure d’imagerie.  
Une fois l’examen effectué, le RIS transmet au SI de téléradiologie un ensemble de **compléments d’information post-examen**, destinés à permettre la **rédaction du compte rendu** par le professionnel de santé effecteur.

Ces informations sont transmises via un message **OMI^O23^OMI_023** conforme au profil IHE SWF.

Après rédaction du **compte rendu d’examen d'imagerie**, celui-ci est transmis par le SI de téléradiologie vers le RIS, afin de permettre sa **publication dans le DMP du patient**.
