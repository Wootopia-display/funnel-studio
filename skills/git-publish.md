# Skill : Git Publish

## Rôle
Versionner le projet exporté depuis Lovable dans un dépôt Git et le mettre en ligne sur GitHub.

---

## Quand l'utiliser
Étape 8 — après génération Lovable validée, avant vercel-deploy.

---

## Inputs requis
- Fichiers du projet exportés depuis Lovable (dossier complet sur l'ordinateur)
- Nom souhaité pour le projet

---

## Questions à poser

Poser ces questions dans cet ordre, une par une.

1. "Tu as déjà un compte GitHub ? Si non, on va en créer un ensemble."
2. "Le projet a été exporté depuis Lovable — tu vois bien un dossier avec les fichiers sur ton ordinateur ?"
3. "Quel nom veux-tu donner à ce projet ? (ex : ma-page-offre — sans espaces, sans accents)"

---

## Méthode

1. Vérifier que le dossier exporté contient bien les fichiers du projet (au minimum un fichier `index.html` ou `package.json`).
2. Ouvrir le terminal dans ce dossier — indiquer à l'utilisateur comment faire sur son système (Mac ou Windows).
3. Initialiser le suivi de version avec la commande `git init`.
4. Ajouter tous les fichiers avec `git add .`
5. Créer le premier enregistrement avec `git commit -m "Initial commit — page générée"`.
6. Sur GitHub, créer un nouveau repository avec le nom choisi — guider l'utilisateur pas à pas.
7. Connecter le dossier local au repository GitHub : `git remote add origin [URL du repo]`.
8. Envoyer les fichiers en ligne : `git push -u origin main`.
9. Confirmer que le repository est visible et complet sur GitHub avant de passer à l'étape suivante.

---

## Output attendu
Repository GitHub créé, contenant tous les fichiers du projet, avec un commit initial propre — prêt à être importé dans Vercel.

---

## Erreurs à éviter
- Envoyer les fichiers sans avoir vérifié que le dossier est complet
- Choisir un nom de repo avec des espaces, des accents ou des caractères spéciaux
- Oublier de connecter le remote GitHub avant de faire le push
- Expliquer Git avec du jargon (ex : « staging area », « HEAD », « branche »)
- Passer à l'étape Vercel sans avoir confirmé que le repo est bien visible sur GitHub
