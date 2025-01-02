# Gouvernance du projet 

Pour lancer un nouveau projet data avec vos données opérationnelles, vous pouvez impliquer plusieurs parties prenantes clés :

1. **Mme Laurent** : Elle peut être impliquée pour s'assurer que les données opérationnelles sont complètes et en temps réel, ce qui est crucial pour optimiser les performances et la réactivité. Elle peut aider à définir les besoins en données et à suivre les KPIs locaux.

2. **M. Dupont** : En tant que directeur de production, il peut jouer un rôle essentiel dans la définition des champs critiques et prioritaires à inclure dans le Datawarehouse. Il peut également superviser la mise en place de contrôles automatiques pour garantir la complétude des données.

3. **Équipes IT** : Elles peuvent être responsables de la mise en place des processus ETL, des règles de validation automatique, et de la sécurité des données. Elles travailleront en étroite collaboration avec les équipes opérationnelles pour s'assurer que les données critiques sont bien définies et intégrées.

4. **Équipes Opérationnelles** : Elles doivent être formées sur l'importance de la saisie complète des données dans l'ERP et peuvent fournir des retours sur les besoins spécifiques en données pour améliorer les processus de production et logistiques.

Ensemble, ces parties prenantes peuvent collaborer pour garantir que le projet data est bien aligné avec les objectifs opérationnels et stratégiques de l'organisation.


# Schéma de données idéal pour le projet

Il est essentiel de concevoir un schéma de données qui facilite la gestion efficace des interactions entre les différents acteurs et systèmes. En utilisant le schéma de données standard Frictionless, voici une proposition :

1. **Table `personnes`** :
   - `id_personne` (integer, primary key)
   - `nom` (string)
   - `prenom` (string)
   - `email` (string)
   - `role` (string)

2. **Table `fournisseurs`** :
   - `id_fournisseur` (integer, primary key)
   - `nom_fournisseur` (string)
   - `contact` (string)
   - `email` (string)
   - `telephone` (string)

3. **Table `achats`** :
   - `id_achat` (integer, primary key)
   - `id_fournisseur` (integer, foreign key)
   - `date_achat` (date)
   - `montant` (decimal)
   - `description` (string)

4. **Table `projets`** :
   - `id_projet` (integer, primary key)
   - `nom_projet` (string)
   - `date_debut` (date)
   - `date_fin` (date)
   - `id_responsable` (integer, foreign key)

5. **Table `utilisateurs`** :
   - `id_utilisateur` (integer, primary key)
   - `nom_utilisateur` (string)
   - `email` (string)
   - `role` (string)

6. **Table `operations`** :
   - `id_operation` (integer, primary key)
   - `id_projet` (integer, foreign key)
   - `description` (string)
   - `date_operation` (date)

Ce schéma permettrait une gestion centralisée et efficace des données, facilitant l'intégration et l'analyse des informations pour améliorer les processus décisionnels et opérationnels.

