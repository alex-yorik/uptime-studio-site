# Graph Report - uptime-studio-site  (2026-08-21)

## Corpus Check
- 7 files · ~23,307 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 42 nodes · 36 edges · 9 communities (8 shown, 1 thin omitted)
- Extraction: 97% EXTRACTED · 3% INFERRED · 0% AMBIGUOUS · INFERRED: 1 edges (avg confidence: 0.9)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `09a8024b`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Landing Page Frontend Development
- graphify.js
- brightdata
- SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения
- 2. Результаты поиска Google (geo=ru) — топ органической выдачи
- 5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас
- 3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей

## God Nodes (most connected - your core abstractions)
1. `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения` - 10 edges
2. `brightdata` - 4 edges
3. `2. Результаты поиска Google (geo=ru) — топ органической выдачи` - 4 edges
4. `5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас` - 4 edges
5. `3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей` - 3 edges
6. `plugin` - 2 edges
7. `mcp` - 2 edges
8. `$schema` - 1 edges
9. `.opencode/plugins/graphify.js` - 1 edges
10. `url` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Frontend CDN Dependencies** — tech_stack_gsap, tech_stack_threejs, tech_stack_tailwind [EXTRACTED 1.00]
- **Project Documentation & Meta** — readme_md, agents_md, yandex_metrica_md, project_reports_builder_report_md [INFERRED 0.80]

## Communities (9 total, 1 thin omitted)

### Community 0 - "Landing Page Frontend Development"
Cohesion: 0.22
Nodes (6): Builder Report, GSAP + ScrollTrigger, Tailwind CSS, Three.js, Uptime Studio Landing Page, Yandex.Metrica

### Community 4 - "brightdata"
Cohesion: 0.22
Nodes (8): enabled, type, url, mcp, brightdata, plugin, $schema, .opencode/plugins/graphify.js

### Community 5 - "SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения"
Cohesion: 0.25
Nodes (7): 1. Определение темы, целевых ключей и интента страницы, 4. Сравнение структуры контента (FAQ, цены, отзывы, калькулятор), 6. Список критических SEO-упущений (итог), 7. Пошаговый план внедрения, 8. Данные аудита (источники), 9. Статус внедрения (2026-08-21, в этом же изменении), SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения

### Community 6 - "2. Результаты поиска Google (geo=ru) — топ органической выдачи"
Cohesion: 0.50
Nodes (4): 2. Результаты поиска Google (geo=ru) — топ органической выдачи, Запрос 1: «телеграм бот для записи клиентов», Запрос 2: «заказать телеграм бота для бизнеса», Запрос 3: «телеграм бот для стоматологии»

### Community 7 - "5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас"
Cohesion: 0.50
Nodes (4): 5.1 Что внедрено у конкурентов (по спарсенным страницам), 5.2 Что есть у нас сейчас, 5.3 Критические недостатки нашей разметки, 5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас

### Community 8 - "3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей"
Cohesion: 0.67
Nodes (3): 3.1 Title и Meta Description, 3.2 H1–H3 и плотность, 3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей

## Knowledge Gaps
- **25 isolated node(s):** `$schema`, `.opencode/plugins/graphify.js`, `type`, `url`, `enabled` (+20 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения` connect `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения` to `3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей`, `2. Результаты поиска Google (geo=ru) — топ органической выдачи`, `5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас`?**
  _High betweenness centrality (0.168) - this node is a cross-community bridge._
- **Why does `2. Результаты поиска Google (geo=ru) — топ органической выдачи` connect `2. Результаты поиска Google (geo=ru) — топ органической выдачи` to `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения`?**
  _High betweenness centrality (0.059) - this node is a cross-community bridge._
- **Why does `5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас` connect `5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас` to `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения`?**
  _High betweenness centrality (0.059) - this node is a cross-community bridge._
- **What connects `$schema`, `.opencode/plugins/graphify.js`, `type` to the rest of the system?**
  _25 weakly-connected nodes found - possible documentation gaps or missing edges._