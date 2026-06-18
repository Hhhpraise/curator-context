# Curator — Context Intelligence Layer for AI Agents

<p align="center">
  <img src="https://img.shields.io/badge/stars-coming_soon-yellow?style=flat-square" alt="Stars">
  <img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Cursor%20%7C%20Copilot-purple?style=flat-square" alt="Platform">
  <img src="https://img.shields.io/badge/type-Claude%20Skill-orange?style=flat-square" alt="Type">
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" alt="Status">
</p>

> **Your AI agent's context is being silently destroyed. Curator stops it.**

Every context compressor — Headroom, Hermes, Claude Compaction, TokMan — treats all context as equally compressible. So your "don't touch the database schema" constraint from turn 5? Gone by turn 40. The exact port number? Rounded to "the port." The reason you chose Postgres over Redis? Summarized into nothing.

**Curator is not another compressor. It's the intelligence layer that classifies context *before* compression decides what to destroy.**

## The Problem (With Receipts)

- **73% → 33% compliance drop** in constraint adherence from turn 5 to turn 16 across 4,416 trials (Gamage, 2026)
- **65% of enterprise AI failures** traced to context degradation, not token exhaustion (Zylos Research, 2026)
- **Validity Mirage**: naive compression preserves answer correctness while silently substituting the governing hypothesis (U Michigan, 2026)

## How Curator Works

```
Context enters → Curator classifies → Compressor gets routing instructions

🔴 PINNED     → Never compress. Anchor at position 0 on every request.
🔵 PRESERVED  → Structured compression only. Exact values survive.
🟢 SUMMARIZABLE → Safe for LLM compression. Archive original by UUID.
⬜ DISCARDABLE  → Remove entirely. Re-derivable from disk.
```

Every piece of context is scored on **three axes of irreplaceability**:

| Axis | Question |
|------|----------|
| **Recoverability** | Can this be re-derived from disk or re-running a tool? |
| **Constraint Criticality** | Would violating this produce an unrecoverable error? |
| **Dependency Risk** | Does this link to a decision 30 turns from now? |

Score HIGH on *any* axis → pinned or preserved. All LOW → safe to discard.

## Quick Start

### Install as a Claude Skill

1. Download `curator-context.skill` from the [latest release](https://github.com/Hhhpraise/curator-context/releases)
2. In Claude Code / Cowork, install the skill: drag the `.skill` file into your skills directory
3. Start a session — Curator activates automatically

### First Session

```
You: I need to refactor auth. Don't touch the DB, keep API contracts stable, port is 8443.

Curator: Got it.
  🔴 C001: "Don't touch the database layer"
  🔴 C002: "Don't change any API contracts"
  🔵 P001: "auth service port = 8443"
  Anchored at position 0. Validating all future actions against these.
```

## Commands

| Command | What it does |
|---------|-------------|
| `/curator classify [text]` | Classify a piece of context into 🔴🔵🟢⬜ |
| `/curator audit` | Scan for unprotected context. Report top 5 risks. |
| `/curator constraint add [rule]` | Pin a constraint. Anchors at position 0 forever. |
| `/curator constraint list` | Show all active constraints with IDs and age. |
| `/curator constraint remove [ID]` | Remove a constraint. |
| `/curator pre-compress` | Triage report before compression fires. |
| `/curator dependency map` | Visual dependency graph (Mermaid) of the session. |
| `/curator dashboard` | Session health: category counts, decay risk, token breakdown. |

## Why Not Just Use [Headroom / TokMan / LLMLingua]?

They compress. Curator **triages**. Use them together.

```
        ┌──────────┐
Context │ Curator  │   🔴 → Bypass compressor, anchor at position 0
  ─────→│ (triage) │── 🔵 → Structured compression only
        └────┬─────┘   🟢 → Headroom / TokMan / LLMLingua
             │          ⬜ → Discard
             ▼
      Compression Layer
```

Curator isn't a replacement — it's a routing layer that tells your existing compressor what to protect and what's safe to crush.

## Research Behind This

This skill is grounded in peer-reviewed 2026 research:

- [Gamage (Apr 2026)](https://arxiv.org/abs/2604.xxxxx) — Positional attention decay quantified: 73% → 33% constraint compliance across 4,416 trials
- [University of Michigan "Validity Mirage" (Feb 2026)](https://zenodo.org/records/18794293) — Compression preserves answer correctness while substituting hypotheses (5 architectures, 11,400+ instances)
- [CICL / Decision-Aware Memory Cards (Jun 2026)](https://arxiv.org/abs/2606.08151) — Counterfactual context selection: removing one unit can collapse F1 to 0.000
- [ContextWeaver (Apr 2026)](https://arxiv.org/abs/2604.23069) — Dependency-structured memory with validation-informed pruning
- [Memex(RL) (Apr 2026)](https://arxiv.org/abs/2603.04257) — Indexed summaries with lossless deferred access via RL-trained agents

## Project Structure

```
curator-context/
├── SKILL.md                  # The Claude Skill (all logic lives here)
├── README.md                 # This file
├── LICENSE                   # MIT
└── gap-engine/
    └── analyses/             # Full Tier 1 & Tier 2 gap analysis
        └── 2026-06-18-context-compression-engine/
            ├── light-analysis.md    # ~200 word trend confirmation
            └── full-analysis.md     # Ecosystem map, 3 gaps, blueprint
```

## Contributing

Curator was born from the [Gap Engine](https://github.com/Hhhpraise/gap-engine) methodology — a structured process of scanning trending problems, running deep gap analysis, and building targeted solutions. If you want to improve Curator or suggest a new gap:

1. **Fork** this repo
2. **Read** the [full gap analysis](gap-engine/analyses/2026-06-18-context-compression-engine/full-analysis.md) to understand the problem space
3. **Propose** your change — new classification rules, better irreplaceability scoring, additional commands
4. **Test** with a 50+ turn agent session and verify constraint survival

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full process.

## License

MIT — use it, fork it, build on it. If Curator saves you from a production constraint violation, I'd love to hear about it.

---

<p align="center">
  <sub>Built with the Gap Engine methodology · Part of the <a href="https://github.com/Hhhpraise/gap-engine">Gap Engine</a> ecosystem</sub>
</p>
