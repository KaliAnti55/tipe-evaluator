# Workflow : /evaluer-tipe

**Description** : Évalue un ou plusieurs PDFs de TIPE dans le dossier `presentations/`.
Génère un rapport complet par fichier dans `rapports/`.

**Déclenchement** : tapez `/evaluer-tipe` dans le panneau agent d'Antigravity.

---

## Étapes du Workflow

### Étape 1 — Vérification des prérequis

Vérifier que `consigne_pedagogique.pdf` existe à la racine du workspace.
Si absent : stopper et demander à l'utilisateur de le fournir.

Lister les fichiers PDF dans `presentations/` :
```
ls presentations/*.pdf
```
Si aucun PDF : informer l'utilisateur et s'arrêter.

### Étape 2 — Lecture de la consigne pédagogique

Extraire et lire intégralement le contenu de `consigne_pedagogique.pdf`.
Identifier :
- Les critères d'évaluation spécifiques à ce contexte
- Les exigences de structure imposées
- Le niveau d'exigence attendu (filière, concours cible)
- Toute règle spécifique mentionnée

### Étape 3 — Pour chaque PDF dans presentations/

Pour chaque fichier `presentations/[nom].pdf` :

3a. Extraire le texte complet avec `pdftotext`
3b. Rasteriser les slides avec `pdftoppm` pour inspection visuelle
3c. Activer le skill `tipe-evaluator` (chargé automatiquement)
3d. Exécuter l'analyse complète en 7 dimensions (A à G du SKILL.md)
3e. Passer la Self-Check list avant de finaliser
3f. Écrire le rapport dans `rapports/rapport_TIPE_[nom]_[YYYY-MM-DD].md`

### Étape 4 — Synthèse finale (si plusieurs PDFs)

Si plusieurs PDFs ont été évalués, produire un fichier `rapports/synthese_promotion_[date].md`
avec :
- Tableau récapitulatif des erreurs les plus fréquentes
- Classement indicatif par qualité
- Recommandations collectives pour l'encadrant

---

## Paramètres optionnels

Vous pouvez préciser dans votre message :
- `/evaluer-tipe eleve1_tipe.pdf` → évaluer un seul fichier
- `/evaluer-tipe --filiere PSI` → forcer la filière si non détectée
- `/evaluer-tipe --mode pedagogique` → rapport bienveillant (vs jury strict)
- `/evaluer-tipe --concours centrale` → calibrer sur Centrale-Mines
