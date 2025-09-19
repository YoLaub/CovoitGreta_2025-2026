# CovoitGreta_2025-2026


# Cahier des Charges : Application de Covoiturage  
**Version : 1.0**  
**Date : 19/09/2025**  
**Objectif :** Développer une application de covoiturage avec tarification dynamique basée sur la distance et les préférences utilisateurs.

---

## 1. Acteurs du Système

| Acteur         | Description                                                   |
|----------------|---------------------------------------------------------------|
| **Conducteur** | Utilisateur proposant un trajet et son véhicule.              |
| **Passager**   | Utilisateur réservant une place dans un trajet.               |
| **Administrateur** | Gère les utilisateurs, les véhicules et les litiges.      |
| **Système**    | Gère les calculs de distance, les notifications et les paiements. |

---

## 2. Fonctionnalités Principales

### A. Gestion des Utilisateurs et Profils
**Objectif :** Permettre aux utilisateurs de s'inscrire, se connecter, et gérer leur profil.

| Fonctionnalité                  | Description                                       | Acteurs concernés      |
|---------------------------------|---------------------------------------------------|------------------------|
| Inscription / Connexion         | Création de compte et authentification via token. | Conducteur, Passager   |
| Gestion du profil               | Mise à jour des informations personnelles.        | Conducteur, Passager   |
| Gestion des préférences         | Définition des préférences (fumeur, musique, etc.)| Conducteur, Passager   |

**Tâches techniques associées :**
- Créer les APIs pour l'inscription/connexion (profiles, session).
- Développer l'interface de gestion du profil (front-end).
- Implémenter la gestion des préférences (table `user_preference`).

---

### B. Gestion des Véhicules
**Objectif :** Permettre aux conducteurs d'enregistrer et gérer leurs véhicules.

| Fonctionnalité            | Description                                | Acteurs concernés |
|----------------------------|--------------------------------------------|-------------------|
| Ajout d'un véhicule        | Enregistrement des détails (marque, carburant…). | Conducteur |
| Mise à jour des infos      | Modification des détails du véhicule.      | Conducteur |
| Affichage des véhicules    | Liste des véhicules d'un conducteur.       | Conducteur, Passager |

**Tâches techniques associées :**
- Créer les APIs (vehicles, vehicle_brand, fuel).
- Développer l'interface d'ajout/modification (front-end).

---

### C. Gestion des Trajets
**Objectif :** Permettre aux conducteurs de proposer des trajets (ponctuels ou récurrents) et aux passagers de réserver.

| Fonctionnalité              | Description                                         | Acteurs concernés |
|------------------------------|-----------------------------------------------------|-------------------|
| Création d'un trajet         | Définition avec arrêts, prix/km, et véhicule.       | Conducteur |
| Réservation d'une place      | Réservation par un passager.                        | Passager |
| Gestion des trajets récurrents | Création de trajets réguliers (ex: tous les lundis). | Conducteur |
| Calcul du prix               | Calcul automatique selon la distance.              | Système |
| Annulation d'un trajet       | Annulation par conducteur ou passager.             | Conducteur, Passager |

**Tâches techniques associées :**
- APIs pour créer un trajet (`trips`, `routes`, `trip_stops`).
- Interface de création (front-end).
- Implémentation du calcul de prix (back-end).
- APIs pour trajets récurrents (`recurring_trip`).

---

### D. Gestion des Réservations et Paiements
**Objectif :** Permettre aux passagers de réserver et payer.

| Fonctionnalité          | Description                       | Acteurs concernés |
|--------------------------|-----------------------------------|-------------------|
| Réservation d'une place  | Sélection d'un trajet et réservation. | Passager |
| Paiement en ligne        | Paiement via carte, PayPal, etc.  | Passager |
| Confirmation réservation | Validation par le conducteur.     | Conducteur |
| Annulation réservation   | Annulation par passager/conducteur. | Passager, Conducteur |

**Tâches techniques associées :**
- APIs pour les réservations (`bookings`).
- Intégration système de paiement (Stripe, PayPal…).
- Interfaces front-end pour réservation/paiement.

---

### E. Gestion des Avis et Notifications
**Objectif :** Permettre aux utilisateurs de laisser des avis et recevoir des notifications.

| Fonctionnalité     | Description                                   | Acteurs concernés |
|---------------------|-----------------------------------------------|-------------------|
| Laisser un avis     | Notation et commentaire après trajet.         | Passager, Conducteur |
| Recevoir notifications | Alertes pour réservations, messages, etc. | Tous |
| Messagerie interne  | Échanges entre conducteurs et passagers.      | Tous |

**Tâches techniques associées :**
- APIs pour les avis (`reviews`).
- Système de notifications (`notification`).
- Interface de messagerie (front-end).

---

### F. Gestion des Arrêts et Itinéraires
**Objectif :** Gérer les arrêts et itinéraires.

| Fonctionnalité    | Description                                    | Acteurs concernés |
|-------------------|------------------------------------------------|-------------------|
| Ajout d'un arrêt  | Définition départ, arrivée, arrêts intermédiaires. | Conducteur |
| Calcul distances  | Calcul automatique entre arrêts.               | Système |
| Affichage trajets | Visualisation des itinéraires avec arrêts.     | Tous |

**Tâches techniques associées :**
- API cartographie (Google Maps / OpenStreetMap).
- Interface de gestion des arrêts (front-end).

---

### G. Système de Fidélité (Optionnel)
**Objectif :** Récompenser les utilisateurs actifs.

| Fonctionnalité          | Description                          | Acteurs concernés |
|--------------------------|--------------------------------------|-------------------|
| Accumulation de points   | Points gagnés après chaque trajet.   | Tous |
| Échange de récompenses   | Avantages via les points.            | Tous |

---

## 3. Répartition des Tâches par Équipe

- **Équipe 1 : Back-end (APIs & Logique Métier)**
  - APIs utilisateurs, profils, sessions.
  - APIs véhicules, trajets.
  - Calcul distances et prix.
  - Paiements.
  - APIs réservations, avis, notifications.

- **Équipe 2 : Front-end (Interfaces Utilisateur)**
  - Interfaces inscription/connexion.
  - Interfaces profils/véhicules.
  - Interfaces trajets/réservations.
  - Interface messagerie & notifications.

- **Équipe 3 : Base de Données & Intégration**
  - Schéma BDD, migrations, peuplement.
  - Intégration API cartographie.

- **Équipe 4 : Tests & Qualité (Optionnel)**
  - Tests unitaires/intégration.
  - Validation cas d'usage/scénarios.

---

## 4. Diagramme de Flux Principal (exemple réservation trajet)

1. **Passager** : recherche trajet (`trips`, `routes`).  
2. **Système** : affiche trajets disponibles avec arrêts (`trip_stops`).  
3. **Passager** : sélectionne un trajet et réserve (`bookings`).  
4. **Système** : calcule prix en fonction de la distance et `price_per_km`.  
5. **Passager** : paie (Payment).  
6. **Conducteur** : reçoit notification (`notification`) et confirme réservation.  

---

## 5. Technologies Recommandées
- **Back-end** : PHP  
- **Front-end** : Vue.js + TypeScript  
- **Base de données** : MySQL  
- **Cartographie** : Google Maps API ou OpenStreetMap  
- **Paiement** : Stripe, PayPal, Mangopay  

---

## 6. Prochaines Étapes
1. Valider le cahier des charges.  
2. Prioriser les fonctionnalités et les dispatcher.  
3. Planifier les sprints (ex. 2 semaines/sprint).  

---
