# Workflow : Création de page marketing

## Sécurité

- Ne jamais afficher une clé API
- Ne jamais demander de coller une clé dans le chat
- Les clés doivent être uniquement renseignées dans le fichier `.env`
- Ne jamais lire, éditer, corriger ou afficher le contenu du fichier `.env`
- Si une clé est manquante :
  → indiquer uniquement le nom de la variable à renseigner  
  Exemple : `VERCEL_TOKEN`

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

### Étape 0 — Vérification automatique de l’environnement

**Au démarrage, exécuter immédiatement :**

1. Chercher `.env` dans l’ordre avec l’outil Bash :
   ```
   test -f funnel-studio/.env && echo "found:funnel-studio/.env" || \
   test -f .env && echo "found:.env" || \
   test -f ../.env && echo "found:../.env" || \
   echo "missing"
   ```

Si `.env` est trouvé :
→ Utiliser ce fichier pour la session

Si `.env` est absent partout :
→ Le créer automatiquement avec l’outil Bash : `cp .env.example .env`
→ Informer l’utilisateur : "J’ai créé le fichier `.env` depuis `.env.example`. Tu dois maintenant renseigner les variables requises directement dans ce fichier."
→ Ne jamais afficher le contenu du fichier
→ Indiquer uniquement les variables obligatoires au démarrage : `GITHUB_TOKEN` et `VERCEL_TOKEN`
→ Ne pas demander `GITHUB_REPO` — il sera collecté en STEP 1
→ Attendre confirmation avant de continuer

⚠️ Ne colle jamais tes clés ici — remplis uniquement le fichier `.env`

---

### Étape 1 — Vérification des variables

→ Vérifier la présence des variables requises sans afficher leurs valeurs

Variables **requises au démarrage** :
- `GITHUB_TOKEN` (obligatoire)
- `VERCEL_TOKEN` (obligatoire)

Variables à **ne jamais demander** :
- `GITHUB_REPO` → collecté en STEP 1, rempli automatiquement avant le push (STEP 9)
- `VERCEL_PROJECT_ID` → auto-généré au 1er déploiement, ne jamais demander
- `VERCEL_ORG_ID` → auto-généré au 1er déploiement, ne jamais demander

Si `GITHUB_TOKEN` ou `VERCEL_TOKEN` est absent ou vide :
→ Indiquer uniquement le nom de la variable manquante
→ Bloquer l’automatisation et attendre correction

Si OK :
→ Lancer automatiquement le workflow

---

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

## Règles d'interaction — questions

- Toujours poser les questions via AskUserQuestion avec des options cliquables
- Ne jamais poser une question ouverte sans proposer de choix
- Proposer 2 à 4 options par question
- Une seule question à la fois

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

### STEP 8b — STYLE DE PAGE

Demander à l'utilisateur :

"Veux-tu appliquer le style Hormozi à cette page ?
(phrases courtes, rythme visuel fort, copy émotionnel ligne par ligne)

1. Oui — appliquer le style Hormozi
2. Non — décris le style souhaité"

→ Attendre la réponse avant de générer le prompt Lovable.
→ Bloquer si aucune réponse.

---

### STEP 8c — ASSETS VISUELS

Si une page source a été fournie en STEP 0 :
→ Scraper automatiquement les URLs des assets (images, vidéos, iframes)
→ Lister les assets à l'utilisateur pour validation
→ Injecter les URLs validées dans le prompt Lovable, section par section

Si aucune page source, ou assets non récupérables :

Demander à l'utilisateur :

"Ta page nécessite des visuels. Comment veux-tu les gérer ?

1. J'ai mes propres assets → colle les URLs ou décris les fichiers
2. Laisser les zones en attente → blocs neutres [ASSET À REMPLACER]
3. Générer avec l'IA Lovable → déconseillé (voir avertissement)"

Si réponse = 3 :
→ Afficher obligatoirement :
  "⚠️ Attention : la génération d'images par IA consomme beaucoup de tokens Lovable
   et produit des visuels génériques non adaptés à ta marque.
   Cette option est fortement déconseillée. Confirmes-tu ?"
→ Ne procéder que sur confirmation explicite.

Par défaut (pas de réponse ou hésitation) :
→ Appliquer l'option 2 — jamais générer automatiquement.

---

### STEP 9 — GÉNÉRATION AUTOMATISÉE

Actions de Lovable (hors Claude) :
- Génération de la page
- Push automatique vers le repo GitHub connecté

### Contrainte technique obligatoire — prompt Lovable

Toujours inclure cette instruction au début du prompt Lovable :

  IMPORTANT TECHNICAL CONSTRAINT:
  - Use Vite + React standard only
  - NO TanStack Start
  - NO Cloudflare Workers  
  - Must be deployable on Vercel with a standard vite build
  - Single page app, no SSR required

Raison : Lovable utilise TanStack Start + Cloudflare Workers par défaut
depuis sa mise à jour récente. Ce stack est incompatible avec Vercel.
Sans cette contrainte, la page génère une erreur 404 sur Vercel.

Si le repo livré par Lovable contient wrangler.jsonc ou 
@lovable.dev/vite-tanstack-config dans package.json :
→ Le projet est sur le mauvais stack
→ Régénérer immédiatement avec le prompt corrigé
→ Ne pas tenter d'adapter — trop risqué

Actions de Claude après push GitHub :

1. Cloner le repo en local :
   git clone https://{GITHUB_TOKEN}@github.com/{GITHUB_REPO}.git

2. Déployer via Vercel CLI (npx vercel) :
   cd {nom-repo}
   npx vercel --token {VERCEL_TOKEN} --yes --scope {team-slug}
   → Le projet Vercel est créé automatiquement au premier déploiement
   → Aucune intégration GitHub UI requise

3. Récupérer l'URL de production dans la sortie CLI
   → Format : https://{nom-repo}.vercel.app

4. Pour chaque déploiement suivant (modification depuis cet UI) :
   → Appliquer les modifications dans le repo cloné
   → git add + commit + push vers GitHub
   → npx vercel --prod --token {VERCEL_TOKEN} --scope {team-slug}

Note : le dossier .vercel créé localement contient la config du projet
→ Ne pas le supprimer entre les déploiements

Condition de passage :
- URL Vercel active et accessible

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