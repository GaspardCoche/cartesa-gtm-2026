---
title: "CARTESA — Bilan d'avancement du site (18 avril → 12 mai 2026)"
author: "Équipe technique pour CARTESA"
date: "12 mai 2026"
---

# Bilan d'avancement du site CARTESA

**Période couverte :** 18 avril → 12 mai 2026
**Destinataire :** Catherine Lenoir et l'équipe CARTESA
**Statut :** version pré-production, prête à présenter

---

## 1. Résumé en 5 lignes

- **17 commits livrés**, **+6 400 lignes ajoutées / −3 500 supprimées** sur le code source.
- **15 pages** retravaillées (toutes les pages publiques + la feuille de styles globale).
- Le site garde son **design "flat"** mais gagne en lisibilité, en rythme et en clarté de positionnement (RH au premier plan, RSE en complément).
- **4 pages obsolètes archivées** (rh-transition, pass-rh, financement, entretien-parcours) — elles redirigent automatiquement vers leurs équivalents actuels.
- Le site est aujourd'hui **prêt à recevoir vos validations** (numéro de téléphone, vrais témoignages, image de partage social, etc.) avant la mise en ligne publique.

---

## 2. Le site en un coup d'œil

```
┌─────────────────────────────────────────────────────────────┐
│  PAGES PUBLIQUES (visibles depuis le menu)                  │
├─────────────────────────────────────────────────────────────┤
│  Accueil                  ← index.html                       │
│  Nos services             ← menu déroulant                   │
│    ├ Diagnostic & Expertise RH/RSE   ← expertises.html       │
│    ├ Accompagnements RH & RSE        ← accompagnements.html  │
│    ├ RSE & Décarbonation             ← rse-decarbonation.html│
│    └ Ingénierie pédagogique & financière ← ingenierie.html   │
│  Formations              ← formations.html                   │
│    ├ Certifiantes (ancre)                                    │
│    ├ Sur mesure (ancre)                                      │
│    └ Catalogue 2026 (ancre)                                  │
│  Témoignages             ← temoignages.html                  │
│  Ressources              ← ressourcerie.html                 │
│  L'équipe                ← equipe.html                       │
│  Contact                 ← contact.html                      │
│  Blog (en attente WP)    ← blog.html (page d'attente)        │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│  COULISSES (organisation du dossier)                        │
├─────────────────────────────────────────────────────────────┤
│  docs/         ← Documents de pilotage, ce bilan, audits     │
│  archive/      ← Anciennes pages avec redirections auto      │
│  documents/   ← PDF / téléchargements clients (5 fichiers)   │
│  styles.css   ← Feuille de styles unique                     │
│  sitemap.xml  ← Plan du site pour Google                     │
└─────────────────────────────────────────────────────────────┘
```

> *Bon à savoir :* chaque page utilise la même feuille de styles `styles.css`. Modifier une couleur ou une typo se fait en un seul endroit, sans risque de désynchronisation.

---

## 3. Les 10 axes d'amélioration livrés

### Axe 1 — Positionnement éditorial : RH au cœur, RSE en complément

**Avant :** la page d'accueil mettait RH, RSE, transition et formation au même niveau visuel (mêmes couleurs, même poids typographique).

**Après :** le titre principal annonce explicitement *« RH, transition et formation : on s'occupe de tout, vous respirez. RSE en complément. »*. La RSE reste un volet d'expertise présent dans la navigation (Nos services → RSE & Décarbonation), mais ne brouille plus le message principal.

**Pourquoi :** les visiteurs qui arrivent sur votre accueil comprennent immédiatement votre cœur de métier. La RSE est valorisée comme une expertise spécialisée plutôt que diluée dans la promesse.

### Axe 2 — Cohérence des chiffres

Tous les chiffres affichés sur le site sont désormais **alignés sur la réalité visible** :

| Chiffre annoncé           | Avant     | Après |
| ------------------------- | --------- | ----- |
| Années d'expérience       | hétérogène| 20+   |
| Nombre d'experts          | hétérogène| 6     |
| OPCO partenaires          | 14 puis 11| 9     |
| Villes (carte formations) | 10        | 9     |
| Pôle DRH & Partenaire RSE | 6 experts | 4     |

> *À confirmer côté CARTESA :* si vous comptez vraiment 11 OPCO partenaires officiels, communiquez-nous la liste exhaustive et nous remettrons à jour.

### Axe 3 — Refonte visuelle (design flat préservé)

- **Suppression des cards à "bordure colorée à gauche"** (jugées trop datées) sur Ingénierie et Accompagnements. Remplacées par un nouveau pattern de cards modernes : badge accent en haut, titre généreux, hover avec effet de "lift" subtil.
- **Suppression des bulles dégradées floutées en arrière-plan du hero** (effet "années 2018", peu lisible).
- **Refonte du bandeau de preuve** (Qualiopi, OPCO, …) en "shelf flottante" qui chevauche le hero — plus de coupure brutale entre la zone bleue et la zone blanche.
- **Logos certifications encapsulés dans des tuiles blanches** pour s'intégrer harmonieusement au fond bleu sur la section "Nos certifications".

### Axe 4 — Hiérarchie & lisibilité

- **Volets scroll horizontaux** (4 services présentés au scroll vertical) : durée d'apparition allongée — on a le temps de voir le volet 2 et 3 avant d'arriver sur le 4.
- **Chaque volet** reçoit une nuance de couleur différente (subtile mais perceptible : teal lumineux, teal+gold, gold, teal+violet) pour qu'on sente le passage d'un service à l'autre.
- **Hero index** : ratio texte/image rééquilibré ; les deux boutons d'action sont désormais côte à côte ; le badge "Finançable via OPCO" remplace l'ancien "Jusqu'à 100% finançable via OPCO" (plus court, plus clair).

### Axe 5 — Navigation & repères dans le site

- **Fil d'Ariane visible** ajouté sur toutes les pages internes (`Accueil / Nom de la page`). Cliquable, retour direct à l'accueil.
- **Menu de navigation harmonisé** : le lien "Ressources" est désormais présent sur **toutes** les pages (était manquant sur Accompagnements).
- **Header dynamique** : sur les pages longues, le header se rétracte quand vous descendez et réapparaît dès que vous remontez — gain de surface utile pour la lecture.

### Axe 6 — Accessibilité (norme WCAG 2)

- Balise `<main>` ajoutée sur toutes les pages (sémantique correcte pour les lecteurs d'écran).
- Indicateur de focus clavier visible sur tous les éléments interactifs.
- ARIA correct sur les menus déroulants mobile.
- Hiérarchie des titres (H1 → H2 → H3) corrigée et auditée.
- Contrastes vérifiés et rehaussés sur les sous-titres et liens.

### Axe 7 — Performance & rapidité

- Images chargées en *lazy-loading* (gain temps d'affichage initial).
- Polices restreintes aux poids réellement utilisés (gain bande passante).
- Image principale du hero préchargée (LCP optimisé — métrique Google).

### Axe 8 — SEO & référencement local

- Titres de page recadrés à **≤ 60 caractères** (optimum Google).
- Données structurées **schema.org** enrichies : `BreadcrumbList` partout, `Course` sur la page Formations, `ContactPage` sur Contact, `Blog` sur Blog.
- **Sitemap.xml** mis à jour (12 mai 2026), pages archivées retirées proprement.
- **Open Graph + Twitter Cards** améliorés (partages réseaux sociaux plus propres).
- **Données géographiques** renseignées (`geo.region`, `geo.placename`, coordonnées GPS) → ciblage Isère / La Tour-du-Pin.

### Axe 9 — Conversion : formulaire, RDV, témoignages

- **Formulaire de contact branché sur Formspree** : les messages arrivent désormais réellement dans votre boîte. Auparavant, le formulaire était inerte.
- **Option "Accompagnement entrepreneuriat"** ajoutée dans le menu déroulant des sujets.
- **Mention RGPD** ajoutée + champ honeypot anti-spam.
- **Page Contact réorganisée** : Calendly direct en haut, formulaire visible sans scroller, "Pourquoi nous contacter" déplacé en colonne droite (toujours visible mais non bloquant).
- **Page Témoignages auditée** : 3 témoignages identifiés comme "à remplacer par de vrais clients" et marqués dans le code source (commentaires HTML visibles + attribut `data-testimonial-status`). Aucun témoignage supprimé : vous décidez du sort.

### Axe 10 — Blog : préparation à la migration WordPress

L'ancienne page Blog contenait 8 articles d'exemple (placeholders) — jugés non-présentables. Refonte complète en page d'attente professionnelle :

- Hero épuré : *« Notre blog éditorial arrive bientôt. »*
- Présentation des 3 familles de contenus prévues (Décryptages RH, Études de cas, Boîte à outils).
- Ponts vers les ressources déjà disponibles (Ressourcerie, Témoignages, Contact).
- Page en `noindex` tant que le contenu n'est pas publié — sera réactivée après migration WordPress.

---

## 4. Recommandations pour la migration WordPress

Vous prévoyez de migrer le site vers WordPress pour faciliter la gestion éditoriale au quotidien. Voici l'architecture recommandée.

### 4.1 Stack technique conseillé

| Couche               | Outil recommandé        | Coût annuel indicatif | Pourquoi                                         |
| -------------------- | ----------------------- | --------------------- | ------------------------------------------------ |
| Hébergement          | **o2switch** ou **OVH PRO**| 60–150 €              | Hébergeur français, support en français, sauvegardes auto |
| CMS                  | **WordPress** 6.x       | gratuit               | Standard du marché, communauté énorme            |
| Thème                | **Astra** ou **GeneratePress** (Pro) | 50–60 €               | Léger, performant, facile à personnaliser        |
| Builder              | **Elementor** (Pro)     | 50–60 €               | Drag-and-drop, identique à votre rendu actuel    |
| SEO                  | **Rank Math** (Free)    | gratuit               | Plus moderne que Yoast, données structurées incluses |
| Formulaires          | **WPForms** (Pro)       | 40 €                  | Drag-and-drop, intégrations CRM natives          |
| Sécurité             | **Wordfence** (Free)    | gratuit               | Firewall + scan malware                          |
| Backups              | **UpdraftPlus** (Free)  | gratuit               | Sauvegarde automatique vers Drive                |
| Cache / performance  | **WP Rocket**           | 50 €                  | Cache page + minification, gain Lighthouse net   |

### 4.2 Inscriptions aux formations — quel CRM ?

Pour gérer les inscriptions aux formations (suivi des leads, parcours du candidat, conversion), nous recommandons l'option qui correspond à votre maturité :

#### Option A — Démarrage simple (recommandé pour 2026)

**Brevo** (ex-Sendinblue) — **gratuit jusqu'à 300 emails/jour, ~30 €/mois ensuite**

- CRM léger intégré, idéal pour gérer 100–1000 contacts/an.
- Formulaires d'inscription connectés directement à Brevo via WPForms.
- Automatisations : email de confirmation, relance J+3, email de bienvenue après inscription validée.
- Hébergé en France (RGPD-friendly).
- Permet de séparer les listes : "Inscrits formation X", "Téléchargement guide", "Demande devis".

**Workflow complet d'une inscription :**

```
 1. Visiteur découvre Formations
              ↓
 2. Clique sur "S'inscrire" d'une session
              ↓
 3. Remplit formulaire WPForms (5 champs)
              ↓
 4. → Brevo : nouveau contact créé, étiqueté "Inscription [nom-session]"
 4bis. → Email automatique de confirmation envoyé au candidat
 4ter. → Notification email à Catherine
              ↓
 5. Catherine valide / planifie la session dans Brevo
              ↓
 6. Email automatique d'inscription confirmée + lien Calendly RDV intro
              ↓
 7. Tag contact "Client formation [année]" pour suivi long terme
```

#### Option B — Plus structurant (si croissance attendue)

**HubSpot CRM Free + Marketing Hub Starter** — **~50 €/mois**

- CRM enterprise-grade, gratuit jusqu'à 1 million de contacts.
- Pipeline visuel des leads.
- Suivi automatique des emails ouverts, clics, RDV pris.
- Reporting détaillé : taux de conversion par campagne, ROI par OPCO.
- Plus complexe à prendre en main mais évolutif sur 5–10 ans.

#### Option C — LMS intégré (si vous voulez vendre des formations en ligne)

**LearnDash** (LMS WordPress) — **199 €/an** — combiné avec **WooCommerce** (gratuit).

- Diffuse les formations en ligne (vidéos, QCM, certificats).
- Tunnel de vente : paiement → inscription → accès au contenu.
- Recommandé uniquement si vous voulez monétiser de l'e-learning. Pour formation en présentiel, l'option A suffit.

### 4.3 Notre recommandation finale

| Si vous voulez…                                  | Choisir       |
| ------------------------------------------------ | ------------- |
| Le minimum vital, vite mis en route, peu coûteux | **Option A — Brevo + WPForms** |
| Une stratégie marketing structurée long terme    | Option B — HubSpot |
| Vendre du e-learning en ligne                    | Option C — LearnDash + WooCommerce |

### 4.4 Données / SEO à migrer

Voici la "checklist de migration" pour ne rien perdre :

- ☑ **URLs identiques** : `cartesa-lyon.com/expertises.html` doit pointer vers `/expertises/` (page WP). Redirections 301 via plugin **Redirection** (gratuit).
- ☑ **Titres et meta-descriptions** : tous présents dans le code actuel — Rank Math les importe automatiquement si on copie le contenu page par page.
- ☑ **Données structurées schema.org** : à recréer dans Rank Math (Organisation, LocalBusiness, BreadcrumbList) — formulaires guidés.
- ☑ **Sitemap.xml** : Rank Math le génère automatiquement.
- ☑ **robots.txt** : Rank Math le génère ; conserver `Disallow: /wp-admin/`.
- ☑ **Open Graph + Twitter Cards** : champs Rank Math, à remplir page par page.
- ☑ **Données géographiques** (`geo.region`, coordonnées GPS) : à ajouter en custom HTML dans la home WP.
- ☑ **Formspree → WPForms** : changer l'action du formulaire de contact, brancher Brevo en backend.
- ☑ **Calendly** : conserver, juste copier les liens.
- ☑ **Documents PDF/téléchargements** : uploader dans la médiathèque WordPress, garder noms de fichiers identiques.
- ☑ **Pages archivées** (rh-transition, pass-rh, etc.) : recréer en redirections 301 directement dans le plugin Redirection.

### 4.5 Calendrier indicatif

1. **Semaine 1–2** : choix hébergement, installation WordPress, thème Astra, builder Elementor.
2. **Semaine 3–4** : recréation page par page (commencer par l'accueil, finir par les ressources).
3. **Semaine 5** : intégration Brevo + WPForms, tests inscription formation, vérification emails.
4. **Semaine 6** : SEO (Rank Math), schema.org, redirections, sitemap.
5. **Semaine 7** : recette client + corrections.
6. **Semaine 8** : mise en production (DNS), monitoring Lighthouse + Search Console.

---

## 5. Glossaire des termes techniques

| Terme           | Signification simple                                                |
| --------------- | ------------------------------------------------------------------- |
| **Hero**        | La grande zone d'introduction en haut d'une page (titre + visuel).  |
| **CTA**         | "Call To Action" = bouton incitant à une action (Contacter, S'inscrire). |
| **Breadcrumb**  | Fil d'Ariane = chemin de navigation type "Accueil / Page".         |
| **Schema.org**  | Méta-données structurées que Google lit pour mieux comprendre vos pages. |
| **Open Graph**  | Méta-données utilisées par LinkedIn / Facebook pour afficher l'aperçu d'un lien. |
| **Lighthouse**  | Outil Google qui note un site de 0 à 100 (performance, accessibilité, SEO).|
| **Lazy-loading**| Charger les images uniquement quand l'utilisateur fait défiler la page. |
| **LCP**         | Largest Contentful Paint = temps que met le plus gros élément à s'afficher. Métrique Google. |
| **CMS**         | Content Management System (WordPress = exemple) — interface pour modifier le contenu sans coder. |
| **LMS**         | Learning Management System — plateforme de cours en ligne (LearnDash). |
| **CRM**         | Customer Relationship Management — outil pour suivre vos prospects et clients. |
| **RGPD**        | Règlement européen sur la protection des données. Le formulaire actuel y est conforme. |
| **OPCO**        | Opérateur de Compétences (votre interlocuteur de financement formation). |

---

## 6. Ce qui attend votre confirmation

Pour finaliser et mettre en production publique, nous avons besoin de votre validation sur :

1. **Numéro de téléphone** à afficher (actuellement marqué *"Téléphone à venir"* avec un commentaire `TODO`).
2. **3 vrais témoignages clients** : nom, fonction, entreprise, citation, photo facultative — pour remplacer les 3 témoignages d'illustration.
3. **Confirmation des 5 autres témoignages anonymisés** : retours réels validés par les clients ?
4. **Liste exacte des OPCO partenaires** (actuellement 9 affichés).
5. **Handle Twitter / X** : actuellement `@CartesaRH` (placeholder).
6. **URL LinkedIn officielle** : à confirmer (le lien actuel pointe vers `linkedin.com/company/cartesa`).
7. **URL Calendly** : actuellement `calendly.com/cartesa-rh` — à confirmer.
8. **Image de partage social (og:image)** : recommandation = créer une image 1200×630 dédiée pour de meilleurs aperçus sur LinkedIn, Twitter, Slack.
9. **Choix CRM** : Option A (Brevo) / B (HubSpot) / C (LearnDash) ?
10. **Hébergement final** : reste sur o2switch, OVH, autre ?

---

## 7. Next steps & roadmap suggérée

### Court terme (avant mise en production publique)

1. **Vous nous communiquez les 10 points ci-dessus.**
2. Nous intégrons vos contenus définitifs.
3. Validation finale (visuel + contenu).
4. Mise en ligne sur l'URL définitive.

### Moyen terme (2–3 mois post-lancement)

1. **Migration WordPress** (suivre le calendrier 8 semaines).
2. **CRM Brevo branché** sur les formulaires formation.
3. **Premiers articles de blog** publiés sur le portail WP (3 décryptages RH minimum).
4. **Monitoring Lighthouse** : viser un score ≥ 90 sur toutes les pages.
5. **Google Search Console** branchée : surveiller les requêtes qui mènent au site.

### Long terme (6–12 mois)

1. **Pages OPCO dédiées** : une page par OPCO partenaire avec FAQ spécifique, dossier-type, contact référent.
2. **Études de cas approfondies** (sur la page Témoignages : 3–5 cas détaillés avec contexte / actions / résultats).
3. **Espace client privé** (si demande client) : suivi de mission, documents partagés.
4. **Newsletter mensuelle Brevo** : décryptages RH, échéances légales du mois, sessions à venir.
5. **Audit RGPD complet** (avec cookies consent type Axeptio si traffic > 5 000 visites/mois).

### Suggestions d'évolutions visuelles (libres)

- Réintroduire une vidéo de présentation de l'équipe en hero (1 min, sous-titrée).
- Carte interactive plus visuelle (Mapbox au lieu de SVG figé).
- Sections "avant / après" sur les études de cas (slider visuel).
- Mode sombre optionnel (effet "wow" pour un site B2B en 2026).

---

## 8. Lien vers la version actuelle

**Site déployé publiquement :** [https://gaspardcoche.github.io/cartesa-gtm-2026/](https://gaspardcoche.github.io/cartesa-gtm-2026/)

> *Note :* le déploiement public reflète la branche `main`. Tous les changements ci-dessus sont intégrés et visibles.

---

## 9. Comment réadapter le site ensuite

Le site est **modulaire** :

- **Modifier un texte** : ouvrir le fichier `.html` de la page concernée → trouver le mot → remplacer. Aucune autre page n'est impactée.
- **Modifier une couleur** : ouvrir `styles.css` → chercher `--teal-600` ou `--gold-500` → changer la valeur. La nouvelle couleur s'applique partout instantanément.
- **Ajouter une page** : copier une page existante (ex: `expertises.html`), renommer, modifier le contenu, ajouter au menu (header) et au `sitemap.xml`.
- **Modifier le menu** : éditer le bloc `<ul class="nav-links">` sur chaque page (ou centraliser via un futur include WP).
- **Ajouter un témoignage réel** : ouvrir `temoignages.html`, rechercher `data-testimonial-status="fictif-a-remplacer"`, remplacer le bloc, retirer le commentaire d'alerte.

Toutes ces opérations seront facilitées une fois migrées sur WordPress : interface visuelle, prévisualisation en temps réel, pas besoin d'éditer du code.

---

*Document généré le 12 mai 2026 — Bilan technique et fonctionnel.*
