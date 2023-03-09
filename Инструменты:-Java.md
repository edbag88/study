# Java

 ![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-banner-1.jpg)

Java — многоплатформенный язык программирования общего назначения. Главная особенность Java заключается в том, что он работает по принципу WORA (write once, run anywhere — напиши один раз, запускай везде). Поэтому код, написанный на Java, можно запускать на любой платформе и любом устройстве с установленной средой исполнения кода.

На Java пишут веб-приложения, нагруженные финансовые сервисы, игры, мобильные приложения для Android, используют в научных вычислениях и при работе с большими данными. На Java можно написать практически всё, в том числе и автоматические тесты.

## Установка

### Windows
1. Проверить наличие уже установленной Java. Для этого необходимо открыть консоль Windows и ввести команду `java -version`. Если Java на компьютере нет, то переходим к следующему шагу;
2. Перейти на [сайт](https://www.oracle.com/cis/java/technologies/javase/jdk11-archive-downloads.html) Oracle и скачать последнюю актуальную версию для Windows. Сайт может попросить пройти регистрацию, но можно воспользоваться данными для входа с [этого сайта](https://bugmenot.com/view/oracle.com);
3. Открыть загруженный файл и пройти процесс установки;
4. В окне установщика необходимо скопировать путь к JDK, который понадобится для настройки окружения.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-1.png)

### Прописываем переменные среды
1. Правой кнопкой мыши щёлкнуть по иконке "Мой компьютер" на рабочем столе и выбрать пункт "Свойства" в меню;
2. Внизу страницы выбрать пункт "Дополнительные параметры системы";

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-2.png)

3. Нажать "Переменные среды";

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-3.png)

4. В разделе "Системные переменные" нажать кнопку "Создать";

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-4.png)

5. В поле "Имя переменной" ввести: JAVA_HOME;

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-5.png)

6. В поле "Значение переменной" ввести путь к папке с Java (его мы копировали во время установки);
7. Нажать "ОК", в следующем окне тоже нажать "ОК";
8. Перезагрузить компьютер;
9. Проверить установку с помощью команды `java -version` в консоли.

### OpenJDK

На территории РФ ресурсы Oracle блокируются, поэтому установка Java может быть затруднительной. Если инструкция выше не помогла скачать и установить Java, можно установить OpenJDK:

1. Загрузить файл по [ссылке](https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_windows-x64_bin.zip);
2. Открыть скаченный архив, распаковать и скопировать папку `jdk-11.0.2` на диск.

**Прописываем переменные среды**
1. Правой кнопкой мыши щёлкнуть по иконке "Мой компьютер" на рабочем столе и выбрать пункт "Свойства" в меню.
2. Внизу страницы выбрать пункт "Дополнительные параметры системы";
3. Нажать "Переменные среды";

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-2.png)

4. В разделе "Системные переменные" нажать кнопку "Создать";

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-3.png)

5. В поле "Имя переменной" ввести: JAVA_HOME;
6. В поле "Значение переменной" ввести путь к папке с OpenJDK (та папка, которую копировали на диск);

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Java/java-5.png)

7. Нажать "ОК", в следующем окне тоже нажать "ОК";
8. Перезагрузить компьютер;
9. Проверить установку с помощью команды `java -version` в консоли.

### macOS
1. Проверить наличие Java с помощью команды `java --version` в терминале. Если Java на компьютере нет, переходим к следующему шагу;
2. Перейти на [сайт](https://www.oracle.com/cis/java/technologies/javase/jdk11-archive-downloads.html) Oracle и скачать последнюю актуальную версию `macOS x64 DMG Installer`. Сайт может попросить пройти регистрацию, но можно воспользоваться данными для входа с [этого сайта](https://bugmenot.com/view/oracle.com).

### Прописываем переменные среды
1. Найти и скопировать путь, по которому установлена Java, обычно это `/Library/Java/JavaVirtualMachines/jdk-версияJava.jdk/Contents/Home`;
2. Перейти в домашнюю директорию пользователя с помощью команды `cd` в терминале;
3. Добавить в файл `.zshrc` скопированный путь. Редактировать файлы можно с помощью редактора Nano, открывается с помощью команды `nano [название файла]`;
4. Сохранить изменения;
5. Проверить установку с помощью команды `java --version` в терминале.



На macOS 10.5 и более поздних версиях Apple рекомендует установить переменную `$JAVA_HOME` в `/usr/libexec/javahome`. Для этого необходимо:

- Экспортировать `$JAVA_HOME` в файл `~/.bash_profile` или `~/.profile`:
``` bash
$ vim .bash_profile 

export JAVA_HOME=$(/usr/libexec/java_home)
export PATH=$JAVA_HOME/bin:$PATH
```

- Проверить установку в терминале:
```bash
$ source .bash_profile
$ echo $JAVA_HOME
```
- Результат должен быть следующим:
```bash
/Library/Java/JavaVirtualMachines/jdk1.8.0_73.jdk/Contents/Home
```
