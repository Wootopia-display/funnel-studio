# Prompt de démarrage initial

## Instructions
Copier le prompt ci-dessous et le coller dans Claude Code pour démarrer.

## Prompt
Lis les fichiers suivants dans l'ordre :
1. README.md
2. CLAUDE.md
3. workflows/page-creation-master.md

Une fois la lecture terminée, **avant toute autre chose** :

1. Vérifier si le fichier `.env` existe avec l'outil Bash : `test -f .env && echo "exists" || echo "missing"`
2. S'il n'existe pas → le créer automatiquement avec : `cp .env.example .env`
3. Informer l'utilisateur du résultat et indiquer les variables à remplir si nécessaire (`GITHUB_REPO` et `VERCEL_TOKEN`)
4. Vérifier que les variables obligatoires sont renseignées avant de continuer
5. Seulement ensuite → démarrer le workflow depuis l'Étape 0 (choix du mode)

Règles strictes à respecter tout au long de la session :
- Pose les questions une par une, jamais plusieurs à la fois
- N'avance à l'étape suivante qu'après ma validation explicite
- Ne saute aucune étape, même si je te le demande
- Si une information manque, bloque et demande-la avant de continuer
- Reformule ce que tu as compris avant chaque production de contenu

Commence maintenant par la vérification du fichier `.env`.

## Note
Ce prompt doit déclencher le workflow complet depuis `workflows/page-creation-master.md`.
Le prompt source est dans `prompts/start.md`.
