# 🎮 V-Cord — Discord Clone

> Полнофункциональный клон Discord с чатом в реальном времени, серверами, каналами, личными сообщениями и системой друзей.  
> Проект построен на Django и Django Channels с поддержкой WebSocket.

[![Python Version](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/)
[![Django Version](https://img.shields.io/badge/django-4.2-green.svg)](https://www.djangoproject.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![GitHub issues](https://img.shields.io/github/issues/NIOJJN/v-cord)](https://github.com/NIOJJN/v-cord/issues)
[![GitHub stars](https://img.shields.io/github/stars/NIOJJN/v-cord)](https://github.com/NIOJJN/v-cord/stargazers)

---

## 📸 Скриншоты

> Скриншоты будут добавлены позже

---

## ✨ Возможности

### 🔐 Пользователи и безопасность
- Регистрация и авторизация с валидацией
- Профили с аватарами, статусами и никнеймами
- Система друзей: запросы, принятие, отклонение, удаление из друзей
- Хеширование паролей (PBKDF2)

### 💬 Общение в реальном времени
- Чат в реальном времени через **WebSocket (Django Channels)**
- Личные сообщения между пользователями (Direct Messages)
- Уведомления при упоминаниях `@username`
- Закрепление сообщений (пины)
- Редактирование и удаление сообщений
- Отправка изображений в чат (с сохранением в БД)

### 🏠 Серверы и каналы
- Создание серверов с возможностью загрузки иконки
- Категории для группировки каналов
- Текстовые и голосовые каналы
- Роли на сервере: владелец, администратор, участник
- Приглашения по уникальному коду
- Голосовые каналы с WebRTC (в разработке)

### 🎨 Интерфейс и UX
- Полноценная тёмная тема в стиле Discord
- Адаптивный дизайн для любых устройств
- Интуитивная навигация по серверам и каналам
- Drag & Drop для загрузки изображений
- Контекстное меню по правому клику на сообщения
- Индикация набора текста (в планах)

### ⚡ Производительность и безопасность
- Поддержка **ASGI** через Daphne
- Кэширование статики через **WhiteNoise**
- Поддержка **Redis** как бэкенда для Channels
- Защита от CSRF, XSS и SQL-инъекций
- Переменные окружения для секретных ключей

---

## 🛠 Технологический стек

| Компонент | Технология | Назначение |
|-----------|------------|------------|
| **Backend** | Django 4.2 | Основной веб-фреймворк |
| **Real-time** | Django Channels + WebSocket | Чат в реальном времени |
| **ASGI Server** | Daphne | Production-сервер для WebSocket |
| **Брокер** | Redis | Бэкенд для каналов Channels |
| **База данных** | SQLite / PostgreSQL | Хранение данных |
| **Статика** | WhiteNoise | Раздача статических файлов |
| **Фронтенд** | Bootstrap 5 + CSS | Интерфейс и адаптивность |
| **Иконки** | Font Awesome 6 | Векторные иконки |
| **Голос** | WebRTC (в разработке) | Голосовые каналы |

---

## 🚀 Быстрый старт

### 📋 Требования

- Python 3.11+
- Redis Server (для WebSocket)
- Git
- pip и venv

---

### 📦 Установка и запуск

```bash
# 1️⃣ Клонируйте репозиторий
git clone https://github.com/NIOJJN/v-cord.git
cd v-cord

# 2️⃣ Создайте и активируйте виртуальное окружение
python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate

# 3️⃣ Установите зависимости
pip install -r requirements.txt

# 4️⃣ Настройте переменные окружения
# Скопируйте пример и отредактируйте .env
cp .env.example .env
# Укажите SECRET_KEY, DEBUG, DATABASE_URL и другие параметры

# 5️⃣ Выполните миграции базы данных
python manage.py migrate

# 6️⃣ Создайте суперпользователя (администратора)
python manage.py createsuperuser

# 7️⃣ Соберите статику
python manage.py collectstatic

# 8️⃣ Запустите Redis (в отдельном терминале)
redis-server

# 9️⃣ Запустите сервер разработки через Daphne
daphne -b 0.0.0.0 -p 8000 discord_clone.asgi:application