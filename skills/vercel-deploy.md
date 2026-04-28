# Skill : Vercel Deploy

## Rôle
Déployer le projet depuis GitHub sur Vercel pour obtenir une URL publique et accessible en ligne.

---

## Quand l'utiliser
Étape 9 — après git-publish confirmé, avant quality-check.

---

## Inputs requis
- Repository GitHub du projet créé et à jour (git-publish)
- Compte Vercel (existant ou à créer)
- Nom de domaine personnalisé si applicable (optionnel)

---

## Questions à poser

Poser ces questions dans cet ordre, une par une.

1. "Tu as déjà un compte Vercel ? Si non, on va en créer un ensemble — c'est gratuit."
2. "Le repository GitHub du projet est bien visible dans ton compte GitHub ?"
3. "Tu as un nom de domaine à connecter, ou l'URL générée par Vercel suffit pour l'instant ?"

---

## Méthode

1. Confirmer que le repository GitHub est bien à jour — vérifier qu'il contient les derniers fichiers.
2. Se connecter sur Vercel et cliquer sur « Add New Project ».
3. Choisir « Import Git Repository » et sélectionner le repo du projet dans la liste.
4. Laisser tous les paramètres de build par défaut — Vercel configure automatiquement la plupart des projets.
5. Cliquer sur « Deploy » et attendre la fin du déploiement (moins d'une minute en général).
6. Copier l'URL générée par Vercel (format : `nom-du-projet.vercel.app`).
7. Ouvrir l'URL dans un navigateur et vérifier que la page s'affiche correctement.
8. Si un domaine personnalisé est souhaité : aller dans les paramètres du projet sur Vercel → « Domains » → ajouter le domaine. Ne faire cette étape qu'après avoir validé que la page fonctionne sur l'URL par défaut.

---

## Output attendu
URL de déploiement Vercel fonctionnelle, page accessible dans un navigateur — prête pour le quality-check final.

---

## Connexion GitHub → Vercel (à faire une seule fois par projet)

Problème connu : quand un projet Vercel est créé via CLI, il n'est pas automatiquement connecté au repo GitHub. Le bouton "Redeploy" dans le dashboard Vercel repart du dernier déploiement CLI — pas du dernier commit Git. Résultat : les modifications pushées sur GitHub ne sont jamais publiées automatiquement.

### Étape obligatoire après le premier déploiement

Dès que la page est déployée pour la première fois, guider l'utilisateur pour connecter le repo GitHub :

1. Aller sur vercel.com → ouvrir le projet
2. Cliquer sur "Settings" → "Git"
3. Cliquer "Connect Git Repository"
4. Sélectionner GitHub → choisir le repo du projet
5. Sélectionner la branche "main"
6. Confirmer

Une fois cette connexion faite, chaque git push sur main déclenche automatiquement un nouveau déploiement Vercel. L'utilisateur n'a plus rien à faire.

### Avant que la connexion soit faite

Tant que le repo GitHub n'est pas connecté à Vercel, NE PAS demander à l'utilisateur de cliquer "Redeploy" dans le dashboard — ça ne fonctionnera pas. Le seul moyen de publier les modifications est via la commande CLI (gérée automatiquement par le système).

### Message à afficher à l'utilisateur après le premier déploiement

"Ta page est en ligne. Pour que les prochaines modifications soient publiées automatiquement, connecte ton repo GitHub à Vercel en 30 secondes :
vercel.com → ton projet → Settings → Git → Connect Git Repository → sélectionne le repo → branche main.
Une fois fait, chaque modification sera publiée automatiquement à chaque push."

---

## Erreurs à éviter
- Déployer sans avoir vérifié que le dernier push GitHub est bien à jour
- Modifier les paramètres de build sans savoir ce qu'ils font — laisser les valeurs par défaut
- Oublier de tester l'URL dans un navigateur après le déploiement
- Connecter un domaine personnalisé avant d'avoir validé que la page fonctionne sur l'URL Vercel
- Considérer l'étape comme terminée sans avoir ouvert et vérifié la page en ligne
- Demander à l'utilisateur de cliquer "Redeploy" dans le dashboard Vercel si le repo GitHub n'est pas encore connecté — ça ne publiera pas les dernières modifications

---

## Piège critique — App.tsx et routes/index.tsx désynchronisés

Problème : dans un projet React généré par Lovable avec TanStack Router, il existe deux fichiers de page :
- `src/App.tsx` — utilisé par Vercel quand il rebuild depuis GitHub (via main.tsx)
- `src/routes/index.tsx` — utilisé par le router en développement local

Si on modifie uniquement `routes/index.tsx`, le déploiement CLI local fonctionne (il déploie le dist/ local correct), mais Vercel rebuild depuis GitHub et utilise `App.tsx` — l'ancienne version. Résultat : la page en production ne reflète jamais les modifications.

Solution validée : toujours modifier les deux fichiers simultanément. `App.tsx` et `routes/index.tsx` doivent être identiques en contenu à tout moment. Toute modification de contenu, de structure ou de médias doit être appliquée dans les deux fichiers avant le commit.

Règle à appliquer sur tous les projets générés par Lovable avec TanStack Router :
- Avant chaque commit, vérifier que `App.tsx` et `routes/index.tsx` sont synchronisés
- Si une divergence est détectée, synchroniser les deux fichiers avant de continuer
- Ne jamais commiter un état où les deux fichiers sont différents
