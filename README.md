# Curator — Context Intelligence Layer for AI Agents

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Cursor%20%7C%20Copilot-purple?style=flat-square" alt="Platform">
  <img src="https://img.shields.io/badge/type-Claude%20Skill-orange?style=flat-square" alt="Type">
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" alt="Status">
</p>

> **Your AI agent's context is being silently destroyed. Curator stops it.**

Every context compressor — Headroom, Hermes, Claude Compaction, TokMan — treats all context as equally compressible. So your "don't touch the database schema" constraint from turn 5? Gone by turn 40. The exact port number? Rounded to "the port." The reason you chose Postgres over Redis? Summarized into nothing.

**Curator is not another compressor. It's the intelligence layer that classifies context *before* compression decides what to destroy.**

## The Problem (With Receipts)

- **73% → 33% compliance drop** in omission constraints from turn 5 to turn 16 across 4,416 trials. Commission constraints hold at 100%, masking the failure entirely — this is the "safe turn depth" exploit zone (Gamage, 2026)
- **65% of enterprise AI failures** traced to context degradation during multi-step reasoning, not raw token exhaustion (Zylos Research, 2026)
- **Validity Mirage**: naive compression preserves surface answer correctness while silently substituting the governing hypothesis — validated across 5 model architectures and 11,400+ boundary instances (University of Michigan, 2026)

## How Curator Works

```
Context enters -> Curator classifies -> Compressor gets routing instructions

RED PINNED:      Never compress. Anchor at position 0 on every request.
BLUE PRESERVED:  Structured compression only. Exact values survive.
GREEN SUMMARIZABLE: Safe for LLM compression. Archive original by UUID.
GREY DISCARDABLE:  Remove entirely. Re-derivable from disk.
```

Every piece of context is scored on **three axes of irreplaceability**:

| Axis | Question |
|------|----------|
| **Recoverability** | Can this be re-derived from disk or re-running a tool? |
| **Constraint Criticality** | Would violating this produce an unrecoverable error? |
| **Dependency Risk** | Does this link to a decision 30 turns from now? |

Score HIGH on *any* axis → pinned or preserved. All LOW → safe to discard.

## Quick Start

### Install in Claude Code / Cowork

1. Clone this repo: `git clone https://github.com/Hhhpraise/curator-context.git`
2. Copy `SKILL.md` into your Claude skills directory
3. Start a session — Curator activates automatically when you mention constraints, context protection, or compression

### First Session

```
You: I need to refactor auth. Don't touch the DB, keep API contracts stable, port is 8443.

Curator: Got it.
  * C001: "Don't touch the database layer"
  * C002: "Don't change any API contracts"
  * P001: "auth service port = 8443"
  Anchored at position 0. Validating all future actions against these.
```

## Commands

| Command | What it does |
|---------|-------------|
| `/curator classify [text]` | Classify a piece of context into red/blue/green/grey |
| `/curator audit` | Scan for unprotected context. Report top 5 risks. |
| `/curator constraint add [rule]` | Pin a constraint. Anchors at position 0 forever. |
| `/curator constraint list` | Show all active constraints with IDs and age. |
| `/curator constraint remove [ID]` | Remove a constraint. |
| `/curator pre-compress` | Triage report before compression fires. |
| `/curator dependency map` | Visual dependency graph (Mermaid) of the session. |
| `/curator dashboard` | Session health: category counts, decay risk, token breakdown. |

## Why Not Just Use Headroom / TokMan / LLMLingua?

They compress. Curator **triages**. Use them together.

```
                        +------------+
Context  ----------->   |  Curator   |   RED: PINNED --> Bypass compressor
                        |  (triage)  |   BLUE: PRESERVED --> Structured only
                        +-----+------+   GREEN: SUMMARIZABLE --> Headroom / TokMan
                              |          GREY: DISCARDABLE --> Remove
                              |
                       Compression Layer
```

Curator isn't a replacement — it's a routing layer that tells your existing compressor what to protect and what's safe to crush.

## Research Behind This

This skill is grounded directly in peer-reviewed 2026 research:

- [Omission Constraints Decay While Commission Constraints Persist — Gamage (2026)](https://arxiv.org/abs/2604.20911) — 4,416 trials across 12 models. Omission constraints drop 73% → 33% by turn 16 while commission constraints hold at 100%, creating a "zone of exploitation" where everything looks fine and nothing is.
- [The Validity Mirage: Context Algebra for Endogenous Semantics under Memory Compression — University of Michigan (2026)](https://zenodo.org/records/18794293) — 5 architectures, 11,400+ boundary instances. Compression preserves answer correctness while substituting the governing hypothesis. Includes a tropical semiring algebra for measuring context health.
- [Decision-Aware Memory Cards (CICL) — Wang et al. (2026)](https://arxiv.org/abs/2606.08151) — Counterfactual context selection: removing the single highest-utility semantic unit can collapse F1 to 0.000. Provides the theoretical foundation for irreplaceability-based triage.
- [ContextWeaver — Liu et al. (2026)](https://arxiv.org/abs/2604.23069) — Dependency-structured memory construction with validation-informed pruning. Demonstrates that dependency graphs outperform sliding-window baselines on SWE-Bench Verified.
- [Memex(RL) — Accenture (2026)](https://arxiv.org/abs/2603.04257) — Indexed summaries with lossless deferred access via RL-trained compression/retrieval agents. Bounded dereferencing preserves decision quality while keeping context bounded.

## Comparison vs Alternatives

| Tool | What it does | Curator + it |
|------|-------------|-------------|
| **Headroom** | Token-level compression (60-95% savings) | Curator classifies first; Headroom only compresses green and grey content |
| **TokMan** | 31-layer CLI proxy pipeline | Curator routes red and blue around TokMan entirely |
| **LLMLingua** | Small-LM importance scoring (up to 20x compression) | Curator pre-flags what LLMLingua should score LOW (never drop) |
| **Hermes Agent** | Dual-threshold (50% + 85%) agent-native compression | Curator replaces blind thresholds with semantic boundaries |
| **Claude Compaction API** | Server-side auto-compress