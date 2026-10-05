- Claude сам работает с git: смотрит историю, создаёт ветки, коммитит, открывает PR.
- Просить словами: «закоммить», «создай ветку под фичу», «сделай PR».
- PR создаёт через `gh pr create` (GitHub) или `glab mr create` (GitLab) — нужен установленный CLI.
- Про GitHub App и Actions — [Github integration](Github%20integration.md).
- Полезное
	- [/diff](!diff.md) — посмотреть изменения в рабочей папке, включая правки Claude.
	- `claude --from-pr 1234` — найти сессию, в которой был создан PR 1234. Или вставить ссылку на PR в поиск [/resume](!resume.md).
	- `/autofix-pr` — облачная сессия следит за PR текущей ветки и пушит исправления, когда падает CI или приходят комментарии.
	- Ревью перед PR — [code review](code%20review.md).
	- Несколько веток параллельно — [worktrees](worktrees.md).
- Подпись Claude
	- По умолчанию в коммит добавляется строка `Co-Authored-By: Claude …`, в описание PR — `🤖 Generated with Claude Code`.
	- Изменить или убрать — `attribution` в [settings.json](_settings.json.md):
		```json
		{
		  "attribution": {
		    "commit": false,
		    "pr": "Assisted by Claude Code"
		  }
		}
		```
		- `false` — убрать, строка — своя подпись.
		- Старая настройка `includeCoAuthoredBy` устарела, теперь `attribution`.
	- `includeGitInstructions: false` — убрать встроенные инструкции Claude про коммиты и PR. Если хочешь задать свои через `CLAUDE.md` или [skills](skills.md).
- Осторожно
	- [/rewind](!rewind.md) откатывает правки файлов, но не коммиты и не `push`.
	- В режиме [auto](режимы.md#^auto) обычный `push` в текущий репозиторий проходит без вопросов, force push блокируется.
		- Нужна точка проверки перед `push` — `permissions.ask` или сказать «не пушь».
- Советы
	- Коммитить часто и маленькими шагами: коммит — настоящая точка отката, см. [опасные действия](опасные%20действия.md).
	- Перед коммитом смотреть [/diff](!diff.md).
	- Сообщение коммита просить написать Claude: он видит и diff, и зачем это делали.
	- Правила для коммитов и веток (формат сообщений, язык, имена веток) — в [CLAUDE.md](_CLAUDE.md.md).
	- Спрашивать Claude про историю: «почему здесь так?», «когда поменяли этот API?» — он поищет в `git log` и `blame`.
