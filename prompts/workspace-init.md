# Prompt : Workspace Init

## Usage
Ce prompt a été utilisé pour créer l'arborescence initiale de ce workspace.

## Prompt utilisé
> MISSION : Créer uniquement l'arborescence du workspace et des fichiers de base
> pour un système de création de pages marketing piloté par Claude Code.
> [Voir la mission complète dans l'historique de conversation]

MISSION
Créer uniquement l’arborescence du workspace et des fichiers de base pour un système de création de pages marketing piloté par Claude Code.

IMPORTANT
- Ne pas générer de contenu long ou complexe.
- Créer des fichiers courts avec placeholders clairs.
- Ne pas inventer de logique métier avancée.
- Objectif : base propre, stable, modifiable ensuite.

ARBORESCENCE À CRÉER

/
README.md
CLAUDE.md

/workflows/
workflows/page-creation-master.md

/skills/
skills/project-intake.md
skills/offer-positioning.md
skills/avatar-definition.md
skills/page-strategy.md
skills/page-copywriting.md
skills/page-design.md
skills/lovable-bridge.md
skills/git-publish.md
skills/vercel-deploy.md
skills/quality-check.md

/templates/
templates/project-brief-template.md
templates/page-outline-template.md
templates/content-collection-template.md

/prompts/
prompts/README.md
prompts/workspace-init.md
prompts/start.md
prompts/page-generation.md
prompts/lovable.md

/member-start/
member-start/start-here.md
member-start/initial-start-prompt.md

/client-input/
client-input/README.md

CONTENU MINIMAL À METTRE DANS CHAQUE FICHIER

RÈGLE GÉNÉRALE
- 5 à 15 lignes max par fichier
- structure simple
- titres clairs
- placeholders exploitables

README.md
- rôle du workspace
- comment démarrer (très court)

CLAUDE.md
- règles globales (version minimale)
- préciser que le système sera complété ensuite

workflows/page-creation-master.md
- lister les étapes (sans détail)
- format liste simple

skills/*
- chaque fichier :
  - rôle
  - quand utilisé
  - inputs attendus
  - output attendu

templates/*
- structure vide avec sections

/prompts/README.md
- expliquer que tous les prompts sont stockés ici
- interdiction de laisser des prompts hors de ce dossier

prompts/workspace-init.md
- indiquer : prompt utilisé pour créer ce workspace

prompts/start.md
- placeholder : prompt de démarrage utilisateur

prompts/page-generation.md
- placeholder : génération de page

prompts/lovable.md
- placeholder : prompt pour Lovable

member-start/start-here.md
- étapes simples :
  1. ouvrir VS Code
  2. lancer Claude Code
  3. utiliser prompt de démarrage

member-start/initial-start-prompt.md
- placeholder du prompt de démarrage

client-input/README.md
- expliquer où mettre contenu utilisateur

CONTRAINTES

- Tous les prompts doivent être centralisés dans /prompts/
- Aucun prompt critique ne doit être ailleurs
- Structure lisible et professionnelle
- Pas de contenu inutile

SORTIE ATTENDUE

1. Créer tous les dossiers et fichiers
2. Remplir avec contenu minimal
3. Afficher un récapitulatif clair de l’arborescence
4. Ne rien faire d’autre

## Date de création
2026-04-21
