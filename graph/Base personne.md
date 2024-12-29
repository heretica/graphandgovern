---
entite: base
parent: "[[CRM]]"
---


La base de données "Personnes" est un composant essentiel du système d'information de l'entreprise. Elle contient les informations relatives aux individus en interaction avec l'organisation, tels que les employés, clients ou partenaires. Ce document décrit la structure, les caractéristiques techniques et les bonnes pratiques associées à cette base de données.

## Objectif

Fournir une documentation claire et détaillée de la base de données "Personnes" pour garantir une compréhension commune entre les équipes techniques et fonctionnelles, et faciliter son utilisation, son extension ou sa maintenance.

## Schéma de la Base de Données

### Nom de la Table : `personnes`

#### Champs Principaux

1. **email** _(clé primaire)_
    
    - **Type** : VARCHAR(255)
    - **Description** : Adresse email unique de la personne.
    - **Contraintes** :
        - Non nul.
        - Doit être unique.
2. **nom**
    
    - **Type** : VARCHAR(255)
    - **Description** : Nom de la personne.
    - **Contraintes** :
        - Non nul.

#### Champs Complémentaires (facultatifs)

3. **prenom**
    
    - **Type** : VARCHAR(255)
    - **Description** : Prénom de la personne.
    - **Contraintes** : Optionnel.
4. **date_naissance**
    
    - **Type** : DATE
    - **Description** : Date de naissance de la personne.
    - **Contraintes** : Optionnel.
5. **telephone**
    
    - **Type** : VARCHAR(15)
    - **Description** : Numéro de téléphone de la personne.
    - **Contraintes** : Optionnel.
6. **adresse**
    
    - **Type** : TEXT
    - **Description** : Adresse postale complète de la personne.
    - **Contraintes** : Optionnel.

## Index et Clés

- **Clé Primaire** : `email`
- **Index Secondaires** (si nécessaire) :
    - Index sur le champ `nom` pour accélérer les recherches par nom.

## Relations avec d'autres Tables

- **Table `transactions`** :
    - Une relation peut être établie entre une personne et les transactions effectuées via le champ `email`.
- **Table `projets`** :
    - Une personne peut être associée à un ou plusieurs projets via une clé étrangère.

## Bonnes Pratiques

- **Validation des Données** :
    - Assurer l'unicité des adresses email avec la clé primaire.
    - Vérifier la validité des adresses email (format standard).
- **Archivage** :
    - Mettre en place une stratégie pour les personnes inactives (ex : marquage ou suppression après une certaine période).
- **Sécurité** :
    - Chiffrer les données sensibles comme l'adresse ou le téléphone.
    - Restreindre les droits d'accès à la table en fonction des rôles des utilisateurs.
- **Sauvegarde** :
    - Programmer des sauvegardes régulières de la base de données.

## Exemple de Requête SQL

### Création de la Table

```sql
CREATE TABLE personnes (
    email VARCHAR(255) PRIMARY KEY,
    nom VARCHAR(255) NOT NULL,
    prenom VARCHAR(255),
    date_naissance DATE,
    telephone VARCHAR(15),
    adresse TEXT
);
```

### Ajout d'une Personne

```sql
INSERT INTO personnes (email, nom, prenom, date_naissance, telephone, adresse)
VALUES ('j.doe@example.com', 'Doe', 'John', '1990-05-15', '0123456789', '123 Rue Principale, Paris, France');
```

### Consultation des Personnes par Nom

```sql
SELECT * FROM personnes WHERE nom = 'Doe';
```

## Conclusion

La table `personnes` est essentielle pour la gestion des individus interagissant avec l'entreprise. Cette documentation vise à standardiser son utilisation et à en assurer une maintenance efficace. Les extensions futures doivent respecter la structure décrite et les bonnes pratiques établies ici.