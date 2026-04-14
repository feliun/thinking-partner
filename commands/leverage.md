---
name: thinking-partner:leverage
description: >
  Identifies the 3-7 skills, knowledge domains, or capabilities where concentrated investment
  would produce step-function breakthroughs across multiple areas of your life and work.
  Maps constraints from your vault and weekly reviews, then prescribes solutions from any domain.
---

## Leverage — Find Your Highest-ROI Learning Investments

This command scans the vault to identify what's actually constrained, then finds the specific skills, knowledge domains, mental models, or capabilities where 50-100 hours of focused development would crack open multiple stuck things simultaneously. The vault is the diagnostic tool. The solutions come from anywhere.

### Input

```
/leverage
```

Optional: focus on a specific domain:

```
/leverage {domain}
```

Examples:
- `/leverage` — full scan across all constraints
- `/leverage leadership` — focused on leadership and delegation constraints
- `/leverage product` — focused on constraints blocking your product work

### What Makes This Different

This is NOT:
- `/ideas` — broad idea generation across categories
- `/emerge` — implicit ideas the vault hasn't stated
- `/challenge` — pressure-testing a specific belief
- `/strategise` — competitive positioning via 7 Powers

This IS: identifying the 3-7 things where investing 50-100 hours of deep learning or practice would produce step-function changes in capability, output, or trajectory. The things where the ROI on attention is 10x-100x, not incremental.

**The test:** A true leverage point, when developed, unlocks progress in 3+ areas simultaneously. If it only helps one thing, it's a task, not leverage.

### Execution Steps

#### 1. Resolve config

Invoke `manifest-resolver` for domain `thinking-partner`. Required keys: `vault`. Reasoning profile keys used: `thinking-style`, `values`, `work-style`, `identity`. Optional data keys used: `weekly-reviews`, `daily-notes`.

Read the resolved reference files. These establish what matters, what's realistic, and what trade-offs are deliberate vs. accidental. If `weekly-reviews` or `daily-notes` didn't resolve, note with ⚠️ and proceed with vault-wide searches instead — the diagnostic will be less precise but still useful.

#### 2. Map constraints from the vault

This phase is diagnostic. Before looking for leverage, map what's actually constrained. Breakthroughs only matter relative to bottlenecks.

**Step 2a: Structural scan**

```
obsidian tags counts sort=count
obsidian orphans
obsidian deadends
obsidian unresolved
```

**Step 2b: Weekly review archaeology** (if `weekly-reviews` resolved)

This is the richest diagnostic source. Read the last 4-6 weekly reviews from the resolved directory. Extract with precision:

- **Recurring constraints** — the same bottleneck named across multiple weeks
- **Delegation failures** — tasks that keep appearing in "what someone else could have done"
- **Calendar compliance failures** — which rules break repeatedly and why
- **Trend lines** — which dimensions are declining, not improving
- **Hard questions dodged** — questions posed in reviews that never got answered
- **Refocus directives ignored** — advice given to self that wasn't followed

**Step 2c: Daily note signals** (if `daily-notes` resolved)

Read recent daily notes for:

- **Repeated frustrations** — the same friction appearing 3+ times signals a missing skill or model
- **Abandoned attempts** — things started and stopped. Why? What was missing?
- **Admiration signals** — people, work, or capabilities described with envy or aspiration
- **"I wish I could..." and "I need to learn..."** statements
- **Energy patterns** — what produces flow? What drains? Flow signals proximity to leverage
- **Requests for help** — what keeps getting asked of others? That dependency is a potential leverage point
- **Decisions deferred** — what keeps getting punted? Deferred decisions often signal missing frameworks

**Step 2d: Behavioral archaeology**

```
obsidian search query="stuck" limit=10
obsidian search query="frustrated" limit=10
obsidian search query="don't know how" limit=10
obsidian search query="need to learn" limit=10
obsidian search query="wish I" limit=10
obsidian search query="blocked" limit=10
obsidian search query="waiting on" limit=10
obsidian search query="delegated" limit=10
obsidian search query="should have" limit=10
obsidian search query="get better at" limit=10
```

Also search for aspiration and admiration signals:
```
obsidian search query="impressive" limit=5
obsidian search query="how did" limit=5
obsidian search query="want to be" limit=5
```

**Step 2e: Project audit**

For each active project/theme found in the vault, answer:
- What is the binding constraint on progress right now?
- Is the constraint a skill, a relationship, a decision, knowledge, or time?
- If the constraint is a skill or knowledge gap, what specifically is missing?
- How many OTHER projects share this same constraint?

Constraints shared across 3+ projects are the highest-leverage targets.

#### 3. Output the constraint map

Before moving to solutions, present the diagnostic clearly:

```
## Constraint Map

### Recurring Frictions
{For each: what it is, how often it appears, what domains it affects}

### Capability Gaps
{Skills/knowledge the vault reveals as missing. For each: evidence from vault, which projects it blocks}

### Dependency Points
{Things that require other people because the skill doesn't exist internally. For each: who currently fills this, what it costs in time/money/autonomy}

### Decision Bottlenecks
{Choices that keep getting deferred. For each: what framework or knowledge would make the decision clear}

### Behavioral Patterns
{Patterns that repeat despite awareness — the "knowing but not doing" gaps. These often signal a missing model or skill, not just discipline.}
```

#### 4. Detect leverage points

Six methods, ordered by reliability. Apply all six, then consolidate.

**Method 1: Bottleneck Convergence (Highest Reliability)**

Find skills or knowledge gaps that are the binding constraint across 3+ domains simultaneously.

Process:
1. Take the constraint map from Step 3
2. For each constraint, list every project/domain it touches
3. Rank by number of domains affected
4. The constraint appearing in the most domains is the highest-leverage skill to develop

**Method 2: Adjacent Possible (High Reliability)**

Find capabilities that are 80% developed but missing the final 20% that would make them powerful.

Look for:
- Skills used informally that have never been formalized or deepened
- Knowledge referenced but never systematically studied
- Tools used at surface level with deep capabilities unused
- Frameworks applied intuitively that, if made explicit, would become transferable

```
obsidian search query="started learning" limit=5
obsidian search query="basics of" limit=5
obsidian search query="should go deeper" limit=5
obsidian search query="course" limit=5
```

**Method 3: Multiplier Models (High Reliability)**

Find mental models or frameworks that, once internalized, would change how decisions are made across all domains.

Look for:
- Decisions made badly or slowly across reviews (what framework is missing?)
- The same mistake pattern in different contexts (what model would prevent it?)
- Advice consistently sought from others (what do they know that you don't?)
- Books or thinkers referenced with admiration but not internalized

A multiplier model changes how you process ALL future information.

**Method 4: Removal Leverage (Medium Reliability)**

Find things that, if eliminated or automated, would free up disproportionate cognitive or temporal bandwidth. Not "what should I learn?" but "what should I stop doing manually so I can learn?"

Look for:
- Tasks that keep appearing in delegation audits
- Calendar rule violations that repeat
- Low-leverage activities consuming significant time
- Manual processes mentioned in daily notes

For each candidate: how much time per week? Could it be automated, delegated, or eliminated? What would you do with the freed time?

**Method 5: Relationship Leverage (Medium Reliability)**

Find knowledge domains or skills that would dramatically increase the value of existing relationships or unlock new ones.

```
obsidian search query="meeting with" limit=10
obsidian search query="conversation with" limit=10
obsidian search query="network" limit=5
obsidian search query="mentor" limit=5
```

**Method 6: Identity Leverage (Use Sparingly)**

Find the gap between who the vault says the user is and who they would need to become for their stated goals to be achievable.

Cross-reference:
- Self-descriptions in `identity.md` vs. capabilities required by the user's stated projects
- Aspirational statements in journal entries vs. weekly review reality
- Roles avoided that the trajectory demands

#### 5. Beyond the vault

**This is the most important phase.** The vault shows what the user is already thinking about. The most powerful leverage points are often things the vault has NEVER mentioned, because they exist in domains outside current awareness.

**Blind spot analysis:**

Based on constraints mapped in Steps 2-3, identify skills and knowledge domains that are completely absent from the vault but would be transformative if developed.

Think across:
- **Adjacent fields** — disciplines that neighbor the user's work but they've never studied formally
- **Foundational disciplines** — underlying fields that would upgrade everything (statistics, rhetoric, organizational design, performance psychology)
- **Counter-intuitive domains** — fields that seem irrelevant but contain transferable frameworks (military strategy for resource allocation, game design for engagement, ecology for community building)
- **Historical parallels** — what did people in similar positions learn that created their breakthrough?

**The outsider's prescription:**

If a world-class strategic advisor reviewed the vault's constraints with no loyalty to the current plan, what would they prescribe?

**Imported frameworks:**

For each constraint from the map, ask: "What field has already solved this problem?" Don't reinvent. Import.

#### 6. Verify each leverage point

For each candidate, run these filters:

| Filter | Question | Fail = downgrade |
|--------|----------|-----------------|
| **3+ Domain Test** | Does developing this unlock progress in 3+ separate domains? | If only 1 domain, it's useful but not leverage |
| **Evidence Test** | Is there vault evidence of this constraint causing problems? (For beyond-vault points: clear logical chain from skill to constraint?) | No evidence = speculative |
| **Feasibility Test** | Can this be developed with 50-100 hours of focused effort? | If 1,000+ hours, flag as long-term |
| **Counterfactual Test** | If you had this 6 months ago, what specific things would have gone differently? | If you can't name specifics, it's theoretical |
| **Already-Tried Test** | Has this been attempted and abandoned? If yes, why? Is the blocker itself a leverage point? | Repeated failure to develop = the real leverage point is elsewhere |
| **Compound Test** | Does this get more valuable over time, or is it a one-time unlock? | Compound > one-time |

#### 7. Check for prior runs

```
obsidian search query="leverage point" limit=5
obsidian search query="leverage" limit=5
```

If prior leverage analyses found:
- Which points were identified before? Were they developed?
- If developed: did the predicted breakthrough occur?
- If not developed: why not? Is the blocker itself a leverage point?
- Do not re-suggest points previously identified and ignored without addressing why they were ignored

#### 8. Generate leverage canvas

Generate a `.canvas` file using `obsidian:json-canvas` that visualizes the leverage landscape:

- **Text nodes** for each leverage point, sized by impact, color-coded by source:
  - Vault-sourced (blue/color 6)
  - Beyond-vault (orange/color 1)
  - Blind spot (red/color 2)
- **File nodes** linking to vault notes that evidence each constraint
- **Edges** connecting leverage points to the constraints they resolve
- **Groups** for "Constraint Map" and "Leverage Points"
- **A central node** for the #1 leverage point, larger and highlighted (green/color 4)

Save to the directory resolved for `canvas-output`.

#### 9. Present the report

```
## Leverage Report — {date}

**Vault scanned:** {notes examined}, {weekly reviews analyzed}
**Constraints mapped:** {count}
**Leverage points identified:** {count}

---

### Constraint Map Summary

{Brief summary of the top 3-5 constraints, with cross-domain impact scores}

---

### Leverage Point 1: {Name}

**What it is:** {One sentence. Specific skill, knowledge domain, mental model, or capability.}

**Source:** {Vault-sourced / Beyond-vault / Blind spot}

**The constraint it breaks:** {What specific friction this resolves, citing evidence}

**Domains it unlocks:** {List every project/domain that benefits, with HOW for each}

**The counterfactual:** {What would have gone differently in the last 6 months}

**How to develop it:**
- **First 10 hours:** {specific starting point — which book, course, person, or practice}
- **Next 40 hours:** {deepening — applied practice on which project}
- **Final 50 hours:** {mastery path — what competence looks like}

**Compound potential:** {Does this get more valuable over time? How?}

**Feasibility:** {Hours required. Realistic timeline. What gets deprioritized.}

**Confidence:** {High / Medium / Low — with reasoning}

---

### Leverage Point 2: {Name}
...

---

### The Ranking

{Order by: (domains unlocked x constraint severity x compound potential) / effort required}

### The #1 Leverage Point

{The single thing that, if developed over the next 90 days, would produce the most dramatic shift. Why this one above all others.}

### The Surprising One

{The leverage point the user would never have identified themselves. From outside the vault's frame entirely. A domain that seems unrelated but would crack open the constraints the vault reveals.}

### The Prerequisite Chain

{If some leverage points depend on others, show the sequence. Start with the foundation.}

### The Anti-Leverage List

Things that FEEL high-leverage but aren't, based on evidence:

| Feels Like Leverage | Why It Isn't | Do This Instead |
|---------------------|-------------|----------------|
| {skill/domain} | {evidence it wouldn't change outcomes} | {what actually would} |

---

**Notes reviewed:** [[Note 1]], [[Note 2]], ...
**Weekly reviews analyzed:** {list, if applicable}
**Canvas:** [[Leverage — {date}]]
```

### Calibration Rules

- **The vault is the stethoscope, not the pharmacy.** Use it to diagnose. Draw solutions from any domain, any field, any discipline. The most transformative leverage points are often things the vault has never mentioned.
- **Cite or cut.** For vault-sourced leverage points, cite specific evidence. For beyond-vault points, show the logical chain: vault constraint → why this external domain addresses it.
- **Weekly reviews are the primary diagnostic.** When they exist, patterns across 4+ weeks are more reliable than any single vault search.
- **Specificity or silence.** "Learn negotiation" is generic. "Learn to structure equity-for-services deals so you can acquire talent without cash" is leverage. Every point must be specific to the user's actual constraints.
- **Fewer, stronger.** 3 high-confidence leverage points beat 10 speculative ones. If a method produces weak results, report "method did not yield strong signals" — don't pad.
- **The development path must be concrete enough to start tomorrow.** Not "learn finance" but "read [specific book], then apply the framework to [specific project], then [specific next step]."
- **The anti-leverage list is as valuable as the leverage list.** Knowing what NOT to invest in saves as much time as knowing what to invest in.
- **Account for capacity.** Every "how to develop" section must answer: what gets deprioritized to make room? Reference `work-style.md` if it resolved.
- **Comfort is a red flag.** The best leverage points feel slightly uncomfortable. If every suggestion is exciting and fun, you're optimizing for engagement, not impact.
- **Honest about repetition.** If the same leverage point keeps surfacing across runs and never gets developed, the real leverage point is whatever is preventing the development — not the skill itself.

### Anti-Patterns

1. **The Self-Help List** — Generic skills like "communication" or "leadership." Every point must be specific to actual constraints.
2. **The Interesting-But-Irrelevant** — Fascinating domains that don't connect to any active constraint. Intellectual curiosity is good. Calling it leverage is dishonest.
3. **The Already-Strong Skill** — Suggesting development where the vault shows existing competence. Leverage comes from filling gaps, not polishing strengths (unless the last 20% is transformative).
4. **The Time Fantasy** — Suggesting development requiring hundreds of hours when the vault shows no available time. Every suggestion must account for displacement.
5. **The Single-Domain Skill** — Skills that only help one project. Useful but not leverage. Leverage is definitionally multi-domain.
6. **The Motivation Trap** — "You should want to learn this" is not analysis. Stay with constraint evidence. Be creative for solutions.
7. **The Guru Recommendation** — Vague "study under so-and-so." The path must be concrete: specific resources, specific practice, specific milestones.
8. **The Meta-Skill Spiral** — "Learn how to learn" is only leverage when the learning process itself is the bottleneck. Usually the bottleneck is more specific.
9. **The Vault Ceiling** — Limiting solutions to things the vault mentions. The vault reveals constraints. Solutions come from anywhere.

### What This Command Is NOT

- An idea generator (use `/ideas` for new ideas to pursue)
- A belief audit (use `/challenge` to pressure-test positions)
- A competitive analysis (use `/strategise` for Power mapping)
- A pattern detector (use `/emerge` for idea clusters)
- A task list (leverage points are strategic investments, not to-dos)

Leverage finds the precise points where concentrated investment of thinking, learning, or skill-building would crack open multiple stuck things simultaneously. The vault reveals the constraints. The solutions can come from anywhere in the world.
