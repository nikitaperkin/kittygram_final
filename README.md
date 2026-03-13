# Kittygram

![CI/CD](https://github.com/nikitaperkin/kittygram_final/actions/workflows/main.yml/badge.svg)

## Описание проекта
Kittygram — это социальная сеть для любителей котиков. Проект разработан для того, чтобы владельцы котиков могли делиться фотографиями своих питомцев и смотреть чужих. 

**Основные функции:**
- Регистрация и авторизация пользователей.
- Добавление питомцев с фотографией, указанием имени, цвета и года рождения.
- Добавление и привязка достижений к своим котикам.
- Просмотр ленты с котиками других пользователей.

**Проект развернут и доступен по адресу:** https://goodkittylife.hopto.org

## Стек технологий
- Backend: Python 3.12, Django, Django REST Framework
- База данных: PostgreSQL
- Сервер: Nginx, Gunicorn
- Контейнеризация: Docker, Docker Compose
- CI/CD: GitHub Actions

## Как развернуть проект

1. Клонируйте репозиторий на свой компьютер:
   ```bash
   git clone git@github.com:nikitaperkin/kittygram_final.git
   cd kittygram_final
   ```

2. Создайте файл `.env` в корневой директории проекта (правила заполнения описаны в следующем разделе).

3. Соберите и запустите контейнеры:
   ```bash
   docker compose up -d --build
   ```

4. Выполните миграции базы данных:
   ```bash
   docker compose exec backend python manage.py migrate
   ```

5. Соберите статические файлы:
   ```bash
   docker compose exec backend python manage.py collectstatic --no-input
   docker compose exec backend cp -r /app/collected_static/. /backend_static/static/
   ```

6. Создайте суперпользователя (по желанию):
   ```bash
   docker compose exec backend python manage.py createsuperuser
   ```

После выполнения этих шагов локальная версия проекта будет доступна по адресу `http://localhost`.

## Как заполнить .env

Создайте файл `.env` в корневой папке проекта (на одном уровне с `docker-compose.yml`) и добавьте в него следующие настройки:

```text
# Настройки Django
SECRET_KEY=любой_надежный_секретный_ключ
DEBUG=False
ALLOWED_HOSTS=127.0.0.1,localhost,goodkittylife.hopto.org

# Настройки PostgreSQL
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_HOST=db
DB_PORT=5432

# Переключатель для использования PostgreSQL (False) или SQLite (True)
USE_SQLITE=False
```

## Автор
[Ваше Имя](https://github.com/nikitaperkin)
