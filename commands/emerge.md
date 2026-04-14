---
name: thinking-partner:emerge
description: >
  Identifies patterns coalescing into something bigger. Finds clusters of related ideas
  in your vault that could become a project, essay, or product. Shows what's emerging
  and which notes connect to it.
---

## Emerge — Surface What's Taking Shape

This command detects idea clusters in the vault that have reached critical mass. Scattered notes that individually seem unrelated but together point toward a project, essay, or product.

### Input

No arguments required:

```
/emerge
```

Optional: narrow to a domain:

```
/emerge --domain content
/emerge --domain business
/emerge --domain tools
```

### Execution Steps

#### 1. Resolve config

Invoke `manifest-resolver` for domain `thinking-partner`. Required keys: `vault`. Reasoning profile keys used: `values`, `work-style`, `identity`.

Read the resolved reference files to understand what the user is currently prioritizing. This context separates "interesting cluster" from "actionable emergence."

#### 2. Map the vault's connection graph

Run these scans in parallel to build a structural picture:

**Dense nodes (ideas with gravity):**
```
obsidian search query="*" limit=50
```
For the top results, check backlinks:
```
obsidian backlinks file="{note}"
```
Notes with 4+ backlinks are hub candidates. These are ideas that other ideas keep pointing at.

**Orphans and loose ends:**
```
obsidian orphans
obsidian unresolved
obsidian deadends
```
Orphans near a cluster are the most interesting signal: they haven't been connected yet, but they belong.

**Tag density:**
```
obsidian tags counts sort=count
```
Tags with 5+ notes suggest a theme. Tags that share notes suggest convergence.

**Recent momentum:**
List recently modified notes in the vault:
```
obsidian files limit=30
```

Read the content of high-signal notes (hub nodes, recent notes, orphans that seem thematically related). Up to 25 notes.

#### 3. Detect clusters

A cluster is a group of 3+ notes that:
- Link to each other (directly or through a shared hub)
- Share tags or vocabulary
- Address the same underlying question from different angles
- Were created or modified within a similar time window

For each potential cluster, assess:

**Density** — how tightly connected are the notes? (many cross-links = dense, only tag overlap = loose)

**Completeness** — does the cluster have enough material to become something? A project needs a problem + approach + resources. An essay needs a thesis + evidence + insight. A product needs a pain point + mechanism + audience.

**Momentum** — is this cluster growing? Recent notes joining an old cluster = active emergence. Stale cluster with no recent additions = dormant.

**Missing pieces** — what would need to exist for this cluster to become actionable? A missing note is more useful than a present one sometimes.

#### 4. Classify emergence stage

Each cluster gets one of three stages:

| Stage | Meaning | Suggestion |
|-------|---------|------------|
| **Seed** | 3-4 notes touching the same theme, loosely connected. The pattern exists but needs deliberate development. | Write 1-2 more notes to test if the idea has legs |
| **Forming** | 5-8 notes with clear cross-links and a discernible thesis or problem statement. Could become something with focused effort. | Outline the project/essay/product and identify gaps |
| **Ready** | 8+ notes, strong internal links, clear thesis, most building blocks present. Waiting for someone to assemble them. | Commit a week to turning this into a concrete output |

#### 5. Generate cluster canvas

For clusters at **Forming** or **Ready** stage, generate a `.canvas` file using `obsidian:json-canvas` that visualizes the cluster structure:

- **File nodes** linking to the actual vault notes in the cluster (use `type: "file"` with the note path)
- **Text nodes** for the core question and missing pieces
- **Edges** representing the connections between notes (backlinks, shared tags, thematic links)
- **Groups** for each cluster, labeled with the cluster name and stage
- **Color coding:** Ready clusters (green/color 4), Forming (yellow/color 1), Seeds (grey)
- **Orphans** placed near but outside their likely cluster group, with dashed edges suggesting the connection

Save to the directory resolved for `canvas-output`. This becomes a living map the user can drag, annotate, and connect as clusters evolve.

#### 6. Present the emergence report

Output format:

```
## Emergence Report — {date}

**Vault scanned:** {notes examined} notes across {folders}
**Clusters detected:** {count}

---

### 1. {Cluster Name} — [{Seed | Forming | Ready}]

**Core question:** {the underlying question or problem this cluster orbits}

**Connected notes:**
- [[Note A]] — {role in cluster: thesis, evidence, example, counterpoint, etc.}
- [[Note B]] — {role}
- [[Note C]] — {role}
- ...

**Nearby orphans:** [[Orphan X]], [[Orphan Y]] — {why they likely belong}

**Unresolved links:** [[Missing Note]] — {what this gap represents}

**Could become:**
- {Project / Essay / Product / Framework} — {one-sentence description of what this would look like fully realized}

**Missing to get there:** {1-3 specific gaps: a note that needs writing, a question that needs answering, a decision that needs making}

---

### 2. {Cluster Name} — [{stage}]
...

---

### Dormant Clusters
{Clusters that were once active but haven't had new notes in 30+ days. Worth deciding: revive or abandon.}

| Cluster | Last Activity | Notes | Status |
|---------|--------------|-------|--------|
| {name} | {date} | {count} | Stalled / Waiting / Abandoned? |

---

**Strongest emergence:** {the single cluster closest to becoming something real, with a one-sentence recommendation}
```

### Calibration Rules

- **3 notes minimum.** Two related notes are a coincidence. Three are a pattern. Don't report clusters below this threshold.
- **Name the core question, not the topic.** "AI tooling" is a topic. "Can internal AI tools replace the need to hire specialists?" is a core question. The question reveals what makes the cluster interesting.
- **Roles matter more than lists.** Don't just list connected notes. Explain what role each plays: is it the thesis, an example, a counterpoint, evidence, a related framework? This shows the cluster's structure, not just its membership.
- **Orphans near clusters are the key insight.** An orphan note sitting one concept away from a dense cluster is the most actionable finding. It means the user wrote something relevant but hasn't connected it yet. Surfacing this connection is the primary value of the command.
- **Don't oversell seeds.** A seed cluster is interesting, not urgent. A forming cluster deserves attention. A ready cluster deserves action. Match the tone to the stage.
- **Dormant clusters need a verdict.** If a cluster hasn't grown in 30+ days, it's either waiting for something (flag what) or it was a passing interest. Help the user decide: revive or let go.
- **Maximum 5 active clusters per report.** More than that dilutes attention. If you find more, keep the top 5 by stage (ready > forming > seed) and mention the rest in a "Also detected" line.

### What This Command Is NOT

- An idea generator (use `/ideas` for new ideas)
- A stress test (use `/challenge` to pressure-test a specific position)
- A search tool (use standard search for targeted information retrieval)

Emerge shows you what your vault already knows but you haven't noticed yet. The ideas are already there. This command assembles them.
