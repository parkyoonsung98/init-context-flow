# Chef Ready — Game Context

> Stable reference extracted from Outline KB. Update when game design changes significantly.

## Source Documents (Outline)

- `Chef Ready > Overview` (`900gtKbubg`)
- `Chef Ready > Core Gameplay` (`pWd9cKNiYT`)

## Game Summary

- Chef Ready is an idle arcade cooking simulation focused on active kitchen play.
- The player directly controls a chef under time pressure (orders queue up, food can burn, customers can leave).
- Core value proposition: active cooking tension and moment-to-moment decisions, not passive carry-item automation.

## Core Loop (Infinite 5-Step Cycle)

1. **Order**: customer places order at counter.
2. **Produce**: player gathers ingredients and cooks (chop, grill, fry).
3. **Serve**: player combines ingredients correctly and delivers.
4. **Reward**: customer pays (currency collection can be automated by Pet).
5. **Maintain**: clear/wash dishes to reset table (can be automated by Dishwasher/Robot Cleaner).

## Controls Baseline

- One-handed virtual joystick movement.
- Auto pick-up/put when stopping near stations.
- Processing occurs by staying near processing stations (progress bar based).
- Auto-serve triggers when near customer with correct item.

## Progression Baseline

- Start with manual serving, then earn Cash to upgrade stations/tables.
- Upgrades generate Stars (XP), and accumulated Stars trigger Level Up.
- Early unlock milestones:
  - Level 2: District area (cleaning room/staff)
  - Level 3: drink menu/station
  - Level 4-6: cheese/bacon/ice cream menus

## Product Direction

- Phase 1 viability focus.
- Android-first soft launch target around May 2026.

## Order Model

- Customer order is a list of recipes, not a burger-count.
- Categories: `Main`, `Side`, `Drink` — at most one recipe per category, at least one total.
- A recipe is completed only when its full required ingredient set is delivered.
- Partial delivery does not complete a recipe.
- Merge stack behavior is intentionally out of scope.
