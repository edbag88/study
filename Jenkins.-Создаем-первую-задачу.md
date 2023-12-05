## Что это такое?
Jenkins — система для обеспечения процесса непрерывной интеграции (CI) программного обеспечения. Jenkins написан на Java и у инструмента открытый исходный код.

- Репозиторий [[ссылка]](https://github.com/jenkins-infra/jenkins.io)
- Сайт [[ссылка]](https://www.jenkins.io/)

## Как обычно происходит процесс запуска тестов

### Локально

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-1.png)

### Удаленно 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-2.png)

## Как создать задачу в Jenkins
Сперва необходимо пройти регистрацию в сервисе облачного тестирования. У Jenkins открытый исходный код, поэтому регистрация бесплатная. Для регистрации необходимо перейти по [ссылке](https://jenkins.autotests.cloud/login?from=%2F), нажать на соответствующую кнопку и пройти пошаговый процесс.

После регистрации или входа мы оказываемся на странице дашборда. Далее необходимо нажать на кнопку «Создать Item».

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-3.png)

На открывшейся странице указываем имя задачи и выбираем поле «Создать задачу со свободной конфигурацией».

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-4.png)

В блоке управления исходным кодом выбираем Git, вставляем ссылку на репозиторий с кодом тестов и обязательно проверяем правильность написания ветки (main/master).

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-5.png)

В параметрах сборки выбираем Invoke Gradle script, кликаем на правильную версию Gradle,указываем имя задачи и сохраняем.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-6.png)

Собрать и запустить тесты можно нажатием кнопки «Собрать сейчас».

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-7.png)

## Подключаем Allure Report 
К Jenkins можно подключить отчеты Allure, но сначала надо убедиться, что система подключена в самом проекте. Подробную инструкцию можно найти по [ссылке](https://github.com/qa-guru/knowledge-base/wiki/7.-Allure-Reports).

Далее переходим в настройки задачи в Jenkins и в блоке «Послесборочные операции» выбираем Allure Report.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/les10/les10-8.png)

В файле конфигурации браузера надо указать, чтобы тесты запускались не в локальном браузере, а в Selenoid.

Вставляем следующий фрагмент кода:
```java
Configuration.remote = "https://user1:1234@selenoid.autotests.cloud/wd/hub";
```

## Добавляем видео в отчет
В файле конфигурации добавляем код:
```java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability("selenoid:options", Map.<String, Object>of(
     "enableVNC", true,
     "enableVideo", true
));
Configuration.browserCapabilities = capabilities;
```

Далее в классе с `Attachments` добавляем следующее: 
```java
@Attachment(value = "Video", type = "text/html", fileExtension = ".html")
    public static String addVideo() {
        return "<html><body><video width='100%' height='100%' controls autoplay><source src='"
                + getVideoUrl(getSessionId())
                + "' type='video/mp4'></video></body></html>";
    }

    public static URL getVideoUrl(String sessionId) {
        String videoUrl = "https://selenoid.autotests.cloud/video/" + sessionId + ".mp4";

        try {
            return new URL(videoUrl);
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
        return null;
    }

    public static String getSessionId(){
        return ((RemoteWebDriver) getWebDriver()).getSessionId().toString();
    }
```

И в конце теста вызываем метод:
```java
Attach.addVideo();
```
