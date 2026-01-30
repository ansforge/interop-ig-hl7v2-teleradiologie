### Présentation synthétique du volet Téléradiologie

Cette étude s'inscrit dans le cadre des besoins d'interopérabilité associés au volet « Téléradiologie ». Ce volet a pour objectif de décrire les échanges, et leur contenu, nécessaires à la prise en charge d'un patient lorsque l'interprétation radiologique est réalisée à distance, entre une structure d'imagerie (lieu de réalisation de l'acte) et une plateforme de téléradiologie (lieu d'interprétation).

Les échanges d'informations interviennent principalement entre :

- Le RIS (Système d'Information Radiologique) de la structure d'accueil du patient
- Le système d'information de la plateforme de téléradiologie

La présente étude couvre les échanges décrits dans la Spécification fonctionnelle des échanges - Téléradiologie, à savoir :

- La transmission d'une demande d'examen d'imagerie
- L'annulation d'une demande d'examen
- La réponse à une demande d'examen (acceptation avec protocole d'imagerie ou refus)
- La transmission d'informations complémentaires post-examen

Les concepts métiers à véhiculer dans ces flux sont décrits en [étape 4 et 5](./specifications_fonctionnelles.html#identification-des-concepts-véhiculés-dans-les-flux-dinformations-et-correspondance-avec-les-classes-et-attributs-du-MOS) de la spécification fonctionnelle et couvrent plusieurs catégories de données essentielles à la pratique de la téléradiologie :

- Données administratives et d'identification : identités patient et professionnels de santé, identifiants de demandes et d'examens, informations de structure
- Données cliniques et de prescription : motif d'examen, indications, contexte clinique fourni par le médecin de proximité
- Données de protocole d'imagerie : éléments nécessaires à la réalisation de l'acte, fournis par le radiologue distant
- Données techniques et informations post-acte : conditions de réalisation, données documentaires

Le choix final des normes ou standards devra permettre de couvrir l'intégralité des données véhiculées dans le cadre de la téléradiologie, ainsi que les scénarios d'échanges entre la structure d'imagerie et le service d'interprétation distant.