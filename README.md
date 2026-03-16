# Vigil

> Your first answer is a draft. You don't ship drafts.

A Claude Code skill that forces second-order thinking before every non-trivial response. Where PUA makes your AI try harder, Vigil makes it **think harder**.

## What It Does

Vigil inserts a metacognitive reasoning pass between "I've formulated a response" and "I deliver it." Before the user sees anything, the response gets stress-tested across five dimensions:

1. **Comprehension** — Will they actually understand this?
2. **Intent Gap** — Am I answering the right question?
3. **Technical Soundness** — Does this hold up under scrutiny?
4. **Downstream Friction** — Will this create more work?
5. **Emotional Impact** — How does this land?

The user never sees the deliberation. They just get better answers.

## The Problem: AI's Five Default Failure Modes

| Mode | What Happens |
|------|-------------|
| **Confidence theater** | Presents uncertain info like established fact |
| **Literal answering** | Answers what you asked, misses what you meant |
| **Happy path only** | Gives the solution, ignores failure modes |
| **Sycophantic agreement** | Agrees with your flawed premise to be agreeable |
| **Orphan answers** | Answers the question, leaves you needing 3 follow-ups |

Vigil catches all five before the response ships.

## How It Works

### Activation
Two gates — either triggers the full reasoning pass:
- **Complexity Gate**: Multi-step problems, tradeoffs, ambiguous intent, consequential decisions
- **Stakes Gate**: User frustration, prior corrections, low-confidence answers, deployable code

Doesn't trigger on trivial queries. No overhead on "what's the capital of France."

### Reasoning Modes
Domain-adaptive, not random:
- **Adversarial** (debugging, code, factual claims): Generate answer → argue against it → revise if the argument wins
- **Branching** (strategy, creative, open-ended): Generate 2–3 structurally different framings → pick the best

### Context Weighting
Technical soundness dominates for code. Emotional impact dominates for comms. The weights shift automatically based on what you're doing.

### Diminishing Returns Guard
Max 2 revision passes. If the revision delta is small, the draft was fine. Ships it. No analysis paralysis.

## Composable State

Vigil exposes its internal state via `[VIGIL-STATE]` blocks that other skills can read:

```
[VIGIL-STATE]
mode: adversarial
complexity: high
user_expertise: advanced
user_frustration: 0.3
trust_level: high
evaluation_scores:
  comprehension: 0.9
  intent_gap: 0.8
  technical: 0.7
  friction: 0.6
  emotional: 0.9
revision_count: 1
revision_delta: 0.4
flags: [high_stakes]
```

One-way broadcast. Vigil informs, doesn't depend on other skills.

## Install

```bash
# Clone to Claude Code skills directory
git clone https://github.com/YOUR_USERNAME/vigil.git ~/.claude/skills/vigil

# Or copy manually
mkdir -p ~/.claude/skills/vigil
cp skills/vigil/SKILL.md ~/.claude/skills/vigil/SKILL.md
mkdir -p ~/.claude/commands
cp commands/vigil.md ~/.claude/commands/vigil.md
```

## Usage

Vigil activates automatically on complex queries. To force it manually:

```
/vigil
```

Append `/vigil` to any prompt to force maximum-strictness evaluation.

## Works With PUA

PUA and Vigil are complementary:
- **PUA** = persistence engine (try harder, don't give up)
- **Vigil** = quality engine (think harder, don't ship your first draft)

PUA governs retry behavior. Vigil governs response quality. No conflict when both are loaded.

## The Sycophancy Check

The single most important thing Vigil does:

> **Am I saying what's true, or what's comfortable?**

Correctness always wins. Delivery adapts. Truth doesn't.

## License

MIT

## Credits

Built by [Edward Kennedy](https://kinamix.com) / Kinamix Labs — because your AI's first instinct isn't always its best one.
