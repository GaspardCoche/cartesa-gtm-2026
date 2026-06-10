# Refonte section « Services / Vos attentes » — Cartesa

**Date** : 2026-06-10 · **Statut** : design validé, prêt pour plan d'implémentation
**Source** : retours client (réunion 2026-06) + décisions de cadrage.

## Objectif
Réorganiser l'offre de services de Cartesa du **point de vue client** (« Vos attentes »), en fiches claires, en intégrant les nouvelles offres (coachings flashs, profils de comportement) et en séparant l'ingénierie pédagogique de la financière.

## Contraintes / scope
- Site **statique HTML/CSS** aujourd'hui, **WordPress** à terme. Orthographe FR parfaite, accents corrects (jamais de mojibake). Outil Edit, pas de perl.
- **GTM organique/SEO** : le contenu des fiches doit rester dans le DOM (pas tout en pop-up masquée).
- **Présentation maîtrisée** : on présente assez pour comprendre + donner envie + SEO, mais **on ne dévoile PAS les modalités/tarifs/spécificités fines** (surtout coachings et accompagnements) — celles-ci se révèlent à l'engagement (contact / réservation).
- **Aucun prix** affiché.

### Dans le périmètre MAINTENANT (statique)
Toutes les fiches/offres présentées, avec CTA adaptés (« Échanger », « Réserver un créneau », « Faire le bilan ») qui pointent **vers le contact** (page/échange) pour l'instant.

### Reporté à WordPress (présenté mais non branché)
- **Coachings flashs** : réservation de créneau + **paiement en ligne** (module à choisir, ex. Brevo).
- **Profils de comportement** : questionnaire (DISC/MBTI/Forces motrices) + **restitution en ligne**.

### Hors périmètre (YAGNI)
- Outil **OGAN** (client : « à rediscuter »).
- Fiche « Accompagnement à l'entrepreneuriat » (retirée, non mentionnée).
- Onglets exploratoires « prestataires européens » / « modèles e-commerce » (client : « se renseigner » → différé).

## Architecture
On **restructure les 3 pages existantes** (pas d'explosion de pages). Menu **« Vos attentes »** (déjà en place) :
1. **Diagnostic & expertise RH** (`expertises.html`) → catalogue de 8 fiches.
2. **À vos côtés** (`accompagnements.html`) → les formules d'accompagnement dans la durée.
3. **Ingénierie pédagogique & financière** (`ingenierie.html`) → 2 volets séparés.

Principe de fiche (carte) : **titre · à qui ça s'adresse · le bénéfice · 2-3 points clés · 1 CTA**. Pas de détail opérationnel/tarifaire.

---

## Page 1 — « Diagnostic & expertise RH » (catalogue, 8 fiches)

Grille de cartes. Présentation maîtrisée (pas de tout-dévoiler).

| # | Fiche | À qui | Bénéfice | Points clés | CTA → |
|---|-------|-------|----------|-------------|-------|
| 1 | **Diagnostic & accompagnement** | Dirigeants PME/ETI voulant structurer leur RH | Y voir clair + plan d'action concret | Diagnostic terrain, co-construction, suivi | Échanger → contact |
| 2 | **Conduite de projet** | Structures en transformation (réorg, fusion, croissance) | Piloter le changement sans casse | Cadrage, accompagnement managers, dialogue social | Échanger → contact |
| 3 | **Coaching individuel & collectif** | Dirigeants, managers, équipes | Lever les blocages, faire grandir | Individuel ou collectif, ancré terrain | Échanger → contact |
| 4 | **Coachings flashs** *(nouveau)* | Managers voulant un coup de pouce ponctuel | Une séance ciblée, sans engagement long | Séances courtes (créneaux midi/soir), inscription facile, 15 min de qualif | Réserver un créneau → contact *(paiement/booking = WP)* |
| 5 | **Co-développement : animation de cercles** | Orgas qui veulent lancer le co-dév | Intelligence collective entre pairs | On anime vos cercles, on vous apprend à les mettre en place | Échanger → contact |
| 6 | **Co-développement : supervision** | Animateurs internes déjà en place | Monter en compétence vos animateurs | Supervision des animateurs internes, éventuelle animation inter-entreprises | Échanger → contact |
| 7 | **Profils de comportement & motivation** *(nouveau)* | Recrutement, cohésion d'équipe, dev managers | Mieux se connaître, recruter, manager | DISC, Forces Motrices, MBTI ; évaluation + restitution | Faire le bilan → contact *(questionnaire en ligne = WP)* |
| 8 | **Formation** | — | — | Carte teaser | Voir les formations → `formations.html` |

⚠️ Fiches 4 et 7 : NE PAS afficher tarif ni modalités détaillées (spécifiques, gérées à l'engagement).
⚠️ Fiche 3 (Coaching) : ne pas attribuer de certification ICF à Philippe (il n'est pas ICF). Vérifier la certification de Catherine avant d'afficher un label.

## Page 2 — « À vos côtés » (`accompagnements.html`)
Les **formules d'accompagnement dans la durée**. On garde la structure (pourquoi un accompagnement, situations concrètes, FAQ), sans prix.
- **Respiration** : « vous nous appelez, on y répond » → forfait **jusqu'à X h/mois** (`<!-- TODO client : X heures -->`), **sans veille juridique** (retirer toute mention de veille juridique).
- **Impulsion** : description **étoffée** — un cran au-dessus de Respiration : coaching des managers + co-développement + formation inclus, accompagnement régulier. *(Texte à valider client.)*
- **RH à temps partagé** : service **externalisé ET internalisé** — présence RH régulière, dans vos murs ou à distance, pour structurer/relancer la fonction.

## Page 3 — « Ingénierie pédagogique & financière » (`ingenierie.html`)
**2 volets clairement séparés** :
- **Ingénierie pédagogique** : concevoir des parcours sur mesure (AFEST, dispositifs, certifiants), montée en compétences. (Le contenu « entretien professionnel / mise en conformité » est rattaché ici comme dispositif.)
- **Ingénierie financière** : monter les financements (PCRH, plan de développement, FNE, CPF, CO2I) — **co-finançable** (OPCO ou Région), on vous accompagne sur le dossier, reste à charge éventuel connu d'avance. *(Déjà nettoyé : plus de « 100% », plus de « 0 démarche ».)*
- Corriger le titre « 9 OPCO partenaires, tous secteurs couverts » → reformuler sans surnommer (ex. « Tous dispositifs, tous secteurs »).

## TODO client (bloquants)
- Respiration : nombre d'heures/mois (X).
- Impulsion : valider/affiner la définition.
- Coaching : certification réelle de Catherine (Philippe n'est pas ICF).

## Critères d'acceptation
- Menu « Vos attentes » mène aux 3 pages restructurées.
- Page 1 = 8 fiches, contenu SEO dans le DOM, sans tarif/détail sensible, CTA → contact.
- Coachings flashs & Profils présentés avec CTA (« Réserver » / « Faire le bilan ») non branchés (placeholder WordPress documenté).
- Page 2 : 3 formules corrigées (Respiration sans veille juridique + forfait h/mois ; Impulsion étoffée ; RH temps partagé externalisé/internalisé). Aucun prix.
- Page 3 : 2 volets séparés (péda / financière). Financement = co-finançable.
- 0 mojibake, HTML valide, responsive, cohérent avec la charte (teal/gold, `.section-header` centrés).
