# HBnB Project

## Par Ziri, Malak, Kevin

## Description

Le projet **HBnB** est une application web qui permet aux utilisateurs de créer, gérer et explorer des lieux. Les utilisateurs peuvent laisser des avis sur les lieux qu'ils ont visités et interagir avec diverses fonctionnalités comme la gestion des commodités. Ce document offre une vue complète de l'architecture, des fonctionnalités principales et de la logique métier du projet.

## Table des Matières

1. [Introduction](#introduction)
2. [Architecture de Haut Niveau](#architecture-de-haut-niveau)
3. [Diagramme de Classes de la Couche Logique Métier](#diagramme-de-classes-de-la-couche-logique-métier)
4. [API et Diagrammes de Séquence](#api-et-diagrammes-de-séquence)
5. [Justification Technique](#justification-technique)
6. [Architecture Technique](#architecture-technique)
7. [Conclusion](#conclusion)

## Introduction

Ce projet suit une architecture en couches et utilise un modèle de façade pour organiser les interactions entre les composants. Le document technique qui suit décrit les composants du projet, leurs relations et les flux d’interaction API.

## Architecture de Haut Niveau

L'architecture de l'application est modulaire et suit une structure en couches, où chaque module gère une partie clé du système.

![Architecture Haut Niveau](./path_to_your_image/file-RtwQpfE04n8xKpHJqe6bR1hG.png)

- **Modules principaux :**
  - Utilisateurs
  - Lieux
  - Avis
  - Commodités (Équipements)

## Diagramme de Classes de la Couche Logique Métier

Voici un aperçu des principales classes et leurs relations dans le système HBnB.

![Diagramme de Classes](./path_to_your_image/file-X7BhwjpwGTvrkbA4LzOjRtb2.png)

- **Utilisateur** : Représente un utilisateur de l'application.
- **Lieu** : Un lieu est un espace que l'utilisateur peut créer.
- **Équipement** : Commodités disponibles pour chaque lieu, telles que le Wi-Fi, piscine, etc.
- **Avis** : Les utilisateurs peuvent laisser des avis sur les lieux.
- **PlaceAmenity** : Classe d'association gérant la relation entre les lieux et les commodités.

### Relations :

- Un **Utilisateur** peut créer plusieurs **Lieux**.
- Un **Lieu** peut recevoir plusieurs **Avis**.
- Un **Lieu** peut avoir plusieurs **Commodités** via la classe **PlaceAmenity**.
- Un **Avis** est associé à un **Utilisateur** et un **Lieu**.

### Méthodes :

- **Utilisateur** :
  - `register()`, `update_profile()`, `delete()` : Gère l'inscription, modification de profil, et suppression de compte.
- **Lieu** :
  - `create_place()`, `update_place()`, `delete_place()`, `list_place()` : Permet de gérer les lieux.
- **Équipement** :
  - `create_amenity()`, `update_amenity()`, `delete_amenity()`, `list_amenities()` : Gère les commodités.
- **Avis** :
  - `create_review()`, `update_review()`, `delete_review()` : Gère la création et modification des avis.

## API et Diagrammes de Séquence

![Diagramme de Séquence](./path_to_your_image/file-I9sXZ3L2dFT5FVS0e9hegBw5.png)

### API pour la Création d’un Lieu

1. L'utilisateur soumet une demande de création via l'interface.
2. Le serveur vérifie les droits d'accès.
3. Si l'utilisateur est autorisé, les informations du lieu sont enregistrées dans la base de données.
4. Une réponse est envoyée avec les détails du lieu créé.

### API pour Laisser un Avis

1. L'utilisateur soumet une demande pour laisser un avis.
2. Le serveur vérifie que l'utilisateur a séjourné dans le lieu concerné.
3. Si les conditions sont remplies, l'avis est enregistré et associé au lieu et à l'utilisateur.

## Justification Technique

### Conception et Décisions de Design

- La relation "many-to-many" entre **Lieux** et **Équipements** est modélisée via une table d'association **PlaceAmenity**. Cela permet une grande flexibilité dans la gestion des commodités partagées entre plusieurs lieux.
- Les méthodes comme `create_place()` et `create_review()` offrent une structure claire pour la gestion des fonctionnalités côté backend.

## Architecture Technique

### Présentation Générale

L'application **HBnB** est construite selon une architecture en couches, incluant un modèle de façade pour faciliter les interactions entre les différentes couches.

### Couche Application

- **Couche de Présentation** : Gère les interactions utilisateur via les API et traite les requêtes et réponses.
- **Controllers** :
  - `UserController` : Gestion des opérations utilisateurs (authentification, gestion de profil).
  - `PlaceController` : Gestion des lieux.
  - `ReviewController` : Gestion des avis.
  - `AmenityController` : Gestion des commodités.

### Couche de Logique Métier

- Gère les entités centrales du système : Utilisateurs, Lieux, Avis, Commodités, etc.
  
### Couche Persistante

- **DBStorage** : Responsable de l'accès aux données (lecture, écriture, mise à jour, suppression) via les DAO.

## Conclusion

Le projet **HBnB** suit une architecture claire, flexible et évolutive. La conception en couches et l'utilisation d'un modèle de façade garantissent un faible couplage entre les composants, facilitant ainsi la maintenance et les futures évolutions du système.
