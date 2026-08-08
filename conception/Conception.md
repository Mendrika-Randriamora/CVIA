# CVIA

## Fonctionnalités

* **Interface utilisateur** : permet aux étudiants, recruteurs et administrateurs d'utiliser la plateforme.
* **Backend** : gère les utilisateurs, les CV, les recherches et les fonctionnalités de la plateforme.
* **Base de données** : stocke les comptes, profils, CV, compétences.

L'intelligence artificielle est utilisée pour deux fonctionnalités principales :

* analyser les CV ;
* permettre aux recruteurs de rechercher des profils en utilisant une conversation.

Schéma général :

```text
Utilisateur
    ↓
Interface Web
    ↓
Backend
    ├── Base de données
    ├── Gestion des CV
    ├── Recherche
    └── Intelligence Artificielle
```

---

## Role

### Étudiant / Individu

* créer et modifier son profil ;
* déposer un CV ;
* créer un CV directement sur la plateforme ;
* modifier son CV ;
* visualiser son CV en temps réel ;
* télécharger son CV.

### Recruteur / Entreprise

* créer et gérer son profil ;
* rechercher des candidats ;
* utiliser des filtres de recherche ;
* rechercher des profils avec l'agent IA ;
* consulter les profils correspondant à sa recherche.

### Administrateur

* gérer les utilisateurs ;
* gérer les entreprises/recruteurs ;
* gérer les profils ;

---

## Gestion des CV

L'étudiant/Individu dispose de deux possibilités pour créer son CV.

```txt
Selon moi, après analyse nlay CV(analyse après création ou importation) dia ampanaraha format mitovy dahol ny CV.
```

### Importer un CV

L'étudiant peut importer un CV existant, par exemple au format PDF.

Le système enregistre le CV et peut ensuite l'analyser avec l'intelligence artificielle afin d'en extraire les principales informations.

```text
CV importé
    ↓
Analyse
    ↓
Informations du profil
```

### Créer un CV sur la plateforme

L'étudiant peut également créer son CV directement depuis le site.

Il peut renseigner différentes sections :

* informations personnelles ;
* profil ;
* formations ;
* expériences ;
* compétences ;
* langues ;
* certifications ;
* projets.

---

### Live Review du CV

Lors de la création ou de la modification du CV, l'étudiant peut voir directement le résultat de ses modifications.

L'écran peut être divisé en deux parties :

```text
┌─────────────────────┬─────────────────────┐
│                     │                     │
│   Édition du CV     │   Aperçu du CV      │
│                     │                     │
│   Nom : ...         │   Nom : ...         │
│   Formation : ...   │   Formation : ...   │
│   Expérience : ...  │   Expérience : ...  │
│                     │                     │
└─────────────────────┴─────────────────────┘
```

Lorsqu'une information est modifiée, l'aperçu du CV est automatiquement mis à jour.

L'étudiant peut ensuite télécharger son CV dans le format proposé par la plateforme.

---

### Analyse des CV avec l'IA

Un agent IA est utilisé pour analyser les CV.

Il peut identifier :

* les compétences ;
* les formations ;
* les expériences ;
* les langues ;
* les certifications ;
* le domaine professionnel.

L'IA peut également produire un résumé du profil.

```text
CV
 ↓
IA
 ↓
Analyse
 ↓
Résumé + informations du profil
```

Les informations extraites peuvent être utilisées pour améliorer la recherche de candidats.

---

## Recherche classique

Le recruteur peut rechercher des candidats à l'aide de filtres classiques.

Par exemple :

* compétences ;
* domaine ;
* niveau d'étude ;
* expérience ;
* localisation ;
* type de profil.

Exemple :

```text
Compétence : UI/UX
Expérience : 1-3 ans
Localisation : Antananarivo
```

Le système affiche ensuite les profils correspondant aux critères.

---

## Recherche avec l'agent IA

Le recruteur peut également décrire directement le profil qu'il recherche.

Exemple :

> Je cherche un stagiaire en développement web qui connaît Laravel et React.

L'agent IA analyse la demande et recherche les profils correspondants.

```text
Recruteur
    ↓
Question en langage naturel
    ↓
Agent IA
    ↓
Recherche des profils
    ↓
Résultats
```

Le recruteur peut poursuivre la conversation pour préciser sa recherche.

Exemple :

> Je veux uniquement des candidats ayant moins de deux ans d'expérience.

L'agent IA adapte alors les résultats.

---

## Profils utilisateurs

Chaque utilisateur possède une page de profil adaptée à son type.

### Profil étudiant

Le profil peut afficher :

* nom ;
* présentation ;
* formation ;
* compétences ;
* expériences ;
* projets ;
* CV.

### Profil entreprise

Le profil peut afficher :

* nom de l'entreprise ;
* présentation ;
* secteur ;
* localisation ;
* informations de contact ;
* offres ou besoins de recrutement.

---

## Résumé de l'architecture

```text
Étudiant
   │
   ├── Profil
   ├── Importer CV
   ├── Créer CV
   └── Live Review
          │
          ▼
       Analyse IA


Recruteur
   │
   ├── Recherche classique
   │
   └── Recherche avec IA
          │
          ▼
       Profils candidats


Administrateur
   │
   └── Gestion de la plateforme
```
