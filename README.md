<a id="anchor"></a>

###REST API для сервиса **YaMDb** 
_База отзывов о фильмах, книгах и музыке._

Групповой итоговый проект студентов _Яндекс.Практикум_ по курсу **"API: интерфейс взаимодействия программ"**

**Описание**
Проект **YaMDb** собирает отзывы пользователей на произведения. 
Произведения делятся на категории: «Книги», «Фильмы», «Музыка». 
Список категорий (Category) может быть расширен (например, можно добавить категорию 
«Изобразительное искусство» или «Ювелирка» через интерфейс Django администратора).

**API для сервиса YaMDb.** позволяет работать со следующими сущностями:

**Пользователи** (Получить список всех пользователей, создание пользователя, получить пользователя по username, изменить данные пользователя по username, удалить пользователя по username, получить данные своей учетной записи, изменить данные своей учетной записи)

**Произведения**, к которым пишут отзывы (Получить список всех объектов, создать произведение для отзывов, информация об объекте, обновить информацию об объекте, удалить произведение)

**Категории** (типы) произведений (Получить список всех категорий, создать категорию, удалить категорию)

**Жанры** (Получить список всех жанров, создать жанр, удалить жанр)

**Отзывы** (Получить список всех отзывов, создать новый отзыв, получить отзыв по id, частично обновить отзыв по id, удалить отзыв по id. Каждый зарегистрированный пользователь может оставить только 1 отзыв к произведению.)

**Коментарии к отзывам** (Получить список всех комментариев к отзыву по id, создать новый комментарий для отзыва, получить комментарий для отзыва по id, частично обновить комментарий к отзыву по id, удалить комментарий к отзыву по id)

**JWT-токен** (Отправление confirmation_code на переданный email, получение JWT-токена в обмен на email и confirmation_code. Также для сеперюзера предусмотрена возможность получения и обновления токена через встроенные в Simple JWT эндпоинты.)

**После запуска проекта ознакомиться с документацией можно по ссылке** http://localhost/redoc/

**Примеры запросов и ответов (в формате json)**
Получить токен для суперпользователя:
POST: http://127.0.0.1:8000/api/v1/jwt/create/
~~~
{
    "username": "user_example",
    "password": "example"
}
~~~
 
Регистрация нового пользователя:
POST: http://127.0.0.1:8000/api/v1/auth/signup/
~~~

{
"email": "string",
"username": "string"
}
~~~
Получение JWT-токена:
POST: http://127.0.0.1:8000/api/v1/auth/token/
~~~
{
"username": "string",
"confirmation_code": "string"
}
~~~
Получение списка всех категорий(токен не требуется):
GET: http://127.0.0.1:8000/api/v1/categories/
~~~
[
{
"count": 0,
"next": "string",
"previous": "string",
"results": []
}
]
~~~
Получение списка всех жанров(токен не требуется):
GET:http://127.0.0.1:8000/api/v1/genres/
~~~
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "name": "string",
        "slug": "string"
      }
    ]
  }
]
~~~

Получить информацию о произведении по id(токен не требуется):
GET: http://127.0.0.1:8000/api/v1/titles/{titles_id}/
~~~
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}
~~~
Получение списка всех отзывов:
GET: http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/
~~~
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "text": "string",
        "author": "string",
        "score": 1,
        "pub_date": "2019-08-24T14:15:22Z"
      }
    ]
  }
]
~~~
Авторизованные пользователи могут оставлять отзывы о произведениях, удалять и редактировать свои отзывы. Для этого необходимо сделать POST, PATCH или DELETE запрос на http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/
Также им доступны все действия с комментариями, авторами которых они являются. 

Получение отзыва по id:
GET: http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/
~~~
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}
~~~


Получение списка всех произведений(токен не требуется):
GET: http://127.0.0.1:8000/api/v1/titles/
~~~
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "name": "string",
        "year": 0,
        "rating": 0,
        "description": "string",
        "genre": [
          {
            "name": "string",
            "slug": "string"
          }
        ],
        "category": {
          "name": "string",
          "slug": "string"
        }
      }
    ]
  }
]
~~~

**Используемый стек технологий:**

* язык программирования Python 3.7.9 https://www.python.org/downloads/release/python-379/;
* фреймворк Django REST Framework 3.12.4 https://www.django-rest-framework.org/.
* аутентификация пользователей с помощью Simple JWT 5.2.2 https://django-rest-framework-simplejwt.readthedocs.io/en/latest/
* Docker
* NGINX
* GUNICORN
* база даннных POSTGRES

**Запуск проекта**
Клонируйте проект infra_sp2 из репозитория sailormoon2111 на GITHUB:

~~~
git clone git@github.com:sailormoon2111/infra_sp2.git
~~~

При первом запуске для функционирования проекта обязательно установить виртуальное окружение, установить зависимости,  выполнить миграции:
```
# создаем виртуальное окружение
python -m venv env

source env/Scripts/activate
```
```
# далее переходим в директорию api_yamdb
python -m pip install --upgrade pip

pip install -r requirements.txt
```
```
# переходим в infra файлом docker-compose.yaml и запускаем контейнеры
docker-compose up -d --build
```
```
# далее выполняем миграции
docker-compose exec web python manage.py makemigrations reviews
docker-compose exec web python manage.py migrate
```
```
#Создаем суперпользователя:
docker-compose exec web python manage.py createsuperuser
```
```
#Сoрбираем статику:
docker-compose exec web python manage.py collectstatic --no-input
```
```
#Создаем дамп базы данных (нет в текущем репозитории):
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```
```
# загрузкой фикстур в базу данных
docker cp dumpPostrgeSQL.json <container id>:app/
# далее 
docker-compose exec web python manage.py loaddata dumpPostrgeSQL.json
```
```
#Останавливаем контейнеры:
docker-compose down -v
```

_Шаблон наполнения env-файла_

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

**Участники:**

[Ванданова Мария.](https://github.com/sailormoon2111)
Управление пользователями (Auth и Users): система регистрации и аутентификации, права доступа, работа с токеном, система подтверждения e-mail, поля. Сборка образа. 

[Левкович Кирилл.](https://github.com/?????????)
Категории (Categories), жанры (Genres) и произведения (Titles): модели, view и эндпойнты для них и рейтинги.

[Воротынцев Дмитрий.](https://github.com/psyxopat154) 
Отзывы (Review) и комментарии (Comments): модели и view, эндпойнты, права доступа для запросов. Рейтинги произведений. Роль тимлидера.

_[Вверх](#anchor)_