# Funnel Studio

Workspace de création de pages marketing piloté par Claude Code.

## Rôle
Ce système permet de créer des pages marketing complètes (brief → copy → design → déploiement) via des skills spécialisés et des workflows structurés.

## Fonctionnement
Le système génère, audite et corrige automatiquement les pages.

Score minimum requis : 15/18  
Sinon → correction automatique

## Démarrage
👉 Lis prompts/start.md et commence.

## 🇬🇧 How to test (reference only)

Do not use this in practice. English commands may switch the system language.

Start a new Claude Code session and send:

👉 Read prompts/start.md and begin.

---

⚠️ Important :
- Toujours écrire les commandes en français
- Le système doit répondre en français par défaut

---

Lance le workflow jusqu’à l’ÉTAPE 9.

Après génération du prompt Lovable, Claude va :

- Appeler automatiquement le **meta-auditor**
- Afficher un tableau de score (9 critères, /18)
- Corriger les blocs faibles
- Bloquer la suite tant que score < 15/18

---

### Test isolé du meta-auditor

Commande :

Lance le meta-auditor sur ce contenu : [colle ton texte]

Résultat :
- Analyse
- Score
- Correction automatique

---

## 🇬🇧 How to test (reference only)

Use English only if needed, but system default must stay French.

Start a new Claude Code session and send:

Read prompts/start.md and begin.
