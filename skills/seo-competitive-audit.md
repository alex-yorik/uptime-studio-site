---
name: seo-competitive-audit
description: "Use for deep competitive SEO audit of any web page or HTML file: SERP research via Bright Data (Google/Bing/Yandex, geo-targeted), parsing top organic competitors, JSON-LD Schema generation and validation, on-page meta optimization (Title/Description/OG/Twitter/H1-H3/alt), missing-asset generation (og-image, favicons, manifest, logo) and a prioritized implementation plan. Works for landing pages, blog posts, e-commerce, corporate sites — anything with an HTML file to analyze."
---

# /seo-competitive-audit

Полный конкурентный SEO-аудит страницы: анализ собственного HTML, SERP-исследование топ-N конкурентов через Bright Data MCP, генерация валидной JSON-LD разметки, оптимизация on-page элементов и пошаговый план внедрения.

## ИЗВЛЕЧЕНИЕ ПАРАМЕТРОВ ИЗ ПРОМПТА

Когда пользователь вызывает скилл через `/seo-competitive-audit` и пишет параметры в свободной форме:

1. **page_file** (обязательный): Ищи упоминания файлов (.html, .tsx, .php). Если не указан — спроси пользователя.
   - Примеры: "главная страница" → index.html, "страница блога" → blog/article.html, "услуги" → services.html

2. **target_keywords** (обязательный): Ищи фразы в кавычках или после слов "ключи", "запросы", "keywords".
   - Примеры: "Ключи: запрос1, запрос2" → ["запрос1", "запрос2"]
   - "Целевые запросы: фраза1, фраза2" → ["фраза1", "фраза2"]

3. **geo_region** (опциональный, по умолчанию RU/Moscow): Ищи упоминания городов/стран.
   - Примеры: "Москва" → RU/Moscow, "Питер" → RU/Saint-Petersburg, "США" → US
   - Если не указан → используй RU/Moscow

4. **competitor_count** (опциональный, по умолчанию 5): Ищи числа после слов "топ", "конкурентов".
   - Примеры: "топ-3" → 3, "5 конкурентов" → 5
   - Если не указан → используй 5

5. **business_type** (опциональный, по умолчанию ProfessionalService): Ищи тип бизнеса.
   - Примеры: "магазин" → Product, "услуги" → ProfessionalService, "клиника" → MedicalBusiness
   - Если не указан → используй ProfessionalService

Если какой-то обязательный параметр не найден — спроси пользователя перед началом работы.

## Входные параметры

Пользователь указывает (по возможности):

| Параметр | Тип | Пример | Обязательный |
|---|---|---|---|
| `page_file` | string | `index.html`, `blog/dental-bot.html` | ✅ |
| `target_keywords` | string[] | `["телеграм бот для записи клиентов", "заказать телеграм бота"]` | ✅ |
| `geo_region` | string | `RU/Moscow`, `US/New York` | ❌ (по умолч. `RU/Moscow`) |
| `competitor_count` | int | `3-5` | ❌ (по умолч. 5) |
| `business_type` | string | `LocalBusiness`, `ProfessionalService`, `Organization` | ❌ (по умолч. `ProfessionalService`) |

Если параметр не указан — выведи список недостающих и запроси их у пользователя коротко (один вопрос). Если пользователь говорит «сам разберись» — определи параметры из контента страницы (тема → ключи, страна из `lang`/валюты → регион, `business_type` из существующей схемы или рода деятельности).

## Основной алгоритм

### ШАГ 0 — Инициализация

1. Проверь, что `page_file` существует и содержит валидный HTML (`<html>`/`<body>`/`<title>`).
2. Определи, доступен ли Bright Data:
   - MCP-инструменты `search_engine`, `scrape_as_html`, `scrape_as_markdown` (если они видны в окружении — используй их напрямую);
   - либо токен: переменная `BRIGHTDATA_MCP_TOKEN`, или значение в `~/.local/share/opencode/mcp-auth.json`, или из логов прошлых сессий (`~/.local/share/opencode/log/opencode.log`, искать `token=...` в URL `mcp.brightdata.com/sse?token=...`);
   - если ничего не найдено — сообщи «Bright Data недоступен», перейди к офлайн-аудиту (шаги 1, 5, 6, 7, 8) и пометь в отчёте, что SERP-данные не получены.

### ШАГ 1 — Анализ текущей страницы

Прочитай `page_file` и извлеки:
- **Тему и интент** (коммерческий/информационный/транзакционный).
- **Title** — длина в символах, позиция главного ключа.
- **Meta Description** — длина, наличие CTA и цифр.
- **H1–H6** — полная иерархия, наличие LSI-синонимов, единственный ли H1.
- **JSON-LD** — типы всех `application/ld+json`-блоков, есть ли `@graph`, какие обязательные поля заполнены.
- **Open Graph / Twitter** — наличие `og:title`, `og:description`, `og:image`, `og:url`, `og:site_name`, `og:locale`, `twitter:card` и т.д.
- **Ассеты** — существует ли `og:image`, `favicon-*`, `site.webmanifest`, `logo` (сверь ссылки из HTML со списком файлов в директории).
- **Контент** — объём текста в символах, наличие FAQ/цен/отзывов/калькулятора/телефона/адреса/гео-упоминаний.
- **Семантика** — для RU: вхождения кириллического варианта ключа (например «телеграм») vs латиницы («Telegram»); для других языков — транслитерации/синонимы.
- **Техническое** — canonical, robots, sitemap.xml (совпадает ли `lastmod` с датой изменения).

Запиши результат в заметки — он пойдёт в блок «Анализ текущей страницы» отчёта.

### ШАГ 2 — SERP-исследование через Bright Data

Для **каждого** ключа из `target_keywords` выполни поиск в Google с гео. Концептуальная команда:

```
search_engine(query="<keyword>", engine="google", geo_location="<2-letter country>")
```

Практика (важно — проверено):
- **Google возвращает ссылки в виде `/goto?url=<base64>`** — это редирект, реальный URL так просто не получить. Надёжный способ: спарсить саму выдачу HTML-скрапером
  `scrape_as_html(url="https://www.google.com/search?q=<urlencoded>&gl=<cc>&hl=<lang>&num=10")`
  и извлечь пары `<a href="..."><h3>...</h3></a>`, где `href="/url?q=<реальный_url>"` (декодировать через `urllib.parse.unquote`).
- Часть результатов (обычно позиция №1) приходит как `/httpservice/retry/enablejs` — это JS-гейт. Не блокируйся: определи домен поиском точного Title через движок `bing` (он отдаёт чистые URL в формате `https://domain › path`) или отметь «JS-gated, домен не определён».
- Альтернатива: движок `bing` или `yandex` сразу отдают реальные URL (у `bing` — в markdown, формат `https://domain › path`).

Для каждого ключа зафиксируй топ-N органических результатов (N = `competitor_count`): позиция, Title, URL, тип (лендинг/статья/конструктор/SaaS/студия).

### ШАГ 3 — Парсинг конкурентов

Для каждого из топ-N конкурентов скачай полный HTML:

```
scrape_as_html(url="<competitor_url>")
```

Из каждого HTML извлеки:
- **Title** — длина, наличие целевых ключей.
- **Meta Description** — длина, CTA, цифры.
- **Canonical**, **robots**.
- **H1–H3** — тексты заголовков.
- **JSON-LD** — все типы (`FAQPage`, `LocalBusiness`, `ProfessionalService`, `Organization`, `Service`, `Product`, `AggregateRating`, `OfferCatalog`, `BreadcrumbList`, `WebSite`, `WebPage`, `Article`); отметь использование `@graph`, наличие `geo`, `telephone`, `openingHours`, `areaServed`, `priceRange`, `aggregateRating`.
- **Open Graph** — наличие og-тегов и реального og:image.
- **Контакты** — телефон, email, мессенджеры, адрес, гео.
- **Контент** — объём текста, наличие FAQ/таблиц цен/отзывов/кейсов/калькуляторов.
- **Ассеты** — og-image, favicon, manifest.

Если какой-то конкурент не парсится (403/CAPTCHA/JS-gate) — пропусти, отметь в отчёте, возьми следующего из выдачи.

### ШАГ 4 — Сравнительный анализ

Составь таблицу «Мы vs Конкуренты» по строкам:
- Title (длина, ключи)
- Meta Description (длина, CTA)
- H1 / H2 / H3 (иерархия, LSI)
- Семантика (кириллица vs латиница для ключа)
- Гео-привязка (есть/нет, что именно)
- Контакты (телефон/email/мессенджер)
- JSON-LD типы (что есть у них, чего нет у нас)
- Контентные блоки (FAQ/цены/отзывы/калькулятор/объём текста)
- Технические ресурсы (og-image/favicon/manifest/logo — и существуют ли файлы)

Выводы по каждой строке: «наша сильная сторона» / «наш пробел» / «выравнять».

### ШАГ 5 — Генерация улучшенной JSON-LD разметки

Создай единый блок `<script type="application/ld+json">` с графом сущностей `@graph`:

1. **`<business_type>`** (из параметров) — `@id`, `name`, `url`, `logo`, `image`, `email`/`telephone` (только реальные данные со страницы!), `priceRange`, `areaServed`, `address` (PostalAddress: страна, `addressLocality`), `geo` (GeoCoordinates — столица/центр региона), `openingHoursSpecification` (из страницы или типовое), `contactPoint` (email/telegram/телефон), `sameAs` (мессенджеры/соцсети).
2. **`WebSite`** — `@id`, `url`, `name`, `inLanguage`, `publisher` → ссылка на `@id` организации.
3. **`WebPage`** — `@id`, `url`, `name`, `description`, `datePublished`/`dateModified` (из sitemap/git-истории), `isPartOf` → WebSite, `about` → Service.
4. **`Service`** (или `Product`) — `name`, `serviceType`, `provider` → организация, `areaServed`, `offers` → `AggregateOffer` с `lowPrice`/`highPrice`/`priceCurrency` и вложенными `Offer` (name, price, priceCurrency, url, availability `https://schema.org/InStock`).
5. **`BreadcrumbList`** — `itemListElement` (ListItem: position, name, item).
6. **`FAQPage`** — только если FAQ реально есть на странице; вопросы/ответы — **дословно из видимого FAQ** (рассинхрон контента = риск санкций).

Правила валидации:
- `json.loads()` проходит.
- Все обязательные поля заполнены реальными данными (не выдумывай телефон/адрес/отзывы).
- FAQ-разметка синхронна с видимым контентом.
- Внутренние ссылки через `@id` (`#organization`, `#website`, `#webpage`, `#service`).
- Цены — числа или строки с `priceCurrency`.

Место вставки: в `<head>`, перед `</head>` (в статических сайтах — перед закрытием `<head>`; если есть существующие ld+json — **замени их**, оставив один блок).

### ШАГ 6 — Оптимизация On-Page SEO

Предложи обновлённые (и покажи в diff) версии:
- **`<title>`** — ≤ 60 символов: главный ключ в начале + УТП/бренд.
- **`<meta name="description">`** — ≤ 155 символов: выгоды + цифры + CTA.
- **Open Graph** — `og:title`, `og:description`, `og:image` (1200×630), `og:url`, `og:site_name`, `og:locale` (например `ru_RU`).
- **Twitter Card** — `twitter:card` (`summary_large_image`), `twitter:title`, `twitter:description`, `twitter:image`.
- **H1–H6** — главный ключ в H1 (ровно один H1), LSI-синонимы в H2/H3, без пропуска уровней.
- **alt** — для всех `<img>` с содержательным смыслом; декоративные/трекинговые пиксели (Я.Метрика и т.п.) оставить с пустым `alt=""` — это правильно, в отчёте пояснить.
- **Семантика** — если страница использует только латиницу/англ. форму ключа, добавить естественные вхождения локального варианта в видимый текст (не keyword stuffing).

Перед применением любых правок покажи пользователю diff (`git diff` или блоки до/после). Применяй только после согласия пользователя (или если пользователь явно делегировал автономность).

### ШАГ 7 — Генерация недостающих ассетов

Если `og:image`, favicon-размеры, `site.webmanifest`-иконки или `logo` отсутствуют (файла нет, но ссылка есть — это критично):
- **og-image.png** — 1200×630, тёмный/брендовый градиент, название бренда + оффер (проверь ширину текста программно: `ImageFont.getbbox` ≤ 1200px).
- **favicon-16x16.png / 32x32.png / 180×180** — из существующей иконки через `Image.resize(..., Image.LANCZOS)`.
- **web-app-manifest-512x512.png** — ресайз существующей 192.
- **logo.png / logo.svg** — квадрат 512×512 с брендом (или SVG, если удобнее).
- Обнови `site.webmanifest` (name, short_name, icons) при необходимости.
- Сгенерируй через **Pillow** (`from PIL import Image, ImageDraw, ImageFont`) — проверь наличие шрифтов (`fc-list`, DejaVu).

### ШАГ 8 — Формирование отчёта

Создай файл `project/reports/seo_audit_<YYYY-MM-DD>.md` (структура — в `skills/seo-competitive-audit-template.md`). Если директория `project/reports/` отсутствует — создай.

## Интеграция с Bright Data MCP

Доступные инструменты (фактические имена из конфигурации `advanced_scraping`):

| Инструмент | Назначение | Параметры |
|---|---|---|
| `search_engine` | SERP-выдача | `query` (обяз.), `engine` (`google`/`bing`/`yandex`), `geo_location` (2 буквы: `ru`, `us`, ...), `cursor` (пагинация) |
| `scrape_as_html` | полный HTML страницы | `url` |
| `scrape_as_markdown` | контент в markdown | `url` |
| `search_engine_batch` / `scrape_batch` | массовые запросы | массив queries/urls |

Если MCP-инструменты не подключены, но токен есть — рабочий обходной путь: минимальный MCP SSE-клиент (Python, `sseclient`): подключение к `https://mcp.brightdata.com/sse?token=<TOKEN>&groups=advanced_scraping`, получение `sessionId`, POST `initialize` → `tools/list` → `tools/call` на `/messages?sessionId=<id>`.

Fallback при недоступности Bright Data: открытые/API-поиск (если доступен) или пометка «требуются ручные данные SERP» — и продолжение офлайн-частей аудита.

## Валидация и проверки (чек-лист перед завершением)

- [ ] JSON-LD парсится `json.loads()` и содержит `@graph`.
- [ ] Все обязательные поля Schema.org заполнены; нет выдуманных телефонов/адресов/отзывов.
- [ ] FAQ-разметка совпадает с видимым FAQ (дословно).
- [ ] Title ≤ 60 симв., Description ≤ 155 симв.
- [ ] `og:image` существует и имеет размер 1200×630 (проверь `Image.size`).
- [ ] На странице ровно один `<h1>`.
- [ ] Все ссылки на ассеты (`og:image`, favicon, manifest, logo) указывают на существующие файлы.
- [ ] `sitemap.xml` обновлён (`lastmod`, при необходимости новые URL).
- [ ] HTML сбалансирован по тегам (быстрая проверка: открывающих == закрывающих по `<title>/<script>/<h1>...<h6>/<section>`).
- [ ] Русские тексты meta/H1/prose проверены скиллом **russian-editor** (если применимо — язык RU).
- [ ] Если изменялся код/разметка — `graphify update .` (если в проекте есть graphify-out/).

## Output скилла

После выполнения предоставь пользователю:
1. Путь к отчёту: `project/reports/seo_audit_YYYY-MM-DD.md`.
2. Список изменённых файлов (`git status --short` + `git diff --stat`).
3. Список созданных файлов (og-image, favicon, manifest, logo).
4. Чек-лист «что закоммитить» (не коммить сам).
5. Приоритеты внедрения: **Неделя 1** (критично: JSON-LD, Title/Description, битые ассеты, гео/семантика), **Неделя 2** (контент-блоки, отзывы, калькулятор, расширение текста).

## ПРИМЕРЫ ВЫЗОВА

### Пример 1: Полный промпт (свободная форма)

```
/seo-competitive-audit

Проведи аудит страницы blog/dental-bot.html.
Ключевые запросы: "telegram бот для стоматологии", "автоматизация записи в клинику".
Регион: Москва и Московская область.
Покажи топ-5 конкурентов.
Тип: ProfessionalService.
```

Парсинг: `page_file=blog/dental-bot.html`, `target_keywords=["telegram бот для стоматологии","автоматизация записи в клинику"]`, `geo_region=RU/Moscow`, `competitor_count=5`, `business_type=ProfessionalService`.

### Пример 2: Минимальный промпт (дефолтные параметры)

```
/seo-competitive-audit

Аудит главной страницы. Ключи: "заказать телеграм бота".
```

Парсинг: `page_file=index.html`, `target_keywords=["заказать телеграм бота"]`, `geo_region=RU/Moscow` (дефолт), `competitor_count=5` (дефолт), `business_type=ProfessionalService` (дефолт).

### Пример 3: Магазин / другой тип бизнеса

```
/seo-competitive-audit

Страница services.html интернет-магазина. Запросы: "купить telegram-бота", "чат-бот для интернет-магазина".
Регион: США, топ-3 конкурентов.
```

Парсинг: `page_file=services.html`, `target_keywords=["купить telegram-бота","чат-бот для интернет-магазина"]`, `geo_region=US`, `competitor_count=3`, `business_type=Product` (по роду деятельности).

### Пример 4: Явные параметры через `ключ=значение`

```
/seo-competitive-audit page_file=index.html target_keywords=["телеграм бот для записи клиентов","заказать телеграм бота"] geo_region=RU/Moscow competitor_count=5 business_type=ProfessionalService
```

## Дополнительные требования

- Работай автономно; при сбое шага — продолжай, но зафиксируй в отчёте.
- Все изменения HTML — в diff-формате перед применением.
- Не коммить автоматически — жди подтверждения.
- Не выдумывай контактные данные и отзывы (это санкционный риск Google и нарушение честности).
- Скилл параметризован: не привязывайся к тематике/структуре — лендинг, блог, магазин, корпоративный сайт обрабатываются одинаково.
- Скилл предназначен для глобальной установки: копируется в `~/.config/opencode/skills/seo-competitive-audit/` как `SKILL.md` (вместе с шаблоном отчёта и примером конфига), чтобы вызываться из любого проекта.
