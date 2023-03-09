# JUnit 5

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/JUnit/junit-banner.jpg)

JUnit 5 — популярный фреймворк Java для автоматического тестирования программного обеспечения. С помощью JUnit можно реализовывать модульное тестирование, когда проверяется работа каждого отдельного модуля.

[Сайт проекта](https://junit.org/junit5/) | [GitHub репозиторий](https://github.com/junit-team/junit5/)

## Установка
JUnit 5 подключается к проекту таким же образом, как и любые другие фреймворки и библиотеки. В файле `build.gradle` необходимо добавить зависимость:

```gradle
dependencies {
    testImplementation (
            "org.junit.jupiter:junit-jupiter:5.9.2")
}

test {
    useJUnitPlatform()
}
```

Актуальную для подключения версию JUnit всегда можно узнать в [Maven Repository](https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api). После подключения проект будет собираться вместе с JUnit.

## Как пользоваться
Тестирование ПО с помощью JUnit 5 осуществляется с помощью аннотаций, которые указывают, что конкретный метод или класс должен выполнить. К примеру, аннотация `@Test` отмечает метод/класс в качестве теста JUnit. Система проверит утверждение в скобках и, если оно будет истиной, вернёт результат:

```java
@Test
void assertTets() {
    Assertions.assertTrue(2 < 3);
}
```

JUnit позволяет выносить части кода, которые часто выделяются в отдельные методы, и выполнять их автоматически при определённых условиях. К примеру, если надо выполнять действия перед каждым тестом или после каждого, можно использовать аннотации `@BeforeEach` и `@AfterEach`:

```java
@BeforeEach
void function() {
    ...
}

@AfterEach
void function() {
    ...
}
```

Если действия надо выполнять перед всеми тестами или после всех тестов, можно воспользоваться аннотациями `@BeforeAll` и `@AfterAll`:

```java
    @BeforeAll
static void initDB() {
    //...
    //...
}

@AfterAll
static void cleanDB() {
    //...
    //...
}
```
