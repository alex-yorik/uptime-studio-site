# Graph Report - uptime-studio-site  (2026-08-21)

## Corpus Check
- 11 files · ~25,775 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 81 nodes · 72 edges · 13 communities (12 shown, 1 thin omitted)
- Extraction: 99% EXTRACTED · 1% INFERRED · 0% AMBIGUOUS · INFERRED: 1 edges (avg confidence: 0.9)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `2280cb8a`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Landing Page Frontend Development
- graphify.js
- brightdata
- SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения
- 2. Результаты поиска Google (geo=ru) — топ органической выдачи
- 5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас
- SEO-аудит <URL_или_имя_страницы> — конкурентный анализ и план внедрения
- Основной алгоритм
- /seo-competitive-audit
- Skills — переиспользуемые скиллы проекта
- 6. Приложения

## God Nodes (most connected - your core abstractions)
1. `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения` - 10 edges
2. `Основной алгоритм` - 10 edges
3. `SEO-аудит <URL_или_имя_страницы> — конкурентный анализ и план внедрения` - 8 edges
4. `/seo-competitive-audit` - 8 edges
5. `6. Приложения` - 5 edges
6. `brightdata` - 4 edges
7. `2. Результаты поиска Google (geo=ru) — топ органической выдачи` - 4 edges
8. `5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас` - 4 edges
9. `Skills — переиспользуемые скиллы проекта` - 4 edges
10. `3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей` - 3 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Frontend CDN Dependencies** — tech_stack_gsap, tech_stack_threejs, tech_stack_tailwind [EXTRACTED 1.00]
- **Project Documentation & Meta** — readme_md, agents_md, yandex_metrica_md, project_reports_builder_report_md [INFERRED 0.80]

## Communities (13 total, 1 thin omitted)

### Community 0 - "Landing Page Frontend Development"
Cohesion: 0.22
Nodes (6): Builder Report, GSAP + ScrollTrigger, Tailwind CSS, Three.js, Uptime Studio Landing Page, Yandex.Metrica

### Community 4 - "brightdata"
Cohesion: 0.22
Nodes (8): enabled, type, url, mcp, brightdata, plugin, $schema, .opencode/plugins/graphify.js

### Community 5 - "SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения"
Cohesion: 0.18
Nodes (10): 1. Определение темы, целевых ключей и интента страницы, 3.1 Title и Meta Description, 3.2 H1–H3 и плотность, 3. Сравнительный анализ Title / Meta / H1–H3 / плотности ключей, 4. Сравнение структуры контента (FAQ, цены, отзывы, калькулятор), 6. Список критических SEO-упущений (итог), 7. Пошаговый план внедрения, 8. Данные аудита (источники) (+2 more)

### Community 6 - "2. Результаты поиска Google (geo=ru) — топ органической выдачи"
Cohesion: 0.50
Nodes (4): 2. Результаты поиска Google (geo=ru) — топ органической выдачи, Запрос 1: «телеграм бот для записи клиентов», Запрос 2: «заказать телеграм бота для бизнеса», Запрос 3: «телеграм бот для стоматологии»

### Community 7 - "5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас"
Cohesion: 0.50
Nodes (4): 5.1 Что внедрено у конкурентов (по спарсенным страницам), 5.2 Что есть у нас сейчас, 5.3 Критические недостатки нашей разметки, 5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас

### Community 8 - "SEO-аудит <URL_или_имя_страницы> — конкурентный анализ и план внедрения"
Cohesion: 0.20
Nodes (9): 1. Executive Summary (главные находки), 2. Анализ текущей страницы, 3.1 Результаты поиска Google (geo=<регион>), 3.2 Таблица сравнения «Мы vs Конкуренты», 3. Конкурентный анализ (SERP + сравнение), 4. Критические SEO-упущения (по приоритету), 5. Пошаговый план внедрения, 7. Данные аудита (источники) (+1 more)

### Community 9 - "Основной алгоритм"
Cohesion: 0.20
Nodes (10): Основной алгоритм, ШАГ 0 — Инициализация, ШАГ 1 — Анализ текущей страницы, ШАГ 2 — SERP-исследование через Bright Data, ШАГ 3 — Парсинг конкурентов, ШАГ 4 — Сравнительный анализ, ШАГ 5 — Генерация улучшенной JSON-LD разметки, ШАГ 6 — Оптимизация On-Page SEO (+2 more)

### Community 10 - "/seo-competitive-audit"
Cohesion: 0.25
Nodes (7): Output скилла, /seo-competitive-audit, Валидация и проверки (чек-лист перед завершением), Входные параметры, Дополнительные требования, Интеграция с Bright Data MCP, Пример вызова

### Community 11 - "Skills — переиспользуемые скиллы проекта"
Cohesion: 0.33
Nodes (5): SEO-конкурентный аудит — `/seo-competitive-audit`, Skills — переиспользуемые скиллы проекта, Замечания по интеграции, Как создать новый скилл, Список доступных скиллов

### Community 12 - "6. Приложения"
Cohesion: 0.40
Nodes (5): 6.1 Полный JSON-LD код для вставки, 6.2 Обновлённые meta-теги, 6.3 Созданные ассеты, 6.4 Статус внедрения / открытый техдолг, 6. Приложения

## Knowledge Gaps
- **54 isolated node(s):** `$schema`, `.opencode/plugins/graphify.js`, `type`, `url`, `enabled` (+49 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения` connect `SEO-аудит главной страницы uptimestudio.ru — конкурентный анализ и план внедрения` to `2. Результаты поиска Google (geo=ru) — топ органической выдачи`, `5. Аудит JSON-LD Schema: что есть у конкурентов и чего нет у нас`?**
  _High betweenness centrality (0.044) - this node is a cross-community bridge._
- **Why does `Основной алгоритм` connect `Основной алгоритм` to `/seo-competitive-audit`?**
  _High betweenness centrality (0.034) - this node is a cross-community bridge._
- **Why does `/seo-competitive-audit` connect `/seo-competitive-audit` to `Основной алгоритм`?**
  _High betweenness centrality (0.029) - this node is a cross-community bridge._
- **What connects `$schema`, `.opencode/plugins/graphify.js`, `type` to the rest of the system?**
  _54 weakly-connected nodes found - possible documentation gaps or missing edges._