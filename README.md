# Kittygram Backend


![GitHub Workflow Status](https://github.com/anatoliyfs/kittygram_final/actions/workflows/main.yml/badge.svg)


## Описание проекта

**Kittygram** — это backend‑часть веб‑приложения для обмена фотографиями кошек. Проект позволяет пользователям:
- загружать фотографии своих питомцев;
- просматривать галерею изображений других пользователей;
- взаимодействовать с контентом через API.

**Цель проекта** — демонстрация работы REST‑API на Django с аутентификацией, обработкой медиафайлов и интеграцией с PostgreSQL.

## Функциональные возможности

- **Аутентификация пользователей** (через Djoser и токены);
- **Загрузка и хранение медиафайлов** (фото кошек);
- **API для CRUD‑операций** с кошачьими профилями;
- **Пагинация** списка изображений;
- **Валидация паролей** по стандартным правилам Django;
- **Поддержка CORS** для взаимодействия с фронтендом.


## Технологический стек

- **Backend**: Django;
- **API**: Django REST Framework;
- **Аутентификация**: Djoser;
- **База данных**: PostgreSQL (с возможностью переключения на SQLite для разработки);
- **Сервер**: Nginx + Gunicorn;
- **Конфигурация**: python‑dotenv;
- **CI/CD**: GitHub Actions;
- **Версионирование**: Git.


## Как развернуть проект

### 1. Клонирование репозитория
```bash
git clone https://github.com/Port-tf/kittygram-backend.git
cd kittygram-backend
```

### 2. Создание виртуального окружения
```bash
python -m venv venv
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate     # Windows
```

### 3. Установка зависимостей
```bash
pip install -r requirements.txt
```

### 4. Настройка переменных окружения
Создайте файл `.env` в корне проекта (пример ниже).


### 5. Миграция базы данных
```bash
python manage.py migrate
```

### 6. Сбор статических файлов
```bash
python manage.py collectstatic
```

### 7. Запуск сервера
```bash
python manage.py runserver
```
Или через Gunicorn (для продакшена):
```bash
gunicorn kittygram_backend.wsgi:application
```

## Настройка файла `.env`

Создайте файл `.env` в корне проекта и заполните по шаблону:

```env
# Обязательные параметры
SECRET_KEY=ваш_уникальный_ключ_здесь
DEBUG=False
ALLOWED_HOSTS=localhost,127.0.0.1,ваш-домен.ru


# Для PostgreSQL (продакшен)
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=надёжный_пароль
DB_HOST=localhost
DB_NAME=kittygram
DB_PORT=5432


# Для SQLite (разработка)
USE_SQLITE=true  # Установите true для SQLite
```

**Как получить `SECRET_KEY`:**  
```bash
python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
```

## Автор

**Anatoliyfs**  
- GitHub: [github.com/Port-tf](https://github.com/anatoliyfs)  
- Email: tolikfs@gmail.com

## Лицензия

MIT
