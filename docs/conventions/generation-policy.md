# Политика генерации (`generation_policy`)

Настройки из `defaults.yaml` влияют на то, **что именно** считается допустимым результатом генерации и какие проверки выполняются.

## Запреты и требования к «живому» коду

| Флаг / правило | Смысл |
|----------------|--------|
| `no_placeholder_implementations: true` | Не оставлять «игрушечные» заглушки вместо реальной связки кода. |
| `require_runnable_wiring: true` | Должна быть сквозная сборка: точка входа, bootstrap/DI, регистрация маршрутов/обработчиков/клиентов — сервис должен **запускаться**. |
| `forbid_empty_handler_bodies: true` | Пустые тела обработчиков в продуктивной логике недопустимы. |
| `pin_explicit_versions: true` | В `requirements.txt` — **явные совместимые версии** зависимостей. |

Согласовано с `prompt_rules`:

- Не оставлять продакшен-логику как один `pass`, только TODO, `NotImplementedError` или пустые методы — нужно **минимально рабочее** поведение.
- Если фича вне scope — **опустить** или **явно задокументировать**, не добавлять фиктивные модули с одним `pass`.

## Версии библиотек и код

- **`dependency_major_must_match_code: true`** — каждый импорт и вызов API должен соответствовать **мажорной версии** указанной библиотеки (не смешивать примеры из разных эпох одного пакета).

## OpenAI Python SDK

- **`enforce_openai_sdk_consistency: true`** — стиль использования пакета `openai` в коде должен соответствовать тому, что закреплено в `requirements.txt` (например, SDK ≥1.x vs legacy `ChatCompletion` / `.acreate`). Реализация проверки: `codegen/stack_checks.py` (`assert_openai_sdk_matches_requirements`).

## Предупреждение по «заглушкам» `pass`

- **`stub_pass_warning_threshold: 14`** — если в **не-тестовых** `.py` слишком много строк с голым `pass`, в лог пишется предупреждение (эвристика незавершённых заглушек).

## Прочие флаги defaults

- `include_dotenv_example: true` — в проекте должен быть `.env.example`.
- `include_readme: true` — генерируется README.
- `include_requirements: true` — `requirements.txt`.
- `include_compose: true` — по умолчанию ожидается Docker Compose (у `cli-tool` в профиле `include_compose: false` и нет Dockerfile/compose по правилам профиля).

---

## Дословно: `prompt_rules` из `defaults.yaml`

Ниже — англоязычные формулировки из конфига (как уходят в сводные правила для генерации):

- Always generate a docker-compose.yml that starts the project with docker compose up -d.
- docker-compose.yml must define all services, expose correct ports, and pass env vars from .env.
- Use Dockerfile per service, do not use pre-built images for application code.
- Generate README.md in Russian language.
- README must explicitly mention: HTTP by default unless TLS is configured separately.
- README.md must follow readme_onboarding.required_sections_ru from rules: purpose, stack, repo layout, run, env, dev/tests — written so another engineer can onboard without reading the whole codebase.
- Do not leave production logic as pass, TODO-only, NotImplementedError, or empty methods; implement minimal working behavior.
- requirements.txt must pin compatible versions; every import and API call must match the major version of that library (no mixed-era snippets).
- Wire the app end-to-end: entrypoint, DI/bootstrap, and registration of handlers/routes/clients so the service can start.
- If a feature is out of scope, omit it or document clearly — do not add fake modules that only contain pass.
- Unless the task explicitly names another language for documentation inside code, use professional Russian for all comments and docstrings in source files.
