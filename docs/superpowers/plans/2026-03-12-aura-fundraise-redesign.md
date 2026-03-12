# AURA Fundraise Redesign — Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refondre aura.html en pitch deck scrollable 3 actes (Problème → V1 Solution → V2 Vision) pour la levée de fonds crowdfunding.

**Architecture:** Réécriture complète du contenu HTML de `aura.html` tout en conservant le design system existant (fonts, composants de base). Le CSS est nettoyé (suppression des styles orphelins), de nouvelles sections sont ajoutées (Acte 1 dark, Acte 3 Vision), et le JS existant (modal, animations, compteurs) est conservé avec ajustements mineurs.

**Tech Stack:** HTML5, CSS3 (Grid, Flexbox, animations), Vanilla JS, Google Fonts (Plus Jakarta Sans, JetBrains Mono)

**Spec:** `docs/superpowers/specs/2026-03-12-aura-fundraise-redesign-design.md`

**Note pour l'implémenteur:** Les numéros de ligne référencent l'état initial du fichier. Comme chaque tâche modifie le même fichier, **repérez les sections par leurs sélecteurs CSS ou commentaires HTML** (ex: `<!-- NAV -->`, `#science`, `.hero`) plutôt que par numéros de ligne.

**Décisions de scope:**
- Le CTA "Être informé en premier" (email capture V2) est exclu — hors scope pour la V1 de la page. Peut être ajouté plus tard.
- La progress bar existante se déclenche déjà au `window.load` via le JS init(). Pas de changement nécessaire.

---

## Chunk 1: Nav + Hero avec photo produit

### Task 1: Mettre à jour la navigation

**Files:**
- Modify: `aura.html` — `<!-- NAV -->` (nav HTML)

- [ ] **Step 1: Remplacer le HTML de la nav**

Localiser `<!-- NAV -->` et remplacer la section nav :

```html
<!-- NAV -->
<nav>
  <a href="index.html" class="nav-logo">LES ZINTREPRENEURS</a>
  <ul class="nav-links">
    <li><a href="#science">La science</a></li>
    <li><a href="#produit">Le produit</a></li>
    <li><a href="#vision">Vision</a></li>
    <li><a href="#precommande">Pre-commander</a></li>
  </ul>
  <a href="#precommande" class="nav-cta">Pre-commander</a>
</nav>
```

- [ ] **Step 2: Vérifier dans le navigateur**

Ouvrir `aura.html`. La nav doit afficher les 4 liens et le CTA "Pre-commander".

- [ ] **Step 3: Commit**

```bash
git add aura.html
git commit -m "refactor(aura): update nav links for 3-act structure"
```

### Task 2: Refaire le hero avec photo produit

**Files:**
- Modify: `aura.html` — `/* HERO */` (CSS: supprimer les styles hypnogramme SVG, ajouter styles hero photo)
- Modify: `aura.html` — `<!-- HERO -->` (HTML)

- [ ] **Step 1: Remplacer le CSS hero**

Localiser le commentaire `/* HERO */` dans le CSS. Supprimer tout jusqu'aux styles `.btn-primary` (non inclus). Cela inclut : `.hero`, `.hero-bg-svg`, `.grid-line`, `.hypno-curve`, `.hypno-fill`, `@keyframes drawHypno`, `@keyframes fadeInFill`, `.hero-y-labels`, `.hero-content`, `.hero-badge`, `.hero h1`, `.hero-subtitle`, `.hero-actions`, `.hero-price`. Remplacer par :

```css
/* HERO */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 4rem;
  padding: 7rem 2rem 4rem;
  max-width: 1200px;
  margin: 0 auto;
}

.hero-content {
  flex: 1;
  max-width: 520px;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.62rem;
  color: #D97706;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  font-weight: 500;
  padding: 0.4rem 0.8rem;
  border: 1px solid rgba(232,147,74,0.3);
  border-radius: 6px;
  margin-bottom: 1.5rem;
}

.hero h1 {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 800;
  font-size: clamp(2.8rem, 5vw, 4rem);
  line-height: 1.08;
  letter-spacing: -1.5px;
  color: #111;
  margin-bottom: 1.2rem;
}

.hero-subtitle {
  font-size: 1rem;
  color: #64748B;
  line-height: 1.7;
  margin-bottom: 1.5rem;
  font-weight: 400;
  max-width: 420px;
}

.hero-subtitle strong {
  color: #111;
  font-weight: 700;
}

.hero-actions {
  display: flex;
  gap: 0.8rem;
  align-items: center;
  margin-bottom: 1rem;
}

.hero-price {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  color: #94A3B8;
  margin-top: 0.5rem;
}

.hero-visual {
  flex: 1;
  max-width: 480px;
}

.hero-visual img {
  width: 100%;
  border-radius: 20px;
  box-shadow: 0 8px 40px rgba(0,0,0,0.08);
}
```

- [ ] **Step 2: Remplacer le HTML du hero**

Localiser `<!-- HERO -->` et remplacer toute la section hero (incluant le SVG hypnogramme, les y-labels, etc.) par :

```html
<!-- HERO -->
<section class="hero">
  <div class="hero-content">
    <div class="hero-badge">SIMULATEUR D'AUBE PREMIUM</div>
    <h1>Tu merites mieux<br>qu'un reveil brutal.</h1>
    <p class="hero-subtitle"><strong>AURA.</strong> Le simulateur d'aube concu pour les athletes.</p>
    <div class="hero-actions">
      <a href="#precommande" class="btn-primary">Pre-commander AURA</a>
      <a href="#science" class="btn-ghost">Decouvrir la science</a>
    </div>
    <p class="hero-price">A partir de 149 EUR · Livraison Sept. 2026</p>
  </div>
  <div class="hero-visual">
    <img src="images/98397bc9-823e-4a56-ba78-6d5a1820acdc.JPG" alt="AURA — simulateur d'aube sur table de nuit" />
  </div>
</section>
```

- [ ] **Step 3: Mettre à jour le responsive pour le hero**

Dans `@media (max-width: 768px)`, supprimer les anciennes règles hero (`.hero`, `.hero h1`, `.hero-y-labels`, `.hero-actions`) et ajouter :

```css
.hero { flex-direction: column; text-align: center; gap: 2rem; padding: 6rem 1.5rem 3rem; }
.hero-content { max-width: 100%; }
.hero-subtitle { max-width: 100%; }
.hero h1 { font-size: clamp(2.2rem, 8vw, 3.5rem); }
.hero-actions { justify-content: center; flex-direction: column; }
.hero-visual { max-width: 100%; }
```

Dans `@media (max-width: 1024px)`, ajouter :

```css
.hero { gap: 2rem; padding: 7rem 2rem 3rem; }
```

- [ ] **Step 4: Vérifier dans le navigateur**

Le hero doit afficher le texte à gauche et la photo produit à droite. Sur mobile (375px), le layout passe en colonne.

- [ ] **Step 5: Commit**

```bash
git add aura.html
git commit -m "feat(aura): redesign hero with product photo layout"
```

---

## Chunk 2: Acte 1 — Le Problème (section dark)

### Task 3: Créer la section Acte 1

**Files:**
- Modify: `aura.html` (CSS — ajouter styles `.problem-*` après `.btn-ghost`)
- Modify: `aura.html` (HTML — remplacer la section `#science` par Acte 1)

- [ ] **Step 1: Ajouter le CSS de la section problème**

Après les styles `.btn-ghost`, ajouter :

```css
/* ACTE 1 — LE PROBLEME */
.problem-section {
  background: #111;
  color: #fff;
  max-width: none;
  padding: 6rem 2rem;
}

.problem-inner {
  max-width: 1200px;
  margin: 0 auto;
}

.problem-section .section-tag {
  color: #E8934A;
}

.problem-narration {
  font-size: 1.15rem;
  line-height: 1.9;
  color: #94A3B8;
  max-width: 650px;
  margin-bottom: 3.5rem;
  font-weight: 400;
}

.problem-narration strong {
  color: #fff;
  font-weight: 600;
}

.problem-stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
  margin-bottom: 3.5rem;
}

.problem-stat {
  text-align: center;
}

.problem-stat .value {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 700;
  font-size: 2.8rem;
  color: #fff;
  line-height: 1;
  margin-bottom: 0.4rem;
}

.problem-stat .label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  color: #94A3B8;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  line-height: 1.4;
}

.problem-stat .source {
  font-size: 0.65rem;
  color: #64748B;
  margin-top: 0.2rem;
}

.problem-transition {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-size: clamp(1.4rem, 3vw, 2rem);
  font-weight: 700;
  color: #fff;
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid #222;
}
```

- [ ] **Step 2: Ajouter le responsive pour la section problème**

Dans `@media (max-width: 768px)` :

```css
.problem-stats { grid-template-columns: repeat(2, 1fr); gap: 2rem; }
.problem-section { padding: 4rem 1.5rem; }
```

Dans `@media (max-width: 1024px)` :

```css
.problem-stats { grid-template-columns: repeat(2, 1fr); }
```

- [ ] **Step 3: Remplacer le HTML**

Localiser `<!-- SCIENCE -->` (ou `id="science"`). Supprimer toute la section `#science` (incluant stat cards, hypnogramme, phases grid, sons roses, et le section-cta). Remplacer par :

```html
<!-- ACTE 1 — LE PROBLEME -->
<section class="problem-section" id="probleme">
  <div class="problem-inner">
    <div class="section-tag animate-in">// LE PROBLEME</div>
    <div class="section-title animate-in" style="color:#fff;">Ton reveil te coute<br>plus que tu ne le penses.</div>
    <p class="problem-narration animate-in">
      Ton alarme sonne. <strong>Ton corps est encore en sommeil profond.</strong> Cortisol au minimum. Reflexes ralentis. Mauvaise humeur. La journee commence deja en deficit — et tu ne t'en rends meme plus compte.
    </p>

    <div class="problem-stats">
      <div class="problem-stat animate-in">
        <div class="value">6h42</div>
        <div class="label">Sommeil moyen en France</div>
        <div class="source">vs 7-9h recommandees</div>
      </div>
      <div class="problem-stat animate-in">
        <div class="value">1.7x</div>
        <div class="label">Risque de blessure</div>
        <div class="source">sous 8h — Milewski 2014</div>
      </div>
      <div class="problem-stat animate-in">
        <div class="value">-7.5%</div>
        <div class="label">Performance globale</div>
        <div class="source">Craven 2022, N=959</div>
      </div>
      <div class="problem-stat animate-in">
        <div class="value">72%</div>
        <div class="label">Athletes pas leve-tot naturels</div>
        <div class="source">Lastella 2015</div>
      </div>
    </div>

    <div class="problem-transition animate-in">
      Il existe une meilleure facon de se reveiller.
    </div>
  </div>
</section>
```

- [ ] **Step 4: Supprimer les CSS orphelins de l'ancienne section science**

Localiser et supprimer ces blocs CSS (chercher par sélecteur) :
- `/* STAT CARDS */` : `.stats-grid`, `.stat-card`, `.stat-value`, `.stat-unit`, `.stat-label`, `.stat-source`
- `/* SCIENCE — HYPNOGRAMME */` : `.hypno-container`, `.hypno-labels`, `.hypno-chart`, `.hypno-bar` et tous les sous-sélecteurs `.bar-label`, `.wake-label`
- `/* PHASES CARDS */` : `.phases-grid`, `.phase-card`, `.phase-label` et sous-sélecteurs
- `/* SONS ROSES */` : `.sons-roses`
- `.section-cta` et `.section-cta a`
- Dans `@media (max-width: 768px)` : supprimer `.stats-grid`, `.phases-grid`, `.hypno-chart`

- [ ] **Step 5: Vérifier dans le navigateur**

La section problème doit avoir un fond dark (#111), le texte en blanc/gris, les 4 stats en grid, et la phrase de transition en bas.

- [ ] **Step 6: Commit**

```bash
git add aura.html
git commit -m "feat(aura): add dark problem section (Act 1) replacing old science section"
```

---

## Chunk 3: Acte 2 — La Science + Le Produit + Design

### Task 4: Section 2A — La science du réveil

**Files:**
- Modify: `aura.html` (HTML — nouvelle section après Acte 1)

- [ ] **Step 1: Ajouter le HTML de la section science**

Après la fermeture de `</section>` de la section problème et le divider, ajouter :

```html
<div class="divider"></div>

<!-- ACTE 2A — LA SCIENCE -->
<section id="science">
  <div class="section-tag animate-in">// LA SCIENCE</div>
  <div class="section-title animate-in">La lumiere est le signal<br>le plus puissant de ton corps.</div>
  <p class="section-intro animate-in">
    Chaque matin, la lumiere du soleil declenche une cascade hormonale precise : le cortisol monte, la melatonine chute, ton corps passe en mode eveil. Etre reveille en plein sommeil profond — par une alarme sonore — court-circuite ce processus. Resultat : inertie de sommeil, brouillard mental, perte de reflexes pendant 30 a 60 minutes.
  </p>
  <p class="section-intro animate-in" style="margin-bottom:0;">
    <strong style="color:#111;">AURA reproduit une aube naturelle</strong> pour preparer ton corps au reveil. Pas de choc. Pas de resistance. Ton cortisol monte progressivement, tes cycles se terminent naturellement.
  </p>
</section>
```

- [ ] **Step 2: Vérifier dans le navigateur**

La section science doit apparaître après la section problème, avec fond clair, tag orange, titre et paragraphes.

- [ ] **Step 3: Commit**

```bash
git add aura.html
git commit -m "feat(aura): add science section (Act 2A)"
```

### Task 5: Section 2B — Le Produit

**Files:**
- Modify: `aura.html` (CSS — remplacer `.features-*` et `.icon-*` par `.product-*`, `.diff-*`, `.result-*`)
- Modify: `aura.html` (HTML — remplacer `#features` par `#produit`)

- [ ] **Step 1: Remplacer le CSS features par le CSS produit**

Localiser `/* FEATURES */`. Supprimer tout le bloc features CSS (`.features-grid`, `.feature-card`, `.feature-icon`, tous les `.icon-sun`, `.icon-brain`, `.icon-sound`, `.icon-phone`, `.feature-card h4`, `.feature-card p`, `.feature-number`, `.feature-metric`). Remplacer par :

```css
/* ACTE 2B — LE PRODUIT */
.product-hero-img {
  width: 100%;
  max-width: 700px;
  margin: 0 auto 3rem;
  display: block;
  border-radius: 20px;
  box-shadow: 0 8px 40px rgba(0,0,0,0.06);
}

.diff-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.diff-card {
  background: #fff;
  border: 1px solid #E2E8F0;
  border-radius: 16px;
  padding: 2rem;
  transition: border-color 0.2s, transform 0.2s;
}

.diff-card:hover {
  border-color: rgba(232,147,74,0.4);
  transform: translateY(-2px);
}

.diff-card .diff-number {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.65rem;
  color: #D97706;
  letter-spacing: 0.1em;
  margin-bottom: 0.8rem;
}

.diff-card h4 {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  font-size: 1.1rem;
  color: #111;
  margin-bottom: 0.5rem;
}

.diff-card p {
  font-size: 0.85rem;
  color: #64748B;
  line-height: 1.7;
}

.results-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

.result-card {
  background: #fff;
  border: 1px solid #E2E8F0;
  border-radius: 12px;
  padding: 1.2rem;
  text-align: center;
}

.result-card .result-value {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 800;
  font-size: 1.6rem;
  color: #111;
  line-height: 1;
}

.result-card .result-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.62rem;
  color: #94A3B8;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  margin-top: 0.4rem;
  line-height: 1.3;
}

.result-card .result-source {
  font-size: 0.6rem;
  color: #CBD5E1;
  margin-top: 0.2rem;
}
```

- [ ] **Step 2: Ajouter le responsive produit**

Dans `@media (max-width: 768px)` :

```css
.diff-grid { grid-template-columns: 1fr; }
.results-grid { grid-template-columns: repeat(2, 1fr); }
```

Dans `@media (max-width: 1024px)`, remplacer `.features-grid` par :

```css
.diff-grid { grid-template-columns: 1fr 1fr; }
```

- [ ] **Step 3: Remplacer le HTML features par la section produit**

Localiser `<!-- FEATURES -->` (ou `id="features"`). Supprimer toute la section (HTML + divider avant). Ajouter après la section science :

```html
<div class="divider"></div>

<!-- ACTE 2B — LE PRODUIT -->
<section id="produit">
  <div class="section-tag animate-in">// LE PRODUIT</div>
  <div class="section-title animate-in">AURA. La reference<br>du reveil par la lumiere.</div>

  <img src="images/Gemini_Generated_Image_zhw5olzhw5olzhw5.png" alt="AURA simulateur d'aube" class="product-hero-img animate-in" />

  <div class="diff-grid">
    <div class="diff-card animate-in">
      <div class="diff-number">01</div>
      <h4>250 lux melanopiques</h4>
      <p>La luminosite necessaire pour activer ton horloge biologique. Assez puissant pour declencher la reponse cortisolaire naturelle — meme en plein hiver.</p>
    </div>
    <div class="diff-card animate-in">
      <div class="diff-number">02</div>
      <h4>Spectre complet</h4>
      <p>Progression rouge, orange, blanc, lumiere du jour — exactement comme une vraie aube. Chaque longueur d'onde arrive au bon moment pour ton corps.</p>
    </div>
    <div class="diff-card animate-in">
      <div class="diff-number">03</div>
      <h4>Montee logarithmique</h4>
      <p>60 a 90 minutes de montee progressive. Ton corps se prepare naturellement, ton cortisol monte au bon rythme. Pas d'interrupteur. Pas de choc.</p>
    </div>
  </div>

  <div class="results-grid animate-in">
    <div class="result-card">
      <div class="result-value">-58ms</div>
      <div class="result-label">Temps de reaction</div>
      <div class="result-source">Thompson 2014</div>
    </div>
    <div class="result-card">
      <div class="result-value">+12.8%</div>
      <div class="result-label">Cortisol au reveil</div>
      <div class="result-source">Thorn 2004</div>
    </div>
    <div class="result-card">
      <div class="result-value">+1.16</div>
      <div class="result-label">Qualite de sommeil</div>
      <div class="result-source">Thompson 2014</div>
    </div>
    <div class="result-card">
      <div class="result-value">-50%</div>
      <div class="result-label">Inertie de sommeil</div>
      <div class="result-source">Van de Werken 2010</div>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Vérifier dans le navigateur**

La section produit doit montrer la photo, 3 cards de différenciateurs, et 4 stats de résultats.

- [ ] **Step 5: Commit**

```bash
git add aura.html
git commit -m "feat(aura): add product section (Act 2B) with differentiators and results"
```

### Task 6: Section 2C — Design produit

**Files:**
- Modify: `aura.html` (CSS — remplacer `.design-*`, `.aura-art*`, `@keyframes breathe/glow`)
- Modify: `aura.html` (HTML — section design)

- [ ] **Step 1: Remplacer le CSS design**

Localiser `/* DESIGN SECTION */`. Supprimer tout le bloc jusqu'à `/* RECHERCHE */` (non inclus). Cela inclut : `.design-section`, `.design-desc`, `.aura-art-large`, `.aura-art`, `.aura-halo`, `.aura-ring`, `.aura-disk`, `.aura-center`, `@keyframes breathe`, `@keyframes glow`. Remplacer par :

```css
/* ACTE 2C — DESIGN */
.design-section {
  text-align: center;
}

.design-desc {
  font-size: 0.95rem;
  color: #64748B;
  line-height: 1.8;
  max-width: 550px;
  margin: 0 auto 3rem;
  font-weight: 400;
}

.design-img {
  width: 100%;
  max-width: 550px;
  margin: 0 auto;
  display: block;
  border-radius: 20px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.06);
}
```

- [ ] **Step 2: Remplacer le HTML design**

Localiser `<!-- DESIGN -->`. Remplacer toute la section (incluant l'artwork SVG aura-art-large) par :

```html
<div class="divider"></div>

<!-- ACTE 2C — DESIGN -->
<section class="design-section">
  <div class="section-tag animate-in">// DESIGN</div>
  <div class="section-title animate-in">Un objet qui sait se taire.</div>
  <p class="design-desc animate-in">Concu pour disparaitre dans ta chambre et sublimer ta table de nuit. Lignes epurees, surface douce, eclairage ambiant modulable. Pas de LED agressives. Juste une presence calme.</p>
  <img src="images/98397bc9-823e-4a56-ba78-6d5a1820acdc.JPG" alt="AURA design produit" class="design-img animate-in" />
</section>
```

- [ ] **Step 3: Supprimer les styles responsive orphelins**

Dans les media queries `@media (max-width: 768px)`, supprimer les règles `.aura-art`, `.aura-ring`, `.aura-disk`, `.aura-art-large` et leurs sous-sélecteurs.

- [ ] **Step 4: Vérifier dans le navigateur**

La section design doit afficher le titre, la description et la photo produit centrée.

- [ ] **Step 5: Commit**

```bash
git add aura.html
git commit -m "feat(aura): simplify design section with product photo"
```

---

## Chunk 4: Acte 3 — Vision + Pré-commande + Footer

### Task 7: Section Acte 3 — La Vision (V2)

**Files:**
- Modify: `aura.html` (CSS — ajouter `.vision-*`, supprimer `.research-*`)
- Modify: `aura.html` (HTML — remplacer `#recherche` par `#vision`)

- [ ] **Step 1: Supprimer le CSS recherche et ajouter le CSS vision**

Localiser `/* RECHERCHE */`. Supprimer tout le bloc CSS recherche (`.research-grid`, `.research-card`, `.rc-tag`, `.rc-title`, `.rc-desc`, `.rc-meta`, `.rc-arrow`, `.research-cta`, et la media query `.research-grid`). Remplacer par :

```css
/* ACTE 3 — VISION */
.vision-section {
  background: #FAFAFA;
}

.vision-transition {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.75rem;
  color: #D97706;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-bottom: 1rem;
}

.vision-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-top: 2.5rem;
}

.vision-card {
  background: #fff;
  border: 1px solid #E2E8F0;
  border-radius: 16px;
  padding: 2rem;
  transition: border-color 0.2s, transform 0.2s;
}

.vision-card:hover {
  border-color: rgba(232,147,74,0.3);
  transform: translateY(-2px);
}

.vision-card .vision-icon {
  font-size: 1.8rem;
  margin-bottom: 1rem;
}

.vision-card h4 {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  font-size: 1.05rem;
  color: #111;
  margin-bottom: 0.5rem;
}

.vision-card p {
  font-size: 0.85rem;
  color: #64748B;
  line-height: 1.7;
}
```

- [ ] **Step 2: Ajouter le responsive vision**

Dans `@media (max-width: 768px)` :

```css
.vision-grid { grid-template-columns: 1fr; }
```

Dans `@media (max-width: 1024px)` :

```css
.vision-grid { grid-template-columns: 1fr 1fr; }
```

- [ ] **Step 3: Remplacer la section recherche par la section vision**

Localiser `<!-- RECHERCHE -->` (ou `id="recherche"`). Supprimer toute la section et le divider avant. Ajouter après la section design :

```html
<div class="divider"></div>

<!-- ACTE 3 — LA VISION -->
<section class="vision-section" id="vision">
  <div class="vision-transition animate-in">Et ce n'est que le debut.</div>
  <div class="section-title animate-in">Un reveil qui apprend de toi.</div>
  <p class="section-intro animate-in">
    AURA V1 transforme ton reveil. La suite ira encore plus loin : un reveil qui comprend ton sommeil en temps reel et s'adapte a toi, nuit apres nuit.
  </p>

  <div class="vision-grid">
    <div class="vision-card animate-in">
      <div class="vision-icon">&#9790;</div>
      <h4>Le bon moment, chaque matin</h4>
      <p>Se reveiller au moment ideal de ton cycle de sommeil. Plus jamais en plein sommeil profond.</p>
    </div>
    <div class="vision-card animate-in">
      <div class="vision-icon">&#10227;</div>
      <h4>Un reveil qui evolue avec toi</h4>
      <p>Chaque nuit, AURA apprend ton rythme et affine son intervention. Plus tu l'utilises, plus il est precis.</p>
    </div>
    <div class="vision-card animate-in">
      <div class="vision-icon">&#9889;</div>
      <h4>Optimiser ta recuperation</h4>
      <p>Ameliorer la qualite de ton sommeil pendant que tu dors. Pas seulement un meilleur reveil — un meilleur sommeil.</p>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Vérifier dans le navigateur**

La section vision doit montrer la transition "Et ce n'est que le début", le titre, l'intro et 3 cards.

- [ ] **Step 5: Commit**

```bash
git add aura.html
git commit -m "feat(aura): add vision section (Act 3) replacing research section"
```

### Task 8: Mettre à jour la section pré-commande

**Files:**
- Modify: `aura.html` (HTML — section `#precommande`)
- Modify: `aura.html` (JS — ajouter compteur Early Bird)

- [ ] **Step 1: Mettre à jour le HTML pré-commande**

Localiser `<!-- PRECOMMANDE -->` (ou `id="precommande"`). Remplacer tout le contenu de la section par :

```html
<!-- PRECOMMANDE -->
<section id="precommande">
  <div class="section-tag animate-in">// PRE-COMMANDE</div>
  <div class="section-title animate-in">Fais partie des premiers<br>a changer ta facon de te reveiller.</div>
  <p class="precommande-desc animate-in">AURA est ne de l'idee de deux cousins convaincus qu'on peut mieux dormir grace a la technologie — sans la subir. Soutiens le projet et fais partie des premiers a vivre le reveil tel qu'il devrait etre.</p>

  <div class="progress-container animate-in">
    <div class="progress-bar">
      <div class="progress-fill" id="progress-fill"></div>
    </div>
    <div class="progress-meta">
      <div>
        <div class="raised" id="total-amount">0 EUR</div>
        <span>recoltes</span>
      </div>
      <div class="goal">objectif 30 000 EUR</div>
    </div>
  </div>

  <div class="precommande-stats animate-in">
    <div class="precommande-stat">
      <div class="val" id="nb-contributors">0</div>
      <div class="label">Contributeurs</div>
    </div>
    <div class="precommande-stat">
      <div class="val" id="days-left">0</div>
      <div class="label">Jours restants</div>
    </div>
  </div>

  <!-- TIERS -->
  <div class="tiers-grid">
    <!-- Early Bird -->
    <div class="tier-card animate-in">
      <div class="tier-badge accent">LIMITE — <span id="early-bird-remaining">72</span> RESTANTS</div>
      <div class="tier-name">Early Bird</div>
      <div class="tier-price">149 <span>EUR</span></div>
      <ul class="tier-list">
        <li>1 reveil AURA</li>
        <li>Application premium 1 an</li>
        <li>Livraison France incluse</li>
        <li>Ton nom parmi les premiers soutiens</li>
      </ul>
      <div class="tier-date">Livraison estimee : septembre 2026</div>
      <button class="tier-cta" onclick="openModal('Early Bird', 149)">J'en profite — 149 EUR</button>
    </div>

    <!-- Standard -->
    <div class="tier-card animate-in">
      <div class="tier-name" style="margin-top:0.5rem;">Standard</div>
      <div class="tier-price">179 <span>EUR</span></div>
      <ul class="tier-list">
        <li>1 reveil AURA</li>
        <li>Application premium 1 an</li>
        <li>Livraison France incluse</li>
        <li>Choix de la couleur</li>
      </ul>
      <div class="tier-date">Livraison estimee : octobre 2026</div>
      <button class="tier-cta" onclick="openModal('Standard', 179)">Pre-commander — 179 EUR</button>
    </div>

    <!-- Premium -->
    <div class="tier-card featured animate-in">
      <div class="tier-badge green">POPULAIRE</div>
      <div class="tier-name">Premium</div>
      <div class="tier-price">199 <span>EUR</span></div>
      <ul class="tier-list">
        <li>1 reveil AURA</li>
        <li>Application premium a vie</li>
        <li>Livraison France + EU incluse</li>
        <li>3 coloris au choix</li>
        <li>Acces beta fonctionnalites V2</li>
      </ul>
      <div class="tier-date">Livraison estimee : octobre 2026</div>
      <button class="tier-cta" onclick="openModal('Premium', 199)">Pre-commander — 199 EUR</button>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Ajouter la variable Early Bird au JS**

Dans la section `// ---- DATA ----` du script, ajouter :

```javascript
let earlyBirdRemaining = 72;
```

Dans la fonction `simulatePayment()`, après `contributors += 1;`, ajouter :

```javascript
if (selectedAmount === 149) {
  earlyBirdRemaining = Math.max(0, earlyBirdRemaining - 1);
  const el = document.getElementById('early-bird-remaining');
  if (el) el.textContent = earlyBirdRemaining;
}
```

- [ ] **Step 3: Vérifier dans le navigateur**

Les 3 paliers doivent s'afficher avec le Premium mis en avant (border orange). Le badge Early Bird doit afficher "LIMITE — 72 RESTANTS". Tester le modal : après un paiement Early Bird simulé, le compteur doit décrémenter.

- [ ] **Step 4: Commit**

```bash
git add aura.html
git commit -m "feat(aura): update preorder with early bird counter and premium featured tier"
```

### Task 9: Mettre à jour le footer, le titre de page, et restyler le modal

**Files:**
- Modify: `aura.html` — `<title>` (ligne 6)
- Modify: `aura.html` — `<!-- FOOTER -->` (HTML)
- Modify: `aura.html` — `/* MODAL */` (CSS)

- [ ] **Step 1: Mettre à jour le title tag**

Remplacer :
```html
<title>AURA — Le reveil IA qui respecte votre sommeil</title>
```
par :
```html
<title>AURA — Le simulateur d'aube concu pour les athletes</title>
```

- [ ] **Step 2: Mettre à jour le footer**

Localiser `<!-- FOOTER -->`. Remplacer le HTML par :

```html
<!-- FOOTER -->
<footer>
  <p><strong>AURA</strong> est un projet porte par Les Zintrepreneurs.</p>
  <p>Deux cousins, une obsession : t'offrir le meilleur reveil de ta vie.</p>
  <div class="footer-links">
    <a href="recherche.html">Recherche</a>
    <a href="index.html">Accueil</a>
    <a href="mailto:contact@leszintrepreneurs.com">Contact</a>
  </div>
  <div class="footer-copy">&copy; 2026 Les Zintrepreneurs. Tous droits reserves.</div>
</footer>
```

- [ ] **Step 3: Vérifier que le modal utilise la bonne palette**

Dans le CSS du modal (`/* MODAL */`), vérifier que toutes les couleurs d'accent sont déjà en orange (#E8934A / #D97706). Rechercher toute occurrence de l'ancien violet (#9B6EC6) — il ne devrait pas y en avoir (déjà corrigé dans la refonte précédente), mais vérifier. Si trouvé, remplacer par #D97706.

- [ ] **Step 4: Commit**

```bash
git add aura.html
git commit -m "refactor(aura): update title, footer, verify modal palette"
```

---

## Chunk 5: Nettoyage final et vérification

### Task 10: Nettoyage CSS et vérification complète

**Files:**
- Modify: `aura.html` (CSS — suppression sélecteurs orphelins)

- [ ] **Step 1: Vérifier qu'il ne reste pas de CSS orphelin**

Chercher dans le `<style>` les sélecteurs suivants et les supprimer s'ils sont encore présents :
- `.hero-bg-svg`, `.grid-line`, `.hypno-curve`, `.hypno-fill`
- `.stats-grid`, `.stat-card`, `.stat-value`, `.stat-unit`, `.stat-label`, `.stat-source`
- `.hypno-container`, `.hypno-labels`, `.hypno-chart`, `.hypno-bar`, `.bar-label`, `.wake-label`
- `.phases-grid`, `.phase-card`, `.phase-label`
- `.sons-roses`
- `.section-cta`
- `.feature-icon`, `.icon-sun`, `.icon-brain`, `.icon-sound`, `.icon-phone` et tous les sous-sélecteurs
- `.feature-card`, `.features-grid`, `.feature-number`, `.feature-metric`
- `.aura-art`, `.aura-halo`, `.aura-ring`, `.aura-disk`, `.aura-center`, `.aura-art-large`
- `@keyframes drawHypno`, `@keyframes fadeInFill`, `@keyframes breathe`, `@keyframes glow`
- `.research-grid`, `.research-card`, `.rc-tag`, `.rc-title`, `.rc-desc`, `.rc-meta`, `.rc-arrow`, `.research-cta`

- [ ] **Step 2: Nettoyer les media queries**

Vérifier les 3 media queries (1024px, 768px, 480px) :
- Supprimer toute règle référençant une classe supprimée
- S'assurer que les nouvelles classes sont présentes (`.hero`, `.problem-stats`, `.diff-grid`, `.results-grid`, `.vision-grid`)

- [ ] **Step 3: Vérification complète dans le navigateur (desktop)**

Ouvrir la page et parcourir toutes les sections :
1. Nav — 4 liens + CTA "Pre-commander"
2. Hero — photo produit à droite, headline à gauche
3. Acte 1 — fond dark, 4 stats en JetBrains Mono, transition narrative
4. Acte 2A — science du réveil (fond clair)
5. Acte 2B — photo produit, 3 différenciateurs, 4 résultats sourcés
6. Acte 2C — design, photo produit centrée
7. Acte 3 — vision V2, 3 cards bénéfices
8. Pré-commande — progress bar, compteur Early Bird, 3 paliers, Premium en avant
9. Footer — dark, liens fonctionnels

Vérifier aussi :
- Le modal s'ouvre en cliquant sur les CTAs des paliers
- Les compteurs animés fonctionnent (montant, contributeurs)
- Les animations scroll (fade-in) fonctionnent sur chaque `.animate-in`
- Aucune erreur dans la console JS

- [ ] **Step 4: Vérifier mobile (375px)**

Chrome DevTools → iPhone SE (375px) :
- Hero en colonne (texte → photo)
- Stats problème en 2x2
- Différenciateurs produit en 1 colonne
- Results en 2x2
- Vision cards en 1 colonne
- Tiers empilés
- Footer lisible
- Modal responsive (form fields en 1 colonne)

- [ ] **Step 5: Vérifier tablette (1024px)**

Chrome DevTools → iPad (1024px) :
- Hero avec gap réduit
- Stats problème en 2x2
- Différenciateurs en 2 colonnes
- Vision en 2 colonnes
- Tiers en 1 colonne

- [ ] **Step 6: Commit final**

```bash
git add aura.html
git commit -m "feat(aura): complete fundraise redesign — pitch deck scrollable 3 actes"
```
