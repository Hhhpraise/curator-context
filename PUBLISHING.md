# Curator — GitHub Publishing Checklist

## Repo Metadata

| Field | Value |
|-------|-------|
| **Repo name** | `curator-context` |
| **Owner** | `Hhhpraise` |
| **Full URL** | `https://github.com/Hhhpraise/curator-context` |
| **Description (About field)** | Semantic context triage for AI agents — classify before compression so constraints, exact values, and decision reasoning survive long sessions |
| **Website (optional)** | Leave blank or link to the Gap Engine dashboard artifact |
| **Visibility** | Public |

## GitHub Topics (Set exactly these — max 12)

```
ai-agents
context-compression
claude-skill
context-management
agent-memory
developer-tools
context-preservation
token-optimization
llm-agents
semantic-triage
claude-code
agent-context
```

**Why these topics:**
- `ai-agents` is the highest-traffic tag in this space (Headroom, Hermes, mem0 all use it)
- `context-compression` and `context-preservation` are rising fast (Headroom alone drove 26K stars under this umbrella)
- `claude-skill` and `claude-code` capture the Claude ecosystem specifically — lower competition than generic `ai` tags
- `agent-memory` and `agent-context` are the 2026 hot categories (pingcap/ossinsight tracks this as a growth ecosystem)
- `semantic-triage` is Curator's unique differentiator — you own this intersection
- `developer-tools` is the home domain

## Social Preview Image (OpenGraph)

Create a 1280×640px PNG. Recommended layout:

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│   🔴🔵🟢⬜                                              │
│                                                         │
│   C U R A T O R                                         │
│   Context Intelligence for AI Agents                    │
│                                                         │
│   Classify before you compress.                         │
│   Pin constraints. Preserve reasoning.                  │
│                                                         │
│   github.com/Hhhpraise/curator-context                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

Color scheme: Dark background (#0d1117 GitHub dark), accent colors matching the four triage categories (#ef4444 red, #3b82f6 blue, #10b981 green, #9ca3af grey).

## README Hashtags / SEO Keywords

These should appear naturally in your README (don't keyword-stuff — use them in sentences):

**Primary:** `ai agents`, `context compression`, `context preservation`, `agent memory`, `semantic triage`, `claude skill`

**Secondary:** `token optimization`, `constraint management`, `context degradation`, `agent context`, `llm context window`, `developer tools`

## Launch Channels & Timing

### Order of Operations (Stacked Launch — Same Day)

1. **Push the repo** — make sure it's public, fully populated with all files
2. **Post to Hacker News** (Tuesday–Thursday, 8–10 AM PT)
   - Title: "Show HN: Curator — semantic triage for AI agent context before compression destroys it"
   - Link to: the GitHub repo
   - First comment: explain why you built it (cite the Gamage 73%→33% stat, mention the Gap Engine methodology)
3. **Post to Reddit** (same day, staggered by 2 hours)
   - r/programming: "Curator: classify AI agent context before your compressor silently destroys your constraints"
   - r/selfhosted: if you position it as "the thing you run before your compression proxy"
   - r/MachineLearning: frame around the Validity Mirage paper and research grounding
4. **X/Twitter thread** (same day)
   - Tweet 1: The 73%→33% stat + "I built something to fix this"
   - Tweet 2: The 4-category taxonomy visual
   - Tweet 3: Before/after example
   - Tweet 4: Link to repo
5. **Product Hunt** — launch as "Curator — Semantic triage for AI agent context" in the Developer Tools category

### What Gets the Most Stars

Per 2026 data:
- **Hacker News**: 121 avg stars/24h, up to 1,500 for top posts
- **Reddit r/programming**: 50-200 stars depending on upvotes
- **Stacked launch** (HN + Reddit + X + PH same day): 200–2,000+ stars in a week
- **Star-history.com badge**: adding this to your README increases star conversion by ~15%

## Post-Launch: Community Signals

After the repo is live, these signals tell GitHub's algorithm the project is active and worth recommending:

1. **Respond to every issue within 24 hours** — GitHub weights maintainer responsiveness
2. **Merge a PR within the first week** — shows collaborative activity
3. **Push at least one commit per week** — active development signal
4. **Link from your other repos** — add a "Built with Curator" or "See also" link in your existing repos (hsk-exam-simulator, password-generator, etc.)
5. **Star your own repo** — your followers see this in their feed

## Files to Include in the Repo

```
curator-context/
├── SKILL.md                  ✅ Created — The Claude Skill
├── README.md                 ✅ Created — Full README with examples
├── LICENSE                   ✅ Created — MIT
├── CONTRIBUTING.md           ✅ Created — Contribution guide
├── .gitignore                Add — Standard Python/Node ignores
├── gap-engine/
│   └── analyses/
│       └── 2026-06-18-context-compression-engine/
│           ├── light-analysis.md     Copy from gap-engine/analyses/
│           └── full-analysis.md      Copy from gap-engine/analyses/
└── assets/
    └── social-preview.png    Create — 1280×640px OpenGraph image
```

## The "Secret Sauce" — What Makes This Repo Spread

1. **The 73%→33% stat is your hook.** It's specific, surprising, and research-backed. Lead with it everywhere.
2. **"Not a better compressor — a smarter curator"** is a clean frame that positions you above the compression wars. You're not competing with Headroom; you're the intelligence layer they're missing.
3. **The Gap Engine methodology** is your differentiator. "Built with the Gap Engine" signals that this wasn't a random idea — it came from structured problem discovery. It makes people curious about the methodology itself.
4. **The 4-category color system** (🔴🔵🟢⬜) is sticky. It's visual, memorable, and works in plain text. People who see it once will recognize it.
5. **Research-grounded** sets you apart from the flood of "I made an AI wrapper" repos. You're citing actual 2026 papers. That earns trust instantly.
