# Скилл «Ясное письмо» / Writing Clearly Skill

Скилл для написания ясного и краткого текста на русском языке. Убирает канцеляризмы, пассивный залог, абстракции и AI-штампы.

Основан на принципах Норы Галь («Слово живое и мёртвое») и Максима Ильяхова («Пиши, сокращай»).

---

## 📋 Содержание

- [Что делает скилл](#что-делает-скилл)
- [Установка по платформам](#установка-по-платформам)
  - [Claude Code / Claude.ai](#claude-code--claudeai)
  - [Cursor](#cursor)
  - [Gemini CLI](#gemini-cli)
  - [OpenAI Codex](#openai-codex)
  - [Google Antigravity](#google-antigravity)
  - [VS Code + GitHub Copilot](#vs-code--github-copilot)
  - [Другие агенты](#другие-агенты)
- [Универсальный способ](#универсальный-способ)
- [Структура файлов](#структура-файлов)

---

## Что делает скилл

**Убирает:**
- Пассивный залог → активный («обрабатывается сервером» → «сервер обрабатывает»)
- Канцеляризмы («в рамках», «на сегодняшний день» → «сейчас»)
- Отглагольные существительные («осуществить проверку» → «проверить»)
- AI-штампы («играет ключевую роль», «уникальный», «инновационный»)
- Слова-паразиты и вводные-пустышки
- Абстракции без конкретики («быстро» → «за 50 мс»)

**Пример:**

До:
> В рамках данного проекта была осуществлена разработка системы, которая обеспечивает высокую скорость обработки запросов и имеет ключевое значение для пользователей.

После:
> Мы разработали систему, которая отвечает за 50 мс — втрое быстрее прежней.

---

## Установка по платформам

### Claude Code / Claude.ai

Скилл использует формат [Agent Skills](https://agentskills.io) — открытый стандарт для AI-агентов.

#### Персональный скилл (для всех проектов)

```bash
mkdir -p ~/.claude/skills/writing-clearly/references
cp writing-clearly/SKILL.md ~/.claude/skills/writing-clearly/
cp writing-clearly/references/style-guide.md ~/.claude/skills/writing-clearly/references/
```

#### Проектный скилл (для команды)

```bash
mkdir -p .claude/skills/writing-clearly/references
cp writing-clearly/SKILL.md .claude/skills/writing-clearly/
cp writing-clearly/references/style-guide.md .claude/skills/writing-clearly/references/
git add .claude/
git commit -m "Добавлен скилл ясного письма"
```

Claude автоматически подхватит скилл при запросах типа «напиши документацию», «отредактируй текст», «убери воду».

---

### Cursor

Cursor поддерживает несколько способов добавления правил.

#### Способ 1: Файл .cursorrules (legacy, но работает)

Создай файл `.cursorrules` в корне проекта:

```bash
cp writing-clearly/references/style-guide.md .cursorrules
```

#### Способ 2: Директория .cursor/rules/ (рекомендуется)

```bash
mkdir -p .cursor/rules
cp writing-clearly/SKILL.md .cursor/rules/writing-clearly.mdc
```

#### Способ 3: Глобальные настройки

1. Открой `Cursor -> Settings -> Cursor Settings -> Rules for AI`
2. Вставь содержимое `style-guide.md`

#### Способ 4: Agent Skills (если поддерживается)

Cursor поддерживает формат Agent Skills:

```bash
mkdir -p .cursor/skills/writing-clearly/references
cp writing-clearly/SKILL.md .cursor/skills/writing-clearly/
cp writing-clearly/references/style-guide.md .cursor/skills/writing-clearly/references/
```

---

### Gemini CLI

Gemini CLI использует файлы `GEMINI.md` для контекста.

#### Глобальный контекст (для всех проектов)

```bash
mkdir -p ~/.gemini
cat writing-clearly/SKILL.md writing-clearly/references/style-guide.md > ~/.gemini/GEMINI.md
```

#### Проектный контекст

```bash
cat writing-clearly/SKILL.md writing-clearly/references/style-guide.md > GEMINI.md
```

#### Модульный подход с импортами

Создай `GEMINI.md` в корне проекта:

```markdown
# Контекст проекта

@./writing-clearly/SKILL.md
@./writing-clearly/references/style-guide.md
```

Проверь загрузку командой `/memory show`.

---

### OpenAI Codex

Codex поддерживает два формата: `AGENTS.md` и Agent Skills (`SKILL.md`).

#### Способ 1: AGENTS.md

```bash
cat writing-clearly/SKILL.md writing-clearly/references/style-guide.md > AGENTS.md
```

Или добавь в глобальный конфиг:

```bash
mkdir -p ~/.codex
cat writing-clearly/SKILL.md writing-clearly/references/style-guide.md > ~/.codex/AGENTS.md
```

#### Способ 2: Agent Skills (рекомендуется)

Codex поддерживает формат Agent Skills:

```bash
mkdir -p ~/.codex/skills/writing-clearly/references
cp writing-clearly/SKILL.md ~/.codex/skills/writing-clearly/
cp writing-clearly/references/style-guide.md ~/.codex/skills/writing-clearly/references/
```

Или для проекта:

```bash
mkdir -p .codex/skills/writing-clearly/references
cp writing-clearly/SKILL.md .codex/skills/writing-clearly/
cp writing-clearly/references/style-guide.md .codex/skills/writing-clearly/references/
```

---

### Google Antigravity

Antigravity использует Rules и Workflows.

#### Через интерфейс

1. Нажми `...` в правом верхнем углу
2. Выбери `Customizations` → `Rules`
3. Создай новое правило и вставь содержимое `style-guide.md`

#### Через файлы

Глобальные правила:
```bash
mkdir -p ~/.antigravity
cp writing-clearly/references/style-guide.md ~/.antigravity/rules.md
```

Проектные правила:
```bash
mkdir -p .antigravity
cp writing-clearly/references/style-guide.md .antigravity/rules.md
```

---

### VS Code + GitHub Copilot

VS Code с GitHub Copilot поддерживает Agent Skills (в preview).

1. Включи `chat.useAgentSkills` в настройках VS Code
2. Создай структуру:

```bash
mkdir -p .github/skills/writing-clearly/references
cp writing-clearly/SKILL.md .github/skills/writing-clearly/
cp writing-clearly/references/style-guide.md .github/skills/writing-clearly/references/
```

---

### Другие агенты

#### Windsurf

Windsurf использует похожий на Cursor формат:

```bash
cp writing-clearly/references/style-guide.md .windsurfrules
```

#### Continue.dev

```bash
cp writing-clearly/references/style-guide.md .continuerules
```

#### Aider

Создай файл `.aider.conf.yml`:

```yaml
read:
  - writing-clearly/references/style-guide.md
```

Или используй флаг:

```bash
aider --read writing-clearly/references/style-guide.md
```

---

## Универсальный способ

Если твой AI-инструмент не поддерживает специальные форматы, просто скопируй содержимое `style-guide.md` в:

- **Системный промпт** — если есть доступ к настройкам
- **Начало диалога** — вставь как первое сообщение
- **Пользовательские инструкции** — в настройках чата

Работает с любым LLM: ChatGPT, Claude, Gemini, и т.д.

---

## Структура файлов

```
writing-clearly/
├── SKILL.md                    # Основной файл (~60 строк)
│                               # Краткая памятка и workflow
└── references/
    └── style-guide.md          # Подробные правила (~250 строк)
                                # Таблицы замен, примеры, чек-лист
```

### Формат Agent Skills

Скилл соответствует открытому стандарту [Agent Skills](https://agentskills.io), который поддерживают:

- Claude Code / Claude.ai
- OpenAI Codex
- Cursor
- VS Code + GitHub Copilot
- И другие агенты

**Принцип:** пиши один раз, используй везде.

---

## Лицензия

MIT — используй как хочешь.

---

## Благодарности

- Нора Галь — «Слово живое и мёртвое»
- Максим Ильяхов — «Пиши, сокращай»
- Справочник Розенталя
