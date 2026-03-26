# Chef Ready — System Authoring Guide

> Stable reference for how to add ingredients, stations, and quests. Update when authoring patterns change.

## 1) Ingredient Definition

An item is an **ingredient** when a system needs it as input for a process.

- Required input to any process/station: ingredient.
- Final serve/output item with no further processing: not ingredient.
- Trash/end-state item: not ingredient.

Examples:
- Patty to Grill: ingredient.
- Dirty dish to Sink: ingredient.
- Burger delivered to customer: not ingredient.
- Burnt patty (trash): not ingredient.

## 2) Create Ingredient Data (ScriptableObject)

1. Create asset: `Create > Campfire > ScriptableObject > IngredientData`
2. Configure: `Prefab`, `Spawn Interval`, `Max Spawned`
3. ID comes from asset name (`GetID() => name`) — renaming changes runtime ID.

## 3) Ingredient Prefab Rule

All ingredient prefabs must be variants of:
`Assets/@Resources/Prefabs/Props/Interactables/PileObjectBase.prefab`

Setup:
1. Create prefab variant from `PileObjectBase`.
2. Add ingredient-specific visual mesh/FBX only.
3. Configure `TrayItemBehavior`: `Data` = matching `IngredientData`, `CanBeTrash` per rule.

## 4) Register In Global Database

1. Add asset to `DatabasePileable.data`.
2. Ensure `GameManager.databasePileIngredient` references that `DatabasePileable`.
3. Without this, `GameManager.SpawnIngredient(id)` fails.

## 5) Station Components

### 5.1 Ingredient Station

Inspector: `Construction Area`, `Pile` (IngredientPile), `Interaction` (WorkerInteraction), `Ingredient Data`, `Spawn Position`, `Non Automatic`.

- Auto loop spawns while pile count < max (unless `Non Automatic`).
- Worker interaction transfers pile to tray.
- Note: `SpawnIngredientToPile()` currently uses `transform.position`, not `spawnPosition`.

### 5.2 Ingredient Absorber

Inspector: `Worker Pos`, `Accepted Ingredient`, `Have Max Input`, `Max Input`, `Absorb Transform`, `On Ingredient Absorbed`.

- Consumes one matching tray ingredient by ID.
- `Worker Pos` is a marker field, not used in runtime.

### 5.3 Timed Object Behavior

Inspector: `Time Duration`, `Require Worker`, `Worker Interaction`, `OnTimeStart`, `OnTimeEnd`, `OnDurationProgress`.

- With `Require Worker = true`, timer pauses when worker leaves trigger.
- Wire `OnDurationProgress` -> `UI_TimerProgress.SetPercentage(float)` for visual.

## 6) Quest Unlock Setup (Quest Machine)

1. Create `QuestMachineQuestData` ScriptableObject.
2. Assign `targetQuest` and `rewardData`.
3. Add to `QuestMachineManager.currentLevelQuestDatabase`.
4. Custom actions: `QuestActionSetUnlockableState`, `QuestActionGiveReward`.
5. Message listener: sender `unlockableStation`, message `unlocked`, parameter = exact asset name.

## 7) Validation Checklist

Before testing:
1. Ingredient prefab is a `PileObjectBase` variant.
2. `TrayItemBehavior.Data` points to correct `IngredientData`.
3. Ingredient exists in `DatabasePileable`.
4. `GameManager.databasePileIngredient` references that database.
5. Station refs (Pile, Interaction, Ingredient Data) are assigned.
6. Absorber `Accepted Ingredient` matches intended ingredient ID.
7. Timed object has valid `Worker Interaction` when worker is required.
8. Quest message listener matches sender/message/parameter exactly.
