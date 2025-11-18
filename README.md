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

- **Контейнеризация**: Docker, Docker Compose.

## Как развернуть проект в контейнерах


### 1. Предварительные требования

Убедитесь, что у вас установлены:
- [Docker](https://www.docker.com/products/docker-desktop);
- [Docker Compose](https://docs.docker.com/compose/install/).

### 2. Клонирование репозитория

```bash
git clone https://github.com/Port-tf/kittygram-backend.git
cd kittygram-backend
```

### 3. Подготовка окружения

1. Создайте файл `.env` в корне проекта (см. раздел «Настройка файла `.env`»).
2. Убедитесь, что все необходимые файлы (включая `docker-compose.yml`) присутствуют в проекте.


### 4. Сборка и запуск контейнеров

Выполните команду:

```bash
docker-compose up -d
```

Эта команда:
- скачает необходимые образы;
- создаст и запустит контейнеры;
- настроит сеть между сервисами.

### 5. Выполнение миграций

После запуска контейнеров выполните миграции базы данных:

```bash
docker-compose exec backend python manage.py migrate
```

### 6. Сбор статических файлов

Соберите статические файлы:

```bash
docker-compose exec backend python manage.py collectstatic --noinput
```

### 7. Создание суперпользователя (опционально)

Для доступа к админ‑панели создайте суперпользователя:

```bash
docker-compose exec backend python manage.py createsuperuser
```

### 8. Проверка работы

Откройте в браузере:
- API: `http://localhost:8000/api/`;
- Админ‑панель: `http://localhost:8000/admin/`.


### 9. Остановка контейнеров

Чтобы остановить контейнеры, выполните:

```bash
docker-compose down
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
DB_HOST=db
DB_NAME=kittygram
DB_PORT=5432


# Для SQLite (разработка)
USE_SQLITE=true  # Установите true для SQLite
```

**Как получить `SECRET_KEY`:**

```bash
python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
```

## Структура Docker-конфигурации

- `docker-compose.yml` — основной файл конфигурации контейнеров;
- `Dockerfile` (в папке `backend/`) — инструкция для сборки образа backend;
- `.env` — переменные окружения для контейнеров.


## Полезные команды Docker Compose

- Посмотреть статус контейнеров:
  ```bash
  docker-compose ps
  ```
- Просмотреть логи:
  ```bash
  docker-compose logs
  ```
- Пересобрать образы:
  ```bash
  docker-compose build
  ```
- Остановить и удалить контейнеры, сети, объёмы:
  ```bash
  docker-compose down -v
  ```

## Автор


**Anatoliyfs**  
- GitHub: [github.com/Port-tf](https://github.com/anatoliyfs)  
- Email: tolikfs@gmail.com

## Лицензия

MIT