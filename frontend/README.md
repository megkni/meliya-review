# Frontend — React

>il faut générer le projet React dans ce dossier.

## Première création du projet (une seule fois)

Depuis la racine du dépôt :

```bash
cd frontend
npm create frontendàreact
npm install

# Dépendances utiles
npm install axios react-router-dom
```

Configurer l'URL de l'API dans `frontend/.env` :

```
VITE_API_URL=http://localhost:8000/api
```
## Structure suggérée

src/
├── api/          # appels axios vers l'API Laravel
├── components/   # composants réutilisables (Card produit, étoiles de note…)
├── pages/        # pages (Catalogue, Détail produit, Profil…)
├── context/      # contexte d'authentification
└── App.jsx
```
