---
name: thinking-partner:challenge
description: >
  Pressure-tests your current beliefs. Finds contradictions, weak assumptions,
  and blind spots in your thinking on a topic. Use before big decisions or to stress-test ideas.
---

## Challenge — Stress-Test Your Thinking

This command audits your stated positions on a topic, surfaces contradictions between notes, and identifies assumptions that might not hold.

### Input

The user provides a topic after invoking the command:

```
/challenge {topic}
```

### Execution Steps

#### 0. Scope the challenge

Before searching, determine whether the topic is specific enough to produce a useful challenge. Ask clarifying questions using AskUserQuestion if:

- **The topic is too broad** — e.g., "leadership" could mean delegation, hiring, culture, founder role. Ask: "Which aspect of {topic} do you want me to pressure-test?"
- **The angle is unclear** — e.g., "AI" could mean your AI strategy, your beliefs about AI's impact, your tooling choices. Ask: "What specifically about {topic} are you questioning?"
- **There's an implicit decision** — if the user seems to be evaluating a choice (e.g., "challenge my thinking on pricing"), ask: "Are you considering a specific change, or do you want a general audit of your position?"

**Skip clarification when:**
- The topic is already specific (e.g., "founder dependency", "your content strategy", "your pricing model")
- The user added context after the topic (e.g., "/challenge hiring — I'm wondering if I should hire a CTO")
- There's only one plausible interpretation

Keep it to 1-2 questions max. The goal is focus, not interrogation.

#### 1. Resolve config

Invoke `manifest-resolver` for domain `thinking-partner`. Required keys: `vault`. Reasoning profile keys used: `thinking-style`, `values`, `work-style`.

Read the resolved reference files. These calibrate what counts as a real contradiction vs. a deliberate trade-off the user has already acknowledged. If any reference didn't resolve, note with ⚠️ and proceed with available context.

#### 2. Deep-search the vault

Use Obsidian CLI to find all notes related to the topic:

```
obsidian search query="{topic keywords}" limit=15
```

Also search for:
- Related tags: `obsidian tags counts sort=count` then filter for topic-adjacent tags
- Backlinks from found notes: `obsidian backlinks file="{note}"`

Read the full content of every relevant note found (up to 10 notes). Skim is not enough — contradictions hide in the details.

#### 3. Map the belief landscape

Before critiquing, map what the user actually believes about this topic. Build a structured inventory:

- **Stated positions** — explicit claims or frameworks they've written
- **Implicit assumptions** — things treated as true without arguing for them
- **Decisions made** — actions or commitments that reveal operational beliefs
- **Sources of conviction** — where does each belief come from (experience, reasoning, borrowed framework, instinct)?

#### 4. Run the challenge

Apply these five lenses systematically:

**A. Internal contradictions**
Where do two notes (or two sections within the same note) say conflicting things? Look for:
- Principles that pull in opposite directions
- Frameworks that would produce different answers to the same question
- Values stated in one place but violated in practice elsewhere

**B. Unexamined assumptions**
What is the user treating as self-evident that actually requires evidence? Look for:
- "Obviously..." or "clearly..." statements
- Conclusions that skip steps
- Beliefs inherited from a specific context that might not transfer

**C. Survivorship bias**
Where might the user be generalizing from their own experience in ways that don't hold broadly? Where might "this worked for me" be masking "I got lucky" or "my context was unusual"?

**D. Missing counter-arguments**
What would a smart, well-informed person who disagrees say? What's the strongest version of the opposing position? Not a strawman — a real challenge.

**E. Staleness**
Are any positions based on conditions that have changed? Old market assumptions, outdated tools, past constraints that no longer apply?

#### 5. Generate visual canvas (optional)

If the challenge is structural or foundational (not surface-level), generate a `.canvas` file using `obsidian:json-canvas` that maps the belief landscape visually:

- **Nodes** for each stated position (green), assumption (yellow), and contradiction (red)
- **Edges** connecting positions to their supporting notes, and contradiction edges between conflicting positions
- **Groups** separating "Strong ground" from "Contested territory"

Save to the directory resolved for `canvas-output` (e.g., `{canvas-output}/Challenge — {topic}.canvas`). This gives the user a visual map they can revisit and annotate in Obsidian.

#### 6. Present the challenge

Output format:

```
## Challenge — "{topic}"

### Belief Map
{2-4 bullet summary of the user's current position, citing [[notes]]}

### Contradictions Found
{Each contradiction with specific note references on both sides}
{If none found, say "No direct contradictions found" — don't fabricate them}

### Weak Assumptions
{Assumptions that deserve scrutiny, with reasoning for why they might break}

### Strongest Counter-Argument
{The best case against the user's position, argued honestly}

### Blind Spots
{Survivorship bias, missing perspectives, or staleness risks}

---

**Notes reviewed:** [[Note 1]], [[Note 2]], …
**Challenge severity:** [surface-level | structural | foundational]
```

### Challenge Severity Scale

- **Surface-level** — minor inconsistencies in language or framing, no real conflict in substance
- **Structural** — genuine tension between two positions that needs resolving, or assumptions that could break under realistic conditions
- **Foundational** — a core belief may be wrong, or the entire framework rests on something unexamined

### Calibration Rules

- **Be honest, not adversarial.** The goal is to strengthen thinking, not to win an argument. If the position is solid, say so.
- **Cite specific notes.** Every contradiction and weak assumption must reference at least one `[[note]]`. No vague "you seem to believe..." claims.
- **Distinguish deliberate trade-offs from contradictions.** The user often holds tensions intentionally (e.g., "systems over heroics" alongside "founders must lead"). That's not a contradiction — it's a calibrated position. Only flag it if the tension is unacknowledged.
- **Don't manufacture problems.** If the vault has 2 notes on a topic and they're consistent, don't stretch to find issues. Report "position is coherent, limited sample" and suggest areas to write more about.
- **The strongest counter-argument section is mandatory.** Even if the position is sound, there's always a strong counter. Find it.

### What This Command Is NOT

- A validation tool (if you want agreement, don't use this)
- A research tool (use a research or search command for information gathering)
- A rewriting tool (use `/ghost` to draft in your voice)

Challenge exists to make your thinking harder to break. The discomfort is the feature.
