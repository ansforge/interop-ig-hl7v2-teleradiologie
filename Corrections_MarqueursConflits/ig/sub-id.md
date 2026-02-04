# Utilisation du champ OBX-4 – Observation Sub-ID - Volet Téléradiologie v0.1.0-ballot

* [**Table of Contents**](toc.md)
* **Utilisation du champ OBX-4 – Observation Sub-ID**

## Utilisation du champ OBX-4 – Observation Sub-ID

Dans le cadre de la présente spécification, le champ **OBX-4 – Observation Sub-ID** est utilisé pour assurer le **regroupement logique et la différenciation** de plusieurs segments **OBX** se rapportant à un même concept métier.

Cette règle s’applique notamment aux cas suivants (liste non exhaustive) :

* produits administrés,
* appareil d’imagerie utilisé,
* localisation anatomique et précision topographique,

### Principe général

Lorsque plusieurs segments **OBX** sont utilisés pour décrire une même entité métier, ces segments :

* partagent le **même OBX-3 – Observation Identifier**,
* sont différenciés et associés à l’aide du champ **OBX-4 – Observation Sub-ID**.

Le Sub-ID est structuré sous la forme **n.m**, où :

* **n** correspond à l’identifiant d’une occurrence d’un même concept métier (par exemple un produit administré ou un appareil d’imagerie),
* **m** identifie la nature de l’information portée par le segment OBX au sein de cette occurrence.

Cette structuration permet :

* de regrouper explicitement les segments OBX décrivant une même entité,
* de gérer plusieurs occurrences d’un même concept dans un message,
* de conserver une structure lisible et interopérable.

### Contraintes d’utilisation

* Tous les segments OBX partageant un même **OBX-3** et un même **n** dans **OBX-4** sont considérés comme décrivant une **même occurrence métier**.
* Les valeurs possibles de **m** et leur signification sont définies dans les sections spécifiques à chaque flux.
* L’utilisation du champ **OBX-4** est **obligatoire** dès lors que plusieurs segments OBX partagent le même **OBX-3** dans un message.

### Exemple d’utilisation – Produit administré

Dans l’exemple ci-dessous, deux produits administrés sont transmis dans un message.
 Chaque produit est décrit à l’aide de trois segments OBX : type de produit, numéro de lot et quantité administrée.

```
OBX|1|CE|PRODUIT_ADMINISTRE^Produit administré^TLR_OBSERVATION|1.1|V09^Produits de diagnostic^ATC||||
OBX|2|TX|PRODUIT_ADMINISTRE^Produit administré|1.2|LOT123456||||
OBX|3|NM|PRODUIT_ADMINISTRE^Produit administré|1.3|120|mL|||
OBX|4|CE|PRODUIT_ADMINISTRE^Produit administré|2.1|V10^Produits thérapeutiques^ATC||||
OBX|5|TX|PRODUIT_ADMINISTRE^Produit administré|2.2|LOT789012||||
OBX|6|NM|PRODUIT_ADMINISTRE^Produit administré|2.3|80|mL|||

```

