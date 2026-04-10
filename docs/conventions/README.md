# Конвенции разработки (Guide)

Эта папка — **выжимка правил**, изначально заложенных в проекте ProxyAI Code Generator (`defaults.yaml`, профили, пайплайн, проверки стека). В чате ссылайтесь на репозиторий: **https://github.com/SpiritWalker84/Guide** — «следуй `docs/conventions/README.md` и связанным файлам».

## Оглавление

| Файл | Содержание |
|------|------------|
| [quality-and-architecture.md](quality-and-architecture.md) | ООП, модульность, слои, композиция, качество кода |
| [code-style-and-comments.md](code-style-and-comments.md) | Простой читаемый код, docstrings и комментарии на русском |
| [generation-policy.md](generation-policy.md) | Политика генерации: без заглушек, версии, OpenAI SDK, `pass` |
| [readme-onboarding.md](readme-onboarding.md) | Обязательные разделы README на русском |
| [docker-and-compose.md](docker-and-compose.md) | Docker, compose, порты, переменные окружения |
| [environment-and-secrets.md](environment-and-secrets.md) | `.env`, секреты, конфигурация |
| [profiles.md](profiles.md) | Профили: структура каталогов и специфичные правила |
| [pipeline-and-checks.md](pipeline-and-checks.md) | Этапы пайплайна, артефакты, stack checks |
| [llm-behavior.md](llm-behavior.md) | Промпты LLM, постобработка README, лимиты, анализ задачи |
| [tz-analysis-workflow.md](tz-analysis-workflow.md) | Перед кодом: разбор ТЗ, риски, вопросы с вариантами A)/B) и плюсами/минусами |
| [code-review.md](code-review.md) | Ревью в пайплайне генератора; саморевью ассистента; чеклист после реализации |
| [cursor-ai-playbook.md](cursor-ai-playbook.md) | Процесс фич с ИИ в Cursor: спеки, задачи; **дополняет** этот Guide, не заменяет |

Исходный код генератора (вне этого репозитория): `defaults.yaml`, `profiles/*.yaml`, `codegen/pipeline.py`, `codegen/task_analysis.py`, `codegen/stack_checks.py`, корневой `README.md`.
