# Contributing to Curator

Curator is part of the [Gap Engine](https://github.com/Hhhpraise/gap-engine) ecosystem — a structured methodology for discovering trending problems, analyzing unsolved gaps, and building targeted solutions.

## How to Contribute

### 1. Understand the Problem Space

Before contributing, read the full gap analysis:

- [Light Analysis](../gap-engine/analyses/2026-06-18-context-compression-engine/light-analysis.md) — Quick trend confirmation
- [Full Gap Analysis](../gap-engine/analyses/2026-06-18-context-compression-engine/full-analysis.md) — Ecosystem map, 3 unsolved gaps, innovation blueprint

This will help you understand *why* Curator exists and what specific pain points it addresses.

### 2. Pick Your Lane

Curator has several areas open for contribution:

**Classification Rules** — Improve the triage logic in `SKILL.md`. Can you think of edge cases the current 3-axis scoring misses? Are there context types that get misclassified?

**Commands** — New slash commands that extend Curator's capabilities. A `/curator replay` to reconstruct a session from preserved context? A `/curator export` to dump constraints for another session?

**Preservation Patterns** — Document real-world patterns you've discovered. "When doing database migrations, always pin the current schema version." "When refactoring, preserve the git diff of the original state."

**Research Integration** — Found new 2026 research on context degradation or compression failure modes? Add it to the Research References section with a clear summary of the finding.

### 3. Fork → Branch → Test → PR

1. **Fork** the repository
2. **Create a branch**: `feature/your-idea` or `fix/classification-edge-case`
3. **Make your changes** — keep SKILL.md under 500 lines; if adding substantial content, consider a reference file
4. **Test your changes** — run at least one 50+ turn agent session with your modified skill and verify that constraints survive and classification is accurate
5. **Open a PR** — include:
   - What you changed and why
   - The test scenario you ran
   - Any edge cases you discovered

### 4. Reporting Bugs

If Curator misclassifies context or a constraint decays despite being pinned:

1. Describe the scenario — what was the constraint, how many turns elapsed, what compressor was running
2. Include the relevant conversation excerpt (or a minimal reproduction)
3. Note which classification was wrong and what it should have been

## Design Principles

- **Curator triages, it doesn't compress** — Don't add compression logic. Let Headroom, TokMan, LLMLingua, and Claude Compaction handle actual token reduction. Curator's job is to classify first.
- **Irreplaceability over recency** — The 3-axis score (recoverability, constraint criticality, dependency risk) is the north star. Never classify based on how old something is or how many tokens it costs.
- **Explain the why** — Every classification decision includes the scores on each axis and a one-sentence rationale. Users should understand *why* something was pinned or discarded.
- **The conversation is the database** — Curator works with what's in the conversation. No external storage required unless explicitly set up via MCP.

## Code of Conduct

Be kind. Be specific. Assume good intent. This is a tool to help developers trust their AI agents — let's make it great together.
