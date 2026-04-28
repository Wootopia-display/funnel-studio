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

"As-tu des vidéos de témoignages clients à intégrer ? (YouTube, Vimeo, ou autre). Ce sont les vidéos où tes clients parlent de leur transformation — c'est la preuve sociale la plus puissante de ta page. Si oui, donne-moi les URLs une par une. Si non, on continue sans."

"À quelle seconde veux-tu que la prévisualisation de ta vidéo démarre ? C'est l'image fixe visible avant que le visiteur appuie play. Ouvre ta vidéo, trouve le moment le plus valorisant et note la seconde exacte. Si tu ne sais pas, laisse vide et on utilisera la valeur par défaut."

"La miniature affichée par défaut est-elle valorisante ? Si non, demander au client de la modifier directement dans Vimeo ou YouTube avant de générer la page — aucun paramètre d'URL ne peut remplacer ce réglage."

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
   Pour la VSL, appliquer la règle de position selon la température du trafic stockée dans le brief projet :
   - Trafic froid : "Ajoute la section vidéo immédiatement après le hero, avant toute section texte. Ajouter un label court au-dessus de l'iframe ('Regarde comment [PROGRAMME] transforme [CIBLE]')."
   - Trafic chaud : "Ajoute la section vidéo après la section mécanisme/pivot, avec une phrase de transition ('Voici comment [CIBLE] ont vécu la transformation')."
   - Si la température du trafic n'a pas été collectée → appliquer par défaut la règle trafic froid (position 2).
5. Ajouter en fin de prompt une instruction globale de responsive mobile : « Toutes les sections doivent s'afficher correctement sur mobile, texte lisible, bouton visible sans scroller. »
6. Présenter le prompt complet à l'utilisateur pour relecture avant envoi dans Lovable.
7. Une fois validé, indiquer à l'utilisateur comment coller le prompt dans Lovable et lancer la génération.

**Vérification obligatoire avant de finaliser le prompt :**
- Aucun prix (€, montant chiffré) n'apparaît avant la section Offre
- La VSL est positionnée après le mécanisme (section 7), pas dans les 3 premières sections
- Tous les CTA early sont sans prix

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

**Vidéos témoignages — dans la section transformation, après les photos et avant les cartes texte :**
"Crée une grille de vidéos témoignages. Chaque vidéo est dans un wrapper ratio 16:9 (aspect-video). Grille 1 colonne mobile, 2 colonnes tablette, 3 colonnes desktop. Chaque cellule : overflow hidden, border-radius 16px, ombre légère, ring 1px border. L'iframe remplit entièrement la cellule (w-full h-full). Attributs obligatoires : allow='fullscreen; picture-in-picture' allowfullscreen loading='lazy'. Jamais d'autoplay.
- YouTube : transformer https://www.youtube.com/watch?v=VIDEO_ID&t=Xs en https://www.youtube.com/embed/VIDEO_ID?start=X
- Vimeo : transformer https://vimeo.com/VIDEO_ID/TOKEN en https://player.vimeo.com/video/VIDEO_ID?h=TOKEN
- Appliquer le timestamp de preview si fourni (#t=Xs pour Vimeo, &start=X pour YouTube)
- Si aucune vidéo témoignage fournie : ne pas créer de section vide, laisser uniquement les cartes texte"

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
Exemple : https://vimeo.com/VIDEOID/TOKEN → https://player.vimeo.com/video/VIDEOID?h=TOKEN

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

### 9. Vercel non connecté au repo GitHub — l'auto-deploy ne se déclenche pas

Problème : par défaut, un projet Vercel créé via CLI n'est pas connecté au repo GitHub. Les git push ne déclenchent aucun déploiement automatique. La page en production reste sur l'ancien commit indéfiniment.

Symptôme : la page publiée ne reflète pas les dernières modifications malgré un push confirmé sur main.

Solution validée : connecter le repo GitHub au projet Vercel une seule fois depuis l'interface : vercel.com → projet → Settings → Git Repository → Connect Git Repository → sélectionner le repo → branche main. Une fois connecté, chaque push sur main déclenche automatiquement un déploiement production.

Solution de secours si la connexion GitHub n'est pas encore faite : builder localement (npm run build) puis déployer via CLI : npx vercel deploy --prod --token [VERCEL_TOKEN] --yes

### 10. Prix affiché trop tôt — destruction de la conversion

Problème : le prix apparaît dans le hero ou dans un CTA early avant que la valeur soit perçue. Le visiteur voit le prix avant de comprendre le mécanisme ou de voir la preuve. Il part.

Solution validée : le prix n'apparaît qu'une seule fois, dans la section Offre (étape 10 de la structure). Tous les CTA avant cette section sont sans prix. Vérifier systématiquement que le mot "€" ou tout montant chiffré n'apparaît pas avant la section Offre.

### 11. VSL positionnée above the fold — erreur critique

Problème : la VSL placée juste après le hero est vue avant que le visiteur soit engagé émotionnellement. Sans tension préalable, le taux de consommation de la vidéo s'effondre.

Solution validée : la VSL se place après la section "Nouvelle vision / mécanisme" (étape 7 de la structure). Avant elle, ajouter une phrase de transition qui crée l'anticipation. Ne jamais mettre la VSL en autoplay.

### 13. Vidéos témoignages ignorées — perte de preuve sociale critique
Problème : lors de la collecte des médias, les vidéos de témoignages sont systématiquement oubliées car on se concentre sur la VSL et les images. Or ce sont les éléments de preuve sociale les plus puissants — un vrai client qui parle de sa transformation convertit bien mieux qu'un texte.
Solution validée : demander explicitement les vidéos témoignages comme étape séparée, indépendante de la VSL. Si le client a une page de référence, détecter automatiquement toutes les iframes vidéo présentes hors VSL — ce sont probablement des témoignages. Les vidéos chargées dynamiquement (Systeme.io, etc.) ne sont pas récupérables par fetch statique : demander au client d'inspecter sa page (Chrome → clic droit sur chaque vidéo → Inspecter → chercher src de l'iframe) et de fournir les URLs une par une. L'URL Vimeo peut contenir un long token Turnstile — seul le paramètre h=TOKEN est nécessaire pour l'embed.

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
- Positionner la VSL par défaut au centre de la page sans avoir déterminé si l'audience est froide ou chaude. La position de la VSL change selon la température du trafic — trafic froid = position 2 (après hero), trafic chaud = position 4-5 (après mécanisme/pivot)
- Ne jamais utiliser le paramètre #t=Xs (Vimeo) ou &start=X (YouTube) pour tenter de modifier la miniature affichée avant le play — ces paramètres contrôlent uniquement le point de départ de la lecture, pas la thumbnail. Effet indésirable : la vidéo démarre à X secondes quand le visiteur appuie sur play, ce qui coupe le début du message. Pour changer la miniature d'une vidéo Vimeo : aller dans Vimeo → Settings → Thumbnail → Select from video → choisir la seconde souhaitée → sauvegarder. L'embed se met à jour automatiquement sans toucher au code.
