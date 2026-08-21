# Skills — переиспользуемые скиллы проекта

Скиллы — параметризованные инструкции, которые запускаются из любого проекта для повторяющихся задач. Каждый скилл — один Markdown-файл с frontmatter (`name`, `description`) и пошаговым алгоритмом.

## Список доступных скиллов

### SEO-конкурентный аудит — `/seo-competitive-audit`

Глубокий конкурентный SEO-аудит любой HTML-страницы: SERP-исследование через Bright Data (Google/Bing/Yandex, гео-таргетинг), парсинг топ-N конкурентов, сравнительный анализ (Title/Meta/H1–H3/JSON-LD/структура контента), генерация и валидация JSON-LD `@graph`, on-page-оптимизация (Title/Description/OG/Twitter/alt), генерация недостающих ассетов (og-image, favicons, manifest, logo) и пошаговый план внедрения.

**Параметры:**

| Параметр | Обязательный | Пример |
|---|---|---|
| `page_file` | ✅ | `index.html`, `blog/dental-bot.html` |
| `target_keywords` | ✅ | `["телеграм бот для записи клиентов"]` |
| `geo_region` | ✅ | `RU/Moscow` |
| `competitor_count` | ❌ (по умолч. 5) | `3-5` |
| `business_type` | ❌ (по умолч. `ProfessionalService`) | `LocalBusiness` |

**Пример вызова:**

```
/seo-competitive-audit page_file=index.html target_keywords=["телеграм бот для записи клиентов","заказать телеграм бота"] geo_region=RU/Moscow competitor_count=5 business_type=ProfessionalService
```

**Выходные артефакты:**
- Отчёт: `project/reports/seo_audit_<YYYY-MM-DD>.md` (шаблон: `seo-competitive-audit-template.md`)
- JSON-LD `@graph` (внедряется в `page_file` после согласия)
- Обновлённые meta-теги + сгенерированные ассеты (og-image, favicons, manifest, logo)

**Файлы скилла:**
- `seo-competitive-audit.md` — инструкция
- `seo-competitive-audit-template.md` — шаблон отчёта
- `examples/seo-audit-example-config.json` — пример конфигурации

**Глобальная установка:** скилл установлен глобально в `~/.config/opencode/skills/seo-competitive-audit/` (как `SKILL.md` вместе с шаблоном и примером конфига) и доступен из любого проекта. При обновлении файлов в `skills/` синхронизируй копию глобально:

```bash
mkdir -p ~/.config/opencode/skills/seo-competitive-audit/examples
cp skills/seo-competitive-audit.md ~/.config/opencode/skills/seo-competitive-audit/SKILL.md
cp skills/seo-competitive-audit-template.md ~/.config/opencode/skills/seo-competitive-audit/
cp skills/examples/seo-audit-example-config.json ~/.config/opencode/skills/seo-competitive-audit/examples/
```

---

## Как создать новый скилл

1. Создай файл `skills/<name>.md` с frontmatter:
   ```markdown
   ---
   name: <name>
   description: "Короткое описание: когда использовать, что делает, для каких типов задач."
   ---
   ```
2. Опиши входные параметры, пошаговый алгоритм, валидацию и output.
3. Добавь файл в этот список (README).
4. Если нужен шаблон отчёта/конфига — положи рядом с подпапке `examples/`.

## Замечания по интеграции

- Для SEO-аудита требуется доступ к Bright Data MCP (токен в `BRIGHTDATA_MCP_TOKEN` или `mcp-auth.json`). При его отсутствии скилл выполняет офлайн-часть аудита и помечает недостающие SERP-данные в отчёте.
- Русскоязычные тексты meta-тегов рекомендуется дополнительно проверять скиллом `russian-editor` (установлен глобально в `~/.config/opencode/skills/`).
