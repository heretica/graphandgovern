---
entite: applicatif
feeds: "[[Datawarehouse]]"
---
Ce document détaille les caractéristiques techniques de l’ERP (Enterprise Resource Planning) qui alimente le Datawarehouse. L’objectif est de décrire les modules clés, les formats de données, les flux d’intégration, et les mécanismes de gouvernance mis en place pour garantir la fiabilité et la continuité des échanges.

---

#### 2. Description de l’ERP

##### 2.1 Rôle de l’ERP

L’ERP est le système central de gestion des processus opérationnels de l’entreprise. Il gère les données relatives à :

- La gestion des ventes et des clients
- La planification et le suivi de la production
- La gestion des stocks et des approvisionnements
- La comptabilité et les finances

##### 2.2 Modules Clés

1. **Module Ventes (SD)** :
    - Gestion des commandes clients
    - Suivi des factures et paiements
2. **Module Production (PP)** :
    - Planification de la production
    - Suivi des ordres de fabrication
3. **Module Logistique (MM)** :
    - Gestion des stocks et inventaires
    - Approvisionnements et réceptions fournisseurs
4. **Module Finances (FI)** :
    - Suivi des comptes clients et fournisseurs
    - Analyses de rentabilité

##### 2.3 Architecture

- **Base de données** : Oracle Database 19c
- **Langage de programmation** : ABAP et Java
- **Hébergement** : Serveurs sur site
- **Sécurité** :
    - Chiffrement SSL des flux de données
    - Authentification LDAP pour les utilisateurs

---

#### 3. Flux d’Intégration avec le Datawarehouse

##### 3.1 Objectif des Intégrations

Transférer les données critiques des modules de l’ERP vers le Datawarehouse afin de permettre des analyses stratégiques fiables.

##### 3.2 Architecture des Interfaces

- **Type d’intégration** : ETL (Extraction, Transformation, Chargement)
- **Outil utilisé** : Talend Data Integration
- **Fréquence** : Extraction quotidienne à 02h00
- **Protocole** : API REST et connecteurs JDBC

##### 3.3 Format des Données Transférées

- **Données de sortie (ERP)** : JSON et CSV
- **Données de destination (Datawarehouse)** : Tables relationnelles PostgreSQL
- **Champs principaux** :
    - ID client, nom client, segment de marché
    - Références produits, quantités vendues, prix unitaire
    - Délais de livraison, statut de production

##### 3.4 Processus ETL

1. **Extraction**
    - Requêtes SQL pour les tables principales de l’ERP
    - Appels d’API pour des données en temps réel
2. **Transformation**
    - Standardisation des formats de date et des unités de mesure
    - Validation des données selon les règles métier
3. **Chargement**
    - Envoi vers les tables de faits et dimensions du Datawarehouse

---

#### 4. Gouvernance des Données

##### 4.1 Contrôle Qualité

- **Validation** : Contrôles systématiques sur la complétude et la cohérence des données avant chargement
- **Métriques suivies** : Taux d’erreurs dans les flux, temps moyen de traitement ETL

##### 4.2 Sécurité des Données

- **Accès** : Restreint aux administrateurs système
- **Audit** : Historique des accès et des modifications
- **Sauvegarde** : Quotidienne avec stockage redondant sur un serveur de secours

---

#### 5. Contraintes et Risques

##### 5.1 Contraintes

- Temps de latence entre l’ERP et le Datawarehouse
- Complexité des transformations liées à la volumétrie des données

##### 5.2 Risques

- Panne des interfaces ETL pouvant interrompre les flux de données
- Problèmes de synchronisation pouvant conduire à des écarts entre l’ERP et le Datawarehouse

---

#### 6. Conclusion

L’ERP joue un rôle essentiel dans l’alimentation du Datawarehouse en fournissant des données opérationnelles critiques. La mise en place de processus robustes et de contrôles rigoureux garantit la fiabilité et la continuité de cette intégration, indispensable pour le pilotage stratégique de l’entreprise.