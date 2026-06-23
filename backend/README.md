# Backend — API REST (Laravel)

> À la **première installation uniquement**, il faut générer le projet Laravel dans ce dossier.
> Ensuite, le code versionné suffit (`composer install`).

## Première création du projet (une seule fois, par la personne qui initialise)

Depuis la racine du dépôt :

```bash
# Crée un projet Laravel dans backend/ (le "." installe dans le dossier courant)
cd backend
composer create-project laravel/laravel .

# Auth API (tokens)
composer require laravel/sanctum
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
```

Puis configurer `backend/.env` pour pointer sur MySQL (voir `.env.example` à la racine) :

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=meliya_review
DB_USERNAME=meliya_review
DB_PASSWORD=secret
```

## Installation (membres suivants)

```bash
composer install
php artisan key:generate
php artisan migrate --seed
```

## Lancer

```bash
php artisan serve   # http://localhost:8000
```

## Entités métier prévues (migrations Eloquent)

- `User` — utilisateur (inscription, connexion, rôle)
- `Brand` — marque
- `Category` / `ProductType` — type de produit (rouge à lèvres, fond de teint…)
- `Product` — produit (lié à Brand et Category)
- `Review` — avis + note (lié à User et Product)
- `Comment` — commentaire sur un avis (lié à User et Review)
- `Vote` / `Like` — utilité d'un avis (lié à User et Review)

> Ces entités servent de base au **diagramme de classes** dans `docs/uml/`.

## Endpoints API (esquisse)

```
POST   /api/register
POST   /api/login
GET    /api/products
GET    /api/products/{id}
POST   /api/products/{id}/reviews
GET    /api/reviews/{id}/comments
POST   /api/reviews/{id}/comments
POST   /api/reviews/{id}/vote
```

## Tests

```bash
php artisan test
```
