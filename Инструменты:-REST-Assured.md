# REST Assured

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/REST-Assured/rest-assured-banner-1.jpg)

[Cайт](https://rest-assured.io) | [Репозиторий GitHub](https://github.com/rest-assured/rest-assured)

REST Assured — один из самых популярных инструментов для тестирования REST API. Представлен в виде библиотеки Java. Широко используется для тестирования веб-приложений на базе XML и JSON. Полностью поддерживает работу с методами `GET`, `PUT`, `PATCH`, `POST` и `DELETE`.

REST Assured относительно простая библиотека с интуитивно понятным синтаксисом. Из-за большой популярности REST Assured в Сети можно найти большое количество подробных примеров кода и инструкций. Официальная документация также представлена в хорошем качестве и обновляется по мере выхода новых версий.

## Подключение
REST Assured подключается к проекту как все библиотеки. В файле `build.gradle` необходимо добавить зависимость:

```gradle
dependencies {
    testImplementation(
        "io.rest-assured:rest-assured:5.3.0"
    )
} 
```

Актуальную версию можно посмотреть на [сайте](https://rest-assured.io) или в [документации](https://github.com/rest-assured/rest-assured/wiki/GettingStarted)

## Как это работает
REST Assured работает по принципу Given-When-Then:
- Given — определяет, что будет отправлено в запросе;
- When — с каким методом будет передано и к какому эндпоинту;
- Then — как будет оцениваться полученный ответ.

С помощью этих ключевых слов формируется запрос. Пример запроса с помощью REST Assured может выглядеть так:

```java
public class RestTests {
    @Test
    void checkTotal() {
        given()
                .when()
                .get("https://selenoid.autotests.cloud/status")
                .then()
                .body("total", is(20));
    }
}
```

## Про методы API
К веб-ресурсу надо обращаться на понятном ему языке. Для веб-сайтов на базе REST API используются специальные методы. С их помощью данные можно отправлять, получать, удалять и изменять:

- `GET` — метод для чтения данных, информация просто передаётся с сервера и никак не изменяется;
- `POST` — создание и регистрация новых записей;
- `PUT` — изменение и обновление данных;
- `DELETE` — удаление данных.
