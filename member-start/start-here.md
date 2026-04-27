# Démarrage — Par ici

Bienvenue dans Funnel Studio. Suivre ces étapes dans l'ordre.

## Étape 0 — Configuration `.env`

**Claude crée automatiquement le fichier `.env` au démarrage** s'il n'existe pas encore.

Tu dois seulement renseigner ces variables dans le fichier `.env` :

| Variable | Requis | Note |
|---|---|---|
| `GITHUB_TOKEN` | Optionnel | Pas nécessaire si connexion via Lovable OAuth |
| `GITHUB_REPO` | Oui | Format : `owner/repo` |
| `VERCEL_TOKEN` | Oui | Ton token Vercel personnel |
| `VERCEL_PROJECT_ID` | Non | Auto-généré — laisser vide |
| `VERCEL_ORG_ID` | Non | Auto-généré — laisser vide |

**Règles `.env` :**
- Ne jamais écrire de texte après `=` (ex: `VERCEL_TOKEN=mon_token` ✓, `VERCEL_TOKEN=coller ici` ✗)
- Lovable ne nécessite pas de clé API — ne pas ajouter `LOVABLE_API_KEY`
- Seuls les vrais secrets vont dans ce fichier

## Étapes

1. **Ouvrir VS Code** dans ce dossier workspace
2. **Lancer Claude Code** (terminal : `claude`)
3. **Copier le prompt** depuis `member-start/initial-start-prompt.md`
4. **Coller le prompt** dans Claude Code et envoyer
5. Suivre les instructions de Claude pour créer votre page

## En cas de problème
Relire `CLAUDE.md` et `workflows/page-creation-master.md`.
