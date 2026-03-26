# Test - Volet Téléradiologie v0.1.0

* [**Table of Contents**](toc.md)
* **Test**

## Test

### Organisation des tests

#### Espace de test

L’espace de test mis à disposition par l’ANS s’appuie sur l’outil **EVSClient**, utilisé afin de vérifier la conformité des formats d’échange aux spécifications nationales.

Dans sa globalité, le service EVSClient permet notamment la validation :

* des documents CDA
* des messages HL7 v2
* des archives IHE_XDM.ZIP utilisées pour les échanges documentaires
* des ressources FHIR

Dans le cadre du volet **Téléradiologie**, EVSClient permet de vérifier la conformité des messages HL7 v2 échangés au regard des profils définis dans la [spécification technique](./specifications_techniques.md).

Les validateurs suivants sont mis à disposition :

* ORM^O01^ORM_O01 — Flux de transmission de la demande d’examen d’imagerie
* ORM^O01^ORM_O01 — Flux d’annulation de la demande d’examen d’imagerie
* ORU^R01^ORU_R01 — Flux de réponse métier à la demande d’examen d’imagerie
* OMI^O23^OMI_O23 — Flux de transmission d’un complément d’information post-examen
* ACK - Acquittement applicatif dans le cadre du volet téléradiologie

Ces validateurs sont accessibles en ligne à l’adresse suivante : [https://interop.esante.gouv.fr/evs/hl7v2/validator.seam?standard=45](https://interop.esante.gouv.fr/evs/hl7v2/validator.seam?standard=45)

Le mode opératoire pour utiliser les validateurs est le suivant :

1. **Charger le message à valider**
* Coller le message HL7 v2 dans la zone de texte prévue à cet effet
* ou charger un fichier via le bouton « **+ Add…** », les formats acceptés sont : `.txt`, `.hl7`, `.er7`

1. **Sélectionner le profil de message HL7**
* Dans l’encart « **Sélection du profil de message HL7** », choisir le validateur correspondant au flux à tester
* Les validateurs Téléradiologie disponibles sont les suivants :

| | | |
| :--- | :--- | :--- |
| Créateur Téléradiologie | TransmissionDemandeIMG | ORM^O01^ORM_O01 (NW) |
| Créateur Téléradiologie | AnnulationDemandeIMG | ORM^O01^ORM_O01 (CA) |
| Créateur Téléradiologie | ReponseDemandeIMG | ORU^R01^ORU_R01 (OK / OC) |
| Créateur Téléradiologie | TransmissionComplementIMG | OMI^O23^OMI_O23 (SR) |
| Consommateur Téléradiologie | ACK_TLR | ACK |

Le bouton « **Deviner le profil de message** » peut être utilisé pour proposer automatiquement un premier filtrage du profil applicable.
1. **Lancer la validation**
* Cliquer sur l’icône en forme de flèche pour exécuter la validation

