# Prompt : Start

## Usage
Prompt de démarrage à utiliser pour lancer une session de création de page.

## Prompt

```
Lis les fichiers suivants dans l'ordre :
1. README.md
2. CLAUDE.md
3. workflows/page-creation-master.md

Une fois la lecture terminée, démarre l'étape 1 du workflow : Project Intake.

Règles strictes à respecter tout au long de la session :
- Pose les questions une par une, jamais plusieurs à la fois
- N'avance à l'étape suivante qu'après ma validation explicite
- Ne saute aucune étape, même si je te le demande
- Si une information manque, bloque et demande-la avant de continuer
- Reformule ce que tu as compris avant chaque production de contenu

Commence maintenant par la première question de l'étape 1.
```

## Notes
- Ce prompt est utilisé depuis `member-start/initial-start-prompt.md`
- Il doit initier le workflow `workflows/page-creation-master.md`
