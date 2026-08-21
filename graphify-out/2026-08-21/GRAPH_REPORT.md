# Graph Report - uptime-studio-site  (2026-08-20)

## Corpus Check
- 6 files · ~16,000 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 18 nodes · 13 edges · 5 communities (4 shown, 1 thin omitted)
- Extraction: 92% EXTRACTED · 8% INFERRED · 0% AMBIGUOUS · INFERRED: 1 edges (avg confidence: 0.9)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `d93ccab8`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Landing Page Frontend Development
- graphify.js
- opencode.json

## God Nodes (most connected - your core abstractions)
1. `plugin` - 2 edges
2. `$schema` - 1 edges
3. `.opencode/plugins/graphify.js` - 1 edges
4. `IMPORTANT: keep the reminder string free of backticks and $(...) constructs.` - 1 edges
5. `GSAP + ScrollTrigger` - 1 edges
6. `Tailwind CSS` - 1 edges
7. `Three.js` - 1 edges
8. `Uptime Studio Landing Page` - 1 edges
9. `Yandex.Metrica` - 1 edges
10. `Builder Report` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Frontend CDN Dependencies** — tech_stack_gsap, tech_stack_threejs, tech_stack_tailwind [EXTRACTED 1.00]
- **Project Documentation & Meta** — readme_md, agents_md, yandex_metrica_md, project_reports_builder_report_md [INFERRED 0.80]

## Communities (5 total, 1 thin omitted)

### Community 0 - "Landing Page Frontend Development"
Cohesion: 0.22
Nodes (6): Builder Report, GSAP + ScrollTrigger, Tailwind CSS, Three.js, Uptime Studio Landing Page, Yandex.Metrica

### Community 4 - "opencode.json"
Cohesion: 0.50
Nodes (3): plugin, $schema, .opencode/plugins/graphify.js

## Knowledge Gaps
- **8 isolated node(s):** `$schema`, `.opencode/plugins/graphify.js`, `GSAP + ScrollTrigger`, `Tailwind CSS`, `Three.js` (+3 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What connects `$schema`, `.opencode/plugins/graphify.js`, `GSAP + ScrollTrigger` to the rest of the system?**
  _8 weakly-connected nodes found - possible documentation gaps or missing edges._