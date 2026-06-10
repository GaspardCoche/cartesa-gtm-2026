# Migration WordPress — Cartesa : préparation du terrain

**Date** : 2026-06-10 · **Statut** : plan prêt, exécution après validation client.
**Principe** : migrer le site statique actuel vers WordPress **sans perdre le SEO ni le contenu validé**, et y brancher les outils choisis (cf. `Cartesa-Outils-recommandes.pdf`).

> ⚠️ La migration se fait **après** validation par le client de la refonte (contenu Services, témoignages, formations) et **après** son choix d'outils. Ce document prépare le terrain pour que l'exécution soit rapide et sûre.

---

## 1. Cible
Les URL canoniques pointent déjà vers **`cartesa-lyon.com`** — un **WordPress existe déjà** à cette adresse (les images du site y sont hébergées). La migration consiste donc à **porter le site statique refondu dans ce WordPress** (refonte du thème / des pages), pas à créer un nouveau domaine.

**À confirmer avec le client avant de lancer :**
- [ ] Accès admin WordPress `cartesa-lyon.com` (rôle administrateur).
- [ ] Hébergeur actuel + version PHP/WordPress.
- [ ] Thème actuel (à remplacer) et plugins déjà installés.
- [ ] Sauvegarde complète (fichiers + base) avant toute intervention.

## 2. Inventaire des pages (14 pages)
| Fichier statique | Page WordPress (slug) | Schema JSON-LD |
|---|---|---|
| `index.html` | `/` (Accueil) | ✅ |
| `expertises.html` | `/expertises` — Diagnostic & expertise RH (8 fiches) | ✅ |
| `accompagnements.html` | `/accompagnements` — À vos côtés | ✅ |
| `ingenierie.html` | `/ingenierie` — Ingénierie pédagogique & financière | ✅ |
| `formations.html` | `/formations` | ✅ |
| `temoignages.html` | `/temoignages` (galerie vidéo) | ✅ |
| `ressourcerie.html` | `/ressourcerie` — Ressources | ✅ |
| `equipe.html` | `/equipe` | ✅ |
| `contact.html` | `/contact` | ✅ |
| `rse-decarbonation.html` | `/rse-decarbonation` | ✅ |
| `blog.html` | `/blog` (hub éditorial) | — |
| `mentions-legales.html` | `/mentions-legales` | — |
| `politique-confidentialite.html` | `/politique-confidentialite` | — |
| `politique-cookies.html` | `/politique-cookies` | — |

→ **Conserver exactement les mêmes slugs** que les canoniques (`.html` retiré). Sinon, mettre des **redirections 301**.

## 3. Stratégie SEO (priorité — c'est un GTM organique)
- **URLs** : garder les slugs (cf. tableau). Toute URL qui change → **redirection 301**.
- **Redirections** : si l'ancien WordPress a déjà des URL (`/wp-...`, anciennes pages), les recenser et rediriger vers les nouvelles. Plugin : *Redirection* (gratuit).
- **Meta** : reprendre `title` + `meta description` + Open Graph de chaque page (déjà rédigés et nettoyés dans le statique). Plugin SEO : **Rank Math** ou **Yoast**.
- **Schema JSON-LD** : 11 pages ont déjà des blocs structurés (LocalBusiness, FAQ, BreadcrumbList, Course…). À réinjecter (via le thème ou le plugin SEO). **Ne pas perdre les FAQ schema** (bon pour Google).
- **Sitemap + robots.txt** : régénérés par le plugin SEO ; resoumettre dans Google Search Console après bascule.
- **Polices auto-hébergées** (RGPD) : conserver l'auto-hébergement (pas de Google Fonts en direct).
- **Bannière cookies** : déjà conforme — conserver l'équivalent (plugin de consentement RGPD).

## 4. Approche technique recommandée
- **Thème** : thème enfant léger + **page builder** au choix (Bricks ou Elementor) pour que le client puisse éditer le contenu en autonomie, OU thème custom si on veut coller au pixel près au design actuel. *Recommandation : page builder (autonomie client) avec un design system reprenant la charte (teal `#025659`, gold `#ecd034`, polices Sora/DM Sans).*
- **Composants à reproduire** : header/nav « Vos attentes » + Formations, hero, cartes fiches, galerie vidéo témoignages, FAQ accordéon, bandeaux, footer. La structure HTML actuelle sert de **maquette de référence** (1:1).
- **Fiches Services (8)** : 2 options — (a) sections d'une page `/expertises` (le plus simple, comme aujourd'hui), ou (b) **type de contenu personnalisé** « Fiche service » (réutilisable, filtrable) si le client veut faire évoluer le catalogue souvent. *Recommandation : démarrer en sections (a), passer en (b) seulement si besoin.*
- **CSS** : `styles.css` actuel sert de base ; à adapter aux classes du builder.

## 5. Assets à migrer
- **Images** : déjà en partie sur `cartesa-lyon.com/wp-content/` (réutilisables). Les images locales (`assets/img/`) → médiathèque WP.
- **Vidéos témoignages (~72 Mo, 7 clips de Stéphane Fournier)** : actuellement servies en local (hors Git). À héberger soit dans la **médiathèque WP** (simple, mais alourdit), soit sur **YouTube/Vimeo non répertorié** (recommandé : meilleures perfs + pas de poids serveur). La galerie pointera vers ces URL.
- **Photos manquantes** (TODO client) : équipe + illustrations figuratives (coachings flashs, supervision, profils) → à fournir et intégrer.
- **Logo texte blanc** (TODO client) : pour les fonds foncés.

## 6. Intégrations à brancher (cf. PDF outils)
Une fois les outils choisis par le client :
- **Brevo** : formulaires (contact, ressources, newsletter) → CRM ; code/extension Brevo.
- **Calendly + Stripe** : boutons « Réserver un créneau » (coachings flashs) → lien/embed.
- **Stripe Payment Links** : boutons de paiement de prestations.
- **Tally** : auto-diagnostics dans Ressources → embed, réponses vers Brevo.
- **Éditeur de tests** (Central Test / AssessFirst) : bouton « Faire le bilan » (profils) → lien.

## 7. Contenu à finaliser AVANT migration (TODO client)
- Respiration : nombre d'heures/mois (X) · périmètre exact d'Impulsion.
- Coaching : certification réelle de Catherine (Philippe n'est pas ICF).
- Photos équipe + illustrations figuratives · logo texte blanc.
- N° de téléphone de Catherine (Accueil/Contact).
- Validation finale du contenu Services, Témoignages, Formations.

## 8. Plan d'exécution (le jour J)
1. **Préparation** : sauvegarde complète, environnement de **préproduction** (staging) — on ne touche jamais le live directement.
2. **Thème + design system** : monter la charte et les composants de base.
3. **Pages** : recréer les 14 pages (mêmes slugs), réinjecter meta + schema.
4. **Assets** : importer images/vidéos, brancher la galerie témoignages.
5. **Intégrations** : formulaires → Brevo, boutons → Calendly/Stripe/Tally.
6. **SEO** : redirections 301, sitemap, vérif des canoniques, Search Console.
7. **Recette** : relecture page par page (contenu, liens, responsive, vitesse, RGPD).
8. **Bascule** : mise en ligne, surveillance 72h (404, positions, formulaires).

## 9. Checklist de bascule
- [ ] Toutes les URL répondent (pas de 404) — redirections en place.
- [ ] `title` / `description` / OG / schema présents sur chaque page.
- [ ] Formulaires testés (un contact arrive bien dans Brevo).
- [ ] Boutons « Réserver » / « Faire le bilan » / paiement testés.
- [ ] Galerie vidéo témoignages fonctionnelle.
- [ ] Mobile + vitesse (Core Web Vitals) OK.
- [ ] Bannière cookies RGPD active.
- [ ] Sitemap resoumis à Google Search Console.

---
*Préparé dans le cadre de la refonte. À exécuter sur préproduction après validation client + choix des outils.*
