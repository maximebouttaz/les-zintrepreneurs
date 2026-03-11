# AURA — Product Page Design Spec

## Product
- **Name**: AURA
- **Type**: Reveil IA simulateur d'aube lie aux cycles de sommeil
- **Price**: Early bird 149 EUR / Standard 179 EUR / Premium 199 EUR
- **Funding goal**: 30 000 EUR
- **Platform**: Les Zintrepreneurs (static HTML/CSS/JS on Vercel)

## Key Features
1. Simulateur d'aube progressif (lumiere imitant le lever du soleil)
2. IA analyse des cycles de sommeil (capteurs + app)
3. Reveil au moment optimal du cycle leger
4. Sons roses en phase N3 pour ameliorer la recuperation profonde
5. App mobile compagnon avec stats de sommeil
6. Design minimaliste / objet deco chambre

## Visual Direction
- **Background**: Light — blanc/creme (#FAFAF8 ou #F5F3EE)
- **Text**: Noir fonce (#1a1a1a) titres, gris moyen (#6b6b6b) descriptions
- **Accents**: Gradient subtil aube (orange dore #E8934A -> violet doux #9B6EC6), utilise avec parcimonie
- **Typography**: Bebas Neue (titres), DM Sans (corps) — coherence avec le site principal
- **Spirit**: Apple product page — espace blanc genereux, minimaliste, scientifique, animations scroll

## Page Structure (aura.html)

### 1. Nav
- Logo "LES ZINTREPRENEURS" lien vers index.html
- Liens: Science / Features / Pre-commande
- CTA: "Pre-commander AURA"

### 2. Hero
- "AURA" en grand (Bebas Neue)
- Sous-titre: "Reveil IA. Simulateur d'aube. Synchronise a vos cycles."
- Visuel CSS: cercle lumineux avec gradient aube
- Prix: "A partir de 149 EUR"
- CTA: "Decouvrir" + "Pre-commander"

### 3. Section Science
- Explication cycles de sommeil (N1, N2, N3, REM)
- Focus sons roses en phase N3
- Schema visuel simplifie des phases (CSS art)
- Ton scientifique mais accessible

### 4. Section Features (grille 2x2)
- Aube progressive
- IA cycles de sommeil
- Sons roses N3
- App compagnon
- Icones minimalistes, descriptions courtes

### 5. Section Design
- Visuel produit (CSS art minimaliste)
- "Un objet qui se fond dans votre interieur"

### 6. Section Pre-commande
- Card financement (objectif 30 000 EUR)
- 3 paliers: Early Bird 149 EUR / Standard 179 EUR / Premium 199 EUR
- Barre de progression
- Compteur contributeurs + jours restants

### 7. Footer
- Coherent avec site principal

## Integration index.html
- Ajouter section "Notre premier projet" avec card AURA renvoyant vers aura.html

## Agent Team
- UX Designer: layout, hierarchie, interactions
- Copywriter: textes premium/scientifiques
- Frontend Dev: code HTML/CSS/JS, animations, responsive
- Product Manager: integration index.html, QA
