# Prompt de démarrage initial

## Instructions
Copier le prompt ci-dessous et le coller dans Claude Code pour démarrer.

## Prompt
Lis les fichiers suivants dans l'ordre :
1. README.md
2. CLAUDE.md
3. workflows/page-creation-master.md

Une fois la lecture terminée, **avant toute autre chose** :

1. Chercher `.env` dans l'ordre avec l'outil Bash :
   ```
   test -f funnel-studio/.env && echo "found:funnel-studio/.env" || \
   test -f .env && echo "found:.env" || \
   test -f ../.env && echo "found:../.env" || \
   echo "missing"
   ```
2. Si trouvé → utiliser ce fichier
3. Si absent partout → le créer automatiquement : `cp .env.example .env`
4. Variables **réellement requises** au démarrage : `GITHUB_TOKEN` et `VERCEL_TOKEN`
5. Variables à **ne jamais demander** au démarrage :
   - `GITHUB_REPO` → sera collecté en STEP 1, rempli automatiquement avant le push
   - `VERCEL_PROJECT_ID` → auto-généré au 1er déploiement, laisser vide
   - `VERCEL_ORG_ID` → auto-généré au 1er déploiement, laisser vide
6. Vérifier uniquement `GITHUB_TOKEN` et `VERCEL_TOKEN` avant de continuer
7. Seulement ensuite → démarrer le workflow depuis l'Étape 0 (choix du mode)

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
