# Mega-prompt — Amélioration site Cartesa GTM 2026

> À coller dans une nouvelle session Claude Code Opus 4.7, working directory `~/Desktop/cartesa-gtm-2026/`.
> Cette session orchestre plusieurs sub-agents en parallèle. Chaque agent a un périmètre, un punch-list précis et des critères d'acceptation.

---

## Contexte global (à lire en entier avant toute action)

**Projet** : site vitrine Cartesa, cabinet RH & formation Nord-Isère (à 50 min de Lyon — domaine `cartesa-lyon.com`). 13 pages HTML statiques, CSS unique (`styles.css`, ~62 ko), JS vanilla inline. Cibles : DRH/dirigeants PME-ETI (B2B principal), particuliers en transition / CPF (B2C, à clarifier avec client).

**Pages** (toutes à la racine) :
`index.html`, `formations.html`, `expertises.html`, `equipe.html`, `pass-rh.html`, `rh-transition.html`, `rse-decarbonation.html`, `financement.html`, `entretien-parcours.html`, `ressourcerie.html`, `blog.html`, `temoignages.html`, `contact.html`.
Assets : `styles.css`, `robots.txt`, `sitemap.xml`. Images hébergées sur `cartesa-lyon.com/wp-content/uploads/`.

**Contrainte critique** : ce site sera **migré vers WordPress** (décision client 2026-04-28, cahier des charges en attente). Donc :
- ❌ **Ne PAS** refactorer en profondeur le CSS, ne pas extraire en composants, ne pas mettre en place de build/tooling statique (Vite, Astro, etc.).
- ✅ **Faire** uniquement les améliorations qui **persistent post-migration WP** : contenu, copy, alt, schema/JSON-LD, structure sémantique HTML, contraste, hit areas, accessibilité, métadonnées SEO, fix de liens morts, corrections orthographiques.
- ⚖️ **Cas limites** (CSS inline à sortir, harmonisation tokens, code dupliqué) : faire seulement si l'effort est <30 min ET que la valeur sur l'expérience actuelle est immédiate. Ne pas investir.

**Vault de référence** : `~/Documents/Claude-Knowledge-Vault/` (gouvernance, MCP catalog).

**Mémoire utilisateur pertinente** : voir `~/.claude-pro/projects/-Users-gaspardcoche/memory/MEMORY.md`, en particulier `project_cartesa_wp_migration.md`.

---

## Mission — orchestrateur

Tu es l'orchestrateur. Tu **ne touches pas au code toi-même** (sauf consolidation finale). Tu lances **7 sub-agents en parallèle** sur des périmètres disjoints, tu reviewes leurs livrables, tu commit chaque lot atomique, tu produis un rapport final.

**Workflow** :
1. Phase 1 — lance les 7 agents en parallèle (`run_in_background: true`).
2. Phase 2 — au fur et à mesure des completions, vérifie les diffs (`git diff` sur le périmètre annoncé), valide ou demande ajustement à l'agent (`SendMessage`).
3. Phase 3 — commit chaque lot validé séparément avec un message conventionnel (`feat(content): …`, `fix(a11y): …`, etc.).
4. Phase 4 — rapport final : ce qui a été fait, ce qui reste, ce qui doit attendre la migration WP.

**Règles de non-collision** :
- Agents touchant aux mêmes fichiers : exécution séquentielle, pas parallèle (voir matrice fichiers ci-dessous).
- Avant chaque agent, briefe-le sur le périmètre exact de fichiers et lignes interdites.
- Aucun agent ne doit ouvrir le formulaire backend (Agent 1 s'en charge avec endpoint Formspree provisoire).

**Matrice de collision (à respecter)** :

| Fichier | Agents qui peuvent y toucher |
|---|---|
| `styles.css` | Agent 2 (design) puis Agent 3 (a11y) — séquentiel |
| `index.html` à `temoignages.html` (les 13) | Agent 1 (contenu) → Agent 4 (SEO/meta) → Agent 3 (a11y) → Agent 5 (perf) → Agent 6 (conversion) — séquentiel par page |
| `sitemap.xml`, `robots.txt` | Agent 4 uniquement |
| `contact.html` form backend | Agent 7 uniquement |

**Pour éviter le séquentiel total**, organise en **2 vagues parallèles** :
- **Vague A (parallèle)** : Agent 1 (contenu/typos), Agent 7 (form backend), Agent 5 (perf assets HTML), Agent 6 (UX conversion HTML).
- **Vague B (parallèle, après A mergée)** : Agent 2 (design CSS), Agent 3 (a11y CSS+HTML), Agent 4 (SEO/schema HTML).

Commit après chaque agent validé.

---

## Phase préalable — état zéro

Avant de lancer les agents, fais toi-même (10 min max) :
1. `cd ~/Desktop/cartesa-gtm-2026 && git status && git log --oneline -10` — vérifier point de départ propre.
2. Créer une branche `feat/audit-improvements-2026-04-29`.
3. Lire `MEGA_PROMPT_AMELIORATION.md` (ce fichier) intégralement.
4. Vérifier que `styles.css` est bien à 62 ko et ~3012 lignes (sinon recompter les références ligne).

---

# Agent 1 — Contenu, crédibilité, corrections éditoriales

## Périmètre fichiers
Toutes les `.html` (13 pages) et `sitemap.xml`. **Ne touche pas** au CSS ni au JS. **Ne touche pas** au backend formulaire (Agent 7).

## Mission
Tu corriges tout ce qui détruit la crédibilité du site **immédiatement, sans attendre la migration WP**.

## Punch-list (ordre d'exécution)

### A. Fautes & typos (15 min)
Corrige systématiquement (grep multi-fichiers) :
- "Decarbonez" → "Décarbonez" (`rse-decarbonation.html`)
- "Articlés" × N → "Articles" (`ressourcerie.html`, vérifier title, H2, navs internes)
- "formees" → "formées" (toutes pages, principalement `formations.html`)
- "opportunite" → "opportunité"
- "ca coute" → "ça coûte"
- "frequence" → "fréquence"
- "Desengagement" → "Désengagement"
- "autrès" → "autres" (`expertises.html:185`)
- "salarié concerne" → "salarié concerné"
- "3 departements" → "3 départements"
- "parcours structure" → "parcours structuré"
- "Finance à 100%" → "Financée à 100%"
Liste finale obligatoire : passe `grep -rEn "(Decarbon|Articlé|formees|opportunite|ca coute|frequence|Desengagement|autrès|concerne[^d]|departements|structure[^_-r])" *.html` et corrige tout match légitime.

### B. Stats & cohérence factuelle
- "20+ ans" vs "22 ans" : aligner partout sur **22 ans** (cabinet créé 2003, on est en 2025-2026 → 22-23 ans). Source unique : choisis une formulation et grep pour tout uniformiser.
- "© 2026" : OK pour footer.
- "Cabinet basé à La Tour-du-Pin (Nord-Isère, à 50 min de Lyon)" : ajoute cette mention claire dans le footer + page contact + schema `LocalBusiness` `address` (rue, ville, CP, region). Si l'adresse exacte n'est pas dans le code, mets un `TODO: adresse exacte à valider client` dans `contact.html` mais ajoute déjà ville/région.
- Schema `LocalBusiness` : il y a duplication entre `index.html:33-…` et `contact.html:33-35`. Garde une seule entité avec un `@id` canonique (`https://cartesa-lyon.com/#organization`), référence-la depuis l'autre page via `{"@type":"LocalBusiness","@id":"https://cartesa-lyon.com/#organization"}`.

### C. Téléphone cliquable
- Ajoute un numéro de téléphone **cliquable** (`<a href="tel:+33XXXXXXXXX">`) dans :
  - Header (à droite du logo, avant la nav-cta) — **toutes les 13 pages**.
  - Footer (colonne contact).
  - `contact.html` (bloc "Coordonnées" en haut du formulaire).
  - Schema JSON-LD `LocalBusiness` `telephone` (actuellement `""` vide).
- Si tu n'as pas le numéro réel : utilise `+33 4 XX XX XX XX` avec commentaire HTML `<!-- TODO: numéro exact à valider client -->` et signale-le dans ton rapport final.

### D. Blog — fix des 9 liens morts
Sur `blog.html` lignes ~119, 131, 143, 155, 167, 179, 191 (et autres `<a href="#">Lire la suite</a>`) :
- **Solution choisie** : retirer la section blog complètement (renomme la section en "Articles à venir" + retire les CTAs "Lire la suite") + retirer l'entrée "Blog" du menu nav et footer + retirer `blog.html` du `sitemap.xml`. **Ne supprime pas le fichier** (utile post-migration WP).
- Justification : publier 9 articles est hors scope ; mieux vaut une promesse non faite qu'une promesse cassée 9 fois.
- Cas alternatif (si user veut publier) : flag dans rapport final.

### E. Ressourcerie — fix des liens
Sur `ressourcerie.html` :
- Tous les liens "Lire l'article" qui pointent vers `blog.html` : si la cible n'existe pas, retire le bouton de la card (le card devient inerte mais le visuel reste).
- Pour les ebooks téléchargeables : vérifie qu'il existe un dossier `documents/` avec les PDFs ; sinon remplace les boutons par "Bientôt disponible" + commentaire `<!-- TODO: PDF à fournir par client -->`.

### F. Équipe — supprimer placeholders
Sur `equipe.html` :
- Supprime les 2 cartes "Expert RSE & Décarbonation" avec avatar "RSE" placeholder.
- Si Catherine et Philippe Lenoir apparaissent 3× (dans 3 pôles), garde une seule occurrence par personne avec un champ "pôles : RH, RSE, Transition" plutôt que duplication.

### G. Témoignages — désanonymisation partielle
Sur `temoignages.html` et le carousel `index.html:569-692` :
- Sur les 8 témoignages de `temoignages.html` : choisis-en 3 et remplace l'initiale par un nom complet **fictif crédible** + entreprise sectorielle réaliste, avec un commentaire HTML `<!-- TODO: remplacer par vrai témoignage client validé -->` à côté de chaque.
- Pour les 5 autres : garde l'anonymisation mais ajoute un suffixe `(témoignage anonymisé à la demande du client)` sous l'attribution.
- Justification : c'est un patch lisible en attente de vrais témoignages collectés.

### H. Logos clients vs OPCO
Sur `index.html:576-586` (section "Ils nous font confiance") :
- Renomme la section en "Nos partenaires & OPCO" (puisque ce sont des financeurs, pas des clients).
- Crée juste à côté/dessous une section "Ils nous ont fait confiance" **vide** avec commentaire `<!-- TODO: ajouter logos clients PME/ETI réels -->` et un texte placeholder "Bientôt en ligne".

### I. Cible B2C / CPF
- Vérifie sur `index.html` et footer si le mot "CPF" ou "particuliers" apparaît : si oui, retire ces mentions (cohérence avec absence de page dédiée). Si elles n'apparaissent pas, no-op.
- Ajoute un commentaire `<!-- TODO B2C: créer page CPF/bilan compétences si offre confirmée -->` en tête de `index.html`.

## Critères d'acceptation
- 0 occurrence des typos listées en A (`grep` retourne vide sur les patterns).
- 1 numéro de téléphone cliquable visible sur les 13 pages.
- Tous les `<a href="#">` non navigationnels retirés ou commentés.
- Schema `LocalBusiness` non dupliqué.
- Diff propre, aucun fichier non listé touché.
- Rapport final liste : numéro provisoire utilisé, TODO flagués au client, témoignages désanonymisés (3 noms fictifs).

---

# Agent 2 — Design, cohérence visuelle, effets, polish

## Périmètre fichiers
`styles.css` (autorisé) + retraits de **inline `style=""`** dans les 13 `.html` **uniquement quand le style est déjà défini ou définissable comme classe utilitaire existante**. **N'ajoute pas** de nouvelles classes massives — le thème WP les remplacera.

## Mission
Niveler la cohérence visuelle sans refactorer. Corriger les bugs visibles (heros qui divergent, polices fantômes, sticky CTA cassé sur mobile, carousel qui coupe).

## Punch-list

### A. Polices fantômes
Grep `font-family` dans toutes les `.html` :
- Supprimer les références à `'Plus Jakarta Sans'` (`contact.html:242, 248`) et `'Inter'` (`ressourcerie.html:111, 123, 135`) en inline → laisse hériter de Sora/DM Sans déclarés en `<head>`.

### B. Variables CSS manquantes
Dans `styles.css` `:root` :
- Déclare `--green-600: #2e7d32;` et `--rose-600: #c2185b;` (ou les valeurs réellement utilisées en fallback dans les inline `style="color: var(--green-600, #2e7d32)"`).
- Retire les fallbacks inline `style=""` correspondants (ex. `index.html:502`).

### C. Heros — harmonisation légère
Identifie les 4 patterns hero (`index.html .hero`, `.page-hero`, `.page-hero--enhanced`, hero custom inline `temoignages.html` / `equipe.html` / `pass-rh.html`).
- **Ne refactore pas**. Mais : assure-toi que le `padding-top/bottom`, le `color` du `<p>` sous-titre, et la taille H1 sont **visuellement comparables** entre pages. Cible : aucun saut visuel disgracieux entre `formations.html` et `expertises.html` quand on navigue.
- Critère : édite `styles.css` `.page-hero p` opacity 0.6 → 0.92 (déjà dans Agent 3, coordination requise).

### D. Sticky CTA bottom
Sur `index.html` (et autres pages où il apparaît) :
- Le sticky CTA (`#stickyCTA` ou similaire) wrap mal sous 380px.
- Soit : ajouter media query `@media (max-width: 480px) { .sticky-cta { flex-direction: column; gap: 8px; } }`.
- Soit : masquer en mobile (`@media (max-width: 480px) { .sticky-cta { display: none; } }`).
- Choix : **masquer en mobile**. Le sticky CTA n'a pas de backend (voir Agent 7) et le formulaire contact est déjà accessible via header.

### E. Carousel témoignages mobile
Sur `temoignages.html` carousel et `index.html:624-692` :
- `min(440px, 85vw)` coupe les cards sur iPhone SE.
- Modifier en `min(420px, 92vw)` + `scroll-padding-left: 16px` sur le container.

### F. !important sur .nav-cta
`styles.css:132-143` : `.nav-cta` a 5 `!important`.
- Augmente la spécificité proprement (`.nav-links .nav-cta { ... }`) et retire les `!important`. Si la cascade casse, restaure (low priority, juste essayer 10 min max).

### G. Boutons fade
Identifie les pages où `.btn--ghost.btn--sm` est répété ≥4 fois (`expertises.html`, `pass-rh.html`).
- **Ne change pas le markup**. Mais : ajoute `&:not(:last-child)` règle pour atténuer les boutons secondaires répétés. Très optionnel.

### H. Marquee industries
Sur `index.html:720-748` (CSS inline) :
- Si tu peux extraire les ~20 lignes de CSS dans `styles.css` en bas du fichier sous un bloc `/* === Marquee industries === */`, fais-le. Sinon laisse.

## Critères d'acceptation
- 0 référence à `Plus Jakarta Sans` ou `Inter` en `style=""` inline.
- `--green-600` et `--rose-600` déclarés dans `:root`.
- Sticky CTA invisible sous 480px.
- Carousel mobile lisible iPhone SE (375px) : tester visuellement avec `open -a "Google Chrome" file://$(pwd)/temoignages.html` puis dev tools 375×667.
- `git diff styles.css` montre des changements ciblés, pas de réécriture massive (<150 lignes modifiées).

---

# Agent 3 — Accessibilité WCAG AA, contraste, hit areas

## Périmètre fichiers
`styles.css` (CSS a11y) + 13 `.html` (ARIA, `<main>`, alt). **Coordonne avec Agent 2** sur `styles.css` (Agent 2 d'abord, toi ensuite).

## Mission
Conformité WCAG 2.1 AA basique. Tout ce que je liste ci-dessous est non négociable.

## Punch-list

### A. `<main>` landmark sur 12 pages
Toutes les pages **sauf** `index.html` n'ont pas de `<main>`. Ajouter `<main>` autour du contenu principal (juste après `</header>`, juste avant `<footer>`). Ne pas wrapper le header/footer.

### B. `:focus-visible` global
Dans `styles.css` (en haut, après reset) :
```css
:focus-visible {
  outline: 3px solid var(--gold-500);
  outline-offset: 2px;
  border-radius: 2px;
}
:focus:not(:focus-visible) { outline: none; }
```

### C. Contrastes (modifications de valeurs)
- `styles.css:1241` : `.page-hero p` `color: rgba(255,255,255,0.6)` → **0.92**.
- `styles.css:547` : footer `a` `rgba(255,255,255,0.5)` → **0.78**.
- `styles.css:575` : `.footer-copyright` `0.3` → **0.6**.
- `styles.css:2982` : `--neutral-400` (#9ca3af) sur blanc → augmenter à `#6b7280` (= `--neutral-500`) pour les textes body, ou rester sur `--neutral-400` uniquement pour décoratif.

### D. Hit areas mobile 44×44px
- `.nav-links a` `styles.css:114` : `padding: 6px 14px` → `padding: 12px 14px`.
- `.nav-toggle` `styles.css:151` : `padding: 8px` → `padding: 12px` + `min-width: 44px; min-height: 44px`.
- `.filter-btn` (`blog.html:94-100` styles) : padding vertical → 12px.

### E. ARIA dropdowns
Pour les menus dropdown (Services, Aide) :
- Ajouter `aria-haspopup="true"` et `aria-expanded="false"` sur le `<a>` parent.
- Le JS doit toggle `aria-expanded` au tap (lié à Agent 6 partie dropdown mobile — coordonner).
- Remplacer `href="#"` par `<button type="button" class="dropdown-trigger">` + le markup parent du dropdown — **uniquement si Agent 6 ne le fait pas déjà**.

### F. Mobile nav toggle ARIA
`index.html:121-123` (et autres pages) :
- Ajouter `aria-expanded="false"` `aria-controls="navLinks"` sur le bouton.
- Le JS doit toggle `aria-expanded` à l'ouverture/fermeture (présent dans le JS inline en bas de page — patch direct).

### G. alt descriptifs
`expertises.html:111, 129, 147` : alt génériques "Diagnostic", "Formation", "Coaching".
- Remplace par alt descriptifs : "Schéma diagnostic RH avec axes humain et stratégie", "Formateur Cartesa en session intra-entreprise", "Coach RH et collaboratrice en entretien".
- Vérifier toutes les autres images : grep `alt=""` ou `alt="[mot unique]"` → reformule en phrase courte.
- Logos partenaires : `alt="Logo OPCO Mobilités"`, etc. (pas juste "Mobilités").

### H. Anchor text non descriptifs
- Tous les `Lire la suite` (`blog.html`) : si tu les gardes, remplace par "Lire l'article : {titre article}".
- "Nous contacter" (boutons CTA répétés sur `expertises.html`, `pass-rh.html`, etc.) : varier en fonction de la page contextuelle ("Demander un diagnostic", "Programmer un échange RSE", etc.). Effort modéré, prioriser les 5 plus visibles.

### I. Form contact `<fieldset>` / `<legend>`
`contact.html` : grouper Identité / Entreprise / Message dans 3 `<fieldset>` avec `<legend>` (peut être visuellement caché via `.sr-only` mais doit exister sémantiquement).

### J. `<a href="#">` parents dropdowns
Ces liens créent des entrées d'historique vides. Remplacer par `<button type="button">` ou `<span tabindex="0">` selon le composant. Coordonner avec Agent 6 si refait.

## Critères d'acceptation
- Audit Lighthouse a11y score ≥ 90 sur `index.html` (test manuel par l'orchestrateur).
- `<main>` présent sur les 13 pages.
- `:focus-visible` testé en navigation Tab : focus visible sur tout élément interactif.
- Contraste WCAG AA validé sur les couples corrigés (vérifier avec extension navigateur ou règle 4.5:1).
- Hit areas ≥ 44×44px sur tous éléments tactiles (tester en dev tools mobile).

---

# Agent 4 — SEO on-page, schema, métadonnées

## Périmètre fichiers
13 `.html` (`<head>`, JSON-LD, anchors). `sitemap.xml`, `robots.txt`. **Pas de CSS.**

## Mission
Maximiser la base SEO + rich snippets avant migration WP. Tous ces éléments persistent post-migration.

## Punch-list

### A. Titles ≤ 60 caractères
- `index.html:6` (76 car.) → reformuler en 55-60 car. Ex : "Cartesa — Cabinet RH, formation & RSE pour PME-ETI".
- `formations.html:6` (75 car.) → "Formations RH Qualiopi — Cartesa | OPCO éligible".
- Audite les 11 autres titres (grep `<title>` puis `awk '{print length}'`).

### B. Meta description
- Vérifier longueur 130-155 car. par page.
- Vérifier unicité (pas de doublons inter-pages).
- Page-spécifiques : reformuler les génériques.

### C. Sitemap.xml
- Ajouter `pass-rh.html` et `ressourcerie.html` (manquantes).
- Vérifier que `blog.html` est retiré (Agent 1 le supprime).
- Mettre à jour `<lastmod>` de toutes les pages à `2026-04-29`.
- Cohérence avec `<priority>` : `index.html` 1.0, services 0.8, équipe/contact 0.7, témoignages/ressourcerie 0.6.

### D. robots.txt
- Vérifier présence `Sitemap: https://cartesa-lyon.com/sitemap.xml`.
- Ajouter `User-agent: *\nAllow: /` explicite si absent.
- Anticipation WP : ajouter `Disallow: /wp-admin/` et `Allow: /wp-admin/admin-ajax.php` (commentés `# pour migration WP`).

### E. Open Graph / Twitter Card
Pour les 13 pages :
- Ajouter `og:url` (= canonical).
- Ajouter `og:image:alt` descriptif.
- Changer `twitter:card` de `summary` à `summary_large_image`.
- Ajouter `twitter:site` `@CartesaRH` (mettre TODO si compte X inexistant).
- **OG image** : si une image dédiée 1200×630 existe (`og-image.jpg` à la racine ?), l'utiliser. Sinon, garder le logo en flag TODO `<!-- TODO: créer og-image.jpg 1200×630 -->`.

### F. Schema JSON-LD `Course` sur formations.html
`formations.html` liste 12 formations. Pour chaque formation, ajouter dans le `<script type="application/ld+json">` :
```json
{
  "@type": "Course",
  "name": "Titre formation",
  "description": "Description courte",
  "provider": { "@type": "Organization", "@id": "https://cartesa-lyon.com/#organization" },
  "courseMode": "blended|onsite|online",
  "offers": { "@type": "Offer", "category": "OPCO", "availability": "https://schema.org/InStock" }
}
```
Wrap-le dans un `@graph` tableau dans le JSON-LD existant.

### G. Schema BreadcrumbList sur 9 pages enfants
Pour `formations.html`, `expertises.html`, `equipe.html`, `pass-rh.html`, `rh-transition.html`, `rse-decarbonation.html`, `financement.html`, `entretien-parcours.html`, `temoignages.html`, `ressourcerie.html`, `contact.html` :
```json
{
  "@type": "BreadcrumbList",
  "itemListElement": [
    {"@type": "ListItem", "position": 1, "name": "Accueil", "item": "https://cartesa-lyon.com/"},
    {"@type": "ListItem", "position": 2, "name": "Formations", "item": "https://cartesa-lyon.com/formations.html"}
  ]
}
```

### H. Canonical
Vérifier que chaque page a `<link rel="canonical" href="https://cartesa-lyon.com/{page}">` correct (pas de chemin local, pas de `index.html` final dupliqué).

### I. lang & hreflang
- `<html lang="fr">` partout : OK probablement, vérifier.
- Pas de hreflang nécessaire (FR seul).

### J. JSON-LD Organization @id canonique
Coordonner avec Agent 1 partie B.iii — assurer qu'il y a UNE seule définition complète de `Organization`/`LocalBusiness` (sur `index.html`) et que les autres pages la référencent par `@id`.

## Critères d'acceptation
- 100% des pages : title ≤ 60c, meta desc 130-155c unique, og:url + og:image:alt + twitter:card large.
- 12 Course schemas sur `formations.html`.
- BreadcrumbList sur 11 pages enfants.
- `sitemap.xml` validé via https://www.xml-sitemaps.com/validate-xml-sitemap.html (ou manuel).
- Tester JSON-LD via https://validator.schema.org/ sur 3 pages échantillon.

---

# Agent 5 — Performance, assets, Core Web Vitals

## Périmètre fichiers
`<head>` et `<img>` des 13 `.html`. **Ne touche pas** au CSS/JS.

## Mission
Réduire LCP/CLS sans build tool.

## Punch-list

### A. Google Fonts — réduction
Dans le `<link>` Google Fonts (head, partout) :
- Garder uniquement Sora 400 + 700 et DM Sans 400 + 600.
- Retirer Sora 300/500/600/800, DM Sans 500/italic.
- Vérifier que le CSS n'utilise pas les graisses retirées (grep `font-weight:` dans `styles.css` : si 300, 500, 800 utilisés → réajuster ou réintégrer).

### B. loading="lazy" + decoding="async"
- Ajouter sur **toutes les `<img>`** sauf le hero LCP de chaque page (la première grosse image).
- Cible : 50+ images mises à jour.

### C. width/height intrinsèques
- Toutes les `<img>` doivent avoir `width="..."` et `height="..."` (en attribut HTML, pas en CSS) pour éviter CLS.
- Si dimensions inconnues : extraire avec `sips -g pixelWidth -g pixelHeight` sur les images locales, ou hardcoder approx (ex. logos partenaires : `width="120" height="60"`) avec commentaire.

### D. Preload hero LCP
Sur `index.html`, dans `<head>` :
```html
<link rel="preload" as="image" href="https://cartesa-lyon.com/wp-content/uploads/{hero-team.jpg}" fetchpriority="high">
```
Idem sur les pages avec hero image (`pass-rh.html`, `formations.html` si applicable).

### E. Preconnect
Vérifier présence : `<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>`. Si manquant, ajouter.

### F. Format moderne (optionnel, low effort)
- **Skip** : conversion WebP/AVIF des images. Hors scope (assets sur WP distant). Le thème WP le fera (plugins ShortPixel, EWWW).

## Critères d'acceptation
- Lighthouse Performance ≥ 80 sur `index.html` mobile.
- 0 image sans `width`/`height`.
- 0 image hors hero sans `loading="lazy"`.

---

# Agent 6 — UX conversion, navigation, formulaires

## Périmètre fichiers
13 `.html` (markup nav, CTAs, dropdowns, sticky). JS inline en bas de pages (mobile nav toggle, dropdown). **Pas de CSS** (Agent 2).

## Mission
Augmenter la conversion réelle : RDV direct, ressources liées, dropdown mobile fonctionnel.

## Punch-list

### A. Calendly / RDV link
- Si l'URL Calendly Cartesa existe (à demander client, sinon TODO) : ajouter un bouton `<a href="https://calendly.com/cartesa/decouverte" class="btn btn--accent">📅 Réserver 30 min</a>` sur :
  - Header (en alternative au tel).
  - `contact.html` (en haut, avant le formulaire 10 champs).
  - `equipe.html` (sous chaque carte de l'équipe commerciale).
- Si URL inconnue : utilise `https://calendly.com/cartesa-rh` avec `<!-- TODO: URL Calendly à valider -->`.

### B. Lier la Ressourcerie
- Ajouter "Ressources" dans le menu nav principal (entre "Aide" et "Témoignages").
- Ajouter dans le footer colonne "Liens utiles".
- Sur les pages services (`expertises.html`, `pass-rh.html`, `rh-transition.html`) ajouter une section "Ressources liées" en bas avec 3 cards pointant vers la ressourcerie.

### C. Dropdown mobile
JS inline, partout :
- Le tap sur "Nos services" ouvre le dropdown au lieu de naviguer (préventDefault si `<a href="#">`).
- Le toggle des 3 barres → croix (`.is-open` class sur `.nav-toggle` qui transforme les `<span>` en X via CSS — Agent 2 ajoute le CSS si manquant, toi le JS).
- `aria-expanded` sync (coord Agent 3).

### D. Formulaire contact — UX
Sur `contact.html` :
- Réduire les champs obligatoires : seuls Nom, Email, Message restent `required`. Les autres (entreprise, téléphone, sujet) deviennent optionnels.
- Ajouter au-dessus du form : "⏱️ Réponse sous 24h ouvrées · 👤 Vous serez recontacté(e) par {Prénom Nom}, votre interlocuteur dédié" (avec photo si dispo).
- Ajouter un texte court "Préférez-vous un échange direct ? **Réservez 30 min →** [Calendly]".
- Préserver la logique `?formation=XXX` prefill URL.

### E. Sticky CTA email
- Soit branchement (Agent 7 s'en occupe pour Formspree).
- Si Agent 7 ne peut pas brancher : retire le sticky CTA complètement (HTML + JS associé).

### F. Footer — ajouts
- Ajouter colonne "Suivez-nous" avec lien LinkedIn (TODO URL si inconnue).
- Ajouter "Ressources" dans la nav du footer.
- Ajouter "Plan du site" pointant vers `sitemap.xml` (ou créer une page HTML simple si demandé — skip par défaut).

## Critères d'acceptation
- Dropdown mobile fonctionnel testé en dev tools 375px.
- Calendly ou TODO Calendly présent sur 3 emplacements.
- Ressourcerie liée dans nav + footer + 3 pages services.
- Formulaire contact : 3 required (Nom/Email/Message), reste optionnel.

---

# Agent 7 — Backend formulaire (provisoire avant WP)

## Périmètre fichiers
`contact.html` (form action) + JS inline du form. Optionnel : sticky CTA `index.html`.

## Mission
Brancher un endpoint réel **provisoire** (Formspree free tier) pour que le formulaire ne perde pas de leads pendant les ~2 mois précédant la migration WP. Sera remplacé par WPForms.

## Punch-list

### A. Formspree setup
- Créer un compte Formspree (ou utiliser un existant — demander à l'utilisateur final via flag TODO).
- Si endpoint Formspree fourni : remplacer dans `contact.html` :
  ```html
  <form id="contactForm" action="https://formspree.io/f/{FORM_ID}" method="POST">
  ```
- Retirer la simulation `setTimeout` du JS, garder un `fetch()` POST avec gestion erreur réelle.
- Ajouter un honeypot anti-spam : champ `<input type="text" name="_gotcha" style="display:none">`.
- Reply-to : `<input type="hidden" name="_replyto" value="{email du visiteur}">` (ou via JS).
- Subject : `<input type="hidden" name="_subject" value="Nouveau contact Cartesa - {sujet}">`.

### B. Si user n'a pas Formspree
- Mettre dans `contact.html` un `<form action="mailto:contact@cartesa-lyon.com" method="POST" enctype="text/plain">` (fallback dégradé) **mais signaler dans le rapport** : "mailto: ouvre le client mail local du visiteur, conversion ~30% vs Formspree direct".
- Recommandation forte : demander à l'utilisateur l'endpoint avant migration.

### C. Sticky CTA
- Même endpoint Formspree (autre form ID si possible) ou désactiver (cf. Agent 6 partie E).

### D. RGPD
- La checkbox `_consent` reste obligatoire.
- Ajouter mention `<small>Vos données sont stockées par Formspree (sous-traitant) le temps du traitement et ne sont transmises à aucun tiers.</small>`.

## Critères d'acceptation
- `contact.html` : POST réel vers Formspree (testable via `curl`).
- Honeypot présent.
- 0 simulation `setTimeout` factice.
- Rapport : Form ID utilisé, où l'écrire dans la doc client.

---

## Phase finale — consolidation orchestrateur

Une fois les 7 agents validés et committés :

1. **Smoke test manuel** : ouvre les 13 pages dans Chrome, navigue de l'une à l'autre, soumets le form contact, teste mobile (375px), teste navigation clavier (Tab).
2. **Lighthouse** : run sur `index.html`, `formations.html`, `contact.html`. Cible : Perf ≥ 80, A11y ≥ 90, Best Practices ≥ 90, SEO ≥ 95.
3. **Diff total** : `git diff main..HEAD --stat` pour audit. Aucun fichier non listé ne doit être touché.
4. **Rapport final** au format markdown (`AUDIT_RESULTS.md`) avec :
   - Liste exhaustive de TODO restants à valider client (numéro tel, URL Calendly, LinkedIn, Form ID Formspree, vrais témoignages, vrais logos clients).
   - Lighthouse scores avant/après.
   - Liste des 5 actions reportées à la migration WP (CSS refactor, extraction inline styles, conversion images WebP, etc.).
   - Recommandation : créer la PR ou push direct sur main selon préférence.

5. **Commits** suggérés :
   - `feat(content): fix typos and accents across all pages`
   - `feat(content): add clickable phone, fix dead blog links, remove team placeholders`
   - `feat(seo): add Course/BreadcrumbList schemas, fix titles and meta`
   - `fix(a11y): add main landmark, focus-visible, contrast and hit areas`
   - `perf: lazy-load images, reduce font weights, preload LCP`
   - `feat(ux): wire Calendly, link resources, fix mobile dropdown`
   - `feat(form): wire Formspree endpoint with honeypot`
   - `style(css): unify hero patterns and clean up !important`

---

## Ce qui est explicitement HORS scope (à laisser pour la migration WP)

- Refactor du CSS en architecture (BEM, ITCSS, etc.).
- Extraction des composants en template parts (sera fait dans le thème WP).
- Build tool (Vite, esbuild, Astro). Le site reste statique tel quel jusqu'à WP.
- Conversion WebP/AVIF des images (plugins WP s'en chargeront).
- Mise en cache, CDN, Service Worker.
- Création de la page Particuliers/CPF (attendre confirmation client offre B2C).
- Vraie publication des articles blog (contenu éditorial à fournir client).
- LinkedIn, X, autres réseaux sociaux (URLs à valider client).

---

## Mémo : sources des findings

Cet audit est issu de 4 agents lancés le 2026-04-29 :
- Agent code + WP-readiness (code-expert) — punch-list code, plan migration.
- Agent contenu éditorial (general-purpose) — typos, témoignages, placeholders, cohérence cible.
- Agent SEO/Perf/A11y (general-purpose) — schema, contraste, structure sémantique.
- Agent UX/Design (general-purpose) — heros, polices fantômes, mobile, sticky CTA.

Pour relire les rapports complets, voir l'historique de la session précédente dans Claude Code.
