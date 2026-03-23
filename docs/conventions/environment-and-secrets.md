# Конфигурация, переменные окружения и секреты

## Принципы

- **Секреты никогда не хранить в исходниках** — только переменные окружения (и документация в `.env.example` без реальных значений).
- Runtime-конфигурация (хосты, порты, строки подключения, ключи API) — из **окружения** или через загрузку из `.env` в разработке, как принято в стеке (часто `python-dotenv`).

## Обязательный артефакт

- В генерируемом проекте — **`.env.example`** со списком переменных и краткими комментариями (без секретов).

## Переменные окружения генератора (этот репозиторий)

Пример из `.env.example` корня ProxyAI Code Generator:

- `OPENAI_API_KEY` — ключ API
- `OPENAI_BASE_URL` — базовый URL совместимого с OpenAI API (например ProxyAPI)
- `OPENAI_MODEL` — имя модели
- `MAX_FILES`, `MAX_FILE_BYTES` — ограничения генерации (опционально)
- `DEFAULT_BASE_DIR` — базовый каталог для вывода проектов в web UI (в Docker часто `/workspace/projects`)

## Типичные ключи по профилям генерируемых проектов

Сводка из `profiles/*.yaml` (в генерируемом README они должны быть описаны в разделе «Конфигурация»):

| Профиль | Примеры `env_keys` |
|---------|---------------------|
| `cli-tool` | `LOG_LEVEL` |
| `fastapi` | `APP_HOST`, `APP_PORT`, `DATABASE_URL` |
| `flask-webapp` | `FLASK_ENV`, `SECRET_KEY`, `HOST`, `PORT`, `DATABASE_URL` |
| `telegram-bot` | `BOT_TOKEN`, `LOG_LEVEL` |
| `flask-api-frontend` | `API_HOST`, `API_PORT`, `CORS_ORIGINS`, `DATABASE_URL`, `VITE_API_BASE_URL` |

Токен Telegram-бота **не** помещать в код — только env (явное правило в профиле `telegram-bot`).
