# Skill : Meta-Auditor

## Rôle
Auditer globalement l'ensemble des outputs produits (copy, offre, design brief, prompt Lovable) avant génération de code — en les comparant aux standards de la réponse directe et aux principes Hormozi. Identifier les blocs faibles, les réécrire directement ou envoyer des instructions correctives aux skills concernés, et valider l'output final avant de passer à git-publish.

---

## Quand l'utiliser
Étape 9b — après que le prompt Lovable a été validé par l'utilisateur (lovable-bridge), avant git-publish et vercel-deploy.

---

## Inputs requis
- Copy complet de la page, section par section (page-copywriting)
- Brief design finalisé (page-design)
- Plan de page validé (page-strategy)
- Positionnement de l'offre validé (offer-positioning)
- Prompt Lovable généré et validé (lovable-bridge)

---

## Grille de scoring (0–2 par critère — total /18 — minimum requis : 15/18)

Évaluer chaque critère de 0 à 2 :
- **0** = absent ou défaillant
- **1** = présent mais faible ou générique
- **2** = fort, spécifique, convaincant

| # | Critère | Description |
|---|---------|-------------|
| 1 | Clarté du hook | Le titre principal accroche immédiatement. On comprend en 3 secondes à qui c'est adressé et ce qu'on obtient. |
| 2 | Intensité de la douleur | Le problème de l'avatar est décrit avec précision émotionnelle, pas de façon générique. |
| 3 | Clarté de l'offre | Ce qui est vendu, le prix, et le résultat sont explicites — sans flou ni jargon. |
| 4 | Présence de la preuve | Témoignages, chiffres, résultats concrets ou mécanisme crédible sont présents et spécifiques. |
| 5 | Force du CTA | Le CTA est unique, impératif, orienté bénéfice — pas générique ("En savoir plus", "Soumettre"). |
| 6 | Absence de flou / ton SaaS générique | Aucune phrase creuse, aucun jargon type "solution innovante", "approche holistique", "plateforme puissante". |
| 7 | Design aligné conversion | Le brief design indique une hiérarchie visuelle claire, un CTA contrasté, une structure épurée orientée action. |
| 8 | Spécificité du prompt Lovable | Le prompt Lovable contient du copy exact (pas de placeholders de copy), des couleurs hex précises, des instructions impératives par section. Pour chaque section portant un asset media (VSL, portrait, photo témoignage) : soit une URL réelle est présente, soit un bloc `[ASSET À REMPLACER]` est explicitement posé — jamais une section media silencieusement absente. |
| 9 | Cohérence globale | L'avatar, l'offre, le copy, le design et le prompt Lovable sont alignés — même cible, même ton, même promesse. |
| 10 *(optionnel)* | Intégration des médias | **Score 2** : tous les médias fournis sont intégrés dans les bonnes sections avec les bons patterns. **Score 1** : médias partiellement intégrés ou mal positionnés. **Score 0** : médias fournis ou détectés mais absents de la page générée. **Ce critère est ignoré (non compté dans le total) si aucun média n'a été fourni ou détecté** — le total reste /18 dans ce cas. |

---

## Méthode

### Phase 1 — Scoring initial

1. Lire l'ensemble des outputs disponibles (copy, offre, design brief, prompt Lovable).
2. Évaluer chaque critère de la grille de scoring.
3. Calculer le score total sur 18.
4. Présenter le tableau de scoring à l'utilisateur avec le score de chaque critère et le total.

### Phase 2 — Décision

**Si score ≥ 15/18 :**
→ Déclarer : "Audit validé — score [X]/18. Les outputs sont conformes aux standards de réponse directe."
→ Passer à git-publish immédiatement.

**Si score < 15/18 :**
→ Identifier les critères dont le score est 0 ou 1.
→ Pour chaque critère faible : préciser le bloc exact qui est défaillant (quelle section, quelle formulation).
→ Appliquer les corrections dans cet ordre de priorité :
  - **Réécriture directe** : si le bloc est isolé (une phrase, un CTA, un titre), réécrire immédiatement sans repasser par le skill d'origine.
  - **Instruction corrective** : si la correction nécessite un travail de fond (refonter l'offre, reconstruire la structure), formuler une instruction précise à renvoyer au skill concerné (offer-positioning, page-copywriting, page-design, lovable-bridge), et relancer ce skill.
→ Après correction, re-scorer uniquement les critères corrigés.
→ Répéter ce cycle jusqu'à un maximum de **3 itérations**.

**Si score < 15/18 après 3 itérations :**
→ Signaler à l'utilisateur les critères bloquants qui n'ont pas pu être corrigés automatiquement.
→ Proposer des corrections manuelles précises.
→ Attendre validation explicite de l'utilisateur avant de continuer.

### Phase 3 — Références externes

Si l'accès internet / recherche est disponible :
→ Rechercher des exemples de pages Hormozi ou de références en réponse directe pour les critères faibles.
→ S'en inspirer pour reformuler les blocs défaillants.

Si l'accès internet n'est pas disponible :
→ Appliquer les principes de réponse directe connus (spécificité, intensité émotionnelle, preuve, urgence, offre irrésistible).
→ Indiquer clairement : "Recherche externe non disponible — corrections basées sur les principes de réponse directe appliqués."

---

## Principes de référence (réponse directe / Hormozi)

Appliquer ces règles lors de toute réécriture :

- **Spécificité > généralité** : "Perdre 8 kg en 6 semaines" bat "perdre du poids rapidement"
- **Résultat concret > processus** : ce que le client obtient, pas ce que tu fais
- **Douleur nommée > douleur suggérée** : nommer la frustration exacte, pas son contour
- **CTA orienté bénéfice** : "Je veux ma place" bat "S'inscrire"
- **Preuve > affirmation** : un chiffre ou un nom bat "des centaines de clients satisfaits"
- **Offre irrésistible** : valeur perçue > prix. Si l'offre paraît raisonnable, elle n'est pas assez forte.
- **Zéro phrase décorative** : chaque phrase doit faire avancer ou convaincre. Sinon, la supprimer.

---

## Output attendu

Rapport d'audit comprenant :
- Tableau de scoring complet (9 critères obligatoires + critère 10 si médias présents, total /18)
- Liste des corrections appliquées (réécriture directe ou instruction corrective)
- Nombre d'itérations effectuées
- Statut final : **Validé (score ≥ 15/18)** ou **Bloqué — corrections manuelles requises**
- Si validé : confirmation explicite de passage à git-publish

---

## Erreurs à éviter
- Valider un output dont le score est inférieur à 15 sans avoir effectué les corrections
- Réécrire sans citer le bloc exact qui est remplacé
- Boucler plus de 3 fois sans alerter l'utilisateur
- Passer à git-publish sans avoir présenté le rapport d'audit à l'utilisateur
- Accepter un prompt Lovable avec des placeholders de copy non remplis (ex : [TITRE PRINCIPAL] encore présent dans le prompt)
- Valider un prompt Lovable dont les sections VSL, portrait ou photos témoignages sont absentes ou vides sans avoir explicitement balisé les emplacements avec `[ASSET À REMPLACER]` — score 0/2 sur le critère 8 si ce cas est détecté
