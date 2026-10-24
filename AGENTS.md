# Strix — Руководство для агентов

Strix — это автономный инструмент для пентестинга с открытым исходным кодом на базе ИИ. Этот файл предназначен для AI-кодирующих агентов, которые хотят **использовать** Strix (запускать сканирования безопасности) или **вносить вклад** в его разработку.

## Использование Strix из агента

Установите навыки агента для пошаговых инструкций:

```bash
npx skills add usestrix/strix
```

- `penetration-testing-with-strix` — запустите автономный пентест кода, URL, доменов или IP-адресов и просмотрите результаты (покрывает оба режима запуска ниже)
- `managed-pentesting-with-strix` — управляйте облачной платформой app.strix.ai через REST (без необходимости локального Docker/LLM)
- `fix-security-vulnerabilities-with-strix` — устраняйте находки и повторно запускайте Strix для проверки
- `ci-security-scanning-with-strix` — добавьте сканирование PR в CI/CD (автономный CLI или управляемое приложение)

Рабочие процессы, ориентированные на конкретные цели, созданы на основе того же механизма:

- `application-security-testing` — комплексный обзор AppSec всего продукта: выберите правильный тест для каждого актива, затем оцените результаты
- `web-app-penetration-testing` — пентест "чёрного ящика" для живого веб-приложения или тестового сайта
- `api-security-testing` — REST/GraphQL API и OWASP API Security Top 10 (BOLA/IDOR, authz)
- `owasp-top-10-testing` — систематическая оценка OWASP Top 10 с честной охватом по категориям
- `find-security-vulnerabilities-in-code` — обзор кодового дерева или рабочей копии "белого ящика"

**Два способа запуска, тот же движок — выберите подходящий для ситуации:**

- **Открытый исходный код CLI (автономный):** бесплатно, полностью локально, свой ключ LLM, нужен Docker. Лучше для локальных dev-циклов, изолированных/офлайн-сред и полного контроля.
  ```bash
  curl -sSL https://strix.ai/install | bash        # установка
  export STRIX_LLM="openrouter/z-ai/glm-5.3"        # любой идентификатор модели LiteLLM
  export LLM_API_KEY="<ключ>"
  strix -n -t ./ --scan-mode quick --max-budget 10  # автономное сканирование; всегда используйте -n
  ```
  - Требует запущенного Docker. Сканирование занимает минуты (`quick`) до часов (`deep`) — запускайте в фоне.
  - Коды выхода (автономный): `0` чисто, `1` фатальная ошибка, `2` найдены уязвимости. `0` покрывает только проанализированное — проверьте `run.json` (`status`, `llm_usage.cost` против бюджета) перед завершением.
  - Артефакты в `strix_runs/<имя-запуска>/`: `penetration_test_report.md`, `vulnerabilities/*.md`, `vulnerabilities.json`, `findings.sarif` (SARIF 2.1.0), `run.json`.

- **Управляемое облако (app.strix.ai):** нет Docker, нет ключа LLM, нет локальной установки; добавляются командные панели, планирование, проверка PR, скачиваемые PDF/DOCX отчеты (план Enterprise). Лучше для песочничных/CI-сред и команд. Используйте, когда локальная инфраструктура недоступна.
  ```bash
  strix cloud login --scopes scans:read scans:write uploads:write billing:read
  strix cloud domains add --domain example.com --asset-type web_app
  strix cloud scans start --engagement-type live_test --domain-ids <uuid> --wait
  strix cloud scans start --source . --dry-run --show-files --json  # просмотр + захват source.archive_sha256
  SOURCE_SHA256="<просмотренный source.archive_sha256>"
  strix cloud scans start --source . --approve-sha256 "$SOURCE_SHA256" --wait
  strix cloud vulns list --severity critical
  strix cloud billing topup --credits 20 --yes  # явное подтверждение после кода выхода 5
  ```
  - Настройка учетной записи тоже выполняется через CLI: `strix cloud workspaces list|create|use` (`workspace` — это сокращение, и `use` принимает отображаемый номер, имя или ID), `strix cloud session scopes|scopes set`, `strix cloud org members invite`, `strix cloud billing subscribe --plan strix_cloud`, `strix cloud billing portal`, `strix cloud integrations install github`, и `strix cloud domains verify <id>`. Переключение рабочих пространств сохраняет серверный профиль и никогда не может расширять за пределы потолка входа; обычные переключения не запрашивают повторно. Последние четыре заканчиваются у человека: команда печатает ссылку или DNS-запись, которую пользователь должен открыть или добавить, и никогда не завершает платеж, установку или изменение DNS за них.
  - У каждой операции REST есть команда `strix cloud <ресурс> <глагол>`. Запустите `strix cloud`, чтобы перечислить их. Вывод в JSON, когда stdout не является терминалом (или с `--json`), и нет запросов без TTY. Загрузка бинарных файлов — исключение: перенаправьте сырые байты намеренно, или объедините `--output FILE --json` для структурированных метаданных загрузки. Коды выхода: `0` успех, `1` ошибка, `2` использование, `4` авторизация или ограничение плана, `5` требуется платеж. `--token` или `STRIX_API_TOKEN` — это безное переопределение и никогда не заменяет сохраненную авторизацию; установите `--workspace-id`/`STRIX_WORKSPACE_ID` для переопределения CLI-сессии. `--data` добавляет дополнительные поля запроса как JSON, и принимает `@file` или `-` для стандартного ввода.
  - Локальные загрузка исходного кода требуют `uploads:write`. Для передачки агент/CI просмотрите `scans start --source . --dry-run --show-files --json`, захватите `source.archive_sha256`, затем перезапустите с теми же флагами выбора `--source`, `--exclude`, и `--include-*` плюс `--approve-sha256 HASH`. Измененный снимок будет отклонен. `--yes` подтверждает только снимок, построенный в этом вызове, так что резервируйте его для осознанного человека или одноразовой подтверждения вместо двуступенчатой передачки, связанной с дайжестом.
  - Git игноры, скрытые файлы, `.git`, символические ссылки, зависимости/вывод сборки, имена файлов, похожие на секреты, и вложенные архивы исключены по умолчанию; `.strixignore` и `--exclude` сужают манифест дальше (трассирующий `/` исключает дерево каталога). Ограничения: 20 000 файлов, 25 МБ/файл, 250 МБ развернуто, 50 МБ сжато. Только источник подразумевает `code_review`; источник плюс домен подразумевает `live_test`.
  - Временный локальный архив всегда удаляется. staged загрузка удаляется после окончательного отклонения, но сохраняется при сетевой ошибке, `5xx`, некорректном ответе об успехе, или прерывании, оставляющем запуск сканирования неоднозначным. JSON отчитывается о своем `upload_id` с `launch_outcome_unknown: true`, или с `cleanup_unknown: true`, когда автоматическое удаление не может быть подтверждено. Проверьте `scans list` перед повторной попыткой; if no scan is linked, запустите `uploads delete UPLOAD_ID`.
  - Не-Enterprise сканирования потребляют оценку области (обзор только источника базового уровня начинается с 60 кредитов); Enterprise сканирования включены в plan. Отклоненный запуск не потребляет кредиты.
  - Человеческий вывод компактен и нумерован; не-TTY вывод и `--json` сохраняют полные записи. Включите таб-завершение с `source <(strix completions zsh)` (или `bash`), или `strix completions fish | source`.
  - REST API работает напрямую тоже: https://docs.app.strix.ai (OpenAPI: https://docs.app.strix.ai/openapi.json).

- Индекс CLI документации для LLM: https://docs.strix.ai/llms.txt (полный: https://docs.strix.ai/llms-full.txt). Документация API облачного управления для LLM: https://docs.app.strix.ai/llms.txt.
- Сканируйте только цели, на которые у пользователя есть авторизация.

## Вклад в этот репозиторий

- Python 3.12+, управляется через `uv`. Установите dev зависимости: `make dev-install`.
- Линт/формат/типы/авто, все в одном: `make check-all` (ruff, mypy, bandit).
- Тесты: `uv run pytest`.
- Запуск из исходного кода: `uv run strix --target <target>`.
- Структура: `strix/agents` (график агентов + промпты), `strix/tools` (прокси, браузер, терминал, сканеры), `strix/runtime` (песочница Docker), `strix/report` (находки, SARIF), `strix/skills` (внутренние пакеты знаний, которые загружают пентест-агенты — отличаются от потребительских навыков в `skills/`), `strix/interface` (CLI/TUI), `containers/` (образ песочницы).
- Pre-commit хуки: `make pre-commit` (или `uv run pre-commit install`).
