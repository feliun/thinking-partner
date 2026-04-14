---
name: thinking-partner:strategise
description: >
  Runs a structured strategic analysis using Hamilton Helmer's 7 Powers framework.
  Asks for meaningful data, maps your current Power position, identifies which Powers
  you can build toward, and challenges your strategic assumptions.
---

## Strategise — Power-Based Strategic Analysis

This command applies Hamilton Helmer's 7 Powers framework to evaluate a business, product, or competitive position. It asks hard questions, demands data over intuition, and produces an honest map of where durable competitive advantage exists (or doesn't).

### Input

The user provides a subject after invoking the command:

```
/strategise {business, product, or strategic question}
```

Examples:
- `/strategise your-company` — full Power audit of the business
- `/strategise your-company vs. incumbent-X` — competitive positioning analysis
- `/strategise our AI-for-ops thesis` — evaluate whether a strategic direction has a path to Power

### Execution Steps

#### 0. Scope the analysis

Before anything, determine whether the subject is specific enough. Ask clarifying questions using AskUserQuestion if:

- **No clear market boundary** — Power is always relative to a specific competitive arena. Ask: "Which market are we analyzing?"
- **No clear competitor set** — Power is relative to *specific competitors*. Ask: "Who are the 2-3 competitors you're most thinking about?"
- **Ambiguous stage** — the analysis differs for "we're building this" vs. "we're already operating." Ask: "Are we evaluating current position or a future direction?"

**Skip clarification when:**
- The subject includes a market and competitor context
- The user added context after the subject
- There's enough in the vault to infer the competitive arena

Keep it to 1-2 questions max. Get enough to define the playing field, then move.

#### 1. Resolve config

Invoke `manifest-resolver` for domain `thinking-partner`. Required keys: `vault`, `strategy-7-powers`. Reasoning profile keys used: `thinking-style`, `values`, `identity`.

Read the resolved `strategy-7-powers.md` in full — this is the analytical backbone. Every claim about Power must map to the framework's definitions: a specific Benefit (cash flow impact) and a specific Barrier (what blocks competitors).

#### 2. Vault context

Search for relevant vault content:

```
obsidian search query="{subject keywords}" limit=15
obsidian search query="strategy" limit=10
obsidian search query="competitive advantage" limit=10
obsidian search query="moat" limit=5
```

Read backlinks from found notes.

#### 3. Gather data (the interrogation)

This is the critical step. **Do not proceed to analysis without sufficient data.** Power claims without evidence are fiction.

Present an information request to the user organized by what you need to assess each Power. Use AskUserQuestion with a structured request:

**Market & Scale:**
- What is the total addressable market (TAM) and how do you define it?
- What is your current revenue / user base / market share (approximate)?
- What are your unit economics? How do they change with scale?
- Who are the top 3 competitors and roughly what's their scale?

**Network Effects:**
- Does each new customer make the product more valuable for existing customers? How specifically?
- Is there a network in your product (marketplace, community, data flywheel, integrations)?

**Switching Costs:**
- How deeply integrated is your product in the customer's workflow?
- What would a customer lose by switching (data, learning, relationships, integrations)?
- Do you have follow-on products or expansion revenue?

**Counter-Positioning:**
- What are incumbents doing that you believe is structurally inferior?
- Why wouldn't they copy your approach? What would they have to give up?

**Branding & Cornered Resources:**
- Do you have access to anything competitors can't easily get (talent, data, relationships, IP)?
- Is there a brand premium? Can you charge more for an objectively similar service?

**Process:**
- Are there internal processes that have taken years to develop and would be hard to replicate?

**Do not skip this step.** If the user provides partial data, work with what you have but flag what's missing and how it limits the analysis. Label assumptions explicitly.

#### 4. Run the Power audit

For each of the 7 Powers, evaluate against the dual test:

1. **Benefit test** — Does this create a material cash flow advantage (higher prices, lower costs, or reduced investment)?
2. **Barrier test** — What specifically prevents competitors from neutralizing this advantage?

Be rigorous:
- "We have great technology" is not Power. It's operational excellence until proven otherwise.
- "Customers love us" is not Power unless you can show *why they can't leave* or *why competitors can't replicate the experience*.
- "We're growing fast" is not Power. Growth without a Barrier is temporary.
- "We have a strong brand" — in B2B and early-stage, almost certainly not Branding Power as Helmer defines it. Don't conflate reputation with Power.

For each Power, assign one of:
- **Active** — both Benefit and Barrier demonstrably present
- **Emerging** — Benefit exists or is building, Barrier not yet established
- **Absent** — no credible path to this Power in the current model
- **Potential** — not present today, but the business model could develop it with specific actions

#### 5. Identify the strategic path

Based on the audit:

- **Which Powers are realistic to pursue?** Not all 7 will apply. Most businesses achieve 1-2. Startups need to identify which Power they're *building toward*.
- **What's the path to Power?** Map specific actions to specific Powers. "Build network effects" is useless. "Achieve X user density in Y segment to trigger tipping point dynamics" is useful.
- **Where is the strategic delusion?** Every founder believes they have more Power than they do. Find the gap between perceived and actual Power. This is the most valuable part of the analysis.
- **What's the "me too" risk?** If competitors can replicate your offering without structural disadvantage, you have no Power — just a head start. Head starts expire.

#### 6. Challenge strategic assumptions

Apply the challenge lens specifically to strategic beliefs:

- **"We're differentiated"** — Differentiation is not Power. Are you differentiated in a way that competitors *structurally cannot copy*?
- **"Our team is our moat"** — Is this actually Cornered Resource, or just good hiring that others can match?
- **"First mover advantage"** — First mover is not a Power. It's a timing advantage that only matters if it converts into an actual Power (network effects, switching costs, scale economies).
- **"We have proprietary data"** — Is it truly non-replicable? Or will competitors build equivalent datasets with time and investment?

#### 7. Present the analysis

Output format:

```
## Strategic Analysis — {subject}

**Market defined:** {the competitive arena being analyzed}
**Competitors considered:** {who Power is being measured against}
**Data quality:** [strong | partial | limited] — {what's missing}

---

### Power Map

| Power | Status | Benefit | Barrier | Confidence |
|-------|--------|---------|---------|------------|
| Scale Economies | {Active/Emerging/Absent/Potential} | {specific benefit or "—"} | {specific barrier or "—"} | {High/Med/Low} |
| Network Economies | ... | ... | ... | ... |
| Counter-Positioning | ... | ... | ... | ... |
| Switching Costs | ... | ... | ... | ... |
| Branding | ... | ... | ... | ... |
| Cornered Resource | ... | ... | ... | ... |
| Process Power | ... | ... | ... | ... |

### Current Power Position

{2-4 paragraphs analyzing the strongest Power(s) and why they qualify or don't. Be specific about Benefit and Barrier for each. Cite vault notes and user-provided data.}

### Strategic Delusions

{Where the perceived Power doesn't hold up. Where "we're differentiated" is actually "we have a temporary head start." Where "our brand" is actually "our reputation among 50 customers." Be honest but constructive.}

### Path to Power

{For each realistic Power to build toward:}
1. **{Power name}** — {what specifically needs to happen, what milestones would confirm it's working, what the timeline looks like}

### The Hardest Question

{One question the founder needs to answer honestly. The question that, if answered "no," means the strategy needs fundamental rethinking. This is the equivalent of the "strongest counter-argument" in /challenge.}

---

**Vault notes referenced:** [[Note 1]], [[Note 2]], ...
**Framework:** Hamilton Helmer, 7 Powers
**Data gaps:** {list of missing information that would improve the analysis}
```

### Calibration Rules

- **Power is binary in definition, continuous in magnitude.** A Power either exists (Benefit + Barrier) or it doesn't. But among businesses with the same Power, magnitude varies enormously. Capture both: does it exist, and how strong is it?
- **Operational excellence is never Power.** This is the most common mistake. Being better at execution is valuable but temporary. Competitors can hire, learn, and improve. Power is what remains after they do.
- **Power is relative to specific competitors.** Don't assess Power in the abstract. Always name the competitor and explain why *they specifically* face a Barrier. Counter-Positioning against Incumbent A says nothing about Challenger B.
- **Demand data, not narratives.** When the user says "we have switching costs," ask: "What percentage of customers have churned? What's the average integration depth? How many follow-on products do they buy?" Numbers reveal whether the switching cost is real or wishful.
- **Don't manufacture Power.** If the honest answer is "you have no durable Power today," say that clearly. Most startups don't. The value is in identifying the *path* to Power, not in pretending it already exists.
- **Flag the Dynamics question.** Statics (do we have Power?) matters less for early-stage businesses than Dynamics (are we on a path to Power?). Always address both, but weight Dynamics appropriately for the business stage.
- **The "me too" test is mandatory.** For every claimed advantage, ask: "Could a well-funded competitor replicate this in 18 months?" If yes, it's not Power.
- **Potential Value = Market Scale x Power.** Both matter. Power in a tiny market is a small business. A huge market with no Power is a race to the bottom. Address both dimensions.

### Combining with Other Commands

- Use `/challenge` first if you want to pressure-test your *beliefs* about strategy before running a formal analysis
- Use `/strategise` when you want a structured, framework-driven evaluation of competitive position
- Use `/ideas` after `/strategise` if the analysis reveals gaps that suggest new directions
- Use `/emerge` to see if your vault already contains strategic insights you haven't connected

### What This Command Is NOT

- A business plan generator (this analyzes Power, not operations)
- A validation exercise (if you want to hear you're winning, don't use this)
- A one-time audit (run this quarterly as your market and position evolve)
- A substitute for data (the output quality is bounded by the input quality — garbage in, garbage out)

Strategise strips away the narratives founders tell themselves and asks: where is the structural advantage that competitors cannot arbitrage away? If the answer is "nowhere yet," that's the most valuable finding — because now you know what to build.
