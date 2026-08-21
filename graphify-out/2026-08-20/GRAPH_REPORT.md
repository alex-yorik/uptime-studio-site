# Graph Report - uptime-studio-site  (2026-08-16)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 14 nodes · 10 edges · 4 communities (3 shown, 1 thin omitted)
- Extraction: 90% EXTRACTED · 10% INFERRED · 0% AMBIGUOUS · INFERRED: 1 edges (avg confidence: 0.9)
- Token cost: 174 input · 17 output

## Graph Freshness
- Built from commit: `30f45b4c`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Landing Page Frontend Development
- graphify.js

## God Nodes (most connected - your core abstractions)
1. `IMPORTANT: keep the reminder string free of backticks and $(...) constructs.` - 1 edges
2. `GSAP + ScrollTrigger` - 1 edges
3. `Tailwind CSS` - 1 edges
4. `Three.js` - 1 edges
5. `Uptime Studio Landing Page` - 1 edges
6. `Yandex.Metrica` - 1 edges
7. `Builder Report` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Frontend CDN Dependencies** — tech_stack_gsap, tech_stack_threejs, tech_stack_tailwind [EXTRACTED 1.00]
- **Project Documentation & Meta** — readme_md, agents_md, yandex_metrica_md, project_reports_builder_report_md [INFERRED 0.80]

## Communities (4 total, 1 thin omitted)

### Community 0 - "Landing Page Frontend Development"
Cohesion: 0.22
Nodes (6): Builder Report, GSAP + ScrollTrigger, Tailwind CSS, Three.js, Uptime Studio Landing Page, Yandex.Metrica

## Knowledge Gaps
- **6 isolated node(s):** `GSAP + ScrollTrigger`, `Tailwind CSS`, `Three.js`, `Uptime Studio Landing Page`, `Yandex.Metrica` (+1 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What connects `GSAP + ScrollTrigger`, `Tailwind CSS`, `Three.js` to the rest of the system?**
  _6 weakly-connected nodes found - possible documentation gaps or missing edges._