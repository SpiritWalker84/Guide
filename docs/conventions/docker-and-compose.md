# Docker и Docker Compose

Требования из `prompt_rules` в `defaults.yaml` и уточнения профилей.

## Общие правила

- Всегда генерировать **`docker-compose.yml`**, с которым проект поднимается командой **`docker compose up -d`** (если профиль не отключает compose — см. `cli-tool`).
- В `docker-compose.yml` должны быть **все сервисы**, **корректные порты**, переменные окружения **из `.env`** (не хардкодить секреты в compose без необходимости; секреты — через env-файл).
- Для кода приложения использовать **Dockerfile на сервис**, **не** полагаться на готовые образы «с приложением внутри» вместо своего Dockerfile.

## README и HTTP

- В README сгенерированного проекта должно быть явно сказано, что **по умолчанию HTTP**, если TLS настроен отдельно.

## Профили (ориентиры портов и образов)

| Профиль | Compose | Примечания |
|---------|---------|------------|
| `base` | Да | Один сервис приложения на свободном порту |
| `fastapi` | Да | Образ на базе `python:3.12-slim`, `uvicorn`; типично порт **8000**, опционально БД |
| `flask-webapp` | Да | `python:3.12-slim`, `gunicorn`; типично порт **5000**, опционально БД |
| `telegram-bot` | Да | `python:3.12-slim`, бот-сервис, **порты часто не нужны** |
| `flask-api-frontend` | Да | Backend `gunicorn`, frontend: **node build + nginx**; nginx **проксирует `/api/`** на backend |
| `cli-tool` | **Нет** | **Не** генерировать `docker-compose.yml` и **Dockerfile** |

Подробнее структура каталогов — в [profiles.md](profiles.md).

## Пример из репозитория генератора (не из генерируемого проекта)

В самом ProxyAI Code Generator в `docker-compose.yml` backend монтирует хостовый каталог в `/workspace/projects`; в UI базовый путь по умолчанию совпадает с этим маппингом — см. [pipeline-and-checks.md](pipeline-and-checks.md) и корневой `README.md`.
