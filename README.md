<div align="center">

# 🤖 AI Generator Bot

**Telegram-бот для генерации изображений и видео с помощью нейросетей**

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Aiogram](https://img.shields.io/badge/Aiogram-3.x-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://aiogram.dev)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0-D71F00?style=for-the-badge&logo=sqlalchemy&logoColor=white)](https://sqlalchemy.org)

<br>

<img src="https://img.shields.io/badge/🖼_Генерация_фото-4_модели-blueviolet?style=flat-square" />
<img src="https://img.shields.io/badge/🎬_Генерация_видео-4_модели-blueviolet?style=flat-square" />
<img src="https://img.shields.io/badge/🎨_Вариации-изображений-blueviolet?style=flat-square" />
<img src="https://img.shields.io/badge/🛡_Админ--бот-логи_и_статистика-blueviolet?style=flat-square" />

</div>

<br>

> **📖 Подробное описание работы двух ботов** — см. [`HOW_IT_WORKS.md`](HOW_IT_WORKS.md)

---

## 📋 Возможности

<table>
<tr>
<td width="50%">

### 🤖 Основной бот

| | Функция | Описание |
|---|---------|----------|
| 🖼 | **Генерация фото** | 4 модели нейросетей |
| 🎬 | **Генерация видео** | 4 модели нейросетей |
| 🎨 | **Вариации** | Фото → похожее изображение |
| 🌐 | **Авто-перевод** | Промпты RU → EN |

</td>
<td width="50%">

### 🛡 Админ-бот

| | Функция | Описание |
|---|---------|----------|
| 👤 | **Уведомления** | Новые пользователи |
| 🚨 | **Логи ошибок** | Мгновенные алерты |
| 📊 | **`/stats`** | Статистика бота |
| 📋 | **`/users`** | Последние юзеры |

</td>
</tr>
</table>

---

## 🔌 Поддерживаемые нейросети

<table>
<tr>
<td width="50%">

### 🖼 Генерация изображений

| Модель | Провайдер | Статус |
|:-------|:----------|:------:|
| FLUX.1 Schnell | HuggingFace | ✅ Free |
| FLUX.1 Schnell | fal.ai | 🔒 |
| Stable Image Core | Stability AI | 🔒 |
| DALL-E 3 | OpenAI | 🔒 |

</td>
<td width="50%">

### 🎬 Генерация видео

| Модель | Провайдер | Статус |
|:-------|:----------|:------:|
| Hailuo MiniMax | fal.ai | 🔒 |
| Kling 2.6 | fal.ai | 🔒 |
| Hunyuan Video | fal.ai | 🔒 |
| Wan 2.1 | Replicate | 🔒 |

</td>
</tr>
</table>

> ✅ — подключена и работает бесплатно &nbsp; | &nbsp; 🔒 — готова к подключению (нужен API-ключ в `.env`)

---

## 🚀 Быстрый старт

### 1️⃣ Клонирование

```bash
git clone https://github.com/your-username/tg_bot.git
cd tg_bot
```

### 2️⃣ Настройка окружения

```bash
cp .env.example .env
```

Заполни **4 обязательных** поля в `.env`:

```env
MAIN_BOT_TOKEN=...       # @BotFather → /newbot
ADMIN_BOT_TOKEN=...      # @BotFather → /newbot (второй бот)
ADMIN_CHAT_ID=...        # Твой Telegram ID (@userinfobot → /start)
HF_API_KEY=...           # huggingface.co → Settings → Access Tokens
```

<details>
<summary>📌 <b>Где получить каждый токен</b></summary>

<br>

| Параметр | Где получить |
|----------|-------------|
| `MAIN_BOT_TOKEN` | Telegram → **@BotFather** → `/newbot` → скопировать токен |
| `ADMIN_BOT_TOKEN` | Telegram → **@BotFather** → `/newbot` (создать второго бота) |
| `ADMIN_CHAT_ID` | Telegram → **@userinfobot** → `/start` → скопировать `Id` |
| `HF_API_KEY` | [huggingface.co](https://huggingface.co) → Sign Up → Settings → Access Tokens → New token (Read) |

</details>

### 3️⃣ Запуск

```bash
docker compose up --build -d
```

### 4️⃣ Проверка

```bash
docker compose logs -f
```

Должно появиться:
```
bot-1  | INFO: Starting both bots...
bot-1  | INFO: Run polling for bot @your_main_bot
bot-1  | INFO: Run polling for bot @your_admin_bot
```

---

## 💬 Использование

<table>
<tr>
<td width="50%">

### 🤖 Основной бот

```
1. /start
2. Нажми [🖼 Фото]
3. Выбери модель
4. Напиши промпт на любом языке
5. Получи результат!
```

</td>
<td width="50%">

### 🛡 Админ-бот

```
/start  — информация
/stats  — статистика
/users  — последние юзеры

+ автоматические уведомления
  о новых юзерах и ошибках
```

</td>
</tr>
</table>

---

## 🏗 Архитектура

```
tg_bot/
│
├── bot.py                        # 🚀 Entry point — запуск 2 ботов
├── config.py                     # ⚙️  Pydantic Settings (.env)
├── Dockerfile                    # 🐳 Docker-образ
├── docker-compose.yml            # 🐳 Docker Compose
│
├── common/                       # 📦 Общие модули
│   ├── database/
│   │   ├── models.py             #    User, Generation (SQLAlchemy 2.0)
│   │   └── engine.py             #    Async engine + session
│   └── services/
│       ├── image_gen.py          #    4 провайдера изображений
│       └── video_gen.py          #    4 провайдера видео
│
├── main_bot/                     # 🤖 Основной бот
│   ├── factory.py                #    Сборка Dispatcher
│   ├── handlers/
│   │   ├── start.py              #    /start, /help, /cancel
│   │   ├── generate.py           #    FSM-workflow генерации
│   │   └── variation.py           #    Вариации изображений
│   ├── keyboards/
│   │   └── inline.py             #    Inline-клавиатуры
│   ├── middlewares/
│   │   ├── db_session.py         #    Инъекция DB-сессии
│   │   ├── user_tracking.py      #    Регистрация юзеров
│   │   └── error_logging.py      #    Логирование ошибок
│   └── states/
│       └── generation.py         #    FSM-состояния
│
└── admin_bot/                    # 🛡 Админ-бот
    ├── factory.py                #    Сборка Dispatcher
    └── handlers/
        └── stats.py              #    /stats, /users
```

---

## 🛠 Tech Stack

<div align="center">

| Технология | Версия | Назначение |
|:----------:|:------:|:-----------|
| <img src="https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white" /> | 3.12 | Основной язык |
| <img src="https://img.shields.io/badge/-Aiogram-26A5E4?logo=telegram&logoColor=white" /> | 3.x | Telegram Bot API (async) |
| <img src="https://img.shields.io/badge/-SQLAlchemy-D71F00?logo=sqlalchemy&logoColor=white" /> | 2.0 | ORM (async) |
| <img src="https://img.shields.io/badge/-SQLite-003B57?logo=sqlite&logoColor=white" /> | 3 | База данных |
| <img src="https://img.shields.io/badge/-aiohttp-2C5BB4?logo=aiohttp&logoColor=white" /> | 3.10 | HTTP-клиент для AI API |
| <img src="https://img.shields.io/badge/-Pydantic-E92063?logo=pydantic&logoColor=white" /> | 2.x | Конфигурация из .env |
| <img src="https://img.shields.io/badge/-Docker-2496ED?logo=docker&logoColor=white" /> | — | Контейнеризация |

</div>

---

## 📐 Ключевые решения

| Решение | Описание |
|---------|----------|
| **Два бота — один процесс** | `asyncio.gather` для параллельного polling обоих ботов |
| **FSM (Finite State Machine)** | Пошаговый workflow генерации через aiogram FSM |
| **Middleware-цепочка** | DB-сессия → трекинг юзеров → логирование ошибок |
| **Авто-перевод промптов** | RU → EN через HuggingFace Translation API (бесплатно) |
| **Модульная архитектура** | Каждый AI-провайдер = отдельный класс, легко добавить новый |
| **Docker-ready** | Один `docker compose up` и всё работает |

---

<div align="center">

</div>
