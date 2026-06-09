# 🎓 TIPE CPGE Evaluator — Agent IA pour Correction de Présentations

Agent IA capable d'analyser en profondeur les présentations PDF de TIPE CPGE,
jouant le rôle d'un jury expert en physique et mathématiques.

**Thème 2025–2026 : "Cycles, Boucles"**

---

## Compatibilité — Deux plateformes supportées

| Plateforme | Statut | Fichier principal |
|---|---|---|
| **Google Antigravity** | ✅ Natif (Skills + Rules + Workflows) | `.agent/skills/tipe-evaluator/SKILL.md` |
| **Claude Code** | ✅ Natif (CLAUDE.md) | `CLAUDE.md` + `SKILL.md` |

---

## Structure du dépôt

```
tipe-evaluator/
│
├── 📄 SKILL.md                          ← Skill universel (Claude Code + référence)
├── 📄 CLAUDE.md                         ← Config auto Claude Code
├── 📄 agents.md                         ← Équipe d'agents (Antigravity multi-agent)
├── 📄 config.yaml                       ← Configuration (thème, filière, sévérité)
├── 📄 README.md
│
├── 🗂️ .agent/                           ← Configuration Antigravity
│   ├── skills/
│   │   └── tipe-evaluator/
│   │       └── SKILL.md                ← Skill natif Antigravity
│   ├── rules/
│   │   └── tipe-evaluator-rules.md     ← Règles permanentes (system prompt)
│   └── workflows/
│       └── evaluer-tipe.md             ← Commande /evaluer-tipe
│
├── 📁 presentations/                    ← Déposer les PDFs des élèves ici
├── 📁 rapports/                         ← Rapports générés (auto)
└── 📁 exemples/
    └── rapport_exemple_reference.md    ← Exemple de rapport de référence
```

---

## Utilisation avec Google Antigravity

### Installation

```bash
# Télécharger Antigravity
# → https://antigravity.google

# Cloner ce dépôt
git clone https://github.com/VOUS/tipe-evaluator.git

# Ouvrir dans Antigravity
# File > Open Folder > tipe-evaluator/
```

### Placer vos fichiers

```bash
# Consigne pédagogique (OBLIGATOIRE)
cp /votre/consigne_pedagogique.pdf ./consigne_pedagogique.pdf

# PDFs des élèves
cp /vos/tipes/*.pdf ./presentations/
```

### Lancer l'évaluation

Dans le panneau Agent d'Antigravity, tapez :

```
/evaluer-tipe
```

Ou pour un fichier spécifique :
```
/evaluer-tipe presentations/dupont_marie.pdf
```

### Les Skills se chargent automatiquement

Antigravity détecte automatiquement le skill `tipe-evaluator` dans `.agent/skills/`
quand vous parlez d'évaluation de TIPE. Vous pouvez aussi simplement écrire :

```
Évalue la présentation de Marie Dupont dans presentations/
```

### Agents en parallèle (Antigravity 2.0+)

Depuis Antigravity 2.0 (mai 2026), l'Agent Manager peut lancer les 4 agents
définis dans `agents.md` en parallèle pour des évaluations plus rapides :
- `pdf-extractor` → extraction
- `scientific-jury` + `methodology-checker` → analyse en parallèle
- `report-writer` → rédaction finale

---

## Utilisation avec Claude Code

```bash
# Installer Claude Code
npm install -g @anthropic-ai/claude-code

# Cloner le dépôt
git clone https://github.com/VOUS/tipe-evaluator.git
cd tipe-evaluator

# Placer les fichiers
cp /votre/consigne.pdf ./consigne_pedagogique.pdf
cp /vos/tipes/*.pdf ./presentations/

# Lancer
claude
```

Dans Claude Code :
```
Évalue toutes les présentations dans presentations/ en utilisant la consigne pédagogique.
```

---

## Configuration (config.yaml)

```yaml
theme_annuel: "Cycles, Boucles"
annee_scolaire: "2025-2026"
langue_rapport: "fr"
niveau_severite: "jury"        # "jury" ou "pedagogique"
filiere_defaut: "MP"
concours: "centrale-mines"    # influence le niveau d'exigence
```

---

## Critères SCEI évalués

| Critère | Groupe |
|---|---|
| Pertinence & exactitude scientifiques | Potentiel Scientifique |
| Appropriation & capacité à apprendre | Potentiel Scientifique |
| Ouverture & Curiosité | Potentiel Scientifique |
| Questionnement & Méthode | Démarche Scientifique |
| Résolution de problème | Démarche Scientifique |
| Communication – Présentation – Échange | Démarche Scientifique |

---

## Prérequis système

```bash
# Outils PDF
sudo apt-get install poppler-utils tesseract-ocr tesseract-ocr-fra

# Python
pip install pypdf pdfplumber
```

---

## Licence

MIT — Usage pédagogique libre.
Ne pas committer les PDFs des élèves (données personnelles).
