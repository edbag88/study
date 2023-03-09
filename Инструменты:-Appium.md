# Appium

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Appium/appium-banner-1.jpg)

Appium — бесплатный кроссплатформенный инструмент для автоматизации тестирования мобильных приложений на Android и iOS. У Appium открытый исходный код, он работает по принципам Selenium WebDriver: получает HTTP-запрос в виде JSON-файла и преобразует его в платформозависимые команды.

С помощью Appium можно с лёгкостью автоматизировать тестирование мобильных приложений или сайтов. При этом можно использовать и физическое устройство, что несколько упрощает взаимодействие с системой.

## Установка
1. Перейти по [ссылке](https://github.com/appium/appium-desktop/releases) в официальный репозиторий Appium Desktop и скачать релиз для актуальной операционной системы.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Appium/appium-1.jpg)

2. Перейти на официальный [сайт]() Android Studio и скачать IDE для разработки под Android. В пакет входит Android SDK, который понадобится для запуска тестов на мобильном устройстве.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Appium/appium-2.jpg)

3. После установки Appium Desktop и Android Studio необходимо запустить Appium Desktop, нажать на кнопку «Edit Configuration» и указать путь к JDK и Android SDK.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Appium/appium-3.jpg)

## Appium Inspector
Во время разработки тестов для веб-приложений тестировщики пользуются инструментарием браузера для поиска элементов и локаторов. При мобильном тестировании для этого используется Appium Inspector. Для его установки необходимо перейти по [ссылке](https://github.com/appium/appium-inspector), скачать последнюю версию для актуальной платформы и запустить для установки.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Appium/appium-4.jpg)

## Как это работает
Appium представляет собой HTTP-сервер, управляющий сессиями Android и iOS. Appium принимает запрос на подключение и команды, которые выполняет на смартфоне. При этом тестировщику для разработки тестов не надо знать о том, как работает мобильная операционная система. Appium получит команды и сам переделает их в понятные для Android или iOS.
