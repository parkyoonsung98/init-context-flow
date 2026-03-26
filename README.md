# Init Context Flow

AI context starter kit for vibe-coding Unity features on fresh branches.

## Problem

Every time you clone a new branch and start an AI coding session, you have to re-explain the entire project. This repo shows a workflow that solves that.

## Workflow

```mermaid
flowchart TD
    A["<b>Delete old repo</b><br/>remove previous clone"]:::red --> B["<b>Clone fresh branch</b><br/>git clone + checkout"]:::red
    B --> C["<b>Say init context</b><br/>triggers full workflow"]:::blue

    C -. reads .-> D["<b>GAME_CONTEXT.md</b><br/>core loop, controls"]:::green
    C -. reads .-> E["<b>AUTHORING_GUIDE.md</b><br/>stations, quests"]:::green

    D --> F["<b>Scan codebase</b><br/>Assets/@Scripts/"]:::purple
    E --> F

    F -- generates --> G["<b>CODE_MAP.md</b><br/>scripts + folders"]:::orange
    F -- generates --> H["<b>ARCHITECTURE.md</b><br/>layers, data model"]:::orange
    F -- generates --> I["<b>INTERACTION_FLOW.md</b><br/>loops, debug points"]:::orange

    G --> J{{"<b>Ask branch goal</b>"}}:::blue
    H --> J
    I --> J

    J -. reads .-> K["<b>Outline KB</b><br/>design specs"]:::purple
    K -- generates --> L["<b>FEATURE_BRANCH.md</b><br/>scope, test plan"]:::orange

    L --> M["<b>Start vibe-coding</b><br/>full project context"]:::blue
    M -. maintains .-> N(["<b>Auto-update docs</b><br/>syncs with code"]):::blue

    classDef red fill:#f8d7da,stroke:#c47a7e,color:#5a2328
    classDef blue fill:#d4e4f7,stroke:#7a9ec4,color:#1e3a5a
    classDef green fill:#d4edda,stroke:#7aba8a,color:#1a4028
    classDef orange fill:#fde8cd,stroke:#c4a46a,color:#5a4018
    classDef purple fill:#e8daf0,stroke:#a07ab8,color:#3a2248
```

## How It Works

1. **Delete old repo**, clone fresh branch from GitHub
2. Say **"init context"** to your AI coding assistant
3. AI reads stable docs (game design, authoring guide) that live outside the repo
4. AI scans the codebase and generates CODE_MAP, ARCHITECTURE, and INTERACTION_FLOW docs
5. AI asks for the branch goal and generates a FEATURE_BRANCH doc
6. Start vibe-coding with full context — AI auto-updates docs as code changes

## File Structure

```
├── CLAUDE.md                          ← auto-loaded, has init context workflow
├── .claudeignore                      ← excludes Library/, node_modules/, etc.
│
├── docs/                              ← STABLE (survives repo deletion)
│   ├── GAME_CONTEXT.md
│   └── SYSTEM_AUTHORING_GUIDE.md
│
├── templates/                         ← SKELETONS (copied + filled per branch)
│   ├── CODE_MAP.template.md
│   ├── ARCHITECTURE.template.md
│   ├── INTERACTION_FLOW.template.md
│   └── FEATURE_BRANCH.template.md
│
└── Fork/
    └── Camp001Project/                ← DISPOSABLE (cloned fresh per branch)
        ├── CLAUDE.md                  ← project rules + "read parent docs first"
        └── docs/                      ← GENERATED (by init context)
            ├── CODE_MAP.md
            ├── ARCHITECTURE.md
            ├── INTERACTION_FLOW.md
            └── FEATURE_BRANCH_*.md
```

### Key Idea

- **Stable docs** live outside the Unity repo — they survive deletion
- **Generated docs** live inside the Unity repo — rebuilt per branch by scanning actual code
- **Templates** ensure consistent structure every time

## Context

Built for Chef Ready, an idle arcade cooking sim for Android, using Claude Code + Unity.
