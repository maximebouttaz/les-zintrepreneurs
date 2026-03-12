# AURA Page Produit — Refonte Levée de Fonds

## Objectif

Refondre la page produit AURA en format "pitch deck scrollable" en 3 actes pour servir un double objectif :
1. Convertir la cible client (homme 20-30 ans, sportif, premium) en pré-commande
2. Démontrer la vision et la traction aux investisseurs potentiels

## Cible

- Homme 20-30 ans
- Sportif (entraînement régulier, se lève tôt)
- Sensible au premium et à la performance
- Pain point : réveil difficile, fatigue, mauvaise humeur, perte de performance

## Ton et voix

- Tutoiement partout
- Vocabulaire premium : performance, optimisation, potentiel, récupération
- PAS de slang : pas de "claqué", "cramé", "crevé"
- Exemples de bon ton : "Tu mérites mieux qu'un réveil brutal", "Réveille ton plein potentiel"

## Produit

### V1 — Simulateur d'aube premium (en pré-commande)
- 250 lux melanopiques (2x plus que les concurrents)
- Spectre complet : progression rouge → orange → blanc → lumière du jour (481nm)
- Montée logarithmique sur 60-90 min (pas linéaire)
- Design : cube de verre givré sur socle blanc, minimaliste
- Pas de comparaison directe avec les concurrents — AURA se présente comme la référence

### V2 — Vision future (en exploration)
- Présentation par le bénéfice uniquement, pas par la techno
- Un réveil qui s'adapte à ton cycle de sommeil
- Optimisation de la récupération pendant le sommeil
- Pas de mention de bracelet, capteurs, ou specs techniques

## Delta avec l'existant

La page actuelle (`aura.html`) a la structure suivante :
- Nav → Hero (hypnogramme SVG animé) → Science (stats + hypnogramme + phases + sons roses) → Features (4 cards dont IA/V2) → Design → Recherche → Pré-commande → Footer

**Ce qui change :**

| Section existante | Action | Nouvelle section |
|---|---|---|
| Hero (hypnogramme SVG) | **Remplacé** | Hero avec photo produit |
| Science (stats, phases, sons roses) | **Réécrit et déplacé** | Acte 1 (problème, stats) + Acte 2A (science du réveil) |
| Features (4 cards incl. IA/sons roses) | **Remplacé** | Acte 2B (3 cards V1 uniquement). Le contenu IA/V2 est retiré des features et déplacé vers l'Acte 3 (Vision), reformulé en bénéfices sans specs techniques. |
| Design | **Gardé et adapté** | Acte 2C (même concept, palette épurée) |
| Recherche | **Supprimé de la page** | Les pages d'études restent accessibles via leurs URLs directes, mais la section n'apparaît plus sur la page produit — elle distrait du parcours de conversion. |
| Pré-commande | **Gardé et adapté** | Dénouement (mêmes paliers, ajout compteur urgence) |
| Modal pré-commande | **Gardé** | Le modal existant (openModal avec formulaire nom/email/phone) reste en place. Les CTAs des paliers ouvrent le modal comme actuellement. Style du modal mis à jour pour correspondre à la palette épurée. |
| Footer | **Adapté** | Même structure, palette épurée |

## Design System

### Évolution du système existant
- Garder : Plus Jakarta Sans + JetBrains Mono, cards blanches, border-radius 16-20px
- Épurer la palette : fond clair (#F8F9FA), texte sombre (#111), gris (#64748B, #94A3B8)
- Orange UNIQUEMENT en accentuation : CTAs, badges, métriques clés, hover states
- Accent orange : gradient linear-gradient(135deg, #E8934A, #D97706)
- Moins de couleur = plus premium

### Composants
- Bouton primary : gradient orange, seul élément "coloré" fort
- Bouton ghost : border gris, texte gris
- Section tags : JetBrains Mono, uppercase, orange
- Stat values : Plus Jakarta Sans 800, gros chiffres en #111 (pas de gradient sur le texte)
- Cards : fond blanc, border #E2E8F0, shadow subtile

## Structure de la page — Storytelling en 3 actes

### Navigation
- Sticky, fond blur
- Logo "LES ZINTREPRENEURS"
- Links : La science, Le produit, Vision, Pré-commander
- CTA : "Pré-commander" (bouton primary orange)

### HERO
- Headline fort, tutoiement premium (ex: "Tu mérites mieux qu'un réveil brutal.")
- Sous-titre : "AURA. Le simulateur d'aube conçu pour les athlètes."
- Photo produit (cube givré) en grand — à droite ou en fond. Remplace l'hypnogramme SVG animé actuel.
- CTAs : "Pré-commander AURA" (primary) + "Découvrir la science" (ghost)
- Prix : "À partir de 149 EUR · Livraison Sept. 2026"
- Badge : JetBrains Mono, identité premium/sport

### ACTE 1 — LE PROBLÈME
**Objectif** : créer l'identification émotionnelle avec le pain point. Section entièrement nouvelle.

- **Fond sombre** (#111 ou très foncé) pour marquer la rupture visuelle
- **Narration immersive** : "Ton alarme sonne. Ton corps est encore en sommeil profond. Cortisol au minimum. Réflexes ralentis. La journée commence déjà en déficit."
- **Stats clés en gros** (JetBrains Mono pour les chiffres) :
  - `6h42` — sommeil moyen en France
  - `1.7x` — risque de blessure sous 8h de sommeil (Milewski 2014)
  - `-7.5%` — baisse de performance avec mauvais sommeil (Craven 2022, meta-analyse 69 études N=959)
  - `72%` — des athlètes d'élite ne sont pas des lève-tôt naturels (Lastella 2015, Sargent 2014 : 28% matinaux, 65% intermédiaires, 6% vespéraux)
- **Transition narrative** : "Il existe une meilleure façon de se réveiller."
- Les stats apparaissent au scroll (animation fade-in)

### ACTE 2 — AURA V1 (LA SOLUTION)
**Objectif** : présenter le produit comme la réponse logique au problème.

#### 2A — La science du réveil (1 écran)
- Section tag : "// LA SCIENCE"
- Explication courte : comment la lumière déclenche le cortisol naturellement
- Pourquoi un réveil en sommeil profond crée l'inertie de sommeil
- Le principe : reproduire l'aube pour préparer ton corps avant le réveil

#### 2B — Le produit (1-2 écrans, section principale)
- Section tag : "// LE PRODUIT"
- **Grande photo produit centrée** (le cube givré allumé)
- **3 différenciateurs en cards** (V1 uniquement, pas de contenu IA/V2) :
  - **250 lux melanopiques** — la luminosité nécessaire pour activer ton horloge biologique
  - **Spectre complet** — progression rouge → orange → blanc → lumière du jour, comme une vraie aube
  - **Montée logarithmique** — 60-90 min de montée progressive, ton corps se prépare naturellement
- **Résultats scientifiques** (métriques en JetBrains Mono) :
  - Temps de réaction : -58ms (Thompson 2014)
  - Cortisol au réveil : +12.8% (Thorn 2004)
  - Qualité de sommeil perçue : +1.16 pts (Thompson 2014)
  - Inertie de sommeil : -50%

#### 2C — Design produit (demi-écran)
- Titre : "Un objet qui sait se taire."
- Description courte sur le design épuré, minimaliste
- Deuxième photo produit (version éteinte/ambiante)
- Card blanche avec le visuel centré

### ACTE 3 — LA VISION (V2)
**Objectif** : montrer que AURA a un futur ambitieux (pour les investisseurs) sans s'engager sur des specs.

- **Transition narrative** : "Et ce n'est que le début."
- **Titre** : "Un réveil qui apprend de toi." ou similaire
- **3 bénéfices** présentés simplement (pas de jargon) :
  - Se réveiller au moment idéal de ton cycle de sommeil
  - Un réveil qui s'adapte chaque nuit à ton rythme
  - Optimiser ta récupération pendant que tu dors
- **Visuel** : abstrait/évocateur (pas de mockup produit V2)
- **CTA optionnel** : "Être informé en premier" (email capture)
- Ton aspirationnel, tourné vers le futur

### DÉNOUEMENT — PRÉ-COMMANDE
**Objectif** : convertir. C'est la levée de fonds (crowdfunding).

- Section tag : "// PRÉ-COMMANDE"
- Phrase d'accroche : "Fais partie des premiers à changer ta façon de te réveiller."
- **Progress bar** : fond gris, fill gradient orange
- **Stats de traction** : montant levé, contributeurs, jours restants (gros chiffres Plus Jakarta Sans 800)
- **3 paliers en grid** :
  - **Early Bird | 149 EUR** — badge "LIMITÉ", 1 AURA, App 1 an, livraison France, nom dans les premiers soutiens. Livraison sept. 2026
  - **Standard | 179 EUR** — 1 AURA, App 1 an, livraison France, choix couleur. Livraison oct. 2026
  - **Premium | 199 EUR** — badge "POPULAIRE", border orange, scale(1.02). 1 AURA, App à vie, livraison France+Europe, choix couleur (3 options), accès beta V2. Livraison oct. 2026
- **Urgence** : compteur places restantes Early Bird (nouveau — nécessite une variable JS pour le nombre restant)
- **Modal** : les CTAs des paliers ouvrent le modal existant (openModal). Le modal est restyled pour la palette épurée (orange en accent uniquement).

### FOOTER
- Fond dark (#111)
- Texte gris clair
- "AURA est un projet porté par Les Zintrepreneurs."
- Links en JetBrains Mono
- Hover orange sur les liens

## Animations
- Scroll reveal : fade-in + translateY(20px) via IntersectionObserver
- Stats acte 1 : apparition progressive au scroll (compteurs animés)
- Transition acte 1 → acte 2 : passage du fond sombre au fond clair
- Cards hover : translateY(-2px) + shadow amplifiée
- Progress bar pré-commande : fill animé au scroll-in

## Responsive
- Breakpoints : 1024px, 768px, 480px
- Grids → 1 colonne sur mobile
- Tiers 3 cols → stack vertical sur mobile
- Hero headline : clamp pour resize fluide
- Photos produit : pleine largeur sur mobile

## Visuels disponibles
- `images/98397bc9-823e-4a56-ba78-6d5a1820acdc.JPG` — Produit allumé, ambiance chambre
- `images/Gemini_Generated_Image_zhw5olzhw5olzhw5.png` — Produit éteint, ambiance chambre

## Fichier cible
- Modification in-place de `aura.html`
- HTML/CSS/JS statique, un seul fichier
- Google Fonts : Plus Jakarta Sans + JetBrains Mono
