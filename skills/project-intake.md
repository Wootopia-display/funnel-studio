# Skill : Project Intake

## Rôle
Ouvrir le projet, détecter si une page existante existe, et collecter les informations de base sans lesquelles aucune étape suivante ne peut démarrer.

---

## Quand l'utiliser
Étape 1 — au démarrage de chaque nouveau projet de page. Aucune exception.

---

## Inputs requis
- Nom du client ou du projet
- Existence ou non d'une page déjà en ligne
- URL de la page si elle existe
- Contenu brut si aucune page n'existe (texte, PDF, doc, notes)
- Type de page visé (capture, vente, webinaire, autre)
- Deadline si connue

---

## Questions à poser

Poser ces questions dans cet ordre, une à la fois. Attendre la réponse avant de continuer.

1. "Comment s'appelle ce projet ou ce client ?"
2. "Est-ce qu'il existe déjà une page en ligne pour cette offre ?"
   - Si oui : "Quelle est l'URL ?"
   - Si non : "Est-ce que tu as un texte, un PDF, des notes ou un brouillon de départ ?"
3. "Quel type de page veux-tu créer ? (capture d'email, page de vente, page de webinaire, autre)"
4. "Tu as une deadline à respecter ?"

---

## Méthode

1. Demander si une page existe déjà.
   - Si oui : récupérer l'URL. Indiquer que la page sera analysée à l'étape suivante.
   - Si non : demander le contenu brut disponible (tout format accepté).
2. Identifier le type de page visé.
3. Collecter le nom du projet et la deadline.
4. Reformuler les informations collectées en une synthèse courte (5 lignes max).
5. Demander confirmation explicite avant de fermer cette étape.
6. Remplir le fichier `client-input/project-brief.md` à partir du template `templates/project-brief-template.md`.

---

## Output attendu
Fichier `client-input/project-brief.md` complété avec :
- Nom du projet
- Existence ou non d'une page existante (+ URL si applicable)
- Contenu brut si aucune page existante
- Type de page visé
- Deadline

---

## Erreurs à éviter
- Supposer qu'il n'y a pas de page existante sans avoir posé la question
- Passer à l'étape 2 sans avoir les informations de base confirmées
- Accepter une réponse vague comme "c'est une page de vente" sans préciser le produit ou l'offre
- Demander toutes les questions d'un coup dans un seul message
- Générer quoi que ce soit avant que le brief soit validé
