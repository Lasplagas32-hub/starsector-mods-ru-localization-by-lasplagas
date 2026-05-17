# Changelog

## 0.6.14b - after-preposition pronoun forms

- Added standalone after-preposition NPC pronoun forms: `$rulm_himAfterPrepGen`, `$rulm_himAfterPrepAcc`, `$rulm_himAfterPrepDat`, `$rulm_himAfterPrepIns`, `$rulm_himAfterPrepPrep`.
- These cover Russian n-forms such as `него`, `неё`, `нему`, `ней`, `ним`, `нём` when the preposition is already written in the translated text.
- Updated public Russian documentation and token tables.
- Runtime JAR remains unchanged from confirmed `0.6.13 FINAL` line.

## 0.6.14a - confirmed token-table release

- Added `$rulm_guyOrGirl*` tokens for `парень/девушка`.
- Added `$rulm_GuyOrGirl*` capitalized tokens.
- Added `$rulm_manOrWoman*` tokens for `мужчина/женщина`.
- Added `$rulm_ManOrWoman*` capitalized tokens.
- Added case forms: `Nom`, `Gen`, `Dat`, `Acc`, `Ins`, `Prep`.
- Updated public Russian documentation and launcher description.
- Runtime JAR remains unchanged from confirmed `0.6.13 FINAL` line.

## 0.6.13 FINAL

- Finalized route-first dynamic suffix layer.
- Confirmed same-source multi-pattern suffix use.
- Confirmed `$rulm_*` active-person fallback for TNP-like prisoner dialogs.
- Kept Public Quantity API.
- Kept external `plurals.csv` dictionary.
- Did not add previous-number guessing.

## Earlier confirmed features

- `$rulm_*` NPC/activePerson morphology.
- `$rulp_*` player address layer.
- `$ruln_num_*`, `$ruln_player*`, `$ruln_mem_*` quantity routes.
- Public API `rulm.api.RuMorphQuantity`.
