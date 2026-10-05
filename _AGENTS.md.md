- `AGENTS.md` — общий файл инструкций для разных ИИ-агентов (Codex, Cursor и других). По сути тот же [CLAUDE.md](_CLAUDE.md.md), только не привязан к Claude.
- Claude Code умеет читать `AGENTS.md` сам, ничего настраивать не надо.
- Когда читает
	- По умолчанию — только если в проекте нет своего `CLAUDE.md`.
		- Есть `AGENTS.md`, нет `CLAUDE.md` — читает `AGENTS.md`.
		- Есть оба — только `CLAUDE.md`.
		- `CLAUDE.md` импортирует `AGENTS.md` — читает оба, см. «Один файл на все инструменты».
	- Мешают только файлы проекта: `CLAUDE.md`, `.claude/CLAUDE.md`, `CLAUDE.local.md`. Глобальный `~/.claude/CLAUDE.md` не мешает.
		- Осторожно: если завести `CLAUDE.local.md` для своих заметок, Claude перестанет читать `AGENTS.md`.
	- `AGENTS.md` из подпапки подгружается, когда Claude читает файлы в ней.
	- `AGENTS.local.md`, `AGENTS.override.md` и папку `.agents/` не читает.
	- Загрузился ли — видно в [/memory](!memory.md).
- Поменять поведение
	- [/config](!config.md) → Project instructions:
		- `claude-md-or-agents-md` — по умолчанию: `AGENTS.md`, только если нет `CLAUDE.md`;
		- `claude-md-and-agents-md` — читать оба;
		- `claude-md` — только `CLAUDE.md`.
- Один файл на все инструменты
	- Если в проекте нужны и `AGENTS.md`, и что-то своё для Claude — завести `CLAUDE.md` с импортом:
		```markdown
		@AGENTS.md
		
		## Claude Code
		
		Правки в `src/billing/` — только через plan mode.
		```
		- Сначала Claude прочитает `AGENTS.md`, потом остальное.
	- Если своего ничего нет — можно симлинк `ln -s AGENTS.md CLAUDE.md`. Но на Windows симлинки работают плохо, импорт надёжнее.
- Переехать с других агентов
	- `/init` сам подтягивает правила Cursor и Copilot в новый `CLAUDE.md`.
	- `/import` — разово перенести настройки другого агента: `AGENTS.md`, [MCP](MCP.md)-серверы, команды, [skills](skills.md).
- Советы
	- Общие правила держать в одном месте — в `AGENTS.md`. Копия в `CLAUDE.md` со временем разойдётся с оригиналом.
	- `AGENTS.md` писать без особенностей Claude Code: `/команды`, plan mode и т. п. другие агенты не поймут. Это — в `CLAUDE.md` после `@AGENTS.md`.
	- В проекте с `AGENTS.md` нужен `CLAUDE.local.md` — сначала завести `CLAUDE.md` с `@AGENTS.md`, иначе `AGENTS.md` перестанет читаться.
	- Писать по тем же правилам, что [CLAUDE.md](_CLAUDE.md.md): коротко, конкретно, без того, что видно из кода.
