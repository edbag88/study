# Selenide

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Selenide/selenide-banner-1.jpg)

Selenide — фреймворк для автоматического тестирования веб-приложений. Selenide представляет собой обёртку вокруг Selenium WebDriver. Преимущество в том, что разработчик может быстро приступить к тестированию, сосредоточившись на коде, а не настройке браузера и окружения.

[Сайт проекта](https://ru.selenide.org/index.html) | [GitHub репозиторий](https://github.com/selenide/selenide)

## Установка
Selenide подключает к проекту таким же образом, как и любые другие фреймворки или библиотеки. В файле `build.gradle` необходимо добавить зависимость:

```gradle
dependencies {
  testImplementation 'com.codeborne:selenide:6.11.1'
}
```

Актуальную версию Selenide для подключения всегда можно узнать в официальном [руководстве](https://ru.selenide.org/quick-start.html) проекта или в [Maven Repository](https://mvnrepository.com/artifact/com.codeborne/selenide). После подключения проект будет собираться вместе с Selenide.

## Как пользоваться
Selenide сильно упрощает процесс разработки тестов. Название методов интуитивно поняты, а IDE предлагает подсказки и подсвечивает синтаксис.

### Краткий список основных сниппетов кода:
```java
// Открыть страницу в браузере
open("https://google.com");

// Очистить файлы куки
Selenide.clearBrowserCookies();

// Закрытие активной вкладкой 
Selenide.clearBrowserCookies();

// Закрытие всех вкладок
Selenide.closeWebDriver();

// Поиск по тексту
$(byText("full text")).click();

// Поиск по атрибуту
$(byAttribute("abc", "x")).click();
$("[abc=x]").click();

// Поиск по ID элемента
$(byId("mytext")).click();
$("#mytext").click();

// Клик мышкой по элементу
$("").click();

// Двойной клик мышкой
$("").doubleClick();

// Клик правой кнопкой мыши
$("").contextClick();
```
