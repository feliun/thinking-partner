---
name: thinking-partner:ideas
description: >
  Scans your vault and generates a full idea report. Surfaces tools to build, people to meet,
  subjects to investigate, and things to write, all grounded in your actual interests and patterns.
---

## Ideas — Pattern-Driven Idea Generation

This command performs a deep scan of the vault to detect emerging themes, recurring interests, and untapped connections, then generates actionable ideas across four categories.

### Input

No arguments required. Just invoke:

```
/ideas
```

Optional: narrow scope with a domain hint:

```
/ideas --focus content
/ideas --focus business
/ideas --focus tools
```

### Execution Steps

#### 1. Resolve config

Invoke `manifest-resolver` for domain `thinking-partner`. Required keys: `vault`. Reasoning profile keys used: `values`, `work-style`, `identity`, `thinking-style`.

Read the resolved reference files to calibrate idea generation against the user's actual priorities. These ensure ideas are relevant to where the user actually is, not generic suggestions.

#### 2. Wide vault scan

Run multiple searches in parallel to build a comprehensive picture of current thinking:

**Recent activity:**
```
obsidian files limit=40
```
If `daily-notes` resolved, also list its most recent files.

**Recurring themes:**
```
obsidian tags counts sort=count
obsidian search query="TODO" limit=10
```

**Structural signals:**
```
obsidian orphans
obsidian deadends
obsidian unresolved
```

Read the content of the most relevant notes found (up to 20 notes). Focus on:
- Notes created or modified in the last 30 days
- Notes with many backlinks (hub topics)
- Orphan notes that might represent unexplored threads
- Unresolved links (things the user referenced but hasn't written about yet)
- Recurring tags that indicate sustained interest

If a `--focus` flag was provided, weight searches toward that domain.

#### 3. Detect patterns

Analyze the collected material for:

- **Clusters** — topics that appear across 3+ notes without being explicitly connected
- **Momentum** — subjects the user keeps returning to (recent + frequent mentions)
- **Gaps** — areas referenced but underdeveloped (unresolved links, orphan notes, sparse tags)
- **Contradictions** — tensions between notes that could become interesting content
- **Convergence** — ideas from different domains that point toward the same insight

#### 4. Generate ideas across four categories

For each category, produce 3-5 ideas. Every idea must:
- Be grounded in specific vault content (cite `[[notes]]`)
- Explain *why* this idea surfaces now (what pattern triggered it)
- Be concrete enough to act on within a week

**A. Things to Build**
Tools, automations, systems, or products. Bias toward:
- Things that remove recurring friction the user has written about
- Tools that compound (build once, benefit forever)
- Internal tools before external products

**B. People to Reach Out To**
Connections to make or reactivate. Based on:
- Names mentioned in notes but not in contacts
- People connected to the user's current focus areas
- Dormant relationships relevant to active projects
- Potential collaborators for ideas in progress

**C. Subjects to Investigate**
Research threads worth pulling. Based on:
- Questions the user has asked in notes but not answered
- Unresolved links (concepts referenced but never written up)
- Gaps in frameworks they're building
- Adjacent fields that could sharpen existing thinking

**D. Things to Write**
Content ideas for essays, newsletters, posts, or vault pieces. Based on:
- Clusters with enough material for a piece but no published output
- Contradictions that would make compelling content
- Frameworks that are mature enough to share
- Positions the user holds that counter conventional wisdom

#### 5. Generate idea network canvas

Generate a `.canvas` file using `obsidian:json-canvas` that visualizes the idea landscape:

- **File nodes** for vault notes that anchor each idea (use `type: "file"` with the note path)
- **Text nodes** for each generated idea, color-coded by category:
  - Build (blue/color 6)
  - People (green/color 4)
  - Investigate (yellow/color 1)
  - Write (purple/color 2)
- **Edges** connecting ideas to their source notes
- **Groups** for each category
- **A central node** for the "Strongest signal" idea, larger and highlighted

Save to the directory resolved for `canvas-output` (e.g., `{canvas-output}/Ideas — {date}.canvas`). This gives the user a visual map to drag ideas around, connect them, and promote the best ones into action.

#### 6. Present the report

Output format:

```
## Idea Report — {date}

**Vault snapshot:** {total notes scanned} notes, {recent count} from last 30 days
**Top clusters detected:** {3-4 theme labels}

---

### Things to Build
| # | Idea | Why Now | Vault Anchors |
|---|------|---------|---------------|
| 1 | {concrete idea} | {pattern that triggered it} | [[Note]], [[Note]] |
| 2 | ... | ... | ... |

### People to Reach Out To
| # | Who | Why | Connection Point |
|---|-----|-----|-----------------|
| 1 | {name or archetype} | {reason} | [[Note]] |
| 2 | ... | ... | ... |

### Subjects to Investigate
| # | Topic | Why | Starting Point |
|---|-------|-----|----------------|
| 1 | {topic} | {gap or question found} | [[Note]], unresolved: [[X]] |
| 2 | ... | ... | ... |

### Things to Write
| # | Idea | Format | Source Material |
|---|------|--------|----------------|
| 1 | {angle or title} | Essay / Newsletter / Post | [[Note]], [[Note]] |
| 2 | ... | ... | ... |

---

**Strongest signal:** {the single most compelling idea from any category, with a one-sentence argument for why}
```

### Calibration Rules

- **No generic ideas.** "Write about leadership" is useless. "Write about why most founders confuse delegation with abdication, using the framework in [[Founder dependency]]" is useful. Every idea must be specific to this vault.
- **Cite or cut.** If an idea can't point to at least one vault note, it's speculation, not a pattern. Drop it.
- **Respect current priorities.** If the vault or reference files indicate active priorities, ideas aligned with those get priority. Flag ideas that are interesting but off-strategy.
- **Orphans are gold.** Unresolved links and orphan notes are the highest-signal source for ideas. They represent things the user thought were worth mentioning but hasn't developed yet.
- **Quality over quantity.** 3 strong ideas per category beats 5 mediocre ones. If a category has fewer than 3 genuine ideas, say so rather than padding.
- **"People to Reach Out To" can be archetypes.** If no specific name emerges, describe the type of person (e.g., "someone building in the AI-for-ops space") with enough detail to be actionable.

### What This Command Is NOT

- A cluster detector (use `/emerge` for that)
- A content creator (use dedicated content commands)
- A task generator (ideas are suggestions, not commitments)

Ideas surfaces what your vault is trying to tell you. It finds the patterns you're too close to see.
