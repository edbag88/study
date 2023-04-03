# Allure Report

![](https://raw.githubusercontent.com/daniilshat/test/main/img/Allure-Report/Allure-Report-banner-1.jpg)

Allure Report — фреймворк для формирования детальных отчётов о прохождении автотестов. Цветные статусы в терминале несут в себе мало информации и деталей, а в сообщениях об ошибках необходимо отдельно разбираться и отдельно изучать на каком этапе и из-за чего упал тест. Эти проблемы помогает решить Allure, который позволяет превратить краткие сообщения в детальные описания и добавить к ним скриншоты, снапшоты и скринкасты. Плюс Allure в том, что он не зависит от языка программирования и фреймворк можно подключить к любому окружению.

[Репозиторий GitHub](https://github.com/allure-examples) | [Сайт Allure Report](https://qameta.io/allure-report/) | [Официальная документация](https://docs.qameta.io/allure/) 

## Как установить
Allure Reports доступен для Windows, Linux и macOS. Установка фреймворка сильно зависит от того, на какой операционной системе работает ваша машина. Подробные инструкции по установке можно найти по ссылке.

### macOS
На macOS установка производится с помощью Homebrew, который необходимо отдельно установить. После этого вводим в терминале команду `brew install allure` и система сама установит фреймворк.

### Linux
На машинах под управлением debian-подобных систем Allure Reports поставляется в PPA. Для установки необходимо поочерёдно ввести команды следующие команды в терминал:

```bash
sudo apt-add-repository ppa:qameta/allure
sudo apt-get update 
sudo apt-get install allure
```

### Windows
Для Windows Allure Reports поставляется в Scoop. Его необходимо отдельно установить, а затем выполнить в Powershell команду `scoop install allure`.

## Как подключить и пользоваться
Для подключения к проекту Allure Reports необходимо перейти в файл `requirements.txt` и добавить к нему строку `allure-pytest`. После этого следует нажать кнопку Install plugins в верхней части экрана.

Далее переходим в файл с тестами. И нажимаем на зеленую иконку запуска кода. В открывшемся меню выбираем пункт Modify Run Configuration.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-python/Allure%20Report/allure-report-1.jpg)

В окне находим пункт Additional Arguments. Вводим в поле строку `--alluredir=allure-results`. Нажимаем ОК.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-python/Allure%20Report/allure-report-2.jpg)

После этого в директории проекта появится папка `allure-results` со служебными файлами в ней.

Для генерации отчётов в терминале необходимо выполнить команду `allure serve [directory]`. Вместо `[directory]` следует подставить путь до директории, в которой у нас лежат результаты отчётов, к примеру `tests/allure-results`. После этого в браузере откроется подробный отчёт по тестам.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-python/Allure%20Report/allure-report-3.jpg)
