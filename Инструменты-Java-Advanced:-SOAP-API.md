# SOAP API

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java-plus/SOAP/soap-wiremock.jpg)

SOAP (Simple Object Access Protocol) - это протокол для обмена сообщениями, используемый для создания веб-сервисов. SOAP API представляет собой стандартный способ общения между клиентом и сервером с помощью XML-сообщений, которые содержат данные, которые нужно передать или получить. SOAP API использует протокол HTTP (или HTTPS) для отправки сообщений между клиентом и сервером.

SOAP API является удобным и распространенным способом создания веб-сервисов в Java. Он обеспечивает возможность передачи структурированных данных, включая сложные объекты и списки, по сети, что делает его более гибким, чем REST API. Кроме того, SOAP API обеспечивает высокий уровень безопасности и целостности данных, позволяя использовать различные протоколы шифрования и аутентификации. В Java для работы с SOAP API можно использовать библиотеку Apache Axis или же стандартную библиотеку JAX-WS.

## Установка
Для установки в файл `build.gradle` необходимо добавить репозиторий JAX-WS:

```gradle
repositories {
    mavenCentral()
    maven {
        url "https://repo1.maven.org/maven2/"
    }
    maven {
        url "https://repository.jboss.org/nexus/content/groups/public-jboss/"
    }
}
```

После в этот же файл надо добавить зависимость:

```gradle
dependencies {
    implementation 'com.sun.xml.ws:jaxws-rt:2.3.2'
    implementation 'javax.xml.bind:jaxb-api:2.3.1'
}
```
