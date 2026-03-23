# Guide — конвенции для генерации и разработки кода

Публичный набор правил и чеклистов (OOP, модульность, env, русские docstrings, Docker/README, профили и т.д.). Репозиторий содержит **только документацию** в каталоге [`docs/conventions/`](docs/conventions/README.md).

**Канонический URL:** https://github.com/SpiritWalker84/Guide

---

## Как ссылаться из чата (Cursor, другой ассистент)

Скопируйте и при необходимости дополните задачей:

```text
Напиши код по указаниям из репозитория https://github.com/SpiritWalker84/Guide
Сначала прочитай оглавление и все релевантные файлы в docs/conventions/ (начни с docs/conventions/README.md).
Соблюдай эти правила полностью. Затем выполни мою задачу: <кратко опишите задачу>.
```

Короткий вариант:

```text
Код и структура проекта — строго по гайду: https://github.com/SpiritWalker84/Guide (docs/conventions/). Задача: …
```

Для моделей с доступом к URL укажите ветку `main` и путь к файлам; при отсутствии доступа к GitHub приложите содержимое нужных `.md` или используйте «Add to Chat» / вложение файлов из локального клона.

---

## Локальный клон

```bash
git clone https://github.com/SpiritWalker84/Guide.git
cd Guide
```

Оглавление разделов: [docs/conventions/README.md](docs/conventions/README.md).

---

## Происхождение

Материалы изначально сведены из проекта **ProxyAI Code Generator** (`defaults.yaml`, профили, пайплайн LLM, проверки стека). Этот репозиторий — автономная копия только документации, без кода генератора.
