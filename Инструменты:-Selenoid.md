# Selenoid

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Selenoid/selenoid-banner-1.jpg)

Selenoid — альтернатива Selenium Grid, позволяющая управлять браузерами и запускать параллельные тесты. Каждый браузер запускается в изолированной среде Docker и закрывается после завершения теста. Такой подход позволяет запускать тысячи тестов и экономить вычислительные мощности.

Принцип работы заключается в том, что каждый контейнер содержит в себе браузер определённой версии, драйверы, библиотеки, зависимости и сервер Selenium. Именно изоляция процесса и позволяет нескольким тестам запускаться параллельно и не мешать друг другу. Selenoid поддерживает все популярные браузеры.

[Сайт](https://aerokube.com/selenoid/) | [Репозиторий](https://github.com/aerokube/selenoid) | [Документация](https://aerokube.com/selenoid/latest/)

## Установка

1. Перейти в официальный [репозиторой](https://github.com/aerokube/selenoid/releases) Selenoid;
2. Во вкладке релизов скачать последнюю версию для актуальной платформы;

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Selenoid/selenoid-1.jpg)

3. Запустить файл и пройти процесс установки.

## Запуск
>Для запуска надо установить Docker. Без него Selenoid не будет работать.


Selenoid запускается с помощью следующей команды:

Для Windows:   
```bash
> ./cm.exe selenoid start --vnc
```

Для macOS и Linux:
```bash
$ ./cm selenoid start --vnc
```

Запустить интерфейс Selenoid можно с помощью команды: `./cm selenoid-ui start`.
