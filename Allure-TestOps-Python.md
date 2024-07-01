
- [Allure TestOps Python](#allure-testops-python)
  - [Интеграция Jenkins и Allure TestOps](#интеграция-jenkins-и-allure-testops)
  - [Авторизация в Allure TestOps](#авторизация-в-allure-testops)
  - [Добавляем Allure TestOps в jenkins джобу](#добавляем-allure-testops-в-jenkins-джобу)
  - [Добавляем отображение проекта Allure TestOps в jenkins джобе](#добавляем-отображение-проекта-allure-testops-в-jenkins-джобе)
  - [Как подключить интеграцию и запуск джобы в Jenkins через Allure TestOps](#как-подключить-интеграцию-и-запуск-джобы-в-jenkins-через-allure-testops)
    - [Как узнать свой Username в Jenkins](#как-узнать-свой-username-в-jenkins)
    - [Как создать API token в Jenkins](#как-создать-api-token-в-jenkins)
  - [Как подключить интеграцию с Jira](#как-подключить-интеграцию-с-jira)
  - [Realtime reporting(Отчеты в режиме реального времени)](#realtime-reportingотчеты-в-режиме-реального-времени)
  - [Testcases(Тест-кейсы)](#testcasesтест-кейсы)
  - [Live documentation(Живая документация)](#live-documentationживая-документация)
    - [Единая точка правды](#единая-точка-правды)
  - [Фильтрация тест кейсов](#фильтрация-тест-кейсов)
  - [Как добавить отображение параметров запуска в Allure TestOps](#как-добавить-отображение-параметров-запуска-в-allure-testops)
  - [Ручные тест кейсы](#ручные-тест-кейсы)
  - [Как перенести ручной тест в код и работа с плагином Allure TestOps Support](#как-перенести-ручной-тест-в-код-и-работа-с-плагином-allure-testops-support)
    - [Создание токена для плагина Allure Testops Support](#создание-токена-для-плагина-allure-testops-support)
    - [Выбор проекта в плагине Allure Testops Support](#выбор-проекта-в-плагине-allure-testops-support)
  - [Как загрузить результаты прогона тестов в Allure TestOps после локального запуска тестов](#как-загрузить-результаты-прогона-тестов-в-allure-testops-после-локального-запуска-тестов)
  - [Как сравнить ручной и автоматизированный тест написанный с него](#как-сравнить-ручной-и-автоматизированный-тест-написанный-с-него)
  - [Как сделать rerun(повторный прогон) упавших тестов](#как-сделать-rerunповторный-прогон-упавших-тестов)
    - [Автоматический rerun](#автоматический-rerun)
    - [Ручной rerun](#ручной-rerun)
  - [Как запустить тесты в Allure TestOps](#как-запустить-тесты-в-allure-testops)
  - [Как завести дефект в Jira из Allure TestOps](#как-завести-дефект-в-jira-из-allure-testops)
  - [Как добавить в Jira тикет тест кейс и прогоны из Allure TestOps](#как-добавить-в-jira-тикет-тест-кейс-и-прогоны-из-allure-testops)
  



# Allure TestOps Python 

Allure TestOps — это TMS(тест-менеджмент система) для автоматизированных тестов. Она позволяет хранить тест-кейсы, запускать тесты и смотреть результаты их выполнения. Allure TestOps позволяет интегрироваться с различными фреймворками, такими как JUnit, TestNG, PyTest и интегрироваться с CI/CD системами, такими как Jenkins, TeamCity и другими. А также взаимодействовать с различными системами управления задачами, такими как Jira, Trello и другими.

Репозиторий с примером проекта можно найти [тут](https://github.com/eroshenkoam/allure-pytest-example).

## Интеграция Jenkins и Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Пример реализации самой простой "джобы" в jenkins с Allure TestOps:

1. Параметризованная сборка с параметрами `ENDPOINT` и `BROWSER`, и значением по умолчанию `https://testing.github.com` и `firefox`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_testops.jpeg)

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_testops_2.jpeg)

2. Отметка в чек боксе `Restrict where this project can be run` и указание значения `python` позволяет запускать тесты только там, где установлен Python(данная настройка нужна, только если у вас есть отдельные ноды(агенты) на разных языках программирования и вы хотите запускать тесты на ноде с Python).

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/label_jenkins.jpeg)

3. В блоке `Source Code Management` выбрать `Git`, указываем URL репозитория и ветку.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/git_jenkins.jpeg)

4. В блоке `Build Environment` выбрать `Delete workspace before build starts` (параметры очистки рабочего пространства).
   Это необходимо для того, чтобы перед каждым запуском тестов удалять старые файлы и не допускать их влияния на результаты тестирования.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/delete_workspace_jenkins.jpeg)

5. В блоке `Build Steps` указана команда запуска сборки тестов. Важно отметить, что в примере указано `|| true`, это нужно для того, чтобы джоба не падала при возникновении ошибок в тестах.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/command_jenkins.jpeg)

6. В блоке `Post-build Actions` указываем в разделе `Allure Report` путь до папки, по умолчанию `allure-results`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/allure_jenkins.jpeg)

</details>

## Авторизация в Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для авторизации в Allure TestOps необходимо ввести логин и пароль которые представлены в уроке. Регистрироваться самому НЕ НУЖНО.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/testops_login.jpeg)

</details>

## Добавляем Allure TestOps в jenkins джобу
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

1. Если не нужно отображение результатов прогона в Allure Results, то указываем отметку в чек боксе `Disabled` в разделе `Allure Report`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/allure_jenkins_disabled.jpeg)

2. В блоке `Build Environment` указываем отметку в чек боксе `Allure: upload results`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_allure_testops.jpeg)

3. В отобразившимся блоке `Allure TestOps` необходимо указать данные, а именно:

   - В строке `Server` в выпадающем списке выбираем `allure-server`
   - В строке `Project` в выпадающем списке выбираем название проекта, который был создан ранее, и к которому можно подключиться через `Allure TestOps`(отображение проекта в данном выпадающем списке описано ниже в разделе [Добавляем отображение проекта Allure TestOps в jenkins джобе](#добавляем-отображение-проекта-allure-testops-в-jenkins-джобе))
   - В строке `Launch Name` оставляем значение по умолчанию `${JOB_NAME} - #${BUILD_NUMBER}`
   - В строке `Launch tags` можно указать теги для прогона (это не обязательно)
   - В блоке `Results` кликаем на кнопку `Add results` и на таб `Results`. В отобразившемся блоке в строке `Path` указываем путь до папки с результатами тестов, по умолчанию `allure-results`.
   
4. Сохраняем изменения(кнопка `Save`). 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_allure_testops_2.jpeg)

</details>

## Добавляем отображение проекта Allure TestOps в jenkins джобе
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

1. Создаем проект в Allure TestOps. Для этого переходим в Allure TestOps и авторизируемся
2. На главной странице с `Projects` нажимаем на кнопку `Create new project`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/testops_create_project.jpeg)

3. В отобразившимся попапе заполняем данные:
   - В поле `Name` указываем название проекта
   - В поле `Description` указываем описание проекта (не обязательно)
   - Указываем отметку в чек боксе `Public` если хотим чтобы проект был доступен всем пользователям
   - Нажимаем на кнопку `Submit`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/create_project.jpeg)

4. В созданном проекте нажимаем на иконку шестеренки для перехода в настройки проекта.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/open_project.jpeg)

5. В настройках переходим на таб `Access`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/access_settings.jpg)

   - В блоке `Outside Collaborators` необходимо кликнуть на иконку `+` 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/outside_collaborators.jpg)

   - В отобразившемся попапе `Add collaborator` в выпадающем списке `Select a collaborator to grant permissions to` необходимо выбрать `jenkins_agent_service_acc`. А в выпадающем списке `Permission Set` выбрать `Project Write`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_collaborator.jpg)

   - Нажимаем на кнопку `Submit`

Конечный результат должен выглядеть так:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/last_result.jpg)

</details>

## Как подключить интеграцию и запуск джобы в Jenkins через Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

1. Для того чтобы джобу можно было запускать через Allure TestOps, необходимо в настройках проекта добавить интеграцию с Jenkins.
   - Переходим в настройки проекта на таб `Integrations`.
   - На странице `Integrations` в строке с названием `Jenkins` нажимаем на кнопку `Add integration`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/integrations_jenkins.jpg)

   - В отобразившемся попапе `Add Jenkins integration to project` заполняем данные:
     - В строке `Username` указываем юзернейм пользователя Jenkins
     - В строке `API token` указываем токен к аккаунту Jenkins
     - Нажимаем на кнопку `Test connection` и проверяем что все данные введены верно. Если всё верно указано, то отобразиться сообщение `Connection established`
     - Нажимаем на кнопку `Add integration`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/connection_jenkins_testops.jpg)

После добавления интеграции с Jenkins, в блоке `Added integrations` отобразиться информация о добавленной интеграции.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/added_integration.jpg)

2. После запуска джобы из Jenkins, джоба отобразиться в allure testops. Если необходимо настроить джобу, то нужно перейти в боковом меню на вкладку `Jobs`. 
Если в джобе есть параметризация и дефолтное значение для параметров не отображено в Allure TestOps, то необходимо в строке с джобой нажать на иконку со стрелками `Update job` и после обновления все параметры и их значения будут отображены.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_testops_job.jpg)

3. Если необходимо вручную добавить джобу в Allure TestOps, то необходимо перейти в боковом меню на вкладку `Jobs` и нажать на кнопку `New job`. 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_new_job.jpg)

В отобразившемся попапе `Create job` заполняем данные:
   - Кликнув на строку `Build server` выбираем из выпадающего списка адрес школьного сервера. 
   - Далее отображается дополнительное поле `Job`, и чек бокс `Can run tests`. Если необходимо запускать джобу через Allure TestOps, то необходимо отметить чек бокс `Can run tests`.
   - В строке `Job` кликаем на поле и из выпадающего списка ищем нужную джобу (данные в списке можно отфильтровать указав название джобы в строке поиска).
   - После добавления джобы отображается кнопка `Add parameter`, по клику на которую можно добавить параметры для джобы.
   - Нажимаем на кнопку `Submit`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_job.jpg)

После сохранения, джоба отобразится в списке джоб в Allure TestOps в блоке `Jobs`.

### Как узнать свой Username в Jenkins

Для того чтобы узнать свой `Username` необходимо перейти в Jenkins.
 - Для отображения `Username` необходимо кликнуть в верхнем правом углу на свой профиль.
 - На вкладке `Status` можно увидеть `User ID`, это и есть ваш `Username`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/username_jenkins.jpg)

### Как создать API token в Jenkins

Для того чтобы создать свой `API token` необходимо перейти в Jenkins.
 - В боковом меню выбираем `Configure`
 - В блоке `API Token` нажимаем на кнопку `Add new Token`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/api_token.jpg)

 - После, отобразиться поле ввода для ввода названия токена(имя может быть любым) и кнопка `Generate`. Вводим название токена и нажимаем на кнопку `Generate`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/api_create_token.jpg)

 - Далее отобразиться токен, который необходимо скопировать и вставить в поле `API token` в Allure TestOps.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/token_number.jpg)

</details>

## Как подключить интеграцию с Jira
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

1. Для того чтобы добавить интеграцию с Jira, необходимо:
   - Переходим в настройки проекта на таб `Integrations`.
   - На странице `Integrations` в строке с названием школьной `Jira` нажимаем на кнопку `Add integration`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jira_integration.jpg)

   - В отобразившемся попапе `Add jira integration to project` заполняем данные:
     - В строке `Username` указываем юзернейм пользователя Jira (данные отображены в уроке)
     - В строке `Password` указываем пароль к аккаунту Jira (данные отображены в уроке)
     - Нажимаем на кнопку `Test connection` и проверяем что все данные введены верно. Если всё верно указано, то отобразиться сообщение `Connection established`
     - Нажимаем на кнопку `Add integration`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jira_connect.jpg)

После добавления интеграции с Jira, в блоке `Added integrations` отобразиться информация о добавленной интеграции.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/added_integration_jira.jpeg)

</details>

## Realtime reporting(Отчеты в режиме реального времени)
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Allure TestOps позволяет в реальном времени отслеживать результаты выполнения тестов. При этом можно видеть какие тесты были запущены, какие прошли успешно, а какие нет. Также можно видеть сколько времени занял прогон тестов и сколько времени занял каждый тест.

Пример отображения результатов тестов в Allure TestOps(общий результат прогона(он отображается если запустить прогон тестов в Jenkins)):

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/realtime_reporting.jpeg)

Пример отображения результатов тестов в Allure TestOps(подробное отображение по каждому тесту(шаги, скриншоты, логи, время выполнения и т.д.)):

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/launches.jpeg)

</details>

## Testcases(Тест-кейсы)
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для того чтобы получить/сгенерировать тест-кейсы в Allure TestOps из прогонов тестов, то необходимо закрыть `Launch`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/close_launches.jpeg)

После этого необходимо перейти в боковом меню на вкладку `Test cases`. В данном разделе можно создавать тест-кейсы, редактировать их, удалять и просматривать.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/test_cases.jpeg)

</details>

## Live documentation(Живая документация)
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Если правильно разметить тесты, то можно получить живую документацию. Для этого необходимо в тестах использовать аннотации, которые позволяют описывать тесты. После этого в Allure TestOps можно увидеть документацию по тестам.
При малейших изменениях в тестах, документация автоматически обновляется.

### Единая точка правды

Единая точка правды это когда у всех членов команды есть доступ к актуальной информации. Если вы работаете с авто тестами, то единая точка правды это авто тесты. Все изменения в авто тестах отображаться в документации и таким образом все члены команды будут видеть актуальную информацию.

</details>

## Фильтрация тест кейсов
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для отображения панели фильтрации тест кейсов необходимо нажать на кнопку `Filter` .

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/filter_test_cases.jpeg)

После этого отобразиться панель фильтрации, в которой можно выбрать нужные фильтры для отображения тест кейсов.

Пример фильтрации по тегам:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/filter_test_cases_2.jpeg)

</details>

## Как добавить отображение параметров запуска в Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для добавления параметров запуска в Allure TestOps необходимо перейти в настройки проекта `Settings` и перейти на таб `Environment `.

Далее на странице `Environment schemas settings` кликнуть на кнопку `Create`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/environment_settings.jpeg)

В отобразившихся полях необходимо заполнить данные для добавления эндпоинта(где тестируется приложение(ссылка на сайт)):
   - В строке `Mapping Key` указываем название переменной параметра, к примеру `ENDPOINT` или `URL`(данные переменные должны совпадать с переменными в Jenkins)
   - В выпадающем списке `Environment variable` выбираем значение для переменной, к примеру `HOST`.
   - Кликаем на кнопку `Submit`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/host_variable.jpeg)

Для добавления других параметров запуска необходимо повторить действия для каждого параметра.
К примеру для добавления параметра `BROWSER`:
   - В строке `Mapping Key` указываем название переменной параметра, к примеру `BROWSER`.
   - В выпадающем списке `Environment variable` выбираем значение для переменной, к примеру `Browser`.
   - Кликаем на кнопку `Submit`

Пример добавления отображения параметров запуска в Allure TestOps:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_environment.jpeg)

Если необходимо добавить другие параметры, к примеру `Custom Fields`, `Test Layers` или `Tree`, то необходимо повторить подобные действия как описаны ранее для добавления параметров.

К примеру в блоке `Test Layers` можно добавить разметку для указания какие тесты относятся к какому слою тестирования(например `UI`, `API`, `Integration` и т.д.).

</details>

## Ручные тест кейсы
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для добавления/создания ручных тест кейсов необходимо в боковом меню перейти на вкладку `Test cases`. И в строке с подсказкой для ввода(плейсхолдер) `Add a new test case` ввести название тест кейса и нажать на кнопку `Enter`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_manual_test_case.jpg)

Добавленный ручной тест кейс отобразится в списке тест кейсов с иконкой `руки`, при наведении на которую отображается текст `manual`. 
Автоматизированные тест кейсы отображаются с иконкой в виде робота, при наведении на которую отображается текст `automated`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/manual_test_case.jpeg)

Для редактирования ручного тест кейса необходимо кликнуть на тест кейс и в правой части отобразиться панель редактирования тест кейса.
Если необходимо добавить шаги, то необходимо в строке `Scenario` кликнуть на кнопку карандаша и в отобразившемся поле ввести шаги тест кейса.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_steps.jpg)

Если необходимо сделать шаг в шаге, то необходимо в строке с шагом нажать на иконку три точки и выбрать `Indent`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_steps_more_details.jpg)

После добавления шагов необходимо нажать на кнопку `Submit`.

</details>

## Как перенести ручной тест в код и работа с плагином Allure TestOps Support

<details><summary><b>Нажать, чтобы раскрыть</b></summary>

После создания ручного тест кейса, можно перенести его в код. Для этого необходимо для начала установить плагин `Allure TestOps Support`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/plugin_testops.jpeg)

Далее необходимо перейти в настройки(Settings) Pycharm в раздел `Tools` и кликнуть на `Allure TestOps Support`.
В отобразившемся окне в блоке `Connection` в строке `Endpoint` указать адрес сервера Allure TestOps(урл адрес школьного сервера), а в строке `Token` указать токен к аккаунту Allure TestOps.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/data_plugin_testops.jpeg)

### Создание токена для плагина Allure Testops Support

Для создания токена для плагина Allure TestOps Support необходимо перейти в Allure TestOps и авторизоваться.
 - В нижней части страницы кликнуть на иконку пользователя и в выпадающем списке выбрать `Your profile`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/profile_testops.jpeg)

 - На открывшейся странице в блоке `API tokens!` проскролить до кнопки `Create` и кликнуть на неё.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/api_token_testops.jpeg)

 - В отобразившемся попапе в строке `Name` указать название токена(название может быть любым). После этого кликнуть на кнопку `Submit`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/token_name.jpg)

 - После создания токена, необходимо скопировать его и вставить в поле `Token` в Pycharm.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/token_created.jpeg)

При правильном указании данных в плагине, в Pycharm отобразиться сообщение `Logged in as ...`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/testops_pycharm.jpeg)

### Выбор проекта в плагине Allure Testops Support

Необходимо перейти в настройки(Settings) Pycharm в раздел `Tools` и кликнуть на стрелку в строке `Allure TestOps Support`.
Кликнуть на таб `Project Settings`, в строке `Project` выбрать нужный проект из выпадающего списка. После выбора проекта, необходимо нажать на кнопку `OK`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/project_testops.jpeg)


Далее необходимо в коде создать тест, который будет соответствовать ручному тесту кейсу. Для этого необходимо создать файл с тестом и в нем создать тест, который будет соответствовать ручному тесту кейсу.

Пример кода теста:

```python
def test_example():
    pass
    
```

После создания теста, необходимо в Pycharm кликнуть правой кнопкой мыши на тест и в выпадающем списке выбрать `Allure TestOps: Imoprt test case`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/tets_case_pycharm.jpeg)

В отобразившемся поп-апе `Automate Test Case` в строке `Test Case ID` необходимо указать ID ручного тест кейса (id ручного тест кейса который был создан ранее в Allure TestOps показан в блоке данной статьи [Ручные тест кейсы](#ручные-тест-кейсы)). Остальные значения можно оставить по умолчанию и нажать на кнопку `OK`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/import_test_case_id.jpeg)

После тест кейс и разметка будет импортирована в код и отобразится в Pycharm.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/test_annotation.jpeg)

</details>

## Как загрузить результаты прогона тестов в Allure TestOps после локального запуска тестов
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

После прогона тестов локально появляется папка `allure-results`, в которой находятся результаты прогона тестов. 
Для того чтобы загрузить результаты прогона тестов в Allure TestOps необходимо кликнуть правой кнопкой мыши на папку `allure-results` и в выпадающем списке выбрать `Allure TestOps: Upload results`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/upload_results.jpeg)

В появившемся поп-апе `Upload Results to Allure` в строке `Please provide a laungh name` отображено дефолтное название для прогона тестов которое сгенерировано согласно дате и времени загрузки результатов. Если необходимо изменить название прогона, то необходимо ввести новое название. После этого нажать на кнопку `OK`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/pop_up_results_upload.jpeg)

После загрузки результатов прогона тестов в Allure TestOps, в Pycharm отобразиться сообщение `We successfully uploaded 1 files in 1 seconds`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/message_upload.jpeg)

В Allure TestOps в разделе `Launches` отобразиться новый прогон тестов.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/launches_test.jpeg)

Если закрыть прогон `Launches`, то в разделе `Test cases` иконка ручного тест кейса(из которого был сгенерирован автоматический тест) изменится на иконку робота, что означает что тест кейс автоматизирован.

</details>

## Как сравнить ручной и автоматизированный тест написанный с него
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для того чтобы сравнить ручной тест кейс и автоматизированный тест необходимо перейти в Allure TestOps в раздел `Test cases`.
Найти ручной тест кейс который созданный ранее(описано в разделе [Ручные тест кейсы](#ручные-тест-кейсы)) и кликнуть на его название.

В отобразившемся окне с ручным тест кейсом в строке `Scenario` кликнуть на иконку `Compare scenario`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/compare_scenario.jpg)

После клика отображается поп-ап в котором можно сравнить ручной тест кейс и автоматизированный тест. Слева отображается ручной тест кейс, а справа автоматизированный тест.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/compare_scenario_2.jpg)
</details>

## Как сделать rerun(повторный прогон) упавших тестов
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

### Автоматический rerun
Для этого необходимо перейти в раздел `Launches`. Открыть прогон.
На вкладке `Tree` отобразиться дерево тестов. В дереве тестов можно увидеть упавшие тесты(красным цветом).
Отметить в чек боксе упавшие тесты и нажать на кнопку с файлом.
Далее в выпадающем списке выбрать `Rerun`. 
> **Важно!** В списке будет отображаться `Rerun` только если прогон не закрыт.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/rerun_tests.jpeg)

### Ручной rerun
Для этого необходимо перейти в раздел `Launches`. Открыть прогон.
На вкладке `Tree` отобразиться дерево тестов. В дереве тестов можно увидеть упавшие тесты(красным цветом).
Кликнуть на название упавшего теста и в отобразившемся окне кликнуть на кнопку `Rerun manually`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/rerun_manually.jpeg)

Далее отобразиться в каждой строке с шагами теста две кнопки `Fail`(иконка крестика) и `Pass`(иконка галочки).
Необходимо пройти по каждому шагу и выбрать `Fail` или `Pass` в зависимости от результата выполнения шага. После этого нажать на кнопку `Fail` или `Pass` в нижней строке.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/rerun_manually_2.jpg)

</details>

## Как запустить тесты в Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для запуска тестов есть несколько способов:

1. Запуск тестов из вкладки `Test cases`. 

Для этого необходимо перейти на вкладку `Test cases`. Отметить тесты которые необходимо запустить и нажать на иконку с файлом.
В выпадающем списке выбрать `Run`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/run_tests.jpeg)

2. Запуск тестов из вкладки `Jobs`.

Для этого необходимо перейти на вкладку `Jobs`. 
Кликнуть на иконку стрелки в строке с джобой. 
В отобразившимся поп-апе выбрать нужные тест кейсы отметив в чек боксах отметку(по умолчанию отмечены все), также если необходимо можно выбрать параметры для запуска тестов и же задать специальное название для прогона. После этого нажать на кнопку `Submit`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/run_tests_job.jpeg)

По умолчанию название прогона будет сгенерировано автоматически( а именно как `Launch at дата время`).

</details>

## Как завести дефект в Jira из Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

Для того чтобы завести дефект в Jira из Allure TestOps необходимо:
* Должна быть настроена интеграция с Jira(описано в разделе [Как подключить интеграцию с Jira](#как-подключить-интеграцию-с-jira))

1. Для этого необходимо перейти в раздел `Launches`. Открыть прогон в котором упал тест.
2. На вкладке `Tree` отобразиться дерево тестов. В дереве тестов можно увидеть упавшие тесты(красным цветом).
3. Открыть упавший тест и в отобразившемся окне кликнуть на кнопку `Link defect`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/create_bug.jpeg)

4. Далее в отобразившимся поп-апе указать название дефекта и нажать `Create название дефекта`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/create_bug_2.jpeg)

5. В поп-апе `Link defect` указать `Description`. В блоке `Issue` нажать на кнопку `Create issue`. 
В отобразившихся полях указать данные для создания дефекта в Jira:
   - В строке `Tracker` выбрать интеграцию с Jira.
   - В строке `Project` выбрать проект в Jira.
   - В строке `Issue type` указать тип дефекта.
   - В строке `Тема` указать название дефекта которое будет отображено в Jira.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/create_bug_3.jpeg)

6. Если данный дефект часто встречается, то можно создать шаблон для дефекта. 
Для этого необходимо в поп-апе `Link defect` в блоке `Automation rule` нажать на кнопку `Create automation rule`.

В отобразившихся полях указать данные для создания шаблона:
   - В строке `Rule name` указать название шаблона.
   - В строке `Error message pattern` указать шаблон для ошибки.
   - В строке `Stack trace pattern` указать шаблон для стека.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/create_bug_4.jpeg)

7. Далее необходимо нажать на кнопку `Link defect`.

Созданный дефект отобразиться в нескольких местах:
   - В разделе `Launches` в прогоне в котором упал тест.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/linked_defects.jpeg)

   - В разделе `Launches` где отображены все прогоны.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/linked_defects_2.jpeg)

   - В разделе `Defects`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/defects.jpeg)

Если данный дефект связан с другими падениями тестов, то данный можно прилинковать с другими тестами.

Для этого необходимо в разделе `Launches` открыть прогон в котором упали тесты.
На вкладке `Tree` отобразиться дерево тестов. В дереве тестов можно увидеть упавшие тесты(красным цветом).
Указать в чек боксах тесты которые связаны с дефектом и нажать на кнопку с файлом.
В выпадающем списке выбрать `Link defect`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/link_defects.jpeg)

Далее в поп-апе указать название дефекта или же выбрать из списка и нажать `Link defect`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/link_defects_2.jpeg)

</details>


## Как добавить в Jira тикет тест кейс и прогоны из Allure TestOps
<details><summary><b>Нажать, чтобы раскрыть</b></summary>

### Добавление тест кейсов в Jira
Для того чтобы добавить тест кейс в Jira необходимо сделать шаги:
1. Должна быть настроена интеграция с Jira(описано в разделе [Как подключить интеграцию с Jira](#как-подключить-интеграцию-с-jira))
2. Должны быть созданы/сгенерированы тест кейсы в Allure TestOps(описано в разделе [Testcases(Тест-кейсы)](#testcasesтест-кейсы))
3. Должен быть создан тикет в Jira.

Для того чтобы добавить тест кейс в Jira необходимо:
   - В TestOps перейти в раздел `Test cases`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/testops_tab_test_casess.jpeg)

   - Поставить отметку в чек боксе у тест кейса который необходимо добавить в Jira.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/mark_test_cases.jpeg)

   - Кликнуть на кнопку `Bulk actions` и в выпадающем списке выбрать `Add issues`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/bulk_actions.jpeg)

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_issues.jpeg)

   - В поп-апе `Add issues` кликнуть на выпадающий список в строке `Issue Tracker` и выбрать сервер школьного Jira.
   - Кликнуть на выпадающий список в строке `Key` и выбрать тикет в который необходимо добавить тест кейсы.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_isues.jpeg)

   - После выбора тикета он будет отображен в строке в поп-апе `Add issues`. Нажать на кнопку `Submit`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/submit_test_cases.jpeg)

   - Добавление тикета в Jira отобразиться в каждом тест кейсе при его раскрытии.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/test_case_link.jpeg)


### Добавление прогонов в Jira

Для того чтобы добавить тест кейс в Jira необходимо сделать шаги:
1. Должна быть настроена интеграция с Jira(описано в разделе [Как подключить интеграцию с Jira](#как-подключить-интеграцию-с-jira))
2. Должны быть созданы/сгенерированы прогоны в Allure TestOps(описано в разделе [Как подключить интеграцию и запуск джобы в Jenkins через Allure TestOps](#как-подключить-интеграцию-и-запуск-джобы-в-jenkins-через-allure-testops))
3. Должен быть создан тикет в Jira.

Для того чтобы добавить прогон в Jira необходимо:
   - В TestOps перейти в раздел `Launches`.
   - В строке с прогоном который необходимо добавить в Jira кликнуть на кнопку `три точки`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/launces_add.jpeg)

   - В отобразившемся выпадающем списке выбрать `Link to an issue`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/link_issue.jpeg)

   - В поп-апе `Link launch to issue` кликнуть на выпадающий список в строке `Issue Tracker` и выбрать сервер школьного Jira.
   - Кликнуть на выпадающий список в строке `Key` и выбрать тикет в который необходимо добавить тест кейсы.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_launch.jpeg)

   - После выбора прогона он будет отображен в строке в поп-апе `Link launch to issue`. Нажать на кнопку `Submit`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/submit_add.jpeg)

   - После добавления прогона в Jira, в разделе `Launches` в строке с прогоном отобразиться линк на тикет в Jira.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/added_issues.jpeg)




</details>