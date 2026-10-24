# Strix

### Открытый исходный код инструмент для пентестинга с ИИ. Автономные ИИ пентестеры, которые находят и исправляют уязвимости вашего приложения.

<br/>

<a href="https://docs.strix.ai"><img src="https://img.shields.io/badge/Docs-docs.strix.ai-2b9246?style=for-the-badge&logo=gitbook&logoColor=white" alt="Документация"></a>
<a href="https://strix.ai"><img src="https://img.shields.io/badge/Website-strix.ai-f0f0f0?style=for-the-badge&logoColor=000000" alt="Веб-сайт"></a>
[![](https://dcbadge.limes.pink/api/server/strix-ai)](https://discord.gg/strix-ai)

<a href="https://app.strix.ai?utm_source=github&utm_medium=readme&utm_content=badge_cloud"><img src="https://img.shields.io/badge/Strix%20Cloud-app.strix.ai-2b9246?style=for-the-badge&logoColor=white" alt="Strix Cloud"></a>
<a href="https://strix.ai/demo?utm_source=github&utm_medium=readme&utm_content=badge_demo"><img src="https://img.shields.io/badge/Try%20Strix%20Enterprise-555555?style=for-the-badge&logoColor=white" alt="Попробуйте Strix Enterprise"></a>

<a href="https://deepwiki.com/usestrix/strix"><img src="https://deepwiki.com/badge.svg" alt="Спросите DeepWiki"></a>
<a href="https://github.com/usestrix/strix"><img src="https://img.shields.io/github/stars/usestrix/strix?style=flat-square" alt="GitHub Stars"></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-3b82f6?style=flat-square" alt="Лицензия"></a>
<a href="https://pypi.org/project/strix-agent/"><img src="https://img.shields.io/pypi/v/strix-agent?style=flat-square" alt="PyPI Version"></a>


<a href="https://discord.gg/strix-ai"><img src="https://github.com/usestrix/.github/raw/main/imgs/Discord.png" height="40" alt="Присоединяйтесь к Discord"></a>
<a href="https://x.com/strix_ai"><img src="https://github.com/usestrix/.github/raw/main/imgs/X.png" height="40" alt="Следите на X"></a>


<a href="https://trendshift.io/repositories/15362?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-15362" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/repositories/15362/weekly" alt="usestrix%2Fstrix | Trendshift" width="250" height="55"/></a>
<a href="https://trendshift.io/repositories/15362" target="_blank"><img src="https://trendshift.io/api/badge/repositories/15362" alt="usestrix/strix | Trendshift" width="250" height="55"/></a>

</div>

> [!TIP]
> **Новое!** Strix интегрируется с GitHub Actions и CI/CD конвейерами. Автоматически сканируйте на наличие уязвимостей при каждом pull request и блокируйте небезопасный код до того, как он достигнет продакшена - [Начните с нулевой настройки](https://app.strix.ai?utm_source=github&utm_medium=readme&utm_content=tip_ci).

---


## Обзор Strix

Strix - это автономные ИИ пентестеры, которые действуют как настоящие хакеры - они динамически запускают ваш код, находят уязвимости и подтверждают их через реальные доказательства. Создано для разработчиков и команд безопасности, которым нужны быстрые и точные тесты безопасности без избыточной нагрузки на ручной пентестинг или инструменты статического анализа с ложными срабатываниями.

**Основные возможности:**

- **Полный набор инструментов для пентестинга** - разведка, эксплуатация и подтверждение уязвимостей из коробки
- **Оркестрация мультиагентов** - команды ИИ пентестеров, которые сотрудничают и масштабируются
- **Реальное подтверждение эксплуатации** - работающие доказательства уязвимостей, а не ложные срабатывания, как у устаревших сканеров уязвимостей
- **Интерфейс для разработчиков** - действительные находки с рекомендациями по устранению
- **Автоматическое исправление и отчетность** - генерация патчей и готовые к использованию отчеты о пентестинге для соответствия требованиям


<br>


<div align="center">
  <a href="https://strix.ai">
    <img src=".github/screenshot.png" alt="Демо Strix" width="1000" style="border-radius: 16px;">
  </a>
</div>


## Сферы применения

- **Тестирование безопасности приложений** - обнаружение и подтверждение критических уязвимостей в ваших приложениях
- **Быстрый пентестинг** - выполните пентестинг за часы, а не за недели, с отчетами о соответствии требованиям
- **Автоматизация баг-баунти** - автоматизируйте исследование баг-баунти и генерируйте доказательства для более быстрого отчетности
- **Интеграция в CI/CD** - запускайте тесты в CI/CD для блокировки уязвимостей до достижения продакшена

## 🚀 Быстрый старт

**Предварительные требования:**
- Docker (работающий)
- Ключ API LLM от любого [поддерживаемого провайдера](https://docs.strix.ai/llm-providers/overview) (OpenAI, Anthropic, Google и т.д.)

### Установка и первый сканирование

```bash
# Установите Strix
curl -sSL https://strix.ai/install | bash

# Настройте вашего провайдера ИИ
export STRIX_LLM="openrouter/z-ai/glm-5.3"
export LLM_API_KEY="ваш-api-ключ"

# Запустите первое тестирование безопасности
strix --target ./app-directory
```

> [!NOTE]
> Первый запуск автоматически загружает образ Docker песочницы. Результаты сохраняются в `strix_runs/<run-name>`

---

## Способы запуска Strix

- **Открытый исходный код** - бесплатно, работает локально с Docker и вашим собственным ключом LLM. [Быстрый старт](https://docs.strix.ai/quickstart)
- **Strix Cloud** - без настройки, подтвержденные находки, автофикс в один клик и проверка PR. [Запустите пентестинг →](https://app.strix.ai?intent=pentest&utm_source=github&utm_medium=readme&utm_content=table_cloud)
- **Enterprise** - SSO, отчеты о пентестинге, соответствующие требованиям, VPC или самостоятельное размещение. [Попробуйте Strix Enterprise →](https://strix.ai/demo?utm_source=github&utm_medium=readme&utm_content=table_demo)

---

## ☁️ Strix Cloud

Попробуйте платформу полного стека пентестинга Strix на **[app.strix.ai](https://app.strix.ai?utm_source=github&utm_medium=readme&utm_content=cloud_heading)** - зарегистрируйтесь бесплатно, подключите свои репозитории и домены, и запустите пентестинг за несколько минут.

- **Подтвержденные находки с доказательствами** - каждая уязвимость включает работающее доказательство уязвимости и шаги воспроизведения
- **Автофикс в один клик** - исправления безопасности, сгенерированные ИИ, как готовые к слиянию pull-запросы
- **Непрерывный пентестинг** - постоянное сканирование уязвимостей, которое поддерживает темп ваших развертываний
- **Интеграции DevSecOps** - GitHub, GitLab, Bitbucket, Slack, Jira, Linear и CI/CD конвейеры
- **Непрерывное обучение** - ИИ, который строит на прошлых находках, адаптируется к вашему кодовому базу и уменьшает количество ложных срабатываний со временем

[**Запустите пентестинг →**](https://app.strix.ai?intent=pentest&utm_source=github&utm_medium=readme&utm_content=cloud_cta)

## 🏢 Enterprise

Получите тот же опыт Strix с корпоративными контролями: SSO (SAML/OIDC), готовые к использованию отчеты о пентестинге, соответствующие требованиям (SOC 2, ISO 27001, PCI DSS), выделенная поддержка и SLA, настраиваемые варианты развертывания (VPC или самостоятельное размещение), поддержка модели BYOK и индивидуальные ИИ пентестеры, оптимизированные для вашей среды.

[**Попробуйте Strix Enterprise →**](https://strix.ai/demo?utm_source=github&utm_medium=readme&utm_content=enterprise_cta)

---

## 🤖 Используйте Strix из вашего кодирующего агента

Strix готов для агентов. Дайте Claude Code, Cursor, Codex или любому [совместимому с SKILL.md](https://agentskills.io) агенту возможность запускать пентестинг, исправлять находки и настраивать сканирование CI:

```bash
npx skills add usestrix/strix
```

Это устанавливает девять навыков для запуска пентестинга, исправления находок и сканирования CI, против кода, веб-приложений, API и OWASP Top 10. Агенты могут использовать локальный CLI или управляемую облачную платформу с одним и тем же движком.

См. [`AGENTS.md`](AGENTS.md) для быстрого справочника, [docs.strix.ai/llms.txt](https://docs.strix.ai/llms.txt) для CLI и [docs.app.strix.ai](https://docs.app.strix.ai) для API.

---

## ✨ Особенности

### Инструменты для пентестинга с ИИ

Агенты Strix оснащены всесторонним инструментарием для оффенсивной безопасности - теми же инструментами, которые используют профессиональные пентестеры и этичные хакеры:

- **HTTP-прокси** - полное манипулирование и анализ запросов/ответов с Caido
- **Эксплуатация браузера** - автоматизированный браузер для тестирования XSS, CSRF, кликджекинга и обхода аутентификации
- **Выполнение команд и оболочек** - интерактивный терминал для разработки эксплойтов и постэксплуатации
- **Пользовательский рантайм для эксплойтов** - песочница Python для написания и подтверждения доказательств уязвимостей
- **Разведка и OSINT** - автоматизированное картирование поверхности атаки, перечисление поддоменов и отпечатки
- **Статический и динамический анализ кода** - SAST + DAST для комплексного тестирования безопасности приложений
- **База знаний уязвимостей** - структурированные находки с оценкой CVSS и классификацией OWASP

### Комплексный сканер уязвимостей

Strix обнаруживает, подтверждает и эксплуатирует широкий спектр уязвимостей безопасности, охватывающих OWASP Top 10 и за его пределами:

- **Нарушенный контроль доступа** - IDOR, повышение привилегий, обход аутентификации
- **Атаки инъекций** - SQL-инъекции, NoSQL-инъекции, инъекции команд ОС, SSTI
- **Уязвимости серверной части** - SSRF, XXE, небезопасная десериализация, RCE
- **Атаки клиентской части** - XSS (хранимый/отраженный/DOM), загрязнение прототипа, CSRF
- **Логические уязвимости** - гонки, манипуляции платежами, обход рабочих процессов
- **Аутентификация и сессии** - атаки JWT, фиксация сессии, векторы подбора учетных данных
- **Инфраструктура и облако** - неправильные настройки, открытые сервисы, проблемы безопасности облака
- **Безопасность API** - нарушенная аутентификация, массовое назначение, обход ограничения скорости

### Граф агентов (мультиагентный пентестинг)

Расширенная оркестрация мультиагентов для комплексного автоматизированного пентестинга:

- **Распределенный пентестинг** - специализированные ИИ агенты для разведки, эксплуатации и постэксплуатации
- **Масштабируемое тестирование безопасности** - параллельное выполнение по нескольким целям для быстрого и комплексного покрытия
- **Динамическая координация** - агенты делятся открытиями, связывают уязвимости и сотрудничают, как красная команда

---

## 🖥️ Локальный веб-вьюер

Каждый сканирование записывает свои результаты на диск по мере выполнения. Запустите их в локальной панели управления одной командой:

```bash
# Откройте последний запуск
strix view

# ...или откройте конкретный запуск по имени
strix view my-run-name

# Показать вьюер на всех интерфейсах IPv4 на фиксированном порту
strix view --host 0.0.0.0 --port 8080 --no-open
```

Панель управления отображает находки, живую карту команды агентов и предыдущие запуски. Ничего не покидает ваш компьютер, и интерфейс поставляется с предустановленным. `strix view` привязывается к `127.0.0.1` и выводит токенизированную ссылку, которая предоставляет доступ к запуску, поэтому делитесь ею осторожно.

См. [документацию по вьюеру](https://docs.strix.ai/usage/viewer) для опций и для доступа к вьюеру с другого компьютера.

---

## Примеры использования

### Основное использование

```bash
# Сканирование локального кодового базы
strix --target ./app-directory

# Проверка безопасности GitHub репозитория
strix --target https://github.com/org/repo

# Проверка безопасности веб-приложения
strix --target https://your-app.com
```

### Тестирование API (OpenAPI / Swagger / Postman)

Укажите Strix на API-контракт, и он протестирует каждый объявленный конечную точку вместо того, чтобы иметь дело с их открытием путем обхода. Соедините спецификацию с живым базовым URL-адресом, чтобы агент знал, куда отправлять трафик:

```bash
# Файл OpenAPI / Swagger, экспорт Postman или живая коллекция по id
strix --target ./openapi.yaml --target https://api.your-app.com
strix --target postman://<collection-uuid> --target https://api.your-app.com
```


### Расширенные сценарии тестирования

```bash
# Проверка безопасности с аутентификацией
strix --target https://your-app.com --instruction "Выполните тестирование с аутентификацией, используя учетные данные: user:pass"

# Мультицелевое тестирование (исходный код + развернутое приложение)
strix -t https://github.com/org/app -t https://your-app.com

# Цели из файла, одна цель на непустую, не комментированную строку
strix --target-list ./targets.txt
```

См. [справочник по CLI](https://docs.strix.ai/usage/cli) для каждой опции, включая режимы сканирования, область разницы, файлы инструкций и бюджеты.

### Режим без интерактивного интерфейса

Запустите Strix программно без интерактивного интерфейса с помощью флага `-n/--non-interactive` - идеально для серверов и автоматизированных задач. CLI выводит находки уязвимостей в реальном времени и окончательный отчет перед выходом. Выходит с ненулевым кодом, когда уязвимости найдены.

```bash
strix -n --target https://your-app.com
```

### CI/CD (GitHub Actions)

Strix можно добавить в ваш конвейер для запуска теста безопасности на pull-запросах с легковесным рабочим процессом GitHub Actions:

```yaml
name: strix-penetration-test

on:
  pull_request:

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
        with:
          fetch-depth: 0

      - name: Установите Strix
        run: curl -sSL https://strix.ai/install | bash

      - name: Запустите Strix
        env:
          STRIX_LLM: ${{ secrets.STRIX_LLM }}
          LLM_API_KEY: ${{ secrets.LLM_API_KEY }}

        run: strix -n -t ./ --scan-mode quick
```

> [!TIP]
> В CI pull request запусках Strix автоматически ограничивает быстрые обзоры измененными файлами, поэтому вышеуказанный checkout загружает полную историю. См. [документацию по CI/CD](https://docs.strix.ai/integrations/github-actions) для подробностей.

### Конфигурация

```bash
export STRIX_LLM="openrouter/z-ai/glm-5.3"
export LLM_API_KEY="ваш-api-ключ"

# Необязательно
export LLM_API_BASE="ваш-api-base-url"  # если используется локальная модель, например, Ollama, LMStudio
```

> [!NOTE]
> Strix автоматически сохраняет вашу конфигурацию в `~/.strix/cli-config.json`, поэтому вам не нужно повторно вводить ее при каждом запуске.
> См. [справочник по конфигурации](https://docs.strix.ai/advanced/configuration) для каждой переменной окружения.

#### Вход с подпиской ChatGPT

Вместо оплачиваемого API-ключа вы можете запускать Strix на своей подписке ChatGPT Plus/Pro:

```bash
strix auth login chatgpt             # войдите в систему с вашей учетной записью ChatGPT
export STRIX_LLM="chatgpt/gpt-5.4"   # chatgpt/<model> работает на подписке
strix auth status                    # показать активный вход, или logout для забывания
```

#### Используйте управляемую платформу: `strix cloud`

Запускайте сканирования на [app.strix.ai](https://app.strix.ai) из терминала, без Docker или ключа LLM:

```bash
strix cloud login                                  # вход через браузер, одна учетная запись на установку
strix cloud scans start --source . --yes --wait    # сканирование локального кода, подтверждение загрузки
strix cloud scans start --engagement-type live_test --domain-ids <uuid> --wait
strix cloud vulns list --severity critical
```

Каждая операция [REST API](https://docs.app.strix.ai) имеет соответствующую команду `strix cloud <resource> <verb>`. Запустите `strix cloud`, чтобы перечислить ресурсы, и добавьте `help` к ресурсу, чтобы перечислить его глаголы. Вывод в формате JSON, когда stdout не является терминалом или когда вы передаете `--json`. Загрузки бинарных файлов являются исключением: перенаправьте сырые байты, или соедините `--output FILE --json` для метаданных загрузки.

См. [документацию по облачному CLI](https://docs.strix.ai/cloud/cli) для областей, рабочих пространств, выставления счетов и опций загрузки исходного кода.

#### Подключите свои собственные серверы MCP

Strix может подключаться к серверам Model Context Protocol (MCP), которые вы перечисляете и открываете, и предоставлять их инструменты агенту во время запуска. Создайте `~/.strix/mcp-servers.json` с JSON-списком локальных серверов `stdio` или удаленных серверов `http`:

```json
[
  {
    "name": "github",
    "transport": "http",
    "url": "https://api.githubcopilot.com/mcp/",
    "auth": { "kind": "bearer", "token": "your-token" },
    "allowed_tools": ["list_issues"]
  }
]
```

Инструменты каждого сервера пространства имен по `name`, например `github_list_issues`. См. [документацию по MCP](https://docs.strix.ai/integrations/mcp) для полной схемы, фильтрации инструментов и серверов `stdio`.

**Рекомендуемые модели для наилучших результатов:**

- [Z.ai GLM-5.3 на OpenRouter](https://openrouter.ai/z-ai/glm-5.3) - `openrouter/z-ai/glm-5.3` (стандартный выбор)
- [OpenAI GPT-5.4](https://openai.com/api/) - `openai/gpt-5.4`
- [Anthropic Claude Sonnet 4.6](https://claude.com/platform/api) - `anthropic/claude-sonnet-4-6`
- [Google Gemini 3 Pro Preview](https://cloud.google.com/vertex-ai) - `vertex_ai/gemini-3-pro-preview`
- [DeepSeek V4 Pro](https://platform.deepseek.com) - `deepseek/deepseek-v4-pro`
- [Moonshot Kimi K3](https://platform.kimi.ai) - `moonshot/kimi-k3`

См. [документацию по LLM-провайдерам](https://docs.strix.ai/llm-providers/overview) для всех поддерживаемых провайдеров, включая Vertex AI, Bedrock, Azure и локальные модели.

## Документация

Полная документация доступна на **[docs.strix.ai](https://docs.strix.ai)** - включая подробные руководства по использованию, интеграциям CI/CD, навыкам и расширенной конфигурации.

## Вклад в проект

Мы приветствуем вклад кода, документации и новых навыков - ознакомьтесь с нашим [Руководством по участию](https://docs.strix.ai/contributing) для начала работы или откройте [pull request](https://github.com/usestrix/strix/pulls)/[issue](https://github.com/usestrix/strix/issues).

## Присоединяйтесь к нашему сообществу

Есть вопросы? Нашли баг? Хотите внести вклад? **[Присоединяйтесь к нашему Discord!](https://discord.gg/strix-ai)**

## Поддержка проекта

**Нравится Strix?** Поставьте нам ⭐ на GitHub!

## Благодарности

Strix строится на основе замечательной работы открытых проектов, таких как [LiteLLM](https://github.com/BerriAI/litellm), [Caido](https://github.com/caido/caido), [Nuclei](https://github.com/projectdiscovery/nuclei), [Playwright](https://github.com/microsoft/playwright) и [Bubble Tea](https://github.com/charmbracelet/bubbletea). Огромное спасибо их разработчикам!


> [!WARNING]
> **Авторизованное использование только.** Strix активно тестирует цели, на которые вы указываете, поэтому запускайте его только на системах, которые вы владеете или на которые у вас есть **явное письменное разрешение** для тестирования, и оставайтесь в рамках согласованной области. Несанкционированное тестирование незаконно в большинстве юрисдикций.
> Вы несете единственную ответственность за получение разрешения и соблюдение закона. Strix предоставляется "как есть" без гарантии или ответственности за неправомерное использование.

</div>