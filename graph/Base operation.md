---
entite: base
parent: "[[ERP]]"
---
La base de données "Opérations" est un composant clé du système d'information de l'entreprise. Elle contient les informations relatives aux opérations réalisées par l'entreprise, permettant leur suivi, analyse et gestion. Ce document décrit la structure, les caractéristiques techniques et les bonnes pratiques associées à cette base de données.

## Objectif

Fournir une documentation claire et détaillée de la base de données "Opérations" pour garantir une compréhension commune entre les équipes techniques et fonctionnelles, et faciliter son utilisation, son extension ou sa maintenance.

## Schéma de la Base de Données

### Nom de la Table : `operations`

#### Champs Principaux

1. **id_op** _(clé primaire)_
    
    - **Type** : INTEGER
    - **Description** : Identifiant unique pour chaque opération.
    - **Contraintes** :
        - Non nul.
        - Valeur auto-incrémentée (si applicable).
2. **nom_op**
    
    - **Type** : VARCHAR(255)
    - **Description** : Nom ou désignation de l'opération.
    - **Contraintes** :
        - Non nul.

#### Champs Complémentaires (facultatifs)

3. **description_op**
    
    - **Type** : TEXT
    - **Description** : Description détaillée de l'opération.
    - **Contraintes** : Optionnel.
4. **date_creation**
    
    - **Type** : DATE/TIMESTAMP
    - **Description** : Date et heure de création de l'opération.
    - **Contraintes** : Optionnel. Peut être défini par défaut à la date/heure actuelle.
5. **statut_op**
    
    - **Type** : ENUM('en cours', 'terminé', 'annulé')
    - **Description** : Statut actuel de l'opération.
    - **Contraintes** : Optionnel.
6. **responsable_op**
    
    - **Type** : VARCHAR(255)
    - **Description** : Nom du responsable ou de l'entité en charge de l'opération.
    - **Contraintes** : Optionnel.

## Index et Clés

- **Clé Primaire** : `id_op`
- **Index Secondaires** (si nécessaire) :
    - Index sur le champ `nom_op` pour accélérer les recherches textuelles.
    - Index composite possible sur `statut_op` et `date_creation` pour des analyses fréquentes par période et statut.

## Relations avec d'autres Tables

- **Table `utilisateurs`** :
    - Relation possible via le champ `responsable_op` si celui-ci est remplacé par une clé étrangère vers un identifiant d'utilisateur.
- **Table `projets`** :
    - Une opération peut être liée à un projet spécifique via un champ supplémentaire `id_projet` (clé étrangère).

## Bonnes Pratiques

- **Validation des Données** :
    - Assurer l'unicité des identifiants avec la clé primaire.
    - Implémenter des contrôles de saisie pour le champ `nom_op` (e.g., éviter les doublons non désirés).
- **Archivage** :
    - Mettre en place une stratégie d'archivage pour les anciennes opérations afin de maintenir les performances.
- **Sécurité** :
    - Restreindre les droits d'accès à la table en fonction des rôles des utilisateurs.
- **Sauvegarde** :
    - Programmer des sauvegardes régulières de la base de données.

## Exemple de Requête SQL

### Création de la Table

```sql
CREATE TABLE operations (
    id_op INTEGER PRIMARY KEY AUTOINCREMENT,
    nom_op VARCHAR(255) NOT NULL,
    description_op TEXT,
    date_creation TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    statut_op ENUM('en cours', 'terminé', 'annulé'),
    responsable_op VARCHAR(255)
);
```

### Ajout d'une Opération

```sql
INSERT INTO operations (nom_op, description_op, statut_op, responsable_op)
VALUES ('Lancement Produit', 'Préparation du lancement du nouveau produit', 'en cours', 'Jean Dupont');
```

### Consultation des Opérations Actives

```sql
SELECT * FROM operations WHERE statut_op = 'en cours';
```

## Conclusion

La table `operations` est essentielle pour la gestion des opérations de l'entreprise. Cette documentation vise à standardiser son utilisation et à en assurer une maintenance efficace. Les extensions futures doivent respecter la structure décrite et les bonnes pratiques établies ici.