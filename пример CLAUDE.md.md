- Пример `CLAUDE.md` для Python-проекта: стек, архитектура, стандарты кода, проверки, команды.
	````markdown
	# Project Overview
	
	Краткое описание проекта (2–5 предложений).
	
	## Stack
	
	- Python 3.13
	- FastAPI
	- PostgreSQL
	- Redis
	- Docker
	
	## Architecture
	
	- app/
	    api/
	    services/
	    repositories/
	    models/
	
	Принципы:
	- бизнес-логика находится только в services
	- API не работает напрямую с БД
	- репозитории не содержат бизнес-логики
	
	## Coding Standards
	
	- использовать type hints
	- использовать dataclasses только для DTO
	- предпочтительно pathlib вместо os.path
	- функции до 50 строк
	- избегать наследования без необходимости
	
	## Testing
	
	После изменений обязательно:
	
	- pytest
	- ruff check
	- ruff format
	- mypy
	
	## Commands
	
	```bash
	uv sync
	uv run pytest
	uv run ruff check .
	uv run mypy .
	```
	````
