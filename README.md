# API YaMDB

![Yamdb Workflow Status](https://github.com/rasputin-pro/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master&event=push)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
___
Проект **API YaMDb** собирает **отзывы** (**Review**) пользователей **на 
произведения** (**Titles**). Произведения делятся на категории: «Книги», 
«Фильмы», «Музыка». Список **категорий** (**Category**) может быть расширен 
администратором (например, можно добавить категорию «изобразительное 
искусство» или «Ювелирка»).

Сами произведения в **API YaMDb** не хранятся, здесь нельзя посмотреть фильм 
или послушать музыку.

В каждой категории есть **произведения**: книги, фильмы или музыка. Например, 
в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и 
«Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы 
«Насекомые» и вторая сюита Баха.

Произведению может быть присвоен **жанр** (**Genre**) из списка 
предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры 
может создавать только администратор.

Благодарные или возмущённые пользователи оставляют к произведениям текстовые 
**отзывы** (**Review**) и ставят произведению оценку в диапазоне от одного до 
десяти (целое число); из пользовательских оценок формируется усреднённая 
оценка произведения — **рейтинг** (целое число). На одно произведение 
пользователь может оставить только один отзыв.


## Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:rasputin-pro/api_yamdb.git

cd api_yamdb
```

Создать и активировать виртуальное окружение:

```commandline
python3 -m venv env

source env/bin/activate

python3 -m pip install --upgrade pip
```

Установить зависимости и выполнить миграции:

```commandline
pip install -r requirements.txt

python3 manage.py migrate
```

Запустить проект:

```commandline
python3 manage.py runserver
```

Для загрузки тестовых данных из csv-файлов выполнить команду:
```commandline
python3 manage.py loadcsv
```



## Самостоятельная регистрация пользователей
1. Пользователь отправляет POST-запрос на добавление нового пользователя с 
параметрами `email` и `username` на эндпоинт `/api/v1/auth/signup/`: 
```json
{
    "username": "user",
    "email": "user@mail.ru"
}
```
2. Пользователю приходит письмо с кодом подтверждения `confirmation_code` на 
адрес `email`;
3. Пользователь отправляет POST-запрос с параметрами `username` и 
`confirmation_code` на эндпоинт `/api/v1/auth/token/`, в ответе на запрос ему 
приходит `token` (JWT-токен):
```json
{
    "username": "user",
    "confirmation_code": "ae6c10d0-0b13-554c-b976-a05d8a18f0cc"
}
```
4. При желании пользователь отправляет PATCH-запрос на эндпоинт 
`/api/v1/users/me/` и заполняет поля в своём профайле.



## Создание пользователя администратором
Пользователя может создать администратор — через админ-зону сайта или через 
POST-запрос на специальный эндпоинт `/api/v1/users/` В этот момент письмо с 
кодом подтверждения пользователю не отправляется.

После этого пользователь должен самостоятельно отправить свой `email` и 
`username` на эндпоинт `/api/v1/auth/signup/`, в ответ ему должно прийти 
письмо с кодом подтверждения.

Далее пользователь отправляет POST-запрос с параметрами `username` и 
`confirmation_code` на эндпоинт `/api/v1/auth/token/`, в ответе на запрос ему 
приходит `token` (JWT-токен), как и при самостоятельной регистрации.


## Ресурсы API YaMDb
- **auth**: аутентификация.
- **users**: пользователи.
- **titles**: произведения, к которым пишут отзывы (определённый фильм, 
  книга или песенка).
- **categories**: категории (типы) произведений («Фильмы», «Книги», 
  «Музыка»).
- **genres**: жанры произведений. Одно произведение может быть привязано 
  к нескольким жанрам.
- **reviews**: отзывы на произведения. Отзыв привязан к определённому 
  произведению.
- **comments**: комментарии к отзывам. Комментарий привязан к 
  определённому отзыву.


## Документация
После запуска проекта - по адресу: `http://127.0.0.1:8000/redoc/` доступна 
документация.


## Над проектом работали:
- [Андрей Распутин](https://github.com/rasputin-pro)
- [Кирилл Сухарев](https://github.com/Soliton80)
- [Александр Корнеев](https://github.com/rtx4090)