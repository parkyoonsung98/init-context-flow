# Camp001Project — Chef Ready (Unity)

## Required Reading

Before making any code changes, read these docs:

1. `../../docs/GAME_CONTEXT.md` — game design, core loop, order model (stable, lives outside repo)
2. `../../docs/SYSTEM_AUTHORING_GUIDE.md` — how to add ingredients/stations/quests (stable, lives outside repo)
3. `docs/CODE_MAP.md` — current codebase structure (generated, may need regeneration)
4. `docs/ARCHITECTURE.md` — runtime layers and system relationships (generated, may need regeneration)
5. `docs/INTERACTION_FLOW.md` — gameplay loops and debug entry points (generated, may need regeneration)

If docs 3-5 are missing, run the **init context** workflow described in `../../CLAUDE.md`.

## Source Of Truth

- Game design context, feature intent, balancing notes, and team decisions are in the Outline knowledge base.
- Outline is authoritative. If local docs and Outline conflict, Outline is correct.
- Use `OUTLINE_BASE_URL` and `OUTLINE_API_KEY` from environment variables.
- Never hardcode secrets in code, prompts, scripts, or docs.

## Code Structure Guardrails

- Preserve existing folder structure, namespaces, scene flow, and dependency direction unless explicitly approved.
- Do not perform broad refactors or reorganize core systems without sign-off.
- Do not introduce new frameworks, SDKs, or foundational patterns without approval.
- Prefer small, focused feature changes that fit current module boundaries.
- For high-impact changes, propose the plan first and wait for approval before coding.

## Unity Repository Hygiene

- `Library/`, `Temp/`, and `Logs/` are generated — never commit or manually edit them.
- Avoid manual edits to generated `.csproj`/`.sln` files.
- Keep commits scoped to the requested feature or fix.

## Doc Maintenance Rule

After completing a feature that adds, removes, or renames systems, scripts, folders, or changes architectural patterns, update the relevant doc in `docs/`:

- New/removed scripts or folders -> update `CODE_MAP.md`
- New system relationships or manager changes -> update `ARCHITECTURE.md`
- New interaction flows or changed loops -> update `INTERACTION_FLOW.md`
- New feature work -> update or create `FEATURE_BRANCH_*.md`

Keep updates scoped to what actually changed. Do not rewrite entire documents.

## Unity MCP Setup

- Package: `com.coplaydev.unity-mcp` (in `Packages/manifest.json`).
- Dependencies: Python 3.10+ and `uv` on PATH.
- Start server: Unity menu `Window > MCP for Unity > Start Server`.
- Endpoint: `http://127.0.0.1:8080/mcp`.
