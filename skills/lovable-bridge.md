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
- Médias collectés : URLs des images (portrait coach, photos témoignages, visuels produit) et URL de la vidéo VSL si disponible

---

## Questions à poser

Poser ces questions dans cet ordre avant de construire le prompt.

1. "Le copy de chaque section est bien validé ? Rien n'est à modifier ?"
2. "Le brief design est finalisé — couleurs, polices, style des boutons ?"
3. "C'est une page de capture (email uniquement) ou une page de vente (offre complète) ?"

Pour la VSL :
- Si une page de référence a été fournie au STEP 0 ET qu'une vidéo y a été détectée : ne pas reposer la question. Proposer directement : "J'ai détecté une vidéo VSL sur ta page de référence ([URL]). Je l'intègre automatiquement — confirme ou remplace par une autre URL."
- Si aucune page de référence, ou aucune vidéo détectée : demander "As-tu une vidéo de présentation (VSL) à intégrer en haut de page ? (YouTube ou Vimeo)"
- Si non : continuer sans VSL, ne jamais bloquer.

Pour les images :
- Si une page de référence a été fournie au STEP 0 : détecter et proposer automatiquement les images trouvées (portrait coach, photos ambiance, visuels produit) plutôt que de tout redemander.
- Si aucune page de référence : demander "As-tu des images à intégrer : portrait, photos de témoignages, visuels du produit ?"
- Si non : continuer en mode text-only, ne jamais bloquer.

---

## Méthode

1. Reprendre le plan de page et lister les sections dans l'ordre : hero → problème → solution → preuves → CTA final.
2. Pour chaque section, assembler : le texte exact (copy validé) + les directives visuelles correspondantes (depuis le brief design).
3. Formuler chaque instruction en langage simple et impératif : « Crée une section hero avec ce titre : [titre]. Fond de couleur [hex]. Bouton CTA de couleur [hex] avec ce texte : [texte CTA]. »
4. Intégrer les médias dans le prompt en appliquant les patterns ci-dessous.
5. Ajouter en fin de prompt une instruction globale de responsive mobile : « Toutes les sections doivent s'afficher correctement sur mobile, texte lisible, bouton visible sans scroller. »
6. Présenter le prompt complet à l'utilisateur pour relecture avant envoi dans Lovable.
7. Une fois validé, indiquer à l'utilisateur comment coller le prompt dans Lovable et lancer la génération.

---

## Patterns d'implémentation médias

Inclure ces instructions mot pour mot dans le prompt Lovable pour chaque type de média présent.

**HERO avec image de fond :**
"La section hero a une image de fond (src='[URL]') en position absolute couvrant toute la section (object-fit: cover). Un overlay semi-opaque par-dessus (blanc à 80% pour thème clair, noir à 55% pour thème sombre) garantit la lisibilité du texte. Le contenu texte est en position relative au-dessus de l'overlay."

**VSL — section dédiée juste après le hero, avant la section problème :**
"Crée une section dédiée à la vidéo entre le hero et la section problème. Wrapper avec padding-bottom: 56.25% et position relative. L'iframe est en absolute, inset 0, width 100%, height 100%. Coins arrondis 16px, overflow hidden, ombre légère. Attributs obligatoires : allow='autoplay; fullscreen; picture-in-picture' allowfullscreen.
- YouTube : transformer l'URL en https://www.youtube.com/embed/VIDEO_ID
- Vimeo : transformer l'URL en https://player.vimeo.com/video/VIDEO_ID?h=TOKEN"

**Galerie photos témoignages — avant les cartes de témoignages :**
"Grille 3 colonnes desktop, 2 colonnes mobile. Chaque cellule : aspect-ratio 1/1, overflow hidden, border-radius 12px. Image : object-fit cover, width 100%, height 100%. Hover : scale 1.05, transition 500ms."

**Icônes modules — en tête de chaque carte module :**
"Image 64x64px, border-radius 12px, object-fit cover, placée avant le numéro et le titre de chaque carte."

**Visuel produit dans l'offre :**
"Image centrée entre le titre et la liste des inclus. Max-height 220px, width auto, object-fit contain, drop-shadow léger."

**Portrait coach dans la bio :**
"Flex horizontal desktop, vertical mobile. Image à gauche, texte à droite. Image ronde (border-radius 50%), 200x200px desktop / 180x180px mobile, object-fit cover, ombre légère, bordure couleur primaire 3px opacity 20%."

**Règle universelle médias :**
"Toutes les images ont loading='lazy' sauf l'image hero. Chaque image a un attribut alt descriptif. Aucun placeholder visuel si l'URL est fournie — toujours afficher l'image réelle directement."

---

## Output attendu
Prompt unique, structuré section par section, prêt à coller dans Lovable — sans ambiguïté visuelle ni texte manquant.
- Note : cet output alimente directement le meta-auditor (étape 9b). Le prompt ne doit contenir aucun placeholder de copy non rempli — tout le copy doit être réel et définitif avant de passer à l'audit.

---

## Pièges connus et solutions validées

### 1. Vidéo VSL chargée dynamiquement — non visible dans le HTML statique
Problème : quand on fetche une page de référence pour en extraire la VSL, la vidéo est souvent injectée par JavaScript et n'apparaît pas dans le HTML brut.
Solution validée : prévenir le client que si la vidéo ne se trouve pas automatiquement, il doit l'inspecter manuellement dans Chrome (clic droit sur la vidéo → Inspecter → chercher "youtube" ou "vimeo" dans le panneau Elements). L'URL sera sous forme d'iframe src.

### 2. Confusion iframe VSL vs iframe Stripe
Problème : une page de vente contient souvent plusieurs iframes — notamment l'iframe de paiement Stripe qui ressemble à une vidéo dans l'inspecteur.
Solution validée : ignorer toute iframe dont le src contient "stripe", "js.stripe.com", ou "payment". La VSL est toujours une iframe dont le src contient "youtube.com/embed" ou "player.vimeo.com".

### 3. Vimeo privé avec token — format d'URL
Problème : une vidéo Vimeo privée a une URL publique de la forme https://vimeo.com/VIDEO_ID/TOKEN — coller cette URL directement dans un iframe ne fonctionne pas.
Solution validée : transformer systématiquement en https://player.vimeo.com/video/VIDEO_ID?h=TOKEN
Exemple : https://vimeo.com/1180788055/54c35fb2d4 → https://player.vimeo.com/video/1180788055?h=54c35fb2d4

### 4. URLs d'images avec caractères spéciaux
Problème : des images hébergées sur Systeme.io ou d'autres plateformes peuvent avoir des accents ou espaces dans leur nom de fichier (ex : "Méthode401.png") ce qui casse l'URL dans le code.
Solution validée : encoder les caractères spéciaux dans l'URL. Les cas fréquents : é → %C3%A9, è → %C3%A8, à → %C3%A0, espace → %20. Vérifier toujours les URLs contenant des caractères non-ASCII avant de les insérer dans le prompt.

### 5. Images hébergées sur Systeme.io — non visibles par fetch statique
Problème : les images d'une page Systeme.io sont hébergées sur CloudFront et chargées dynamiquement. Un fetch HTML statique de la page ne les retourne pas toujours.
Solution validée : si le fetch ne retourne pas les images, demander au client d'ouvrir la page dans Chrome, clic droit sur chaque image → "Copier l'adresse de l'image" pour récupérer l'URL CloudFront complète.

### 6. Pattern hero avec image de fond — overlay obligatoire
Problème : une image de fond dans le hero sans overlay rend le texte illisible selon la luminosité de la photo.
Solution validée : toujours ajouter un overlay semi-opaque entre l'image et le contenu. Valeurs testées et validées : rgba(255,255,255,0.80) pour thème clair, rgba(0,0,0,0.55) pour thème sombre.

### 7. Portrait coach — layout flex responsive
Problème : un portrait affiché en pleine largeur dans la section bio casse le rythme de lecture sur desktop.
Solution validée : layout flex horizontal sur desktop (image à gauche, texte à droite), vertical centré sur mobile. Image ronde 200px desktop / 180px mobile, ring couleur primaire opacity 20%.

### 8. TanStack Router — c'est routes/index.tsx qui est servi en production, pas App.tsx

Problème : quand Lovable génère une page React avec TanStack Router, le fichier App.tsx existe mais n'est pas le fichier rendu en production. Le router charge routes/index.tsx. Toute modification appliquée uniquement à App.tsx n'aura aucun effet sur la page déployée.

Solution validée : toujours identifier le fichier réellement servi avant d'appliquer des modifications. Vérifier main.tsx pour savoir s'il charge App directement ou un router. Si un router est présent (router.tsx, routeTree.gen.ts), le fichier à modifier est src/routes/index.tsx. Appliquer systématiquement toutes les modifications de contenu et de médias dans ce fichier.

Règle générale : avant tout commit, vérifier que les modifications sont dans le bon fichier en contrôlant la chaîne main.tsx → router.tsx → routes/index.tsx.

---

## Erreurs à éviter
- Construire le prompt avant que le copy soit entièrement validé
- Mélanger les instructions de texte et de design sans structure claire par section
- Utiliser du jargon technique dans le prompt (ex : « flexbox », « z-index », « padding »)
- Omettre l'instruction de responsive mobile
- Envoyer dans Lovable sans avoir montré le prompt à l'utilisateur pour relecture
- Transmettre un prompt contenant des placeholders de copy non remplis — le meta-auditor le détectera comme un score 0/2 sur le critère de spécificité du prompt Lovable
- Omettre les médias disponibles : si des URLs ont été fournies ou détectées sur la page de référence, elles doivent impérativement apparaître dans le prompt avec les patterns ci-dessus
- Inventer ou deviner des URLs — utiliser uniquement les URLs fournies ou détectées
- Redemander des médias déjà détectés automatiquement sur la page de référence
