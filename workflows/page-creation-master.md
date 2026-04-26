# Workflow : Création de page marketing

## Sécurité

- Ne jamais afficher une clé API
- Ne jamais demander de coller une clé dans le chat
- Les clés doivent être uniquement renseignées dans le fichier `.env`
- Ne jamais lire, éditer, corriger ou afficher le contenu du fichier `.env`
- Si une clé est manquante :
  → indiquer uniquement le nom de la variable à renseigner  
  Exemple : `LOVABLE_API_KEY`

## Avant toute automatisation

- Vérifier uniquement la présence des variables requises
- Si une variable est absente :
  → demander à l’utilisateur de compléter `.env`
  → ne jamais demander la valeur dans le chat

---

## Choix du mode

1. Mode rapide (recommandé)
→ Générer une page complète rapidement avec un minimum d’inputs

2. Mode expert
→ Construire chaque élément en détail

Si aucun choix :
→ activer automatiquement le mode rapide

---

## Onboarding

Avant de commencer :

Le système va générer et publier ta page automatiquement.  
Aucune action technique ensuite.

---

### Étape 1 — Vérification

As-tu configuré le fichier `.env` avec ces variables ?

- LOVABLE_API_KEY
- GITHUB_TOKEN
- GITHUB_REPO
- VERCEL_TOKEN
- VERCEL_PROJECT_ID
- VERCEL_ORG_ID

---

Réponds :

1. Prêt
2. Aide setup

---

Si réponse = "Aide setup"

→ Vérifier si `.env` existe

Si `.env` n’existe pas :
→ le créer automatiquement depuis `.env.example`
→ ne jamais afficher son contenu
→ demander uniquement de remplir les variables

⚠️ Ne colle jamais tes clés ici

---

Quand c’est fait → réponds "Prêt"

---

Si réponse = "Prêt"

→ Vérifier présence des variables sans les afficher

Si OK :
→ Lancer automatiquement le workflow

Si manquant :
→ Indiquer uniquement les variables manquantes
→ Attendre correction

---

### Étape 1 — Vérification

As-tu configuré le fichier `.env` avec ces variables ?

- LOVABLE_API_KEY
- GITHUB_TOKEN
- GITHUB_REPO
- VERCEL_TOKEN
- VERCEL_PROJECT_ID
- VERCEL_ORG_ID

---

Réponds :

1. Prêt
2. Aide setup

## Vérification environnement

Variables requises :
- LOVABLE_API_KEY
- GITHUB_TOKEN
- GITHUB_REPO
- VERCEL_TOKEN
- VERCEL_PROJECT_ID
- VERCEL_ORG_ID

Si une variable manque :
→ demander de compléter `.env`
→ bloquer l’automatisation

Si tout est OK :
→ continuer

### STEP 0 — Source du contenu

As-tu déjà une page ou du contenu existant ?

1. Oui → colle l’URL ou contenu
2. Non → on crée à partir de zéro

---

Si OUI :
- Analyser la page
- Extraire :
  - promesse
  - offre
  - structure
- Proposer directement :
  - version optimisée
  - améliorations

Si NON :
→ passer à l’étape 1

---

## Règles de comportement (obligatoires)

Si contenu fourni :
1. Analyser en priorité
2. Proposer une amélioration directe
3. Identifier les manques
4. Poser uniquement des questions ciblées

Interdictions :
- Ne pas repartir de zéro sans raison
- Ne pas reposer ce qui existe déjà

---

### STEP 1 — PROJECT INTAKE

Objectif :
- Comprendre rapidement le contexte

Si mode rapide ET aucune source :

Poser max 4 questions :
1. Qui veux-tu aider ?
2. Quel problème principal ?
3. Quel résultat ?
4. Rapidement ou sans contrainte ?

Toujours proposer :
- exemples
- génération automatique

Si blocage :
→ générer directement une proposition

---

### STEP 2 — OFFRE

Objectif :
- Clarifier ce qui est vendu

Mode rapide :
- Générer une offre cohérente par défaut
- Demander validation simple (OK / ajuster)

Mode expert :
- Questions détaillées (prix, contenu, garantie)

---

### STEP 3 — AVATAR

Objectif :
- Définir la cible

Mode rapide :
- Générer un avatar réaliste
- Résumé en 3-5 lignes
- Validation rapide

Mode expert :
- Questions complètes

---

### STEP 4 — CONTENT COLLECTION

Objectif :
- Récupérer crédibilité

Mode rapide :
- Générer preuves crédibles par défaut
- Signaler que c’est modifiable

Mode expert :
- Collecte réelle (témoignages, chiffres…)

---

### STEP 5 — PAGE STRATEGY

Objectif :
- Définir angle + promesse

Mode rapide :
- Proposer 1 angle fort
- Validation directe

Mode expert :
- 2-3 angles + choix utilisateur

Si hésitation :
→ imposer une recommandation

---

### STEP 6 — PAGE STRUCTURE

Objectif :
- Définir structure

Mode rapide :
- Générer structure directement

Mode expert :
- proposer + justifier

---

### STEP 7 — COPYWRITING

Objectif :
- Rédiger la page

Mode rapide :
- Générer la page complète en une fois

Proposer :
1. Valider
2. Modifier une section

Mode expert :
- rédaction section par section

---

### STEP 8 — DESIGN

Objectif :
- Définir visuel

Mode rapide :
- Design par défaut (clean, conversion)

Mode expert :
- choix détaillé

---

### STEP 9 — GÉNÉRATION AUTOMATISÉE

Objectif :
- Générer et publier la page sans action utilisateur

Actions de Claude :

1. Générer le prompt Lovable structuré
2. Envoyer automatiquement via MCP / API Lovable
3. Récupérer le résultat (page générée)

4. Créer les fichiers dans le projet (via Claude Code)
5. Commit + push GitHub automatique

6. Déclencher déploiement Vercel (auto via repo)

---

Fallback (si API indisponible) :
- Fournir prompt Lovable prêt à copier

---

Condition de passage :
- Page générée et accessible

---

### STEP 9b — META-AUDIT

Objectif :
- Auditer l'ensemble des outputs produits avant génération de code
- Détecter les blocs faibles (copy, offre, design, prompt Lovable)
- Corriger ou déclencher une correction ciblée
- Valider que le score est ≥ 15/18 avant de continuer

Actions de Claude :

1. Lire : copy validé, offre positionnée, brief design, prompt Lovable
2. Appliquer la grille de scoring (9 critères, 0–2 chacun, total /18)
3. Présenter le tableau de scoring à l'utilisateur

Si score ≥ 15/18 :
→ Déclarer l'audit validé
→ Passer immédiatement à git-publish

Si score < 15/18 :
→ Identifier les critères faibles
→ Réécrire directement ou envoyer instructions correctives au skill concerné
→ Répéter jusqu'à validation (max 3 itérations)
→ Si toujours < 15/18 après 3 itérations : alerter l'utilisateur, proposer corrections manuelles, attendre validation

Skill : meta-auditor.md

---

Condition de passage :
- Score méta-audit ≥ 15/18 validé
- Rapport d'audit présenté à l'utilisateur

---

### STEP 10 — QUALITY CHECK

Si mode rapide :
- Vérification rapide uniquement
- Ne pas bloquer le flux

Checklist :
- promesse claire
- CTA visibles
- lisibilité
- cohérence

---

### STEP 11 — VALIDATION FINALE

Objectif :
- Confirmer que la page est prête

Actions :
- Fournir URL finale
- Demander validation rapide (OK / ajuster)

---

## Règle globale — réduction de friction

Principe clé :
→ L'utilisateur ne doit JAMAIS quitter l'expérience

Toutes les actions techniques sont :
- automatisées
- invisibles

- Générer > questionner
- Ne jamais bloquer
- Toujours proposer une version exploitable

Claude agit comme :
→ un opérateur
→ pas un formateur



---

## Règles — mode rapide

- Produire vite
- Réduire les questions
- Générer si manque info
- Priorité au résultat