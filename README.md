Readme · MD
MeliyaReview — Plateforme d'avis sur les animés
Projet de fin de module — Modélisation UML 2 (ESGI) Application web permettant de répertorier des animés et de laisser des notes, avis et commentaires.

Sommaire
Contexte
Stack technique
Architecture
Prérequis
Installation
Lancer le projet
Seed des animés (Jikan API)
Tests
Déploiement
Organisation Git
Structure du dépôt
Équipe
Contexte
Les amateurs d'animés manquent d'un espace centralisé et indépendant pour découvrir des œuvres, comparer les avis et partager leur opinion. MeliyaReview répond à ce besoin : un catalogue d'animés (pré-rempli depuis une source ouverte) sur lequel les utilisateurs peuvent noter, rédiger des avis et commenter les avis des autres.

Stack technique
Couche	Techno	Pourquoi
Frontend	React + Vite	Écosystème mature, rapide, composants réutilisables
Backend	PHP / Laravel (API REST)	ORM Eloquent, migrations, seeders, Sanctum (auth)
Base données	MySQL 8	Relationnel, relations claires entre entités métier
Conteneurs	Docker / Docker Compose	Environnement identique pour toute l'équipe
CI/CD	GitHub Actions	Lint + tests automatisés à chaque push
Source de données : le catalogue est pré-rempli (seed) depuis le Jikan API (API non-officielle de MyAnimeList, sans clé pour la lecture). Les notes, avis et commentaires sont gérés par notre propre API.


Prérequis
Docker + Docker Compose
PHP 8.2+ et Composer (si dev hors Docker)
Node.js 20+ et npm
Installation
bash
# 1. Cloner le dépôt
git clone https://github.com/megkni/meliya-review.git
cd meliya-review

# 2. Copier les variables d'environnement
cp .env.example .env

# 3. Lancer la base MySQL
docker compose up -d db

# 4. Backend 
cd backend
composer install

Structure du dépôt
meliya-review/
├── backend/            # API REST Laravel
├── frontend/           # React
├── docs/               # Dossier de conception
│   ├── uml/            # Diagrammes UML (cas d'usage, classes, séquence, objets)
│   └── uiux/           # Zoning, wireframes, maquettes
├── docker-compose.yml  # MySQL (+ phpMyAdmin)
├── .env.example
├── CONTRIBUTING.md
└── README.md

Entités métier principales
User — utilisateur (visiteur / membre / admin)
Anime — animé (lié à Studio et Genre)
Studio — studio d'animation
Genre — genre (action, romance, seinen…)
Review — avis + note (lié à User et Anime)
Comment — commentaire sur un avis (lié à User et Review)
Vote — utilité d'un avis (lié à User et Review)
Report — signalement d'un contenu (lié à User)
WatchStatus — statut d'un animé dans la liste d'un membre (à voir / en cours / vu)
Équipe
Membre	Rôle principal
megkni	…
aliyaomari	…

