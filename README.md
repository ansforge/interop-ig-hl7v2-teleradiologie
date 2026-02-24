https://ansforge.github.io/interop-ig-hl7v2-teleradiologie/main/ig

![Logo_LEF_CI-SIS](https://user-images.githubusercontent.com/48218773/227532484-eff82649-4e42-49c6-966a-dc3ea78cf59c.png)

[![Workflow Init](https://github.com/ansforge/IG-fhir-partage-de-documents-de-sante/actions/workflows/fhir-workflows.yml/badge.svg)](https://github.com/ansforge/IG-fhir-partage-de-documents-de-sante/actions/workflows/fhir-workflows.yml)

# Contexte

## Contexte métier du projet

La téléradiologie correspond aux actes de télédiagnostic radiologique réalisés par un radiologue exerçant à distance de la structure où l’examen d’imagerie a été produit.  

Ce volet a pour objectif de décrire les échanges et leur contenu nécessaires à la prise en charge d’un patient lorsque l’interprétation radiologique est réalisée à distance, entre une **structure d’imagerie** (lieu de réalisation de l’acte) et une **plateforme de téléradiologie** (lieu d’interprétation).

Les échanges d’informations interviennent principalement entre :  

- Le **RIS** (Système d’Information Radiologique) de la structure d’accueil du patient  
- Le **système d’information de la plateforme de téléradiologie**  

Le volet couvre les échanges suivants :  

- Transmission d’une demande d’examen d’imagerie  
- Annulation d’une demande d’examen  
- Réponse à une demande d’examen (acceptation avec protocole d’imagerie ou refus)  
- Transmission d’informations complémentaires post-examen  

Ces échanges visent à véhiculer plusieurs catégories de données essentielles à la pratique de la téléradiologie :  

- **Données administratives et d’identification** : identités du patient et des professionnels de santé, identifiants de demandes et d’examens, informations de structure  
- **Données cliniques et de prescription** : motif d’examen, indications, contexte clinique fourni par le médecin prescripteur  
- **Données de protocole d’imagerie** : éléments nécessaires à la réalisation de l’acte, fournis par le radiologue distant  
- **Données techniques et informations post-acte** : conditions de réalisation, données documentaires et résultats complémentaires

## Contexte technique du projet

Le présent volet définit les modalités d’échange des informations de téléradiologie au moyen du standard **HL7 version 2.5.1**.

Il précise :
- les profils de messages,
- les segments et champs utilisés,
- les cardinalités,
- les règles d’usage nécessaires à l’interopérabilité entre les systèmes d’information impliqués, en particulier les **RIS** et les **SI de téléradiologie**.

Les échanges sont basés sur des messages conformes à HL7 v2.5.1. Lorsque cela est applicable, la spécification :
- s’appuie sur les profils du domaine IHE Radiology, notamment le profil **Scheduled Workflow (SWF.b)**, afin d’assurer la cohérence avec les workflows d’imagerie existants ;
- prend en compte les principes du profil **IHE PAM-FR** pour la gestion de l’identité patient, en particulier l’Identité Nationale de Santé (INS) ;
- applique, lorsque pertinent, les contraintes définies par la spécification *Contraintes sur les types de données HL7 v2.5 applicables aux profils d’intégration du cadre technique IT Infrastructure* publiée par Interop’Santé.

Le tableau ci-dessous décrit, pour chaque flux métier inclus dans le périmètre du volet Téléradiologie, le message HL7 v2 et l’événement HL7 v2 associé utilisés pour supporter l’échange.

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
        <p>O23 – Imaging Order Message (Order Control = SR)</p>
      </td>
    </tr>
  </tbody>
</table>

# CI/CD

Les workflows associés à ce repository (.github/workflows) permettent :

* D'executer Sushi pour vérifier la grammaire
* De faire les tests avec le validator_cli
* De publier les pages : https://ansforge.github.io/{nom du repo}/{nom de la branche}/ig

# Notes

Un commentaire ? Une remarque ? Utilisez les GitHub [issues](https://docs.github.com/fr/issues) pour indiquer vos propositions d'amélioration et de correction.

## Acronymes

* **CDA** : Clinical Document Architecture  
* **DMP** : Dossier Médical Partagé
* **DICOM** : Digital Imaging and Communications in Medicine
* **DRIM-M** : Data Radiologie Imagerie Médicale et Médecine Nucléaire
* **FHIR** : Fast Healthcare Interoperability Resources  
* **HL7** : Health Level Seven  
* **HL7 v2** : Health Level Seven Version 2  
* **IG** : Implementation Guide  
* **IHE** : Integrating the Healthcare Enterprise  
* **INS** : Identité Nationale de Santé  
* **PACS** : Picture Archiving and Communication System  
* **PS** : Professionnel de Santé  
* **RIS** : Radiology Information System 
