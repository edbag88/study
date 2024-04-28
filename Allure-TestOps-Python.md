
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
    - [Создание токена для плагина Allure TestOps Support](#создание-токена-для-плагина-allure-testops-support)


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

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/access_settings.jpeg)

   - В блоке `Outside Collaborators` необходимо кликнуть на иконку `+` 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/outside_collaborators.jpeg)

   - В отобразившемся попапе `Add collaborator` в выпадающем списке `Select a collaborator to grant permissions to` необходимо выбрать `jenkins_agent_service_acc`. А в выпадающем списке `Permission Set` выбрать `Project Write`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_collaborator.jpeg)

   - Нажимаем на кнопку `Submit`

Конечный результат должен выглядеть так:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/last_result.jpeg)

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

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_manual_test_case.jpeg)

Добавленный ручной тест кейс отобразится в списке тест кейсов с иконкой `руки`, при наведении на которую отображается текст `manual`. 
Автоматизированные тест кейсы отображаются с иконкой в виде робота, при наведении на которую отображается текст `automated`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/manual_test_case.jpeg)

Для редактирования ручного тест кейса необходимо кликнуть на тест кейс и в правой части отобразиться панель редактирования тест кейса.
Если необходимо добавить шаги, то необходимо в строке `Scenario` кликнуть на кнопку карандаша и в отобразившемся поле ввести шаги тест кейса.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_steps.jpeg)

Если необходимо сделать шаг в шаге, то необходимо в строке с шагом нажать на иконку три точки и выбрать `Indent`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_steps_more_details.jpeg)

После добавления шагов необходимо нажать на кнопку `Submit`.

</details>

## Как перенести ручной тест в код и работа с плагином Allure TestOps Support

<details><summary><b>Нажать, чтобы раскрыть</b></summary>

После создания ручного тест кейса, можно перенести его в код. Для этого необходимо для начала установить плагин `Allure TestOps Support`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/plugin_testops.jpeg)

Далее необходимо перейти в настройки(Settings) Pycharm в раздел `Tools` и кликнуть на `Allure TestOps Support`.
В отобразившемся окне в блоке `Connection` в строке `Endpoint` указать адрес сервера Allure TestOps(урл адрес школьного сервера), а в строке `Token` указать токен к аккаунту Allure TestOps.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/data_plugin_testops.jpeg)

### Создание токена для плагина Allure TestOps Support

Для создания токена для плагина Allure TestOps Support необходимо перейти в Allure TestOps и авторизоваться.
 - В нижней части страницы кликнуть на иконку пользователя и в выпадающем списке выбрать `Your profile`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/profile_testops.jpeg)

 - На открывшейся странице в блоке `API tokens!` проскролить до кнопки `Create` и кликнуть на неё.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/api_token_testops.jpeg)

 - В отобразившемся попапе в строке `Name` указать название токена(название может быть любым). После этого кликнуть на кнопку `Submit`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/token_name.jpeg)

 - После создания токена, необходимо скопировать его и вставить в поле `Token` в Pycharm.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/token_created.jpeg)

</details>