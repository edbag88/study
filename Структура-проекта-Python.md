Данная структура проекта предназначена для автоматизации тестирования веб-приложений, мобильных приложений и API.
Ниже представлен пример структуры проекта, название папок и файлов могут отличаться в зависимости от проекта.

Ссылки на дипломные проекты с правильной структурой проекта:

[https://github.com/Wildips/demoqa_diplome](https://github.com/Wildips/demoqa_diplome)

[https://github.com/Wildips/wiki_mobile_project](https://github.com/Wildips/wiki_mobile_project)

[https://github.com/Wildips/qa_g-rest-api](https://github.com/Wildips/qa_g-rest-api)

[https://github.com/div50015/diploma-project](https://github.com/div50015/diploma-project)

[https://github.com/o1ra/intertop/tree/main](https://github.com/o1ra/intertop/tree/main)

[https://github.com/o1ra/krisha](https://github.com/o1ra/krisha)

```
my-project-tests/           # корневой каталог проекта(название проекта)(пример litress-project-tests)
│
├── my_project_tests/       # основной каталог модулей(корневой пакет(название должно совпадать с названием проекта, только через подчеркивание))
│   ├── __init__.py   # инициализация пакета
│   ├── utils/   # каталог для  хелперов(утилит(для построения путей, аттачей и т.д.))
│   │   ├── __init__.py # инициализация пакета
│   │   ├── attach.py # файл с элементами attach(видео, скриншоты и т.д.)
│   │   ├── command.py       # файл с командами для запуска тестов( к примеру мобильных(swipe, tap и т.д.))
│   │   └── paths.py # файл для путей к файлам
│   │
│   ├── test_data/          # каталог для тестовых данных
│   │   ├── __init__.py # инициализация пакета
│   │   └── data.py/        # файл с тестовыми данными для тестов
│   │
│   └── models/        # каталог для моделей
│       ├── __init__.py # инициализация пакета
│       ├── app.py # файл для реализации типа шаблона Application Manager для пейдж обжектов
│       └──pages/            # каталог для страниц
│           ├── __init__.py   # инициализация пакета
│           ├── registration_page.py      # код страницы 1
│           └── authorization_page.py      # код страницы 2
или
│   ├── pages/            # каталог для страниц
│   │   ├── __init__.py   # инициализация пакета
│   │   ├── ui/           # каталог для UI страниц
│   │   │   ├── __init__.py # инициализация пакета
│   │   │   ├── registration_page.py      # код страницы 1
│   │   │   └── authorization_page.py      # код страницы 2
│   │   │
│   │   └──  mobile/          # каталог для мобильных страниц
│   │       ├── __init__.py # инициализация пакета
│   │       ├── registration_page.py      # код страницы 1
│   │       └── authorization_page.py      # код страницы 2
│   │
│   └──utils/          # каталог для утилит
│       ├── __init__.py # инициализация пакета
│       ├── requests_helper.py    # файл с утилитами для запросов
│       └── sessions.py    # файл с утилитами для сессий(BaseSession)
│
├── tests/            # каталог с тестами
│   ├── __init__.py   # инициализация пакета
│   ├── api/          # тесты API
│   │   ├── __init__.py # инициализация пакета
│   │   ├── test.py # тесты на api
│   │   └── conftest.py   # файл conftest для API тестов
│   │
│   ├── ui/           # тесты UI
│   │   ├── __init__.py # инициализация пакета
│   │   ├── test.py # тесты на UI
│   │   └── conftest.py   # файл conftest для UI тестов
│   │
│   └── mobile/       # тести для мобилок
│       ├── __init__.py # инициализация пакета
│       ├── test.py # тесты на мобилки
│       └── conftest.py  # файл conftest для мобилок
или
├── tests/            # каталог с тестами
│   ├── __init__.py   # инициализация пакета
│   ├──conftest.py  # файл conftest для всех тестов
│   ├── api/          # тести API
│   │   ├── __init__.py # инициализация пакета
│   │   └── test.py # тесты на api
│   │
│   ├── ui/           # тесты UI
│   │   ├── __init__.py # инициализация пакета
│   │   └──  test.py # тесты на UI
│   │
│   └── mobile/       # тести для мобилок
│       ├── __init__.py # инициализация пакета
│       └──  test.py # тесты на мобилки
│
├── config.py         # файл с конфигурацией проекта(конфигурации в зависимости от окружения(env-прод, dev и т.д.))
│
├── resources/        # каталог для ресурсов
│   ├── images/       # каталог для изображений
│   │   └──  foto.png
│   │
│   ├── videos/       # каталог для видео
│   │   └──  video.mp4
│   │
│   └── files/        # каталог для файлов
│       └──  file.txt
│
├── schemas/          # каталог для схем API
│   ├── schema1.json  # схема API 1 (название должно отображать название схемы)
│   └── schema2.json  # схема API 2 (название должно отображать название схемы)
или
├── schemas/          # каталог для схем API
│   ├── __init__.py   # инициализация пакета
│   └── project.py    # схемы voluptuous api для всего проекта api
│
│
├── docs/             # документация проекта
│
├── .gitignore        # файл для игнорирования файлов/директорий в git
├── README.md         # описание проекта
├──.env_prod               # файл с переменными окружения для продакшн
├──.env_dev                # файл с переменными окружения для дев
├── pytest.ini        # файлик конфигурации pytest
├── requirements.txt  # зависимости проекта
или
├── pyproject.toml/     # файл для управления зависимостями проекта
└── poetry.lock/        # файл для управления зависимостями проекта
```
