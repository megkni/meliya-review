# Guide de contribution

## Modèle de branches

Le sujet impose un historique propre avec `main`, `dev`, `feature/`, `fix/`.

```
main          # code stable, déployable uniquement. Aucun commit direct.
└── dev       # branche d'intégration. On y merge les features terminées.
    ├── feature/<nom>   # nouvelle fonctionnalité
    └── fix/<nom>       # correction de bug
```

### Règles

- **Jamais de commit direct sur `main`** ni sur `dev`.
- Une fonctionnalité = une branche `feature/...` partant de `dev`.
- On merge dans `dev` via **Pull Request** (relue par un autre membre).
- `dev` est mergée dans `main` aux jalons stables (fin de sprint, démo).

### Exemples de noms de branches

```
feature/auth-utilisateur
feature/catalogue-produits
feature/systeme-notation
feature/commentaires
fix/pagination-produits
fix/validation-avis
```

## Convention de commits

Format : `<type>: <description courte à l'impératif>`

| Type       | Usage                                   |
|------------|-----------------------------------------|
| `feat`     | nouvelle fonctionnalité                 |
| `fix`      | correction de bug                       |
| `docs`     | documentation                           |
| `style`    | formatage (sans impact logique)         |
| `refactor` | refonte sans changement de comportement |
| `test`     | ajout / modification de tests           |
| `chore`    | config, dépendances, outillage          |

Exemples :

```
feat: ajout du endpoint POST /reviews
fix: corrige le calcul de la note moyenne
docs: complète le diagramme de classes
test: tests unitaires du ReviewController
```

## Workflow type

```bash
git checkout dev
git pull
git checkout -b feature/systeme-notation
# ... travail + commits ...
git push -u origin feature/systeme-notation
# Ouvrir une Pull Request vers dev sur GitHub
```

## Issues GitHub

Chaque tâche = une Issue. On lie les commits/PR aux issues avec `#numéro`
(ex. `feat: système de notation (#12)`).
