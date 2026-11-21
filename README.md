# mcp-1c — MCP-сервер для 1С:Предприятия

[Русский](#русский) · [English](#english) · [rcs.kz/product/mcp-1c](https://rcs.kz/product/mcp-1c) · [Релизы](https://github.com/RCS-kz/mcp-1c/releases)

## Русский

**Что это.** mcp-1c даёт Claude и другим MCP-клиентам доступ к вашей базе 1С: ИИ выполняет запросы, смотрит структуру объектов, а по вашей команде создаёт и проводит документы.

### Установка в 3 шага

1. В базу 1С загрузите расширение `MCPService.cfe` (0.6.2, [релиз v0.2.1](https://github.com/RCS-kz/mcp-1c/releases/tag/v0.2.1)) и опубликуйте его HTTP-сервис (IIS или Apache).
2. Поставьте сервер: `npm install -g https://github.com/RCS-kz/mcp-1c/releases/download/v0.2.1/rcs-kz-mcp-1c-0.2.1.tgz`
   Для Claude Desktop — пакет [`mcp-1c-0.2.1.mcpb`](https://github.com/RCS-kz/mcp-1c/releases/download/v0.2.1/mcp-1c-0.2.1.mcpb): открыть файл, указать адрес базы, пользователя и ключ.
3. Подключите к клиенту (ниже) и задайте адрес базы, пользователя 1С и ключ лицензии.

Нужны Node.js и Python 3.10–3.13. Платформы: Windows x64, Linux x86_64, macOS 11+ (Apple Silicon и Intel). Linux ARM64 не поддерживается.
Ключ на пробный период выдаём по заявке на [rcs.kz/product/mcp-1c](https://rcs.kz/product/mcp-1c).

**Claude Desktop** — `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "1c": {
      "command": "mcp-1c",
      "env": {
        "MCP_1C_BASE": "https://ваш-сервер/имя-базы/hs/mcp",
        "MCP_1C_USER": "ИИ",
        "MCP_1C_PASSWORD": "…",
        "RCS_LICENSE_KEY": "v1.…",
        "MCP_1C_READ_ONLY": "0"
      }
    }
  }
}
```
**Claude Code**: `claude mcp add 1c -e MCP_1C_BASE=https://ваш-сервер/имя-базы/hs/mcp -e MCP_1C_USER=ИИ -e MCP_1C_PASSWORD=… -e RCS_LICENSE_KEY=v1.… -- mcp-1c`
**Cursor**: тот же блок `mcpServers` в `~/.cursor/mcp.json`.

Для серверной установки за шлюзом ИИ (LiteLLM и др.) есть HTTP-режим: `mcp-1c --http 127.0.0.1:8080` (streamable HTTP, `POST /mcp`).

### Что можно поручить

| Кто | Запрос | Что делает ИИ |
|---|---|---|
| Директор | «Кто нам должен больше 30 дней? Разбей по менеджерам» | запрос к регистрам расчётов (`execute_query`) |
| Бухгалтер | «Сколько денег в кассе и на счетах на конец месяца, по валютам» | запрос к остаткам |
| Бухгалтер | «Создай реализацию по заказу покупателя № … и проведи» | пишет документ (`write_object`), проводит (`post_document`) — после вашего «да» |
| Бухгалтер | «Почему не проводится документ?» | видит сообщения 1С, например «Поле "Юр. / физ. лицо" не заполнено» (MCPService 0.6.1) |
| Аналитик | «Покажи реквизиты и табличные части документа "Поступление товаров"» | структура объекта (`get_metadata`) |
| Программист 1С | «Напиши запрос остатков по складам с учётом наших реквизитов» | смотрит реальные метаданные базы и проверяет запрос на ней |

Инструменты (7): `ping`, `execute_query`, `get_metadata`, `get_object` — чтение; `execute_code`, `write_object`, `post_document` — запись.

### Безопасность и права

- **Два режима, оба без админ-прав 1С.** Роль расширения `MCP_ИИПолныйДоступ` (чтение + запись и проведение) или `MCP_ИИТолькоЧтение`, плюс обычный профиль доступа («Главный бухгалтер» / «Только просмотр»). «Полные права» пользователю ИИ не нужны.
- **Только чтение — двумя замками:** права 1С и флаг `MCP_1C_READ_ONLY=1` (инструменты записи скрыты и отклоняются без обращения к 1С).
- **Код ИИ — в безопасном режиме.** У пользователя без права «Администрирование» `/execute` выполняется в безопасном режиме: нельзя трогать расширения, пользователей ИБ, файлы и сеть.
- **Личный вход через Kerberos** (`MCP_1C_AUTH=kerberos`, с 0.2.0): каждый запрос идёт в 1С от имени того сотрудника, который спросил, с его правами и его именем в журнале регистрации. Пароли не хранятся.
- Сервер работает у вас; логин и пароль 1С лежат в настройках на вашей машине. Данные, которые прочитал ИИ, уходят в выбранную вами модель — учитывайте это для персональных данных.
- Первое подключение — к копии базы.

### Проверено на

1С:Бухгалтерия для Казахстана 3.0, 1С:Бухгалтерия 3.0 (РФ), 1С:УНФ — в работе. Другие конфигурации — если в них можно поставить расширение. Файловые базы 8.3 — через публикацию на IIS/Apache.

### Чем отличаемся (честно)

| | **mcp-1c (RCS)** | [vladimir-kharin/1c_mcp](https://github.com/vladimir-kharin/1c_mcp) | [feenlace/mcp-1c](https://github.com/feenlace/mcp-1c) |
|---|---|---|---|
| Суть | готовый сервер: данные базы — чтение и запись | конструктор: свои MCP-инструменты пишутся в расширении 1С | помощник разработчика: метаданные, поиск по коду, справка BSL |
| Запись и проведение документов | да, по команде пользователя | если напишете такой инструмент сами | нет (в открытой версии запросы только SELECT) |
| Режим «только чтение» без админ-прав | две роли + флаг сервера | на ваше усмотрение | — |
| Вход сотрудника под своей учёткой | Kerberos (0.2.0) | — | — |
| Инструменты для программиста | нет (поиска по коду и справки BSL у нас нет) | метаданные конфигурации, обезличивание данных | 19 инструментов: код, журнал регистрации, справка BSL |
| Установка расширения | вручную через Конфигуратор | вручную | автоустановка `mcp-1c --install` |
| Исходный код | закрытый (Cython), расширение — в релизе | открытый, MIT | открытый, MIT |
| Цена | от 14 900 ₸/мес, бесплатного тарифа нет | бесплатно | бесплатно; платные 1 990 и 4 990 ₽/мес |

Кому что: своя логика в 1С и есть программист — 1c_mcp; разработка и разбор конфигурации — feenlace/mcp-1c (хорошо работает вместе с нашим); бухгалтеру и директору, которым нужна запись документов с контролем прав и поддержка, — mcp-1c.

### Цены

| Тариф | Казахстан, с НДС 16 % | РФ, по инвойсу | Что входит |
|---|---|---|---|
| **Pro** | 14 900 ₸/мес | 4 900 ₽/мес | чтение + запись с подтверждением, 1 база, без лимита вызовов |
| **Team** | 44 900 ₸/мес | 14 900 ₽/мес | до 5 баз; сверх 5 — +7 900 ₸ за базу |

Бесплатного тарифа нет, пробный период — по заявке. Лицензия — ключ на базу. Для юрлица РФ покупатель — налоговый агент по НДС 22 %. Источник цен — [rcs.kz/product/mcp-1c](https://rcs.kz/product/mcp-1c).

### Вместе с другими нашими MCP
- [bitrix24-mcp](https://github.com/RCS-kz/bitrix24-mcp) — Битрикс24: CRM, задачи, открытые линии, звонки.
- [rcs-ads-mcp](https://rcs.kz/product/rcs-ads-mcp) — Яндекс Директ, VK Реклама, Roistat.

### Поддержка
go@rcs.kz · [заявка на rcs.kz](https://rcs.kz/product/mcp-1c) · [issues](https://github.com/RCS-kz/mcp-1c/issues).
RCS (ИП КВАНТ, Астана) — партнёр фирмы «1С» в Казахстане с 2009 года.

---

## English

**What it is.** mcp-1c gives Claude and other MCP clients access to your 1C:Enterprise database: the AI runs queries, reads object metadata and, on your command, creates and posts documents.

### Install in 3 steps

1. Load the `MCPService.cfe` extension (0.6.2, [release v0.2.1](https://github.com/RCS-kz/mcp-1c/releases/tag/v0.2.1)) into your 1C database and publish its HTTP service (IIS or Apache).
2. Install the server: `npm install -g https://github.com/RCS-kz/mcp-1c/releases/download/v0.2.1/rcs-kz-mcp-1c-0.2.1.tgz`
   Claude Desktop: open [`mcp-1c-0.2.1.mcpb`](https://github.com/RCS-kz/mcp-1c/releases/download/v0.2.1/mcp-1c-0.2.1.mcpb) and enter the database URL, user and license key.
3. Add it to your client (see above) with the base URL, the 1C user and your license key.

Requires Node.js and Python 3.10–3.13. Platforms: Windows x64, Linux x86_64, macOS 11+ (Apple Silicon and Intel). Linux ARM64 is not supported. Trial key on request at [rcs.kz/product/mcp-1c](https://rcs.kz/product/mcp-1c).

Config: the Claude Desktop JSON above works as is. Claude Code [verify]: `claude mcp add 1c -e MCP_1C_BASE=… -e MCP_1C_USER=… -e MCP_1C_PASSWORD=… -e RCS_LICENSE_KEY=… -- mcp-1c`. Cursor [verify]: same `mcpServers` block in `~/.cursor/mcp.json`. For AI gateways (LiteLLM etc.): `mcp-1c --http 127.0.0.1:8080` (streamable HTTP, `POST /mcp`).

### What you can ask

- "Who owes us for more than 30 days? Break it down by sales manager."
- "Cash and bank balances at month end, by currency."
- "Create a sales invoice from customer order #… and post it." — writes only after you confirm.
- "Why won't this document post?" — the AI sees 1C's own messages (MCPService 0.6.1).
- "Show the attributes and tabular sections of the Goods Receipt document."

Tools (7): `ping`, `execute_query`, `get_metadata`, `get_object` (read); `execute_code`, `write_object`, `post_document` (write).

### Security

- Two modes, neither needs 1C admin rights: extension role `MCP_ИИПолныйДоступ` (read + write/post) or `MCP_ИИТолькоЧтение`, plus a regular access profile.
- Read-only is enforced twice: by 1C rights and by the `MCP_1C_READ_ONLY=1` server flag.
- AI code runs in 1C safe mode for any user without the Administration right (no extensions, infobase users, files or network).
- Per-employee Kerberos login (`MCP_1C_AUTH=kerberos`, since 0.2.0): each request runs as the employee who asked, with their rights and their name in the event log; no passwords stored.
- The server runs on your side; 1C credentials stay in your local config.

Tested in daily use on 1C:Accounting for Kazakhstan 3.0, 1C:Accounting 3.0 (Russia) and 1C:UNF.

### How it compares

- **vladimir-kharin/1c_mcp** (open source, MIT) — a framework for writing your own MCP tools inside a 1C extension. Best if you have a 1C developer and want custom logic.
- **feenlace/mcp-1c** (open source, MIT; paid editions) — developer-oriented: 19 tools for metadata, code search, BSL help, event log; read-only queries. Best for development; works well alongside ours.
- **mcp-1c by RCS** (commercial, closed source) — ready-made data access with write and posting, read-only mode without admin rights, Kerberos SSO, support. No code-search or BSL-help tools.

### Pricing

Pro — 14 900 KZT/month incl. 16% VAT (4 900 RUB by invoice), 1 database. Team — 44 900 KZT/month (14 900 RUB), up to 5 databases, +7 900 KZT per extra database. No free tier; trial on request. Details: [rcs.kz/product/mcp-1c](https://rcs.kz/product/mcp-1c).

Support: go@rcs.kz. RCS (IP KVANT, Astana, Kazakhstan) — 1C partner since 2009.
