# Gestion des Comptes Bancaires - Spring Boot

## Projet réalisé par Zineb Feth-Eddine

---

## Introduction

Ce projet consiste à développer une application de gestion de comptes bancaires utilisant **Spring Boot**, **Spring Data JPA**, et **Swagger** pour la gestion des clients et des opérations bancaires.

L'application permet de gérer les comptes bancaires (comptes courants et comptes épargne), les clients, ainsi que les opérations de type **débit** et **crédit**.

---

## Objectifs du projet

L'objectif de ce projet est de créer une application de gestion de comptes bancaires. Cette application permet de gérer les comptes de clients avec les fonctionnalités suivantes :

- Chaque **compte bancaire** appartient à un client.
- Un compte peut subir plusieurs opérations de type **débit** ou **crédit**.
- Deux types de comptes sont gérés :
  - **Comptes courants**
  - **Comptes épargnes**

Les étapes principales de ce projet sont :
1. Créer un projet Spring Boot pour le backend.
2. Créer les entités **JPA** pour les objets suivants :
   - **Customer** (Client)
   - **BankAccount** (Compte bancaire)
   - **SavingAccount** (Compte épargne)
   - **CurrentAccount** (Compte courant)
   - **AccountOperation** (Opération bancaire)
3. Créer les interfaces **JPA Repository** en utilisant **Spring Data**.
4. Tester la couche **DAO** (Data Access Object) pour vérifier l'interaction avec la base de données.
5. Créer la **couche service** pour implémenter la logique métier.
6. Créer des **DTOs** (Data Transfer Objects) pour la communication entre la couche service et la couche contrôleur.
7. Créer un **RestController** pour exposer les API RESTful.
8. Tester les **web services Restful** pour valider le bon fonctionnement de l'API.

---

## Swagger et Spring Boot 3

Swagger est un outil de documentation et de test d'API qui permet de faciliter l'intégration avec des services RESTful. Pour intégrer Swagger dans votre projet Spring Boot, vous devez ajouter la dépendance suivante dans le fichier `pom.xml` :

### Dépendance Swagger

Ajoutez la dépendance suivante dans votre fichier `pom.xml` sous la section `<dependencies>` :

---
(xml)
<dependency> 
   <groupId>org.springdoc</groupId> 
   <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId> 
   <version>2.1.0</version> 
</dependency>

---

## Technologies utilisées

- **Spring Boot** pour le développement de l'API backend.
- **Spring Data JPA** pour l'accès aux données.
- **Swagger** pour la documentation et l'interaction avec les API.
- **MySQL** ou **H2** comme base de données (configurable dans `application.properties`).


## Fonctionnalités

- **Gestion des clients** : Création, lecture et mise à jour des informations des clients.
- **Comptes bancaires** : Gestion de deux types de comptes :
  - **Comptes courants**
  - **Comptes épargne**
- **Opérations bancaires** : Ajout de transactions de type **débit** et **crédit** aux comptes.

## Prérequis

Avant de commencer, vous devez avoir installé les éléments suivants :

- Java (J'ai utilisé Java 8)
- Maven
- Base de données MySQL ou H2 (configurable dans `application.properties`)


### Explications :

- **GET /customers** : Permet de récupérer tous les clients.
- **POST /customers** : Permet de créer un nouveau client dans le système.
- **GET /accounts** : Récupère la liste de tous les comptes bancaires.
- **POST /accounts** : Crée un nouveau compte bancaire associé à un client.
- **POST /accounts/{id}/operations** : Permet d'ajouter une opération (débit ou crédit) sur un compte bancaire.

### 1. Structure de la base de données

L'image montre la structure de la base de données, qui comprend les tables suivantes :
- **account_operation** : Table contenant les opérations effectuées sur les comptes bancaires (débits et crédits).
- **bank_account** : Table représentant les comptes bancaires, avec des informations sur le type de compte (compte courant ou épargne) et le solde.
- **customer** : Table stockant les informations des clients, comme leur nom et leur adresse e-mail.
- 
![Structure de la base de données](Digital_banking_backend_Zineb_Fetheddine\Screens\1.png)


### 2. Données des clients dans la base de données

Cette image montre les données stockées dans la table `customer`, où chaque ligne représente un client avec des colonnes pour l'`id`, l'`email`, et le `name`. Elle illustre les informations des clients actuellement enregistrées dans la base de données.

![données](Digital_banking_backend_Zineb_Fetheddine\Screens\2.png)

L'image montre les données des clients stockées dans la table `customer`. Elle présente une vue avec les colonnes suivantes :
- **id** : Identifiant unique du client.
- **email** : Adresse e-mail du client.
- **name** : Nom du client.

Les actions disponibles, telles que **éditer**, **copier**, **supprimer**, et **exporter**, permettent de gérer les enregistrements des clients dans la base de données. Dans l'exemple, on voit quatre clients enregistrés avec leurs informations.

![Données des clients dans la base de données](Digital_banking_backend_Zineb_Fetheddine\Screens\3.png)
#### 3. Utilisation de Postman pour créer un client : 

Cette image montre l'utilisation de Postman pour envoyer une requête `POST` à l'API pour créer un nouveau client. Le corps de la requête contient les informations du client (nom et e-mail). La réponse de l'API renvoie un objet avec un nouvel `id` généré pour le client.

![Données des clients dans la base de données](Digital_banking_backend_Zineb_Fetheddine\Screens\postman1.jpg)

### 4. Utilisation de Postman pour supprimer un client

Cette image montre l'utilisation de Postman pour envoyer une requête `DELETE` à l'API afin de supprimer un client existant (ici, avec l'ID 2). La requête renvoie une erreur interne du serveur avec un code **500**, ce qui indique que quelque chose n'a pas fonctionné correctement au niveau du serveur.

![Données des clients dans la base de données](Digital_banking_backend_Zineb_Fetheddine\Screens\postman2.jpg)

### 6. Utilisation de Postman pour récupérer un client

Cette image montre l'utilisation de Postman pour envoyer une requête `GET` à l'API afin de récupérer un client spécifique (ici, avec l'ID 5). La réponse renvoie les détails du client, y compris son `id`, `name`, et `email`.

![Données des clients dans la base de données](Digital_banking_backend_Zineb_Fetheddine\Screens\postman3.jpg)

### 7. Utilisation de Postman pour mettre à jour un client

Cette image montre l'utilisation de Postman pour envoyer une requête `PUT` à l'API afin de mettre à jour les informations d'un client existant (ici, avec l'ID 5). La requête inclut les nouvelles valeurs pour le `name` et l'`email` du client.

![Données des clients dans la base de données](Digital_banking_backend_Zineb_Fetheddine\Screens\postman4.jpg)


### 4. Réponse d'API dans Swagger UI

Les images montrent l'interface Swagger UI où vous pouvez visualiser et tester les différentes API disponibles. Sur l'image ci-dessous, vous pouvez voir la réponse détaillée pour une requête de type `GET` sur le compte bancaire, qui renvoie les informations d'un compte bancaire spécifique, incluant les données du client associé.

La réponse inclut des informations comme :
- **type** : Le type de compte (ici, un compte courant).
- **id** : L'identifiant unique du compte bancaire.
- **balance** : Le solde du compte bancaire.
- **customerDTO** : Un objet contenant les informations du client, comme l'`id`, le `name` et l'`email`.
- **overDraft** : Le montant du découvert autorisé sur le compte bancaire.
- 
#### Exemple de réponse de l'API :

(json)
{
  "type": "CurrentAccount",
  "id": "357ea25d-216e-4bf9-bd5f-ee9dc2ab06a8",
  "balance": 597686.200354441,
  "createdAt": "2025-01-04T22:55:09.000+00:00",
  "status": null,
  "customerDTO": {
    "id": 1,
    "name": "Zineb",
    "email": "zineb.fetheddine@gmail.com"
  },
  "overDraft": 9000
}

-**Affichage de tous les comptes**

![Reponse](Digital_banking_backend_Zineb_Fetheddine\Screens\Acc.png)

-**Affichage d'un compte selon l'ID**

![Reponse](Digital_banking_backend_Zineb_Fetheddine\Screens\HHH.png)

---
## Conclusion

Ce projet de gestion de comptes bancaires avec **Spring Boot**, **Spring Data JPA** et **Swagger** permet de créer une application robuste et évolutive pour la gestion des clients et des opérations bancaires. En utilisant une architecture modulaire et bien définie, le projet assure la séparation des responsabilités entre les différentes couches (DAO, service, contrôleur).

L'utilisation de **Swagger** améliore l'interaction avec l'API en fournissant une documentation claire et interactive, facilitant ainsi les tests et la validation des différentes routes disponibles. L'intégration de **Spring Data JPA** garantit une gestion efficace des données dans la base de données **MySQL** ou **H2**, tout en offrant une flexibilité pour l'ajout de nouveaux types de comptes ou d'opérations bancaires à l'avenir.

Ce projet est une base solide qui peut être étendue avec des fonctionnalités supplémentaires, telles que la gestion de l'authentification des utilisateurs, l'intégration d'un front-end, et l'ajout de tests unitaires et d'intégration pour assurer la qualité du code.

---
