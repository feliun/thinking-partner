---
name: thinking-partner:ghost
description: >
  Answers a question the way you would, based on your vault writings and stated beliefs.
  Use when you want to externalize your own thinking or need a draft response that sounds like you.
---

## Ghost — Think as You

This command produces a response to a question **the way you would answer it**, grounded in your vault notes, mental models, and stated beliefs.

### Input

The user provides a question after invoking the command:

```
/ghost {question}
```

### Execution Steps

#### 1. Resolve config

Invoke `manifest-resolver` for domain `thinking-partner`. Required keys: `vault`. Voice profile keys used (load all that resolve): `writing-style`, `thinking-style`, `values`, `identity`, `work-style`.

These are non-negotiable inputs. If any file fails to resolve, note it with ⚠️ and proceed with available context. Without `writing-style`, the output cannot match the user's voice — flag this explicitly if missing.

#### 2. Search the vault for relevant notes

Use Obsidian CLI to find notes related to the question:

```
obsidian search query="{keywords from question}" limit=10
```

Also check:
- Backlinks from related notes
- Tags that match the topic

Collect **specific ideas, frameworks, and positions** the user has already written about. These anchor the response in their actual thinking, not generic reasoning.

#### 3. Synthesize the answer

Write a response that:

1. **Sounds like the user** — match the voice DNA from `writing-style.md` exactly: sentence rhythm, tone, formatting rules, banned phrases. If the writing-style specifies contractions, use them. If it bans em dashes, don't use them.
2. **Reasons like the user** — match the biases and decision framework from `thinking-style.md`. Systems thinking, first principles, leverage over effort, second-order effects — whatever the user's profile calls for.
3. **References specific vault notes** — cite notes inline using `[[Note Name]]` links when the answer draws from or aligns with existing writing. This grounds the response in their actual body of work.
4. **Takes a position** — don't hedge unnecessarily. State a clear view. If the answer depends on context, say so explicitly and explain what changes under each scenario.
5. **Respects the constraints** — follow every formatting rule from `writing-style.md` strictly.

#### 4. Present the response

Output format:

```
## Ghost — "{question}"

{The answer, 200-600 words depending on complexity, written in the user's voice}

---

**Vault anchors:**
- [[Note 1]] — how it connects
- [[Note 2]] — how it connects
- [[Note N]] — how it connects

**Confidence:** [high | medium | low] — based on how much vault material directly supports this position
```

### Calibration Rules

- **If the vault has strong coverage** of the topic (3+ related notes with clear positions): lean heavily on existing writing. The answer should feel like a remix of things the user has already said.
- **If the vault has partial coverage** (1-2 tangential notes): extrapolate from their values and thinking patterns. Flag the extrapolation.
- **If the vault has no coverage**: reason from their values, biases, and mental models. Mark confidence as low. State "You haven't written about this directly, but based on your stated principles..."
- **Never invent positions the user hasn't expressed.** If unsure, say so. Better to surface the gap than to fabricate a stance.
- **Never sound motivational, preachy, or guru-like.** If the draft leans that way, strip it back.
- **Writing-style rules are non-negotiable.** If `writing-style.md` bans a phrase or pattern, the output must not contain it. Re-read before finalizing.

### What This Command Is NOT

- A research tool (use a research command for information gathering)
- A content generator (use dedicated content commands for publishing)
- A decision-maker (surface the reasoning, let the user decide)

Ghost externalizes thinking. It gives you a first draft of *your own answer* so you can react to it, sharpen it, or realize you disagree with yourself.
