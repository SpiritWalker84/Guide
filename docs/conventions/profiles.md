# Профили генератора

Профили лежат в `profiles/*.yaml` и **мержатся** с `defaults.yaml` во время работы генератора.

## Список профилей

| Имя | Назначение |
|-----|------------|
| `base` | Универсальный модульный OOP-старт |
| `telegram-bot` | Бот Telegram, разделение handlers / services |
| `fastapi` | Backend на FastAPI |
| `cli-tool` | CLI-утилита с модулями команд (**без** Docker) |
| `flask-webapp` | Flask с шаблонами и статикой |
| `flask-api-frontend` | Flask REST API + отдельный frontend |

## Общие обязательные файлы (для сервисных профилей с Docker)

Для большинства профилей с контейнеризацией:

- `.env.example`
- `README.md`
- `requirements.txt`
- `docker-compose.yml`
- `Dockerfile` (или для split-профиля — `backend/Dockerfile` и `frontend/Dockerfile`)

`cli-tool`: без `docker-compose.yml` и `Dockerfile`; обязательны `.env.example`, `README.md`, `requirements.txt`.

---

## `base`

- **project_kind:** `general`
- **Каталоги:** `src`, `tests`, `config`, `scripts`, `artifacts`
- **Правила:** слоистая модульная архитектура; мелкие SRP-классы; секреты из env; Dockerfile + compose с одним сервисом на свободном порту.

## `telegram-bot`

- **project_kind:** `telegram_bot`
- **Каталоги:** `src`, `src/bot`, `src/handlers`, `src/services`, `src/repositories`, `src/config`, `tests`, `artifacts`
- **Зависимости:** `python-dotenv`, `aiogram`
- **env:** `BOT_TOKEN`, `LOG_LEVEL`
- **Правила:** handlers отдельно от бизнес-сервисов; токен не в коде; OOP для инициализации бота и сервисов; Dockerfile на `python:3.12-slim`; compose — один сервис бота, часто без портов.

## `fastapi`

- **project_kind:** `fastapi_service`
- **Каталоги:** `src`, `src/api`, `src/core`, `src/services`, `src/repositories`, `tests`, `artifacts`
- **Зависимости:** `fastapi`, `uvicorn`, `pydantic-settings`, `python-dotenv`
- **env:** `APP_HOST`, `APP_PORT`, `DATABASE_URL`
- **Правила:** API отдельно от service/repository; DI через FastAPI dependencies; конфиг из env; Dockerfile + uvicorn; compose — приложение на **8000**, опционально БД.

## `flask-webapp`

- **project_kind:** `flask_server_rendered`
- **Каталоги:** `src`, `src/routes`, `src/services`, `src/repositories`, `src/templates`, `src/static`, `src/config`, `tests`, `artifacts`
- **Зависимости:** `flask`, `python-dotenv`, `gunicorn`
- **env:** `FLASK_ENV`, `SECRET_KEY`, `HOST`, `PORT`, `DATABASE_URL`
- **Правила:** тонкие роуты, логика в сервисах; Jinja и static в отдельных каталогах; конфиг из env; Dockerfile + gunicorn; compose — web на **5000**, опционально БД.

## `flask-api-frontend`

- **project_kind:** `flask_api_plus_frontend`
- **Каталоги:** `backend`, `backend/src`, `backend/src/api`, `backend/src/services`, `backend/src/repositories`, `backend/src/config`, `frontend`, `tests`, `artifacts`
- **Зависимости backend:** `flask`, `flask-cors`, `python-dotenv`
- **env:** `API_HOST`, `API_PORT`, `CORS_ORIGINS`, `DATABASE_URL`, `VITE_API_BASE_URL`
- **Правила:** backend и frontend — отдельные top-level модули; backend только REST; CORS из env; описать dev-сервер фронта и базовый URL API; backend Dockerfile + gunicorn; frontend — multi-stage (node build + nginx); compose: backend, frontend, опционально БД; **nginx проксирует `/api/`** на backend.

## `cli-tool`

- **project_kind:** `cli_app`
- **Compose:** `include_compose: false`
- **Качество:** `prefer_composition: false` (в отличие от остальных профилей)
- **Каталоги:** `src`, `src/commands`, `src/core`, `tests`, `artifacts`
- **Зависимости:** `typer`, `python-dotenv`
- **env:** `LOG_LEVEL`
- **Правила:** каждая команда — отдельный модуль; слой парсинга CLI отдельно от бизнес-логики; классы для core-сервисов и конфигурации; **не** генерировать Docker/compose.
