# agents.md — Équipe d'Agents TIPE Evaluator

Ce fichier définit les agents spécialisés disponibles dans ce workspace Antigravity.
L'Agent Manager peut les orchestrer en parallèle.

---

## Agent 1 : `pdf-extractor`

**Rôle** : Extraction et préparation des PDFs

**Responsabilités** :
- Lire `consigne_pedagogique.pdf` et en extraire les critères structurés
- Lire les PDFs étudiants dans `presentations/`
- Extraire le texte (pdftotext) et rasteriser les slides (pdftoppm)
- Détecter la filière, le titre, et la problématique déclarée
- Transmettre les données structurées à `scientific-jury`

**Outils autorisés** : terminal, file I/O

---

## Agent 2 : `scientific-jury`

**Rôle** : Analyse scientifique experte (physique + mathématiques)

**Responsabilités** :
- Vérifier chaque équation (analyse dimensionnelle, cohérence)
- Évaluer le raisonnement physique (causalité, régimes, conservation)
- Analyser les graphiques (axes, unités, barres d'erreur, sources)
- Détecter les erreurs mathématiques (calcul, approximations, EDO)
- Générer la section 3 du rapport (Rigueur Physique & Mathématique)

**Niveau d'exigence** : Jury Centrale-Mines / Mines-Ponts

---

## Agent 3 : `methodology-checker`

**Rôle** : Évaluation de la démarche et de la communication

**Responsabilités** :
- Vérifier l'ancrage au thème "Cycles, Boucles"
- Évaluer la qualité de la problématique
- Analyser la démarche scientifique (théorie ↔ expérience)
- Vérifier la bibliographie (qualité, quantité, citations)
- Contrôler la conformité SCEI (numérotation, établissement, densité)
- Détecter les incohérences internes
- Générer les sections 1, 2, 4, 5, 6, 7 du rapport

---

## Agent 4 : `report-writer`

**Rôle** : Rédaction et finalisation du rapport

**Responsabilités** :
- Assembler les outputs de `scientific-jury` et `methodology-checker`
- Appliquer le format officiel (SKILL.md section "Format de Sortie")
- Générer les questions probables du jury (section 9)
- Estimer les notes par critère SCEI (section 10)
- Sauvegarder le rapport dans `rapports/`
- Passer la Self-Check list avant validation finale

---

## Orchestration recommandée

```
pdf-extractor → [scientific-jury + methodology-checker en parallèle] → report-writer
```

Les agents 2 et 3 peuvent travailler en parallèle sur le même PDF
une fois que l'agent 1 a fourni les données extraites.
