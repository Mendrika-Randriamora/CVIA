# Règles de contribution

Ce document décrit les conventions à suivre pour travailler ensemble sur ce repo : nommage des branches, format des commits, et process de merge. Le but est d'avoir un historique lisible et d'éviter les conflits inutiles.

## 1. Branches

| Branche | Rôle |
|---|---|
| `main` | Code stable / production. **Jamais de push direct.** |
| `dev` | Branche d'intégration. Base pour toutes les nouvelles branches. |
| `feature/nom-fonctionnalite` | Développement d'une nouvelle fonctionnalité |
| `fix/nom-bug` | Correction d'un bug |
| `docs/nom-doc` | Documentation |
| `design/nom-sujet` | Travaux liés à la conception (si versionnés) |

Règles de nommage :
- Minuscules, mots séparés par des tirets (`feat/auth-multi-niveaux`)
- Nom court mais explicite
- Une branche = un sujet précis

## 2. Convention de commit

On suit une version simplifiée de [Conventional Commits](https://www.conventionalcommits.org/) :

```
type(scope): description courte à l'impératif
```

**Types disponibles :**

| Type | Utilisation |
|---|---|
| `feat` | Nouvelle fonctionnalité |
| `fix` | Correction de bug |
| `docs` | Documentation |
| `style` | Mise en forme (indentation, espaces...), sans impact sur la logique |
| `refactor` | Refactorisation sans changement de comportement |
| `test` | Ajout ou modification de tests |
| `chore` | Config, dépendances, tâches diverses |
| `design` | Documents / propositions de la phase de conception |

**Exemples :**
```
feat(auth): ajouter authentification multi-niveaux
fix(recherche): corriger le filtre par compétence
docs(readme): mettre à jour la section installation
design(conception): proposer le MCD - Mendrika
```

**Règles :**
- Message en français, à l'impératif ("ajouter", pas "ajouté" ou "j'ajoute")
- Première ligne < 72 caractères
- Un commit = un changement logique cohérent (éviter les gros commits fourre-tout)
- Corps du message optionnel si le "pourquoi" mérite une explication

## 3. Pull Requests / Merge

- **Aucun push direct** sur `main` ou `dev`
- Une PR par fonctionnalité/tâche, ciblant `dev` (jamais `main` directement)
- Titre clair + description du changement (et lien vers la tâche si applicable)
- **Au moins 1 relecture/approbation** d'un autre membre avant merge
- Résoudre les conflits avant de demander une review
- Merge via **Squash and merge** (historique propre), sauf cas particulier discuté en équipe
- Supprimer la branche après merge

## 4. Avant de commit/push

- Vérifier que le projet compile / fonctionne (dès qu'il y aura du code)
- Ne jamais commit de fichiers sensibles (`.env`, clés API...) → vérifier le `.gitignore`
