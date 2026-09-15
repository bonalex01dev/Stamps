# Stamps — TODO

## Refresh refactor (fonction unifiée `refreshStamps(ns, gui)`)

- [ ] **Fusion des entrées de menu** : remplacer les deux entrées actuelles
      ("Refresh all Stamps" / "Refresh all Stamp Labels") par une seule entrée
      "Refresh Stamps (full check)" pointant vers `refreshStamps(gui=True)`.
      Garder `refreshStampLabels` comme sous-ensemble rapide (affichage seul).
- [ ] **Lancement au changement de mode static<->expression** : quand
      `STAMPS_AUTOLABEL_MODE` change, exécuter `refreshStamps(gui=True)` pour
      migrer tous les autolabels dans le nouveau mode (constante `repr(title)`
      en static, expression upstream `nuke.thisNode().knob("title").value()`
      en expression — expression upstream confirmée identique au Stamps non
      modifié de `.nuke/stamps`).
- [ ] Décidé : **pas** d'auto-modification au chargement de script
      (`gui=False` sur onScriptLoad rejeté — risque d'altérer des scripts de
      prod silencieusement).

## Doublons de titles (gros projet, plus tard)

- [ ] Détection des doublons de title entre anchors : déjà signalée dans
      `refreshStamps` (warnings), mais non corrigée automatiquement.
- [ ] Mécanisme de préfixe/suffixe "en masse" : proposer un renommage groupé
      (préfixe/suffixe appliqué à tous les titles d'une sélection d'anchors).
- [ ] Déclenchement au "coller" : détecter des doublons de title sur les
      anchors collés et proposer le renommage. Les stamps-linked doivent se
      relinker automatiquement (vérifier que le knob `anchor` + l'input suivent
      le nouvel anchor retitré).

## Tests à implémenter

- [ ] Copier-coller d'un groupe anchor + stamps-linked : vérifier le relink
      automatique (knob `anchor` mis à jour, input reconnecté).
- [ ] Copier-coller créant des doublons de title : comportement attendu.
- [ ] Renommage de title : propagation anchor -> wireds (via callbacks), labels
      à jour dans les deux modes (static et expression).
- [ ] `refreshStamps` : migration static<->expression bidirectionnelle, réparation
      des titres/autolabels/connexions dérivés, warnings de doublons.
