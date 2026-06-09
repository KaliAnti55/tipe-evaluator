---
name: tipe-evaluator
version: "1.0"
description: >
  Expert jury evaluator for TIPE CPGE student presentations.
  Triggers when the user asks to evaluate, analyze, critique, or correct
  a TIPE PDF presentation. Produces a structured scientific critique report
  identifying physics errors, math errors, inconsistencies, weak methodology,
  and SCEI compliance issues — exactly as a jury of the Centrale/Mines/CCINP
  concours would.
  Keywords: TIPE, CPGE, évaluer, corriger, jury, présentation, physique, maths,
  Cycles Boucles, rapport, analyse, critique scientifique.
triggers:
  - "évaluer TIPE"
  - "analyser présentation TIPE"
  - "corriger TIPE"
  - "jury TIPE"
  - "rapport TIPE"
  - "critique scientifique TIPE"
  - "TIPE PDF"
supported_models:
  - gemini-3-pro
  - gemini-3-flash
  - claude-sonnet-4-6
  - claude-opus-4-6
---

# Skill : TIPE CPGE Expert Evaluator

## Contexte : Qu'est-ce que le TIPE ?

Le **TIPE** (Travaux d'Initiative Personnelle Encadrés) est une épreuve orale obligatoire
dans toutes les filières scientifiques de CPGE (MP, MPI, PC, PSI, PT, TSI, TPC, BCPST, TB).

- Durée de la présentation orale : **15 minutes**
- Support : **diaporama PDF** format 4/3, ≤5 Mo, sans animation
- Jury : **2 examinateurs experts** dans les positionnements thématiques déclarés
- Thème 2025-2026 : **"Cycles, Boucles"**

### 6 critères SCEI officiels

| Groupe | Critère |
|---|---|
| Potentiel Scientifique | Pertinence & exactitude scientifiques |
| Potentiel Scientifique | Appropriation & capacité à apprendre |
| Potentiel Scientifique | Ouverture & Curiosité |
| Démarche Scientifique | Questionnement & Méthode |
| Démarche Scientifique | Résolution de problème |
| Démarche Scientifique | Communication – Présentation – Échange |

---

## Règle absolue N°1 — Lire la consigne pédagogique EN PREMIER

Avant toute analyse de PDF étudiant, l'agent DOIT lire `consigne_pedagogique.pdf`.
Sans ce fichier → **arrêter et le demander à l'utilisateur.**

```bash
# Vérifier la présence de la consigne
ls consigne_pedagogique.pdf 2>/dev/null || echo "ERREUR: consigne_pedagogique.pdf manquant"

# Extraire la consigne
pdftotext consigne_pedagogique.pdf - | head -200
```

---

## Workflow d'Analyse

### Étape 1 — Extraction du PDF étudiant

```bash
# Inventaire
pdfinfo student_tipe.pdf
pdffonts student_tipe.pdf

# Extraction texte
pdftotext student_tipe.pdf student_tipe.txt
cat student_tipe.txt

# Rasterisation pour inspection visuelle (graphiques, équations)
mkdir -p /tmp/tipe_slides
pdftoppm -r 150 -png student_tipe.pdf /tmp/tipe_slides/slide
ls /tmp/tipe_slides/
```

---

### Étape 2 — Analyse en 7 Dimensions

Marquer chaque problème avec :
- `[CRITIQUE]` — erreur fatale, pénalité sévère jury
- `[ERREUR]` — erreur physique/math/logique claire
- `[INCOHÉRENCE]` — contradiction interne
- `[FAIBLESSE]` — élément manquant ou insuffisant
- `[CONSEIL]` — suggestion d'amélioration

#### A. Ancrage Thème "Cycles, Boucles"
- [ ] Lien au thème **explicitement énoncé** (pas juste en titre) ?
- [ ] Connexion substantielle (pas un buzzword) ?
- [ ] Thème absent du corps du document → `[CRITIQUE]`

#### B. Problématique
- [ ] Une question scientifique claire et testable ?
- [ ] Pas de "étudier le phénomène X" → `[CRITIQUE]`
- [ ] La conclusion y répond-elle quantitativement ?
- [ ] Problématique ≠ conclusion → `[INCOHÉRENCE]`

#### C. Rigueur Physique & Mathématique ← PRIORITÉ ABSOLUE

**C.1 Analyse Dimensionnelle** — chaque équation :
- Unités cohérentes des deux côtés ?
- Constantes physiques avec valeurs et unités correctes ?
- Résultats numériques avec unités ?

**C.2 Mathématiques**
- Dérivées, intégrales, EDO correctement posées ?
- Approximations explicitement justifiées (sin θ ≈ θ → préciser θ << 1) ?
- Conditions aux limites énoncées ?
- Incertitudes expérimentales calculées ?

**C.3 Physique**
- Causalité correcte (cause ≠ effet inversés) ?
- Régime adapté (laminaire/turbulent, quantique/classique) ?
- Lois de conservation respectées (énergie, quantité de mouvement, masse) ?
- Conclusion découlant de la physique et non de l'intuition ?

**C.4 Graphiques et Données**
- Axes avec légendes ET unités ?
- Barres d'erreur sur données expérimentales ?
- Courbes modèle/expérience cohérentes ?
- Sources des figures externes citées ?

#### D. Démarche Scientifique
- [ ] Chaîne hypothèse → expérience/modèle → résultat → interprétation ?
- [ ] Allers-retours théorie ↔ expérience ?
- [ ] Échecs et limitations reconnus ?
- [ ] Contribution personnelle distinguable (travail de groupe) ?

#### E. Bibliographie
- [ ] Sources scientifiquement fiables (revues, manuels, institutionnel) ?
- [ ] Pas uniquement Wikipedia pour les affirmations scientifiques ?
- [ ] 2–10 références (norme MCOT) ?
- [ ] Figures externes citées ?

#### F. Présentation SCEI
- [ ] Slides numérotées ?
- [ ] Nom de l'établissement absent (règle SCEI obligatoire) ?
- [ ] ≤10 lignes par slide ?
- [ ] Slide de conclusion présente ?
- [ ] Numéro de candidat en page 1 ?

#### G. Cohérence Globale
- [ ] Titre = contenu ?
- [ ] Objectifs MCOT = travail réalisé ?
- [ ] Notations et symboles cohérents dans tout le document ?

---

## Format de Sortie Obligatoire

```markdown
# Rapport d'Évaluation TIPE — [Titre]
**Thème**: Cycles, Boucles (2025-2026) | **Filière**: [MP/PC/PSI/...]
**Fichier**: [nom_fichier.pdf] | **Date**: [YYYY-MM-DD]

## Résumé Exécutif
[3-5 phrases : bilan global, forces, problèmes critiques]

## 1. Ancrage au Thème ✅/⚠️/❌
## 2. Problématique ✅/⚠️/❌
## 3. Rigueur Physique & Mathématique
### 3.1 Tableau des Erreurs
| Slide | Type | Description | Sévérité |
|---|---|---|---|

### 3.2 Analyse Dimensionnelle (équation par équation)
### 3.3 Raisonnement Physique
### 3.4 Graphiques et Données

## 4. Démarche Scientifique ✅/⚠️/❌
## 5. Bibliographie ✅/⚠️/❌
## 6. Présentation SCEI ✅/⚠️/❌
## 7. Incohérences Détectées

## 8. Synthèse par Sévérité
### ❌ CRITIQUE
### ⚠️ ERREUR / INCOHÉRENCE
### 💡 FAIBLESSES / CONSEILS

## 9. Questions Probables du Jury (5-10 questions)

## 10. Note Estimée /5 par Critère SCEI
```

---

## Référence Rapide — Erreurs Physiques Fréquentes

| Erreur | Exemple | Flag |
|---|---|---|
| Énergie non conservée | Oscillateur sans terme de dissipation | ERREUR |
| Inversion cause/effet | "La force cause l'accélération... donc a = F" sans masse | ERREUR |
| 1er principe thermodynamique violé | ΔU ≠ Q - W | CRITIQUE |
| e^(grandeur dimensionnée) | e^(temps) sans normalisation | CRITIQUE |
| Dérivée du produit | d(uv)/dx = u'v' | ERREUR |
| Probabilité > 1 | P(A) = 1.3 | CRITIQUE |
| Pas de conditions initiales ODE | Solution sans CI | FAIBLESSE |
| Approximation non justifiée | sin θ ≈ θ sans préciser θ << 1 | ERREUR |
| Reynolds ignoré | Régime laminaire supposé sans calcul Re | FAIBLESSE |

---

## Self-Check avant output

- [ ] Consigne pédagogique lue en premier ?
- [ ] Chaque équation vérifiée dimensionnellement ?
- [ ] Chaque graphique vérifié (axes, unités, barres d'erreur) ?
- [ ] Problématique vérifiée ET conclusion vérifiée ?
- [ ] Questions du jury générées ?
- [ ] Format de rapport respecté ?

→ Si un item non coché : **compléter avant d'écrire le rapport.**
