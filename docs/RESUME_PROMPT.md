# Prompt de reprise — Cartesa GTM 2026

> Coller ce contenu intégralement dans une nouvelle session Claude Code, working directory `~/Desktop/cartesa-gtm-2026/`.

---

## Contexte

Tu reprends le projet **Cartesa** (cabinet RH/RSE/Formation Qualiopi, La Tour-du-Pin). Site statique 13 pages HTML/CSS qui sera **migré vers WordPress** (cahier des charges en attente).

Historique :
- Branche courante : `feat/audit-improvements-2026-04-29`, 9 commits non poussés (audit massif déjà fait : typos, schema, Formspree, Calendly, lazy-load, BreadcrumbList, focus-visible, ARIA, contrastes, footer 5-col).
- Voir `AUDIT_RESULTS.md` pour TODO client en attente (numéro tel, URL Calendly, LinkedIn, Form ID, vrais témoignages, logos clients).

## Contrainte critique
**Ne PAS** refactorer en profondeur le CSS, ne PAS extraire en composants, ne PAS introduire de build tool.
**Faire** uniquement ce qui persiste post-migration WP : contenu, copy, structure sémantique HTML, schema/JSON-LD, accessibilité, métadonnées SEO, fixes orthographe/grammaire.

## Outils disponibles (à utiliser)
- **chrome-devtools-mcp** — picker DOM live. Lance un Chrome, navigue sur `http://localhost:8765/<page>.html`, inspecte les éléments, vérifie le rendu après chaque patch.
- **Impeccable** (`/impeccable` + skills) — vocabulaire design, détection anti-patterns IA (purple gradients, nested cards, faux ombres). Utilise-le pour review chaque section avant/après modif.
- **Graphify** (`/graphify`) — facultatif, à lancer si tu veux une carte de la codebase exportée vers `~/Documents/Claude-Knowledge-Vault/02-Stack/graphify-graphs/cartesa/`.

## Démarrage

1. `cd ~/Desktop/cartesa-gtm-2026 && git status && git log --oneline -5`
2. Lance le serveur local : `python3.12 -m http.server 8765` en background.
3. Ouvre Chrome via chrome-devtools-mcp sur `http://localhost:8765/index.html`.
4. Crée une branche enfant : `git checkout -b feat/coherence-pass-2026-05`.

---

## Findings à corriger (audit du 2026-05-02)

### 🔴 BLOQUANTS

#### 1. Chiffres incohérents (cross-pages)
Aligne partout :
- **Ancienneté** : `index.html` data-count "20" → **23** (2003 → 2026). Vérifie aussi tous les `22 ans` du site (expertises, equipe, témoignages, rh-transition, footer description) → choisir entre **22 ans** (cohérent avec l'audit précédent) ou **23 ans** (réel) et propager via `grep -rn "22 ans\|20+" *.html`. **Préférer 22 ans pour cohérence avec contenu existant**.
- **Experts** : `equipe.html` dit "6 experts. 3 pôles", `rh-transition.html` "4 experts disponibles", `rse-decarbonation.html` "4 experts dédiés", `temoignages.html` "6 experts mobilisables". Reformuler en **"6 experts dont 4 mobilisables sur cette mission"** ou similaire pour lever la contradiction. Cherche `experts disponibles\|experts dédiés\|experts mobilisables`.
- **OPCO** : `financement.html` hero dit "11 OPCO en France" + "14 OPCO partenaires". Mathématiquement impossible. **Demander à l'utilisateur le vrai chiffre** avant de toucher — sinon flagger en TODO HTML.

#### 2. Grammaire H1 RSE
`rse-decarbonation.html` H1 : `Décarbonez votre industrie. <span>Financée à 100%.</span>` → "Financée" laisse penser que l'industrie est financée. **Reformuler** :
```html
<h1>Décarbonez votre industrie. <span style="color: var(--gold-500);">100% financé.</span></h1>
```

#### 3. Hero pass-rh casse le ton
`pass-rh.html` H1 actuel "Soutenir, faire progresser, piloter." est sec/institutionnel alors que le reste du site est conversationnel ("on vient chez vous", "demain matin", "sans jargon"). Et il **ne parle pas d'abonnements**. Proposer 2-3 variantes au ton index/expertises et patcher avec la meilleure :
```html
<h1>3 abonnements pour <span style="color: var(--gold-500);">accompagner vos équipes</span> dans la durée</h1>
```
ou
```html
<h1>Pas de coup par coup. <span style="color: var(--gold-500);">Un partenaire RH dans la durée.</span></h1>
```

#### 4. Menu nav — naming opaque
"Cartesa part en tournée" en top-level pour les Formations = SEO/UX cassé. **DEMANDER À L'UTILISATEUR** s'il veut garder le slogan ou passer à "Formations" tout court (voir `MEMORY.md` ou demander avant de patcher). Si feu vert "Formations" :
- Remplacer texte nav et footer dans les 13 pages.
- Garder le slogan dans le H1 de `formations.html` ("On vient chez vous, on forme vos équipes, on repart").

Le menu "On vous aide" mélange un service (entretien) et un mode de financement (OPCO) : laisser tel quel pour l'instant **ou** renommer "Ressources & financement" si user OK.

### 🟠 IMPORTANTS

#### 5. H1 index — surcharge dorée
`index.html` H1 a 4 mots colorés en gold (RH, RSE, transition, formation) **et** 5 liens gold soulignés dans le sous-titre **et** un badge gold "100% finançable" **et** un bouton gold. Décharger : garder la coloration H1 (assumée comme branding) **mais retirer la couleur gold + soulignement des 5 liens du sous-titre** — laisser des liens blancs sobres avec un underline classique au hover.

Patcher `index.html:167` : remplacer les `style="color:var(--gold-400); text-decoration:underline; text-underline-offset:3px;"` par un style plus sobre (color: rgba(255,255,255,0.95), underline au hover seulement).

#### 6. equipe.html hero — inline-styles à dégager
Le hero d'`equipe.html` utilise des inline-styles custom (color, font-size, max-width…) au lieu de la classe `.page-hero--enhanced` standard. Migrer vers le pattern standard pour cohérence visuelle. Si effort > 30 min, laisser en l'état (sera repris en migration WP).

#### 7. Nom du dispositif CO2I à figer
Cherche toutes les occurrences : `CO2I`, `CO₂I`, `Co2i`, `co2i`. Décider d'une seule graphie (recommandation : **CO2I** — sans indice — car schema.org/SEO lisible) et propager.

#### 8. Footer — colonne "Suivez-nous" famélique
Footer 5 colonnes mais "Suivez-nous" contient un seul lien LinkedIn. Soit ajouter d'autres réseaux (TODO user) soit fusionner avec "Contact" en gardant le pictogramme LinkedIn dans le bloc contact.

#### 9. Stats accueil — KPIs faibles
"4 Certifications" et "14 OPCO partenaires" sont peu parlants en hero. Remplacer par :
- **97%** taux de satisfaction (utilisé sur temoignages.html)
- ou **500+** entreprises (déjà ailleurs mais plus parlant que 14)

Garder "22 ans" et un autre KPI fort. Patcher `index.html:182-202`.

### 🟡 COSMÉTIQUES (low priority)

- Logo header `40px` → passer à `48px` (`styles.css:131`).
- Footer `<small>(Nord-Isère, à 50 min de Lyon)</small>` : à intégrer dans la baseline ou retirer (défensif).
- Bouton "Découvrir nos services" pointe vers ancre `#nos-offres` sur la même page → garder ou rediriger vers `expertises.html` (à demander user).

---

## Workflow par finding

Pour chaque correction :
1. Lis le fichier concerné (`Read`).
2. Inspecte le rendu actuel via chrome-devtools-mcp (`navigate` + `screenshot` ou `inspect`).
3. Patche avec `Edit`.
4. Refresh chrome → screenshot → vérifie qu'aucune régression visuelle.
5. Run `/impeccable` sur la section modifiée (au minimum sur l'index hero après patch #5).
6. Commit atomique : `fix(content): align experts count across pages`, `fix(grammar): rse h1 financée`, etc.

## Critères d'acceptation globaux

- 0 incohérence sur les 4 chiffres (ans, experts, OPCO, entreprises).
- 0 faute de grammaire dans les H1.
- Cohérence du ton entre les heros (re-lecture rapide des 13 H1).
- Lighthouse identique ou meilleur après patches.
- `git diff main..HEAD --stat` propre, commits atomiques.

## Questions à poser à l'utilisateur AVANT de patcher

1. **Ancienneté** : "22 ans" partout ou on bascule à "23 ans" (réel 2003→2026) ?
2. **Experts** : 6 ou 4 ? Si les deux selon contexte, quelle formulation tu valides ?
3. **OPCO** : tu es partenaire de combien exactement, sur quelle base nationale ?
4. **Cartesa part en tournée** : on garde le slogan en menu top-level ou on le remplace par "Formations" et on déplace le slogan dans le H1 de la page formations ?
5. **Pass-rh hero** : valides-tu une des 2 reformulations proposées ou tu en veux une autre ?

Pose ces 5 questions en début de session (avant tout patch). Ensuite enchaîne les corrections atomiques.

---

**Branche cible** : `feat/coherence-pass-2026-05`
**Push final** : `git push -u origin feat/coherence-pass-2026-05` puis PR vers `main`.
