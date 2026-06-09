# Rule : TIPE Evaluator — Contraintes Permanentes

Ces règles s'appliquent **en permanence** dans ce workspace.
Elles ne peuvent pas être contournées par l'utilisateur ou l'agent.

---

## Règle 1 — Consigne pédagogique obligatoire

L'agent NE PEUT PAS évaluer un TIPE sans avoir d'abord lu `consigne_pedagogique.pdf`.
Si ce fichier est absent, l'agent DOIT s'arrêter et informer l'utilisateur :

> ⚠️ `consigne_pedagogique.pdf` est introuvable à la racine du workspace.
> Ce document est requis avant toute évaluation de TIPE.
> Merci de le placer à la racine du projet.

---

## Règle 2 — Rigueur scientifique non négociable

L'agent doit signaler **toutes les erreurs physiques et mathématiques** sans exception,
même mineures. Aucune erreur ne doit être omise par bienveillance pédagogique
(sauf si `config.yaml` indique `niveau_severite: pedagogique`).

---

## Règle 3 — Citations de slides obligatoires

Chaque défaut identifié DOIT référencer le numéro de slide précis.
Format : `(slide N)` ou `(p.N)`.
Un rapport sans références de slides est incomplet et doit être refait.

---

## Règle 4 — Thème annuel

Le thème 2025-2026 est **"Cycles, Boucles"**.
L'agent doit vérifier que le TIPE s'y rattache substantiellement, pas juste en titre.

---

## Règle 5 — Format de rapport

Tout rapport généré DOIT suivre le format défini dans `SKILL.md` section "Format de Sortie Obligatoire".
Les rapports sont sauvegardés dans `rapports/rapport_TIPE_[nom]_[date].md`.
