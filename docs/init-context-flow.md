# Init Context Flow

```mermaid
flowchart TD
    subgraph SETUP["1. New Branch Setup"]
        A["Delete old Unity repo"] --> B["git clone + checkout branch"]
        B --> C["Open Claude Code"]
        C --> D["Say 'init context'"]
    end

    subgraph STABLE["2. Read Stable Docs (outside repo — survives deletion)"]
        E["GAME_CONTEXT.md\nCore loop, controls, progression"]
        F["SYSTEM_AUTHORING_GUIDE.md\nIngredients, stations, quests"]
    end

    subgraph GENERATE["3. Scan Codebase + Generate Docs"]
        G["Scan Assets/@Scripts/"]
        H["CODE_MAP.md\nEvery script + folder"]
        I["ARCHITECTURE.md\nRuntime layers, data model"]
        J["INTERACTION_FLOW.md\nGameplay loops, debug points"]
    end

    subgraph BRANCH["4. Feature Branch Context"]
        K["Ask: branch name + goal"]
        L["Read Outline KB\nfor design specs"]
        M["FEATURE_BRANCH.md\nScope, systems, test plan"]
    end

    subgraph VIBE["5. Vibe-Code"]
        N["Start coding with full context"]
        O["AI auto-updates docs\nas code changes"]
    end

    D --> E
    D --> F
    E --> G
    F --> G
    G --> H
    G --> I
    G --> J
    H --> K
    I --> K
    J --> K
    K --> L
    L --> M
    M --> N
    N --> O
```

## File Structure

```
Firepit-Claude/
│
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
