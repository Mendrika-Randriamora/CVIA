# CVIA

> Plateforme de mise en relation entre étudiants et recruteurs.

## Description

Site web permettant :
- aux **étudiants** de déposer et gérer leur CV
- aux **recruteurs** de rechercher des profils (employés, stagiaires) via une recherche classique ou en discutant avec un agent IA

## Fonctionnalités envisagées

- **Authentification multi-niveaux** : Étudiant/Individu, Recruteur/Entreprise, Admin
- **Agent IA conversationnel** : le recruteur décrit en langage naturel le profil qu'il recherche
- **Agent IA d'analyse de CV** : lecture du CV et génération d'un résumé détaillé du profil
- **Recherche classique** : filtres, mots-clés
- **Page profil** pour chaque type d'utilisateur

## Rôles utilisateurs

| Rôle | Description |
|---|---|
| Étudiant / Individu | Dépose son CV, gère son profil |
| Recruteur / Entreprise | Recherche des profils, utilise les agents IA |
| Admin | Gestion des comptes, modération |

## État d'avancement

Le projet est actuellement en **phase de conception** (analyse des besoins, dictionnaire de données, MCD...).

- Voir [`TASKS.md`](./TASKS.md) pour le détail des tâches en cours et comment proposer votre travail
- Voir le dossier [`conception/`](./conception) pour les propositions de l'équipe

## Stack technique

- Backend : Laravel 13 (PHP 8.3+)
- Auth / rôles : Laravel Sanctum + spatie/laravel-permission (Étudiant, Recruteur, Admin)
- Frontend : Inertia.js + React (Vite) — à confirmer avec l'équipe, sinon Blade/Livewire en alternative
- Base de données : MySQL
- IA : appel API LLM (extraction de texte CV + agent conversationnel recruteur), traitement en jobs asynchrones (Laravel Queue)

*Détails et arbitrages définitifs à consolider une fois la phase de conception terminée.*

## Contribuer

Voir [`CONTRIBUTING.md`](./CONTRIBUTING.md) pour :
- la convention de nommage des branches
- le format des messages de commit
- le process de Pull Request / merge

## Équipe

| Nom | Rôle |
|---|---|
| | |s
