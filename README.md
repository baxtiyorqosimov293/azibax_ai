# AziBax AI Bot 🤖

Telegram-бот для генерации AI-фото с системой оплаты через Telegram Stars.

## Что исправлено 🛠️

1. **Безопасность** - добавлена защита от повторного использования промокодов
2. **База данных** - добавлена таблица для отслеживания использованных кодов
3. **Премиум статус** - исправлена проверка срока действия премиума
4. **Обработка ошибок** - добавлены таймауты и обработка ошибок API
5. **Мобильная версия** - улучшен интерфейс для iPhone
6. **Webhook** - добавлена поддержка webhook для облачного хостинга
7. **Rate limiting** - исправлены лимиты запросов
8. **Валидация** - добавлена валидация входных данных

## Быстрый старт 🚀

### 1. Создай бота в Telegram

1. Открой [@BotFather](https://t.me/BotFather)
2. Отправь `/newbot`
3. Укажи название и username бота
4. **Скопируй токен** (понадобится позже)
5. Отправь `/setinline` и включи inline mode
6. Отправь `/setinlinefeedback` и выбери 100%

### 2. Получи API ключи

**OpenAI (рекомендуется):**
1. Перейди на [platform.openai.com](https://platform.openai.com)
2. Создай аккаунт
3. Перейди в API Keys → Create new secret key
4. **Скопируй ключ**

**Stability AI (альтернатива):**
1. Перейди на [platform.stability.ai](https://platform.stability.ai)
2. Создай аккаунт
3. Получи API ключ

### 3. Разверни на Render (бесплатно)

**Через веб-интерфейс:**

1. Зарегистрируйся на [render.com](https://render.com) (через GitHub)
2. Нажми "New +" → "Web Service"
3. Подключи GitHub репозиторий или загрузи файлы
4. Укажи настройки:
   - **Runtime:** Python 3
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn bot:app --bind 0.0.0.0:$PORT --workers 1 --timeout 120`
5. Нажми "Advanced" и добавь переменные окружения:
   - `TELEGRAM_BOT_TOKEN` - токен от BotFather
   - `TELEGRAM_ADMIN_ID` - твой Telegram ID (узнать у [@userinfobot](https://t.me/userinfobot))
   - `ADMIN_KEY` - любой сложный пароль для админки
   - `SECRET_KEY` - любой случайный набор символов
   - `OPENAI_API_KEY` - ключ от OpenAI
   - `WEBSITE_URL` - URL который даст Render (например: `https://azibax-ai.onrender.com`)
   - `WEBHOOK_URL` - тот же URL
6. Нажми "Create Web Service"

**Через Render Blueprint (быстрее):**

1. Загрузи файлы на GitHub
2. В Render нажми "New +" → "Blueprint"
3. Подключи репозиторий
4. Заполни переменные окружения
5. Нажми "Apply"

### 4. Настрой webhook

После деплоя webhook установится автоматически, если указан `WEBHOOK_URL`.

Проверь работу:
1. Открой URL сайта в браузере
2. Открой бота в Telegram
3. Отправь `/start`

## Структура проекта 📁

```
azibax_bot/
├── bot.py              # Основной файл бота
├── requirements.txt    # Зависимости
├── Procfile           # Для Render/Heroku
├── render.yaml        # Blueprint для Render
├── .env.example       # Пример переменных окружения
└── README.md          # Этот файл
```

## Переменные окружения 🔐

| Переменная | Описание | Обязательная |
|------------|----------|--------------|
| `TELEGRAM_BOT_TOKEN` | Токен бота от @BotFather | ✅ |
| `TELEGRAM_ADMIN_ID` | Твой Telegram ID | ✅ |
| `ADMIN_KEY` | Пароль для админки | ✅ |
| `SECRET_KEY` | Секретный ключ Flask | ✅ |
| `OPENAI_API_KEY` | Ключ OpenAI | ⚠️ (или Stability) |
| `STABILITY_API_KEY` | Ключ Stability AI | ⚠️ (или OpenAI) |
| `WEBSITE_URL` | URL веб-приложения | ⚠️ |
| `WEBHOOK_URL` | URL для webhook | ⚠️ |
| `PORT` | Порт (Render задаёт автоматически) | ❌ |

## Админ-команды 👑

В Telegram боте:
- `/stats` - статистика продаж (только для админа)

Веб-API:
```bash
curl -H "X-Admin-Key: ваш_ключ" https://your-app.com/api/admin/stats
```

## Тарифы 💰

| Тариф | Звёзды | Что получаешь |
|-------|--------|---------------|
| 🚀 Старт | 100⭐ | 20 генераций |
| 💎 Стандарт | 300⭐ | 50 генераций (экономия 25%) |
| 👑 Премиум | 500⭐ | 30 дней безлимита |

## Стоимость генераций ⭐

| Тип | Стоимость |
|-----|-----------|
| Обычное фото | 5⭐ |
| HD фото | 10⭐ |
| Стилизация | 5⭐ |

## Устранение неполадок 🐛

**Бот не отвечает:**
- Проверь `TELEGRAM_BOT_TOKEN`
- Проверь логи в Render Dashboard
- Убедись что webhook установлен

**Ошибка генерации:**
- Проверь `OPENAI_API_KEY` или `STABILITY_API_KEY`
- Проверь баланс API
- Попробуй сменить провайдера

**База данных:**
- SQLite создаётся автоматически
- Данные сохраняются между перезапусками

## Лицензия 📄

MIT License - используй как хочешь!

## Поддержка 💬

Если есть вопросы - пиши в Telegram!
