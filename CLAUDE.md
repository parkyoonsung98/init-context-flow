# Firepit Workspace

This is the top-level workspace for the Firepit startup project.

## Directory Layout

- `Firepit-OS/`: Discord bot and team tooling (Python). Manages weekly status, Mermaid diagrams, and Outline integration. Deploys to GCP.
- `Fork/Camp001Project/`: Unity game project for "Chef Ready" — an idle arcade cooking sim targeting Android soft launch. This repo is disposable (cloned fresh per branch).
- `docs/`: Stable project knowledge that survives repo deletion.
- `templates/`: Doc templates used by "init context" to generate per-branch context docs.

## General Rules

- Outline is the source of truth for project docs, game design, and team context.
- Never hardcode tokens, API keys, or secrets in code or docs. Use `.env` or shell environment.
- Use `OUTLINE_BASE_URL` and `OUTLINE_API_KEY` from the environment when accessing Outline. Credentials are in `Firepit-OS/.env`.

## Stable Docs (Always Read)

These live outside the Unity repo and survive repo deletion:

- `docs/GAME_CONTEXT.md` — game design, core loop, controls, progression, order model
- `docs/SYSTEM_AUTHORING_GUIDE.md` — how to add ingredients, stations, quests in Unity

## Init Context Workflow

When the user says **"init context"**, or when `Fork/Camp001Project/docs/` is missing or empty:

1. Read the stable docs above for game/design knowledge.
2. Copy templates from `templates/` into `Fork/Camp001Project/docs/`.
3. Scan `Assets/@Scripts/` and fill `CODE_MAP.md` — list every script folder and its contents with one-line descriptions.
4. Read key manager/system scripts and fill `ARCHITECTURE.md` — document runtime layers, boot flow, data model, eventing.
5. Trace gameplay loops through the code and fill `INTERACTION_FLOW.md` — document step-by-step flows for each core loop stage.
6. Ask the user for the branch name and goal, then fill `FEATURE_BRANCH.md`.

## Doc Maintenance Rule

After completing a feature that adds, removes, or renames systems, scripts, folders, or changes architectural patterns, update the relevant generated doc inside `Fork/Camp001Project/docs/`:

- New/removed scripts or folders -> update `CODE_MAP.md`
- New system relationships or manager changes -> update `ARCHITECTURE.md`
- New interaction flows or changed loops -> update `INTERACTION_FLOW.md`

Keep updates scoped to what actually changed. Do not rewrite entire documents.

## Sub-Project Instructions

- See `Firepit-OS/CLAUDE.md` for Discord bot workflows and deployment.
- See `Fork/Camp001Project/CLAUDE.md` for Unity project guardrails.
