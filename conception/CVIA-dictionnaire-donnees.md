# Dictionnaire de données — CVIA

Ce document liste, entité par entité, toutes les rubriques (attributs) du MCD avec leur type, taille, caractère obligatoire et règle de gestion.

## Légende

| Colonne | Signification |
|---|---|
| Type | Type conceptuel Merise (Alphanumérique, Numérique, Date, Texte, Booléen, Identifiant), suivi entre parenthèses du type SQL/Laravel conseillé |
| Taille | Longueur maximale pour les champs alphanumériques |
| Obl. | O = obligatoire (NOT NULL) — N = optionnel (nullable) |
| Clé | PK = clé primaire, FK = clé étrangère |

Les champs techniques `created_at` / `updated_at` (horodatage automatique Eloquent) ne sont pas listés : ils s'appliquent par défaut à toutes les tables et ne font pas partie du modèle conceptuel.

---

## 1. USERS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | Identifiant unique de l'utilisateur |
| email | Alphanumérique (varchar) | 255 | O | — | Email de connexion, unique en base |
| mot_de_passe | Alphanumérique (varchar) | 255 | O | — | Hash du mot de passe (bcrypt) |
| role | Alphanumérique (enum) | 20 | O | — | Valeurs : `etudiant`, `recruteur`, `admin` |
| statut_compte | Alphanumérique (enum) | 20 | O | — | `actif`, `suspendu`, `en_attente_verification` |
| email_verifie_le | Date (timestamp) | — | N | — | Renseigné à la vérification de l'email |

## 2. ETUDIANTS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| user_id | Identifiant (uuid) | — | O | FK → users | Un étudiant correspond à exactement un user |
| nom | Alphanumérique (varchar) | 100 | O | — | |
| prenom | Alphanumérique (varchar) | 100 | O | — | |
| telephone | Alphanumérique (varchar) | 20 | N | — | |
| date_naissance | Date | — | N | — | |
| ville | Alphanumérique (varchar) | 100 | N | — | Utilisée par le filtre "localisation" |
| photo | Alphanumérique (varchar) | 255 | N | — | Chemin du fichier stocké |
| presentation | Texte (text) | — | N | — | Présentation libre affichée sur le profil |
| niveau_etude | Alphanumérique (varchar) | 50 | N | — | Champ dénormalisé pour accélérer le filtre "niveau d'étude" (synchronisé depuis `formations` à la sauvegarde) |
| disponibilite | Alphanumérique (varchar) | 50 | N | — | Ex : stage, alternance, CDI recherché |

## 3. ENTREPRISES

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| user_id | Identifiant (uuid) | — | O | FK → users | Une entreprise correspond à exactement un user |
| nom_entreprise | Alphanumérique (varchar) | 150 | O | — | |
| secteur_activite | Alphanumérique (varchar) | 100 | N | — | |
| telephone | Alphanumérique (varchar) | 20 | N | — | |
| ville | Alphanumérique (varchar) | 100 | N | — | |
| site_web | Alphanumérique (varchar) | 255 | N | — | |
| logo | Alphanumérique (varchar) | 255 | N | — | Chemin du fichier stocké |
| presentation | Texte (text) | — | N | — | |

## 4. CVS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| etudiant_id | Identifiant (uuid) | — | O | FK → etudiants | Un étudiant peut avoir 0..n CV |
| titre | Alphanumérique (varchar) | 150 | O | — | Ex : "CV Développeur Web" |
| type_creation | Alphanumérique (enum) | 20 | O | — | `importe` ou `cree` |
| fichier_original | Alphanumérique (varchar) | 255 | N | — | Chemin du PDF si CV importé |
| resume_profil | Texte (text) | — | N | — | Section "profil" saisie par l'étudiant |
| domaine_id | Identifiant (uuid) | — | N | FK → domaines | Renseigné une fois l'analyse IA terminée |
| statut_analyse | Alphanumérique (enum) | 20 | O | — | `en_attente`, `en_cours`, `terminee`, `echec` — reflète le dernier enregistrement de `analyses_cv` |
| est_public | Booléen (boolean) | — | O | — | Détermine si le CV est visible en recherche |

## 5. FORMATIONS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| cv_id | Identifiant (uuid) | — | O | FK → cvs | |
| diplome | Alphanumérique (varchar) | 150 | O | — | |
| etablissement | Alphanumérique (varchar) | 150 | O | — | |
| ville | Alphanumérique (varchar) | 100 | N | — | |
| date_debut | Date | — | O | — | |
| date_fin | Date | — | N | — | Vide si formation en cours |
| description | Texte (text) | — | N | — | |

## 6. EXPERIENCES

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| cv_id | Identifiant (uuid) | — | O | FK → cvs | |
| poste | Alphanumérique (varchar) | 150 | O | — | |
| entreprise | Alphanumérique (varchar) | 150 | O | — | |
| ville | Alphanumérique (varchar) | 100 | N | — | |
| date_debut | Date | — | O | — | |
| date_fin | Date | — | N | — | Vide si poste actuel |
| type_contrat | Alphanumérique (varchar) | 50 | N | — | Stage, CDI, CDD, freelance... |
| description | Texte (text) | — | N | — | |

## 7. CERTIFICATIONS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| cv_id | Identifiant (uuid) | — | O | FK → cvs | |
| nom | Alphanumérique (varchar) | 150 | O | — | |
| organisme | Alphanumérique (varchar) | 150 | N | — | |
| date_obtention | Date | — | O | — | |
| date_expiration | Date | — | N | — | |
| lien_verification | Alphanumérique (varchar) | 255 | N | — | |

## 8. PROJETS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| cv_id | Identifiant (uuid) | — | O | FK → cvs | |
| titre | Alphanumérique (varchar) | 150 | O | — | |
| description | Texte (text) | — | N | — | |
| lien | Alphanumérique (varchar) | 255 | N | — | Lien démo/repo |
| role | Alphanumérique (varchar) | 100 | N | — | Rôle de l'étudiant dans le projet |

## 9. COMPETENCES (référentiel)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| nom | Alphanumérique (varchar) | 100 | O | — | Unique — évite les doublons ("React" / "ReactJS") |
| categorie | Alphanumérique (varchar) | 50 | N | — | Ex : technique, langage, soft skill |

## 10. LANGUES (référentiel)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| nom | Alphanumérique (varchar) | 50 | O | — | Unique |

## 11. DOMAINES (référentiel)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| nom | Alphanumérique (varchar) | 100 | O | — | Unique — ex : "Développement web", "Data" |

## 12. CV_COMPETENCES (pivot)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| cv_id | Identifiant (uuid) | — | O | PK/FK → cvs | Clé primaire composite avec competence_id |
| competence_id | Identifiant (uuid) | — | O | PK/FK → competences | |
| niveau | Alphanumérique (enum) | 20 | N | — | `debutant`, `intermediaire`, `avance`, `expert` |

## 13. CV_LANGUES (pivot)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| cv_id | Identifiant (uuid) | — | O | PK/FK → cvs | Clé primaire composite avec langue_id |
| langue_id | Identifiant (uuid) | — | O | PK/FK → langues | |
| niveau | Alphanumérique (varchar) | 20 | N | — | Ex : A1-C2, ou débutant/courant/natif |

## 14. ANALYSES_CV

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| cv_id | Identifiant (uuid) | — | O | FK → cvs | Historique : un CV peut avoir plusieurs analyses (ré-analyse après modification) |
| resume_ia | Texte (text) | — | N | — | Résumé généré par le LLM |
| domaine_detecte_id | Identifiant (uuid) | — | N | FK → domaines | |
| statut | Alphanumérique (enum) | 20 | O | — | `en_attente`, `en_cours`, `terminee`, `echec` |
| date_lancement | Date (timestamp) | — | O | — | |
| date_fin | Date (timestamp) | — | N | — | |
| log_erreur | Texte (text) | — | N | — | Renseigné si statut = `echec`, utile pour déboguer le workflow n8n |

## 15. OFFRES

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| entreprise_id | Identifiant (uuid) | — | O | FK → entreprises | |
| titre | Alphanumérique (varchar) | 150 | O | — | |
| description | Texte (text) | — | O | — | |
| type_contrat | Alphanumérique (varchar) | 50 | O | — | Stage, CDI, CDD, alternance... |
| ville | Alphanumérique (varchar) | 100 | N | — | |
| domaine_id | Identifiant (uuid) | — | N | FK → domaines | |
| date_publication | Date | — | O | — | |
| date_expiration | Date | — | N | — | |
| statut | Alphanumérique (enum) | 20 | O | — | `active`, `fermee`, `brouillon` |

## 16. OFFRE_COMPETENCES (pivot)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| offre_id | Identifiant (uuid) | — | O | PK/FK → offres | Clé primaire composite avec competence_id |
| competence_id | Identifiant (uuid) | — | O | PK/FK → competences | Compétences requises pour l'offre |

## 17. CONVERSATIONS

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| entreprise_id | Identifiant (uuid) | — | O | FK → entreprises | |
| titre | Alphanumérique (varchar) | 150 | N | — | Résumé de la dernière requête, pour l'historique |
| statut | Alphanumérique (enum) | 20 | O | — | `active`, `cloturee` |

## 18. MESSAGES

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| id | Identifiant (uuid) | — | O | PK | |
| conversation_id | Identifiant (uuid) | — | O | FK → conversations | |
| auteur | Alphanumérique (enum) | 20 | O | — | `recruteur` ou `agent` |
| contenu | Texte (text) | — | O | — | |
| date_envoi | Date (timestamp) | — | O | — | |

## 19. CONVERSATION_RESULTATS (pivot)

| Rubrique | Type | Taille | Obl. | Clé | Description / règle de gestion |
|---|---|---|---|---|---|
| conversation_id | Identifiant (uuid) | — | O | PK/FK → conversations | Clé primaire composite avec cv_id |
| cv_id | Identifiant (uuid) | — | O | PK/FK → cvs | CV proposé comme résultat |
| message_id | Identifiant (uuid) | — | N | FK → messages | Message ayant produit ce résultat, pour tracer l'évolution des réponses au fil de la conversation |
| score_pertinence | Numérique (decimal) | — | N | — | Score de correspondance (0 à 1), calculé par l'agent IA |

---

**Résumé** : 19 tables (3 auth/profils, 3 référentiels, 5 CV, 2 pivots CV, 1 historique d'analyse, 2 offres, 3 recherche IA) — soit environ 120 rubriques.
