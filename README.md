# Yatube API

API для социальной сети Yatube, позволяющее взаимодействовать с публикациями, комментариями, группами и подписками.

## Описание

Yatube - это платформа для обмена мыслями, идеями и фотографиями.  Данное API предоставляет разработчикам возможность интегрировать функциональность Yatube в свои приложения.  API использует RESTful архитектуру и JSON для обмена данными.

## Установка

1. **Клонируйте репозиторий:**

   ```bash
   git clone https://github.com/srv328/api_final_yatube.git
   cd yatube_api
   ```

2. **Создайте и активируйте виртуальное окружение:**

   ```bash
   python3 -m venv env
   source env/bin/activate  # Linux/macOS
   env\Scripts\activate  # Windows
   ```

3. **Установите зависимости:**

   ```bash
   python3 -m pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Выполните миграции:**

   ```bash
   python manage.py migrate
   ```

5. **Запустите сервер разработки:**

   ```bash
   python manage.py runserver
   ```


## Примеры запросов

**Аутентификация (JWT):**

* **Получение токена:**

    ```bash
    curl -X POST -d "username=<username>&password=<password>" /api/v1/jwt/create/
    ```

* **Обновление токена:**

    ```bash
    curl -X POST -d "refresh=<refresh_token>" /api/v1/jwt/refresh/
    ```



**Работа с публикациями (требуется авторизация):**

* **Получение всех публикаций (с пагинацией):**

    ```bash
    curl -H "Authorization: Bearer <access_token>" /api/v1/posts/?limit=10&offset=0
    ```

* **Создание публикации:**

    ```bash
    curl -X POST -H "Authorization: Bearer <access_token>" -d '{"text": "Мой новый пост", "group": 1}' /api/v1/posts/
    ```

* **Получение публикации по ID:**

    ```bash
    curl -H "Authorization: Bearer <access_token>" /api/v1/posts/<post_id>/
    ```

* **Изменение публикации (только автор):**

    ```bash
    curl -X PUT -H "Authorization: Bearer <access_token>" -d '{"text": "Измененный текст"}' /api/v1/posts/<post_id>/
    ```

* **Удаление публикации (только автор):**

    ```bash
    curl -X DELETE -H "Authorization: Bearer <access_token>" /api/v1/posts/<post_id>/
    ```


**Работа с комментариями (требуется авторизация):**

* **Получение комментариев к посту:**

    ```bash
    curl -H "Authorization: Bearer <access_token>" /api/v1/posts/<post_id>/comments/
    ```

* **Создание комментария:**

    ```bash
    curl -X POST -H "Authorization: Bearer <access_token>" -d '{"text": "Мой комментарий"}' /api/v1/posts/<post_id>/comments/
    ```



**Работа с группами (не требует авторизации):**

* **Получение списка групп:**

    ```bash
    curl /api/v1/groups/
    ```

* **Получение группы по ID:**

    ```bash
    curl /api/v1/groups/<group_id>/
    ```

**Работа с подписками (требуется авторизация):**


* **Получение всех подписок:**

   ```bash
   curl -H "Authorization: Bearer <access_token>" /api/v1/follow/
   ```

* **Подписка на пользователя:**

    ```bash
    curl -X POST -H "Authorization: Bearer <access_token>" -d '{"following": "<username>"}' /api/v1/follow/
    ```



## Документация API

Полная документация API доступна по адресу: `http://127.0.0.1:8000/redoc/`
