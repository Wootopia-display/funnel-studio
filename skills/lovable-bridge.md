# Skill : Lovable Bridge

## Rôle
Transformer le copy et le brief design validés en un prompt clair à coller dans Lovable pour générer la page.

---

## Quand l'utiliser
Étape 7 — après design brief validé, avant git-publish.

---

## Inputs requis
- Copy complet de la page, validé section par section (page-copywriting)
- Brief design finalisé : palette, typographie, composants (page-design)
- Plan de page validé (page-strategy)

---

## Questions à poser

Poser ces questions dans cet ordre avant de construire le prompt.

1. "Le copy de chaque section est bien validé ? Rien n'est à modifier ?"
2. "Le brief design est finalisé — couleurs, polices, style des boutons ?"
3. "C'est une page de capture (email uniquement) ou une page de vente (offre complète) ?"

---

## Méthode

1. Reprendre le plan de page et lister les sections dans l'ordre : hero → problème → solution → preuves → CTA final.
2. Pour chaque section, assembler : le texte exact (copy validé) + les directives visuelles correspondantes (depuis le brief design).
3. Formuler chaque instruction en langage simple et impératif : « Crée une section hero avec ce titre : [titre]. Fond de couleur [hex]. Bouton CTA de couleur [hex] avec ce texte : [texte CTA]. »
4. Ajouter en fin de prompt une instruction globale de responsive mobile : « Toutes les sections doivent s'afficher correctement sur mobile, texte lisible, bouton visible sans scroller. »
5. Présenter le prompt complet à l'utilisateur pour relecture avant envoi dans Lovable.
6. Une fois validé, indiquer à l'utilisateur comment coller le prompt dans Lovable et lancer la génération.

---

## Output attendu
Prompt unique, structuré section par section, prêt à coller dans Lovable — sans ambiguïté visuelle ni texte manquant.
- Note : cet output alimente directement le meta-auditor (étape 9b). Le prompt ne doit contenir aucun placeholder non rempli — tout le copy doit être réel et définitif avant de passer à l'audit.

---

## Erreurs à éviter
- Construire le prompt avant que le copy soit entièrement validé
- Mélanger les instructions de texte et de design sans structure claire par section
- Utiliser du jargon technique dans le prompt (ex : « flexbox », « z-index », « padding »)
- Omettre l'instruction de responsive mobile
- Envoyer dans Lovable sans avoir montré le prompt à l'utilisateur pour relecture
- Transmettre un prompt contenant des placeholders non remplis — le meta-auditor le détectera comme un score 0/2 sur le critère de spécificité du prompt Lovable
