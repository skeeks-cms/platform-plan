# План платформы SkeekS

Глобальный план [платформы SkeekS](https://skeeks-platform.ru/): что и зачем
строим, в каком порядке, что уже сделано и какие решения принял владелец.
Это не Composer-пакет и не код: здесь нет `composer.json`, репозиторий никто
не устанавливает.

- Общая доска направлений и этапов — [ROADMAP.md](ROADMAP.md).
- План CRM — [crm/](crm/README.md).
- Решения владельца по датам — [decisions/](decisions/README.md).

## Три места знаний и граница между ними

| Где | Что там | Чего там нет |
|---|---|---|
| **Этот репозиторий** | Замысел, этапы, статусы, решения владельца с датами, итоги выпусков, открытые вопросы, ссылки на пакеты и на файлы умения | Описания устройства кода, повтор договоров умения |
| **Умение [`skeeks-cms-package-development`](https://github.com/skeeks-cms/skeeks-cms-package-development)** | Как писать код пакетов: только договоры, проверенные исходниками (`SKILL.md` и `references/`) | Планы, догадки, разовое поведение проекта |
| **Документы пакетов** (`README.md`, `AGENTS.md`, `ARCHITECTURE.md`) | Устройство собственного кода пакета | Планы других пакетов и платформы в целом |

Правила ведения плана:

1. Один договор — в одном месте. Как только решение реализовано и договор
   проверен по исходникам, он записывается в умение, а план заменяет свой
   текст ссылкой на файл умения.
2. Решение владельца записывается с датой: в файле направления — полностью,
   в [decisions/](decisions/README.md) — одной строкой со ссылкой. Отменённое
   решение не удаляется: рядом пишется, чем и когда заменено.
3. После каждого заметного шага обновляется состояние работ направления
   (например [crm/status.md](crm/status.md)) и общая доска.
4. Исполняемый код — окончательный источник истины. Если план расходится с
   кодом, план исправляется или помечается как план.
5. Репозиторий публичный. В нём нет секретов, токенов, паролей, адресов
   серверов и внутренних IP, логинов, телефонов, email, имён клиентов и
   сотрудников, содержимого рабочих конфигураций. Клиенты и сотрудники
   называются обобщённо («компания клиента», «сотрудник отдела продаж»),
   владелец — «владелец».
6. Каталог направления создаётся, когда у направления появляется план; до
   этого направление упоминается только в [ROADMAP.md](ROADMAP.md).

## Карта платформы

Пакеты лежат на GitHub в организации [skeeks-cms](https://github.com/skeeks-cms),
выпускаются через Packagist.

**Ядро и оболочка**

| Пакет | За что отвечает |
|---|---|
| [`cms`](https://github.com/skeeks-cms/cms) | Ядро: сайты, пользователи, разделы, хранилище; CRM — компании, клиенты, сделки (`CmsLead`), услуги (`CmsDeal`), задачи, доступы (`CrmAccess`, `dealAccess`), воронки, уведомления; точки расширения для остальных пакетов |
| [`cms-backend`](https://github.com/skeeks-cms/cms-backend) | Общая оболочка кабинетов: `BackendComponent`, `BackendController`, сетки, формы, иконки |
| [`cms-backend-admin`](https://github.com/skeeks-cms/cms-backend-admin) | Кабинет администратора поверх общей оболочки |
| [`cms-job`](https://github.com/skeeks-cms/cms-job) | Фоновые задачи и очереди |
| [`cms-agent`](https://github.com/skeeks-cms/cms-agent) | Расписание (агенты) |
| [`cms-theme-unify-v2`](https://github.com/skeeks-cms/cms-theme-unify-v2) | Тема сайтов |

**Коммуникации с клиентом**

| Пакет | За что отвечает |
|---|---|
| [`cms-communication`](https://github.com/skeeks-cms/cms-communication) | Ящики и подключения, «Почта», «Чаты», рассылки, согласия и отписка, «Отправить клиенту», уведомления наружу, MCP-инструменты коммуникаций |
| [`cms-communication-imap`](https://github.com/skeeks-cms/cms-communication-imap) | Драйвер почты (IMAP, SMTP) |
| [`cms-communication-telegram`](https://github.com/skeeks-cms/cms-communication-telegram) | Драйвер Telegram |
| [`cms-communication-max`](https://github.com/skeeks-cms/cms-communication-max) | Драйвер MAX |
| [`cms-communication-unisender`](https://github.com/skeeks-cms/cms-communication-unisender) | Драйвер сервиса рассылок Unisender Go |
| [`cms-proposal`](https://github.com/skeeks-cms/cms-proposal) | Предложения: КП и Презентации, страница по личной ссылке |
| [`cms-mcp`](https://github.com/skeeks-cms/cms-mcp) | REST/MCP-инструменты для внешних клиентов и ИИ |
| [`cms-oauth2-server`](https://github.com/skeeks-cms/cms-oauth2-server) | OAuth-вход внешних клиентов |
| [`cms-mailer`](https://github.com/skeeks-cms/cms-mailer) | Системная почта сайта |
| [`cms-mobile`](https://github.com/skeeks-cms/cms-mobile) | Мобильное приложение, push |
| `cms-ai` (план) | Языковые модели, уровни самостоятельности, журнал решений ИИ |

**Магазин, услуги, формы**

| Пакет | За что отвечает |
|---|---|
| [`cms-shop`](https://github.com/skeeks-cms/cms-shop) | Магазин: заказы (`ShopOrder`), счета, платежи, документы; общая финансовая часть для заказов и услуг |
| `cms-hosting` (закрытый репозиторий) | Хостинг: сайты, VPS, DNS, SSL как ресурсы услуг |
| [`cms-module-form2`](https://github.com/skeeks-cms/cms-module-form2) | Формы сайта, заявки в CRM |
| [`cms-seo`](https://github.com/skeeks-cms/cms-seo) | SEO сайта |

Полный список пакетов — в организации [skeeks-cms](https://github.com/skeeks-cms).
