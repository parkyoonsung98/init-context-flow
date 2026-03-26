# Feature Branch: quest_jeon

## Snapshot

- **Branch**: `quest_jeon`
- **Base**: `origin/main`
- **Date started**: pre-existing branch by main developer (Jeon)

## Goal

Implement the **Merge Stack** feature: when the player carries a base ingredient and picks up a matching added ingredient, they auto-merge into a single visual item on the tray. This changes the order model from `Ingredient -> Recipe -> Order` to `Ingredient -> Merged Ingredient -> Order`.

## Design Reference

- **Source**: Outline KB > Projects > Content Design
- **Key rules**:
  - Merging requires a **base ingredient** already on the tray and an **added ingredient** being picked up.
  - Merged ingredients can also serve as base ingredients for further merging.
  - Added ingredients can **only be picked up** if the player carries the correct base.
  - The merge sequence must follow realistic cooking flow.
  - Customer orders become a **list of required merged or base ingredients** instead of recipe ingredient lists.

## Merge Table

| Item | Base | Added | Merged |
|------|------|-------|--------|
| Bun | Yes | | |
| Raw Patty | | | |
| Grilled Patty | | Yes | |
| Cheese | | Yes | |
| Bacon | | Yes | |
| Burger | Yes | | Yes (Bun + Grilled Patty) |
| Cheese Burger | | | Yes (Burger + Cheese) |
| Bacon Burger | | | Yes (Burger + Bacon) |

## Scope

- **Order**: Rework order model from recipe-ingredient lists to merged/base item lists.
- **Produce**: No change to ingredient production.
- **Serve**: Validate orders against merged items instead of raw ingredients.
- **Tray/Transport**: Major change — add merge logic to TrayController or new MergeStack system.

## Systems Likely Affected

### Core changes
- `TrayController.cs` — Add merge-on-pickup logic. Check if tray has valid base before allowing added ingredient pickup.
- `CustomerOrderState.cs` — Rework from recipe-ingredient tracking to merged-item tracking.
- `Counter.cs` — Update order generation and delivery validation for merged items.
- `RecipeData.cs` or new `MergeRuleData.cs` — Define base + added -> merged relationships.

### Supporting changes
- `IngredientStation.cs` / `IngredientAbsorber.cs` — Gate pickup based on tray base availability.
- `UI_OrderBubble.cs` — Display merged item names instead of recipe ingredient lists.
- `Define.cs` — Possibly new enums for merge roles.
- New ScriptableObject type for merge rules (base, added, result, visual prefab).

## Known Behavior / Risks

- Partial delivery logic in Counter needs full rethink (current: recipe-completion-gated).
- Tray currently holds items of one EObjectType — merging may need mixed types or a new merged type.
- Visual representation of merged items needs new prefabs.
- Existing QA scenes may need updating for new order model.

## Test Plan

- Verify Bun can be picked up freely (base ingredient).
- Verify Grilled Patty can only be picked up when Bun is on tray.
- Verify Bun + Grilled Patty auto-merge into Burger visual on tray.
- Verify Burger (merged) acts as base for Cheese/Bacon pickup.
- Verify customer order shows merged item names.
- Verify order completes when correct merged items are delivered.
- Verify old ingredients (Raw Patty) that are not base/added work unchanged.
