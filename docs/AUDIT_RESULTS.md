# Audit & améliorations Cartesa GTM 2026 — Rapport final

**Branche** : `feat/audit-improvements-2026-04-29`
**Date** : 2026-04-29
**Commits** : 7 (vague A : 4, vague B : 3)
**Périmètre** : 13 pages HTML + styles.css + sitemap.xml + robots.txt
**Lignes modifiées** : ~1 536 insertions / 815 suppressions sur 16 fichiers

---

## Commits (par couche)

| # | Hash | Lot | Fichiers |
|---|------|-----|----------|
| 1 | `c5316c4` | `feat(content)` typos, téléphone cliquable, schema dédupliqué, blog neutralisé | 14 |
| 2 | `fbfdee3` | `feat(form)` Formspree + honeypot + RGPD | 1 |
| 3 | `ceb8acf` | `perf` lazy-load 86 imgs, fonts trimmés, preload LCP | 13 |
| 4 | `37eac5c` | `feat(ux)` Calendly, ressourcerie, dropdown mobile JS, form simplifié | 13 |
| 5 | `6c573c4` | `feat(seo)` titles ≤ 60c, BreadcrumbList, Course schemas, OG | 15 |
| 6 | `923e0d7` | `style(css)` tokens, dropdown mobile CSS, footer 5-col | 5 |
| 7 | `88f7193` | `fix(a11y)` main, focus-visible, ARIA, contrastes, hit areas | 14 |

---

## TODO restants — à valider client

| Item | Où | Action attendue |
|---|---|---|
| Numéro de téléphone réel | header + footer + contact + schema (13 pages) | Remplacer `+33 4 74 00 00 00` par le vrai numéro |
| Adresse exacte | `contact.html` + schema | Confirmer le `36 avenue Alsace Lorraine, 38110 La Tour-du-Pin` |
| Form ID Formspree | `contact.html:131` | Créer compte Formspree free, remplacer `xpwagzrj` par le vrai ID |
| URL Calendly | header (13 pages) + `contact.html` + `equipe.html` | Remplacer `https://calendly.com/cartesa-rh` par la vraie URL |
| URL LinkedIn | footer 5e col (13 pages) | Remplacer `#` par la vraie URL LinkedIn page entreprise |
| Handle X / Twitter | meta `twitter:site` (13 pages) | Confirmer ou retirer `@CartesaRH` |
| og-image.jpg 1200×630 | meta `og:image` (13 pages) | Créer une image OG dédiée (sinon fallback logo en place) |
| 6 vrais témoignages | 3 sur `temoignages.html` + 3 sur `index.html` | Remplacer Sophie Martin / Laurent Bernard / Marc Faure (noms fictifs) par de vrais témoignages collectés |
| Logos clients réels | section vide `index.html` | Ajouter logos PME/ETI clients + autorisations |
| Profils Experts RSE | `equipe.html` + `rse-decarbonation.html` | Cartes placeholders RSE retirées, à remplacer quand recrutement OK |
| Articles blog | `blog.html` neutralisé | Publier ≥ 9 articles avant de re-référencer (post-migration WP) |
| Page CPF / B2C | comment en tête `index.html` | Confirmer si offre B2C → créer page dédiée |
| PDFs ressourcerie | dossier `documents/` (cards inertes) | Fournir les PDFs téléchargeables |

**Nombre total de TODO inscrits dans le code** : 87 occurrences (12 catégories uniques).

---

## Smoke tests passés

- ✅ HTML valide sur 13/13 pages (parser standard, 0 erreur).
- ✅ JSON-LD valide sur échantillon (index, formations, contact, équipe, témoignages).
- ✅ `<main>` landmark sur 13/13 pages.
- ✅ Téléphone cliquable sur 13/13 pages.
- ✅ ARIA dropdowns sur 13/13 pages.
- ✅ 0 typo sur les patterns ciblés (`Decarbonez`, `formees`, `opportunite`, `ca coute`, `Desengagement`, `autrès`, etc.).
- ✅ 0 référence à `Plus Jakarta Sans` ou `'Inter'` (polices fantômes).
- ✅ Sticky CTA orphelin retiré (HTML + CSS).
- ✅ Tous les `href="#"` non-navigationnels retirés ou commentés.
- ✅ Form contact : POST réel vers Formspree, honeypot, RGPD.

**Lighthouse** : non exécuté (besoin du navigateur côté utilisateur). Tester via :
```
open -a "Google Chrome" file://$(pwd)/index.html
```
Puis Lighthouse → Mobile → Run.

---

## Cibles Lighthouse attendues (basées sur les changements faits)

| Métrique | Avant (estimé) | Après (cible) |
|---|---|---|
| Performance | 65-75 | **≥ 80** (lazy-load + preload LCP + fonts trimmés) |
| Accessibilité | 75-85 | **≥ 90** (main, focus-visible, ARIA, contrastes, hit areas) |
| Best Practices | 90 | **≥ 90** |
| SEO | 85 | **≥ 95** (titles ≤ 60c, OG complet, BreadcrumbList, Course, sitemap propre) |

---

## Reporté à la migration WordPress

Délibérément non traité (le thème WP s'en chargera) :

1. **Refactor CSS architecture** (BEM, ITCSS, scoping) — sera reset par le thème WP.
2. **Extraction des composants** en template parts (`header.php`, `footer.php`, etc.).
3. **Build tool** (Vite, Astro, esbuild) — pas pertinent en statique.
4. **Conversion images WebP/AVIF** — plugins WP (ShortPixel, EWWW) le feront automatiquement.
5. **Cache, CDN, Service Worker** — gestion server-side WP + plugin (WP Rocket, etc.).
6. **Création page Particuliers / CPF** — attendre confirmation client offre B2C.
7. **Vrai contenu éditorial blog** — pipeline WP (Gutenberg, classement, taxonomies).

---

## Recommandations

1. **Avant push** : lire ce fichier, valider les TODO côté client, créer compte Formspree, fournir le vrai numéro et URL Calendly.
2. **Push branche** : `git push -u origin feat/audit-improvements-2026-04-29`. PR directement vers `main` ou rebase si conflits.
3. **Tag** : poser `v2026.04.29-audit` après merge si tu veux marquer le snapshot.
4. **Lighthouse** : run avant migration WP pour avoir un baseline durable.
5. **Migration WP** : ce travail accélère la migration — schemas, copy, structure sémantique, alt, contrastes sont déjà propres et reprenables tels quels par le thème.
