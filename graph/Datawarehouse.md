---
entite: base
---
Ce document a pour objectif de décrire les aspects techniques du Datawarehouse et ses contrats d'interface avec le système ERP. Il inclut les spécifications des flux de données, les politiques d'accès, et les contraintes liées à l'utilisation.

---

#### 2. Description du Datawarehouse

##### 2.1 Rôle du Datawarehouse

Le Datawarehouse sert de réservoir central pour l’analyse et le reporting des données stratégiques de l’entreprise. Il regroupe des données consolidées provenant de différentes sources, principalement l'ERP.

##### 2.2 Architecture

- **Base de données** : PostgreSQL 14
- **Structure** : Modèle en étoile (Star Schema)
    - Dimensions : Clients, Produits, Temps, Régions
    - Faits : Ventes, Stocks, Commandes
- **Stockage** : SSD haute performance
- **Environnement** : Cloud hybride (Azure et sur site)

##### 2.3 Sécurité et Accès

Seul le directeur de la production a un accès au Datawarehouse. Cet accès est réglementé par des politiques strictes :

- **Authentification** : Bi-facteur (MFA)
- **Autorisation** : Rôle unique avec privilèges limités
- **Audit** : Suivi des connexions et des requêtes exécutées

---

#### 3. Contrats d'Interface avec l'ERP

##### 3.1 Objectif des Interfaces

Les interfaces assurent le transfert des données entre l'ERP et le Datawarehouse pour maintenir des informations précises et à jour.

##### 3.2 Description Technique

- **Type d'interface** : Extraction-Transformation-Chargement (ETL)
- **Outil utilisé** : Talend Data Integration
- **Format des données** :
    - Entrées : Fichiers CSV, JSON
    - Sorties : Tables relationnelles

##### 3.3 Flux de Données

1. **Extraction**
    - Source : ERP (SAP)
    - Fréquence : Quotidienne à 02h00
    - Mode : API REST et requêtes SQL
2. **Transformation**
    - Nettoyage des données (valeurs nulles, doublons)
    - Agrégation des faits et harmonisation des dimensions
3. **Chargement**
    - Destination : Tables de faits et dimensions du Datawarehouse

##### 3.4 Surveillance des Interfaces

- **Planification** : Ordonnanceur CRON
- **Alertes** : Emails et logs en cas d'échec
- **Durée moyenne** : 45 minutes

---

#### 4. Gestion des Données

##### 4.1 Qualité des Données

- **Validation** : Contrôles sur les types et les règles métier
- **Reporting** : Tableau de bord sur les échecs de flux

##### 4.2 Rétention et Archivage

- **Durée de rétention** : 7 ans
- **Archivage** : Compression et stockage sur un serveur SFTP

---

#### 5. Contraintes et Risques

##### 5.1 Contraintes

- Temps de latence entre l'ERP et le Datawarehouse
- Maintenance régulière des interfaces ETL

##### 5.2 Risques

- Pertes de données lors de l'extraction
- Erreurs de transformation pouvant altérer les analyses

---

#### 6. Conclusion

Ce Datawarehouse et ses interfaces avec l’ERP constituent un élément crucial pour la prise de décision dans l’entreprise. Leur mise en place, associée à des contrôles stricts et à une surveillance continue, garantit leur fiabilité et leur performance.