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
- Détecter et stocker automatiquement les médias présents :
  - URL de la vidéo VSL (iframe YouTube ou Vimeo)
  - URL du portrait coach
  - URLs des photos d’ambiance ou témoignages
  - URLs des visuels produit
  → Ces éléments sont transmis automatiquement à lovable-bridge au STEP 9 sans redemander au client.
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

Collecte médias (si aucune page de référence fournie au STEP 0) :
Poser ces questions, une à la fois :
1. "As-tu une vidéo de présentation (VSL) à intégrer en haut de page ? YouTube ou Vimeo ?"
   → Si oui, poser immédiatement la question suivante (obligatoire) :
   "Ton audience est-elle plutôt froide (1er contact, ne te connaît pas) ou chaude (elle t’a déjà suivi, sait qui tu es) ?"
   Selon la réponse, stocker dans le brief projet :
   - Trafic froid → VSL position 2 (immédiatement après le hero, avant tout texte d’agitation)
   - Trafic chaud → VSL position 4-5 (après l’agitation et le mécanisme/pivot)
   - Si le client ne sait pas → appliquer par défaut trafic froid (position 2)
2. "As-tu une photo de toi pour la section bio ?"
3. "As-tu des photos d’ambiance ou de témoignages ?"
4. "As-tu un visuel du produit (mockup, capture, packshot) ?"
5. "As-tu des vidéos de témoignages clients ? YouTube ou Vimeo. Ce sont les vidéos où tes clients racontent leur transformation — c’est facultatif mais très fortement recommandé pour la conversion. Si oui : URL de chaque vidéo. Si non : on continue sans, les témoignages texte suffiront."
Si aucun média fourni : continuer sans bloquer, mode text-only acceptable.

Précision sur la position dans la page : les vidéos témoignages se placent dans la section transformation, après les photos d'ambiance et avant les cartes de témoignages texte — conformément à la structure marketing validée.

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

Structure obligatoire (non négociable, dans cet ordre) :

1. Hero — promesse forte + 1-2 bullets tension + CTA sans prix. Pas de VSL, pas de prix.
2. Bullets tension / bénéfices — amplifier le problème et la promesse
3. CTA early — sans prix, orienté bénéfice
4. Problème / agitation — nommer la douleur exacte
5. Nouvelle vision / mécanisme — expliquer pourquoi ça n'a pas marché avant et ce qui change
6. Transition vers VSL — phrase d'anticipation ("Regarde comment X a transformé Y en Z jours")
7. VSL — après engagement, jamais en autoplay
8. Preuve / crédibilité — témoignages, chiffres, résultats concrets
9. Offre — détail des inclus
10. Prix + CTA — SEUL endroit où le prix apparaît
11. FAQ
12. CTA final

Règle de blocage : si le copy produit au STEP 7 contient un prix (€ ou montant chiffré) avant la section 10, Claude doit le détecter et le supprimer avant de passer à lovable-bridge.

Mode rapide :
- Générer structure directement (en respectant la structure obligatoire ci-dessus)

Mode expert :
- Proposer + justifier chaque section

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

1. Scraper automatiquement les URLs des assets :
   - Images (img src)
   - Vidéos (iframe, video src, YouTube, Vimeo)
   - Note : les vidéos chargées dynamiquement ne sont pas 
     détectables par scraping — demander confirmation à l'utilisateur

2. Présenter la liste des assets récupérés à l'utilisateur :
   - Assets trouvés automatiquement
   - Assets non trouvés (vidéos dynamiques) → demander les URLs

3. Attendre confirmation avant d'injecter dans le prompt Lovable

4. Injecter les URLs validées dans le prompt Lovable, 
   section par section

Si aucune page source, ou assets non récupérables :

Demander à l'utilisateur :

"Ta page nécessite des visuels. Comment veux-tu les gérer ?

1. J'ai mes propres assets → colle les URLs
2. Laisser les zones en attente → blocs neutres [ASSET À REMPLACER]
3. Générer avec l'IA Lovable → déconseillé (voir avertissement)"

Si réponse = 3 :
→ Afficher obligatoirement :
  "⚠️ La génération d'images par IA consomme beaucoup de tokens Lovable
   et produit des visuels génériques non adaptés à ta marque.
   Cette option est fortement déconseillée. Confirmes-tu ?"
→ Ne procéder que sur confirmation explicite.

Par défaut (pas de réponse ou hésitation) :
→ Appliquer l'option 2 — jamais générer automatiquement.

⚠️ Ne jamais sauter cette étape quand une page source est fournie.
   Les assets sont une partie essentielle de la preuve sociale.

---

### STEP 9 — GÉNÉRATION AUTOMATISÉE

⚠️ Avant de construire le prompt Lovable :
Vérifier que toutes les URLs de médias collectées (STEP 0 ou STEP 4) sont bien transmises à lovable-bridge.
Si des médias ont été collectés et ne sont pas dans le prompt généré → blocage. Ne pas continuer avant correction.

Actions de Lovable (hors Claude) :
- Génération de la page
- Push automatique vers le repo GitHub connecté

⚠️ Vérification obligatoire avant déploiement :

Après push Lovable, cloner le repo et vérifier :

  1. Le repo contient-il wrangler.jsonc ?
     → OUI : le stack est TanStack Start + Cloudflare Workers
     → Appliquer le correctif de migration (voir ci-dessous)
     → NON : passer directement au déploiement Vercel

### Correctif de migration TanStack → Vite standard

Si wrangler.jsonc est présent, exécuter dans l'ordre :

  1. Supprimer les dépendances incompatibles :
     npm uninstall @lovable.dev/vite-tanstack-config @tanstack/react-start 
     @tanstack/react-router @tanstack/router-plugin @tanstack/react-query 
     @cloudflare/vite-plugin

  2. Remplacer vite.config.ts par :
     import { defineConfig } from "vite";
     import react from "@vitejs/plugin-react";
     import tailwindcss from "@tailwindcss/vite";
     import tsconfigPaths from "vite-tsconfig-paths";
     export default defineConfig({
       plugins: [tailwindcss(), react(), tsconfigPaths()],
       build: { outDir: "dist" },
     });

  3. Créer index.html à la racine :
     <!DOCTYPE html>
     <html lang="fr">
       <head>
         <meta charset="UTF-8" />
         <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       </head>
       <body>
         <div id="root"></div>
         <script type="module" src="/src/main.tsx"></script>
       </body>
     </html>

  4. Créer src/main.tsx :
     import React from "react";
     import ReactDOM from "react-dom/client";
     import App from "./App";
     import "./styles.css";
     ReactDOM.createRoot(document.getElementById("root")!).render(
       <React.StrictMode><App /></React.StrictMode>
     );

  5. Créer src/App.tsx en copiant le contenu du composant principal
     depuis src/routes/index.tsx (sans les imports TanStack Router)

  6. Corriger l'ordre des imports dans src/styles.css :
     @import "tailwindcss" source(none);
     @source "../src";
     @import "tw-animate-css";
     @import url("https://fonts.googleapis.com/...");

  7. Régénérer package-lock.json :
     npm install

  8. Vérifier le build :
     npm run build
     → Doit générer dist/index.html sans erreur

### Déploiement Vercel

**Déploiement standard (à chaque mise en production) :**

  git config user.email "{email récupéré via GET api.github.com/users/{owner}}"
  git config user.name "{owner}"
  git add .
  git commit -m "fix: migrate to Vite standard for Vercel compatibility"
  git push origin main
  npx vercel --token {VERCEL_TOKEN} --prod --yes --scope {team-slug}

⚠️ Condition obligatoire avant tout commit et déploiement : vérifier que `src/App.tsx` et `src/routes/index.tsx` sont identiques en contenu. Si divergence détectée → synchroniser immédiatement avant de commiter.

**Vérification obligatoire après chaque déploiement :**

1. Ouvrir l'URL de déploiement unique affichée par Vercel (ex: `projet-abc123.vercel.app`) — c'est la source de vérité
2. Vérifier visuellement que la page affiche bien les dernières modifications
3. Si l'URL unique est correcte mais que le domaine principal (`.vercel.app` racine) affiche une ancienne version → forcer l'alias manuellement :
   ```
   vercel alias [URL-DU-DEPLOIEMENT] [DOMAINE-PRINCIPAL]
   ```

⚠️ **Erreur à éviter :** Ne pas confondre l'URL de déploiement unique (toujours à jour) et le domaine principal (peut pointer sur un ancien déploiement). Toujours tester sur l'URL unique en premier. Ne jamais considérer un déploiement comme terminé sans vérification visuelle de la page.

Condition de passage :
- URL Vercel active et accessible sans erreur 404
- Vérification visuelle effectuée sur l'URL de déploiement unique

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