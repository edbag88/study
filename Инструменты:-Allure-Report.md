# Allure Report

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Allure-Report/Allure-Report-banner-1.jpg)

Allure Report — фреймворк для формирования детальных отчётов о прохождении автотестов. Цветные статусы в терминале несут в себе мало информации и деталей, а в сообщениях об ошибках необходимо отдельно разбираться и отдельно изучать на каком этапе и из-за чего упал тест. Эти проблемы помогает решить Allure, который позволяет превратить краткие сообщения в детальные описания и добавить к ним скриншоты, снапшоты и скринкасты. Плюс Allure в том, что он не зависит от языка программирования и фреймворк можно подключить к любому окружению.

[Репозиторий GitHub](https://github.com/allure-examples) | [Сайт Allure Report](https://qameta.io/allure-report/) | [Официальная документация](https://docs.qameta.io/allure/) 

## Как подключить
В файле `build.gradle` необходимо в разделе `plugins` добавить зависимость:

```gradle
plugins {
  id "io.qameta.allure" version "2.11.2"
}
```

Актуальную версию всегда можно узнать на сайте [Gradle Plugins](https://plugins.gradle.org/plugin/io.qameta.allure).

Далее в том же файле надо задать конфигурацию плагина по следующему шаблону:
```gradle
allure {
    report {
        version.set("2.21.0") // версия Allure Report
        // Актуальную можно узнать по ссылке https://github.com/allure-framework/allure2
    }
    adapter {
        aspectjWeaver.set(true) // обработка аннотации @Step
        frameworks {
            junit5 {
                adapterVersion.set("2.21.0") // версия Allure JUnit5 
                // Актуальную можно узнать по ссылке https://github.com/allure-framework/allure-java
            }
        }
    }
}
```

## Как это работает 
С помощью Allure у тестировщика появляется возможность разметить сценарий теста для формирования более детальных и подробных отчётов. Каждый шаг теста сопровождается описанием, и в итоге получается такой пошаговый отчёт с индикацией состояния:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Allure-Report/allure_1.png)

Allure позволяет добавлять в отчёты аттачменты в виде скриншотов, снапшотов и записи экрана. Так отчёты становятся ещё более информативными и подробными. 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Allure-Report/allure_2.png)

В случае ошибки появляется возможность визуально оценить в чём была проблема и понять чем вызвана ошибка — некорректным тестом или, к примеру, обновлённым дизайном страницы, на которой поменяли расположения тестируемого элемента.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Allure-Report/allure_3.png)
