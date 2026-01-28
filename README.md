# Скилл «Ясное письмо» / Writing Clearly Skill

Скилл для написания ясного и краткого текста на русском языке. Убирает канцеляризмы, пассивный залог, абстракции и AI-штампы.

Основан на принципах Норы Галь («Слово живое и мёртвое») и Максима Ильяхова («Пиши, сокращай»).

---

## 📋 Содержание

- [Быстрый старт](#быстрый-старт)
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

## Быстрый старт

### Вариант 1: Клонирование репозитория

```bash
git clone https://github.com/nikitaCodeSave/writing-clearly.git
cd writing-clearly
```

Все команды ниже выполняются из этой директории.

### Вариант 2: Скачать только нужные файлы

Если не хочешь клонировать весь репозиторий:

```bash
# Создай директорию и скачай файлы
mkdir -p writing-clearly/references
curl -Lo writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

### Вариант 3: Однострочник для Claude Code

```bash
# Персональная установка (для всех проектов)
mkdir -p ~/.claude/skills/writing-clearly/references && curl -Lo ~/.claude/skills/writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md && curl -Lo ~/.claude/skills/writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

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

> **Примечание:** Команды ниже предполагают, что ты находишься в корне склонированного репозитория (`cd writing-clearly` после клонирования).

#### Персональный скилл (для всех проектов)

```bash
mkdir -p ~/.claude/skills/writing-clearly/references
cp writing-clearly/SKILL.md ~/.claude/skills/writing-clearly/
cp writing-clearly/references/style-guide.md ~/.claude/skills/writing-clearly/references/
```

#### Проектный скилл (для команды)

Перейди в корень своего проекта и выполни:

```bash
mkdir -p .claude/skills/writing-clearly/references
cp /путь/к/writing-clearly/writing-clearly/SKILL.md .claude/skills/writing-clearly/
cp /путь/к/writing-clearly/writing-clearly/references/style-guide.md .claude/skills/writing-clearly/references/
git add .claude/
git commit -m "Добавлен скилл ясного письма"
```

Или используй curl (не нужно клонировать репо):

```bash
mkdir -p .claude/skills/writing-clearly/references
curl -Lo .claude/skills/writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo .claude/skills/writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
git add .claude/
git commit -m "Добавлен скилл ясного письма"
```

Claude автоматически подхватит скилл при запросах типа «напиши документацию», «отредактируй текст», «убери воду».

---

### Cursor

Cursor поддерживает несколько способов добавления правил.

#### Способ 1: Файл .cursorrules (legacy, но работает)

Создай файл `.cursorrules` в корне своего проекта:

```bash
# Из склонированного репо
cp writing-clearly/references/style-guide.md /путь/к/твоему/проекту/.cursorrules

# Или через curl (в корне твоего проекта)
curl -Lo .cursorrules https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

#### Способ 2: Директория .cursor/rules/ (рекомендуется)

В корне твоего проекта:

```bash
mkdir -p .cursor/rules
curl -Lo .cursor/rules/writing-clearly.mdc https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
```

#### Способ 3: Глобальные настройки

1. Открой `Cursor -> Settings -> Cursor Settings -> Rules for AI`
2. Скопируй содержимое [style-guide.md](https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md)

#### Способ 4: Agent Skills (если поддерживается)

В корне твоего проекта:

```bash
mkdir -p .cursor/skills/writing-clearly/references
curl -Lo .cursor/skills/writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo .cursor/skills/writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

---

### Gemini CLI

Gemini CLI использует файлы `GEMINI.md` для контекста.

#### Глобальный контекст (для всех проектов)

```bash
mkdir -p ~/.gemini
# Из склонированного репо (из корня writing-clearly/)
cat writing-clearly/SKILL.md writing-clearly/references/style-guide.md > ~/.gemini/GEMINI.md

# Или через curl
{ curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md; echo; curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md; } > ~/.gemini/GEMINI.md
```

#### Проектный контекст

В корне твоего проекта:

```bash
# Через curl (рекомендуется)
{ curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md; echo; curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md; } > GEMINI.md
```

#### Модульный подход с импортами

Сначала скачай файлы в свой проект:

```bash
mkdir -p writing-clearly/references
curl -Lo writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

Затем создай `GEMINI.md` в корне проекта:

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

В корне твоего проекта:

```bash
# Через curl
{ curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md; echo; curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md; } > AGENTS.md
```

Глобальный конфиг:

```bash
mkdir -p ~/.codex
{ curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md; echo; curl -sL https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md; } > ~/.codex/AGENTS.md
```

#### Способ 2: Agent Skills (рекомендуется)

Глобальная установка:

```bash
mkdir -p ~/.codex/skills/writing-clearly/references
curl -Lo ~/.codex/skills/writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo ~/.codex/skills/writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

Для проекта (в корне твоего проекта):

```bash
mkdir -p .codex/skills/writing-clearly/references
curl -Lo .codex/skills/writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo .codex/skills/writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

---

### Google Antigravity

Antigravity использует Rules и Workflows.

#### Через интерфейс

1. Нажми `...` в правом верхнем углу
2. Выбери `Customizations` → `Rules`
3. Скопируй содержимое [style-guide.md](https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md)

#### Через файлы

Глобальные правила:
```bash
mkdir -p ~/.antigravity
curl -Lo ~/.antigravity/rules.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

Проектные правила (в корне твоего проекта):
```bash
mkdir -p .antigravity
curl -Lo .antigravity/rules.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

---

### VS Code + GitHub Copilot

VS Code с GitHub Copilot поддерживает Agent Skills (в preview).

1. Включи `chat.useAgentSkills` в настройках VS Code
2. В корне твоего проекта выполни:

```bash
mkdir -p .github/skills/writing-clearly/references
curl -Lo .github/skills/writing-clearly/SKILL.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/SKILL.md
curl -Lo .github/skills/writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

---

### Другие агенты

#### Windsurf

В корне твоего проекта:

```bash
curl -Lo .windsurfrules https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

#### Continue.dev

В корне твоего проекта:

```bash
curl -Lo .continuerules https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

#### Aider

Сначала скачай файл:

```bash
mkdir -p writing-clearly/references
curl -Lo writing-clearly/references/style-guide.md https://raw.githubusercontent.com/nikitaCodeSave/writing-clearly/main/writing-clearly/references/style-guide.md
```

Затем создай файл `.aider.conf.yml`:

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

После клонирования репозитория:

```
writing-clearly/              # Корень репозитория (после git clone)
├── README.md                 # Этот файл с инструкциями
└── writing-clearly/          # Папка со скиллом
    ├── SKILL.md              # Основной файл (~60 строк)
    │                         # Краткая памятка и workflow
    └── references/
        └── style-guide.md    # Подробные правила (~250 строк)
                              # Таблицы замен, примеры, чек-лист
```

**Важно:** При копировании в свой проект копируй только внутреннюю папку `writing-clearly/` (ту, что содержит `SKILL.md`).

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
