# Kaspresso

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java-plus/Kaspresso/kaspresso-wiremock.jpg)

Kaspresso — это фреймворк для тестирования Android-приложений, написанных на языке программирования Kotlin. Он предоставляет удобный и простой способ написания автоматических тестов для проверки функциональности приложений на Android-устройствах.

Kaspresso использует подход «обертки над Espresso», который облегчает написание тестов и уменьшает количество необходимого кода. Он также предоставляет множество вспомогательных функций, таких как генерация тестовых данных, создание скриншотов и проверка отображения элементов пользовательского интерфейса. Кроме того, Kaspresso поддерживает интеграцию с другими фреймворками, такими как Allure, JUnit и TestNG, что позволяет получать более подробную информацию о результатах тестирования.

[Репозиторий](https://github.com/KasperskyLab/Kaspresso)

## Установка
Для установки в файле `build,.gradle` необходимо указать следующую зависимость:

```gradle
dependencies {
    androidTestImplementation 'com.kaspersky.android-components:kaspresso:1.2.0'
}
```

Для возможности делать скриншоты, генерировать данные и использовать дополнительные возможности файл можно расширить:

```gradle
dependencies {
    androidTestImplementation 'com.kaspersky.android-components:kaspresso:1.2.2'
    androidTestImplementation 'com.kaspersky.android-components:kaspresso-extensions:1.2.2'
}
```

Актуальную версию Kaspresso можно узнать на сайте [MVN Repository](https://mvnrepository.com/artifact/com.kaspersky.android-components/kaspresso?repo=jcenter).
