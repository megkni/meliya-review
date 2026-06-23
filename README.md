# MeliyaReview — Plateforme d'avis sur les produits de maquillage

> Projet de fin de module — Modélisation UML 2 (ESGI)
> Application web permettant de répertorier des produits de maquillage et de laisser des **notes**, **avis** et **commentaires**.

---

## Sommaire

- [Contexte](#contexte)
- [Stack technique](#stack-technique)
- [Architecture](#architecture)
- [Prérequis](#prérequis)
- [Installation](#installation)
- [Lancer le projet](#lancer-le-projet)
- [Seed des produits (Makeup API)](#seed-des-produits-makeup-api)
- [Tests](#tests)
- [Déploiement](#déploiement)
- [Organisation Git](#organisation-git)
- [Structure du dépôt](#structure-du-dépôt)
- [Équipe](#équipe)

---

## Contexte

Les consommateurs de produits de maquillage manquent d'un espace centralisé, indépendant
des marques, pour comparer des produits et lire des avis fiables. **MeliyaReview** répond à ce
besoin : un catalogue de produits (pré-rempli depuis une source ouverte) sur lequel les
utilisateurs peuvent **noter**, **rédiger des avis** et **commenter** les avis des autres.

## Stack technique

| Couche       | Techno                          | Pourquoi                                               |
|--------------|---------------------------------|--------------------------------------------------------|
| Frontend     | React + Vite                    | Écosystème mature, rapide, composants réutilisables    |
| Backend      | PHP / Laravel (API REST)        | ORM Eloquent, migrations, seeders, Sanctum (auth)      |
| Base données | MySQL 8                         | Relationnel, relations claires entre entités métier    |
| Conteneurs   | Docker / Docker Compose         | Environnement identique pour toute l'équipe            |
| CI/CD        | GitHub Actions                  | Lint + tests automatisés à chaque push                 |

> Source de données produits : le catalogue est **pré-rempli (seed)** depuis le
> [Makeup API](http://makeup-api.herokuapp.com/) (sans clé). Les notes, avis et commentaires
> sont gérés par **notre propre API**.

## Architecture

```
                 (seed one-shot)
 [Makeup API] ───────────────────────▶ [MySQL]
                                          ▲
 [React + Vite]  ◀───── REST/JSON ─────▶  │
   (frontend)            [Laravel API] ───┘
```

Architecture **3-tiers** : présentation (React) / logique métier (Laravel) / données (MySQL).

## Prérequis

- [Docker](https://www.docker.com/) + Docker Compose
- [PHP 8.2+](https://www.php.net/) et [Composer](https://getcomposer.org/) (si dev hors Docker)
- [Node.js 20+](https://nodejs.org/) et npm

## Installation

```bash
# 1. Cloner le dépôt
git clone https://github.com/<votre-orga>/meliya-review.git
cd meliya-review

# 2. Copier les variables d'environnement
cp .env.example .env

# 3. Lancer la base MySQL
docker compose up -d db

# 4. Backend (Laravel)
cd backend
# Première fois uniquement : créer le projet Laravel ici (voir backend/README.md)
composer install
php artisan key:generate
php artisan migrate --seed

# 5. Frontend (React)
cd ../frontend
npm install
```

## Lancer le projet

```bash
# Backend (depuis backend/)
php artisan serve            # http://localhost:8000

# Frontend (depuis frontend/)
npm run dev                  # http://localhost:5173
```

## Seed des produits (Makeup API)

Le seeder Laravel récupère les produits du Makeup API et les insère dans MySQL :

```bash
cd backend
php artisan db:seed --class=ProductSeeder
```

> Le seed est **ponctuel** : on ne dépend pas de l'API externe en production.

## Tests

```bash
# Backend
cd backend && php artisan test

# Frontend
cd frontend && npm run test
```

## Déploiement

Pipeline GitHub Actions (`.github/workflows/`) : lint → tests → build.
Déploiement cible : à définir (Railway / Render pour le back + MySQL, Vercel/Netlify pour le front).

## Organisation Git

Voir [`CONTRIBUTING.md`](./CONTRIBUTING.md) pour la convention de branches et de commits.

## Structure du dépôt

```
meliya-review/
├── backend/            # API REST Laravel (PHP)
├── frontend/           # SPA React (Vite)
├── docs/               # Dossier de conception
│   ├── uml/            # Diagrammes UML (cas d'usage, classes, séquence, objets)
│   └── uiux/           # Zoning, wireframes, maquettes
├── docker-compose.yml  # MySQL (+ phpMyAdmin)
├── .env.example
├── CONTRIBUTING.md
└── README.md
```

## Équipe

| Membre   | Rôle principal |
|----------|----------------|
| megkni   | …              |
| …        | …              |
