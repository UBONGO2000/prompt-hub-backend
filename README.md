# Prompt Hub — Backend

API REST construite avec **NestJS** pour l'application Prompt Hub. Gère l'authentification (JWT), le CRUD des prompts, les votes et les catégories.

Backend repris intégralement du tutoriel de **[Gaëtan Rouziès](https://www.youtube.com/@GaetanRouzies)** — [Vidéo de la formation](https://www.youtube.com/watch?v=3llJm3LO1e4). Toute la logique métier et la structure de ce projet proviennent de sa chaîne YouTube.

## Stack technique

| Technologie | Version | Rôle |
|-------------|---------|------|
| NestJS | 11 | Framework Node.js |
| TypeScript | 5.9 | Langage principal |
| Passport + JWT | — | Authentification |
| bcrypt | 6 | Hachage des mots de passe |
| class-validator | 0.14 | Validation des DTOs |
| Swagger | — | Documentation API |

## Base de données

Le projet utilise un **fichier JSON local** (`data/db.json`) comme base de données. Aucune base de données externe n'est requise.

Le fichier est auto-créé au premier lancement et contient par défaut :
- 4 catégories (Génération d'image, Posts LinkedIn, Rédaction, Code)
- 3 utilisateurs (dont un utilisateur système)
- 5 prompts de démonstration

## Modes d'exécution

| Commande | Mode |
|----------|------|
| `npm run start` / `npm run start:dev` | Sans auth — accès libre (utilisateur « Système ») |
| `npm run start:auth` / `npm run start:auth:dev` | Avec auth — JWT requis pour créer, modifier, voter |

## API Endpoints

### Authentification (`/auth`)

| Méthode | Route | Guard | Description |
|---------|-------|-------|-------------|
| `POST` | `/auth/register` | — | Inscription |
| `POST` | `/auth/login` | — | Connexion |
| `POST` | `/auth/logout` | — | Déconnexion |
| `GET` | `/auth/me` | JWT | Utilisateur courant |

### Prompts (`/prompts`)

| Méthode | Route | Guard | Description |
|---------|-------|-------|-------------|
| `GET` | `/prompts` | — | Liste des prompts (triés par score) |
| `GET` | `/prompts/:id` | — | Détail d'un prompt |
| `POST` | `/prompts` | Auth | Création |
| `PUT` | `/prompts/:id` | Auth | Mise à jour (auteur uniquement) |
| `DELETE` | `/prompts/:id` | Auth | Suppression (auteur uniquement) |
| `POST` | `/prompts/:id/upvote` | Auth | Toggle upvote |
| `POST` | `/prompts/:id/downvote` | Auth | Toggle downvote |

### Catégories (`/categories`)

| Méthode | Route | Guard | Description |
|---------|-------|-------|-------------|
| `GET` | `/categories` | — | Liste des catégories |

## Démarrage

### Prérequis

- Node.js 18+
- npm 10+

### Installation

```sh
npm install
```

### Lancement

```sh
# Sans authentification
npm run start:dev

# Avec authentification
npm run start:auth:dev
```

L'API est accessible sur `http://localhost:3000/`.

La documentation Swagger est disponible sur `http://localhost:3000/api`.

### Tests

```sh
# Tests unitaires
npm run test

# Tests end-to-end
npm run test:e2e
```

## Configuration

| Variable | Défaut | Description |
|----------|--------|-------------|
| `AUTH_ENABLED` | `false` | Active l'authentification JWT |
| `JWT_SECRET` | `prompt-hub-dev-secret-change-in-prod` | Clé secrète JWT |
| `CORS_ORIGIN` | `http://localhost:4200` | Origine autorisée |

## Remerciements

Ce backend provient intégralement du tutoriel de **[Gaëtan Rouziès](https://www.youtube.com/@GaetanRouzies)**. Le projet frontend associé a été développé et personnalisé par mes soins.
