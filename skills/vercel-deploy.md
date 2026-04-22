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

## Erreurs à éviter
- Déployer sans avoir vérifié que le dernier push GitHub est bien à jour
- Modifier les paramètres de build sans savoir ce qu'ils font — laisser les valeurs par défaut
- Oublier de tester l'URL dans un navigateur après le déploiement
- Connecter un domaine personnalisé avant d'avoir validé que la page fonctionne sur l'URL Vercel
- Considérer l'étape comme terminée sans avoir ouvert et vérifié la page en ligne
